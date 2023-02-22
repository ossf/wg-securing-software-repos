# Survey Summary and Takeaways

This document summarizes the survey results and gives some insight into some
takeaways from each category of the survey.

In total, we had package manager maintainers (and/or reputable sources) from 11
different package manager ecosystems responded to the survey. Including:

-   PyPI (Python
-   Gradle (JVM)
-   Basalt  (Bash)
-   Opam (OCaml)
-   RubyGems (ruby)
-   Npm (javascript)
-   Pkg.go.dev (go)
-   Cargo (Rust)
-   Pub (Dart)
-   Apache Maven
-   Maven Central

## Integrity

Most support is still around developer owned keys for signing (with PGP being
the most supported signature type), with some a couple ecosystems with no
support for signing yet - but there is interest/plans.

There are no package managers that support keyless signing yet.

Java, OCaml, Go, Ruby and Rust support reproducible builds with Maven Central
making it mandatory.

![image](https://user-images.githubusercontent.com/3060102/220680128-180c076c-31de-4f32-884e-7c2de8137dc0.png)

## Typos & dependency confusion

45.5% of package managers do not require and do not plan on having DNS
verification proof when reserving/exercising a domain/namespace or domain name
attribute of a package. This could lead to impersonation of
organisations/entities. A method to reduce the cost of protecting against this
threat or education of the seriousness of this threat is needed.

General typos and dependency confusion is observed and handled in a myriad of
different ways across ecosystems. It would be helpful to provide guidance on a
list of methods and evaluation of their effectiveness.

![image](https://user-images.githubusercontent.com/3060102/220680273-500cc331-728b-48e6-a8e6-8c5fd131b57a.png)

## Handling compromise and malice

Most ecosystems don't see the responsibility of finding malware in the packages
as their responsibility. However, they provide the ability to flag and handle
malware in releases when it happens.

Rust, Ruby and Gradle have no plans on ensuring that install and build code
doesn't allow execution of arbitrary code on the host in an unprotected way.
This is an area that requires further investigation into why that is not a
priority and look into a way to be able to have isolation and provenance of
builds without this property.

![image](https://user-images.githubusercontent.com/3060102/220681554-3b469808-3fdd-441e-b91c-0cf060461af2.png)

## Protecting the ecosystem

Most ecosystems are not currently performing any security testing against its
code/infrastructure. However, all of them are interested (7) or have it planned
(2). These ecosystems could be funded for security testing.

All ecosystems have a process in place for vulnerability disclosure or are
interested in doing so.

Only 1 ecosystem has additional supply chain security guarantees for the
binaries/tooling that it produces. This is an area for improvement overall.

![image](https://user-images.githubusercontent.com/3060102/220682148-2d488135-4695-41b5-a6ab-e5f85883f612.png)

## Auth and Credential Management

Generally there is interest in protecting token security, which is positive
feedback. There are 2 ecosystems that currently have no plans on requiring MFA.
Further investigation on why would be helpful.

## Policy:

With policy, there is a mix of implementations that help provide ability to
create policy on keys/hashes as well as checking for known vulnerabilities, as
well as a significant number of ecosystems (4-5) which do not but are
interested.

For policies that take into account 3rd party audits and attestations, only 1
ecosystem provided functionality. The rest are mostly interested (8) and planned
(1). This could be somewhere that a supply chain knowledge graph project and
public instance can be leveraged to lower the cost to do so.

![image](https://user-images.githubusercontent.com/3060102/220683454-3d685cb4-861a-498c-b3b9-6fbde42b7d3a.png)

## SBOMs

7 of 11 ecosystems do not currently have support for generating SBOM but are
interested (5) or planned (2). Additional tooling support is required and could
be a place where the OpenSSF SBOMs everywhere workstream 9 can be helpful.

Most SBOM formats are around SPDX and CycloneDX, with the exception of golang
that provides an intermediary format. This is a positive indicator of
convergence around the two SBOM standards.

![image](https://user-images.githubusercontent.com/3060102/220681004-a45e2790-aa2a-45fc-8262-3bb36a183897.png)


## Identify / produce good dependencies

In general most ecosystems allow pinned dependencies that are immutably
verifiable. However, there are 3 ecosystems that do not have this yet. Further
investigation on why would be helpful.

Only 27.3% of ecosystems have fuzzing services and utilities available, 45.5%
have no plans on implementing and the last 27.3% are interested in exploring.
This could be an avenue for education of the value of fuzzing within the
different ecosystems.

There is a surprising lack of SAST/DAST services available for ecosystems to
detect bad code patterns with 5 ecosystems without the capabilities at the
moment. Funding of tooling could be helpful here.

There is a high demand (8) of services and tools for developers to help keep
their code and packages in good shape. E.g. like dependabot for the package
ecosystem. This would be a gap that could be filled by additional tooling.

Across the board, there are no ways to score dependencies based on their
hygiene or security posture. Further education on scorecards, or evaluation of
how scorecards can be made more useful to package ecosystems will be useful.
