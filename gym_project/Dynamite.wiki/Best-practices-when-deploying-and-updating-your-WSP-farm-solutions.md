Some WSP deployment gotchas:

* Always strong-name your assemblies, since that's a requirement for all full-trust code being run within SharePoint 
* Always open a new PowerShell window after a deployment which updates DLLs in the GAC
    * Restart OWSTimer.exe so that timer jobs can see the new DLLs as well
    * In complex BCS scenarios, restarting the search service can also be required
* When in Visual Studio, to ensure correct packaging of your WSP solutions, you should always **retract everything from the GAC - i.e. retract all you WSPs responsible for provisioning DLLs.** This ensure that Visual Studio builds your projects with your project-folder-local dependencies instead of unexpectedly loading wrong-version DLLs from the GAC to use as build dependencies.

> The risk associated with local packaging of SharePoint solution makes the use of a CI server to build your deployment artifacts **a must**, so strive to power through the challenges ahead of you to reach this state of bliss where you can say:
>
> "I will never again build for prod on my developer machine"
>
> Surely, something to be proud of. :)