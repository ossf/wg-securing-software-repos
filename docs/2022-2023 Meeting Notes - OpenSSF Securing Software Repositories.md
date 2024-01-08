<h2 align="center">2022 - 2023 Meeting Notes: OpenSSF Securing Software Repositories</h2>


Important links:



* Zoom meetings: [EMEA-friendly time](https://zoom-lfx.platform.linuxfoundation.org/meeting/98058137343?password=28dafc6e-cfcf-440d-bb63-ca73a1739f06) / [APAC-friendly time](https://zoom-lfx.platform.linuxfoundation.org/meeting/98109462025?password=cd540428-a656-44d7-851b-c3cc658174d2) 
* Join the OpenSSF Slack: [Slack Invite](https://slack.openssf.org/) 
* Join the slack Channel: [#securing_software_repos channel](https://app.slack.com/client/T019QHUBYQ3/C034CBLMQ9G)

**Antitrust Policy Notice:** 

<p align="justify">Linux Foundation meetings involve participation by industry competitors, and it is the intention of the Linux Foundation to conduct all of its activities in accordance with applicable antitrust and competition laws. It is therefore extremely important that attendees adhere to meeting agendas, and be aware of, and not participate in, any activities that are prohibited under applicable US state, federal or foreign antitrust and competition laws. Examples of types of actions that are prohibited at Linux Foundation meetings and in connection with Linux Foundation activities are described in the Linux Foundation Antitrust Policy available at [http://www.linuxfoundation.org/antitrust-policy](http://www.linuxfoundation.org/antitrust-policy). If you have questions about these matters, please contact your company counsel, or if you are a member of the Linux Foundation, feel free to contact Andrew Updegrove of the firm of Gesmer Updegrove LLP, which provides legal counsel to the Linux Foundation.</p>

**Code of Conduct**: All OpenSSF meetings must be conducted according to the OpenSSF Code of Conduct. 

See: [Code of Conduct - Open Source Security Foundation](https://openssf.org/community/code-of-conduct/)




Please use the[ 2024 Meeting Notes](https://docs.google.com/document/d/1HzA4M4toiExUYQAkuLqimy4EuuunHagUQ7rZKJDb1Os/edit?usp=sharing)

<h3>Dec 14, 2023 | Securing Software Repositories (EMEA-friendly)</h3>


Attendees



* Zach Steindler (GitHub, OpenSSF TAC)
* Georg Kunz (Ericsson)
* Luca Bandini (SIGHUP)
* Tobias Bieniek (Rust Foundation / crates.io)
* Elijah Tripp (UNCW Rezlab)

Agenda



* Welcome / intros
    * Elijah Tripp - studying supply chain security
* Principles for Package Repository Security [pull request](https://github.com/ossf/wg-securing-software-repos/pull/37)
    * Tobias can help review from Rust / crates.io
    * Brian will review when he has time
* [https://blog.rubygems.org/2023/12/14/trusted-publishing.html](https://blog.rubygems.org/2023/12/14/trusted-publishing.html) 
    * William Woodruff from Trail of Bits presented on this at OpenSSF Spain event
    * We’re big fans of getting secrets out of CI/CD pipelines!
    * It’s really important to scope these OIDC trust relationships to your owner / repo
* OpenSSF elections
    * Eligible voter registration: [https://forms.gle/M2Rdc1EKbudGt2357](https://forms.gle/M2Rdc1EKbudGt2357)
    * TAC nomination form: [https://forms.gle/nhX6QLfz2jdtRJ2y5](https://forms.gle/nhX6QLfz2jdtRJ2y5) 
    * SCIR nomination form: [https://forms.gle/QJSjZ8LEh22onvu5A](https://forms.gle/QJSjZ8LEh22onvu5A) 
* The Great Artifact Repository Audit!
    * Technically shelved, although we can bring it back
    * Alpha Omega funds security audits, it exists as a line item in the Package Repository Security Principles
* Victor: what about repository disaster recovery?
    * Java ecosystem has had central repositories switch to read-only
    * Is there a race condition between when you submit a commit and when it is geographically distributed?
    * npm (and build provenance) are heavily cachable
    * It’s important for these security capabilities to be available across vendor / hosted toolchains

<h3>Nov 29, 2023 | Securing Software Repositories (APAC-friendly) CANCELED, see you next time!</h3>


<h3>Nov 16, 2023 | Securing Software Repositories (EMEA-friendly)</h3>


Attendees



* Zach Steindler (GitHub, co-chair)
* Amanda Martin (Linux Foundation)
* Luca Bandini(SIGHUP)
* Josef Šimánek (RubyGems/RubyGems.org)
* Trishank Kuppusamy (Datadog)
* Jack Cable
* Kairo Araujo (VMWare)
* Martin Vrachev (VMware)

Agenda



* Welcome / intros
    * Welcome Luca! Interested in software supply chains
* [Josef Šimánek] [RubyGems RSTUF PR](https://github.com/rubygems/rubygems.org/pull/4167)
    * Adding API endpoints for adding and removing packages from the index
    * Working towards making “shadow” deployment that’s used but not exposed to end users, in order to see how it works and uncover bugs
        * Merge on RubyGems and make staging deployment
    * RSTUF allows the client to detect if the package has been tampered with (if it doesn’t match the length or hash stored in RSTUF)
    * Trishank just presented at KubeCon how this simplifies TUF adoption proposals for PyPI and RubyGems
    * Trishank: what keys will the TUF root use?
        * Josef: right now it’s managed locally, probably AWS KMS for staging
    * Trishank: what if the API request to RSTUF fails?
        * Kairo: You can retry and add the package, timestamp, hash, length, etc in the next retry
* [Jack Cable] 
    * Jack has done a round of edits, responding to feedback, and outstanding questions
    * Please take a look at outstanding open questions
    * Have any package managers undertaken the Minimum Viable Security Product?
    * Zach: we should publish this on repos.openssf.org! We should think more about next steps after that.
* Josef: what should be the next step for the working group after RSTUF?
    * Zach: we have build provenance GA in npm, as well as work underway in Homebrew, and interest from Python and Java - lots more to do here!
    * Trishank: I had a proposal at PackagingCon 2023
        * “What’s the TLS of OSS supply chain security?”
        * Where and how is policy for a given artifact stored with integrity? Could also store it in a TUF repository!
            * Policy around SLSA Source Track, build attestations, publish attestations, etc
        * Kairo: RSTUF already supports custom entries!
        * Josef: this is great, but I’d like to see one level lower - what change(s) in what ecosystem(s) would be needed to realize this?
        * Josef: looking for guidance on “if you implement this, it unlocks these other things”
            * Also guidance on what threats are the biggest!
        * Martin: Thank you Josef for proactively reaching out to RubyGems on RSTUF!
        * Trishank: Please reach out if you want to have a follow-up conversation here!

<h3>Nov 1, 2023 | Securing Software Repositories (APAC-friendly) CANCELED, see you next time!</h3>


<h3>Oct 19, 2023 | Securing Software Repositories (EMEA-friendly)</h3>


Attendees



* Trishank Kuppusamy (Datadog)
* Zach Steindler (GitHub, co-chair)
* Tobias Bieniek (crates.io / Rust Foundation)
* Jack Cable (CISA)
* Ciara Carey (Cloudsmith)
* Josef Šimánek (RubyGems/RubyGems.org)
* Maya Costantini
* Jonathan Velando (individual contributor; conda-forge feedstocks maintainer)

Agenda



* Need to get LF calendar invite sorted out - one meeting is LFX, the other is not
* [Jack Cable - 30 min] Package Manager Security Roadmap ([issue](https://github.com/ossf/wg-securing-software-repos/issues/16), [doc](https://docs.google.com/document/d/1mTdf9I4bShEeeQKE0urcQJtzHUSw15yOO6f9vzsUdOo/edit?usp=sharing))
    * There are some open questions on the doc - please review
    * Next step: get feedback from package managers!
        * Maybe open up to OpenSSF more broadly?
        * A public call for comment?
        * But maybe go public later
    * Questions
        * How to record multiple attestations per artifact on a Transparent Log like Rekor?
            * One solution is the package registry maintaining them
            * Another solution is to record a Bundle of attestations per artifact on Rekor in the first place
    * RubyGems is looking at a publishing policy - where should it be specified about hosting malicious code / defining security research?
    * Package namespacing resources:
        * [https://youtu.be/woGwOronU0g?t=1695](https://youtu.be/woGwOronU0g?t=1695) 
        * “Now because I'm showing you NuGet and this is like how we at Microsoft have protected ourselves from dependency confusion. NuGet actually has very specific guidance on this. They actually tried to solve this problem themselves.”
        * [https://github.com/NuGet/Home/issues/10566](https://github.com/NuGet/Home/issues/10566) 
* What does it mean to “own” or “sell” a package namespace?
    * Java and Go tend to link packages to a domain already
    * GitHub has a namespace policy with a path for handling if your trademark is taken: [https://docs.github.com/en/site-policy/other-site-policies/github-username-policy](https://docs.github.com/en/site-policy/other-site-policies/github-username-policy) 
    * Could selling namespaces fund package managers??
    * Actually, to use private packages in npm you do need a paid account (for publishing) [https://docs.npmjs.com/about-private-packages](https://docs.npmjs.com/about-private-packages) 
* [Trishank - 1m] [PackagingCon](https://packaging-con.org/) next week!
    * In person & virtual tickets: [https://ti.to/packagingcon/packagingcon-2023](https://ti.to/packagingcon/packagingcon-2023)

<h3>Oct 4, 2023| Securing Software Repositories (APAC-friendly)</h3>


Attendees



* Zach Steindler (GitHub, TAC)
* Marina Moore (NYU)
* Jeff Borek (IBM)
* Dave Lester
* André Arko (Ruby Central)
* Josef Šimánek (RubyGems/RubyGems.org)
* Kairo de Araujo (VMware/RSTUF)

Agenda



* Marina Moore ~~Mike Fiedler / Trishank Kuppusamy~~: T50 sinUF + PyPI: advancing [PEP 458](https://discuss.python.org/t/pep-458-current-status-and-next-steps-feedback-requested/17211/8) with [RSTUF](https://github.com/pypi/warehouse/pull/13943)
    * PEP 458 - when packages are uploaded to PyPI, they would automatically be signed
        * Different from developer signing, more like in addition to TLS
    * PEP 480 is more about developer signing; since it was written there’s been several developments with Sigstore
    * Trishank Kuppusamy: Want to hear feedback on how people might like to integrate SLSA (more generally, in-toto) and Sigstore with TUF, perhaps in [PEP 480](https://peps.python.org/pep-0480/)
    * Joseph Šimánek from RubyGems is also running some proof-of-concepts around RSTUF
        * André Arko also works on RubyGems, from North American timezone
        * RubyGems has reached out to Alpha Omega, are waiting to hear back
            * Give Alpha Omega some time! They are working through some bureaucracy, but are definitely interested.
            * Also working through a line of communication with Amazon
        * RubyGems would love to work with someone to put together a comprehensive security roadmap
            * RSTUF, Trusted Publishing, Sigstore proof-of-concept (although some open questions about including Rust code)
            * Ideally funding a full-time position for this work, instead of funding individual work items 
    * Can CDNs integrate with RSTUF to provide stronger protection than TLS?
    * We have 3 different approaches today with npm, PyPI, and RubyGems… and that’s okay! We don’t need everyone to do the same thing. At the same time, we want to learn from each other’s approaches.
    * Dana Wang is the new OpenSSF Architect, who could help us tie this information together.
* [15 min] Zach Steindler: Update / next steps on 	
    * Emailing when a package is published
    * RubyGems was the first to implement email domain expiration detection, which then was adopted by npm
* Dave Lester - welcome!
    * Helping out with PackagingCon in Berlin later this month
    * Reviving package manager maintainer Discord [https://package.community](https://package.community)
        * In particular, this community isn’t *just* about security (although obviously that’s one topic people care about!)
    * Interested in helping outreach and reach package managers

<h3>Oct 2, 2023 | Great Artifact Repository Audit</h3>


Attendees

* Chair: Zach Steindler
* William Woodruff (Trail of Bits)

Agenda

* Jonathan is currently out, but will be back later (October 20th?)
* William: Pre-sharing some audit results from ToB?
    * These audits have not been under the auspice of OpenSSF
    * Need to get approval from the orgs to share these
    * Will bring up again at the next meeting
* Repositories undergoing audit should be ready to receive findings and have time blocked off to respond to them
* Zach: Should this group be a sandbox SIG? Let’s discuss at the main working group meeting

<h3> Sept 21, 2023| OpenSSF Securing Software Repositories (EMEA-friendly) </h3>


Attendees:



* Chair: Zach Steindler
* Josef Šimánek(RubyGems/RubyGems.org)
* Jack Cable
* Trishank Kuppusamy (Datadog)
* Zachary Newman (Chainguard)
* Zhuoran Tan
* Cheng Lee (conda/Anaconda)
* Sam “Frenchie” Stewart (Ensignia)

Agenda:



* [15 min] Josef Šimánek: RubyGems [RSTUF](https://repository-service-tuf.readthedocs.io/en/stable/) plan, sponsorship, and current progress
    * Met maintainers a few weeks ago with an interest in applying to RubyGems
    * Needs to cover not only artifacts but also RubyGems metadata such as indices
    * PoC running locally on Josef’s machine
    * Planning to prepare a staging environment for RubyGems
    * Looking for sponsorship (maybe will ask OpenSSF for a grant)
    * Need to also work on the client side, then also integrate Sigstore
    * Alpha Omega has a link for submitting a proposal
    * And our repo has the proposal we submitted for Homebrew
    * A problem is that Python and Ruby cannot simply reuse native Sigstore clients written in, say, Rust
    * Could such fallback cases use an independent verification-as-a-service (like with [Hekate](https://github.com/trishankatdatadog/hekate))?
    * Will RubyGems use RS-TUF to also distribute indices?
    * Tentatively yes, because otherwise there could be some attacks against the indices, but for now, only testing against the artifacts
    * We may be able to outsource development of a universal client to contractors, but verification is very tricky business
    * Sigstore is open to ideas about how we can enable verification in every language
    * One idea is to write a Sigstore client in a policy verification language, whose engine can then be reimplemented across other languages
    *  ← spec for clients
        * How complex?
    * Could we bundle this into the _language_ itself?
        * Sounds like a pretty big ask IMO
        * Ruby = Ruby interpreter + stdlib
            * If you implement as a lib, it can get put in the stdlib
    * Trishank: this seems increasingly important, is Sigstore project doing anything about it?
        * Zach: [Roadmap: Integration into different Sigstore implementations · Issue #61](https://github.com/sigstore/sigstore-conformance/issues/61)
        * Zack: [ROADMAP.md - sigstore/community · GitHub](https://github.com/sigstore/community/blob/main/ROADMAP.md) 
        * Zack: Sigstore can dedicate resources once RubyGems articulates what they need
    * Josef: the challenge is getting verification _natively_ into the package manager
        * If we put verification burden on something else (e.g., a 3p tool) then gem could shell out or users could run the verifier themselves
    * Zack: A couple of variables to play with
        * Sigstore is interested in helping Ruby support a Rust FFI implementation and write a Ruby wrapper
        * Then we could also support a 3p Ruby Gem at the same time
    * Conclusion
        * For now, we’ll continue with Sigstore Rust FFI because we need it anyway (independent of Ruby)
        * For Ruby, we should try to do something “cheap” (easier than getting it in `gem` directly) to start
        * Then, if there’s demand we can talk about a pure-Ruby implementation or getting it into the Ruby stdlib
* [30 min] Zach Steindler: Can we put together a maturity model for securing package managers?
    * Help new (or existing) package managers put together a security roadmap (like [PyPI Fundable Improvements](https://github.com/psf/fundable-packaging-improvements/blob/master/FUNDABLES.md))
        * Guidance for package managers to build their own security roadmap
        * A menu ahead of time (“here’s what we can do if we had funding”)
    * Help with prioritization (e.g. you should probably do [trusted publishing](https://docs.pypi.org/trusted-publishers/) before [provenance](https://repos.openssf.org/build-provenance-for-all-package-registries))
    * Base it off of last year’s [Package Manager Security Landscape Survey](https://github.com/ossf/wg-securing-software-repos/blob/main/survey/2022/README.md)
    * Descriptive instead of prescriptive
        * “Here’s why we want to hash or sign” (instead of specific mechanisms or algorithms)
    * Other sources of inspiration
        * [AWS Security Maturity Roadmap](https://summitroute.com/downloads/aws_security_maturity_roadmap-Summit_Route.pdf) 
        * Lots of content in [this folder](https://drive.google.com/drive/folders/19rkJhu88XanJQUsoRXu8GJyjojcv-yeR) from this WG in the past
        * Zack N wrote this abortively: ["Package Manager Security Levels"](https://drive.google.com/file/d/12e5OgP3-XeThsmwcyyWX8THwiXzp7_CV/view?usp=drive_link)
        * [https://css.csail.mit.edu/6.858/2014/projects/aathalye-rhristov-viettran-qui.pdf](https://css.csail.mit.edu/6.858/2014/projects/aathalye-rhristov-viettran-qui.pdf)
        * OWASP effort: [https://github.com/OWASP/packman](https://github.com/OWASP/packman)
          
    * Looking for collaborators
        * Zack: There was a WIP guide that written in this group that we should continue
        * Identifying malware is another large lift for each ecosystem
        * First thing: We need to review the guide Zack mentioned
        * Zach will start a doc that we can async collab on
        * Trishank and Jack Cable are interested in collaborating

<h3>Sep 6, 2023 | OpenSSF Securing Software Repositories (APAC-friendly) (Canceled)</h3>


Notes



* This meeting has been canceled

<h3>Aug 28, 2023 | Great Artifact Repository Audit</h3>


Attendees:



* Zach Steindler (GitHub)
* William Woodruff (Trail of Bits)
* Jonathan Leitschuh (OpenSSF)

Agenda:



* Proposal living doc: 
    * Amir’s feedback from last time: focus on cloud security infrastructure, red team should come later and be out of scope of initial audit
    * Aeva: can we clarify scope?
        * Red team engagement?
        * CLI?
        * Package manager cloud infrastructure?
        * Fuzzers / other source-based audits
    * Jonathan’s initial motivation was seeing that a package manager never had a pen test, because it didn’t have paid customers (or other “market force”) requiring it to do so
    * What do we mean by pen test?
        * We’d prefer the auditing party to have access to source code, (read/view only) access to cloud accounts, etc.
        * Trail of Bits typically avoids the phrase “pen test” because of the baggage that’s associated with it. “Infrastructure audit” / “code audit” etc.
            * Pen test can often mean attempting to get access to physical resources
    * Aeva: recommend the terminology: “funded audit”, “code audit”
        * CNCF has good history here, around Kubernetes
* Amir (OSTIF) and Scovetta (Microsoft / AO) working on proposal / funding
    * Initial proposal was around doing everything at once
    * Now leaning more towards doing one, small, successful audit
* Jonathan’s request! Please review  and help suggest less adversarial language (especially “red team” and “pen test”).
* William: will the tests occur on a specific cadence?
    * Jonathan: yes, the current doc suggests redoing audits every 2 years
* Amir is presenting later today to Alpha Omega about doing this audit for Ruby Gems
* Amir: how are we thinking about red-team engagements?
    * Jonathan: it’s in the doc! We’d do the technical audit first, and then do red-team engagement as a follow-up
    * Aeva: many package managers are run by volunteers, and are frequently asked by outside parties to disclose their weaknesses and mitigation. This sort of thing needs to be build on trust!
* William: “dispassionate but involved member of the community”
* Zach: can we get a list of package managers we’ve talked to and where we’re at in the relationship?

<h3>Aug 24, 2023 | OpenSSF Securing Software Repositories (EMEA-friendly) (Canceled)</h3>


Notes



* This meeting has been canceled

<h3>Aug 14, 2023 | OpenSSF Securing Software Repositories: Great Artifact Repository Audit (SIG, proposing to be part of WG)</h3>


Attendees:



* David A. Wheeler (LF)
* Amir Montazery (ostif)
* Zach Steindler (Github)

Agenda:



* Scribe
  
    * 
* New faces
  
    * 
* One challenge: Jonathan L spun this audit SIG off, but it’s not been discussed much in WG (this meeting is NOT the WG)
* David A. Wheeler; I need a short description of “what’s been done” and “what we plan to do” to share with governments (at least the US White House, but i suspect others will want to know too). In part it’s to keep them informed, but we hope 
    * Let’s Create a Doc - I have good resources for this. 
    * [https://repos.openssf.org/](https://repos.openssf.org/) 
    * Supplemental information of this work in action
        * [https://ostif.org/the-ostif-2022-annual-report/](https://ostif.org/the-ostif-2022-annual-report/)
        * [https://ostif.org/the-ostif-independent-security-audit-impact-report/](https://ostif.org/the-ostif-independent-security-audit-impact-report/)
        * [https://ostif.org/the-audit-of-git-is-complete/](https://ostif.org/the-audit-of-git-is-complete/)	
* OSTIF is interested in doing audits
    * Less interested in red team - let’s start with lower hanging fruit first
        * David: agree, but let’s phrase this as “prioritized for later”
    * What are the 1-2 repositories who are ready for a cloud security audit?
    * OSTIF provides the people power, once funding has been allocated
* [Zach Steindler] Is Great Artifact Repository Audit a SIG?

<h3>Aug 9, 2023 | OpenSSF Securing Software Repositories (APAC-friendly) (Canceled)</h3>


Notes



* This meeting has been canceled

<h3>July 27, 2023 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>


Attendees:



* Th(independent)
* Seth Larson (PSF)
* Marina Moore (NYU)
* Kairo Francisco de Araujo (VMware)
* Martin Vrachev (VMware)
* Tobias Bieniek (crates.io / Rust Foundation)
* Trishank Kuppusamy  (Datadog)

Agenda:



* Scribe
    * Seth Larson volunteered
* New faces
    * Tobias Bieniek working on crates.io funded by Rust Foundation
    * Martin Vrachev working on supply chain security
*  Kairo Francisco de Araujo  [Repository Service for TUF (RSTUF)](https://github.com/repository-service-tuf/) Announcement (~20min)
    * Announcement at EuroPython 2023
    * TUF: Signing of artifact metadata and key management
    * Protects against packaging attacks (rollback, wrong install, bad data)
    * TUF is tough to implement, lots of operational cost repo-side. Not re-usable. Inconsistency due to processes
    * RSTUF born from PEP 458, abstract TUF spec complexity.
    * Draft PR for Warehouse integrating RSTUF [https://github.com/pypi/warehouse/pull/13943](https://github.com/pypi/warehouse/pull/13943)
    * Artifacts published to the repository needs to be added to RSTUF and distributed from RSTUF with artifacts.
    * RSTUF management process: guide users through the TUF management processes. Command line interface. Encodes the specifications’ processes into a guided flow.
    * Artifact agnostic, language agnostic, any release process.
    * Demo using in-dev warehouse
        * Publish a new artifact using Twine
        * Use pip to install a package, using verbose mode we can see the TUF metadata being used from the repository. Multiple packages contained within each metadata file.
        * What happens during repository compromise? Tampering with a package. Client will attempt to install a compromise package. Length mismatch.
    * Using RSTUF client is mostly sending HTTP requests.
    * Flow for TUF client:
        * Download metadata from TUF and know what to expect for hashes and length.
        * Download the artifact and compare the pre-fetched metadata.
    * Future plans
        * Flexibility on Key Vault and storage
        * Custom role delegation
        * Improved metadata management
        * Distributed signing (Geographic/offline)
    * Questions:
        * What is the status of the PR for Warehouse?
            * Waiting for the PyPI Safety Engineer to be hired to avoid
        * Complexity happened for Rubygems as well. When dealing with very large blobs, do you have to wait for the hash to complete before being able to give metadata?
            * The API for hashing is not exposed. Protection should be done at the repository and access to the RSTUF API.
        * What are the benefits of repositories adopting RSTUF when compared to Sigstore?
            * Received questions on using RSTUF with internal use-cases.
        * Slides
            * [https://onevmw-my.sharepoint.com/:p:/g/personal/kdearaujo_vmware_com/ETfzKpPXK6ZGuDnQO3R9S8sBGvQ1eaH66U6KXHEEjGzeCw](https://onevmw-my.sharepoint.com/:p:/g/personal/kdearaujo_vmware_com/ETfzKpPXK6ZGuDnQO3R9S8sBGvQ1eaH66U6KXHEEjGzeCw) 
* [Jacques] update
    * Resigning from the group, taking a new job and there isn’t space to work on repositories.
    * Update group charter list of contributors.
* AOB

<h3>July 17, 2023 | Great Repository Audit SIG</h3>


Attendees:



* Jacques Chester (independent)
* Jonathan Leitschuh (OpenSSF)
* Victor Lu (?)

Agenda:



* [Jonathan] A/O feedback:
    * Like the idea in general.
    * Breadth-first or depth-first approach? Brian thinks the depth-first approach might not justify the name “great repo audit”.
    * Jacques thinks we should take whatever we can get whenever we can get it
    * Continuation/expansion of list of questions
        * Come up with a “standard” for repos
* Victor: is there a pattern or guide for repo creators?
    * See: [https://github.com/ossf/wg-securing-software-repos/issues/16](https://github.com/ossf/wg-securing-software-repos/issues/16)
* Meeting concluded early

<h3>July 12, 2023 OpenSSF Securing Software Repositories (APAC-friendly) (Canceled)</h3>


Notes



* This meeting has been canceled

<h3>July 10, 2023 | Great Repository Audit SIG</h3>


Attendees:



* Jacques Chester (independent)
* Michael Scovetta (Microsoft / A-O)
* Jonathan Leitschuh (A-O)
* Amir Montazery (OSTIF)
* Brian Behlendorf (LF/OpenSSF)
* Victor Lu
* Seth Larson (PSF)

Agenda:



* Scribe
    * Jacques
* New faces
    * Brian Behlendorf
* Michael Scovetta: A-O update
    * Send email to other leads for buy-in. Hoping to hear back by tomorrow.
    * Given hypothetical list of repos, could OSTIF come back with estimate? 
    * Start with 1 per quarter.
    * Some ecosystems already have lists of work TODO, we could fund that first and then follow with audits.
    * Ensuring we know what particular questions should be asked/addressed
    * Let’s take it slow on red teams and publishing findings, worried about unintentionally antagonizing the community. Though we want to publish _something_ after engagements.
    * Jonathan: previously talked about 3/qtr, what brings it down to 1/qtr?
        * Let’s start slow and ramp it up. Just the audits could be done 3/qtr but we also need to fund remediation as well as competing A-O efforts.
    * Jonathan: how about cases where we wouldn’t need to fund remediation because corp-backed? Eg JFrog, Maven Central, Gradle Plugin Portal, Docker
        * Michael: not sure that A-O should be funding auditing commercial offerings. Would rather we engage with eg Docker to understand “have you had an audit? Could you get one if not?”
    * Jonathan: commercial may not have budget for A-O level of audit. These are “cost centers”, there’s weak incentive or pressure to be audited
        * Jacques: concerned about burning goodwill
        * Michael: worth having conversations with folks about why they haven’t done something? There’d be at least marketing value. Unless something legally precludes us dealing with eg. Docker, we can keep them on the table. But will prioritize non-commercial-backed repos. Matters mostly from optics perspective. If I were large commercial operation would feel silly taking funding from non-profit for this security work.
            * Jonathan: already have interest from orgs
            * Michael: let’s keep it on the table, but still think start with RubyGemses of the world.
    * Michael: keen to keep goodwill. Not sure would set hard deadline on disclosure (OpenSSF policy is 90 days)
        * Jonathan: the proposal is that non-for-profits get no disclosure deadline until we’ve gotten remediation; for-profits get the 90 day deadlines.
    * Amir: sharing some experience with this work. If intention is collaboration, most of work in audits is not just finding problems but to fix them. All OSTIF publications have been concurrent with fixed releases. Re: 90 days deadline - in engagements the goal is “make this better”, OSTIF has never had to wait 90 days. Usually remediation is done or nearly done when report finished (with one exception who asked for extension).
        * Jacques: Combination of audit and remediation?
            * Amir: We work with auditors who know OSS well. Want to not only find problems but willing to help maintainers fix them. In theory there could be cases where extra remediation is needed and we could do that kind of followup
        * Michael Scovetta: Distinguishing between code-level vulns (appsec) vs infrastructure (infrasec) and operational procedure risks. Some of the procedural improvements could take long, intensive engagements. Definitely ideal to have code level fixes happen throughout the engagement. Things like “server runs under disk” would take more time and money though.
            * Jonathan: goes to distinction of corporate-run and community-run repositories.
            * Amir: all those things are also considered.
            * Michael Scovetta: should be part of our list of questions. Corp-run probably won’t share but at least community-run. Overall we can be flexible and adapt.
    * Jonathan: original proposal was to 1st do pen test. Go through, find and fix vulns. 2nd phase, maybe different firm, do red team engagement / live attacker simulation (with prior notice and consent). Real attackers won’t scope to just code and infra, they will attack on more fronts eg. developer laptops. Is that still in view for A-O?
        * Michael: I think lower priority to red team vs pen tests. Recognise benefit of a red team exercise.
        * Jonathan: rationale was to do immediately, why the delay?
        * Michael: not intentional delay. We get value from each audit. Red teams are hella expensive (some discussion of what the range is). Don’t have a problem with the _concept_ of red team exercise on say multiple ecosystems for cost-effectiveness. We’re _kinda_ getting some researchers poking around.
        * Jonathan: but APTs are broader. One country in particular focused on cryptomining campaigns.
        * Michael: feel we should keep talking about red team but not include in initial batch of work.
        * Jonathan to Amir: could we get some idea of how much a red team would cost?
        * Michael: Concerned about doing red team against community without very careful legal arrangements.
            * Jonathan: hired firm would talk to community, A-O doesn’t own risk
            * Michael: different interpretation of risks
            * Let’s loop in LF legal
    * Jonathan: proposal has been emailed, will voting occur at tomorrow’s staff meeting? Will it have all stakeholders present?
        * Michael: vote might be but not guaranteed. Stakeholders will be present.
        * Jonathan: should I present the proposal during relevant meeting?
        * Michael: would appreciate both you and Amir presenting
        * Amir: suggest framing as “menu” as each engagement will probably be different
        * Jonathan: hopefully we can fully fund both parts for each engagement
        * Amir: would it be better to do two audits of different repos, or single repo for both audit and red team?
        * Michael: like the idea of menu

<h3>June 29, 2023 | Securing Software Repos WG (EMEA-friendly)</h3>


Attendees:



* Seth Larson (PSF)
* Jacques Chester (independent, chairing)
* Josef Simanek (RubyGems)
* William Woodruff (Trail of Bits)
* Myles Borins (GitHub / npm)
* Michael Scovetta (Microsoft / Alpha-Omega)
* Aditya Sirish (NYU, in-toto)
* Jenny Shen (Shopify)
* Matt Rutkowski (IBM)
* Zach Steindler (GitHub)
* Sterling Greene (Gradle)
* Kairo Francisco de Araujo (VMware)

Agenda:



* Scribe
    * Zach Steindler volunteers
* New faces
    * Aditya is interested in what this group is doing with in-toto
    * William has done quite a bit of work with PyPI at Trail of Bits
    * Luis is joining from JFrog
    * Seth is the new PSF developer in residence!
* [Jacques / Jonathan L / Michael S] update on audit SIG
    * SIG meetings are ongoing!
    * Discussing funding via AO
        * AO already has an audit with PyPI in scope
    * This work spans critical projects, best practices, securing repos, …
    * Could we target one ecosystem per quarter?
    * What about Drupal plugins, yarn, … want to balance ecosystem size with ensuring we aren’t overlooking anything
    * Code review, active pen-testing, … whatever’s needed
    * Questions around timing of pen-test / red team exercises
    * For ecosystems run by non-profits, we don’t want to overwhelm them with work items
    * AO engagement still under discussion
    * What are your top 3 ecosystems that want to participate in this?
    * Would we consider doing more of a SOC2-style policy audit vs more adversarial red team / pen test exercise?
        * Maybe! We definitely aren’t doing a SOC2 audit.
    * If there are known gaps, we could also figure out how to get those funded by AO.
        * The audit could still help us ensure our survey was accurate, and that we didn’t miss anything
    * Trail of Bits has audits planned for PyPI and Homebrew, both of which will be public
        * What’s the scope of this audit?
            * Codebase of package index and some infrastructure
                * Homebrew infrastructure in particular will be focused on their usage of GitHub Actions and Packages
            * We aren’t concerned about bugs in just the CDN, but something like request splitting in how a system interacts with the CDN.
        * Have you audited other artifact registries?
            * This is ToBs first artifact registry, we have audited kubernetes, openssl, curl, etc
        * Funded via Open Tech Fund - different from OSTIF
    * Have seen CLI tooling to registry authentication CSRF before
    * Please share ToB audit playbook!
        * ToB has seen lots of caching issues in CI, for example
    * Let’s use this WG to ensure we aren’t auditing the same ecosystem multiple times!
* AOB
    * [Zach Steindler] [Adding build provenance for all registries doc](https://github.com/ossf/wg-securing-software-repos/pull/17) 
        * Please bring this up in the APAC WG as well!
        * William is looking at adding build provenance support to Homebrew, and this document could help frame that discussion
        * It would be great to standardize the publish attestation (see above, also [https://github.com/in-toto/ITE/blob/master/ITE/9/README.adoc](https://github.com/in-toto/ITE/blob/master/ITE/9/README.adoc))
        * There are many other things we could attest to!
            * Malware scanning
            * Code review, possibly
            * We could then write policies based on these attestations
            * (Scovetta) Obligatory plug for [Assurance Assertions](https://oafdev1.westus2.cloudapp.azure.com/assertions/show?subject_uuid=0c6aa7ec-b271-4906-989a-4e32d1dcbba1).
                * Current lives in AO, but could be a collaboration
                * Could attach this context to the artifact via GUAC
            
![image](https://github.com/ossf/wg-securing-software-repos/assets/128058721/4395ac4e-0ede-4ef4-8b3d-66cad4c1b1c1)

* Intoto has anticipated this need, with a differentiation between attestation framework and predicates
* Let’s coordinate via this WG!
* “How do we do our security jobs on only one computer monitor?”
* Kairo Francisco de Araujo [Repository Service for TUF (RSTUF)](https://github.com/repository-service-tuf/)
    * Roadmap status
    * Relevant Project updates
    * Minimum working version: [https://github.com/orgs/repository-service-tuf/projects/2](https://github.com/orgs/repository-service-tuf/projects/2) 
    * Working on getting this project in use for PyPI: [https://github.com/pypi/warehouse/pull/13943](https://github.com/pypi/warehouse/pull/13943) 
    * Presented at Open Source Summit North America: [https://www.youtube.com/watch?v=O8zs4NnSR5w](https://www.youtube.com/watch?v=O8zs4NnSR5w) 
    * Will be presenting at EuroPython! [https://ep2023.europython.eu/session/pep-458-a-solution-not-only-for-pypi](https://ep2023.europython.eu/session/pep-458-a-solution-not-only-for-pypi) 
    * TUF will be used to distribute PyPI package signing public keys
        * This pattern should be applicable for any registry, not just PyPI 

<h3>June 26, 2023 | Great Repository Audit SIG</h3>


Attendees:



* Jacques Chester (independent)
* Lori Lorusso (JFrog)
* Josef Simanek
* Jonathan Leitschuh (Open Source Security Foundation)
* Zach Steindler (GitHub)
* Brian Moussalli (JFrog)

Notes:



* What do people want to discuss?
* New faces
    * Brian Moussalli from JFrog malware research team
* [Jonathan] What kinds of vulns do we want auditors to look for?
    * [List WIP](https://docs.google.com/spreadsheets/d/1bPjIa0L6kXPkhunRBj1PviP-aukgzwUzKntnZ0fx4ZY/edit#gid=0)
    * Focusing scope on app sec / infra sec vs single-package issues
    * Zach recommends [AWS Cloud Security Roadmap](https://summitroute.com/downloads/aws_security_maturity_roadmap-Summit_Route.pdf) and [Azure Roadmap](https://www.coffeehousecoders.org/blog/azure_security_roadmap.html)
    * What’s the remediation for social engineering?
    * Attacks on repo maintainers in scope?
    * Obfuscating results of red team to avoid finger-pointing
* Good background on SOC2: [https://securitycryptographywhatever.buzzsprout.com/1822302/11510254](https://securitycryptographywhatever.buzzsprout.com/1822302/11510254) 

<h3>June 22, 2023 | Great Repository Audit SIG</h3>


Attendees:



* Jacques Chester (independent)
* Lori Lorusso (JFrog)
* Jonathan Leitschuh (OpenSSF)
* Michael Scovetta (Microsoft)
* Seth Larson (PSF)
* Amir Montazery (ostif.org) 
* Victor Lu
* Jack K (ControlPlane)

Notes:



* Scribe
* New faces
    * Jack K (ControlPlane)
* Alpha-Omega Update
    * Very important to review repositories. Asked the group to prioritize 2-3 ecosystems. 
    * Those can be added to the set of targets for security work that AO is supporting.
    * Bug Bounty for ecosystems?
        * Possibly via IBB/HackerOne?
* [https://github.com/ossf/wg-securing-software-repos/issues/16](https://github.com/ossf/wg-securing-software-repos/issues/16) for work on whitepaper

<h3>June 15, 2023 | Great Repository Audit SIG</h3>


Attendees:



* Jacques Chester (independent)
* Jonathan Leitschuh (OpenSSF)
* Yesenia Yser (OpenSSF)
* Lori Lorusso (JFrog)
* Amir Montazery (OSTIF)

Notes:



* Scribe: Jacques
* New faces: n/a
* Doodle poll
    * 1pm Mondays ET is be the winner
    * Will publicize on slack, mailing list
    * Collides with staff / community meeting :[
    * 30 mins only
* Proposal is waiting on official A-O leadership approval. Affirmative vibe so far. Amir/OSTIF interested in running the process, Michael Scovetta will talk with him.
* Do we want to keep running the SIG or are we happy with handing off to OSTIF? How frequently do we want updates?
    * Jacques: don’t think we’ll need this SIG once OSTIF have the ball. Can report back to WG. Most work will be 1:1 b/w repos and OSTIF, no routed through WG
    * Lori: do we know who we will work with, who we will audit? What will be the benchmark we give to repos?
        * Jonathan: start with orgs who are willing to us. Once we run through those we can make a decision on what to do next. We can definitely create requirements of what we want to test.
        * Lori: would OSTIF be creating the benchmark to allow work in parallel?
        * Jonathan: inclined that we come up with benchmark, OSTIF focuses on operational emphasis. Plus better WG does it because knowledge/expertise
        * Jacques: repo survey gives us an idea of who’s done what already
    * Jonathan: creating [list of questions](https://docs.google.com/spreadsheets/d/1bPjIa0L6kXPkhunRBj1PviP-aukgzwUzKntnZ0fx4ZY/edit#gid=0)
        * Jacques: we shouldn’t create all of it, services will have standard offerings
        * Jonathan: yes but we will have _specific_ questions
        * General agreement and good spirits
        * Can use work by End Users WG ([threat model](https://docs.google.com/document/d/1lLCsT0a5vp6FcvquWPzx8AzhFMORyw-4rd9WSyUO9zI/edit#heading=h.gjdgxs), based on [paper](https://arxiv.org/pdf/2204.04008.pdf))
        * Jonathan: would ecosystem be prepared to help/share/propose questions?
            * Lori: we have a sec research team in Israel who may be able to help
* Amir joins
    * Jonathan: has Michael Scovetta talked to you yet?
        * Amir: not yet
    * Jonathan: if we hand to OSTIF, how much involvement/comms/meetings do you want or need?
        * Amir: don’t want to be keeping folks in the dark, will occasionally need help with outreach etc. 
    * Jonathan: alternative questions for cases like npm, where they had an internal audit and spun up a multi-year program of work in response to findings. What would we ask? Also questions that are unique to repos (eg CLI login flow). Do you know if pentest firms have standard questions that we can expand/amend?
        * Amir: think we have something. Eg. we work with one expert pentesting firm and OSTIF has lots of docs from working with them. So we have something to look at and augment. Will find and share previous questions.

<h3>Jun 14, 2023 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>


Attendees:



* Dustin Ingram 
* Zachary Newman (Chainguard)
* Marina Moore (NYU)
* Cesar Hernandez (Tomitribe)
* Jacques Chester (independent)
* Zach Steindler (GitHub, npm)
*  Trishank Kuppusamy (Datadog)
* Betty Li (Shopify)
* Victor Lu

Attached files:  

Notes



* Scribe: Zachary Newman
* New faces
    * N/A
* [Zach S] What would it look like for more systems to have fundable improvements, like [https://github.com/psf/fundable-packaging-improvements/blob/master/FUNDABLES.md](https://github.com/psf/fundable-packaging-improvements/blob/master/FUNDABLES.md)
    * [zach s] Context: discussion from two weeks prior about the purpose of this WG
        * The WG has no power to assign work! (and we don’t want to burden maintainers)
        * Great Repository Audit is a great example of turning OpenSSF funding into meaningful security improvements
        * Are there other ways?
        * PSF has been good about keeping a list of [FUNDABLES](https://github.com/psf/fundable-packaging-improvements/blob/master/FUNDABLES.md), which has led to actual work!
        * Can we do that elsewhere?
    * [dustin] Experience with FUNDABLES list (as a co-creator)
        * Wrote down biggest, nice-to-have projects that are too big for volunteer maintainers
        * It worked really well: explains why something hasn’t been done yet, useful in communicating with funders 
        * Though funders haven’t really “ordered off the menu”, it’s more of a starting point
            * Haven’t been able to check things off the list 
        * If doing again, would do it as a GH repo with issues, rather than a big Markdown doc (to enable discussion)
    * [dustin] Can we put together fundable improvements for specific ecosystems?
        * Any list should have buy-in from folks in that ecosystem
        * Ex. Bringing Npm provenance attestations to other ecosystems would be a fair bit of work
        * That experience (how long? Any challenges?) can inform estimates of effort
    * [marina] TUF integrations/ecosystems
        * We’ve learned some things to make process better
        * Also: tooling/usability improvements
    * [zjn] Certainly a place for per-ecosystem fundables
        * Also there are cross-cutting issues, e.g. bringing TUF to an ecosystem vs. documentation for _all_ TUF implementations
        * I have specific fundables in mind 🙂
    * [jacques] is there a fundables table/matrix? Can we reuse fundables across ecosystems?
        * Base this on the survey?
        * Central clearinghouse for funders? Some might prefer specific tech, some might be interested globally
    * [zach s] in great repository audit, might be easier to start with _one_ ecosystem rather than trying to solve everything at the same time
        * Two-sided marketplace: you need repository to be interested, and a funder to fund
        * Can we identify a particular ecosystem to go through the fundables exercise on their own as a test case?
    * [dustin] Prior art would make this more attractive to funders
        * “Python wants to do build attestations? It’s already succeeded in npm” is a much easier case
    * [zach N] Will echo Zach S’ point: shouldn’t block / require changes in any ecosystem based on others
    * [jacques] concreteness helps
        * Different funding models: even “here’s money, we’d like it to be spent on security, but it’s up to you” takes 
    * [zach s] volunteers to help run an ecosystem through this
    * [dustin] i’d be interested in teasing out packaging security stuff from the existing Python list
    * [zjn] another test case (cross-cutting)
        * Sigstore FFI bindings
            * This would enable sigstore-hs, which in turn enables Nix adoption of Sigstore for build signatures 
* [Zach S] (FYI) [https://docs.docker.com/build/attestations/](https://docs.docker.com/build/attestations/)
    * Provenance attestations with in-toto predicates
    * [dustin] how does this compare with NPM/SLSA/in-toto provenance attestations?
        * [zach s] npm has build attestations (more like standard in-toto), publish attestations (more made-up)
        * [trishank] Docker also produces CycloneDX attestations
        * [zach s] we should try to more rigorously figure out what belongs in these attestations. (but not yet, waiting on Frederik / Philip Harrison0
        * [marina] in-toto has a proposal for new standardized attestation types ([ITE-9](https://github.com/in-toto/ITE/blob/master/ITE/9/README.adoc))
        * [zach s] does anyone know whether the docker build attestations include publish attestations?
        * [trishank] I think you’re right, just SLSA and SBOM (CycloneDX)
        * [jacques] should we get the SLSA group involved?
            * [marina] let’s ask in the SLSA channel
        * [dustin] should we pull someone from docker in?
            * [jacques] good that these docs are self-serve
            * Zach s - Could reach out to Justin Chadwell at Docker: [https://www.docker.com/blog/generate-sboms-with-buildkit/](https://www.docker.com/blog/generate-sboms-with-buildkit/) 
        * [trishank] the Docker attestations seem to be using v0.1 of in-toto attestations
        * [zjn] My understanding is there’s a generic mechanism for attaching things to container images, the artifact is an output of the build process
            * [zach s] seems to not  be using OCI reference types from OCI 1.1
* [Dustin] [cargo-vet](https://mozilla.github.io/cargo-vet/) for your ecosystem?
    * Background: cargo vet is tooling for requiring/checking audits of source code and reporting audits in a standardized way
        * Supports different categories of audits (defined by the publishing team)
        * No notion of integrity/identity/verification 
    * [jacques] Previous issues: going through github, other companies a little trepid about attaching their name to public statement
        * Is a transparency log appropriate here? Centralization, rather than distributed across various repositories
        * Do we need a “no warranty” clause?
        * Need for bitemporality/history: did we make the right decision at time T?
        * It’s likely that there could be convergence on a standard policy.
        * [dustin] regarding trepidation: [https://opensource.googleblog.com/2023/05/open-sourcing-our-rust-crate-audits.html](https://opensource.googleblog.com/2023/05/open-sourcing-our-rust-crate-audits.html) 
            * Chrome and Fuschia teams are both publishing audits!
    * [dustin] Discovery: should we be attaching audits next to the artifacts themselves?
    * [Trishank] Could we introduce a standardized in-toto attestation for “vetttastations”?
        * [from marina, above] in-toto has a proposal for new standardized attestation types ([ITE-9](https://github.com/in-toto/ITE/blob/master/ITE/9/README.adoc))
    * [dustin] How does this relate to malware?
        * PyPI is trying to standardize the way third parties report malware. Attestations are a good candidate for that format
            * Coming soon!
* [Jacques] Notary seems to be on the move (seen via [AWS](https://aws.amazon.com/about-aws/whats-new/2023/06/aws-container-image-signing/), more details [in blog post](https://aws.amazon.com/blogs/containers/announcing-container-image-signing-with-aws-signer-and-amazon-eks/))
    * Background: _Does_ use OCI 1.1 reference types
    * [zach s] can CI _and_ CD both support a notion of workload identity?
    * [zach s] AWS is a platform that adopts lots of overlapping options and lets customers decide
        * They have lots of secret stores, HSMs, KMS
        * Might be a different use case: very AWS-focused workflows, not necessarily applicable to OSS use case
* [all] Brainstorming fundable security improvements
    * [zach s] npm has enumerated [threats and mitigations](https://docs.npmjs.com/threats-and-mitigations). Maybe this is a useful model/frame for fundables? 
        * [jacques] also [supply chain taxonomy](https://arxiv.org/abs/2204.04008). Has been adopted by end users WG
    * Malware: uploading malicious packages (“spam” malware vs. “compromise” malware)
        * Standardized reporting API
        * Tooling to simplify verification & takedowns
            * What’s the workflow (with “vettestations”)?
                * Report to repository directly
                * There had been some interested in doing this with OSV, but malware is a little out of scope
        * Build provenance
            * Verifiable links to source enable some malware detection techniques!
    * API keys: downscoping, using for publish flows
        * Fine grained API tokens
        * “Trusted Publishing” (OIDC-based token exchange)
    * Account takeover / recovery / resurrection attacks
        * [HIBP](https://haveibeenpwned.com/) API: make users reset their password if it’s been seen in a breach
            * Could be part of a larger “account takeover” mitigation effort
        * Domain resurrection attacks
            * Regular job to use [Domainr](https://domainr.com/) API, locks accounts with expired email domains
        * 2FA
            * [jacques] distinguish between TOTP vs. tokens/passkeys / WebAuthn
                * Upgrading from TOTP to WebAuthn could be a project
                * [dustin] PyPI did a fundable for 2FA (both TOTP/WebAuthn)
            * [dustin] Support for 2FA mandate/rollout
                * Funding can help with docs, comms, logistics
                * Defining account recovery process when 2FA lost
        * Implementation of Secret/token scanning partnerships
            * [https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning) 
            * [https://docs.gitlab.com/ee/user/application_security/secret_detection/](https://docs.gitlab.com/ee/user/application_security/secret_detection/) 
    * Vettestations
        * Cargo-vet for an ecosystem?
    * Vulnerabilities
        * Vulnerability auditing tooling?
* [dustin] working group’s high-level recommendations of “things repositories should do”
    * Do this _before_ pushing fundables 
    * [zach s]: lots of value in maturity model / whitepaper
        * SLSA has had a lot of impact: pretty easy to understand
    * [zjn] proposed [cryptographic signing guide](https://github.com/ossf/wg-securing-software-repos/issues/10) is a subset

Action items



1. Dustin - find SLSA rep for next meeting
2. Zach S: reach out to Justin Chadwell at Docker, invite to this meeting
3. Zjn: fundables for sigstore FFI
4. ?? - Read [ITE-9](https://github.com/in-toto/ITE/blob/master/ITE/9/README.adoc)
5. Marina  - Reach out to in-toto folks, invite to next meeting
6. ZJN - file an issue in the WG repo w/ source material, turn brainstorm into doc in WG repo

<h3>June 8, 2023 | Great Repository Audit SIG</h3>


Attendees:



* Jonathan Leitschuh (OpenSSF / Alpha-Omega)
* Amir Montazery (OSTIF)
* Jacques Chester (independent)
* Arnaud J Le Hors (IBM)
* Nils Adermann (Composer/Packagist)
* Randall T. Vásquez (LF/SKF/Gentoo)

Apologies:



* Jacques will need to leave early

Agenda:



* Scribe
* New faces
    * Amir from OSTIF
* Discussion of [The Great Artifact Security Audit](https://openssf.slack.com/files/U01LYFRTSQ7/F0595TSF2TA/the_great_artifact_repository_audit) proposal from OSTIF POV
    * Overall makes sense. Some engagements might not need all the things, might be nice to cater/customize to particular repos.
    * What’s next? What are missing?
        * Amir will do a deeper dive and give feasibility feedback based on OSTIF experiences
        * Nils Adermann might know some PHP folks
    * What kind of work has OSTIF done?
        * A mix of things. Mostly code review but done a variety.
    * A-O thinks it can chip in half - Would OSTIF be able to chip in?
        * Basically no, OSTIF runs very lean
    * What would it look like to run audits regularly? What kind of resources / time would that require?
        * OSTIF’s value is helping manage throughout the whole process. Potentially OSTIF could do active management of regular audits.
        * Assuming 4 engineer-weeks, approximately 2 management-weeks of effort (1 week at start and end).
    * So does it make more sense to fund OSTIF and not try to allocate someone from OpenSSF?
        * Plausibly yes. Collaboration helps a lot. 
    * What kind of ongoing infra will this require? Given that the output is the analysis.
        * Easy to assume that but OSTIF has found every piece of the puzzle is important. What the needs of the project are, scoping, talking to the right people, lots of back-and-forth. But yes bulk of the security work happens in the audit itself.
        * Competitive bidding oversight makes a big difference - example of bringing $206k down to $120k.
    * The assumed $150k/engagement, would that include OSTIF overhead?
        * Would be all-inclusive, OSTIF takes a small management fee.
    * When repeating (say every 2 years), how much can previous work be leveraged?
        * Yes. Followup work tends to be cheaper because a lot of upfront work is done, and because there’s a smaller delta to be reviewed.
    * For community-run repos like PyPI, RubyGems etc we’d handle them differently from larger corp-backed offerings. Including paying for a contractor to remediate findings. Can OSTIF help?
        * Yes, have done before. OSTIF process also doesn’t like to dump giant list of problems. Collaboration essential. Audit teams report as they go and work with project team on how to remediate. On almost all engagements work has led to new releases.

<h3>June 1, 2023 | OpenSSF Securing Software Repos (EMEA-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=pQkXFPQpV0U)

Attendees:



* Jacques Chester (independent) [chairing]
* Josef Simanek (RubyGems.org)
* Zach Steindler (GitHub; OpenSSF TAC)
* Jenny Shen (Shopify)
* Myles Borins (GitHub / npm)
* Randall T Vasquez (LF/Gentoo/SKF)
* Nils Adermann (Packagist / Composer)
* Sterling Greene (Gradle)
* Lori Lorusso (JFrog)
* Adam Browning (JFrog)
* Zohar Sacks (Jfrog)
* Avishay Balter (Microsoft)
* Jonathan Leitschuh (OpenSSF)

Apologies:

Agenda:



* Scribe - Lori
* New faces
* [Jacques] PyPI announces [universal MFA policy](https://blog.pypi.org/posts/2023-05-25-securing-pypi-with-2fa/)

  No one from PyPI on the call


  Looking for feedback on how this process goes


  Hoping this makes it easier for all package types to get MFA rolled out


  Shared Help Desk - around account recovery

* How can this group help all users enable MFA and make it easier
* What does this mean towards malicious packages and remediation practices
* Apple requires 2 hardware tokens - backup - is this something to look out for MFA

  * Nils - MFA doesn’t work well for shared email to access account 



* Hard to get adoption bc things work well now - MFA there but not required

  * Myles - npm - does not have ability to prioritize short lived tokens



* Have 2 package types that work around MFA
* Lots of requests for account access support - huge workload significant for support - very tough process to get access to avoid people stealing credentials
* It's a people problem - they do what they want - if an account can’t be recovered it is due to the person not being able to authenticate on their side
* [https://docs.npmjs.com/threats-and-mitigations#account-takeovers](https://docs.npmjs.com/threats-and-mitigations#account-takeovers) 
* [Jonathan Leitschuh]
  
  * Sent out emails to all security emails associated with a ton of package ecosystems
  * Most likely services haven’t had Pen tests bc community run or not $$$ making (for more deets read the doc) & Red Team engagements
  * Open up the convo about what impact this had on the package ecosystems
      * Publish reports and fixes
  * OpenSSF will offer to pay for it (maybe Alpha Omega & other funding source & OSTIF)
      * Check vulnerability disclosure CAVEAT 
  * Zach - OpenSSF $$$ actually being used to help secure package management ecosystem - but is the process solid?
      * Wants to work with teams that manage repositories w/high level scope of what they need for security - risk assessment, use their list of issues and use this to deliver security improvements
      * Nils - sounds good but need both to have oversight on things that may have been missed by the package ecosystem - creates a solid foundation to move forward having both views of the security system issues
  * Myles - npm - an internal team did an audit - security experts paired directly with npm engineers - results of audit multi-quarter effort to revamp almost everything bc the list of enhancements and improvements is massive 
      * OpenSSF - making assumptions based on old architecture which may not be appropriate for each package
      * Larger convo needs to be had based on roadmaps 
  * Lori - we should talk to package types and have a checklist that shows that they are inline with the audit to be ‘secure’
      * Like a badge or something 
  * Jaques - first wave voluntary - do not want to burn goodwill
      * Show the results of tests done and then return back to package
  * Nils - make it an offer and not a requirement - focus on the ones that need it
      * Zach - lets not mandate this - lets run with a few and determine how to increase the scope of the project
  * Myles - this can be done to help level the playing field for security
      * Need to have more conversations on levels of compliance, ongoing expectations. Etc.
      * We want the win but may need to separate and work on independently
  * Jonathan - have a common understanding of what was done in the Audit - standards for achieving the tier of acceptability
  * See you at the next SIG MEETING :)
* [Zach] (meta) what would people like to get out of this working group?
        * Forum for registries to learn best practices and learn from each other
        * Establish common criteria -security/accessibility- and drive ecosystem to those
    * Jonathan - we need something to keep people coming back 
    * Jacques - not a governing group, recommendations/best practices, open ended conversations
        * Everyone short on bandwidth - the audit assigns people to do this and its not on maintainers 
        * Audit can lead to more convo and more commonalities in problems/solutions
    * Zach - documentation in bite size pieces
    * Myles - appreciates the conversation and sharing 

Next meeting APAC timezone - check the calendar 

	



* [Zach] What would it look like for more systems to have fundable improvements, like [https://github.com/psf/fundable-packaging-improvements/blob/master/FUNDABLES.md](https://github.com/psf/fundable-packaging-improvements/blob/master/FUNDABLES.md)
* [Zach] (FYI) [https://docs.docker.com/build/attestations/](https://docs.docker.com/build/attestations/)

<h3>May 25, 2023 | Great Repository Audit SIG</h3>


Attendees:



* Jonathan.Leitschuh (OpenSSF)
* Yesenia Yser (OpenSSF, Alpha-Omega)
* Michael Scovetta (Microsoft)
* Lori Lorusso (JFrog)
* Jacques Chester
* Brian Fox (Sonatype)
* Munawar Hafiz (OpenRefactory)

Apologies:

Agenda:



* Discussion of [The Great Artifact Security Audit](https://openssf.slack.com/files/U01LYFRTSQ7/F0595TSF2TA/the_great_artifact_repository_audit) proposal.

<h3>May 17, 2023 | OpenSSF Securing Software Repos (APAC-friendly)</h3>

  [Recording](https://youtu.be/95BU8dJW1nE)


Attendees:



* Mihai Maruseac (Google)
* Jacques Chester (Independent)
* Zach Steindler (GitHub)
* Josef Simanek (RubyGems)
* Sterling Greene
* Betty Li (Shopify)
* Jonathan Leitschuh

Apologies:

Agenda:



* [ZS] CISA / Jack Cable
    * Panel discussion at OpenSSF day with Brian Behlendorf and USG reps. One was Jack Cable. Quite interested in question of how USG could help security of package managers.
    * JACK.CABLE@cisa.dhs.gov 
* [ZS] Provenance promulgating
    * ~1mth from public beta of provenance in npm. Close to announcing another CI/CD vendor supporting provenance.
    * A major roadblock is Sigstore library implementation. Jacques spent some time looking into using sigstore-rust (with CFFI bindings) in Ruby Gems, but hadn’t yet come to a conclusion about if they should ship a binary or what that would look like
    * See [https://github.com/npm/cli/pull/6375](https://github.com/npm/cli/pull/6375) for an example of provenance implementation in the CLI
* [Jonathan Leitschuh] Proposal: “The Great Repository Audit”.
    * When buying vendor there’s a lot of due diligence and vendor scrutiny. But probably most software repos have never had these requests/audits because they’re free and open services.
    * OpenSSF, funded by Alpha-Omega, go out to software repos and ask if they can provide pentests. If not they would hire firm to perform pentest on repo’s behalf.
    * Spoke to Amir from OSTIF. Price circa $150k for 4-8 person-weeks of effort.
    * Zach: is the goal that an audit happens, or to publish?
        * JL: yes to both. Audit happens, vulns fixed, results published.
    * Zach: what about sensitive findings?
        * JL: most firms will focus on web app testing, but repos have CLI and other components.
    * Jacques: orgs are mostly volunteers. Maybe not disclose until fixed?
        * JL: high-level OpenSSF disclosure policy would apply to repos backed by large orgs. Repos hosted/run on community basis.
    * Zach: category of security risk mentioned before - cloud infrastructure. It would be good if folks cribbed PyPI’s idea for “[fundable security improvements](https://github.com/psf/fundable-packaging-improvements/blob/master/FUNDABLES.md)”. Often the difficulty is not finding risks, it’s bandwidth to fix the risks.
        * JL: maybe for community-driven we will do the audit and maybe also hire a contractor to help fix the issues.
    * Zach: other feedback, social pressure from audited to non-audited ecosystems. My primary objective is to keep available and secure. Concerned giving attackers a prioritized list of weaknesses.
        * JL: carrot/stick. If you want to audit, great. If you don’t we may do it anyway. Eg. npm has a safe harbor provision.
        * CSV file of repo policies: [https://github.com/ossf/wg-securing-software-repos/pull/13](https://github.com/ossf/wg-securing-software-repos/pull/13)
    * Jacques: would prefer carrot-only for now, save stick for someone else to wave
    * Zach: what is the pathway from the proposal to reduction in risk? (paraphrased) Eg. npm where repo is closed-source, what would the approach be?
    * Jacques: is there an action or is this informative?
        * JL: don’t want to write doc solo, so one preference is to have the WG meet more frequently to get faster feedback.
        * Zach: if there isn’t already could we find a single package manager to act as reference stakeholder.
        * JL: “Adam” said Gradle is working on new system and intending to get pentest soon, could it be public? Said yes, should be OK. Brian Fox from Maven Central says they had a pentest a while ago, probably will revisit. Less willing to share.
    * Zach: number of folks we’ve talked to in Python, Rust, C++ ecosystems I could connect you to.
        * JL: Also messaging with NuGet folks.

<h3>May 4, 2023 | OpenSSF Securing Software Repositories(EMEA-friendly)</h3>

 [Recording](https://youtu.be/8ZTIS0Q0tDE)

Attendees:



*  Zachary Newman
* Josef Simanek (RubyGems)
* Joshua Lock (Verizon)
* Jacques Chester (chair)
* Cheng H. Lee (Anaconda/conda)
* Avishay Balter (Microsoft)
* Randall T. Vasquez (LF/Gentoo)

Apologies:

* 

Agenda:



* Jonathan L spoke to Alpha-Omega leadership about repo pen testing. Whether it would be valid for Alpha to pay for audits/pentests? Would like to review proposal
    * Suggestion to go through OSTIF (Amir)
* [Cheng] [PackagingCon 2023](https://packaging-con.org/): 26th to 28th of October in Berlin, Germany
    * CFP should be out in the next week or so
* [Josef] letting folks RubyGems is working on OIDC-to-token flow
* Switch to working session on A-O

<h3>Apr 19, 2023 | OpenSSF Securing Software Repositories (APAC-friendly) (Canceled)</h3>


Attendees:



* Chair: Jacques Chester (Shopify)


Apologies:



* Dustin Ingram (Google)
* Zachary Newman (Chainguard)

Agenda



* **Canceled due to lack of agenda today**

Action items

1. 

<h3>Apr 6, 2023 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://youtu.be/IMIof5Zottc)

Attendees:



* Sterling Greene (Gradle)
* Jussi Kukkonen (Google)
* Jacques Chester (Shopify) [Chairing]
* Josef Simanek (RubyGems)
* Radoslav Dimitrov (VMware)
* Jack K (ControlPlane)
* Randall T. Vasquez (SKF/Gentoo)

Apologies:



* Zachary Newman (Chainguard)

Notes



* New (and returning) faces!
    * Jonathan returning
    * Radoslav working on TUF
    * Jack K returning
* [Jacques] Our next report to TAC is 18th April
* [Jacques] [NPM publish attestation](https://github.com/npm/attestation/tree/main/specs/publish/v0.1)
* [Jacques] Who are folks using as their CNAs? (asked by Madison Oliver)
    * Josef: openwall security list ([https://www.openwall.com/lists/oss-security/](https://www.openwall.com/lists/oss-security/))
    * Jacques: Github?
        * Jonathan: only issued to maintainers. I usually ask Snyk.
        * Jussi: from maintainer perspective GH was painless
* Any other business
    * Jonathan: Gradle dep extractor plugin. GH never tried to make a dep graph for Gradle because it is Turing-complete. New plugin will capture/extract deps as they are resolved and sent to GH API.
        * Sterling: next week at conf will give update on sigstore support for Java/Gradle[https://cfp.devoxx.fr/2023/talk/KTB-9633/Securite_de_la_chaine_logicielle_avec_Sigstore](https://cfp.devoxx.fr/2023/talk/KTB-9633/Securite_de_la_chaine_logicielle_avec_Sigstore) (in French)
    * Jonathan: repositories often don’t have security audits
        * Jacques: what about Alpha-Omega?
        * Josef: there’s at least bug bounties
            * Jonathan: federal law (CFAA) makes it risky to perform unauthorized audits, so bug bounty doesn’t have full coverage
        * Jack: difference between centralized repos like RubyGems vs decentralized repos like Arch mirrors.
            * Jonathan: all in scope, eg CDN cache poisoning
            * Jack: so even Golang would be in scope, wonder if Go repos in safe harbour
    * Any news about [Packaging Con](https://packaging-con.org/)?
        * Not at the moment.

Action items



1. 


<h3>Mar 22, 2023 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://youtu.be/1t1pX32fgrQ)


Attendees:



*  (Chair)
* Zachary Newman 
* Cheng Lee (Anaconda)
* Jacques Chester (Shopify)
* Trishank Kuppusamy (Datadog)
* Jerimiah Willhite (Anaconda)
* Andrew Pollock (Google)
* Henri Yandell (AWS) (late peek into meeting as it ended)

Apologies:



* Dustin Ingram (Google)

Notes



* New faces!
    * Jerimiah Willhite from Anaconda, focused on SBOMs and CVEs
    * Andrew from Google OSST, working on OSV doing CVE conversion work
* [dustin] [https://github.com/slsa-framework/slsa/pull/673](https://github.com/slsa-framework/slsa/pull/673) 
    * SLSA standard for how build provenance will be distributed by software repositories
    * Please read/review/comment!
    * This will be included in the v1.0 RC2 release candidate, so still some time to adjust before v1.0 is finalized
    * Trishank: how would one verify attestations? E.g. which keys to use for attestations?
        * Zack: my thinking is that it’s deliberately non-descriptive. Requirements will vary based on how it gets deployed. “Signing” (aka authorial attestations) vs provenance attestations. Ideal supply chain has attestations as a component. Fetch policy for attestations from something like TUF etc; there’s an end-goal “dream” in mind but we don’t want to hold up everything to nail down the formats. Hunch is that there’s no “one size fits all”.
        * Trishank: Possible bifurcation?
        * Jacques: could you elaborate?
        * Trishank: might just happen accidentally as folks work in this problem area.
        * Zack: this effort is in part to avoid proliferation but for now every package manager for themselves. Once we have some examples we can generalize. Early movers are talking together here. Ideally verification policy would be language-agnostic. Bifurcation in formats would be bad, implementations not a concern.
        * Trishank: so my rough understanding is “let’s start and iterate” with build attestations, then source, then package registry attestations, and so on. Eventually in-toto policies to tie it all together.
        * Zack: yes, perhaps in-toto can be the thing that ties it together. If in-toto understands that provenance format then we’re in good shape. Question remains of how to get the layout?
* [Jacques] Packaging Con
    * [https://packaging-con.org/](https://packaging-con.org/)
    * October 26th to 28th, 2023 in Berlin, Germany
* Any other business

Action items



2. 



<h3>Mar 9, 2023 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>


Attendees:



* Chair Jacques Chester 
* Zach Steindler (GitHub)
* Zachary Newman (Chainguard)
* Sterling Greene (Gradle)
* Jussi Kukkonen (Google)
* Josef Simanek (RubyGems/RubyGems.org)
* Matt Rutkowski (IBM)
* Avishay Balter (Microsoft)
* Lois Anne DeLong (NYU)

Agenda



* New friends!
    * Avishay Balter (MS)
* Final reviews/merge for ​​[https://github.com/ossf/wg-securing-software-repos](https://github.com/ossf/wg-securing-software-repos)
    * Did we mean: [https://github.com/ossf/wg-securing-software-repos/pull/12](https://github.com/ossf/wg-securing-software-repos/pull/12) ?
    * Potential blog post?
* AOB
    * PyPI OIDC publishing, Zach Steindler interested in progress.
        * [https://github.com/pypi/warehouse/issues/10619](https://github.com/pypi/warehouse/issues/10619)
        * [https://github.com/pypi/warehouse/projects/4#card-81167419](https://github.com/pypi/warehouse/projects/4#card-81167419)
    * Jussi says being worked on actively
    * Open issue [https://github.com/ossf/wg-securing-software-repos/issues/10](https://github.com/ossf/wg-securing-software-repos/issues/10) for discussion

Action items



1. Jacques to contact Jennifer about blog post


<h3>Feb 22, 2023| OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=w6Rte7Mw5yM)

Attendees:

* Dustin Ingram (Google)
* Jacques Chester (Shopify)
* Chris Lamb (Reproducible Builds & Debian)
* David A. Wheeler (Linux Foundation)

Apologies:



* Brandon Lum (Google)
* Zach Steindler (GitHub)

Agenda:



* Intros / new friends
    * Victor Lu
    * Noah (Open University). Researching OSS vulns and software
    * Ryan Ware (Intel). 
* [Brandon Lum (unable to attend)]: opened up this PR [https://github.com/ossf/wg-securing-software-repos/pull/12](https://github.com/ossf/wg-securing-software-repos/pull/12) (from previous action item on survey), would like to get eyes/reviews on it. Based on reviewed material by group with minor edits.
* [dustin] npm provenance beta is now available: [https://github.com/gh-community/npm-provenance-private-beta-community](https://github.com/gh-community/npm-provenance-private-beta-community) 
    * Email GitHub & npm username to Steiza @ Github .com  for access
    * Public beta is on our roadmap before end of March: [https://github.com/github/roadmap/issues/612](https://github.com/github/roadmap/issues/612) 
    * Generally available before end of June: [https://github.com/github/roadmap/issues/657](https://github.com/github/roadmap/issues/657) 
* [dustin] SLSA moving to a 1.0 release of the spec: [https://github.com/slsa-framework/slsa/issues/497](https://github.com/slsa-framework/slsa/issues/497)
    * RC 1 coming soon: [https://github.com/slsa-framework/slsa/issues/606](https://github.com/slsa-framework/slsa/issues/606) 
* [Josef] Security of package executables
    * New “gem exec” command [https://github.com/rubygems/rubygems/pull/6309](https://github.com/rubygems/rubygems/pull/6309)
    * Looking for experiences and security lessons from other ecosystems
        * Python equivalent: [https://pypi.org/project/pipx/](https://pypi.org/project/pipx/) 
* [Josef] Ingesting package content
    * Opening up gems to extract contents and store, process etc
    * Any experience to share? [https://github.com/rubygems/rfcs/pull/44](https://github.com/rubygems/rfcs/pull/44)
    * Security scanning, code search, … any recommended storage?
* [dustin] PyPI OIDC-based publishing moving into private beta
    * [https://github.com/pypi/warehouse/issues/12965](https://github.com/pypi/warehouse/issues/12965) 
    * Sign up here: [https://forms.gle/XUsRT8KTKy66TuUp7](https://forms.gle/XUsRT8KTKy66TuUp7)  
* Any other business?
    * Victor: a lot of OpenSSF stuff is cutting edge and tricky for users. CIS has an idea of groups of controls.

<h3>Feb 9, 2023 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=mYQesmMGack)

Attendees:



* Zack Newman (Chainguard)
* Nusrat Zahan (NCSU)
* Sterling Greene (Gradle)
* Brian Fox (Sonatype)
* Trishank Kuppusamy (Datadog)
* Myles Borins (GitHub)
* Laurie Williams (NC State)
* Josef Simanek (RubyGems/RubyGems.org)
*  Kairo Francisco de Araujo (VMware)
* Arnaud J Le Hors (IBM)
* Radoslav Dimitrov (VMware)
* Jonathan Leitschuh
* Randall T. Vasquez (Gentoo/SKF)

Apologies:



* Jacques Chester (Shopify)

Agenda:



* Intros / new friends!
    * Laurie Williams (NC State University)
    * Nusrat Zahan (Laurie’s student)
        * Myles loves their work on npm/GitHub: [https://arxiv.org/abs/2112.10165](https://arxiv.org/abs/2112.10165) 
* [Kairo] RSTUF
    * Making good progress
    * Hoping to ping PyPI/upstream again soon
* [zjn / nusrat] (maybe) updates on data repository proposal
    * In process of writing
    * Other people seem to want this
    * Easiest to scrape npm so far
    * There is an [issue on PyPA](https://github.com/pypa/advisory-database/issues/45) for the same thing (automated advisories)
        * [myles, npm] Worry: false positives (w/ “unpublish” events), to what extent can these be automated?
        * [https://github.com/advisories?query=type%3Amalware](https://github.com/advisories?query=type%3Amalware) ← (distinct format from vuln advisories!)
        * [https://github.blog/2022-06-09-introducing-entitlements-githubs-open-source-identity-and-access-management-solution/](https://github.blog/2022-06-09-introducing-entitlements-githubs-open-source-identity-and-access-management-solution/) 
    * “Chicken and egg” problem
        * Repos not collecting this data right now
        * [josef] RubyGems is working on this!
        * Examples of schemas
    * “Automated” or “semi-automated” malware detection
        * [trishank] [https://github.com/DataDog/guarddog](https://github.com/DataDog/guarddog) 
        * [josef] rubygems uses diffend.io 
            * Can possibly contribute to guarddog for Ruby!
        * [https://arxiv.org/abs/2209.13288](https://arxiv.org/abs/2209.13288) 
        * Heuristics for malware packages
        * Almost non-zero false positive considered unacceptable due to sheer number of packages
            * Need manual review still
        * Common data for signals from malware scanning tools
        * And feeding into malware scanning tools
* [Trishank Kuppusamy] Discussion on how to “best” prevent dependency confusion attacks 
    * Motivation: [Torchtriton incident](https://pytorch.org/blog/compromised-nightly-dependency/)
    * **[Python Discussion](https://discuss.python.org/t/proposal-preventing-dependency-confusion-attacks-with-the-map-file/23414)**
        * Proposal based on TUF TAP 4 for mitigating these attacks
    * Ideas
        * OSS package managers are hard to change!
            * Inertia is high (often for good reasons)
        * Proposals
            * 1. Do nothing (nobody’s happy with this)
            * 2. Use something “extreme” like the map file (relatively high complexity/barriers to adoption)
                * During dependency resolution, the package manager backtracks
                * Adding mapping increases the complexity of dependency resolution! Consider choices of repositories
            * 3. (simple, [Pip issue](https://github.com/pypa/pip/issues/11784)) Error on ambiguity!
                * Currently pip treats multiple repos all with the same priority
            * 4. [https://github.com/pypa/pip/issues/11784#issuecomment-1423105601](https://github.com/pypa/pip/issues/11784#issuecomment-1423105601) 
            * 5. Lockfiles
                * Version/hash pinning
                * Still have this problem on updates / initial creation
            * 6. Network/index proxies
                * Downside: does not generally correctly handle backtracking dependency resolution
    * [josef] how this works in **RubyGems**
        * In Gemfile, if a dependency comes from a non-default source that has to be explicit!
        * Basically, a “namespacing” approach!
        * [https://bundler.io/blog/2021/02/15/a-more-secure-bundler-we-fixed-our-source-priorities.html](https://bundler.io/blog/2021/02/15/a-more-secure-bundler-we-fixed-our-source-priorities.html)
    * [jonathan] corporate organizations often _mirror_ dependencies (mix of internal/external). 
        * Dependency resolver doesn’t have this problem, the _mirror_ does!
            * RubyGems proxy example of applying the same logic [https://github.com/geminabox/geminabox/pull/339](https://github.com/geminabox/geminabox/pull/339)
        * **Gradle**: java has namespacing built into package names (DNS-based). 
            * [https://docs.gradle.org/current/userguide/declaring_repositories.html#sec:declaring_multiple_repositories](https://docs.gradle.org/current/userguide/declaring_repositories.html#sec:declaring_multiple_repositories) 
            * Has something “map”-like: filters on repositories
    * AI: Trishank to start compiling a doc on this
* [Mike Lieberman] SLSA other other metadata distribution and discovery
    * Similar chat at APAC-friendly meeting.
    * Didn’t discuss because of insufficient Mike Liebermans
* Administrivia: get Zachary Newman added as maintainer?
    * Zack to do this 
* Any other business?
    * nope!

<h3>Jan 25, 2023 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=RjpD2GvXP9U)


Attendees:



* Jacques Chester (Shopify; Chairing)
* Mike Lieberman (Kusari)
* Christine Abernathy (F5)
* Randall T. Vasquez (Gentoo/SKF)
* Nusrat Zahan (NCSU)
* Mahzabin Tamanna (NCSU)
* Josef Simanek (RubyGems)

Agenda:



* Introductions and new friends
    * Mike Lieberman from Kusari. Member of SLSA steering committee. CNCF Security TAG lead.
    * Christine from F5
      
* [Mike Lieberman] SLSA distribution and discovery
    * SLSA 1.0 is coming soon, and we’re looking to collaborate with software and package ecosystems to standardize around an approach or specification for distributing SLSA attestations for software and packages.
    * NPM is working on their API.
    * OCI has their spec.
    * Jacques: from RubyGems POV it would ideally be as CDN-friendly as possible
    * Nusrat: is this a before or after SLSA attestations are being published?
        * Mike: We’re seeing publication of SLSA attestation occurring in an ad hoc way now (eg attached to GH releases). It would be nice if it were consistent. Chicken and egg situation: generating vs consuming, no agreement on where/how to retrieve.
    * Nusrat: we wrote about advantages and disadvantages of SBOM after talking to practitioners. Current gripe is lack of standardization. Also a lot don’t want to _provide_ SBOMs (eg what if their competitors see it?). Can’t find examples or dataset to study.
        * Mike: very few tools follow SPDX or CycloneDX, often because of bugs/inconsistencies with specs. From SLSA POV maybe even provide a SLSA publishing library that supports publishing to as many ecosystems as possible to avoid different implementations.
        * Jacques: folks will usually want to implement in their own ecosystem.
        * Mike: could perhaps be a REST API, one to get package, another to get SLSA/SBOM docs.
    * Randall: need to treat with utmost care, folks can see OSS as a religious matter and disagree with introducing security public health measures. If you come with money or donated work to lift maintainer burden then maybe.
    * Jacques volunteers as lightning rod
    * Randall: raises the two cultures, curated packages like Gentoo vs open-access repos like RubyGems or PyPI. Homebrew insist they are not a security defence.
    * Jacques
* [Jacques] Reporting on discussion of malware and metadata repo
* AOB

<h3>Jan 12, 2023 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=XQ6k3QR95J4)

Attendees:



* Zachary Newman (Chair)
* Jacob Finkelman / Eh2406 (Cargo)
* Joshua Lock (VMware/TUF/SLSA)
* Kairo Francisco de Araujo (VMware)
* Josef Simanek RubyGems/RubyGems.org)
*  Sterling Greene (Gradle)
* Chris Lamb (Reproducible Builds)
* Jason Swank
* Marina Moore (NYU)
* Radoslav Dimitrov (VMware)
* Lois Anne DeLong (NYU)
* Lukas Pühringer (NYU, TUF)
* Randall T. Vásquez (Gentoo/Homebrew/SKF)
* Jacques Chester (Shopify)
*  Mattia Rizzolo (Reproducible Builds)
* Holger Levsen (Reproducibke Builds, Debian)
* Cheng Lee (Anaconda, conda)

Agenda:



* Introduction
    * Reproducible Builds team here!
* RSTUF -> openssf [Joshua Lock] (brief [slides](https://docs.google.com/presentation/d/1Eu580ojkdMUEIY1Amh4IJNRga7WxkxaZoO5nyLrgsHw/edit?usp=sharing) summarising RSTUF and why we think OpenSSF is a good home)
    * [RSTUF](https://github.com/vmware/repository-service-tuf): Repository Service for [TUF](https://theupdateframework.com/): we saw a demo recently in this meeting
    * It’s hard to adopt TUF
        * (see e.g. [PEP 458](https://peps.python.org/pep-0458/), a decade old but not implemented)
        * Q: why?
        * Can we provide tooling (in the form of a service) to make it easier?
        * Note: can you document motivation etc.? That will help with projects that are unlikely to take a wholesale dependency on a service.
            * Still useful as a reference implementation
    * Can VMware donate this project to OpenSSF (a neutral foundation)?
    * Motion to sponsor by this group and present to TAC: Voice vote call for objections.
        * Sponsor => Zach goes to TAC to say this WG would like to sponsor this project.
            * Periodic reporting to this group
        * **No objections, motion is adopted**
* SLSA v1.0 [ Joshua Lock]
    * SLSA background (from “[An Overview on SLSA](https://static.sched.com/hosted_files/supplychainsecurityconna21/96/_An%20Overview%20on%20SLSA%20-%20SupplyChainSecurityCon.pdf)” from SupplyChainSecurityCon NA 2021)
    * FYI: SLSA is getting a 1.0 soon (brief [slides](https://docs.google.com/presentation/d/18SaT0L271d0Wb4gl4fSTjildILbOiIUj4lkFxll40hk/edit?usp=sharing) describing changes from current v0.1)
    * Feedback from package repo perspective welcome
* Follow-ups
    * Brandon Lum: Package manager survey
    * (zjn) OpenSSF Package Data Follow-Up
        * Eg [stats from PyPI](https://twitter.com/di_codes/status/1610781657128108033)
* “Greenfield” opportunities
    * Rust: [pre-RFC](https://internals.rust-lang.org/t/pre-rfc-using-sigstore-for-signing-and-verifying-crates/18115)
    * Zig: [ziglang/zig#14265](https://github.com/ziglang/zig/pull/14265#issuecomment-1378382515)
    * What can this group do to support?
        * Misconception (from Linux community): LF is tone-deaf to what really happens
            * “Package Repository” can mean software development repos (RubyGems) or a Debian repository for end-users.
            * Confusing things even more: new group pushing Flatpak/Snap
        * We tend to attack different things (expectations of end users)
            * Curated repos: “if it’s not secure, why are you publishing it?”
            * Vs. community repos 
        * Can we get more folks from distros?
* TUF + in-toto
    * TUF: delegating authority to maintainers
    * In-toto: more rich policies around actors involved in producing the package
    * TUF also becomes the mechanisms by which you distribute in-toto policies (layouts)

AI:



* Zack to follow up on RSTUF
* Zack: what do we do with ideas that we want to do but aren’t going to yet

<h3>Dec 15, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>


[Recording](https://www.youtube.com/watch?v=bCGK7z848T0)

Attendees:



* Zack Newman zjn @ chainguard. dev
* David A. Wheeler (Linux Foundation) [dwheeler@linuxfoundation.org](mailto:dwheeler@linuxfoundation.org)
* Jacques Chester (Shopify)
* Sterling Greene (Gradle)
* Ciara Carey (Cloudsmith)
* Josef Simanek (RubyGems/RubyGems.org)
* Brian Fox (Sonatype / Maven Central, GB)
* Chaitanya S. (GitHub)
* Philip Harrison (GitHub)
* Nusrat Zahan ([nzahan@ncsu.edu](mailto:nzahan@ncsu.edu) -NCSU)
* Jonathan Leitschuh (Dan Kaminsky Fellowship @ HUMAN Security)

Agenda



* New faces
    * Nusrat (NC State U)
    * Reintroduction - Jonathan Leitschuh (OSS researcher, formerly of Gradle)
    * Philip (GitHub Package Security Team)
    * Ciara (Cloudsmith)
    * Chaitanya (GitHub)
* [Jacques] rubygems.org now has WebAuthn support!
    * Next up will be CLI support
    * It’d be good to clarify what the security advantages of Webauthn are. They are:
        * OTPs are a pain! WebAuthn just requires a tap, and taps are easier than typing in numbers as required by OTPs.
        * OTP is phishable - if the user is fooled that they’re at the correct website, they’ll enter the  OTP. In contrast, WebAuthn will only authenticate to that specific website - counters phishing, because the key won’t be sent to the wrong address.
    * Package manager implementation constraints
        * Hesitant to take 3p dependencies (you can bundle _some_ packages by default, plus stdlib)
            * Code sprawl, increase in TCB
            * Bundler (for example) has to vendor a few gems, which creates a problem. Opening a raw socket, etc. requires more functionality. You need an HTTP server (not just a client). Their solution is to redirect a request to localhost.
            * Due credit to npm: they originally were going to do the copy & paste, now local listener (it’s hard to search for)
            * Copy & paste prototype: [https://github.com/Shopify/rubygems.org/pull/56](https://github.com/Shopify/rubygems.org/pull/56)
            * Local listener prototype: [https://github.com/Shopify/rubygems.org/pull/67](https://github.com/Shopify/rubygems.org/pull/67)
          
* [Jonathan Leitschuh] Repo survey
    * Did the pentesting question make it in?
    * 
    * Sensitivity of information—goal is “reasonable”: as open as possible until the data becomes _too_ useful
    * Some version of this turned into a public report
* [zjn] Data from package repos — recap + next steps
    * Some parts are sensitive, & not shared. Talk with Brandan.
    * [David] Would it be useful to create a short public report on “current state” based on this, e.g., as an OpenSSF report? I don’t know of anywhere else to get this info.
    * What about sensitive info? David: OpenSSF doesn’t have a formal “classification” system, maybe use traffic light protocol (TLP). We generally want maximum public access, but our goal is not help adversaries, so we can be reasonable about hiding issues.
    * Yes, let’s create a public shareable version.
    * PyPI data: [https://cloud.google.com/blog/topics/developers-practitioners/analyzing-python-package-downloads-bigquery](https://cloud.google.com/blog/topics/developers-practitioners/analyzing-python-package-downloads-bigquery) 
* Pen testing of repositories
    * Jonathan L: There’s never an incentive on repository hosts to get a security audit done. I propose that many have never been pen tested before, worrying given how critical they are.
    * Jacques C: Shopify is concerned, so we focus on rubygems security. We’ve donated a million dollars to the RubyShield initiative. We’d like other organizations to do the same thing.
    * Jonathan: What’s the barrier for a pen test of your repository host?
    * Zack: Let’s wait until we get the data, hopefully this is moot. If it’s NOT moot, we should revisit.
    * Josef: There’s no barrier to pentesting Rubygems, it’s OSS & can run locally. Bigger issue is private hosts, no visibility, & those are often more critical because they host private data.
        * [https://github.com/rubygems/gemstash](https://github.com/rubygems/gemstash) (officially recommended and maintained by RubyGems to self-host gems)
        * https://github.com/geminabox/geminabox
* Zack: One awesome thing about this group is that before there wasn’t a place where you could see the information about repositories in one place, we’ve now started to collect this information. Our thanks to Brandon Lum (Google) for putting this together.
* There was a switch from the Google Spreadsheet to a text format.

Action items



1. Brandon: public report from the package manager survey?
2. Zack: with Nusrat to outline goals for data project

<h3>Nov 30, 2022 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>


[Recording](https://www.youtube.com/watch?v=mzUYtg480V4)

Attendees:



* Dustin Ingram (Google)
* Josef Simanek (RubyGems)
* Zachary Newman (Chainguard)
* Joel Orlina (Sonatype / Maven Central)
* Marina Moore (NYU)
* Jacques Chester (Shopify)
* Jeffrey Borek (IBM)
* Meder Kydyraliev (Google)
* Brandon Lum (Google)
* Randall T. Vasquez (Gentoo)
* Cheng Lee (Anaconda / conda)

Agenda:



* Welcome new friends
    * Aaron Bray, CEO / co-founder of Phylum
* [Jacques] What are folks doing to surface CVE notices in their UIs? Or thinking about doing?
    * Maven does this currently
    * [There’s a PR for rubygems.org](https://github.com/rubygems/rubygems.org/pull/3264), we’d like to get input on what others have learned or thought about
    * PyPI is getting data from OSV but not surfacing in UI
        * Accessible via API
    * [Meder] Example from deps.dev: [https://deps.dev/maven/org.apache.logging.log4j%3Alog4j-api/2.14.0](https://deps.dev/maven/org.apache.logging.log4j%3Alog4j-api/2.14.0)
    * [Dustin] Lessons from the Node.js community: [https://overreacted.io/npm-audit-broken-by-design/](https://overreacted.io/npm-audit-broken-by-design/) 
* [Josef] “Friendly README.md problem”
    * [Email address variations](https://support.google.com/a/users/answer/9282734#cke_bm_9451S)
    * disposable emails
        * [dustin] [https://github.com/disposable-email-domains/disposable-email-domains](https://github.com/disposable-email-domains/disposable-email-domains) 
    * domain basket
    * Meder: could there be a shared list between package ecosystems?
        * Dustin: it’d be nice if GH folks were here, they probably have a lot of experience/ list / rules
    * [dustin] [https://pypi.org/policy/acceptable-use-policy/](https://pypi.org/policy/acceptable-use-policy/) 
* [Brandon] Next steps for package manager survey results 
* [dustin] 
* [Jacques] data repo / malware repo discussions in other WGs:
    * End Users WG had a similar idea for collecting malware samples
    * OSSIEMILATION
    * How does this relate to GUAC?
    * [Meder]: There's also [https://github.com/ossf/package-analysis](https://github.com/ossf/package-analysis)

Action items



1. [dustin] Write up PyPI’s general policy on abuse remediation
2. [???] next steps on package manager survey results

<h3>Nov 17, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>


[Recording](https://www.youtube.com/watch?v=IXEJpJ50Aj4)

Attendees:



* Jason Swank (Maven Central, Sonatype)
* Zack Newman (Chainguard)
* Cheng Lee (Anaconda/conda)
*  Appu Goundan (Google)
* Kairo de Araujo (VMware)
* Martin Vrachev (VMware)
* Ciara Carey (Cloudsmith)
* Brian Fox (Sonatype, GB)
* Chaitanya S (GitHub)
* Brian DeHamer (GitHub)
* Matt Rutkowski (IBM)
* Lukas Pühringer (NYU)
* Joshua Lock (VMware)
* Radoslav Dimitrov (VMware)
* Velichka Atanasova (VMware)
* Sterling Greene (Gradle)
* Joel Orlina (Maven Central, Sonatype)
* Marina Moore (NYU)
* Josef Simanek (RubyGems)
* Brandon Lum (Google)
* Jussi Kukkonen (Google)

Notes:



* Kairo de Araujo: Demo for [RSTUF](https://github.com/vmware/repository-service-tuf): potentially useful for TUF integration into package repos (15–20 mins)
* EMEA orientation
    * WG discusses how to make package managers and specifically repositories more secure. Sharing knowledge, examples, patterns.
    * Some great proposals and implementations have been announced during WG lifetime
        * PyPI MFA rollout
        * Package signing proposals (i.e., RubyGems & npm RFCs)
    * Meetings are biweekly, alternating between APAC friendly and EMEA friendly meetings times. Every 4 weeks at this time. All recorded. Async communication largely happens via OpenSSF Slack #wg_securing_software_repos, there’s an email list: [https://lists.openssf.org/g/openssf-wg-securing-software-repos](https://lists.openssf.org/g/openssf-wg-securing-software-repos) 
    * WG has a charter which is linked from the Slack channel [https://github.com/ossf/wg-securing-software-repos](https://github.com/ossf/wg-securing-software-repos) 
    * Group may make non-binding recommendations
    * The tangible work outputs are largely happening in the individual package repository projects
*  AI [zjn]: Need to fix Zoom link in OSSF calendar entry AND add the <span style="text-decoration:underline;">meeting notes link</span> to the same calendar entry (EMEA at least)
    * Update: zjn@ has email OpenSSF ops team to get access to edit, sorry for the hiccup
* Update on package manage ecosystem survey  (Data (please request access per view since it includes PII):: [https://docs.google.com/spreadsheets/d/1BEY3lVjEH6M5fSqixGNGACMdosua1TrT4O3YIJL4Ofw/](https://docs.google.com/spreadsheets/d/1BEY3lVjEH6M5fSqixGNGACMdosua1TrT4O3YIJL4Ofw/)) 
* [Packaging Con 2023](https://packaging-con.org/) (to be announced)!
    * Call for papers in the next few weeks. 

<h3>Nov 2, 2022 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=LsshIbsD6oY&list=PLVl2hFL_zAh_VfsvGMCrkPSS1z2VFFy-r)

Attendees:



* Dustin Ingram (Google)
* Matt Rutkowski (IBM)
* Ian Molloy (IBM)
* Jason Swank  (Sonatype, Maven Central)
* Zach Steindler (GitHub)
* Trishank Kuppusamy  (Datadog)
* Sumana Harihareswara (NYU)
* Justin Cappos (NYU)
* Jenn Skeivik (Boeing)
* J.R. Rao (IBM)
* Marina Moore (NYU)
* Jenny Shen (Shopify)
* Jiyong Jang (IBM)
* Mike Brown (IBM, containerd, OCI)
* Jeff Borek (IBM)
* Brian Behlendorf (LF/OpenSSF)
* Meder Kydyraliev (Google)
* Randall T. Vasquez (Gentoo)
* David Edelsohn (IBM)
* Cheng Lee (Anaconda/Conda)
* Aeva Black (Microsoft, OpenSSF TAC, OSI)
* Betty Li (Shopify)
* Josef Simanek (RubyGems)

Agenda



* Quick meta note on upcoming meetings
    * Zack Newman - Point of order: EMEA meetings rescheduled
* Welcome new friends
    * Zach Steindler (GitHub)
    * Justin Cappos (NYU)
    * Jenn Skeivik (Boeing)
    * Ian Molloy (IBM)
    * J.R. Rao (IBM)
    * Jiyong Jang (IBM)
    * David Edelsohn (IBM)
    * Aeva Black (Microsoft, OpenSSF TAC, OSI)
* J.R. Rao, Ian Molloy and Jiyong Jang - IBM previews emerging technologies to secure OS software supply chain at scale, 15-20 minutes.
    * Presentation in this issue: [https://github.com/ossf/wg-securing-software-repos/issues/8](https://github.com/ossf/wg-securing-software-repos/issues/8)
        * Feedback and use cases welcome as well as suggestions for open source possibilities at OpenSSF
    * Q: How are you consuming all the software that exists to compute genes?
        * Existing software repos, feeds. Provide a search engine for code, search by hash, go beyond.
    * Q: Have you considered how the fingerprint relates to dependencies? Connecting/mapping dependencies via a gene.
        * Actually building a large graph behind the scene, including relationships between binaries and dependencies. 
    * Q: What is the granularity? What about reordering positioning?
        * Based on functionality. The hope is that it’s resilient to obfustication. File level could be too coarse, lines could be too fine.
    * Q: How are you handling obfustication generally? What’s the threat model?
        * .
    * Q: This seems to apply to malware, have you explored that?
        * Main focus is SBOM and open source
* Dustin Ingram - 
* Betty Li - Update on  after presenting to TAC.
    * [Presentation](https://docs.google.com/document/d/1o2Q5bELfTjEV-POzen-4BRqOMAGRlUZES-SkIDwMU7c/edit?usp=sharing)
    * [Github Issue](https://github.com/ossf/wg-securing-software-repos/issues/9) to collect questions and feedback
* Zack Newman - Future meeting: [RSTUF](https://repository-service-tuf.readthedocs.io/en/latest/guide/overview/overview.html) demo?
    * Repository simulator for TUF, sandbox for repos to experiment
    * Maybe in the EMEA-friendly meeting?

Action items



1. 

<h3>Oct 19, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly) </h3>

[Recording](https://www.youtube.com/watch?v=Hjp0Qpl9TCk&list=PLVl2hFL_zAh_VfsvGMCrkPSS1z2VFFy-r)

Attendees:



* Jacques Chester (Shopify, chairing)
* Mihai Maruseac  (Google)
* Jason Swank (Maven Central / Sonatype)
* Bob Callaway (Google)
* Zack Newman (Chainguard)
* Brandon Lum (Google)
* Betty Li (Shopify)
* Sebastien Awwad (Anaconda/conda)
* Jacob Finkelman / Eh2406 (Cargo)
* Randall T. Vásquez (Gentoo/Homebrew)
* Matt Rutkowski (IBM)
* Marina Moore (NYU)
* Josef Simanek (RubyGems / RubyGems.org)
* Christine Abernathy (F5)
* Ciara Carey (Cloudsmith)

Regrets:



* Dustin Ingram
* Cheng Lee (Anaconda)

Agenda:



* [Brandon Lum] SBOM Best Practices discussion for Language Ecosystems 
    * With  (Google) and Meder Kydyraliev Ilkka Turunen from Sonatype chatting about best practices on SBOMs
    * Above is a draft discussion/guide
    * Jacques: who is this for? Package maintainers or repo maintainers?
        * Brandon: sort of both. Possibly repos automatically run a tool.
    * Sebastien: says “fully resolve dependency graph”, what about runtime deps?
        * Brandon: eg. you can specify ranges in package requirements files (POM.xml, Gemfile etc) which is different from fully resolving the exact dep. Maybe we need to be specific about runtime vs other time deps
    * Matt: package maintainers should be responsible with tools and guidance. Users assume trust in the package repos tho as their agents for quality assurance. How would this fit with existing efforts like GitHub’s security build profile? Do attestations/provenance centrally. Where would this guidance fit into that?
        * Brandon: granularity of provenance (which is a big topic); if we have confidence in the process of SBOM / attestation generation then that should be OK.
        * Matt: right, but it’s about the trust (or who is trusted: package maintainer or repo maintainer). Because package maintainer can produce SBOM any way they like, or even maliciously. It would be nice to have consistent tooling to improve trust.
        * Brandon: comes back to question of how to collab on this. 
        * Jacques: Matt are you proposing shared tool or central service?
        * Matt: reference point is GitHub’s npm proposal to do some build on GH Actions
        * Zack: agree with Matt that some guidance on tooling, would like guidance to be slightly more concrete
        * Brandon: we think we can add more, want to collaborate with the WG. Are we targeting white paper, recommendation …? What the angle is.
        * Zack: were you intending audience to be primarily in the WG? Or individual package maintainers?
        * Brandon: for folks who are in the room (and who ought to be)
        * Matt: “we have 2000 teams who will use 2000 different tools”
    * Jacques: what are the next actions?
        * Brandon: would hope for feedback over next few weeks, then return to discuss and flesh out doc (Kubecon will be next week). Please ping Brandon or comment on the doc. Aiming for mid- to end-November to visit question of publishing this doc.
* [Jacques] Vote on 
    * Whether to go to TAC: no objections. We will proceed to TAC.
    * Who will keep the ball rolling?
        * Jacques will arrange delegate
* [Zack] work on proposal for repository of data on repos.
    * Have found a potential contractor with polyglot expertise
    * Data like takedown rates, upload rates, download rates. PyPI is a great leader. Goal is to centralise data for security researchers.
* [Matt] something on my radar is that data packages, ML also behaves like / shaped like package repos. We should put on our radar that this is equal to code.
    * Zack: have been having discussions with various folks aiming to be “Github for ML”. All the problems we have with examples like “hugging face” (among others) also faced by ML folks.
* EMEA meeting timing [Zack, for Jussi]
    * APAC is 4 hours later than EMEA which doesn’t seem like a lot. This time is 8-9pm 
    * Are there objections to moving EMEA? None raised.
* AOB
    * None today. Folks got to leave early!

Action Items:



* Zack: reach out to ML repo communities.
* Zack: send an email! And Doodle/etc. and Slack about rescheduling meeting
    * Also check with OpenSSF calendar
* Jacques: arrange delegate to present shared helpdesk proposal to TAC for a vote.

<h3>Oct 5, 2022 | OpenSSF Securing Software Repositories (APAC-friendly) (Canceled)</h3>


**Canceled as no chair was available for this call.**


<h3>Sep 21, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly) </h3>

[Recording](https://www.youtube.com/watch?v=4aP1o5XcKGc)

Attendees:



* Dustin Ingram (Google, chair)
* Jacques Chester (Shopify)
* Mihai Maruseac (Google)
* Cheng Lee (Anaconda/conda)
* Avishay Balter (Microsoft)
* Jacob Finkelman / Eh2406 (Cargo)
* Marina Moore (NYU)
* Trevor Rosen (GitHub)
* Sebastian Crane
* Brian DeHamer (GitHub)
* Randall T. Vasquez (Gentoo)
* Zack Newman (Chainguard)
* Joel Orlina (Sonatype/Maven Central)
* Maciej Mensfeld (Mend / RubyGems)
* Mike Brown (IBM, containerd, kubernetes, OCI)
* Josef Simanek (RubyGems)
* Myles Borins (GitHub / npm)
* Matt Rutkowski (IBM)

Agenda



* Quick meta note on upcoming meetings
    * See table near top of doc for dates, space for agenda items, names of folks who will be chairing (volunteers welcome for gaps!)
* Welcome new friends
* Josef Simanek / Maciej Mensfeld (RubyGems) - How to handle research/harmless malicious packages?
    * Tend to detect some fair number of ‘research’ packages
    * Policy was to allow them as long as they weren’t malicious or are sensitive (beyond security research)
    * npm removes packages like this, RubyGems does not
    * Example: dep confusion attack from [Alex Birsan](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)
    * Dustin: For PyPI (same as npm). If it’s not legit useful software that’s grounds for removal. “PyPI is not a security research tool”. Anything that ticks the box for malware gets pulled. No legit need for obfuscation and no way to tell whether exfiltration was benign.
        * Josef: is there a doc we can look at?
        * Dustin: no, but it’s being drafted
        * Josef: it would be nice to have something consistent across repos, that can be handed to researchers
        * Maciej: would also like to contribute to doc. Planning to open RFC on rubygems for a similar policy.
        * What about placeholder packages? Potentially invalid?
    * What about name squatting? Deps to be published?
        * PyPI will allow case-by-case reservations
    * Sebastian: arguably hostname is PII, meaning there are GDPR implications.
        * Maciej: what about telemetry? Should we have rules about package telemetry?
        * Sebastian: it’s not illegal per se to collect telemetry but most maintainers are not lawyers. Maybe Debian approach of patching packages to be opt-in telemetry.
        * Maciej: perhaps we could have a policy that telemetry has to be opt-in.
        * Sebastian: even small percentage of large sample is still useful data
    * Zack: from researcher perspective, if you went to US IRB to say “we will send data from other people’s computers” you would fail to get approval. So I am in favor of being strict on exfiltration or involuntary telemetry. You need informed consent. Nuance: some data already collected (eg. download counts) is already usable for academic research.
        * Sebastian: example that package was “sending data to Google”, but there were so many dependencies that it was hard to find which dep was actually sending the data. (Twist in the story: it wasn’t but had code that _could_ send data)
        * Zack: and as a software dev I’d be negatively surprised to discover that my deps were sending telemetry data without consent.
    * Randall: story of what happened when telemetry started at Homebrew. Turned out to be massive deal. Were using Google analytics and reddit post was “they’re sharing data with Google”.
    * Dustin: summarizing, it would be good to have a shared / collab doc for policy on the malicious and dial-home case.
    * Mike Brown: different regions will have different regulations, providers need to consider compliance. Eg. IBM hosts in multiple regions and has different policies per region.
* [Jacques] [Shared helpdesk proposal](https://docs.google.com/document/d/1Od9kqd4JIAW1h0vvvkD8NFclxsR8yudOdsZEMT7lBUc/edit#heading=h.mztvqya5xxdj) revisited
    * Most repositories are volunteer-operated, want to expand coverage of policies like MFA requirements, but these need additional support
    * [Randall] Jacques should talk to crob
    * [Sebastian] Opportunity to use CiviCRM (open source platform)
* [Joel] quick questions: anyone planning on attending KubeCon NA in October? Is there a Sigstore-specific conference co-located?
    * [Yes: Sigstorecon :)](https://events.linuxfoundation.org/sigstorecon-north-america/) on Tuesday
        * [Talk by Zach](https://sigstoreconna22.sched.com/event/1Ayks/life-of-a-sigstore-signature-jed-salazar-zack-newman-chainguard?iframe=no&w=100%&sidebar=yes&bg=no)
    * Attending: Cheng Lee (Anaconda), Zack Newman (Chainguard)

Action items



1. Joel Orlina - (or someone else) fill out [survey](https://docs.google.com/forms/d/1I7pGUclfu-pV-nQ0M6OMjOjazP4xldbDdVz67wVR5h8/edit?ts=62d81495) for Maven Central? 
2. Dustin - shared draft on policy for valid/invalid projects (malicious, exfil, name squatting, etc)
    1. [https://peps.python.org/pep-0541/#invalid-projects](https://peps.python.org/pep-0541/#invalid-projects) 
3. All - feedback on  by Oct 19th

<h3>Sep 7, 2022 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=AruRR37YvLM)

Attendees:



* Dustin Ingram  (Google)
* Josef Simanek RubyGems/RubyGems.org)
* Jacques Chester (Shopify)
* Jason Swank (Sonatype/Maven Central)
* Myles Borins (GitHub / npm)
* Jenny Shen (Shopify)
* Sebastian Crane
* Joel Orlina (Sonatype/Maven Central)
* Rahul Gupta (Microsoft)
* Randall T. Vasquez (Gentoo)
* Cheng H. Lee (Anaconda / conda)
* Katherine Druckman (Intel)
* Christine Abernathy (F5)

Agenda



* Welcome new faces
* [Jacques] [WIP draft](https://docs.google.com/document/d/1Od9kqd4JIAW1h0vvvkD8NFclxsR8yudOdsZEMT7lBUc/edit#heading=h.mztvqya5xxdj) of proposal to hire a shared helpdesk person
    * Increasing the focus on exactly what this person(s) would be responsible for
    * Discussion on the feasibility of of giving a shared person high-tier admin access
    * Discussion on potentially pairing this w/ funding for orgs to hire support staff directly
    * Pairing this with a platform for identity verification
* [Josef] Share best practices of recovering MFA from the support side (when device/recovery codes are lost). I (Josef Simanek ) can kick-off sharing RubyGems.org best practice.
    * W/ the scale of the rubygems team, afraid of an increase, especially w/ current size
    * Publishing metadata w/ source URL to github repo, look up author, publish an issue w/ shared secret/code (example issue at [https://github.com/guidance-guarantee-programme/booking_locations/issues/33](https://github.com/guidance-guarantee-programme/booking_locations/issues/33) )
    * Disable MFA to do email reset
    * All done manually, with no automation
    * Myles about NPM
        * Originally much like RubyGems, manual request for id proof (eg make a tweet)
        * Philosophical basis for new system is “points”. You need to collect enough points from other factors or channels to recover the account. 
        * Eg. email is 6 points of ID, MFA is 10 points etc. Lost email? We need 6 points from other sources to get email back.
        * Working to make email+password a hard requirement for account recovery, to make social engineering harder.
        * Will ask internally about sharing more details; script for recovery + chart of points.
    * What is the method for requesting reset?
        * Support email shared w/ Zendesk
    * Dustin, q for group. Who should know about resets? Eg. should reset info be sent to other owners of a dependency? Or make it public?
        * Jacques: yes, worth publishing an attestation about
            * * generally, we’ve shied away from publishing MFA status
        * Myles: there are various types of resets, doesn’t need to be explicit
        * Josef: problem with hiding MFA is only necessary when mandate is not in place
        * Jacques: on the npm sigstore proposal
        * Myles: this is a balance between security and transparency. Public leger: only maintainers that have published show up in authors list
* [Dustin/Brandon] Shout out on [Package Manager Survey](https://docs.google.com/forms/d/1I7pGUclfu-pV-nQ0M6OMjOjazP4xldbDdVz67wVR5h8/edit?ts=62d81495), so far we have 4 ([PyPI](https://pypi.org/), [Gradle](https://gradle.org/), [OPAM](https://github.com/ocaml-opam), [basalt](https://github.com/hyperupcall/basalt))

Action items



1. jacques chester (Shopify)- collect data for shared helpdesk proposal

<h3>Aug 24, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=seCdV7pxio0)

Attendees: 



* Jacques Chester [Chairing] (Shopify)
* Jacob Finkelman / Eh2406 (Cargo)
* Mihai Maruseac (Google)
* Brad Beck (Citi)
* Marina Moore (NYU/Chainguard)
* Randall T. Vasquez (Gentoo)
* Katherine Druckman (Intel)
* Cheng Lee (Anaconda/conda)
* Brian DeHamer (GitHub)
* Brian Fox (Sonatype / Maven Central)
* Joel Orlina (Sonatype / Maven Central)
* Sterling Greene (Gradle)
* Trishank Kuppusamy (Datadog)
* Donald Stufft (Datadog)
* Jay White (Microsoft)
* Zack Newman (Chainguard)
* Patrick Flynn (Chainguard)
* Eddie Zaneski (Chainguard)
* Ciara Carey (Cloudsmith)
* Eric Tice (Wipro)
* Mike Brown (IBM)	

Apologies:



* Dustin Ingram (Google)

Agenda



* Welcome new faces
    * Katherine Druckman, OSS evangelist for Intel, prev Linux Journal
    * Mike Brown, maint OCI standards, containerd
* Sympathy for our PyPI friends ([context](https://twitter.com/pypi/status/1562442188285308929): phishing attack on PyPI users)
* [ Brandon Lum] Updated OpenSSF Package Manager Survey, additional questions on intent ([Survey link](https://forms.gle/zczdmKCQHk5LVdzDA))
* [Zack+Marina] OpenSSF as a home for datasets
    * (out of date) 
    * We’ve got some concrete use cases! Thanks, Dustin (context: [tweet](https://twitter.com/di_codes/status/1562160289918947329))
        * Taken-down malware
        * “Typosquatting”—just metadata
    * Ask: are repo folks amenable?
        * (Sterling) Gradle Plugin Portal may be interested, but backend is closed source. Contact [louis@gradle.com](mailto:louis@gradle.com) and [sterling@gradle.com](mailto:sterling@gradle.com) 
    * If so, Marina + Zack will go ahead and try to move forward with design and getting OpenSSF resources
    * [Cheng] Would this be available only to researchers or could other maintainers/repositories make use of it? Context: conda would make use such information to prevent, e.g., PyPI typo-squats from being repackaged and made available in conda repositories.
        * Possibly. Would have to scope the types of data that would be available.
        * Bias towards more-public sharing
    * Licenses (CDLA?), formats should be concrete
    * We will solicit feedback on formats, the data to collect, from this group and from researchers
* [Jacques] We should ask for money! There are some pools from the [Mobilization Plan](https://openssf.org/oss-security-mobilization-plan/)
    * Shared Helpdesk
        * Mobilization Plan Stream 10: “Enhance the 10 Most Critical OSS Build Systems, Package Managers, and Distribution Systems With Better Supply Chain Security Tools and Best Practices”
        * Jacques will work on this proposal
    * Malware research repository
        * Mobilization Plan Stream 8: “Coordinate Industry-Wide Data Sharing to Improve the Research That Helps Determine the Most Critical OSS Components”
        * Zack & Marina will fold this into their work on data set proposal
* [Patrick] Cosign bundle proposal moving forward with client-side prototype [https://github.com/sigstore/cosign/issues/2131](https://github.com/sigstore/cosign/issues/2131)
* [Jacques] [npm sigstore RFC released](https://github.com/npm/rfcs/pull/626)

Action items

*

<h3>Aug 10, 2022 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=xvcwyaj00FM)

Attendees:



* Dustin Ingram (Google)
* Jacques Chester (Shopify)
* David A. Wheeler (Linux Foundation)
* Cheng Lee (Anaconda/conda)
* Sterling Greene (Gradle)
* Trishank Kuppusamy (Datadog)
* Margaret Tucker (GitHub policy team)
* Justin Colannino (GitHub policy team)
* Brian Fox (Sonatype)
* Randall T. Vasquez (Gentoo)

Agenda



* Welcome new friends!
    * Margaret Tucker (GitHub)
    * Justin Colannino (GitHub/Microsoft)
* [???] TL;DR on [https://github.blog/2022-08-08-new-request-for-comments-on-improving-npm-security-with-sigstore-is-now-open/](https://github.blog/2022-08-08-new-request-for-comments-on-improving-npm-security-with-sigstore-is-now-open/) 
    * [https://github.com/npm/rfcs/pull/626](https://github.com/npm/rfcs/pull/626) 
    * Jacques: Much of the discussion was around stuff being done in a CI (ie token from CI provider) vs CLI (with tokens coming from OIDC IdPs)
* [Dustin] FYI: , OpenSSF TAC voted to endorse funding this proposal
    * Still waiting for GB approval
* [Sterling] Getting some help on 
* [Margaret (GitHub) / Justin (Microsoft)] Principles for Safer Developer Ecosystems
    * Justin has had many years of experience as a lawyer re: OSS
    * Focus: “Developer-first approach to content moderation”
    * [TODO: Link to slides?]
    * Package registries [& Package repos] have unique concerns: speed development but create new attack vectors.
        * GitHub just provides “code at rest”
        * In law, 1st amendment applies to code, including minified code. But the courts have said (DCSS) that there’s a distinction between source code & object code that “just does something” - less learning that you get from just automation. Registries are more like “code in flight”
    * What is the role of registries for posting malware & known vulnerabilities?
        * David: Malware has 2 kinds: inside threat (developer really did create that malware) vs. external threat (account takeover, which can be countered by things like MFA & signatures). They have different countermeasures
    * Actors: Users, maintainers, registry
    * Proposed principles for package registries:
        * Trust comes first
            * Might be good to clarify this for each actor
        * Transparent & consistent policies
            * Many other issues end up here - there are many trade-offs, the key is to make it clear what the decisions are.
            * E.g.: if registries allow developers to remove old package versions at any time for any reasons, that can break a huge number of builds (see: left-pad). Thus, a registry might choose to ensure that a version cannot be deleted after some period of time unless it’s legally required or is determined to be malware.
            * If registries search for malware & something is clearly malware, they may choose to remove it immediately - but that requires a clear definition of malware.
            * If registries require MFA, say so & explain why.
            * It’s good for registries to detect/counter malware. However, techniques such as analyzing for malicious behavior, or re-running builds to determine if they are reproducible (& reporting if they are), take extra resources that some registries may not have. Registries should be clear if they do or don’t do such things.
        * Secure the supply chain
            * Need to clarify what is malware.
            * Add something about “ease” and “by default” - just “giving tools” is too passive
            * Often warnings aren’t seen - many builds are unattended.
                * One solution is to break builds
                * Can we get warnings SEEN without breaking builds?
            * David: In best practices badge we *intentionally* break our builds for known vulnerabilities in a dependency (with the ability to override). That’s almost certainly not appropriate for all, but maybe we could make that easy to choose.
        * Empower maintainers
            * Enforce carefully. E,.g., remove only if clearly malware (or legal requirement), don’t allow removal of old versions in most cases (see left-pad), see “transparent & consistent policies”
        * Always innovate
    * Next step: Create a Google document, the goal is to create a document from this WG to give recommended principles for package registries
        * Many registries are in this WG, and if they sign off many others will consider it
* [Trishank] Should we try to actually make the meeting time APAC-friendly?
    * Is there enough demand?
    * But if we don’t make the time, would we even _see_ the demand?
    * Maybe we should send out a survey to repo communities?
    * Dustin will send a poll to the Slack channel [Trishank: thanks, Dustin]

Action items



1. Dustin - fill out Glossary for Python
2. Dustin - raise timezone APAC issue w/ slack & email list
3. From Justin and Margaret -  please review and comment on the [Principles for Safer Developer Ecosystems](https://docs.google.com/document/d/1OVeSX4OJcuj87AjONNSBY8ECg5bP1q9-Wedb1u23pso/edit?usp=sharing) 

<h3>Jul 27, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly) (Canceled)</h3>


**Canceled as no chair was available for this call.**

<h3>Jul 13, 2022 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=13bIvgmQBIs&list=PLVl2hFL_zAh_VfsvGMCrkPSS1z2VFFy-r&index=6)

Attendees:



* You!
* David A. Wheeler (Linux Foundation)
* Tim Lehnen (Drupal Association)
* Jacques Chester (Shopify)
* Mihai Maruseac (Google)
* Ian Dunbar-Hall (Lockheed Martin)
* Jacob Finkelman / Eh2406 (Cargo)
* Jenny Shen (Shopify)
* Betty Li (Shopify)
* Zack Newman (Chainguard)
* Simon Kent (Google)
* Meder Kydyraliev (Google)
* Trishank Kuppusamy (Datadog)
* Christine Abernathy (F5)
* Alvaro Figueroa (Microsoft)

Apologies:



* Dustin Ingram (OOO, Jacques will be acting chair)

Agenda:



* Welcome new friends!
* [Jacques] Ruby Shield: [https://rubycentral.org/ruby-shield](https://rubycentral.org/ruby-shield)
    * RubyGems / Shopify
* [David A. Wheeler] there has been some community discussion/backlash on repos/forges requiring 2FA (more because of “what else might they require?”). OpenSSF TAC is working on a response
    * [https://lucumr.pocoo.org/2022/7/9/congratulations/](https://lucumr.pocoo.org/2022/7/9/congratulations/) Armin Ronacher posted his thoughts about PyPI's 2FA requirement on top 1% of downloads (~3,500 projects) requiring 2FA. Armin thought 2FA was fine but was worried about future creep of requirements. Many discussions occurred, e.g., [https://news.ycombinator.com/item?id=32037562](https://news.ycombinator.com/item?id=32037562) , [https://lwn.net/Articles/900953/](https://lwn.net/Articles/900953/)
    * The TAC agreed yesterday to try to write a post to help justify/encourage this, supporting these roll-outs. Joshua Lock is drafting this. We’ll acknowledge there are some challenges, but also justify & encourage it.
    * Many organizations are encouraging or requiring that at least some OSS projects use MFA tokens. This includes:
        * PyPI (Python). PyPI is giving away 2FA security tokens and will require 2FA for critical projects (which they define as their top 1% of downloads) - eventually will cover more [https://pypi.org/security-key-giveaway/](https://pypi.org/security-key-giveaway/)
        * RubyGems (Ruby). [https://blog.rubygems.org/2022/06/13/making-packages-more-secure.html](https://blog.rubygems.org/2022/06/13/making-packages-more-secure.html) . Currently Rubygems doesn’t support WebAuthn, that’s on the list of things to do
        * npm (JavaScript). NPM is making 2FA mandatory to their first cohort, all maintainers of top-100 npm packages by dependents, with a wider roll out planned. [https://github.blog/2022-02-01-top-100-npm-package-maintainers-require-2fa-additional-security/](https://github.blog/2022-02-01-top-100-npm-package-maintainers-require-2fa-additional-security/)
        * GitHub. GitHub will require all code contributors to use 2FA by the end of 2023 [https://github.blog/2022-05-04-software-security-starts-with-the-developer-securing-developer-accounts-with-2fa/](https://github.blog/2022-05-04-software-security-starts-with-the-developer-securing-developer-accounts-with-2fa/)
        * The Open Source Security Foundation (OpenSSF)'s "Great MFA Distribution Project" distributed free MFA tokens to a number of OSS projects in 2021. Again, this was to counter these attacks on important projects. For more information see: <[https://github.com/ossf/great-mfa-project](https://github.com/ossf/great-mfa-project)>
    * “This seems to be more like vaccines, it seems to be more that people don’t want to be told what to do. They’re doing this on their own personal time, they didn’t ask to be a critical project & don’t want to be told that they have to do more things.”
    * Perhaps there should be “canary” (small scale first)
    * What about funding underfunded projects?
    * It *IS* correct that this is imposing requirements on maintainers - that’s not epistemically wrong. But there are other issues:
        * The repo doesn’t owe you anything either - you don’t need to choose the repo
        * Allowing account takeovers is a huge harm to users - their needs need to be considered as well
* [Zack, on behalf of Sterling Greene] 
    * It’s very helpful to have common terminology when we’re discussing repositories
    * Request for maintainers of non-Java repos: please read, give feedback on the terminology in my ecosystem
    * Should coordinate efforts with work already ongoing here: [https://slsa.dev/spec/v0.1/terminology](https://slsa.dev/spec/v0.1/terminology) 
* [Tim] Not necessarily a discussion topic - since I know our scope is more about policy than specific tools, but…  
    * Wanted to share as a potential resource a new server-side TUF implementation that was funded by the Drupal Association for use within our ecosystem: [https://rugged.works/](https://rugged.works/) 
    * TUF for Humans: [https://rugged.works/background/tuf_for_humans/](https://rugged.works/background/tuf_for_humans/) 
    * Sigstore project: 
        * TUF delegation as a service?

<h3>Jun 29, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=Mu_hZOpSi_k&list=PLVl2hFL_zAh_VfsvGMCrkPSS1z2VFFy-r&index=5)

Attendees:



* Dustin Ingram (Google)
* Josef Simanek (RubyGems/RubyGems.org)
* Sterling Greene (Gradle)
* Eric Tice (Wipro)
* Jason Swank (Maven Central / Sonatype)
* Jacques Chester (Shopify)
* Cheng Lee (Anaconda/conda)
* Mihai Maruseac  (Google)
* Matt Rutkowski (IBM)
* David A. Wheeler (Linux Foundation)
* Yehuda Gelb (Checkmarx)
* Trishank Karthik Kuppusamy (Datadog)
* Maciej Mensfeld (Mend / RubyGems)
* Ciara Carey (Cloudsmith)
* Marina Moore (Chainguard/NYU)
* Vinod Anandan (Citi)
* Asra Ali (Google)
* Appu Goudan (Google)
* Bobby Holley (Mozilla)
* Zach Steindler (GitHub)
* Randall T. Vasquez (Gentoo)
* Bob Callaway (Google)
* Patrick Flynn (Chainguard))
* Simon Kent (Google)
* Trevor Rosen (GitHub)

Agenda



* Welcome new friends
    * Bobby Holley - Mozilla - have worked on Firefox for 14 years
* Reviewing action items
1. None?
* [Bobby Holley (Mozilla)] Presentation on cargo-vet.
    * This is running for Firefox today. Not really public.
    * Short term objective: Secure Firefox. Long-term objective: Secure the ecosystem
    * Firefox - originally C++, doesn’t have much reused code (more friction to reuse). Then rust came along, much easier to reuse code & that sped development, but soon we had 400 packages. It was hard to enforce review. Hard to know if anyone else used them.
    * Cargo-vet: Minimize friction for reviews. Trivial to set up, fits into workflow, enables ecosystem to share work.
    * Has partnered with Sourcegraph to make it easier to review diffs, friendlier audit experience.
    * For more information: [https://mozilla.github.io/cargo-vet/](https://mozilla.github.io/cargo-vet/)
    * repository: https://github.com/mozilla/cargo-vet/
    * David A. Wheeler: Note that there’s some potential relationship with “security-reviews”: [https://github.com/ossf/security-reviews](https://github.com/ossf/security-reviews) - haven’t talked with them, but happy to do so.
    * Basic model: It’s a list that cargo-vet fetches. It doesn’t contain audits themselves, it contains links to them. It just identifies information, you then decide which sources to trust.
    * Possibly of interest is the PHP Gossamer project: [https://github.com/paragonie/libgossamer/blob/master/docs/specification/Protocol.md](https://github.com/paragonie/libgossamer/blob/master/docs/specification/Protocol.md) 
* [Dustin] FYI: [https://blog.sigstore.dev/an-update-on-general-availability-5c5563d4e400](https://blog.sigstore.dev/an-update-on-general-availability-5c5563d4e400) 
* [David A. Wheeler] FYI: The OpenSSF Mobilization Plan identifies 10 streams. There’s currently discussion about how to address those streams. One idea is to create SIGs that report to the most relevant WG. E.g,. stream 10 “Improved Supply Chains” might end up reporting to this WG. This is still in discussion, just wanted to note it. See: [https://openssf.org/oss-security-mobilization-plan/](https://openssf.org/oss-security-mobilization-plan/)

Action items

*

<h3>Jun 15, 2022 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=Wm3reSRMPcE)


Attendees: 



* Jacques Chester (~~Spotify~~ Shopify) to lead
* Sterling Greene 
*  Zachary Newman 
* Joel Orlina (Sonatype / Maven Central)
* Simon Kent (Google)
* Mihai Maruseac (Google)
* Meder Kydyraliev (Google)
* Caleb Brown (Google)
* Christine Abernathy (F5)
* Patrick Flynn (Chainguard)
* Marina Moore
* Vinod Anandan (Citi)
* Jacob Finkelman / Eh2406 (Cargo)

Apologies:



* Dustin Ingram  (PTO)

Agenda

* Welcome new friends
    * Mihai - Google GOSST
    * Meder - Google GOSST
* Reviewing action items
2. Lorenzo: how widespread? [is the problem of domain resurrection] ← zack to try to dig into this
    * [zack] I did, expect a proposal soonish  
3. Jason (Swank) has a java-specific doc, Jason to share with the community (Jason is on PTO, expect this in July)
4. Alex Salkever - list of intros to package repo maintainers
5. Patrick/Jvz - draft for multi-artifact signing best practices
6. Brandon Lum - review added survey questions 
* [Jacques] Asking for help with domain monitoring
* [Myles] Some security measures require additional manual support—what should we do about that? Should there be OpenSSF support?
* [Jacques] What, if any, expectations do we have before sigstore goes GA?
    * SLOs of repos
        * Example of status.maven.org
        * Separate push/publish/upload from get/retrieve/download
        * Whether to check Rekor directly for each verification vs verifying on an extract from Rekor
* [Brandon - won’t be here, but have a request for the group] Would like to get folks to help playtest the survey form ([https://forms.gle/XM66ERLUMZYZgKfX7](https://forms.gle/XM66ERLUMZYZgKfX7)) [based on the [spreadsheet](https://docs.google.com/spreadsheets/d/12QlaYEtcp2ZwZRfZPHR4D3YpY8k770hYBeFQ6-N7Mts/edit#gid=1022416269)] and provide some feedback. Hoping to launch this soon!
* [Sterling]  defining some [common terminology](https://docs.google.com/document/d/1KiAQYlsOl2xPnXUGiAcdXze8cOUjmsqZ31m6dvSI0aM/edit#heading=h.leveprbtoca1) 

Action items



1. 

<h3>Jun 1, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=pQkXFPQpV0U)

Attendees:



*  Dustin Ingram (Google)
* Jonathan Leitschuh (Dan Kaminsky Fellowship @ HUMAN Security)
* Jason van Zyl (Apache Maven/Chainguard)
* Jason Swank (Sonatype / Maven Central)
* Zachary Newman (Chainguard)
* Patrick Flynn (Chainguard)
* Jacob Finkelman / Eh2406 (Cargo)
* Joel Orlina (Sonatype / Maven Central)
* Myles Borins (GitHub / npm)
* Ciara Carey (Cloudsmith)
* Hayden Blauzvern (Google)
* Cheng Lee (Anaconda/conda)
* Hervé Boutemy (Apache Maven)
* David A. Wheeler (Linux Foundation)
* Jeff Borek (IBM)
* Yehuda Gelb (Checkmarx)
* Radoslav Dimitrov (VMware)
* Jason Hall (Chainguard)
* Appu Goudan (Google)
* Brad Beck (Citi)

Apologies:



* Jacques Chester (Shopify) – I have a conflicting appointment

Agenda

* Welcome new friends
    * Alex Salkever ()
    * Madison Oliver (GitHub)
    * Radoslav Dimitrov (VMWare)
    * Lorenzo de Carli (University of Calgary)
    * Jason Hall (Chainguard)
    * Adolfo García (Chainguard)
* Reviewing action items
7. Dustin - close EMEA-friendly poll, update time
8. Zach - Doc to describe means to counter domain expiry attacks: 
* [Zach] 
    * Lorenzo: how widespread?
    * Maven: Jason Swank has a Maven Central / java-specific doc, Jason to share with the community and maybe we merge the docs
    * Jonathan: to provide references on a previous related attack vector)
        * https://autsoft.net/a-confusing-dependency 
* [Alex Salkever/Hilary Carter] Linux Foundation Critical OSS Projects interviews
    * The Linux Foundation Research is conducting a series of interviews with active maintainers (code, commit management, build management) of critical open source projects. The interviews are part of a project to paint a qualitative picture of the motivations, challenges, and rewards of maintainership. Package managers are a critical part of the OSS supply chain and occupy a unique place in the supply chain. To get their perspective, we would like to interview a handful of maintainers from this group. I am happy to share questions in advance. This is a very friendly project and we are mainly looking for lessons to share with other maintainers to both encourage maintainership and identify ways to improve OSS software production processes. The output will be a 25-50 page eBook / White Paper published by LF Research. My email is [asalkever@contractor.linuxfoundation.org](mailto:asalkever@contractor.linuxfoundation.org) and I might be reaching out to you individually. If you want to participate, please ping me. I would be most grateful.
    * Package manager / repositories of particular interest include:
        * Maven
        * NPM
        * pip/PyPi
        * RubyGems
        * Gradle
        * Cargo
        * Helm
* [Patrick/Jvz Chainguard] #java in sigstore working on how best to sign multi-artifact releases
    * 
    * Would love input from other communities who might face the same problems, ideally we’ll have a shared solution. Related: [https://github.com/sigstore/rekor/issues/845](https://github.com/sigstore/rekor/issues/845)
* [Dustin] 
* [Jonathan]  Additional Questions added to: 
    * New questions added:

<table>
  <tr>
   <td>
B: Package Manager Security Audit - 'clear box test' - Server
   </td>
   <td>Has the package manager SERVER ever had an external security firm perform a 'clear box test' (aka. 'white box test') performed? If so, link to the public report
   </td>
  </tr>
  <tr>
   <td>C: Package Manager Security Audit - 'clear box test' - Client
   </td>
   <td>Has the package manager CLIENT ever had an external security firm perform a 'clear box test' (aka. 'white box test') performed? If so, link to the public report
   </td>
  </tr>
  <tr>
   <td>D: Package Manager Security Audit - 'PEN test' - Server
   </td>
   <td>Has the package manager SERVER ever been had an external security firm perform a penetration test (ie. PEN test) performed? If so, link to the public report
   </td>
  </tr>
  <tr>
   <td>E: Package Manager Security Audit - Vulnerability Disclosure Program (VDP)
   </td>
   <td>Does the package manager have an unrestricted (ie. no NDA) vulnerability disclosure program? If so, please link to it
   </td>
  </tr>
  <tr>
   <td>F: Package Manage Security Audit - Organization Audit - Red Team Engagement
   </td>
   <td>Has the ORGANIZATION hosting the package manager SERVER ever had an external security firm perform a Red Team engagement (ie. a technical & social engineering based attack) against the organization as a whole?
   </td>
  </tr>
  <tr>
   <td>G: Package Manager Security Audit - Vulnerabilities fixed
   </td>
   <td>Are all the vulnerabilities currently identified in SEC-4-B through SEC-4-F fixed? If not, why not?
   </td>
  </tr>
  <tr>
   <td>H: Package Manager Security Audit - Regular Retesting
   </td>
   <td>Are SEC-4-B through SEC-4-F performed on a recurring basis (ie. quarterly, bi-annually, annually, ect..)
   </td>
  </tr>
</table>


Action items



1. Lorenzo: how widespread? [is the problem of domain resurrection] ← zack to try to dig into this 
2. Jason has a java-specific doc, Jason to share with the community
3. Alex Salkever - list of intros to package repo maintainers
4. Patrick/Jvz - draft for multi-artifact signing best practices
5.  - review added survey questions 

<h3>May 11, 2022| OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=Inz5RCTCp60)

Attendees:



* Dustin Ingram (Google)
* Jason van Zyl (Apache Maven/Chainguard)
* Sumana Harihareswara (Python)
* Trevor Rosen (GitHub / npm)
* Jason Swank (Sonatype / Maven Central)
* Matt Rutkowski (IBM)
* Brad Beck (Citi)
* Jacques Chester (Shopify)
* Cheng Lee (Anaconda; conda)
* David A. Wheeler (Linux Foundation)
* Eddie Zaneski (Chainguard)
* Kevin Mittman US (NVIDIA; RPM/Debian)
* Brian Fox (Sonatype / Maven Central)
* Sterling Greene (Gradle)
* Josef Simanek (RubyGems)
* Patrick Flynn (Chainguard)
* Zachary Newman (Chainguard)
* Xuefei Han (JFrog)
* Caleb Brown (Google)
* Nils Adermann (Private Packagist / Composer / Packagist.org)
* Shaun Lowry (ActiveState)
* Drew Davidson (University of Kansas)
* Simon Kent (Google)
* Laurent Simon (Google)
* Jesse Sanford (Autodesk)
* Vinod Anandan (Citi)
* Mike Brown (IBM/containerd/OCI distribution/sig-node)
* Jacob Finkelman / Eh2406 (Cargo)
* Sterling Greene (Gradle)

Agenda:



* Welcome new friends
    * Kevin Mittman (NVIDIA; RPM/Debian)
    * Patrick Flynn (Chainguard)
    * Brad Beck (Citi)
    * Caleb Brown (Google)
    * Nils Adermann (Private Packagist / Composer / Packagist.org)
    * Drew Davidson (University of Kansas)
    * Shaun Lowry (ActiveState)
    * Xuefei Han (JFrog)
    * Jesse Sanford (Autodesk; Crossplane)
    * Jason Lutz (Chainguard)
    * Mike Brown (IBM/containerd/OCI distribution/sig-node)

* Reviewing Action Items
    1. Dustin/Jory - updated EMEA-friendly meeting 
    2. Dustin - doc on testing sigstore/tuf clients
    3. ?? - Features for Rekor entry discoverability / searching
    4. Brandon - follow up on features for survey address security audits/etc. 
    5. Asra - clean up draft doc on attestation bundles and share
    6. Myles: Out of band meeting of survey-fillers
    7. Zack: send out repository data collection proposal again
    8. Zack: write a namespacing doc
* [Jacques] Collecting malicious packages for researchers (raised by Mislav Boroš and Lorenzo De Carli in #general)
    * [David A. Wheeler] This would be helpful for package-analysis, another OpenSSF project, please share with that OpenSSF project as well. More info:
        * [https://openssf.org/blog/2022/04/28/introducing-package-analysis-scanning-open-source-packages-for-malicious-behavior/](https://openssf.org/blog/2022/04/28/introducing-package-analysis-scanning-open-source-packages-for-malicious-behavior/)
        * [https://github.com/ossf/package-analysis](https://github.com/ossf/package-analysis)
    * [David A. Wheeler] The “Backstabber’s Knife Collection” folks have a collection of malicious packages, they will share them if you ask & provide assurance you won’t attack others with it.
    * [Caleb] Package-analysis folks are very interested.
    * [Dustin] Do we have a sense of what format would be most useful? Metadata?
    * [Brandon] Included in known compromises or separate?
        * [Jacques] Separate
    * [Zach] Priority should be to retain packages and not completely disappear them
    * [Drew] W/ regards to academic research + format: as much metadata as possible
* [Shaun Lowry] Demo downloading malware packages from ActiveState’s mirror
    * [Shaun] Currently mirroring PyPI, RubyGems, CPAN, Packagist
    * [Malware Archivist tool](https://github.com/ActiveState/MalwareArchivist)
    * Uses ActiveState’s public APIs
    * Note: Many takedowns are because of legal reasons; they only archive ones that are malware
* [Dustin] Countering domain expiry attacks ([ref](https://twitter.com/lrvick/status/1523774962909298690)) - “foreach” example.
    * [Eddie Zane] Go world has a lot of custom domains. Vendor dependencies and check checksums
    * [Jason Swank] Maven Central has domain-based validation for namespaces, want to revalidate namespaces.  Also working to better understand the impact- dependants which are using the “latest” version of packages.
    * [David W] Don’t want to prevent custom domain use. The threats as I understand it are (1) password resets leading to takeover of an account (e.g., repo), and (2) takeover of the site used to describe/distribute the package in cases where the domain was used that way.
    * ?: Agreed, custom domains are a valid use case.
    * Loss/change of ownership of DNS perhaps should be considered a security event.
    * One thing that could be done: If an MX record goes away, disable the email account & must use something else to log in.
    * [Jacques] 2FA provides sufficient protection here. Alternatively: Make the attacker move in the open by writing domain changes to the transparency log
    * Jason Swank: yes, again on transparency logs.  A domain name expires, it is locked - and should be recorded in a transparency log. When it is renabled based on subsequent request - it should be recorded in a transparency log
    * [Brian Fox] Other attack vector is URLs that are contained by the metadata content
    * [David] Another approach is to create a group of “second eyeballs” to verify non-maliciousness of a new release - that way, subversion of any 1 account is unlikely to release malicious code. This problem is especially common in small npm packages where there’s only a few lines of code that almost never changes, and only a single developer, but if there’s malicious code inserted into the released package then a lot of people will have a bad day.
* [Jason van Zyl] Maven Sigstore update and demo: [https://github.com/jvanzyl/maven-sigstore](https://github.com/jvanzyl/maven-sigstore)
    * Relationship between artifact & signing certificate - not 1:1, cache keypair for a single signing session
* [Eddie Zaneski] ["package" entry type in Rekor](https://github.com/sigstore/rekor/issues/804) - a generic/general way to record package information that would work across ecosystems
    * Many +1s to using purl prefix 
    * If there’s no commonality, InfoSec engineers will have to deal with a large number of different formats, one for each ecosystem, and that would be a big pain for them
    * [Jacob Finkelman] How do we ensure this is useful across ecosystems?
    * Question: How do we define “package”? If we provide different packages for different situations for the same name & version #, are those different packages?
* [Laurent] Looking for comment for the Npm's Security Best Supply-Chain Practices: [npm.md](https://github.com/ossf/package-manager-best-practices/blob/main/review/npm.md). Review process described [process.md](https://github.com/ossf/package-manager-best-practices/blob/main/process.md). 
* [Laurent] We have been working on generating SLSA3+ provenance natively on GitHub using Sigstore's ephemeral keyless signing ([Google blog](https://security.googleblog.com/2022/04/improving-software-supply-chain.html), [GitHub blog](https://github.blog/2022-04-07-slsa-3-compliance-with-github-actions/)). Looking for interested package ecosystem who want to explore doing it

Action items



9. Dustin - close EMEA-friendly poll, update time
10. Zach - Doc to describe means to counter domain expiry attacks:
    

<h3>Apr 27, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://youtu.be/K2L0JjMiCjU)

Attendees: 



* Dustin Ingram  (Google)
* Jason van Zyl (Apache Maven)
* Yehuda Gelb (Checkmarx)
* Jack Aboutboul (AlmaLinux)
* Andrew Lukoshko (AlmaLinux)
*  Jason Swank (Sonatype / Maven Central)
* Brian Fox (Sonatype / Maven Central)
* Matt Rutkowski (IBM)
* Jeffrey Borek (IBM)
* Hervé Boutemy (Apache Maven)
* Jacob Finkelman / Eh2406 (Cargo)
* Sumana Harihareswara (Python packaging)
* Bob Callaway (Google)
* Jacques Chester (Shopify)
* Betty Li (Shopify)
* Ciara Carey (Cloudsmith)
* Cheng Lee (Anaconda/conda)
* Jenny Shen (Shopify)
* Brandon Lum (Google)
* Jory Burson (Linux Foundation)
* Lois Anne DeLong (NYU)
* Jack K (ControlPlane/nixpkgs)
* Marina Moore (NYU)
* Trevor Rosen (GitHub/npm)
* Shachar Menashe (JFrog)
* David A. Wheeler (Linux Foundation)
* Simon Kent (Google)
* Asra Ali (Google)
* Christine Abernathy (F5)
* Eric Tice (Wipro)
* Sandipan Roy (Red Hat)
* Josef Simanek (RubyGems)
* Jonathan Leitschuh (was at Gradle; security of OSS)

Agenda

* Welcome new friends
    * Sumana Harihareswara (Python packaging)
    * Cheng Lee (Anaconda, conda-forge, and friends)
    * Sebastien Awwad (Anaconda, NYU/TUF)
    * Jack K (ControlPlane; promoting nix packages)
    * Diego Rodriguez-Losada (Conan, C++ package manager)
    * Jonathan Leitschuh (was at Gradle; security of OSS)
    * Jack (AmaLinux)
    * Simon Kent (Google/GOSST, working supply chain integrity)
    * Asra Ali (Google)
    * Mikael Barbero (Eclipse Foundation)
    * Julie (Google, Go Security)
* [Dustin] Heads up for new attendees
    * David: Ok to say ‘aggressive no’ (no and object to it) to a feature! Maybe there’s a problem with a feature (at least in some situations) & it’d be good to know that.
    * Jonathan: Adding questions around previous audits?
        * Fair to add
    * Jonathan: Nix packages many different ecosystems & different ways: Rust, etc. How do we handle that?
        * Jacques: This is the first time we’re dealing with “package management over package management”
        * Conda does similar things (i.e., multiple ecosystems)
        * If there’s significant difference, maybe break it out?
        * David: I would focus on “what you do differently”, that is, if you depend on the Rust ecosystem & then build on that, let the Rust column(s) capture that part, and your column(s) capture what you do in addition.
        * In the end “whatever makes sense” to capture the information.
* Reviewing Action Items
    * ~~All: Agreement on WG members~~
    * ~~Members: Approve [https://github.com/ossf/wg-securing-software-repos/pull/4](https://github.com/ossf/wg-securing-software-repos/pull/4) ~~
    * Myles: Out of band meeting of survey-fillers
    * Zack: send out repository data collection proposal again
        * [i sent it out](https://openssf.slack.com/archives/C034CBLMQ9G/p1649929184589519), no major updates
    * Zack: write a namespacing doc
        * Written [as section in existing doc](https://docs.google.com/document/d/1mXrVAkUA9dd4M7fa_AJC8mQ55YnYJ-DKsGq30lh0FvA/edit#heading=h.hnafaao4ptv7)
* [Dustin] WG has been approved! 👏 [https://openssf.org/blog/2022/04/19/your-favorite-software-repositories-now-working-together/](https://openssf.org/blog/2022/04/19/your-favorite-software-repositories-now-working-together/) 
* [Asra] Attestation bundles formats (PKI, attestations, etc) (c/f [https://github.com/sigstore/cosign/issues/1743](https://github.com/sigstore/cosign/issues/1743))
    * Asra: How do we find and discover attestations, and their associated materials?
    * Asra: General discoverability, packaging of verification material
    * Asra: E.g., how do I bundle all the attestations I need? What if the attestations are out-of-band?
    * Jacques: In the RubyGems proposal: we put stuff in the TL, that someone is the author, at some point want to cache that next to the .gem, (same bucket same CDN)
    * Asra: How we verify the veracity of the signature is supported by the envelope
    * Jacques: This seems like a problem that everyone has to solve. Seems undesirable to have everyone making requests against Rekor
    * Asra: Your use case is on signatures but not attestations
    * Marina: Working on a similar problem: Uptane is working on bundling in-toto
    * Jacques: There is a wrinkle: we had a plan to upload more discrete attestations, e.g. security events as well as uploads. Haven’t thought through whether these should be stored alongside.
    * Jack: Interested in how artifacts will be linked to SBOMs, etc. Nix pkgs have something like provenance/attestations, shows every package that went into making that package.
        * [https://edolstra.github.io/pubs/phd-thesis.pdf](https://edolstra.github.io/pubs/phd-thesis.pdf) - p39 (PDF page 47) 2.4 Store Derivations
<img width="651" alt="image" src="https://github.com/ossf/wg-securing-software-repos/assets/128058721/8f32970f-35fc-4372-8f89-81a472235097">

        

* David: Here’s more information on sigstore specifically: :[https://docs.sigstore.dev/](https://docs.sigstore.dev/), e.g.:
    * Blobs: [https://docs.sigstore.dev/cosign/working_with_blobs](https://docs.sigstore.dev/cosign/working_with_blobs)
    * In-toto: [https://docs.sigstore.dev/cosign/attestation](https://docs.sigstore.dev/cosign/attestation)
    * Signing other types like SBOMs: [https://docs.sigstore.dev/cosign/other_types](https://docs.sigstore.dev/cosign/other_types)
    * Rekor signing & uploading: [https://docs.sigstore.dev/rekor/sign-upload](https://docs.sigstore.dev/rekor/sign-upload)
* Asra: We’re also thinking about the SBOM story, where hashes can be used to traverse links between packages
* Bob: The original design was there (to upload the entire blob) to verify (...?). We don’t persist the artifact, with the exception of in-toto attestations. We have to independently verify that the signature is correct. The intent is not for Rekor to be a package manager itself.
* Sebastien: In a transparency log, discoverability is a security feature, are there existing plans to create requirements for features to prevent attackers from making use of entries in the transparency log that evade discoverability?
* Asra: Indexing by hash means anyone can create an artifact linked to that hash. Can’t search without filtering capabilities. There have been requests for more complex searches
* Jacques: Attack scenario we thought of for rubygems was that a malicious user spams a billion entries for a valid artifact hash
* Bob: agree that there’s an issue that we need to work on more. There’s been discussions on how much needs to be built into Rekor vs. a search index over Rekor.
    * [https://github.com/sigstore/rekor/issues/191](https://github.com/sigstore/rekor/issues/191) 
* [Dustin] State of language-native Sigstore/TUF clients
    * Trevor: planning to start for node.js. No sigstore or TUF client. Working on baking into an RFC. Idea is to be able to directly support it w/in npm cli
    * Jacques: Actual interaction is w/in client code. Original thinking was to implement it in the client. One of the constraints for Rubygems is that the gem cli only relies on the stdlib or a very small number of gems. Signing would come as a plugin.
    * Dustin: Any demand for standalone sigstore libraries?
    * Jacques: Unsure for Rubygems
    * For NPM, yes
* [Jonathan Leitschuh] Focus on signing is great, there are other areas for focus (e.g. 2FA). What are folks thinking about for support/plans/thoughts/ideas?
    * Jacques: The survey is a good place to start for teasing out what folks are thinking about or have thought about
    * Jacques: Pushing a 2FA mandate for RubyGems (also other ecosystems)
    * Sumana: One survey: [https://blog.tidelift.com/the-current-state-of-two-factor-authentication-across-package-managers](https://blog.tidelift.com/the-current-state-of-two-factor-authentication-across-package-managers) - it’s from 2019 -- is there a public post/roundup somewhere that is more recent?
    * Jacques: Repository itself: Have a team at Shopify working on Rubygems, thinking about 2FA and signing. Also need help with day to day things, reviewing reports, bug bounties, etc.
    * Jonathan: How do we motivate broader work?
    * Dustin: [OpenSSF Selects Node.js as Initial Project to Improve Supply Chain Security](https://openssf.org/blog/2022/04/18/openssf-selects-node-js-as-initial-project-to-improve-supply-chain-security/) 
    * Sumana: One idea is getting users of that ecosystem to push (especially corporate users), e.g. tidelift surveying 2FA (see above). There will be new US federal regulations & hopefully new investment, that may end up pushing package managers in that direction. But I don’t want to wait around for that; will push, as we all will.
    * Cheng: Particularly for conda ecosystem, we’re thinking about securing a loose confederation of repositories and maintainers.
    * Bob: Reminder/+1 on motivating broader work. Opportunity is to continue to nurture the survey, come to a consensus on top X things that all ecosystems need to focus on (from the OpenSSF) or a call to the TAC/board. 

Action items



1. Dustin/Jory - updated EMEA-friendly meeting 
2. Dustin - doc on testing sigstore/tuf clients
3. ?? - Features for Rekor entry discoverability / searching
4. Brandon - follow up on features for survey address security audits/etc.
5. Asra - clean up draft doc on attestation bundles and share
6. Myles: Out of band meeting of survey-fillers
7. Zack: send out repository data collection proposal again
8. Zack: write a namespacing doc

<h3>Apr 13, 2022| OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://youtu.be/jSyYEQHpRAk)

Attendees:



* Dustin Ingram  (Google)
* VM Brasseur (Wipro)
* Josef Simanek  (RubyGems/RubyGems.org)
* Matt Rutkowski (IBM)
* Sterling Greene (Gradle)
* Octavia Togami (Gradle)
* Zachary Newman (Chainguard)
* Jacques Chester (Shopify)
* Betty Li (Shopify)
* Hervé Boutemy (Apache Maven)
* Jason Swank (Sonatype/Maven Central)
* David A. Wheeler (Linux Foundation)
* Christine Abernathy (F5)
* Appu Goudan (Google)
* Myles Borins (GitHub)
* Eddie Zaneski (Chainguard)
* Bob Callaway (Google)
* Jacob Finkelman / Eh2406 (Cargo)
* Jeff Borek (IBM)
* Vinod Anandan (Citi)

Agenda:



* Welcome new friends
    * Laurent Simon (Google)
    * VM (Vicky) Brasseur (WiPro)
    * Betty Li (Shopify)
    * Eddie Zaneski (Chainguard) - works on Kubernetes
    * Octavia Togami (Gradle)
* Reviewing Action items
    1. Dustin/Myles: Write up on how 2FA mandates are implemented
    2. Bob/Jacques Turn goals into a WG charter
    3. Zach: revise the integrating Sigstore doc
    4. Dustin/Myles: fill out [survey](https://docs.google.com/spreadsheets/u/1/d/12QlaYEtcp2ZwZRfZPHR4D3YpY8k770hYBeFQ6-N7Mts/edit#gid=1022416269) for npm / PyPI, also Nuget?
    5. Jonathan Leitschuh / Sterling: fill out survey for Gradle plugin portal
    6. Brandon/Zach: Sync up on refactoring form to be facilitate analysis
    7. Jacques/David: sync with critical projects WG on downloads dataset
    8. Marina/Zach/David: more crisp ask w/r/t data collection: schema, where it should live, whom we can get data from already, get it into the “goals doc”, coordinate with “scoring packages” WG[Integrating Sigstore with Artifact Repositories](https://docs.google.com/document/u/0/d/1mXrVAkUA9dd4M7fa_AJC8mQ55YnYJ-DKsGq30lh0FvA/edit)
* [Jacques/Bob] Update on WG repo, [readme](https://github.com/ossf/wg-securing-software-repos/blob/main/README.md) and [charter](https://github.com/ossf/wg-securing-software-repos/pull/4)
    * [Proposed “Maintainers” list](https://docs.google.com/spreadsheets/d/1ZzGp20ClSNWqyypxFL7yaMsBA2jivTGgoKpT_ujmqoA/edit#gid=1391015244)
    * Approvals / +1s to be made on the Charter PR
* [Wheeler] I think this WG has met the “5 meetings with multiple organizations” requirement - someone (a lead?) should ask the TAC to make this a formal WG. Include proposed scope & leads (I think that’s Dustin Ingram & Jacques Chester)
    * [bcallaway] it’s on the TAC agenda for April 19th to vote to approve
    * [Wheeler] okay, let’s just make sure the TAC knows it’ll be doing that vote. I expect 0 issues, I just want to make sure it’s done :-)
    * [bcallaway] agreed, i gave a heads up at last TAC meeting but once we vote to approve CHARTER.MD file (in this meeting), then I will email the TAC tonight to give a heads up.
* [Myles] if we do this can we do a poll to pick meeting times
* [Dustin] WG announcement for OpenSSF blog: 
    * Everyone please review!
* [Dustin] Update on 
* 
    * Now includes Python/Node
    * We have added a couple bullet points on the list to capture some missing security ideas (highlighted rows in magenta color)
    * We have added a additional sheet containing couple open questions to get some information about the layout of each ecosystem which will help provide insight and context to the answers
    * One of the open questions is also about requesting thoughts from folks on what is missing that we should include
    * Dustin and Brandon are working on a blogpost to share the work on this for more responses.
* [Marina/Zack] [Proposal for repository data collection](https://docs.google.com/document/d/1dxHxXgqy7t6e7IdNKa7Z0YJ2vkO0FTg7s_a-KNA5TEY/edit?usp=sharing)
    * Hoping to get buy-in+resourcing soon; would you participate (and if so, at what level)?
    * Dustin: Would this duplicate existing datasets?
    * Plan is to be somewhat unstructured, just so we can get the data at all from a centralized format. Over time intend to normalize so it’s easier to analyze for research purposes
* [Josef/Jacques] Scoped / namespaced gems [RFC](https://github.com/rubygems/rfcs/pull/40). Particularly looking for:
    * How much weight to give PURL
        * PURL will be added into SPDX 3, so for reporting SBOMs PURL is helpful
        * Nothing is impossible, but some are easier.
        * Sonatype: We experienced this (in Maven Central) & we understand it. We don’t expect users to directly interact with purls, but we don’t have to change anything to make purls work.
        * Rust is also looking at scoped namespaces, though not connected to domain names, instead “if you own package X” you can own subdomains of that: [https://github.com/rust-lang/rfcs/pull/3243](https://github.com/rust-lang/rfcs/pull/3243)
        * PyPI: namespace PEP is in progress :)
    * Experiences transitioning from non-namespaced to namespaced
* [Zack] Yet another [Integrating Sigstore with Artifact Repositories](https://docs.google.com/document/u/0/d/1mXrVAkUA9dd4M7fa_AJC8mQ55YnYJ-DKsGq30lh0FvA/edit) update
    * Now contains: various identity solutions, associating identities and accounts
    * Please let me know if I missed anything on those questions in the doc
    * Hope to expand to cover other issues
* [Zack] are we ready to invite the world?
    * There’s a lot of package managers not represented
    * We had talked before about not being quite ready to handle the influx
* [Zack] Can we produce quick external reports on progress (like 2-3 paragraphs)?
    * This is perhaps covered by Dustin’s announcement for the OpenSSF blog above, but maybe we want to do this monthly?

Action items:



1. All: Agreement on WG members
2. Members: Approve [https://github.com/ossf/wg-securing-software-repos/pull/4](https://github.com/ossf/wg-securing-software-repos/pull/4) 
3. Myles: Out of band meeting of survey-fillers
4. Zack: send out repository data collection proposal again
5. Zack: write a namespacing doc

<h3>Mar 30, 2022 | OpenSSF Securing Software Repositories (EMEA-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=wewPU02J7WU)

Attendees:



* Dustin Ingram (Google)
* Trishank Kuppusamy (Datadog)
* Zachary Newman (Chainguard)
* Jason Swank (Sonatype / Maven Central)
* Yehuda Gelb (Checkmarx)
* Jacques Chester (Shopify)
* Jenny Shen (Shopify)
* Brandon Lum (Google)
* Marina Moore (NYU)
* Sterling Greene (Gradle)
* Hervé Boutemy (Apache Maven)
* Jory Burson (Linux Foundation)
* Joel Orlina (Sonatype / Maven Central)
* Rick Briganti (Sonatype / Maven Central)
* Brian Fox (Sonatype / Maven Central)
* Ciara Carey (Cloudsmith)
* Myles Boris (GitHub)
* Jacob Finkelman / Eh2406 (Cargo)
* Lakshmi Mohandas (Sonatype)
* Asaf Karas (JFrog)
* Shachar Menashe (JFrog / Artifactory)
* Bob Callaway (Google)
* David A. Wheeler (Linux Foundation)
* Michael Komraz (Snyk)
* Lois Anne DeLong (NYU)
* Josef Simanek (RubyGems)
* Tracy Miranda (Chainguard)
* Joshua Lock (VMware)
* Christine Abernathy (F5)
* Jonathan Leitschuh (Dan Kaminsky Fellowship @ Human Security)
* Eric Tice (Wipro)
* Yotam Perkal (Rezilion)

Agenda:



* Welcome new friends
    * Sterling from Gradle
    * Jory from Linux Foundation to help out
    * Lakshmi from Sonatype / Maven Central
    * Joel from Sonatype / Maven Central
    * Eric from Wipro’s OSPO
    * Miki from Snyk team researching supply chain security
    * Jenny from Shopify
    * Tracy from Chainguard
    * Asaf from JFrog security
    * Shachar from JFrog security
* [dustin ingram] Housekeeping
    * Shared drive in OpenSSF org for docs: [https://drive.google.com/corp/drive/folders/19rkJhu88XanJQUsoRXu8GJyjojcv-yeR](https://drive.google.com/corp/drive/folders/19rkJhu88XanJQUsoRXu8GJyjojcv-yeR)
* [jacques] [New MFA policy for RubyGems accepted by maintainers](https://github.com/rubygems/rfcs/pull/36) - top 100 gems as computed by # of downloads.
    * NPM has had great success with a similar policy
        * Computed by dependencies rather than downloads
        * Some downloads that were not actually widely distributed
        * High-impact: >1M weekly download, >500 dependents
        * Phase-in: Maintainers in “limbo” where their actions are very limited (but they can still publish: don’t want to break CI/CD deployments). This is implemented by the repo itself; anything other than publishing is blocked until they have 2FA
    * PyPI is going to do this (top 1% ~=3500 packages)
        * Giveaway of security keys
        * Draft PR: [https://github.com/pypa/warehouse/pull/10856](https://github.com/pypa/warehouse/pull/10856) 
        * Trishank: [We found](https://www.usenix.org/conference/nsdi16/technical-sessions/presentation/kuppusamy)  (Section 7) a lot of “abandonware” - doesn’t seem to be actively developed but is widely used. We considered *preventing* updates without additional checks for the old but appear to be not-maintained packages, though we haven’t done it.
    * GH doesn’t expose whether accounts are using 2FA (for reasonable security reasons)
        * But it would be quite useful for downstream
        * NPM, Crates blocked on “sign-in with GH”
            * [https://openid.net/specs/openid-connect-core-1_0.html#acrSemantics](https://openid.net/specs/openid-connect-core-1_0.html#acrSemantics) 
    * Npm taxonomy of Abandonware
        * Dormant: <300 downloads, no dependents (allows self-serve delete; otherwise can’t delete at all)
        * Squatted: dormant + no actual functionality in the package
* [zack] [Integrating Sigstore + Artifact Repositories](https://docs.google.com/document/d/1mXrVAkUA9dd4M7fa_AJC8mQ55YnYJ-DKsGq30lh0FvA/edit#heading=h.jyrb6etgzah)
    * (Intro to Sigstore, especially Fulcio)
    * Third-party IDPs and pseudonymity (can authenticate w/o explicitly identifying oneself thru Google, GitHub, etc)
    * Please read and leave comments!
    * [dustin] Seems important to decouple IDPs from repos so that a total compromise is harder
        * But it still seems important to couple identities with repos
        * Seems like we always need some level of trust
    * It’d be good to record “why did the repo accept the update” - don’t care if they use a burner email address, just need to know why it was accepted.
    * Don’t want to trust the repositories [too much?]
    * “Trust on first use” doesn’t work so well, because things change over time.
* “Grab name on first request” is what a lot of repos use, but there are many problems with it. Maybe need to think about namespaces that can be automatically validated
    * Sonatype has created a number of tools to help with this, could be provided. E.g., link to an organization. E.g., who can post from Tesla.
    * [trishank] Something like an ACME challenge might work here: demand whichever pseudonymous entity it is that it still owns the GitHub repo and so on, like Brian seems to be alluding here
    * [josh] I believe Maven does it on domain name ownership
    * Java uses reverse naming based on DNS, maven copies that, that enables tight enforcement up-front. Other languages don’t do that.
    * [https://blog.sonatype.com/why-namespacing-matters-in-public-open-source-repositories](https://blog.sonatype.com/why-namespacing-matters-in-public-open-source-repositories) 
    * Jacques: I’m jealous of that :-)
    * Myles Borins: I’m not convinced, DNS records are a pain, having low barrier to entry is valuable. Don’t want to privilege corporations.
        * Brian F.: We actually provide multiple dns based validations here, including the ability to use eg. io.github.[project] and validations against that at the project level. The main point is to provide a low friction way to ensure someone can’t pretend to be a project they aren’t, which I’ve asserted in the blog above is why we see all these attacks in ecosystems that don’t have this validation  (70,000+ in the last year) vs Central (none). Details on the coordinates and validations are here [https://central.sonatype.org/publish/requirements/coordinates/](https://central.sonatype.org/publish/requirements/coordinates/)
    * [trishank]
        * I don't think there's a perfect, cryptographic way to solve the identity problem TBH
        * It reminds me of that NFT hack yesterday with 5/9 threshold signatures: doesn't matter if 4 of them were the same identity basically
        * We can make things like domain name verification *optional*, but add value to it by having repo add like verification checkmarks ala social media
        * ​​Really, the best you can here I think is like Keybase: show _multiple_ signals of ownership: you own the GitHub repo, the domain name, the Twitter account, etc
        * The more signals, the more trustworthy
    * [David A. Wheeler] It's not *that* hard to get a domain name though. :-)
    * This is something that needs more discussion, need to get to next agenda items.
* [marina,brian,zack] software repo data collection
    * We think that data on software repositories can help understand supply chain risks, and the LF would be a good steward of this data:
        * What packages are most vulnerable? (Most downloaded as an indirect dependency)
        * How much of a problem is typosquatting? Can we design policies to prevent it without too many false positives?
        * At what scale do repo security solutions need to operate?
        * Fraud detection
        * Generally useful resource for researchers (academic, nonprofit)
    * Proposal: add “data collection” to the WG charter
    * Proposal: collect daily upload/download counts for repositories that can provide it
    * [trishank] There might be privacy concerns, but I’m sure we can figure it out with things like k-anonymity, differential privacy, and so on
    * PyPI has been hosting [a public dataset](https://packaging.python.org/en/latest/guides/analyzing-pypi-package-downloads/) for a few years, hosted by Google, but users are locked into BigQuery. We don’t plan to get rid of that, but a way to roll that into something more approachable would be great.
    * Rubygems has [a daily dump of database](https://rubygems.org/pages/data) + [downloads info](https://ui.honeycomb.io/ruby-together/datasets/rubygems.org)
    * Crates.io has periodic dumps
    * Modulecounts.com presents high-level counts of available packages over time
    * ?: Daily downloads - can get what was downloaded
    * It’d be nice to have a consistent schema. It could be trivial, e.g., simple rows with nullable columns.
    * Let’s talk with the critical projects WG about data collection needs.
    * People who willing to help: David A. Wheeler, 
* [brandon] Call to action on [Survey/Landscape spreadsheet](https://docs.google.com/spreadsheets/u/1/d/12QlaYEtcp2ZwZRfZPHR4D3YpY8k770hYBeFQ6-N7Mts/edit#gid=1022416269) + discuss some comments around 
    * Typosquatting
    * Scoring
    * [trishank] Should we build a threat model? Doesn’t have to be the same for everyone, but helps to have a baseline at the very least. Otherwise, it’s not clear what risks we are solving for or not.
* [david wheeler] WG charter - what’s the status?
    * Where’s the charter draft text? Let’s finish a draft of that.
        * Draft of some goals: 
    * Template: [https://github.com/ossf/project-template](https://github.com/ossf/project-template)
    * atendeesWe need 5 meetings, we’ve had 4.
    * We need charter with scope text & initial WG lead, send to TAC to make this WG all official, then we can feature it

Action items



1. Dustin/Myles: Write up on how 2FA mandates are implemented
2. Bob/Jacques Turn goals into a WG charter
3. Zach: revise the integrating Sigstore doc
4. Dustin/Myles: fill out [survey](https://docs.google.com/spreadsheets/u/1/d/12QlaYEtcp2ZwZRfZPHR4D3YpY8k770hYBeFQ6-N7Mts/edit#gid=1022416269) for npm / PyPI, also Nuget?
5. Jonathan Leitschuh / Sterling: fill out survey for Gradle plugin portal
6. Brandon/Zach: Sync up on refactoring form to be facilitate analysis
7. Jacques/David: sync with critical projects WG on downloads dataset
8. Marina/Zach/David: more crisp ask w/r/t data collection: schema, where it should live, whom we can get data from already, get it into the “goals doc”, coordinate with “scoring packages” WG

<h3>Mar 16, 2022 | OpenSSF Securing Software Repositories (APAC-friendly)</h3>

[Recording](https://www.youtube.com/watch?v=FGouzkUTYQk)

Attendees:



* Dustin Ingram  (Google)
* David A. Wheeler (Linux Foundation)
* Marina Moore (NYU) 
* Zachary Newman (Chainguard) 
* Appu Goudan (Google)
* Tim Lehnen (Drupal) [tim@association.drupal.org](mailto:tim@association.drupal.org) 
* Jason Swank (Sonatype / Maven Central)
* Bob Callaway  (Google)
* Jacques Chester (Shopify)
* Hervé Boutemy (Apache Maven, hboutemy@apache.org)
* Ciara Carey (Cloudsmith)
* David Strauss (Drupal/Pantheon)
* Hayden Blauzvern (Google)
* xjm (Drupal/Acquia)
* Josef Šimánek (RubyGems.org)
* Yotam Perkal (Rezilion)
* Brian Fox (Sonatype / Apache Maven /  brianf@sonatype.com)

Agenda



* Welcome new friends
    * Ciara Carey from Cloudsmith
    * Jess (xjm on Drupal.org, TUF signing for Drupal with a Composer client / hopefully 	eventually for Packagist although we have no control over that)
    * Tim Lehnen (hestenet - Drupal project, Drupal Association CTO)
    * Jason Swank (Sonatype, Maven Central)
    * Brian Fox (Sonatype, Apache Maven)
    * Jason van Zyl (nascent sigstore prototype for Java artifacts)
    * Hervé Boutemy (Apache Maven)
    * David Strauss (David Strauss on Drupal.org, TUF signing for Drupal / packagist, Pantheon CTO)
    
* At first we’ve focused on language ecosystems but we’re not exclusive to that (e.g., system packages, Drupal plug-ins, containers, etc.)
* Following up on previous action items:
    * Dustin Ingram - figure out scheduling & permissions w/ LF
        * This meeting now alternates between APAC- and EMEA-friendly times
        * OpenSSF Public Calendar: [Get Involved - Open Source Security Foundation](https://openssf.org/getinvolved/) 
        * Group: [https://groups.google.com/g/ossf-wg-securing-software-repos](https://groups.google.com/g/ossf-wg-securing-software-repos) 
    * Jacques Chester / Bob Callaway - Draft goals for the group
    * Dustin Ingram - Start spreadsheet/survey of software repos w/ group
        * <- Zack’s half-baked sheet with some ideas, to be superseded but maybe something interesting in there
        * Brief discussion about signing. Many repos support cryptographic signing (e.g., Python, Ruby [https://guides.rubygems.org/security/](https://guides.rubygems.org/security/) ), but it’s so hard sign and/or verify that it’s unused. Npm signs all packages, but those signatures are from npm not the developers, so it’s not significantly better than just using TLS (it does counter some attacks but not others). Maven has many signatures.
    * Zachary Newman  - Design doc or issue for neutral IdP from Sigstore
        * [Support a "neutral" IdP](https://github.com/sigstore/fulcio/issues/444)
        * Interesting discussion on the issue, which will clear the path to write a doc soon.
    * Trishank Kuppusamy (Datadog)- Invite PHP ecosystem
        * Welcome PHP folks!
*  Marina Moore  - Data from package repos for research project
    * Academic research project on scaling security for large repositories
    * Also would like to learn more about characteristics of load on repositories (uploads, downloads)
    * Need data from repository operators:
        * Either upload/download logs (anonymized)
            * [https://packaging.python.org/en/latest/guides/analyzing-pypi-package-downloads/](https://packaging.python.org/en/latest/guides/analyzing-pypi-package-downloads/) - [di@python.org](mailto:di@python.org) (this is perfect, thanks Dustin!)
            * Ruby
                * [https://rubygems.org/pages/data](https://rubygems.org/pages/data)
                * [https://rubygems.org/stats](https://rubygems.org/stats)
                * [https://ecosystem.rubytogether.org/](https://ecosystem.rubytogether.org/)
                    * recently added uniq IP filter ([https://github.com/rubytogether/ecosystem/pull/473](https://github.com/rubytogether/ecosystem/pull/473), [https://github.com/rubytogether/kirby/pull/20](https://github.com/rubytogether/kirby/pull/20)  
                    * visible with hidden param [https://ecosystem.rubytogether.org/?unique=true](https://ecosystem.rubytogether.org/?unique=true)
            * Maybe worth to ping [https://libraries.io/](https://libraries.io/) (Josef - I know some people behind if needed)
            * PHP/Packagist: [https://packagist.org/statistics](https://packagist.org/statistics) 
                * Usage(not downloads) from installs phoning home for Drupal core: [https://drupal.org/project/usage/drupal](https://drupal.org/project/usage/drupal) (heavy caveat: This data is based on the update.module, and it is a sometimes-best practice to disable said module in production, so it is missing a lot of sites)
            * One BIG challenge is that download statistics is often hard to convert into usage - e.g., CI pipelines may download many times, or a single download may get put into a Linux distribution
                * One way: monitoring what’s loaded into memory on production systems, so can see what packages are being used. - see Yotam Perkel, his company does that.
                * See https://github.com/rubytogether/kirby/pull/20 + https://github.com/rubytogether/ecosystem/pull/473.
        * OR a few aggregate statistics that can be computed from anonymized logs
    * Email Marina

Notes



* 

Action items



1. Zachary Newman: write a doc about sigstore/IdP <-> artifact provider integrations
    1. [Integrating Sigstore with Artifact Repositories](https://docs.google.com/document/u/0/d/1mXrVAkUA9dd4M7fa_AJC8mQ55YnYJ-DKsGq30lh0FvA/edit)
2. Marina and Zachary promise “a pretty cool demo” of their research on downloads
    2. This is O(months) away

<h3>Mar 3, 2022</h3>

[Recording](https://drive.google.com/file/d/1OLcJ4f7L5xRzfAxJZEr-_l1UIC3X9uqh/view)

Attendees:



* Dustin Ingram 
* Jacques Chester
* Joshua Lock 
* Eric Tice
* Roch Lefebvre
* Bob Callaway
* Zachary Newman 
* Myles Borins 
* Yehuda Gelb
* David A. Wheeler
* Jacob Finkelman (Eh2406)
* Jussi Kukkonen
* Georg Kunz
* Trevor Rosen
* Yotam Perkal
* Josef Šimánek
* Ashley Ellis Pierce

 

There's an issue with the Google Meet link that the LF provided, please use this instead for today's meeting: [https://meet.google.com/gnz-gvcf-xks](https://meet.google.com/gnz-gvcf-xks) 

Agenda:



* [Wheeler/Trishank] Scope
    * What can everyone agree should be the ultimate outcomes?
    * Roadmap
* Vote on chair
    * Dustin Ingram voted as chair
* [Trishank] Steering committee?
    * At least a member from each community repository
    * [Wheeler] Too early for SC, but let’s list the communities represented so we can figure out “who’s missing” to try to engage them - make that part of the spreadsheet (separate tab?)
* [Jacques Chester] Neutral OIDC provider
* [Joshua] outreach to other ecosystems? Wait until we are better established?
    * Which ecosystems are represented in the current attendee list?
* Introductions and new faces

Notes



* Scope
    * Good to have an open discussion space, but risk of no action. Desire to have concrete changes and improvements coming out of OpenSSF groups.
        * General sentiment – anti-goals: no desire to be all talk and no action, no desire to do deep architecture by committee.
    * Suggestion (Wheeler): Don’t want this to be just discussion, want actual changes to result. Helpful to have something specific we’re working on. E.g., enumerate features of each repository that other repositories may wish to implement – document of feature, status (and intent) for each repo.
    * (Myles) At a high-level, agree on useful approaches/architectural components (SBOM, OIDC, etc).
        * Holding space for vendor neutral discussions is extremely valuable, regardless of agenda.
    * (Trishank) Yes, we shouldn’t be remotely prescriptive (e.g., SHALL, MUST) now, but wonder whether in the long-term we want consistent formats and tooling. In other words, do we care about eventually arriving at the equivalent of the TLS of codesigning?
    * (Jacques) Personal goal: agree on events to store in the (a?) transparency log
    * [dustin] Personal goal is to have a forum to lean on the experience of other similar ecosystems when improving our own ecosystems
    * [yaacov/Jacob/Eh2406] Want to push back on the goal that we all align on the exact same tooling
    * [Eric Tice] sync on overlap between well-vetted areas
    * [David W] Short list of what the top/most effective ideas are would be a good outcome to help folks prioritise implementation. If we don’t work on something, we’re all busy & it risks being just talking with no results.
    * [Myles] Has a spreadsheet of the various package repositories and their capabilities – could be a good shared starting point
    * [Myles] We can provide a space to help identify contributors to implement desirable features for not-for-profit content repositories.
    * SO: Next meeting, let’s create a Google docs spreadsheet on “what repos are doing”
* Steering committee
    * [trishank] Having things in a roadmap? Committee is possibly too early.
    * [david] Possibly too early, but let’s identify who’s part of which groups
    * Communities represented:
        * Community - name
        * RubyGems
            * Josef Šimánek
        * npm
            * Myles Borins
            * Trevor Rosen
        * Cargo
            * Jacob/Yaacov/Eh2406
        * PyPI
            * Dustin Ingram 
        * Nuget
            * ?
* Neutral OIDC provider
    * Forked from [this discussion of email verification](https://github.com/sigstore/fulcio/issues/371)
    * Tl;dr: in discussion of [RubyGems RFC](https://github.com/rubygems/rfcs/pull/37) concerns were [raised](https://github.com/rubygems/rfcs/pull/37#issuecomment-1024591418) about requiring accounts with big tech orgs in order to get the benefits of sigstore integration. Alternative proposal, having sigstore support stateless email login flow (OIDC-over-SMTP). To do this flow securely would reinvent OIDC, so little appetite to implement. We can get some of the benefits by having a neutral OIDC provider, that may fall in the mandate of this group/wider OpenSSF.
    * [Jacques] Wrinkle. [Explored RubyGems being an OIDC provider](https://github.com/rubygems/rfcs/pull/37#issuecomment-1029405788), but that provides SPOF. Neutral OIDC provider regains separation. Anticipate most people would just use vendor options, but for full coverage need an independent OIDC provider. There’s a common interest in such a provider.
    * [Dustin] How would a neutral provider become aware of supported identities?
        * [Jacques/Trishank] proof-of-identity e.g. keybase
    * [Jacques] Each ecosystem standing up it’s own IdP would be a mistake, lose economies of scale in defense, multiply our collective efforts
    * [Marina] Would an attacker who has gained access to a repo account be able to prove identity?
        * [Jacques] Yes, this is why we need to publish additional events to the transparency log
    * i think there is oidc support for expressing whether 2fa was involved: https://openid.net/specs/openid-connect-core-1_0.html#acrSemantics (but many idps do not support it)
    * [David] I have an email address on my own domain, as do many others - a way to make this especially easy & yet secure would be great, one that is clearly documented so people can *easily* do things.
* Outreach
    * Missing: Drupal/PHP/composer, Gradle, Maven, Haskell/Hackage, OPAM, Swift, Homebrew, CPAN, Mamba, Conda, Spack, Flatpak, Chocolatey, Vcpkg, Helm, Julia’s Pkg, Conan?, Alire
    * PackagingCon could be a good place to look for ecosystems
    * One list: [http://www.modulecounts.com/](http://www.modulecounts.com/)
    * Another: [https://libraries.io/](https://libraries.io/)
    * “CPAN had interesting thoughts on testing & dependency trees”
    * Are os package ecosystems in scope?
        * Yes, the lines are fuzzy enough that there is shared scope
    * Let’s figure out goals before we cold-call, invite folks we know already.
* Meta
    * Scheduling, should we alternate between APAC and EMEA friendly times?

Action items



1. Dustin Ingram - Start spreadsheet/survey of software repos w/ group
    1. Identify effective security measures implemented by at least one, then identify which repos/package managers implement it or not
    2. Include a champion/stakeholder/representative for each group
2. Jacques Chester /Bob Callaway - Draft goals for the group
3. Zachary Newman - Design doc or issue for neutral IdP from Sigstore: [Support a "neutral" IdP](https://github.com/sigstore/fulcio/issues/444) in fulcio, separate issue for “integration with package manager” coming
4.  Trishank Kuppusamy  - Invite PHP ecosystem
5. Dustin Ingram - figure out scheduling & permissions w/ LF

<h3>Feb 16, 2022 | Sigstore + package managers collaboration</h3>


Attendees: Appu Goundan

axel@redhat.com

Bob Callaway

Dustin Ingram

Philip Harrison

Zachary Newman

Jacques Chester

Joshua Lock

Jussi Kukkonen

mm9693@nyu.edu

Phillip Mendonça-Vieira

roch.lefebvre@shopify.com

Trevor Rosen

trishank.kuppusamy@datadoghq.com

Brandon Lum

Agenda



* Ruby: Quick rundown of [https://github.com/rubygems/rfcs/pull/37](https://github.com/rubygems/rfcs/pull/37) 
* Python: Update on [https://www.python.org/dev/peps/pep-0480/](https://www.python.org/dev/peps/pep-0480/) 
* npm: Plan for npm integration
* Open questions/discussion:
    * signing identities & identity providers
    * resurrection attacks
    * signature formats & distribution
    * Finding commonalities

Notes



* Ruby
    * Proposal to gradually turn MFA on by default for publishers
    * Improving gem-signing mechanism (complete replacement)
        * Trades key-management for identity management
    * Sigstore-backed solution, complimentary to TUF
    * Identity providers: what sigstore already supports (google/microsoft/github)
    * Using email address as subject has been a contentious point
        * Concern about immutable log of “personal” contact details
        * Concern about linkage between known RubyGems id and less well known email address
            * Initially assumed a stronger correlation between maintainer handles and their email addresses – but email address is not public, so linkage to handle isn’t public
        * Concern about using large vendors as identity providers
        * Looking at alternatives to email in code-signing certificate
            * RubyGems as id provider – but SPOF (only need to compromise RubyGems, rather than Gems + identity provider)
        * Does Gems verify whether the signature identity is approved for the Gem publication?
            * Considering having the repo look up signatures by package digest at upload time and ensure signature identities correspond to authorised maintainers
        * Rubygems generally thinking about pushing other events to the transparency log as well (maintainer added/removed, yanks, etc)
* Python/PyPI
    * [PEP 458](https://www.python.org/dev/peps/pep-0458/): PyPI signs all packages
        * Protects against roll-back attacks and on-path attackers, allows for revocation
        * Why? Partly to avoid difficulties with developers signing
        * Roadmap: [https://github.com/pypa/warehouse/issues/10672](https://github.com/pypa/warehouse/issues/10672) 
        * Uses online keys (not Sigstore) backed by offline root keys
        * Lays groundwork for ….
    * [PEP 480](https://www.python.org/dev/peps/pep-0480/): PyPI delegates to developers if they wish
        * Now developers can sign with their own keys
        * Axel Simon’s update to use Fulcio for throwaway/keyless keys: [https://github.com/axelsimon/peps/pull/1](https://github.com/axelsimon/peps/pull/1) 
        * Identity provider: plan to have PyPI be an IdP for PyPI signing with Sigstore/Fulcio
            * Makes PyPI the SPOF for compromise in _some_ cases (where PyPI is IdP and repository)
        * Roadmap (TBD)
    * Both PEPs based on ideas from [Diplomat](https://www.usenix.org/conference/nsdi16/technical-sessions/presentation/kuppusamy)
    * Future/ultimate vision: recording TUF timestamps (which can point to [in-toto](https://in-toto.io/) metadata) on Rekor
        * [https://ssl.engineering.nyu.edu/blog/2020-02-03-transparent-logs](https://ssl.engineering.nyu.edu/blog/2020-02-03-transparent-logs)
        * [https://www.youtube.com/watch?v=PJ6b2eoq0NY&list=PLj6h78yzYM2NOCoaYcYbiAf4KPIF36T8t&index=12](https://www.youtube.com/watch?v=PJ6b2eoq0NY&list=PLj6h78yzYM2NOCoaYcYbiAf4KPIF36T8t&index=12)
* npm
    * **Extremely** early in this process
    * Focusing on making npm a Relying Party for a set of OIDC IdPs, integrating w/ Sigstore
    * Interested in effectively “decorating” claims from IdP w/ maintainer info originating with npm
    * Also starting to look at an effort around improving existing registry signatures via TUF
                        * Implementing a “band-aid” for existing registry signatures: moving away from the PGP-based approach we have today to a KMS-based approach (not a complete solution, but better than what we have now)
    * Nuget also interested
    * SLSA for builds? Trevor: north star for the team
    * Like RubyGems, also working on signature bundle/storage to avoid live lookups
* Q: signature formats & distribution?
    * Ruby:
        * rubygems would look up signatures in Rekor at upload time using digest of given payload, keep them 
        * What would we be downloading? Log entry in JSON form, already signed
        * Repo itself would need to acquire the public key for Rekor (via [TUF client workflow](https://theupdateframework.github.io/specification/latest/#detailed-client-workflow))
            * Sigstore has TUF protected [root of trust](https://github.com/sigstore/root-signing) for the sigstore infra certificates enabling thresholds (i.e. multi-party root signing on public good infra), key-rotation, and revocation on root of trust
        * If we supported many signature per package, would need to bundle them
        * Bundling would require handling:
            * Expiring signatures (see [cosign#1342](https://github.com/sigstore/cosign/issues/1273))
            * Rotating SigStore keys
            * Rotating, other TUF repository keys
* Q: signing identities & identity providers?
    * Python:
        * Plan is for PyPI to become an identity provider
        * Federate with GitHub actions identity
        * Support multiple signatures per artifact
            * Need to think about which level(s): Rekor, TUF, SLSA/in-toto, etc
    * Jacques: probably need to lobby for querying operations to become richer / more efficient
        * Existing issue in [rekor](https://github.com/sigstore/rekor/issues/191)
            * Cloudevents support ([issue](https://github.com/sigstore/rekor/issues/592))
            * Insecure query mechanism via bigquery
        * Must be able to handle [spam](https://access.redhat.com/articles/4264021)
* Q: resurrection attacks?
    * When an account is deleted and re-introduced (with the same handle) by a malicious party
    * GitHub adding more claims to OIDC token (uid & repo id)
    * Rubygems: vulnerable, handle is up for grabs after deletion, profile URI accepts username or ID
        * Can sign based on profile, but based on internal ID for users
    * PyPI: similarly vulnerable, no unique ID available
    * npm: not certain
* Finding commonalities
    * All have similar targets on their backs, let’s work together :-) 

Action items



1. Jacques to reach out to OpenSSF re: setting up a WG on registry protections w/monthly discussion
    1. See here: [https://github.com/ossf/tac/issues/79](https://github.com/ossf/tac/issues/79)
2. Bob to create/find an issue regarding Rekor query efficiency / richnesscreate/refer to rekor issue on adding better query support
3. Atul to share spec on additional claims added to GitHub OIDC token
