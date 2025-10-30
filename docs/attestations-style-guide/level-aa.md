# Style guide: Level AA - Medium

This section of the style guide defines the medium (Level AA) requirements for displaying attestation information on package registries, aiming to strengthen users' sense of security and trust in a package's build integrity.

Package repositories opting to implement these recommendations will need to allocate more visual space within their user interfaces. This approach expands upon the information introduced in the lowest (Level A) requirements by proactively revealing additional details, source links, and clear pathways for users to explore and better understand attestation and related information.

There are variants for medium-level requirements:

1. **Three-Card Layout**: Information is presented in distinct "cards" or modules. Each card includes
   icons, headings, labeled source links, and links to documentation (where relevant). This variant
   typically features three cards, with flexibility for additional cards as needed.

2. **Four (Larger) Card Layout**: Designed for package registries with more visual space, this variant
   utilizes larger card designs. It typically features four cards, with flexibility for additional cards
   as needed.

During user testing, we found that variants one and two (three card and four card layouts) were most effective in helping users explore the safety, security and integrity of a package, along with the included links.

For user research notes from this project, please see [notes from user tests
focused on evaluating attestation user interfaces for clarity and user
preference](https://github.com/ossf/wg-securing-software-repos/issues/66).

![A screenshot of a UI example of the medium level AA requirements for visualising attestation information](/attestations-style-guide/images/medium-requirements-1.png "A screenshot of a UI example of the medium level AA requirements for visualising attestation information")
_A screenshot of a UI example of the medium level AA requirements for visualising attestation information. Box width = 200px Height = 160px in example_

Cards are designed so that three should fit in most main page widths for platforms and boxes can be stacked e.g. if there are two or more attestations the fourth box can go below the Source card etc.

The detail here is the same as the expanded version of the minimal, Level A component. Differences are that the package name, version number and box icon has been swapped with a browser and code brackets icon with the heading of "Source". To users, the package icon, name and the source icon and label source mean the same/similar enough terms and the associating information of repo and source commit contextualise the heading for them.

Later in this style guide we'll clarify the use of the terms like "build confirmed" versus the use of "verification".

Again, the Build Confirmed card contains the build commit (for the version available on the page/platform) and the build logs. Please note these example links may not be exactly accurate link destinations.

The Transparency log link can either be the URL or a hyperlink.
More detail about hyperlinks can be found in the hyperlinks page of this style guide.

![A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size](/attestations-style-guide/images/medium-requirements-2.png "A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size")
_A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size. Box width = 260px Height = 200px in example_

Again, these cards are designed to be stacked and so that two should fit within the width of the main content area of standard page layouts. For example, if there are two or more attestations they can form a row of two: the Source card can go next to the Build Confirmed card, and the Integrity card can occupy a single space with an empty space next to it, or be centered in the layout to suit tastes.

These cards contain the same information as the version on the previous page with three cards in a row. The only notable difference is that, with more space, the Transparency Log label and link can be gently sectioned off with a dotted line to maintain its association with the attestation while also occupying its own distinct space.

By having two (or three, depending on page width) cards horizontally, with others stacked below, we can introduce more supporting information near the attestation box. The Integrity card should contain the "checksum" used to verify the attestation, along with a link to documentation to inform and educate users. Checksums are explored in more detail in this style guide.

The possible and likely scenario of checksums being duplicated across page information is also addressed in the large medium UI mockups. In short, duplication was not an issue for users across any links or information. In fact, repeating details—such as links or checksum details, when they are supposed to match—was seen as a positive. All users we tested with reported greater confidence in the validity of the entire page's information as a result.

![A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size](/attestations-style-guide/images/medium-requirements-3.png "A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size")
_A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size_

An example of the larger card sizes when a page width allows for three cards in a row with an additional Integrity card stacked under them in a row by itself.

This indicates to the users that there could be more future information added here that is relevant to attestations. The design and layout did not look like there was 'unused space' to users but when implementing caution should be used when allowing for many solo/one cards as the information looks 'orphaned' when only one card is present and it does not attempt to span the width of the page layout's available space.

![A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size](/attestations-style-guide/images/medium-requirements-4.png "A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size")
_A screenshot of a UI example of the medium level AA requirements for visualising attestation information with larger 'box' size_

An example—if appropriate and if sufficient page width is available—is centering a smaller row of cards  beneath a larger row, as seen here with three cards in the first row and two cards in the second row, rather than either left or right aligning the smaller row. (The example shown uses two of the same attestation and is only intended to demonstrate display orientation.)

![A screenshot of where the medium level AA UI should ideally be situated on a webpage](/attestations-style-guide/images/medium-requirements-webpage-placement-1.png "A screenshot of where the medium level AA UI should ideally be situated on a webpage")
_A screenshot of where the medium level AA UI should ideally be situated on a webpage_

The positioning for the medium level AA UI are the same as the lowest level A UI.

After critical functional information about what the package does and as near to the 'social proof' information as possible aka download numbers, maintainer/contributor profiles/names and other package provenance information.

There was another tested Medium UI component that we've documented for clarity but no longer recommend implementing. This design follows in the next pages of medium requirements.

![A screenshot of the medium level AA UI that uses a large, segmented container box for all information](/attestations-style-guide/images/medium-box-requirements-1.png "A screenshot of the medium level AA UI that uses a large, segmented container box for all information")
_A screenshot of the medium level AA UI that uses a large, segmented container box for all information_

When testing this large card's design, we learned that every user coming to a package registry page has some level of caution and/or doubt about the information it contains. They already arrive cautious and with shaky trust levels. This is due to thoughts like, "Anyone can just put any text or info on these pages, right? The maintainers or the registry, anyone? So by default, I don't trust information unless I look at the sources and confirm for myself."

This means that "( ! ) caution..." messages—while they reinforce users' existing caution and clarify risks—are often bothersome and typically unhelpful beyond a single, simple warning that reminds users to be careful. We recommend reducing the number of warning and caution-type messages across the page.

This variant of the card component maintains a distinct design for the registries and platforms that would like these details to look like a clearly separate component that is different (external) from regular page information. The colors and brand design elements can be styled per platform.

This version also emphasizes explanatory text and warnings about the limitations of attestations—specifically, what an attestation is versus how the information presented might be interpreted by a user.

Regarding language: this is the minimal design with the most clarifying text. For platforms that want to include as much disclaimer-like text as possible, this design (or the highest level, AAA, described later in this style guide) is recommended.

![A screenshot of the medium level AA UI that uses a large, segmented container box for all information with annotation](/attestations-style-guide/images/medium-box-requirements-2.png "A screenshot of the medium level AA UI that uses a large, segmented container box for all information with annotation")
_A screenshot of the medium level AA UI that uses a large, segmented container box for all information with annotation_

A note on the words "verification," "verified," and "verify" versus using similar words like "confirm," "confirmed," "accepted," "accepts," "validates," "inspected," etc.

When we asked users to explain back to us what attestation language meant to them, in our user tested designs, we avoided using "verified" as a term. Instead we relied on the terms "confirmed" or "accepted" as common language.

Some users who lacked experience with attestation nuances explained this information as 'verification of complete safety of the package'.
When we clarified that verification of complete safety is aspirational--not necessarily what is on offer here--users acknowledged that they understand no package is ever 100% safe, regardless of the details provided.

However, this highlights the need to use terms like "verification" and "verified" with caution, as users often interpret them as a guarantee of complete safety.

The language used in the card here—such as "confirms," "accepts," etc.—still clearly explains to users what is happening: that entities are checking details and asserting an opinionated "clearance" of certain aspects, such as build provenance or expected origin. However, users often jump to "verified!" assumptions. The term "verification" should only be used when a platform is prepared to accept the risk of users assuming full safety of a package when this word is present.

![A screenshot of the medium level AA UI that uses a large, segmented container box with PyPI colors](/attestations-style-guide/images/medium-box-requirements-3.png "A screenshot of the medium level AA UI that uses a large, segmented container box with PyPI colors")
_A screenshot of the medium level AA UI that uses a large, segmented container box with PyPI colors_

Medium design that users least preferred.

We mixed up all designs when showing users the UI. Users received Highest first, Lowest first and Medium first. This design tested the least favourably with users and therefore we're removing from the recommendation but retaining as documentation in the style guide to ensure clarity.

This card attempts to combine all of the most useful information tested in the more minimal light and medium versions. Short of the AAA requirements, we consider this to be the most comprehensive version of the component which introduces new pages or sections to registries and platforms. This design aims to show all of the most relevant and relational information, including the specific, essential attestation data. You could liken it to having the "nutrition label" right next to the food name.

Please open the following annotated UI full webpage examples in an image viewer of your choice. This image is large at 4.6MB and 14052x14542 pixel canvas. There is also a .pdf file.

* [ui-development-medium-ui-version-a-level.png](/attestations-style-guide/images/ui-development-medium-ui-version-a-level.png)
* [ui-development-medium-ui-version-a-level.pdf](/attestations-style-guide/images/ui-development-medium-ui-version-a-level.pdf)

The following text is included in the annotated image file:

* An example of a row of equally sized cards that fits in the width of the main page section.
* Note in this example, there is no checksum/SHA container included in the design.
* Example of a two x two horizontal stacking of cards.  In this example, the Integrity section includes checksum/SHA information, which helps visually balance the design.
* Platforms can choose to make a single container span two spaces. There is no strict rule for how wide or tall box containers should be, but it is strongly advised not to have containers of different heights next to each other (see diagram below).

![A screenshot of the medium level AA UI showing good and bad placement](/attestations-style-guide/images/medium-ui-placement.png "A screenshot of the medium level AA UI showing good and bad placement")
_A screenshot of the medium level AA UI showing good and bad placement_

Note: the cards can either span the full width of the available page space, or they can occupy only the minimum width necessary for accessible visibility of information.

Example of a single card stacked below three standard card. These three horizontal cards also occupy the minimum width space for available information.

---

Next: [Highest UI requirements (Level AAA)](/attestations-style-guide/level-aaa)
