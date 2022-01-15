# Like the work dont forget to hit that Star Button

# Note about this Ceramicskate0's fork:
Ceramicskate0's fork of SwiftOnSecurity's sysmon config differs in 1 key area. With the exception of RegistryEvent, FileCreateTime, ImageLoads, and ProcessAccess I have tried to take a exclude only approach. I use [SWELF](https://github.com/ceramicskate0/SWELF) to ship my logs and thus do not get all of them on the SIEM. I only get the logs I want and if I ever needed all the logs they will remain on the end point until they roll (assuming they dont get cleared or modified). This means that the idea behind this config is that you have only logs for events of interest. It is my hope that a config with this approach gets you to that ~80% solution to start your testing with. Also this fork is under more rapid development than all others.

# Things you need to know:
Due to ongoing research please search the config file for the comment ``Could miss things if you leave this uncommented, but it also reduces noise`` and review each one (yes there are alot) to see if that EventID and that object on that line is something you want to monitor or not. If you dont want to have that object excluded, comment or remove the line in the config if its in the excluded ruleset. These are decisions I cant make for you. Some of them are good files that I know could be used for evil BUT they do generate alot of noise doing normal activities. I do try and narrow them down to a smaller list but I can only do so much.

[HOW TO INSTALL SYSMON AND UPDATE WITH SCHEDULED TASK HERE](https://github.com/ceramicskate0/Scripts/tree/master/WindowsBatch)

[If a .Net EXE is more your thing HERE you go](https://github.com/ceramicskate0/AutoUpdateSysmonEXE)

# sysmon-config | A Sysmon configuration file for everybody to fork #

This is a Microsoft Sysinternals Sysmon configuration file template with default high-quality event tracing.

The file provided should function as a great starting point for system change monitoring in a self-contained package. This configuration and results should give you a good idea of what's possible for Sysmon. Note that this does not track things like authentication and other Windows events that are also vital for incident investigation.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**[sysmonconfig-export.xml](https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml)**

Because virtually every line is commented and sections are marked with explanations, it should also function as a tutorial for Sysmon and a guide to critical monitoring areas in Windows systems.

Pull requests and issue tickets are welcome, and new additions will be credited in-line or on Git.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**[See forks of this configuration](https://github.com/SwiftOnSecurity/sysmon-config/network)**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**[See @ion-storm Threat Intelligence SIEM fork](https://github.com/ion-storm/sysmon-config)**

Note: Exact syntax and filtering choices are deliberate to catch appropriate entries and to have as little performance impact as possible. Sysmon's filtering abilities are different than the built-in Windows auditing features, so often a different approach is taken than the normal static listing of every possible important area.

## Use ##
### Install ###
Run with administrator rights
~~~~
sysmon.exe -accepteula -i sysmonconfig-export.xml
~~~~

### Update existing configuration ###
Run with administrator rights
~~~~
sysmon.exe -c sysmonconfig-export.xml
or
sysmon.exe -i sysmonconfig-export.xml
~~~~

### Uninstall ###
Run with administrator rights
~~~~
sysmon.exe -u
~~~~

## Required actions ##

### Prerequisites ###
Highly recommend using [Notepad++](https://notepad-plus-plus.org/) to edit this configuration. It understands UNIX newline format and does XML syntax highlighting, which makes this very understandable. If Visual Studio Code is more your thing you could look at [darkoperator's vscode-sysmon](https://github.com/darkoperator/vscode-sysmon). I do not recommend using the built-in Notepad.exe.

### Customization ###
You will need to install and observe the results of the configuration in your own environment before deploying it widely. For example, you will need to exclude actions of your antivirus, which will otherwise likely fill up your logs with useless information.

The configuration is highly commented and designed to be self-explanatory to assist you in this customization to your environment.

### Design notes ###
This configuration expects software to be installed system-wide and NOT in the C:\Users folder. 

If your users install Chrome themselves, you should deploy the [Chrome MSI](https://enterprise.google.com/chrome/chrome-browser/), which will automatically change the shortcuts to the machine-level installation. Your users will not even notice anything different.
