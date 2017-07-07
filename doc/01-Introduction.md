Introduction
==============

What is this PowerShell module for? The idea was to create a basic module, providing a framework to 
install new Icinga 2 Agents in Windows more easily in combination with the Icinga Director.
Depending on the configuration of the module, you can install / update the Icinga 2 Agent, sign the 
certificates on your CA (the Icinga 2 master for example) and create the required configuration to 
operate the Agent on Windows correctly.

Furthermore the design allows to install the NSClient++ in addition with a simple configuration, allowing 
the Icinga 2 Agent to locally execute the NSClient to retreive most of the Windows parameters, without 
having to develop custom scripts or modules.

Since the latest version of the module and the Icinga Director 1.4.x, the entire process to install new 
Agents on Windows can be fully automated. The only requirement is a possible connection from the Windows 
host to the Icinga Director Webinterface and the Icinga CA Server.

If you are ready to get started, take a look on the [installation guide](02-Installation.md).