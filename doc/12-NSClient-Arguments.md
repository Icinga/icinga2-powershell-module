NSClient++ Arguments
==============

The NSClient++ is a powerfull tool to extend the Windows monitoring with plenty of plugins and 
functions. The Powershell Module provides a bunch of features to install the client and configure 
all required basics.

## -InstallNSClient
This argument will determine if we shall install the NSClient on this windows machine or not. 
Please be aware that right now no update or downgrade features are available. Once a NSClient++ 
version is installed, no changes will be made on the system regarding the installed version.

Default value: **$FALSE**

## -NSClientAddDefaults
This argument will call the NSClient and add all default configuration values to the nsclient.ini, 
allowing an easier configuration for possible required features.

Default value: **$FALSE**

## -NSClientEnableFirewall
By default the NSClient++ installer is adding an exception for the Windows Firewall, allowing the 
external communication with the NSClient. By default the PowerShell module will remove this firewall 
rule from the Windows System. To keep it, add this argument to your script call.

Default value: **$FALSE**

## -NSClientEnableService
By default a service is installed for the NSClient++, allowing remote checks like nrpe to connect in 
case the NSClient++ is listening on an available port / ip and the firewall is setup correctly. By 
default the service will be stopped and removed from the system by the PowerShell module. In case you 
want to keep it, add this argument to your script call.

Default value: **$FALSE**

## -NSClientDirectory
With this argument you can specify a location in which the NSClient++ will be installed to. Leave this 
argument empty to install the NSClient into the default location ('C:\Program Files (x86)' for x86 
architecture and 'C:\Program Files' for x64 architecture)

## -NSClientInstallerPath
With this argument you can specify a local path or a webaddress from which the PowerShell module will 
download/install the NSClient++. If you leave this argument empty, the PowerShell module will try to 
install the NSClient from the Icinga 2 Agent package in case the Agent is intalled.