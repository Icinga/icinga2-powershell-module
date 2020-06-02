Deprecation Notice
===

This module is deprecated with version 1.3.0. Please use the new [Icinga for Windows](https://icinga.com/docs/windows/latest/) solution for future projects.

Icinga 2 Powershell Module
==============

Welcome to the Icinga 2 PowerShell Module - the most flexible and easy way to configure and install
Icinga 2 Agents on Windows. If you are new to this module, you might want to read the
[installation guide](doc/02-Installation.md) first.

SSL Protocol Workaround
-------------

In the current PowerShell Version distributed by Microsoft, it could appear that TLS 1.2 is not activated within your environment by default. This will result in failing connections to the Icinga Director for example.
As a workaround, you will have to set the SSL Protocol manually within your PowerShell environment or within your script.

Example:
```PowerShell
[Net.ServicePointManager]::SecurityProtocol = "tls12, tls11";
```

This will enable support for TLS Version 1.1 and 1.2. Once this issue is fixed by Microsoft, this workaround is no longer needed. To test if your system is affected by this, you can try to connect to GitHub via PowerShell over HTTPS

```
Invoke-WebRequest https://github.com
```

If this call works without SSL errors, you are save to go. In case you run into an SSL error, you will have to use the above workaround within your session. Afterwards the connection will work.

Documentation
-------------

Please take a look on the following content to get to know the possibilities of the module including
examples on how to use it.

* [Introduction](doc/01-Introduction.md)
* [Installation Guide](doc/02-Installation.md)
* [Basic Arguments](doc/10-Basic-Arguments.md)
* [Icinga Director Arguments](doc/11-Director-Arguments.md)
* [NSClient++ Arguments](doc/12-NSClient-Arguments.md)
* [Icinga 2 CA-Proxy](doc/13-Icinga2-CA-Proxy.md)
* [Full Automation with the Icinga Director](doc/20-Automation.md)
* [Example Configuration](doc/30-Examples.md)
* [Available Placeholders](doc/31-Placeholders.md)
* [Uninstalling the Icinga 2 Agent](doc/31-Uninstall-Agent.md)
* [Writing custom extensions](doc/40-Extensions.md)
* [Troubleshooting](doc/50-troubleshooting.md)
* [Changelog](doc/70-Changelog.md)

Contributing
------------

The Icinga 2 PowerShell module is an Open Source project and lives from your contributions. No
matter whether these are feature requests, issues, translations, documentation or code.

* Please check whether a related issue alredy exists on our [Issue Tracker](https://github.com/Icinga/icinga2-powershell-module/issues)
* Send a [Pull Request](https://github.com/Icinga/icinga2-powershell-module/pulls)
* The master branche shall never be corrupt!
