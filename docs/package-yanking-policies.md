# Package yanking policy tradeoffs

Last updated: March 2025

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
