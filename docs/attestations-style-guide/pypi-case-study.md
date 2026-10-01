# Style guide: PyPI implementation case study

Author: [Nicole Harris](https://github.com/nlhkabu)
Added: October 2026.

PyPI is the first package registry to implement this style guide's recommendations. This work has included:

1. Introducing a dedicated security tab
2. Restructuring the main package page to show provenance status in the sidebar
3. Updating the documentation to introduce security documentation

The implementation was tracked on the [Warehouse issue tracker](https://github.com/pypi/warehouse/issues/19950) and documented on the [PyPI blog](https://blog.pypi.org/posts/2026-07-22-ui-updates/).

This page documents what PyPI built, the additional user research conducted to support the implementation, and what other registries can learn from that process. 

## Unique challenges

### Attestations at the file level

Most of the recommendations in this style guide assume a package has a single, package-level attestation. PyPI doesn't work that way: a single release is a collection of files, with each file carrying (or not carrying) its own attestation. A release can therefore be in a mixed state (e.g., some files fully attested, others missing attestations) with no single "the package is attested" status to display.

This meant PyPI couldn't simply drop the style guide's attestation component onto a project page. It needed to decide, separately, what to show at the release level (a summary) and what to show at the file level (the detail), and how to handle disagreement between the two, without overwhelming users.

PyPI also needed to decide how to cover edge cases and warning states that were not explicitly documented in the style guide, including:

1. **Incomplete provenance:** When a release has some files with attestations and some without.
2. **Inconsistent provenance:** When a release has files with different provenance (e.g., some files from one workflow, other files from another).
3. **Loss of provenance:** When a previous release had provenance/attestations, but the current release does not.
4. **Change of provenance:** When the publishing source or repository changed between releases.

In all cases, there could be legitimate explanations for these anomalies (e.g., a maintainer has moved publishing or code hosting platforms). However, these patterns are also strong "smells" that indicate potential compromise. Communicating this requires a careful balance: warning users to act with appropriate caution, without unfairly "shaming" maintainers who make legitimate choices to change their workflows.

### Other security signals

In addition to attestations, PyPI already surfaced security signals that needed to be accounted for in the redesign:

1. Verification signals: Release metadata was grouped and marked as either "Verified" or "Unverified". This is because PyPI checks certain maintainer-supplied metadata during upload. This labeling was unclear in scope and risked creating confusion with attestations.
2. Malware reporting: The existing malware reporting mechanism needed to be closely coupled with security and provenance status

Historically, PyPI also permitted maintainers to upload additional distribution files indefinitely after the initial release date. This was changed in July 2026 when PyPI [introduced a 14-day window for adding new files](https://blog.pypi.org/posts/2026-07-22-releases-now-reject-new-files-after-14-days/). However, there is still value in surfacing historical “late files” in the UI, particularly when they may help explain or provide context for attestation anomalies - this also needed to be accounted for in the redesign.

## Initial designs, research & validation

We created, refined and built new designs as clickable prototypes. This included:

1. How to update the package detail page to improve communication of security signals (including "verified" and "unverified" data) [#19951] - (https://github.com/pypi/warehouse/issues/19951)
2. How to display provenance status in the sidebar - [19975](https://github.com/pypi/warehouse/issues/19975)
3. How to display attestations, both [on the security tab (as recommended in this style guide)](https://github.com/pypi/warehouse/issues/20069) and on the [page where PyPI shows the details of a file](https://github.com/pypi/warehouse/issues/20185)

The designs were then tested with user research:

1. A survey on the sidebar redesign ([warehouse#20058](https://github.com/pypi/warehouse/issues/20058))
2. User interviews with six participants that reflected [the three personas](https://github.com/ossf/wg-securing-software-repos/issues/70), using clickable prototypes ([warehouse#20111](https://github.com/pypi/warehouse/issues/20111)).

The survey asked respondents how to order metadata (including provenance) based on utility and trustworthiness.
 
The interviews tested six provenance UI states: full provenance, PyPI and SLSA provenance attestations together, no provenance, partial provenance, changed provenance, and per-file anomalies. Key findings:

* All six participants preferred ordering sidebar metadata by utility, with security status shown as labels alongside it, rather than grouping information by security status.
* Four of six participants understood provenance in general terms ("where the thing came from"), but two had no familiarity with the term at all
* Participants treated provenance warnings as useful context for further investigation, not as reasons to reject a package outright

This feedback was then integrated into the final designs before build.

## Implementation

Below are a series of annotated screenshots that document the implementation:




## Documentation overhaul

To support the UI changes, we [updated the user documentation](https://github.com/pypi/warehouse/pull/20550), following this guide's [documentation recommendations](/attestations-style-guide/documentation):

* Content previously scattered across a single `/help` page was migrated into structured, role-specific user documentation
* A new **Package Security** section was added under "Using PyPI," aimed at package consumers rather than maintainers, covering source code assessment, provenance and attestations, checksum verification, common attack patterns, and how to report a security issue.

## Recommendations for other registries

### Define what "provenance" and "attestations" are

Until these terms are universal, it is useful to define them. On PyPI we have added this description to the security tab:

> Provenance describes where a file came from. On PyPI, provenance is shared via attestations, which provide a verifiable record of the build or publishing details. View details, limitations and caveats. 

### Be judicious about using "verified", checkmark icons or _green_ styling

As documented elsewhere in this style guide, we found that users are quick to jump to conclusions about what these mean - often assuming that a positive security mark indicates that a package is 100% secure. Some users assumed that "verified" meant that the PyPI team had manually audited a package codebase.

If you are going to use "verified", checkmarks, or green badges, be very careful to scope them appropriately.  For example, we have labeled verified metadata as:

> Data verified by PyPI on <date>

This makes it clear that the _data_ has been verified - not the release or project.

### Security signals are important, but should not be prioritized above utility

Prioritizing security information above all else is not what users wanted; they wanted the most decision-relevant facts first, security-related or not.

## Warnings should give enough context to help users investigate further

We know that users typically scan websites rather than reading every piece of content in detail. We found that warnings can make users stop and pause when they:

1. Carry enough visual emphasis (our warnings were orange and included an alert icon)
2. Provide enough context, including next steps

## Design in the open

All designs/prototypes were shared on the Warehouse issue tracker for public feedback. We also staged each major change to [TestPyPI](https://test.pypi.org/), linking users to an [issue where they could provide feedback](https://github.com/pypi/warehouse/issues/20267). This caught some minor bugs and collected some good feedback that we were able to address before closing out the project. 

Designing in the open and releasing changes in phases also made it easier for our users to adapt: giving them an opportunity to preview what was coming and provide feedback helped build a sense of involvement and ownership.