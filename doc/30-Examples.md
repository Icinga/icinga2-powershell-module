Examples for using the module
==============

Below you will find some examples to use the module for installing Icinga 2 versions, fetching 
the Agent names and to create host objects within the Icinga Director including automated deployment.


Use the module as simple PowerShell script
--------------

The module is designed to work as simple PowerShell script which can either be executed from the 
PowerShell or by parsing the entire content into a PowerShell console.
To make the script executable from within the PowerShell, rename it from .psm1 to .ps1

### Simple examples as script

To use the module (or as script) you will at first have to initialise a variable with the function 
including parameters

```powershell
    $icinga = Icinga2AgentModule
```    

Now you will have all members and variables availalbe inside $icinga, which can be used to install the 
Agent for example. As we require some parameters to ensure the module knows what you are intending to do, 
here is a full example for installing an Agent:

```powershell
    $icinga = Icinga2AgentModule `
              -AgentName        'windows-host-name' `
              -Ticket           '3459843583450834508634856383459' `
              -ParentZone       'icinga-master' `
              -ParentEndpoints  'icinga2a', 'icinga2b' `
              -CAServer         'icinga-master'

    exit $icinga.install();
```

### Switch Icinga 2 Debug log

The PowerShell module provides a feature to enable / disable the Icinga 2 debug log. To enable the debug
log, simply use this function call:

```powershell
    $icinga = Icinga2AgentModule -IcingaEnableDebugLog

    exit $icinga.install();
```

To disable the debug log, either set the variable to $FALSE or leave the argument empty.

### Change Icinga Agent service user

In some cases it might be required to run the Icinga 2 service as different user, to grant more 
privileges to the Agent. If we want to run the Agent with the NetworkService user, we can modify
it pretty simple:

```powershell
    $icinga = Icinga2AgentModule -IcingaServiceUser 'NT AUTHORITY\NetworkService'

    exit $icinga.install();
```

If we have created a custom user within a domain we want to use, this can be done as well:

```powershell
    $icinga = Icinga2AgentModule -IcingaServiceUser 'icinga\jdoe:mysecretpassword'

    exit $icinga.install();
```

### Recommended automation with Icinga Director Self Service API

For more details please take a look on the [Icinga Director Automation Guide](20-Automation.md).

```powershell
    $icinga = Icinga2AgentModule `
              -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
              -DirectorAuthToken '34086b3480965b083476c08346c34980'

    $icinga.install();
```

### Basic Icinga installation and configuration

This example will install the Icinga 2 Agent, retreive the name of the Windows host, writing all
required configuration to the disk and retreicing the ticket for certificate signing from the
Icinga Director

```powershell
    $icinga = Icinga2AgentModule `
              -InstallAgentVersion  '2.8.0' `
              -AllowUpdates                 `
              -FetchAgentFQDN               `
              -DirectorUrl          'https://icinga2a-master.example.com/icingaweb2/director/' `
              -DirectorUser         'icingaadmin' `
              -DirectorPassword     'icinga' `
              -CAServer             'icinga2a-master.example.com' `
              -ParentZone           'icinga2-master-zone' `
              -ParentEndpoints      'icinga2a-master.example.com', 'icinga2b-master.example.com' `

    exit $icinga.install();
```

### Basic Icinga installation with host creation and deployment

This example will do the same as above, but will in addition create the host inside the Icinga Director. 
The **&hostname_placeholder&** variable is replaced automaticly with the Agents name, making things alot 
easier for us. As we are using the FQDN, we also got our IP Adress automaticly. Once done, the 
Icinga Director will also deploy the configuration immediately and the monitoring is ready.

Take a look on the [placeholders description](31-Placeholders.md) to get to know about additional
available values.

```powershell
    $icinga = Icinga2AgentModule `
              -InstallAgentVersion  '2.8.0' `
              -AllowUpdates                 `
              -FetchAgentFQDN               `
              -DirectorUrl          'https://icinga2a-master.example.com/icingaweb2/director/' `
              -DirectorUser         'icingaadmin' `
              -DirectorPassword     'icinga' `
              -DirectorHostObject   '{"object_name":"&hostname_placeholder&","object_type":"object","vars":{"os":"Windows"},"imports":["Icinga Agent"],"address":"&hostname_placeholder&","display_name":"&hostname_placeholder&"}' `
              -CAServer             'icinga2a-master.example.com' `
              -DirectorDeployConfig `
              -ParentZone           'icinga2-master-zone' `
              -ParentEndpoints      'icinga2a-master.example.com', 'icinga2b-master.example.com' `

    exit $icinga.install();
```

### Shorten the script call

The PowerShell module also provides a possibility to shorten certain actions, not requiring to
define a variable and executing funtions.

**Installation example**

```powershell
    exit Icinga2AgentModule `
              -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
              -DirectorAuthToken '34086b3480965b083476c08346c34980' `
              -RunInstaller;
```

**Uninstallation example**

```powershell
    exit Icinga2AgentModule -RunUninstaller;
```

**Combine uninstallation and installation at once**

```powershell
    exit Icinga2AgentModule `
              -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
              -DirectorAuthToken '34086b3480965b083476c08346c34980' `
              -RunUninstaller `
              -RunInstaller;
```
