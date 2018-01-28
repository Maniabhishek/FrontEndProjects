Welcome to the Dynamite wiki!

Make sure you start with reading the **[Dynamite project README](https://github.com/GSoft-SharePoint/Dynamite)** and its **[Quick Start Guide](https://github.com/GSoft-SharePoint/Dynamite#quick-start-guide)**.

In this wiki you will find:

* Intro to Dynamite: [Building maintanable and modular SharePoint farm solutions with Dynamite](#building-maintanable-and-modular-sharepoint-farm-solutions-with-dynamite)
    * Preamble: [Why Dynamite? Why farm solutions?](#why-dynamite-why-farm-solutions)
    * [1. A modular approach to building SharePoint farm solutions with Dynamite and Autofac](#1-a-modular-approach-to-building-sharepoint-farm-solutions-with-dynamite-and-autofac)
    * [2. Automate your deployments and upgrades end-to-end with the Dynamite PowerShell Toolkit](#2-automate-your-deployments-and-upgrades-end-to-end-with-the-dynamite-powershell-toolkit)
    * [3. Making the best of Dynamite: discover its powerful and time-saving utilities](#3-making-the-best-of-dynamite-discover-its-powerful-and-time-saving-utilities)
* Extra: [Git beginner's guide](#git-beginners-guide)

## Building maintanable and modular SharePoint farm solutions with Dynamite

### Why Dynamite? Why farm solutions?
SharePoint 2013 introduces the new App-model for SharePoint custom solution development. Microsoft's guidelines are clear: [in 2013, whenever possible, build things the App-way](http://msdn.microsoft.com/en-us/library/office/jj163114(v=office.15).aspx). While Apps have the benefit of de-coupling your custom functionality from your mission-critical on-premise SharePoint infrastructure, the SharePoint client-side APIs do come with some limitations.

Full-trust SharePoint solution development is still the most powerful option for customizing your SharePoint 2013 farm. If you are still developing in a SharePoint 2010 context, farm solutions are your only option (if we ignore the unpopular and [soon-to-be-deprecated](http://blogs.msdn.com/b/sharepointdev/archive/2014/01/14/deprecation-of-custom-code-in-sandboxed-solutions.aspx) sandbox solution model).

[The Dynamite project](https://github.com/GSoft-SharePoint/Dynamite) for SharePoint 2013 (built by [GSoft](http://gsoft.com)'s SharePoint development experts - Team Dynamite) is a C# toolkit of reusable components that guide you into the "right" path for full-trust solution development. A version of [Dynamite for SharePoint 2010](https://github.com/GSoft-SharePoint/Dynamite-2010) is also available, for all of you who are still supporting legacy environments.

Some essential values put forward by Dynamite are the following:

* A truly modular architecture through Dependency Injection
    * to promote code reuse across projects
    * to make your components easy to test
    * to provide extension points for alternative usages of your features (i.e. configurability)
    * to avoid massive multi-project deployments when possible (i.e. modular rather than monolithic deployments)
* Entirely automated deployments through templated PowerShell scripts
    * to avoid error-prone manual operations at all costs
    * to provide a reproducible installation process in any SharePoint farm environment
* Intelligent, code-driven, self-correcting features
    * to reduce risk when upgrading your SharePoint solutions
    * to eliminate your dependency on SharePoint's often hard-to-upgrade XML-based definitions
    * to easily maintain your solutions in the long term within the enterprise

Many of these ideas take their origin in [Microsoft's patterns and practices team's famous SharePoint 2010 development guide](http://msdn.microsoft.com/en-us/library/ff770300.aspx). The Dynamite toolkit and the guide that follows are the end results of applying many of these ideas in the wild in real-life enterprise scenarios since 2010.

### 1. A modular approach to building SharePoint farm solutions with Dynamite and Autofac

* [What is Dependency Injection?](https://github.com/GSoft-SharePoint/Dynamite/wiki/What-is-Dependency-Injection%3F)
    * A quick primer on why Inversion of Control containers and Dependency Injection are "good things"
    * A case for using Constructor Injection for all your classes' dependencies
* Building your first Module and Service Locator
    * [How to break up your solution in many Visual Studio projects with their own responsibilities](https://github.com/GSoft-SharePoint/Dynamite/wiki/How-to-break-up-your-solution-in-many-Visual-Studio-projects-with-their-own-responsibilities)
    * [Installing the Dynamite NuGet packages from our MyGet.org feeds](https://github.com/GSoft-SharePoint/Dynamite/wiki/Installing-the-Dynamite-NuGet-packages-from-our-MyGet.org-feeds) (and tips on how to handle package upgrades smoothly)
    * [How to set up your first application-wide Autofac service locator](https://github.com/GSoft-SharePoint/Dynamite/wiki/How-to-set-up-your-first-application-wide-Autofac-service-locator)
    * [How to provide your own reusable services through an Autofac registration module](https://github.com/GSoft-SharePoint/Dynamite/wiki/How-to-provide-your-own-reusable-services-through-an-Autofac-registration-module)
    * [Do's and Don'ts of Service Locator usage](https://github.com/GSoft-SharePoint/Dynamite/wiki/Do's-and-Don'ts-of-Service-Locator-usage)
    * [Controlling the lifetime of your objects through Dynamite's custom lifetime scopes](https://github.com/GSoft-SharePoint/Dynamite/wiki/Controlling-the-lifetime-of-your-objects-through-Dynamite's-custom-lifetime-scopes)
* [Managing assembly versions and assembly dependencies](https://github.com/GSoft-SharePoint/Dynamite/wiki/Managing-assembly-versions-and-assembly-dependencies)
   
### 2. Automate your deployments and upgrades end-to-end with the Dynamite PowerShell Toolkit

* [On the evils of Visual Studio-based deployments](https://github.com/GSoft-SharePoint/Dynamite/wiki/On-the-evils-of-Visual-Studio-based-deployments)
* [Installing Dynamite's very own PowerShell module](https://github.com/GSoft-SharePoint/Dynamite/wiki/Installing-Dynamite's-very-own-PowerShell-module)
* [Templating your PowerShell scripts](https://github.com/GSoft-SharePoint/Dynamite/wiki/Templating-your-PowerShell-scripts) thanks to the ```Update-DSPTokens``` command
* [Best practices when deploying and updating your WSP farm solutions](https://github.com/GSoft-SharePoint/Dynamite/wiki/Best-practices-when-deploying-and-updating-your-WSP-farm-solutions)

### 3. Making the best of Dynamite: discover its powerful and time-saving utilities

* Easy logging to the ULS (SharePoint's Unified Logging System) thanks to [Dynamite's `ILogger`](https://github.com/GSoft-SharePoint/Dynamite#d-other-utilities-logging-and-globalization)
* Error-free resource management through the [`IResourceLocator` interface](https://github.com/GSoft-SharePoint/Dynamite#d-other-utilities-logging-and-globalization)
* [The case for intelligent, code-driven, self-correcting features](https://github.com/GSoft-SharePoint/Dynamite/wiki/The-case-for-intelligent,-code-driven,-self-correcting-features)
    * E.g. provision your content types and lists programmatically instead of through XML for maximum 
flexibility during upgrades
    * SharePoint's great upgrade conundrum: what to do with "click-programming" customizations that took place since your last deployment?
* Promote the isolation and testability of business logic through [easily serializable Entities and Dynamite's entity mapping utilities](https://github.com/GSoft-SharePoint/Dynamite#e-the-sharepoint-entity-binder-easy-mappings-from-entities-to-splistitems-and-back).


## Git beginner's guide

All of Team Dynamite's projects are hosted on Github. We recommend using Atlassian's SourceTree git client for source control management. This guide should help you get started on the path to contributing to the Dynamite project.

* Overview: [Getting started with SourceTree, Git and git-flow](https://github.com/GSoft-SharePoint/Dynamite/wiki/Getting-started-with-SourceTree,-Git-and-git-flow)
* Git step-by-step:
    * Part 1: [Cloning a new repo from github.com with SourceTree, initializing gitflow](https://github.com/GSoft-SharePoint/Dynamite/wiki/Git-step-by-step:-Part-1)
    * Part 2: [Basic local operations - Staging, commiting, branching and merging](https://github.com/GSoft-SharePoint/Dynamite/wiki/Git-step-by-step:-Part-2)
    * Part 3: [Basic remote operations - Fetching, pulling and pushing](https://github.com/GSoft-SharePoint/Dynamite/wiki/Git-step-by-step:-Part-3)
* More Git topics: 
    * [Using gitflow for feature branches, releases and hotfixes](http://danielkummer.github.io/git-flow-cheatsheet/)
    * [The stash is your best friend](https://git-scm.com/book/en/v1/Git-Tools-Stashing)