Changelog
==============

1.2.0
-----

### Fixed issues and related features
* You can find issues and feature requests related to this release on our
[roadmap](https://github.com/Icinga/icinga2-powershell-module/milestone/3?closed=1)

* Added support for Icinga 2.8.0 and above
* Added support for Icinga 2 CA-Proxy
* Changed argument boolean values to switch, which changes
```powershell
    -AllowUpdates $TRUE
```

to

```powershell
    -AllowUpdates
```

for example. This applies to all values, except for **-AcceptConfig**

1.1.0
-----

### Fixed issues and related features
* You can find issues and feature requests related to this release on our
[roadmap](https://github.com/Icinga/icinga2-powershell-module/milestone/2?closed=1)

* Added additional troubleshooting support for dumping Icinga 2 configuration and objects
* Improved documentation for PowerShell 2 support and installation
* Fixed code stylings

1.0.0
-----

### Fixed issues and related features
* You can find issues and feature requests related to this release on our
[roadmap](https://github.com/Icinga/icinga2-powershell-module/milestone/1?closed=1)

### Breaking Change with -DirectorUrl
* The argument -DirectorUrl is now explicit (https://icinga2-master.example.com/icingaweb2/director/)
  and no longer implicit. Be aware to update your scripts to work with this version!
  
### Added support for Director Auto Configuration
* With Icinga Director version 1.4.0 and later you can entirely automate the installation of your 
  Icinga 2 Agent environment on Windows. Take a look on the [Automation Example](20-Automation.md)
  
### Added new HTTP handler
* The HTTP handler has been updated to properly return status codes, allowing a better handling of 
  possible errors and exceptions
  
### Added NSClient++ installer support
* Added support to automaticly install and base-configure the NSClient++ from different locations

### Added support for service user change
* Added support which allows to change the user the Icinga service is running with to grant additional
  privileges to the Agent

### Added argument for enabling / disabling debug log
* Added support for enabling or disabling the Icinga 2 debug log with a PowerShell argument. To make this
  work, you will have to ensure the configuration is written once again with this version of the
  PowerShell module. Otherwise the argument will not work.

### Added support to add inbound firewall rule
* The PowerShell module now allows to open an inbound firewall rule, allowing the connection to the Agent

### Documentation
* Updated documentation for all arguments and added additional examples and use-cases