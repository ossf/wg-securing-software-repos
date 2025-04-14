# Crafting a Package Deletion Policy

Author: [Hayley Denbraver](https://www.github.com/hayleycd)
Last updated: April 2025

## Background

In 2016 after a dispute about the naming of an open source package, a maintainer deleted all the packages he had published to npm, including a small package called `left-pad`.
Although `left-pad` was only about a dozen lines of code, it had impressive reach.
Prior to removal, it had over 15 million downloads and was used by thousands of open source projects--including many that are critical to the npm ecosystem.
The deletion of `left-pad` caused build failures for projects large and small and rendered a large portion of the internet unnavigable. Npm made the decision to republish the package.

[After the `left-pad` incident](https://en.wikipedia.org/wiki/Npm_left-pad_incident), npm updated their package deletion policy to prevent similar failures and other package registries followed suit.
In the over 9 years since the incident, package registries have continued to adjust their package deletion policies to balance the sometimes competing interests of open source maintainers, open source consumers, and the package ecosystem itself.

This paper outlines the components of modern package deletion policies.
It is not meant to be a sample deletion policy, but a list of things to consider when crafting such a policy including package deletion alternatives.

## Defining Terms

Package deletion policies are nuanced and terminology varies slightly between ecosystems. For the purposes of this paper, the following terms apply:

* Deleted package: A deleted package is no longer available for download or installation and is removed from the package registry. If a user attempts an install, their build will break. An ecosystem might also use the term "unpublished" to convey the same idea.
* Yanked version: A yanked version (or range of versions) is not removed from the package registry, but installers will ignore the version unless it is the only release that matches a version specifier. The term "retracted" is also used. 
* Deprecated package/deprecated version: A deprecated package/version is still available to install but has been marked by the author as no longer supported.

## Deletion Policy Considerations

If we consider a hypothetical package deletion policy, it would exist on a spectrum somewhere between never allowing packages to be deleted to allowing packages to be deleted without any restrictions.
Both ends of this spectrum are impractical.

* Never allowing for package deletion could result in the publishing of malicious, abusive, illegal, or copyrighted content without any recourse.
* Allowing for unrestricted package deletion could result in build failures like those seen in the `left-pad` incident, malicious packages snapping up a recently deleted package name, and other undesirable behavior.

So when crafting a deletion policy, we want to stay away from the two extremes, but what needs to be considered?

Whether or not a package registry allows for users to delete packages in some cases, it should allow for the package registry administrators to manually intervene and delete packages.
This allows the administrator team to protect the ecosystem from malicious, abusive, illegal, or copyrighted content. In these cases, the administrator team will need to delete a package even if doing so causes problems for users.

But what if a user wants to delete a package they published?
Although it's possible to require such cases to go to the administrator team to be manually reviewed and removed, that is not a very efficient policy.
Such a policy would place a burden on the (already likely overworked) administrator team, and the ecosystem would be cluttered with the unwanted packages until they are manually removed.

Allowing a user to delete their package in certain cases is therefore good for the user, the package registry administrator team, and the package ecosystem at large.
But what factors need to be considered to minimize the risk of a `left-pad` style incident?

## Ecosystem Impact

A modern package deletion policy aims to minimize the impact a given deletion could have on the ecosystem, while granting authors some flexibility with their packages.

The following considerations are generally used when determining whether a package is a good candidate for deletion, although specific limits and criteria will vary between package registries.

### Time

How long ago was the package published?
Although time since publication is not a perfect metric for ecosystem impact, there are a number of use cases where this metric is very relevant.
For example, the user could have:

* Published the wrong package
* Published the package with an unintended name (or a typo)
* Published a test package to understand and experience the package publishing process

In these cases, it is very useful for the package registry to have a no-hassle deletion policy as long as the package has been published for less than a certain amount of time.
For instance, npm allows maintainers to delete their packages within the first 72 hours after publication.
After 72 hours additional criteria must be met.

### Downloads

How many times has the package been downloaded?
Package download statistics provide an indication of how widely the package has been adopted with the ecosystem.
Deleting a package with less than 50 downloads will have a smaller impact than deleting a package with 5,000 downloads, or 500,000 downloads, or 5 million downloads.
Setting a maximum number of downloads a package can have to be eligible for deletion is a great way to ensure minimal ecosystem impact.
For example, npm's limit is 300 downloads within the previous week.

Download counts are not a perfect way to account for the package's impact on the ecosystem.
They can be arbitrarily inflated or could vary over time.
One ecosystem may count downloads differently than another.
Download counts are best used in conjunction with other criteria in evaluating whether a given package should be eligible for deletion.

### Dependency Status

Is the package under consideration a dependency of other packages within the ecosystem?
How many?
Is _that_ package a dependency of another package (making the package to be deleted a transitive dependency)?

If other packages within the ecosystem depend on the package to be deleted, that is direct proof that deletion would cause ecosystem harm.
A package registry administrator team could choose whatever threshold they like, but many package registries choose to not allow for deletion of dependent packages at all.

### Maintainer Status

Many package deletion policies will not allow packages with more than one maintainer to be deleted.
Allowing a single maintainer to delete the package could contradict the will of the other maintainers and there is not an uncomplicated way to get the consent of the maintainer team.
Multiple maintainers also implies an increased investment in the project.
Additionally a package registry could differentiate between a "maintainer" and an "owner" and only allow for the package owner to delete the package.

## Deletion Granularity

When crafting a deletion policy, it is important to be specific about how granular you want the policy to be.
Will deleting entire packages be allowed? What about individual versions? A version range?
What makes sense for a single version might not make sense for an entire package.
Feel free to differentiate between the two when crafting your policy.

## Package Name and Version Immutability

When a package is deleted from a package registry, does the package name become available?
Unless specifically prohibited, another package could be published with the name of the previously deleted package.
Within a fairly conservative package deletion policy, this is unlikely to be a problem as the deleted package did not have widespread adoption.
However, if a package registry allows for the deletion of widely used, established packages, the open name can become a security issue if a new (potentially malicious) package is published with the same name.
Even if the new package isn't malicious, it has the potential to confuse users.
Therefore, when considering a package deletion policy, it is important to consider what to do with the abandoned names.
Some package registries never reuse a name, which is a best practice security measure.
Alternatively package names could be reused with additional protections in place (for example, file hashing to notify users of changes).

It is also important to decide if version numbers are immutable.
It is a good security practice to have version immutability and when crafting your deletion policy, consider [deletion alternatives](#deletion-alternatives) like yanking or deprecation. 

## Package Registry Structure and Package Deletion Policies

A package deletion policy could be impacted by architectural choices within the given package registry.

### Decentralized Publishing

For example, Go uses [decentralized publishing](https://go.dev/doc/modules/developing#decentralized) to make their modules available. 
A Go module is published by tagging the code in its repository.
When a module is published it is also uploaded to Go's [module proxy server](https://proxy.golang.org/).
The module maintainer never directly adds their module to the proxy server, and there is not a way for the maintainer to delete the module from the proxy server.
They can delete the original repository, but a copy of the project will remain on the proxy server.
Instead, Go uses a [retract directive](https://go.dev/ref/mod#go-mod-file-retract), which is an example of a [package deletion alternative](#deletion-alternatives).

### Test Instances and Staging Environments

Another architecture decision related to a package deletion policy is the use of a separate test instance or a staging environment.

For example PyPI maintains [TestPyPI](https://test.pypi.org/) to allow users to try distribution tools and processes without affecting the real PyPI.
A test instance does not necessarily eliminate the need for a package deletion policy because mistakes can still be made, but it does allow for users to experiment without leaving junk packages on the main instance.

### Other Edge Cases

Some package registries allow for users to be deleted, so a package could theoretically exist without an owner.
Under what conditions would such a package be deleted?

Maybe your package registry would benefit from a list of deleted packages for auditing purposes. 

Take some time to consider your ecosystem's edge cases. Do some testing. Implement things that would be helpful for your users or your administrators.

## Deletion Alternatives

Once we've considered all the decision criteria for whether an author should be allowed to delete their package, it is clear that there are pain points for package authors that are not well addressed by allowing for a package to be deleted. 

What if a package (or version series) is no longer in active development?
What if a specific version is unstable?
In these cases, the community should be informed of the issues, and possibly prevented from using a specific version, but deleting the package outright is not a tenable solution.
These cases require a little more flexibility for users and a comprehensive package deletion policy will provide some more nuanced alternatives to deleting a package. 

### Yanking

Yanking is a way to deprioritize an installer's preference for a given release.
When a package author yanks a version, the version still exists in the package registry but installers will ignore the version unless it is the only release that matches a version specifier.
If a user explicitly requires a yanked version, it will be installed and will not break the build.
Package authors should consider yanking a release if it is broken, unstable, or contains a very severe vulnerability.
Yanking will not completely guarantee that no one is using the yanked version, but it will reduce the installer preference to install it.
If an ecosystem allows for version yanking, it is best practice to also allow maintainers to provide a reason.
Users who are explicitly requiring the yanked version can then appropriately prioritize moving to a non-yanked version.

Some version yanking policies use slightly different terminology but are functionally very similar.
For example, Go uses the term "retract" and the retract directive can indicate that a package version (or version range) should not be used.

Regardless of the term used, the following sets these policies apart from a deletion policy in the following ways:

1. The yanked version is still available.
2. The installer will try to avoid using yanked versions.
3. The package consumer can make an informed decision about whether to use the yanked version.
4. Yanking a version will not break a build.

### Deprecation

Software projects are not supported forever.
When the maintainer/maintainer team is no longer willing to support a specific version series or an entire project, the team can mark the project as deprecated.
Generally, deprecated projects are available for installation and can be continued to be used.
Marking a project as deprecated allows users to make an informed decision about the use of the package.
Going forward, the user knows that not only can they not expect any new features, but they can't even expect continued compatibility with other projects or security updates.

Similar to version yanking policies, deprecation policies could use slightly different languages including terms like 'end of life' or mention moving to the next major version.
Regardless of the terms used, with a deprecation policy:

1. The deprecated version/package is still available for installation.
2. The user is informed of the deprecation and can make an informed decision about continuing to use the package or version.
3. The build will not break.

## A Comprehensive Policy

A package deletion policy should take into account the needs of open source maintainers, open source consumers, the package registry administration team, and the ecosystem at large.
There isn't one correct way to balance these interests, but we suggest that your team consider the following when constructing a policy:

1. Craft your package deletion policy to limit the ecosystem impact to a team-defined acceptable level for author initiated package deletions. The package registry administration team should remove copyrighted, illegal, or abusive content regardless of how widely the package is adopted.  
2. Take into account things like version yanking and deprecation policies, package name reuse, and package registry architecture from the beginning. These issues are intrinsically linked to package deletion policies.
3. Be as granular as you need to balance the competing interests of maintainers, consumers, the package registry, and the ecosystem. Explain when users can delete packages, when package registry administrators will step in because of copywritten or illegal material, and when users can petition for package deletion. Be precise about any deletion alternatives you offer.
4. Keep your community in the loop. Research pain points for your users, thoroughly document your policy, keep the community up to date on when to expect changes, and promote your policy once it is implemented.

## Sources

Go

* [Decentralized publishing](https://go.dev/doc/modules/developing#decentralized)
* [Retract directive](https://go.dev/ref/mod#go-mod-file-retract)

Java

* [Can I change, modify, delete, remove, or update a component on Central?](https://central.sonatype.org/faq/can-i-change-a-component/)

Node

* [Unpublishing Packages from the Registry](https://docs.npmjs.com/unpublishing-packages-from-the-registry)
* [npm Unpublish Policy](https://docs.npmjs.com/policies/unpublish)

NuGet

* [Deleting Packages](https://learn.microsoft.com/en-us/nuget/nuget-org/policies/deleting-packages)

Python

* [Yanking](https://docs.pypi.org/project-management/yanking/)
* [What's an archived project?](https://pypi.org/help/#archived-project)
* [How can I restore a deleted project, release, or file](https://pypi.org/help/#deletion)
* [Why am I getting a "Filename or contents already exists" or "Filename has been previously used" error?](https://pypi.org/help/#file-name-reuse)

Ruby

* [Removing a Published Gem](https://guides.rubygems.org/removing-a-published-gem/)
* [Policy change about gem yank](https://blog.rubygems.org/2015/04/13/permadelete-on-yank.html)

Rust

* [cargo yank](https://doc.rust-lang.org/cargo/reference/publishing.html#cargo-yank)
* [Policies](https://crates.io/policies)
