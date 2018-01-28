Avoid the pitfalls of full-trust (GAC-based) development scenarios by understanding [the basics of GAC deployments and DLL hell](https://msdn.microsoft.com/en-us/library/ms973843.aspx)


Best practices for assembly versioning and dependency management:

* You should avoid changing the `AssemblyVersion` of your SharePoint projects (WSP solutions). Use the `AssemblyFileVersion` to track updated version numbers (ideally using [SemVer](http://semver.org/)) whenever you plan to release an upgrade.
* This is ideal since, no matter what happens, having two different versions of the same WSP solution package to the same farm is impossible. If you keep your `AssemblyVersion` stable, it make your life easier refering to the assembly strong names (e.g. in ASP control template imports).
* Applying the correct `AssemblyFileVersion` should be the responsiblity of your continuous integration build server, to avoid manual versioning errors as much as possible
 Don't trust the "Specific Version" parameter when you add a project reference:
    * Its only meaning is: "use this specific AssemblyVersion of my dependency when *building* my own projet"
    * At *runtime* (i.e. once deployed to GAC), your own assemblies will *always* require the same AssemblyVersion'd dependencies (i.e. those used at *build time* with the same assembly strong name) be present in the GAC as 
    * So you should always use "SpecificVersion=TRUE" to ensure you don't compile using a rogue-version assembly (otherwise, once you deploy, at runtime you may have "Missing assembly" problems
