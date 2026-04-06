# Binary Transparency for Artifact Registries

Authors: [Hayden Blauzvern (Google)](https://github.com/haydentherapper)

Last updated: September 2024

This document defines Binary Transparency for artifacts registries to mitigate the risk of registry compromise by external attackers or insiders.

## What is Binary Transparency?

[Binary Transparency](https://binary.transparency.dev/) (BT) is a security solution that adds cryptographic immutability and discoverability to package identifiers and metadata, which in turn prevents tampering of existing versions and supports detection of unauthorized new versions.

BT is backed by a cryptographic data structure that is immutable and append-only. When publicly accessible, this structure becomes a transparency log, providing transparency into every committed decision present in the log. Each entry into the log receives an inclusion proof, a cryptographically verifiable confirmation of the inclusion of the entry, which is checked during artifact verification.

In the context of artifact registries, BT provides an assurance that all users always receive the same binary for a given package identifier, because users require the registry to transparently commit to all binaries it serves. If a registry is compromised or compelled to serve a different binary, then it must do so for all of its users and for all time, and because this decision must be recorded in a public transparency log, the malicious action can be audited and detected.

## Applying Binary Transparency to Artifact Registries

BT applies to any package distribution method using logically immutable package identifiers[^1]. This includes most OSS package ecosystems, such as Go, PyPI (Python), Cargo (Rust), npm (JavaScript), Maven Central (Java), and CI/CD registries such as GitHub Releases[^2]. In other words, users identify and fetch a package by `<package_name>`, `<version_id>`, and `<filename>` (or similar), referred to as a package identifier, and receive back some artifact. Logically, this process should *always* and *globally* return the same artifact[^3]. However, most ecosystems lack sufficient cryptographic security controls to ensure that this always occurs, making them susceptible to tampering by compromised registries, mirrors, or distribution channels. This is where BT fits in.

BT makes package identifiers immutable and transparent:

* A package registry will publish a commitment that a specific package identifier maps to a cryptographic digest. This commitment creates an immutable mapping between the identifier and digest. The mapping can only be done per package identifier and can never be updated or deleted.  
  * At upload time, the producer verifies that the entry was recorded correctly.  
  * At download time, the consumer verifies that the artifact they received matches the digest found in the log through an offline cryptographic inclusion proof.  
* Since the BT log is public, the mapping is publicly auditable.  
  * Artifact producers will verify that the log only contains artifacts they've released.  
  * Third-party auditors will verify that there exists only one instance of a cryptographic hash per package identifier.

## Threats Mitigated by Binary Transparency

BT mitigates threats associated with registry or mirror compromise or compulsion to serve a malicious artifact. Specifically:

### Tampering of existing versions

The threat is that a client requests a package by its immutable package identifier, but receives an artifact that does not correspond to the artifact the producer originally uploaded. This tampering can occur not only from the registry, but also from a mirror, network-level interference, or from storage.

BT prevents this completely. Once an identifier has been committed to the registry, clients only accept that corresponding digest. A producer can prevent the registry from tampering with the artifact at upload time by requiring proof that the digest has been committed to the BT log correctly, and a consumer must not accept an artifact without verifying the inclusion proof.

### Unauthorized publication of new versions

The threat is that the client asks the registry for the latest version and gets back a version identifier that the producer did not actually publish. For example, if the latest legitimate version of a given package is 1.0.0, a compromised registry might return 1.0.1 with malicious content.

BT does not prevent this threat outright, but makes this type of attack discoverable since the malicious action must be committed to a log. In this example, the malicious artifact could be discovered by a producer that is monitoring the BT log for new instances of their artifact. We recognize that monitoring could require active participation from all artifact maintainers and that there are current gaps in tooling[^4], but we believe that forcing malicious behavior to be publicly auditable acts as a significant deterrent against such behavior and provides non-repudiation for the registry's actions.

In conjunction with a secure update framework such as [The Update Framework](https://theupdateframework.io/) (TUF), artifact updates could be made transparent, immutable, and impossible to rollback or forward without discovery by a producer.

### Covert publication of malicious versions

The threat is that a producer is compelled to produce multiple versions of a given package, one "good" and the other "bad", e.g. two versions of 1.0.0, or a good 1.0.0 release made widely available and a bad 1.0.0-epsilon version which is distributed in a more targeted fashion.

BT makes such attacks discoverable since both versions must be present in the log. 

## Gaps Still Present with BT

### Typosquatting/Dependency Confusion

Typosquatting is when a malicious artifact is uploaded with either a name similar to a popular artifact, and dependency confusion is when an artifact is uploaded to a public registry where it exists only in a private registry with the intent of confusing a dependency resolution system. In either case, the threat is a consumer depending on an incorrect artifact. BT does not solve this problem, as BT cannot detect artifacts with similar names. BT only guarantees that a request for a specific artifact receives a globally consistent response.

Depending on the package identifier, verifiers could use BT log entries to flag suspicious names, as BT would make all package identifiers discoverable.

### Source compromise

Source compromise is a broad category of threats ranging from compromise of the source repo with malicious commits to compromise of the publication process from the repo to the registry. BT does not prevent this, as it cannot block the upload of malicious artifacts.

## Case Studies

### Go SumDB

Go has implemented Binary Transparency with its [checksum database, guaranteeing that there's only one mapping of a package identifier to digest and that all users](https://sum.golang.org/) will download the same artifact given a package identifier. BT for Go prevents the registry, which is effectively Go's module proxy, from tampering with artifacts.

One unique property of Go is the implicit linking of build artifacts with source. Most ecosystems do not link the package identifier to source, and we encourage ecosystems to explore building a mechanism to link an artifact with its source of truth, which could be implemented with source provenance or reproducibility.

BT is a building block towards a complete mitigation against tampering. A complete solution could include BT to mitigate the tampering of artifacts from the registry, signatures or build provenance to provide artifact authenticity, a secure update framework to track version updates, and verifiable reproducibility of a build. Combined, these solutions provide an extremely resilient mitigation against registry compromise and artifact tampering.

### Pixel Binary Transparency

[Android maintains a binary transparency log](https://security.googleblog.com/2023/08/pixel-binary-transparency-verifiable.html) with Pixel firmware. Consumers can [manually verify](https://developers.google.com/android/binary_transparency/verification) their Pixel firmware is present in the transparency log, guaranteeing that the Pixel phone has firmware that has been published by Google. A difference between what this document proposes and Pixel's BT log is that the log is operated by the firmware producer. The [claims](https://developers.google.com/android/binary_transparency/overview#claimant_model) in the log are made by the producer rather than by a registry, so the producer is held accountable for its published firmware. One similarity is that like the mapping of unique package identifiers to digests, the firmware transparency log contains unique firmware identifiers mapping to digests.

### ArmoredWitness Firmware Transparency

[ArmoredWitness](https://github.com/transparency-dev/armored-witness/?tab=readme-ov-file#device) is a small network device based on the [USB armory](https://github.com/usbarmory/usbarmory/wiki) that provides an easy-to-manage log witness that automatically joins a network of other log witnesses. The ArmoredWitness device demonstrates end-to-end integration with Binary Transparency: Inclusion in the log, mandating inclusion proofs, and verifying log entries.

On firmware build and release, the ArmoredWitness's firmware is published to a binary transparency log by the firmware producer. Firmware updates cannot be installed to the device unless proof of log inclusion is presented alongside the firmware update. When a device is initially brought online, device owners will go through manual verification, checking that their device firmware is present in the BT log. Finally, verification of the log entry claims can be automated through reproducibility verifiers that compare entries in the log against reproducibly built firmware hashes.

## Comparison to other solutions

### Pinning

Many dependency management systems support lockfiles which contain a set of hashes for all build dependencies, with the goal being reproducibility of the built artifact. Lockfiles mitigate the threat of tampering with upstream dependencies for a given version. However, pinning only mitigates this threat if the package ecosystem supports lockfiles or if the application has distributed its lockfile with its source.

BT is complementary to pinning. BT provides the digest for a given package identifier, consistent across all consumers, while pinning persists this digest. We can imagine a future iteration of lockfiles that include inclusion proofs for each digest.

### Code signing

Code signing produces a cryptographic digital signature over an artifact, which provides authenticity, integrity and non-repudiation. Code signing is not a new concept, though newer frameworks such as [Sigstore](https://www.sigstore.dev/) aim to simplify signing and make signatures transparently auditable. Artifact signatures would be persisted in the registry alongside the artifact, and verification requires knowledge of the trusted signing identity. To implement code signing thoroughly in an ecosystem, it requires that the package registry add support for signatures and that verification policies are easily derivable. Building verification policies is a hard challenge due to needing to bootstrap trust from an artifact's signing key, with challenges such as determining the correct signing key for a given artifact, updating that key in the event of rotation or compromise, and managing policies for transitive dependencies as well.

BT is complementary to code signing. BT provides integrity for artifacts to prevent tampering, but does not provide authenticity for who produced the artifact. As noted in Mitigated Threats, a compromised registry may choose to present a malicious artifact to all users, and this action is auditable but not caught at consumption time. A signature associates the artifact with a signer who can be trusted through a verification policy.

Code signing also requires active participation by the artifact producer. Producer participation for the publication of an artifact to a BT log is optional, as the registry can publish uploaded artifacts to the log. The producer may choose to operate their own log and publish their own artifacts, for example in the ArmoredWitness case study, but for most cases, the registry can manage log entry uploads which would require no action from the artifact producer.

### Registry-signed artifacts

An alternative to producer-signed artifacts would be for the registry to sign artifacts. This requires that registries support signatures and also manage signing keys. A signature generated by the registry provides integrity, but not authenticity for who produced the artifact.

BT is a simpler solution to integrity. BT simplifies the management of public key infrastructure (PKI). A BT log still needs a signing key for the log inclusion proofs, but there is no need for certificate management, key rotation is a natural part of log lifecycles, and key compromise would not result in needing to re-sign all registry artifacts. Additionally, only the log operator needs to manage the key, which may not be the registry. This benefit of simplifying PKI management cannot be understated \- long-term management of a PKI is costly in terms of maintenance and key compromise or rotation will impact every artifact.

### Release attestations

A Release Attestation is an attestation that a registry has received an artifact for distribution, linking its package identifier to an artifact hash. This attestation has been formalized as an [in-toto predicate type](https://github.com/in-toto/attestation/blob/main/spec/predicates/release.md) and implemented in the npm package registry as a "[publish attestation](https://github.com/npm/attestation/tree/main/specs/publish/v0.1)". By itself, it's effectively a self-signed statement from the registry which still requires trust in the registry and is similar to registry-signed artifacts. When the signed attestation is published to a signature transparency log, it makes the actions of the registry auditable.

BT is an alternative to a Release Attestation. It is a simpler alternative, with the registry not needing to manage an attestation signing key and monitor for key usage in a signature transparency log. The tradeoff is that a Release Attestation could contain far more metadata, but this is also why Binary Transparency is a great solution for this problem \- It's simple, with minimal metadata.

### Build or producer attestations

A build attestation provides provenance for how an artifact was built, in what environment, with what inputs, etc. A producer attestation is an attestation that an artifact meets a set of requirements before being uploaded to a registry, which may include summarization of build provenance or other attestation, and will typically take the form of a [VSA](https://slsa.dev/spec/v1.0/verification_summary).

Like code signing, BT is complementary to build or producer attestations. These attestations provide authenticity and integrity with the tradeoff being more complex verification. These attestations also can contain far more metadata about the production of the artifact.

### PEP 458 / RSTUF

[PEP 458](https://peps.python.org/pep-0458/) proposes the use of [TUF](https://theupdateframework.io/) to secure downloads from PyPI. [RSTUF](https://github.com/repository-service-tuf/repository-service-tuf) is an implementation of a TUF repository as a service to be used by PyPI to manage metadata about artifacts. TUF would prevent [various registry attacks](https://peps.python.org/pep-0458/#appendix-a-repository-attacks-prevented-by-tuf) such as rollback or freeze attacks, where stale metadata is served, in addition to providing a single source of truth for mappings between package identifiers and artifacts.

BT enhances the security posture of PEP 458\. Without BT, PEP 458 requires trust in the registry. Certain attacks are mitigated with respect to the distribution of artifacts, but the registry can still maliciously serve a new artifact to users without detection. There is an element of discoverability since metadata must be committed cryptographically and served via a TUF repository, but this metadata is signed by the registry. This makes PEP 458's threat model similar to registry-signed artifacts where there is still trust in the registry. In addition, the registry can choose to provide split-views to users, where the registry serves different TUF metadata to different callers. BT mitigates this threat by requiring that a log's state be independently verified, or witnessed, to prevent split-view attacks.

PEP 458 and TUF are also complementary to BT. BT only mitigates the threat of a package identifier mapping to multiple hashes, but requires a fully resolved package identifier, such as `name.platform@version`. TUF can provide a mapping between a partial identifier, such as `name@version`, and the fully resolved identifier, where that identifier is then verified to be included in a log.

## Design Ideas

Detailed design will be fleshed out in a later document.

### High-Level Requirements

* An easy-to-deploy-and-manage binary transparency log. Current examples include [Tessera](https://github.com/transparency-dev/trillian-tessera), [Serverless](https://github.com/transparency-dev/serverless-log) and [Sunlight](https://github.com/FiloSottile/sunlight) (designed for Certificate Transparency)  
* Registry support for uploading package identifiers mapped to artifact hashes to a log and providing off-line verifiable proofs of inclusion.  
* Tooling integrated into package managers to seamlessly and transparently verify proofs of inclusion without any configuration from the user.

### Deployment

* Binary Transparency must incorporate all elements of a complete transparency ecosystem integration, with strong offline proofs that bundle an inclusion proof and co-signed witness checkpoints. Witnesses will verify the consistency of the log, that the log remains append-only, as is the requirement for any transparency ecosystem.  
* A log must restrict publishing to only the registry operator. Otherwise, it is not possible to monitor the log for unexpected artifact hashes and hold the registry accountable. A registry may choose to operate the log itself, but the log could also be operated by another entity, as long as in either case, log publication is restricted to the registry operator.

## Claimant Model

Terminology defined in [Trillian documentation](https://github.com/google/trillian/tree/master/docs/claimantmodel).

* The Claim is "There exists at most one mapping between a given artifact's package identifier and its cryptographic hash".  
* The Statement is the package identifier and digest.  
* The Claimant is the Package Registry.  
* The Believer is the artifact consumer.  
* The Verifier is anyone who can view the log, and the artifact maintainer. Anyone can verify that there exists only one instance of a package identifier in the log. The artifact maintainer can verify that the package identifier maps to the expected hash.  
* The Arbiter is the ecosystem.

[^1]:  BT doesn't apply when identifiers are mutable (e.g. identified by a floating label), and provides little value when identifiers are already cryptographically immutable (i.e. identified by digest). Notably, BT doesn't apply to Docker/OCI registries because labels are mutable and image IDs are already digests.

[^2]:  BT also works for software distributed by arbitrary URL, e.g. https://curl.se/download/curl-8.7.1.tar.gz, so long as the URL is logically immutable.

[^3]:  Some package registries support "yanking" or unpublishing an artifact. A registry ideally should not allow a package identifier which includes a version identifier to be reused. BT would enforce this \- an artifact could be unpublished from a registry, but the package identifier could not be reused once committed to the log.

[^4]:  Certificate Transparency relies on search engines like [crt.sh](http://crt.sh) or Cert Spotter to efficiently query certificate transparency logs for domains. These search engines could maliciously hide entries. Without a search engine, an artifact maintainer would need to monitor the log for every entry that matches their package name, which we don't expect every maintainer to do. As future research, the search engine could provide a verifiable search which cryptographically links back to the log with proofs of inclusion and non-inclusion.
