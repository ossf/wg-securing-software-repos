# PyPI implementation case study

* Author: [Nicole Harris](https://github.com/nlhkabu)
* Added: October 2026

The Python Package Index (PyPI) is the first package registry to implement this style guide's recommendations, following the [highest UI requirements (Level AAA)](/attestations-style-guide/level-aaa). This work included:

1. Introducing a dedicated security tab
2. Restructuring the main package page to show provenance status in the sidebar
3. Updating the user documentation to include dedicated security guidance

The implementation was tracked on the [Warehouse issue tracker](https://github.com/pypi/warehouse/issues/19950) and publicized on the [PyPI blog](https://blog.pypi.org/posts/2026-07-22-ui-updates/).

This page documents:

1. What PyPI built
2. The additional user research conducted to support the implementation
3. What other registries can learn from that process

## Unique challenges

### Attestations at the file level

Most recommendations in this style guide assume a package has a single, package-level attestation. PyPI does not work that way: a single release is a collection of files, with each file carrying (or not carrying) its own attestation. A release can therefore be in a mixed state (e.g., some files fully attested, others missing attestations) with no single "the package is attested" status to display.

This meant PyPI could not simply drop the style guide's attestation component onto a project page. The team needed to decide what to show at the release level (a summary), what to show at the file level (the detail), and how to handle discrepancies between the two.

PyPI also needed to decide how to handle edge cases and warning states that were not explicitly documented in the style guide, including:

1. **Incomplete provenance:** When a release has some files with attestations and some without
2. **Inconsistent provenance:** When a release has files with different provenance (e.g., some files from one repository or configuration, others from another)
3. **Loss of provenance:** When a previous release had provenance/attestations, but the current release does not
4. **Change of provenance:** When the publishing repository or configuration has changed between releases

In all cases, there could be legitimate explanations for these anomalies (e.g., a maintainer has migrated publishing or code-hosting platforms). However, these patterns are also strong indicators of a potential compromise. Communicating this requires a careful balance: warning users to act with appropriate caution without unfairly penalizing or shaming maintainers who make legitimate workflow changes.

### Other security signals

Beyond attestations, PyPI already presented other security signals that needed to be considered in the redesign:

1. **Metadata verification:** PyPI checks select maintainer-provided metadata during upload, historically grouping it into "Verified details" and "Unverified details" sections in the sidebar. However, this labeling was ambiguous in scope and sometimes led users to believe the entire release (rather than just its metadata) had been validated.

2. **Late-uploaded distribution files:** PyPI previously allowed maintainers to upload new distribution files indefinitely after a release date. Although PyPI [introduced a 14-day window for adding new files](https://blog.pypi.org/posts/2026-07-22-releases-now-reject-new-files-after-14-days/) in July 2026, the UI still needed to highlight historical "late files", particularly to help contextualize attestation anomalies.

## Initial designs, research & validation

We created, refined, and built new designs as clickable prototypes. This included:

1. [Updating the package detail page](https://github.com/pypi/warehouse/issues/19951) to improve communication of security signals
2. [Displaying provenance status in the sidebar](https://github.com/pypi/warehouse/issues/19975)
3. Displaying attestations, both [on a new security tab](https://github.com/pypi/warehouse/issues/20069) and on the [file detail page](https://github.com/pypi/warehouse/issues/20185)

The designs were then evaluated through user research, including:

1. [A survey on the sidebar redesign](https://github.com/pypi/warehouse/issues/20058)
2. [User interviews](https://github.com/pypi/warehouse/issues/20111) with six participants representing [the three personas](https://github.com/ossf/wg-securing-software-repos/issues/70)

The survey asked respondents to rank metadata (including provenance) by importance when evaluating a package's trustworthiness and suitability.

The interviews asked users to interact with clickable prototypes, testing six provenance states:

1. Full provenance
2. Full provenance with both PyPI Publish and SLSA Build Provenance attestations
3. No provenance
4. Partial provenance
5. Changed provenance
6. Per-file anomalies

Key findings:

* **Provenance is highly valued:** In the survey, provenance ranked second overall in importance for both suitability and trustworthiness
* **Organizing by utility beats separating "verified" vs. "unverified" details:** While a majority of survey respondents found it helpful to prioritize PyPI-verified metadata, 146 of 777 said separate "Verified" and "Not verified" sections made legitimate, unverified metadata look unnecessarily suspicious. All six interview participants preferred organizing metadata by utility, with inline verification badges and labels.
* **Term familiarity varies:** Four of six interview participants understood provenance in general terms ("where the thing came from"), but two had no familiarity with the term, highlighting the need for plain-language explanations
* **Warnings prompt investigation, not immediate rejection:** Interview participants treated provenance anomalies and warnings as actionable context to investigate further, rather than as an automatic signal to abandon a project or release

User feedback was integrated into the final designs before implementation. For example, we dropped the per-file anomalies design: participants found comparisons between _files within a release_ confusing, and comparisons between _releases_ more useful. As a result, provenance warnings are summarized at the release level: even "Inconsistent provenance", which compares files within a release, is presented as a single release-level warning, with files grouped by repository and configuration.

## Implementation

The following screenshots document the PyPI implementation.

### No provenance

When a release has no provenance:

1. A security tab is displayed
2. No provenance-specific metadata is included in the sidebar

![Screenshot of a project without provenance, with the security tab in the navigation bar and the "Data verified by PyPI" labels in the sidebar both highlighted](/attestations-style-guide/images/pypi-case-study/no-provenance-tab-and-metadata.png "A PyPI project page for a release with verified metadata but no provenance")

When users select the security tab, they see:

1. A description of provenance and attestations:

   > Provenance describes where a file came from. On PyPI, provenance is shared via attestations, which provide a verifiable record of the build or publishing details. View details, limitations and caveats.

2. A "No provenance found" alert:

   ![Screenshot of the security tab, showing a description of provenance and attestations followed by a "No provenance found" notice stating that none of the files in this release were uploaded with provenance metadata](/attestations-style-guide/images/pypi-case-study/no-provenance-security-tab.png "The security tab for a release with no provenance metadata")

This approach introduces users to the concepts of provenance and attestations without penalizing maintainers by displaying a negative "No provenance" status on the main tab.

### With provenance

When a release contains provenance metadata, it is surfaced across several parts of the UI.

**On the project description tab:**

![Screenshot of a project with provenance, displaying metadata in the sidebar](/attestations-style-guide/images/pypi-case-study/with-provenance-metadata.png "A PyPI project page with provenance metadata")

1. The sidebar displays the "Provenance" status, linking to the security tab for more details

**On the security tab:**

![Screenshot of the security tab for a project with provenance](/attestations-style-guide/images/pypi-case-study/with-provenance-security-tab.png "A PyPI security tab with provenance metadata")

1. The provenance status of the _release_ is highlighted in an alert near the top of the page
2. A per-file attestations viewer is displayed, allowing users to inspect the attestations for each file. Where both PyPI and SLSA attestations exist, they are differentiated by color, iconography, and description.

![Screenshot of PyPI and SLSA attestation blocks](/attestations-style-guide/images/pypi-case-study/attestations-detail.png "PyPI and SLSA attestation blocks")

The attestations have been adapted for each attestation type:

1. The attestation block, which the style guide [recommends displaying _under_ the other columns](/attestations-style-guide/level-aaa), has been moved _above_ the other metadata to act as a header. This groups each attestation's identity, workflow, and artifact details together, and allows the attestation type to be used as a heading.
2. The attestation title displays the attestation type (i.e., PyPI or SLSA) and links to the predicate definition
3. A logo denotes which service built or signed the attestation alongside the attestation type. Logo combinations include GitHub + PyPI, GitHub + SLSA, GitLab + PyPI, GitLab + SLSA, Google Cloud + PyPI, Google Cloud + SLSA, ActiveState + PyPI, and ActiveState + SLSA.
4. "Identity", "Workflow/Build", and "Artifact" labels reflect the specific data displayed for each attestation type
5. Subtitles are customized to the attestation type. For example, the repository is labeled as a "Publishing repository" for PyPI Publish attestations, whereas for SLSA attestations, it is labeled as a "Build repository".

**On the files tab:**

![Screenshot of the files tab with files marked "With provenance"](/attestations-style-guide/images/pypi-case-study/with-provenance-files-tab.png "Files tab with provenance marked in the files tables")

1. Files with provenance are marked "With provenance" alongside a blue checkmark that matches the iconography on the security tab

The attestation block is also included on the file detail page (accessed via the "Details" button).

### Warning states

When an anomaly is detected in the release's provenance, it is surfaced across the interface:

1. In the release status bar at the top of the page[^1]
2. In the project description sidebar
3. On the security tab
4. On the files tab and file detail page

[^1]: The release status bar is also used to display other critical states, such as when a project or release has been quarantined by PyPI administrators. In this scenario, quarantine status takes precedence, and provenance warnings are suppressed from this top bar.

#### Incomplete provenance

When only some files carry attestations, an "Incomplete provenance" warning appears in the release status bar and the sidebar's provenance panel, linking to further details:

![Screenshot of a project page showing an "Incomplete provenance" warning across the top release status bar stating that 2 of 5 files were uploaded without provenance metadata, and a matching alert in the sidebar with a link to view provenance details](/attestations-style-guide/images/pypi-case-study/incomplete-provenance-banner-metadata.png "A PyPI project page showing an incomplete provenance warning in the release status bar and sidebar")

On the security tab, an alert explains how many files were uploaded without provenance metadata, accompanied by a bar chart breaking down the release's files:

![Screenshot of the security tab showing an "Incomplete provenance" alert with a bar chart showing 3 of 5 files with provenance and 2 of 5 files without provenance](/attestations-style-guide/images/pypi-case-study/incomplete-provenance-security.png "The security tab for a release with incomplete provenance, showing a breakdown of files with and without provenance")

On the files tab, an alert is displayed, with individual files marked as either "With provenance" or "Without provenance":

![Screenshot of the files tab showing an "Incomplete provenance" alert above the source distribution table, with files marked either "With provenance" or "Without provenance"](/attestations-style-guide/images/pypi-case-study/incomplete-provenance-files.png "The files tab for a release with incomplete provenance")

#### Inconsistent provenance

When files within the same release originate from differing repositories or configurations, an "Inconsistent provenance" alert is surfaced across the top bar and sidebar panel:

![Screenshot of a project page showing an "Inconsistent provenance" warning across the top release status bar stating that files in this release originate from inconsistent repositories or configurations, and a matching alert in the sidebar with a link to view provenance details](/attestations-style-guide/images/pypi-case-study/inconsistent-provenance-banner-metadata.png "A PyPI project page showing an inconsistent provenance warning in the release status bar and sidebar")

The security tab outlines the distinct repositories and configurations detected across the artifacts, grouping files by the repository and configuration that produced them:

![Screenshot of the security tab showing an "Inconsistent provenance" alert that breaks down the release's files by repository ("seed-org/alpha" and "seed-org/beta") and configuration ("release.yml" and "publish.yml")](/attestations-style-guide/images/pypi-case-study/inconsistent-provenance-security.png "The security tab for a release with inconsistent provenance, showing files grouped by repository and configuration")

On the files tab, an alert notes that the release's files originate from different repositories or configurations:

![Screenshot of the files tab showing an "Inconsistent provenance" alert above the source distribution table, recommending that users inspect each repository and configuration before proceeding](/attestations-style-guide/images/pypi-case-study/inconsistent-provenance-files.png "The files tab for a release with inconsistent provenance")

#### Loss of provenance

When provenance has been lost between releases[^2], the UI displays a "Loss of provenance" alert in the top bar and sidebar:

[^2]: A release displays "Loss of provenance" if none of its files have attestations, but a prior release created within the preceding 14 days did. We chose a time-based window rather than a release count to prevent an attacker from flooding a project with releases to suppress the warning.

![Screenshot of a project page showing a "Loss of provenance" warning across the top release status bar, and a matching alert in the sidebar with a link to view provenance details](/attestations-style-guide/images/pypi-case-study/loss-of-provenance-banner-metadata.png "A PyPI project page showing a loss of provenance warning in the release status bar and sidebar")

On the security tab, an alert explains that a previous release had provenance metadata while the current one does not, and includes a release comparison table:

![Screenshot of the security tab showing a "Loss of provenance" alert, including a release comparison table that marks release 1.0.0 as "With provenance" and release 2.0.0 as "Without provenance"](/attestations-style-guide/images/pypi-case-study/loss-of-provenance-security.png "The security tab for a release that has lost provenance, showing a release comparison")

On the files tab, an alert is added that links users to the security tab for more information:

![Screenshot of the files tab showing a "Loss of provenance" alert above the source distribution and built distribution tables, with each file marked "Without provenance"](/attestations-style-guide/images/pypi-case-study/loss-of-provenance-files.png "The files tab for a release that has lost provenance, with files marked without provenance")

#### Change of provenance

When the publishing repository or configuration changes between releases, a "Change of provenance" warning is surfaced across the release status bar and sidebar:

![Screenshot of a project page showing a "Change of provenance" warning across the top release status bar, and a matching alert in the sidebar with a link to view provenance details](/attestations-style-guide/images/pypi-case-study/change-of-provenance-banner-metadata.png "A PyPI project page showing a change of provenance warning in the release status bar and sidebar")

On the security tab, an alert explains that the repository and configuration that created this release differ from a previous release, accompanied by a diff comparison:

![Screenshot of the security tab showing a "Change of provenance" alert with a diff comparing the repository ("seed-org/alpha" to "seed-org/beta") and configuration ("release.yml" to "publish.yml") between releases 1.0.0 and 2.0.0](/attestations-style-guide/images/pypi-case-study/change-of-provenance-security.png "The security tab for a release with changed provenance, showing a repository and configuration diff")

On the files tab, an alert is added that links users to the security tab for more information:

![Screenshot of the files tab showing a "Change of provenance" alert above the source distribution table, recommending that users inspect the repository and configuration before proceeding](/attestations-style-guide/images/pypi-case-study/change-of-provenance-files.png "The files tab for a release with changed provenance")

#### Files added late

When a file is uploaded more than 14 days after the first file in a release, a "File added late" warning is surfaced in the release status bar, as well as on the files tab and file detail page. On the security tab, an "Upload timing" section is added to provide more context. Because PyPI now [rejects new files after 14 days](https://blog.pypi.org/posts/2026-07-22-releases-now-reject-new-files-after-14-days/), this warning only appears on historical releases.

![Screenshot of the security tab showing a "File added late" alert in an "Upload timing" section, stating that 1 file was uploaded more than 14 days after the first file in this release](/attestations-style-guide/images/pypi-case-study/file-added-late.png "The security tab's upload timing section for a release with a file added late")

When a release has _both_ late-file and provenance anomalies, the release status bar shows only the provenance warning. On the files tab and file detail page, the warnings are consolidated into a single composite alert for improved usability (e.g., "Loss of provenance, with files added late").

## Documentation updates

To support the UI changes, we [updated the user documentation](https://github.com/pypi/warehouse/pull/20550), following this guide's [documentation recommendations](/attestations-style-guide/documentation):

* Content previously managed within a single `/help` page was migrated into structured, role-specific user documentation
* A new **Package Security** section was added under "Using PyPI" for package consumers, documenting provenance and attestations alongside source code assessment, checksum verification, common attacks, and vulnerability reporting

## Recommendations for other registries

### Define what "provenance" and "attestations" mean

Until these terms become industry-standard knowledge, registries should define them clearly. On PyPI, we added this description to the security tab, which links directly to the updated documentation:

> Provenance describes where a file came from. On PyPI, provenance is shared via attestations, which provide a verifiable record of the build or publishing details. View details, limitations and caveats.

### Be judicious about using "verified", checkmark icons, or green styling

As documented in the [Level AA recommendations](/attestations-style-guide/level-aa), we found that users quickly jump to conclusions about these indicators, sometimes assuming that a positive security badge means a package is 100% secure. Two of six interview participants assumed that "verified" meant the PyPI team had manually audited the release's source code.

If you use "verified", checkmarks, or green badges, be careful to scope them explicitly. For example, we labeled verified metadata as:

> Data verified by PyPI on \<date\>

This clarifies that the _data_ has been verified, not the entire release or codebase.

### Security signals are important, but should not supersede utility

We found that prioritizing security information above all else is not what users wanted; they looked for decision-relevant facts first, whether security-related or not. This finding is consistent with [other recommendations in this style guide](/attestations-style-guide/level-aaa).

### Warnings should provide enough context for users to investigate further

Users typically scan web pages rather than read every piece of text in detail. We found that warnings prompt users to pause when they:

1. Carry sufficient visual emphasis (our warnings were styled in dark orange with an alert icon)
2. Provide enough context, including actionable next steps

### Design in the open

All designs and prototypes were shared on the Warehouse issue tracker for public feedback. We also staged each major change to [TestPyPI](https://test.pypi.org/), directing users to an [issue where they could provide feedback](https://github.com/pypi/warehouse/issues/20267). This process surfaced edge-case bugs and generated actionable feedback that we addressed before closing out the project.

Designing in the open and releasing changes in phases also helped users adapt: previewing upcoming changes and providing early feedback fostered a sense of involvement and community ownership.

---

Back to: [Style guide overview](/attestations-style-guide)
