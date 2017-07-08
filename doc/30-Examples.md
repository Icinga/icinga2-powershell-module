Examples for using the module
==============

Below you will find some examples to use the module for installing Icinga 2 versions, fetching 
the Agent names and to create host objects within the Icinga Director including automated deployment.


Use the module as simple PowerShell script
--------------

The module is designed to work as simple PowerShell script which can either be executed from the 
PowerShell or by parsing the entire content into a PowerShell console.
To make the script executable from within the PowerShell, rename it from .psm1 to .ps1

### Simle examples as script

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

    exit $icinga.installMonitoringComponents();
```

### Switch Icinga 2 Debug log

The PowerShell module provides a feature to enable / disable the Icinga 2 debug log. To enable the debug
log, simply use this function call:

```powershell
    $icinga = Icinga2AgentModule -IcingaEnableDebugLog $TRUE

    exit $icinga.installMonitoringComponents();
```

To disable the debug log, either set the variable to $FALSE or leave the argument empty.

### Change Icinga Agent service user

In some cases it might be required to run the Icinga 2 service as different user, to grant more 
privileges to the Agent. If we want to run the Agent with the NetworkService user, we can modify
it pretty simple:

```powershell
    $icinga = Icinga2AgentModule -IcingaServiceDetails 'NT AUTHORITY\NetworkService'

    exit $icinga.installMonitoringComponents();
```

If we have created a custom user within a domain we want to use, this can be done as well:

```powershell
    $icinga = Icinga2AgentModule -IcingaServiceDetails 'icinga\jdoe:mysecretpassword'

    exit $icinga.installMonitoringComponents();
```

### Hand over JSON converted string to DirectorHostObject argument

To simply create JSON valid strings and to hand them over to the PowerShell Module you can use
the ConvertTo-Json function which creates JSON strings out of hashtables.

**Note: ConvertTo-Json is only available on PowerShell 3.x and later. On PowerShell 2.x you will
have to write the JSON-String yourself.**

An example may look like this:

```
    $JSONObject= @{
      'address'      = '127.0.0.1'
      'object_name'  = '&hostname_placeholder&'
      'display_name' = '&hostname_placeholder&'
      'object_type'  = 'object'
      'imports'      = ('Icinga Agent')
    }

    $icinga = Icinga2AgentModule `
              -DirectorHostObject (ConvertTo-Json -Compress $JSONObject)

    $icinga.installMonitoringComponents();
```

### Recommended automation with Icinga Director Self Service API

For more details please take a look on the [Icinga Director Automation Guide](20-Automation.md).

```
    $icinga = Icinga2AgentModule `
              -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
              -DirectorAuthToken '34086b3480965b083476c08346c34980'

    $icinga.installMonitoringComponents();
```

### Basic Icinga installation and configuration

This example will install the Icinga 2 Agent, retreive the name of the Windows host, writing all
required configuration to the disk and retreicing the ticket for certificate signing from the
Icinga Director

```powershell
    $icinga = Icinga2AgentModule `
              -InstallAgentVersion  '2.6.3' `
              -AllowUpdates         $TRUE `
              -FetchAgentFQDN       $TRUE `
              -DirectorUrl          'https://icinga2a-master.example.com/icingaweb2/director/' `
              -DirectorUser         'icingaadmin' `
              -DirectorPassword     'icinga' `
              -CAServer             'icinga2a-master.example.com' `
              -ParentZone           'icinga2-master-zone' `
              -ParentEndpoints      'icinga2a-master.example.com', 'icinga2b-master.example.com' `

    exit $icinga.installMonitoringComponents();
```

### Basic Icinga installation with host creation and deployment

This example will do the same as above, but will in addition create the host inside the Icinga Director. 
The **&hostname_placeholder&** variable is replaced automaticly with the Agents name, making things alot 
easier for us. As we are using the FQDN, we also got our IP Adress automaticly. Once done, the 
Icinga Director will also deploy the configuration immediately and the monitoring is ready.

```powershell
    $icinga = Icinga2AgentModule `
              -InstallAgentVersion  '2.6.3' `
              -AllowUpdates         $TRUE `
              -FetchAgentFQDN       $TRUE `
              -DirectorUrl          'https://icinga2a-master.example.com/icingaweb2/director/' `
              -DirectorUser         'icingaadmin' `
              -DirectorPassword     'icinga' `
              -DirectorHostObject   '{"object_name":"&hostname_placeholder&","object_type":"object","vars":{"os":"Windows"},"imports":["Icinga Agent"],"address":"&hostname_placeholder&","display_name":"&hostname_placeholder&"}' `
              -CAServer             'icinga2a-master.example.com' `
              -DirectorDeployConfig $TRUE `
              -ParentZone           'icinga2-master-zone' `
              -ParentEndpoints      'icinga2a-master.example.com', 'icinga2b-master.example.com' `

    exit $icinga.installMonitoringComponents();
```