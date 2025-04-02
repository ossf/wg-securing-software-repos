# Package yanking policy tradeoffs

Last updated: March 2025

In 2016 after a dispute about the naming of an open source package, a maintainer deleted all the packages he had published to npm, including a small package called `left-pad`. Although `left-pad` was only about a dozen lines of code, it had impressive reach. Prior to removal, it had over 15 million downloads and was used by thousands of open source projects--including many that are critical to the npm ecosystem. The deletion of `left-pad` caused build failures for projects large and small and rendered a large portion of the internet unnavigable. Npm made the decision to republish the package.  

After the `left-pad` incident, npm updated their package deletion policy to prevent similar failures and other package managers followed suit. In the over 9 years since the incident, package managers have continued to adjust their package deletion policies to balance the sometimes competing interests of open source maintainers, open source consumers, and the package ecosystem itself. 

This paper discusses the components of modern package deletion policies, highlighting the strengths and weaknesses of specific policy components. It is not meant to be a sample deletion policy, but a discussion of things to consider when crafting such a policy. 

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

If other packages within the ecosystem depend on the package to be deleted, that is direct proof that deletion would cause ecosystem harm. A package manager maintainance team could choose whatever threshold they like, but none of the package managers surveyed for this report allowed for packages to be deleted if they are dependencies of other packages in the ecosystem. 

### Maintainer status

Many package deletion policies will not allow packages with more than one maintainer to be deleted. Allowing a single maintainer to delete the package could contradict the will of the other maintainers and there is not an uncomplicated way to get the consent of the maintainer team. Multiple maintainers also implies an increased investment in the project. 

## Package manager structure and package deletion policies

Package managers are not all structured the same way and architecture decisions can have an impact on what makes sense for a given ecosystem.

### Decentralized publishing

For example, Go uses [decentralized publishing](https://go.dev/doc/modules/developing#decentralized) to make their modules available. A Go module is published by tagging the code in its repository. Publishing a moduleit is also uploaded to Go's [module proxy server](https://proxy.golang.org/). The module will be available on the module proxy server even if it is The module maintainer never directly adds their module to the proxy server, so a method to delete it from the proxy server doesn't make a lot of sense. 
### Test ecosystems

## Deletion alternatives
### Yanking
### Deprecation

## Additional considerations
### Namespaces


## Conclusion

## Bibliography


 

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
