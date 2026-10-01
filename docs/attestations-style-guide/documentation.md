# Style guide: Documentation recommendations

Supporting users with effective documentation is key to helping them build an understanding of what attestations are and how they can be used.

Our research found that existing documentation about attestations was either missing entirely or written only for expert audiences. To address this and to support our UI recommendations, we suggest the following principles to help registries create effective documentation for attestation consumers.

## Best practices for documenting attestations

**Attestations documentation should:**

- Help package consumers understand attestations, including what they are, how they work, and what their limitations are

- Help package consumers understand attestations within the context of other security features and practices

- Direct package maintainers towards workflows that generate attestations

For attestation documentation to be most successful, we recommend documentation authors follow these seven principles:

### 1. Use key terms consistently

To ensure clarity and consistency for attestation consumers, use key terms as defined below. Adhering to these standards prevents user confusion across packaging ecosystems.

Provenance
: _Definition_: Where a package came from
: _Do_: Clarify this term in headings or text when the concept might be new to users
: _Example_: "Provenance (package origin)"

Attestation
: _Definition_: A statement of signed facts (or metadata) about a software artifact
: _Do_: Use this as the general term for a signed claim. It is the foundation for more specific terms like "Build Provenance Attestation"

Build Provenance Attestation
: _Definition_: A specific type of attestation that describes how, when, and where a package was built
: _Do_: Clarify the relationship between attestations and build provenance using this term
: _Example_: "A build provenance attestation describes how, when, and where a package was built."

Transparency Log Entry
: _Definition_: The tamper-proof record of the build provenance attestation saved to a public ledger
: _Do_: Use "transparency log entry" to describe how an attestation is recorded
: _Example_: "Each attestation is recorded in a public ledger as transparency log entry, which is a permanent, auditable record that cannot be changed."

Verified / verify / verifying
: _Definition_: The process that a package repository takes when accepting an attestation from a build platform, ensuring the attestation's source matches the maintainer's configuration _and_ the process users can use to confirm that an attestation is valid
: _Do_: Use "verified" to describe the repository's automated check during package upload. Use "verify" to describe the user checking the attestation.
: _Examples_: "PyPI verifies this attestation at upload time, confirming that the identity matches what the maintainer previously configured for Trusted Publishing." "To manually verify an artifact against its provenance object..."

### 2. Structure documentation around user roles

Package consumers and maintainers require (and have) different levels of knowledge about security concepts and features, including attestations.

Content for package consumers should be separated from content for package maintainers, surfacing relevant and actionable information to each audience.

Structure the Information Architecture around user roles, using clear, top-level sections like "Using This Repository" (for consumers) and "Publishing Packages" (for maintainers).

### 3. Provide content to help package consumers understand attestations within the context of other security features

Attestations are only one part of a larger security story. To be effective, documentation must place them in context, helping users build a holistic mental model of risk.

Documentation for package consumers should explain how security practices and features work together as a layered defense. It should be structured around the fundamental questions a user has about risk:

1. Can I trust the source code?
Explaining signals like project activity, vulnerability scanning, etc.

2. Where did this package come from and how was it made?
Explaining build provenance and attestations

3. Did I download the same file that is hosted on the package repository?
Explaining checksums and integrity

### 4. Warn package consumers that packages are not secure by default

Some package consumers hold the incorrect assumption that because a package is published on an official repository it is secure and/or trustworthy. To combat this, include disclaimers on pages for package consumers, directing users towards security documentation.

Example from PyPI:
_Warning: Installing packages from PyPI means running third-party code, which carries inherent security risks. Before installing any package, we strongly recommend reading our Package security guide._

### 5. Normalize secure-by-default publishing workflows

Documentation should be opinionated in favor of security. The most secure method for any task should be presented as the canonical, recommended path.

When writing documentation about publishing packages, prominently feature the most secure, automated publishing method that generates attestations. This should be the first and most detailed workflow described, establishing it as the modern standard.

Where applicable, clearly and explicitly state that using the recommended workflow confers the benefit of generating provenance attestations automatically. This makes adopting the secure workflow more compelling.

Legacy methods that do not produce attestations should be explicitly marked as "deprecated" or "for advanced use cases" to guide users away from them.

### 6. Explain common security attacks and how they are mitigated

Transparently list the threats the user faces (e.g., Typosquatting, Account Takeover) and what they can do to protect themselves. Explain platform-level features that mitigate common attacks, including the role of Trusted Publishing and attestations.

Provide clear reporting channels for users concerned about the security of an individual package or the package repository as a whole.

### 7. Be transparent about limitations and set clear expectations

Documentation must be upfront about the scope and limitations of the security practices or features it describes.

State clearly that an attestation proves provenance (where a file came from) but does not vouch for the code's safety (that the code is free of bugs or vulnerabilities). Explain that trusting an attestation means implicitly trusting the tooling and authority that issued it.

Be transparent about the readiness of downstream tooling. Where applicable, highlight that automated attestation verification is not yet ready in common package managers.

## Applying documentation principles to RubyGems.org, PyPI and npm

To help RubyGems.org, PyPI, and npm adopt attestation documentation best practices, we have created specific recommendations for each repository. Each recommendation includes user-tested templates that can be used to create new documentation or revise existing materials.

We encourage RubyGems.org, PyPI and npm to use, improve, and extend these templates as they see fit. Other package repositories can also use these templates as inspiration for their own attestations documentation.

* [RubyGems.org documentation recommendations](/attestations-style-guide/zips/rubygems_attestation_documentation_templates.zip)
* [PyPI documentation recommendations](/attestations-style-guide/zips/pypi_attestation_documentation_templates.zip)
* [npm documentation recommendations](/attestations-style-guide/zips/npm_attestation_documentation_templates.zip)

---

Next: [PyPI implementation case study](/attestations-style-guide/pypi-case-study)