# arcsight-asset-context-information
Get external asset context information via Integration Command in ArcSight ESM

ArcSight ESM (aka Detect in future releases) has an Integration Command capability that can tak an action on a object, usualy an event field or the whole event. The action is to run a script or call a URL. This extention uses the URL call where you can set the host and other variebles according to your environment.

## Instalation
Import the Asset_information_???.arb file into Packages within the ArcSight ESM Console. The Asset Information package should be visible in /All Packages/ArcSight Foundation, but it will be grayed out.
Install the package with context menu
![Install the package](/images/Install_package.png)

There should be 3 installed Integration Command resources:
![Package installed](/images/Package_installed.png)


## Customisation
All resources are in `Integration Commands/Targets/Configuration/` within `ArcSight Foundation/Asset` info folder

### Commands
Includes the actual parametrized URL to your CMS (Configuration Management System). **No need to customize** unless a new version might requite URL tweak. The default URL is:`https://${host}/ucmdb-browser/ucmdb_browser.jsp?server=${tenantServer}&locale=en&customerID=${custId}#tab=search;search=$selectedItem`

### Targets
There is one `CMS1` target predefined with 3 parameters you **should customize** based on your CMS setup:

![Target host system parameters](/images/Target_customisation.png)

* host - your CMS hostname or IP address
* tenantServer - your CMS tenant name
* custID - your CMS customer ID

Once you save these the Integration Command will use these parameters automatically.

You can also preserve the preset `CMS1` target and create your own targets i.e. `CMS-prod` and `CMS-dev`. Note these extra targets will not be used unless your customize the 3rd `Configurations` resource!

### Configurations
The `Configurations` ties the previous `Commands` and `Targets` together, plus it defines where the Integration Command is available. You **may or may not need to customize** this one.

The most probable customisation would be changing the preset `Targets`. When there is just one `Target` defined the Integration Command uses automatically that Target's parameters and launches the URL directly.

![One Target host config](/images/One_target_config.png)

When you add more than one `Target`, i.e. `CMS-prod` and `CMS-dev`:

![Two Target hosts config](/images/Two_targets_config.png)

Then the Integration Command will ask you every time you launch it on what Target system you would like to perform the action:

![Ask for Target before launch](/images/Ask_target_before_launch.png)

## Usage of Integration Command
Any time you need to check the Asset information in external system, use the context menu on the object like a `sourceAddress` and select `Integration Command/CMS lookup`. Note you may need to login first into the external system if you are not authenticated automatically, if that happens, just louch the command again after succesful login and it show case the needed asset information.

### Console (JAVA client)
![Console usage](/images/Integration_Command_usage.png)

### ArcSight Command Center (web client)
![Web usage](/images/Integration_Command_usage_web.png)

### Asset lookup result
![Asset Lookup](/images/CMS_lookup_result.png)



