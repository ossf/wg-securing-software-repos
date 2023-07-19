# Build Provenance and Code-signing for Homebrew

Authors: [William Woodruff](https://github.com/woodruffw), [Dustin Ingram](https://github.com/di)

## Summary

The document contains a technical proposal for introducing build provenance and cryptographic signatures to the Homebrew package manager. The end goal is to improve Homebrew's authenticity and supply-chain integrity properties, establishing that a given package was both built from an attested source artifact as well as on an attested machine (i.e., a Homebrew-controlled GitHub Actions workflow).

The proposal is broken up into individual technical items, which are meant to be semi-independent units of work. The units of work are ordered by dependency relationship; i.e. signature generation must come before any signatures can be verified on the client side.

## Technical Background

[Homebrew](https://brew.sh/) is the predominant package manager for macOS, with millions of daily users and [hundreds of active contributors](https://github.com/Homebrew/brew/graphs/contributors). Homebrew is written in Ruby, and uses GitHub Actions to create binary packages (called "[bottles](https://docs.brew.sh/Bottles)") of popular open source projects, which clients then install on their machines via the `brew` CLI. Homebrew successfully delivers [over 400 million](https://formulae.brew.sh/analytics/install/365d/) binary builds of open source packages to macOS users each year.

[Sigstore](https://www.sigstore.dev/) is a Linux Foundation project aimed at making codesigning available to everybody. It uses a combination of open standards (OpenID Connect, WebPKI, Certificate Transparency) to bind non-cryptographic identities (such as emails or GitHub Actions workflow identities) to short-lived signing keys, which can then be used to sign for artifacts much like `gpg` or any other signing tool.

[SLSA](https://slsa.dev) is a set of incrementally adoptable guidelines for supply chain security, established by industry consensus, as well as a specification for attesting to the usage of these best practices in a verifiable way. The specification set by SLSA is useful for both software producers and consumers: producers can follow SLSA's guidelines to make their software supply chain more secure, and consumers can use SLSA to make decisions about whether to trust a software package.

## Technical Items

### Provenance attestations and signatures for official Homebrew taps

Homebrew's packaging processes are built around GitHub Actions. In particular, Homebrew uses GitHub Actions to perform builds of all core formulae (package specifications, like LLVM, `bash`, or `git`) into bottles (binary distributions that can be installed on client machines, similar to an `.app` or `.pkg`). Bottles are then hosted on GitHub Packages (or other hosts, for third-party taps) and are installed by end-user clients e.g. during `brew install` invocations.

Because Homebrew uses GitHub Actions for all `homebrew-core` builds, the Homebrew CI has trivial access to GitHub Actions' [ambient OpenID Connect identities](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect). These identities can in turn be used to generate build provenance and sign with Sigstore, meaning that Homebrew's existing CI workflows would require relatively little additional configuration (and zero external key management) to produce valid SLSA attestations and Sigstore signatures for each bottle build.

The high-level flow for bottle signing:

1. Existing bottle-building workflows will gain a signing step, which will only run as a finalization step for bottles that appear on `master` (i.e., not just the temporary bottles that are built as part of the normal PR lifecycle).
2. The signing step is responsible for producing an attestation with a Sigstore signature that _attests_ to the bottle. This signed attestation should include, at minimum, the bottle archive's SHA256 digest and the bottle's filename. The digest is necessary to produce a proof that the signature is for a particular bottle's contents, and the filename is necessary to produce a proof that the signature is intended to accompany a particular install step (i.e. `brew install foo` should not verify if an attacker substitutes `foo`'s bottle for a correctly signed bottle of `bar`, or even a different version of `foo` than the resolver produces). The attestation will follow the [in-toto format](https://github.com/in-toto/attestation/tree/main/spec/v1) and thus will be consistent with [SLSA's attestation model](https://slsa.dev/attestation-model).
3. The signing step is responsible for uploading the resulting signature to the same object storage as the bottle, and ensuring that the uploaded signature is addressable in a predictable and publicly derivable manner from just the formula and bottle's own metadata, [consistent with SLSA's guidenlines on distributing provenance](https://slsa.dev/spec/v1.0/distributing-provenance). In other words: a client that knows how to access the bottle's resource should also be able to access the bottle's signature resource with no additional metadata, similar to how [signature location and management](https://docs.sigstore.dev/cosign/signing_with_containers/#signature-location-and-management) works for signing container images with Sigstore.

At the end of this flow, both the bottle and its attestation with signature should appear in the tap's associated object storage.

In addition to signing for bottles as they're produced, the signing step may be used to "backfill" signatures (and corresponding attestations) for pre-existing bottles. These signatures would effectively act as notarizations for pre-existing bottles, rather than guarantees of build provenance. This "backfill" stage is expected to produce an initial attestation and signature for every pre-existing bottle, after which it will be removed and supplanted by signing during the bottle-building workflows. Removal of the "backfill" functionality after the initial backfill operation ensures that all subsequent attestations have corresponding build provenances.

Once a tap has been fully signed for (i.e., all referenced bottles have either a "backfill" or build attestation), the tap must establish a piece of "flag day" metadata: the tap should designate a timestamp `T`, after which all bottles defined by formulae in the tap are signed. This fundamentally requires that the tap itself is honest about its flag day: an attacker who can replace the tap's flag day can perform a downgrade by disabling signature verification. This is no different in scope from Homebrew's existing threat model, where an attacker must not be allowed to modify files in a tap. In other words: this signing scheme only protects the bottles themselves, not the tap's repository; the tap's repository must continue to be protected as a matter of policy.

### Sigstore signatures for third-party taps

While not in scope for this proposal, this work would also enable signing for third-party taps, such as those maintained by independent open source organizations or companies.

For third-party taps hosted on GitHub, the signing flow would be identical: any bottle-building workflow (including reusing the official one) would sign for bottles.

## Client-side signature verification in Homebrew

The Sigstore signatures described above are submitted to each tap's object storage so that they can be verified by clients during the normal `brew install` flow.

To verify a Sigstore signature, a particular `brew` client needs the following:

- A trust proposition, i.e. a reason to trust the identity producing the signature. For Homebrew, this trust proposition comes from the tap's own identity: the act of performing `brew tap foo/bar` establishes that Sigstore identities tied to `github.com/foo/bar` can be trusted to sign for bottles in that tap. This applies to implicit `brew tap` invocations as well, e.g. `brew install foo/bar/baz` asserts that the user expects a signature on `baz` from the `foo/bar` GitHub identity.
    - In the interest of simplicity, this proposal limits tap identities to just GitHub Actions identities, as these are "intrinsic" to the tap itself and therefore require no additional user trust decisions. Future extensions to this scheme may extend tap identities to include email, user, or other identity types supported by Sigstore.
- A Sigstore client library capable of verifying Sigstore signatures.

Client-side verification of bottles requires `brew` to know which bottles are actually signed. Clients should use the "flag day" metadata above to establish this: `brew install` should refuse to install any unsigned bottle from a tap that both had a flag day _and_ whose flag day is before the local system time.

The high-level flow for bottle signature verification, at tap time:

- A user performs either an explicit tap (`brew tap foo/bar`) or an implicit tap (`brew install foo/bar/baz`), and the local `brew` client establishes a trust proposition based on that action ("bottles from `foo/bar` must be signed by the `foo/bar` identity").
- The local `brew` client looks for the "flag day" metadata and, if present and before the local system time, enforces signature verification for all bottles referenced by the tap.

And at `brew install` time:

- For each bottle resolved during a `brew install` invocation, the bottle must have an accompanying signature. If the accompanying signature is not present, then `brew install` must fail.
- For each bottle and signature, `brew install` must internally reconstruct the _attestation_ described in the signing process above. This is then used as the cleartext input for signature verification. This input is then passed into the underlying Sigstore client along with its associated signature; the Sigstore client is responsible for performing both the signature verification and its associated identity verification.
- If the underlying signature verification fails, then `brew install` must fail.

Like with previous Homebrew features, an experimental feature-flagged variant of signature verification may be merged and enabled before it is enabled by default.

## Full source and build provenance for Homebrew

Bottle signing and subsequent verification unlocks a potential subsequent improvement: because Homebrew performs source builds to produce bottles, Homebrew could also verify signatures for those source artifacts. That signature could then be _countersigned_ for by Homebrew's own bottle signatures, effectively producing a strong cryptographic association from the original source artifact (produced by a third-party upstream) to the Homebrew-produced binary artifact.

Verifying each formula's source artifact requires each formula to carry or derive additional metadata about the identity trusted to sign for that artifact, in a manner similar to the "trust proposition" described under client-side verification. This, in turn, will require changes to Homebrew's formula DSL.

One _potential_ DSL modification for this metadata is shown below:

```ruby
class Ripgrep < Formula
  desc "Search tool like grep and The Silver Searcher"
  homepage "https://github.com/BurntSushi/ripgrep"
  url "https://github.com/BurntSushi/ripgrep/archive/13.0.0.tar.gz"

  # OPTION 1:
  # verifies using the default `#{url}.sigstore` bundle above
  # with the identity and issuer for the repo
  sigstore :default

  # OPTION 2:
  # verifies using the provided bundle/identity/issuer
  sigstore do
    # specifies the signature's URL
    bundle "https://<...>.sigstore"
    # the expected signature identity, e.g. an email or GitHub slug
    identity "<...>"
    # (optionally) the expected OIDC issuer
    oidc_issuer "<...>"
  end
end
```

For source artifacts hosted on GitHub and provided (along with their signatures) through GitHub releases, the first option will be sufficient: Homebrew can re-derive the expected signing identity from the `url`'s `user/repo` component.

For source artifacts hosted on other services (or that are signed with a non-GitHub-Actions identity), the second option allows the formula to explicitly specify the signature's URL and associated identity.

For formulae with verifiable source artifacts, the signed bottle attestation described above can be extended to include the verified source signature, resulting in a countersignature. This countersignature can be verified by `brew` (through a Sigstore client) using the same basic client-side signature verification process described in the task above, making this a progressive enhancement to "bottle-only" signatures.

## Compatibility considerations

### macOS executable code signing

Because this proposal only concerns bottles and not their individual executable members, it should have no effect on Homebrew's current use or any future uses of "ad-hoc" executable signatures (which are produced not for authenticity, but because macOS on Apple Silicon requires all executables to be signed).
