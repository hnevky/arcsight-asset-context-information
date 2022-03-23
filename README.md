# arcsight-asset-context-information
Show external asset context information via Integration Command in ArcSight ESM within external CMS (aka Micro Focus Configuration Management System/CMDB/uCMDb/UD).

ArcSight ESM (aka Detect in future releases) has an Integration Command capability that can take an action on an object, usualy an event field or the whole event. The action can be a script or a URL call. This extention uses the URL call where you can set the host and other variebles according to your environment.

---
## Version log
0.1 - initial MVP for SaaS version of CMS  
0.2 - added On-Prem command next to SaaS command lookup

---
## Usage of Integration Command
Any time you need to check the Asset information in external system, use the context menu on the object like a `sourceAddress` and select `Integration Command/CMS lookup`. Note you may need to login first into the external system if you are not authenticated automatically, if that happens, just louch the command again after succesful login and it show case the needed asset information.

### ArcSight ESM Console (JAVA client)
![Console usage](/images/Integration_Command_usage.png)

### ArcSight Command Center (web client)
![Web usage](/images/Integration_Command_usage_web.png)

### Asset lookup result (on prem CMS) - single IP address found in the CMS
![Asset Lookup](/images/CMS_lookup_result.png)

### Asset lookup result (SaaS CMS) - four IP addresses found in the CMS
![Asset Lookup](/images/assets-4-found.png)

### Asset lookup result - drill down to particular host SW
![Asset Lookup](/images/asset-sw.png)

### Asset lookup result - drill down to particular host HW
![Asset Lookup](/images/asset-hw.png)

---
## Installation
Import the Asset_information_???.arb file into Packages within the ArcSight ESM Console. The Asset Information package should be visible in /All Packages/ArcSight Foundation, but it will be grayed out.
Install the package with context menu:

![Install the package](/images/Install_package.png)

There should be 3 installed Integration Command resources, each containing 2 preset configs for SaaS and On-Prem version:

![Package installed](/images/Asset-info-package.png)

---
## Customisation
All resources are in `Integration Commands/Targets/Configuration/` within `ArcSight Foundation/Asset` info folder

### Commands
Includes the actual parametrized URL to your CMS (Configuration Management System). There are two preset commands `CMS on-prem lookup` and `CMS Saas lookup` as they differ in URL and parameters.

You can disable one of them if not needed with context menu option:

![Disable command](/images/disable-command.png)


### Targets
There are two separate `CMSonprem` and `CMSsaas` targets predefined with parameters you **should customize** based on your CMS setup:

#### SaaS target
![Target host system parameters](/images/Target_customisation.png)

* host - your CMS hostname or IP address
* tenantServer - your CMS tenant name
* custID - your CMS customer ID

#### On-prem target
![Target host system parameters](/images/CMS-onprem-target.png)

* host - your CMS hostname or IP address
* port - your CMS port number used

Once you save these the Integration Command will use these parameters automatically.

You can also preserve the preset targets and create your own extra targets i.e. `CMS-prod` and `CMS-dev`. Note these extra targets will not be used unless your customize the 3rd `Configurations` resource!

### Configurations
The `Configurations` ties the previous `Commands` and `Targets` together, plus it defines where the Integration Command is available. You **may or may not need to customize** this one.

The most probable customisation would be changing the preset `Targets`. When there is just one `Target` defined the Integration Command uses automatically that Target's parameters and launches the URL directly.

![One Target host config](/images/One_target_config.png)

When you add more than one `Target`, i.e. `CMS-prod` and `CMS-dev`:

![Two Target hosts config](/images/Two_targets_config.png)

Then the Integration Command will ask you every time you launch it on what Target system you would like to perform the action:

![Ask for Target before launch](/images/Ask_target_before_launch.png)

