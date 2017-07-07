Changelog
==============

1.0.0
-----

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

### Added argument for enabling / disabling debug log
* Added support for enabling or disabling the Icinga 2 debug log with a PowerShell argument. To make this
  work, you will have to ensure the configuration is written once again with this version of the
  PowerShell module. Otherwise the argument will not work.

### Various fixes and improvements
* Fixed several issues and added missing features / handlings to the module

### Documentation
* Updated documentation for all arguments and added additional examples and use-cases