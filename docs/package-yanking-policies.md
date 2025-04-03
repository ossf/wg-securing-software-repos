# Crafting a package deletion policy

Last updated: April 2025

In 2016 after a dispute about the naming of an open source package, a maintainer deleted all the packages he had published to npm, including a small package called `left-pad`. Although `left-pad` was only about a dozen lines of code, it had impressive reach. Prior to removal, it had over 15 million downloads and was used by thousands of open source projects--including many that are critical to the npm ecosystem. The deletion of `left-pad` caused build failures for projects large and small and rendered a large portion of the internet unnavigable. Npm made the decision to republish the package.  

After the `left-pad` incident, npm updated their package deletion policy to prevent similar failures and other package managers followed suit. In the over 9 years since the incident, package managers have continued to adjust their package deletion policies to balance the sometimes competing interests of open source maintainers, open source consumers, and the package ecosystem itself. 

This paper discusses the components of modern package deletion policies. It is not meant to be a sample deletion policy, but a discussion of things to consider when crafting such a policy. 

## Deletion policy considerations

If we consider a hypothetical package deletion policy, it would exist on a spectrum somewhere between never allowing packages to be deleted to allowing packages to be deleted without any restrictions. Both ends of this spectrum are impractical. 

* Never allowing for package deletion could result in the publishing of malicious, abusive, illegal, or copywritten content without any recourse.
* Allowing for unrestricted package deletion could result in build failures like those seen in the `left-pad` incident, malicious packages snapping up a recently vacated namespace, and other undesireable behavior. 

So when crafting a deletion policy, we want to stay away from the two extremes, but what needs to be considered?

Whether or not a package manager allows for users to delete packages in some cases, it should allow for the package manager maintainers to manually intervene and delete packages. This allows the maintainer team to protect the ecosystem from malicious, abusive, illegal, or copywritten content. 

But what if a user wants to delete a package they published? Although it's possible to require such cases to go to the maintainer team to be manually reviewed and removed, that is not a very efficient policy. Such a policy would place a burden on the (already likely overworked) maintainer team, and the ecosystem would be cluttered with the unwanted packages until they are manually removed. 

Allowing a user to delete their package in certain cases is therefore good for the user, the package manager maintainer team, and the package ecosystem at large. But what factors need to be considered to avoid a `left-pad` style incident? 

## Ecosystem impact

A modern package deletion policy aims to minimize the impact a given deletion could have on the ecosystem, while granting users some flexibilty with their packages. 

The following considerations are generally used when determining whether a package is a good candidate for deletion, although specific limits and criteria will vary between package managers. 

### Time

How long ago was the package published? Although time since publication is not a perfect metric for ecosystem impact (maybe a package has been around for years but only has a handful of users), there are a number of use cases where this metric is very relevant. For example, the user could have:

* Published the wrong package
* Published the package with an unintended name (or a typo)
* Published a test package to understand and experience the package publishing process

In these cases, it is very useful for the package manager to have a no hassle deletion policy as long as the package has been published for less than a certain amount of time. 

### Downloads

How many times has the package been downloaded? Package download statistics provide an indication of how widely the package has been adopted with the ecosystem. Deleting a package with less than 50 downloads will have a smaller impact than deleting a package with 5,000 downloads, or 500,000 downloads, or 5 million downloads. Setting a maximum number of downloads a package can have to be eligible for deletion is a great way to ensure minimal ecosystem impact. 

### Dependency status

Is the package under consideration a dependency of other packages within the ecosystem? How many? Is _that_ package a dependency of another package (making the package to be deleted a transitive dependency)? 

If other packages within the ecosystem depend on the package to be deleted, that is direct proof that deletion would cause ecosystem harm. A package manager maintainance team could choose whatever threshold they like, but many package managers choose to not allow for deletion of dependent packages at all. 

### Maintainer status

Many package deletion policies will not allow packages with more than one maintainer to be deleted. Allowing a single maintainer to delete the package could contradict the will of the other maintainers and there is not an uncomplicated way to get the consent of the maintainer team. Multiple maintainers also implies an increased investment in the project. Additionally a package manager could differentiate between a "maintainer" and an "owner" and only allow for the package owner to delete the package. 

## What to do about namespaces

When a given package meets all the criteria discussed above and the package maintainer deletes the package, what happens next?

When a package is deleted from a package manager, it frees the namespace that the package was occupying. Unless specifically prohibited, another package could be published with the name of the previously deleted package. Within a fairly conservative package deletion policy, this is unlikely to be a problem as the deleted package did not have widespread adoption. However, if a package manager allows for the deletion of widely used, established packages, the open namespace can become a security issue if a new (potentially malicious) package is published with the same namespace. Even if the new package isn't malicious, it has the potential to be confusing to users. Therefore, when considering a package deletion policy, it is reasonable to consider what to do with the vacated namespaces.  

## Package manager structure and package deletion policies

Additionally, a package deletion policy could be impacted by architectural choices within the given package manager. 

### Decentralized publishing

