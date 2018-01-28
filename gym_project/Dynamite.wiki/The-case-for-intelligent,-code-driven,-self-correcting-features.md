## Be idempotent

In all SharePoint provisioning activities, you should strive for **idempotence**:

> [Wikipedia](https://en.wikipedia.org/wiki/Idempotence): **Idempotence** (/ˌaɪdᵻmˈpoʊtəns/ eye-dəm-poh-təns)[1] is the property of certain operations in mathematics and computer science, that can be applied multiple times without changing the result beyond the initial application.

In other words, applying the same operation a second (and third) time should be a no-op.

## Be incremental

All applications evolve over their lifetimes. As such, your SharePoint application should enable easy iteration - even after you hit production.

Too often, SharePoint application development follows this pattern:

1. Sweat hard to build your minimal viable solution
2. Sweat hard to package the app once to go from dev to testing/qa environments
3. Deploy in prod
4. Pray your client never asks for any changes

This is insane. Developers should automate their provisioning and installation procedure to such a level that they are **confident in deploying repeatedly in and incrememental fashion, without fear of unintended consequences**.

## A blueprint for full automation

Use PowerShell to script your installation.

Make sure your **SINGLE AUTOMATED INSTALL SEQUENCE** supports the following scenarios:
* On a developer machine: 
    * First setup 
    * Run again without side effects
    * Change code, then run again to deploy & provision changes incrementally
    * Delete and restart-from-scratch setup on developer machine
* In any non-dev environment (qa, stage, prod, etc.)
    * First setup from-scratch
    * Run again without side effects (so you can use your fat fingers in PROD without worry)
    * Apply upgrades by running the same setup sequence with a new package (ideally auto-versioned and packaged from a CI build)
    * Safeties so that you NEVER delete everything when in PROD :)

A typical setup sequence could look like:

1. Retract, remove and re-deploy the newest WSP solution packages
2. Start a new PowerShell shell to make sure we load the newest DLLs from GAC
3. Do a bit of fiddling in PowerShell to configure SharePoint service applications (e.g. term store imports)
4. Create your sites (if they don't exist yet)
    * allow a `-Force` parameter **with a confirmation prompt** that defaults to "No" to allow deletion of your site collection(s) to start from-scratch
5. Run a sequence of SharePoint feature deactivations + reactivations.
    * This way **most of our provisioning logic resides in, strongly-type, potentially well-unit-and-integration-tested C# code called from Feature event receivers**
6. Do a bit of extra fiddling in PowerShell to finish farm configuration (e.g. search crawls)

The key points here are:
* we can re-run this same automated setup sequence an infinite number of times without side effects
* the exact same sequence is used in dev and in prod
* feature activation C# code is the main source of provisioning 

> **Feature Design Tips**: 
>    * Keep your features small and with a single responsibility.
>    * You can omit `FeatureDeactivated` code, unless it definitely makes sense (e.g. put the original master page URL in the site config). All your feature needs is a `FeatureActivated` event receiver that knows how to provision its SharePoint artefacts in an idempotent way. 
>        * Bonus: Nothing is more annoying than a feature that breaks when you try to de-activate it. You gain confidence in your provisioning sequence because you know you can always attempt to re-activate a feature successfully
>    * Avoid `FeatureUpgraded` complexity in favor of smarter `FeatureActivated` code

## Wait a minute, what about all my `Element.xml` modules?

SharePoint module XML defintions are notoriously finnicky when it comes to upgrade scenarios. Eventually, you can bet that you're going to need an extra bit of C# or PowerShell code to patch up a SharePoint artifact that will not let itself be upgraded through `Element.xml`. 

Your best guess is to provision most of the following SharePoint elements in C# `FeatureActivated` code, giving you maximum flexibility to handle upgrade and migration scenarios to your liking:
* Site columns
* Content types
* Lists and libraries

Depending on your context, you can use a combination of *Element.xml* modules (mostly `<File>` elements) and a sprinkle of C# feature activation to provision the following:
* Page layouts
* Page instances
    * Some code-driven provisioning can be esp. helpful when trying to ensure the web part contents of web part pages
* Branding files (master pages, css to style library, etc.)

## The Dynamite provisioning helpers, idempotent by design

Take [Dynamite's provisioning helpers for a spin](https://github.com/GSoft-SharePoint/Dynamite#c-using-dynamites-provisioning-utilities) to see how robust idempotent provisioning can make your SharePoint server developer life less stressful.

## Beware of customizations

Robust deployments take on a whole new meaning when you consider that SharePoint sites have the potential to be modified by their users through "click-programming" if they have sufficient site management permissions. 

This can lead to great headaches when you attempt to upgrade a SharePoint solution package, since the actual live site has "drifted" from the initial site definition through the accumulation of user customization.

Some basic guidelines for your users and dev teams with regards to this challenge:

* In a collaboration (e.g. team or project sites) context, you should encourage advanced user training so that power users begin customizing their SharePoint space to their liking, thereby maximizing the value of SharePoint's customizability.
    * As a developer, depending on feature re-activation sequences driven by PowerShell makes team site upgrades easier to propagate than traditional SharePoint site-definition-driven approaches
* In a publishing context (e.g. intranet portals or public web sites), you should strive to **lock down** users' abilities to customize their SharePoint site (through reduced permissions).
    * As a developer, you want to minimize the amount of *reverse engineering of user customizations* that becomes necessary with every upgrade if you want to keep your monolithic provisioning sequence up-to-date
    * Such large-audience-facing sites benefit from the added stability of driving all SharePoint customization actions through coded provisioning sequences instead of through the improvisation of its power users

> A takeaway: You should always attempt to train your users in learning the subtleties and possibilities of SharePoint. Their enhanced awareness of SharePoint concepts and constraints will make them better partners in the evolution of your SharePoint solutions.