For example, Go uses [decentralized publishing](https://go.dev/doc/modules/developing#decentralized) to make their modules available. A Go module is published by tagging the code in its repository. When a module is published it is also uploaded to Go's [module proxy server](https://proxy.golang.org/). The module maintainer never directly adds their module to the proxy server, and there is not a way for the maintainer to delete the module from the proxy server. They can delete the original repository, but a copy of the project will remain on the proxy server. Instead, Go uses a [retract directive](https://go.dev/ref/mod#go-mod-file-retract), which is an example of a [package deletion alternative](#deletion-alternatives).  

### Test instances

Another architecture decision related to a package deletion policy is the use of a seperate test instance. For example PyPI maintains [TestPyPI](https://test.pypi.org/) to allows users to try distribution tools and processes without affecting the real PyPI. A test instance does not necessarily eliminate the need for a package deletion policy because mistakes can still be made, but it does allow for users to experiment without leaving junk packages on the main instance. 

## Deletion alternatives

There are a number of reasons that a person would want to delete a package. Package deletion is a good solution for some of those reasons (publishing the wrong package, making a typo, experimenting with the package manager), but not necessarily for others. 

What if a package (or version series) is no longer in active development? What if a specific version has a security issue? In these cases community should be informed of the issues, and possibly prevented from using a specific version, but deleting the package outright is not a tenable solution. So what can package managers do in these cases?

### Yanking

"Yanking" refers to soft deleting a compromised package version. The version still exists, but by marking the version as yanked, installers will ignore the version unless it is the only release that matches a version specifier. If the yanked version is explicitly required, it will be installed and will not break the build. Mainters should consider yanking a release if it is broken or unstable, or if contains a security vulnerability. Yanking will not completely guarantee that no one is using the compromised version, but it will reduce the prevalence of the corrupted version. If an ecosytem allows for version yanking, it is best practice to also allow maintainers to provide a reason. Users who are explicitly requiring the yanked version can then appropriately prioritize moving to a non-yanked version.

Some version yanking policies use slightly different terminology but are functionally very similar. For example, Go uses the term "retract" and the retract directive can indicate that a package version (or version range) should not be used. 

Regardless of the term used, the following sets these policies apart from a deletion policy in the following ways:

1. The yanked version is still available.
2. The installer will try to avoid using yanked versions.
3. The package consumer can make an informed decision about whether to use the yanked version.
4. Yanking a version will not break a build.

### Deprecation

Software projects are not supported forever. When the maintainer/maintainer team is no longer willing to support a specific version series or an entire project, the team can mark the project as deprecated. Generally, deprecated projects are available for installation and can be continued to be used. Marking a project as deprecated allows users to make an informed decision about the use of the package. Going forward, the user knows that not only can the not expect any new features, but they can't even expect continued compatibility with other projects or security updates. 

Similar to version yanking policies, deprecation policies could use slightly different languages including terms like 'end of life' or mention moving to the next major version. Regardless of the terms used, with a deprecation policy:

1. The deprecated version/package is still available for installation.
2. The user is informed of the deprecation and can make an informed decision about continuing to use the package or version.  
3. The build will not break. 

## A comprehensive policy

A package deletion policy should take into account the needs of open source maintainers, open source consumers, the package manager maintainer team, and the ecosystem at large. There isn't one correct way to balance these interests, but we suggest that your team consider the following when constructing a policy:

1. Craft your package deletion policy to limit the ecosystem impact to a team-defined acceptable level. 
2. Considerations like the newly open namespaces, version yanking and deprecation policies, and package manager architecture should be a part of the conversation from the beginning, as they are intrinsically linked to package deletion.
3. Including options like version yanking and project deprecation can help you balance the competing interests of maintainers, consumers, the package manager, and the ecosystem. 
4. Keep your community in the loop. Research pain points for your users, thoroughly document your policy, keep the community up to date on when to expect changes, and promote your policy once it is implemented.  

## Bibliography

(Under construction while draft is reviewed)


 

NOTES: To be deleted when published. 

* Opening
    * Left pad incident
    * Package managers need to protect the integrity of their registries. Package managers provide a valuable service of delivering open source packages and unchecked package deletion would render package managers unable to perform the service for which they were designed. 

* Types of Package deletion policies
    * Allow for no deletion
        * You won't break any builds
        * Registry is cluttered with unnecessary packages
        * Namespaces could be taken up with packages that no one (even the person who published it) is using
    * Allowing users to delete packages under certain conditions
        * Example (npm, Rust)
            * The package manager determines specific conditions under which they will allow package deletion
                * How long ago was the package created?
                * How many downloads has the package received?
                * Do any other packages in the registry depend on the package in question? (Left pad incident)
                * How many maintainers are involved?
                * Etc
        * Pros
            * People may be experimenting with how to create a package on the registry, but they don't actually want to publish a package (or at least, not yet). Not allowing for deletion can discourage new people from engaging. 
            * People make mistakes, they may have a typo in the package name, maybe they published the wrong package, etc
            * Automated--package manager maintainers do not have to manually intervene
            * Limits potential scope of problem. May break _some_ builds, but nothing on the scale of the left pad incident
        * Cons
            * How are these limits determined? Setting them too loose increases the risk of issues, keeping things too tight increases the amount that maintainers will need to intervene. If the settings are too tight the registry is a little cluttered and includes packages that people aren't actually using, etc. 
    * Allow for version yanking
    * Deprecation
    * Mirrors

Crates https://crates.io/policies 
Gems https://guides.rubygems.org/removing-a-published-gem/
PyPI https://peps.python.org/pep-0763/#appendix-a-precedent-in-other-ecosystems 
Go 
Maven
npm https://docs.npmjs.com/policies/unpublish https://docs.npmjs.com/unpublishing-packages-from-the-registry https://blog.npmjs.org/post/190553543620/changes-to-npmunpublish-policy-january-2020

NuGet
