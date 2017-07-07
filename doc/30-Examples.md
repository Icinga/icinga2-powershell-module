Examples for using the module
==============

Below you will find some examples to use the module for installing Icinga 2 versions, fetching 
the Agent names and to create host objects within the Icinga Director including automated deployment.

## Basic installation and configuration

This example will install the Icinga 2 Agent, retreive the name of the Windows host, writing all
required configuration to the disk and retreicing the ticket for certificate signing from the
Icinga Director

```powershell
    $icinga = Icinga2AgentModule `
              -InstallAgentVersion  '2.6.3' `
              -AllowUpdates         $TRUE `
              -FetchAgentFQDN       $TRUE `
              -DirectorUrl          'https://icinga2a-master.localdomain' `
              -DirectorUser         'icingaadmin' `
              -DirectorPassword     'icinga' `
              -CAServer             'icinga2a-master.localdomain' `
              -ParentZone           'icinga2-master-zone' `
              -ParentEndpoints      'icinga2a-master.localdomain', 'icinga2b-master.localdomain' `

    exit $icinga.installMonitoringComponents()          
```

## Basic installation with host creation and deployment

This example will do the same as above, but will in addition create the host inside the Icinga Director. 
The **&hostname_placeholder&** variable is replaced automaticly with the Agents name, making things alot 
easier for us. As we are using the FQDN, we also got our IP Adress automaticly. Once done, the 
Icinga Director will also deploy the configuration immediately and the monitoring is ready.

```powershell
    $icinga = Icinga2AgentModule `
              -InstallAgentVersion  '2.6.3' `
              -AllowUpdates         $TRUE `
              -FetchAgentFQDN       $TRUE `
              -DirectorUrl          'https://icinga2a-master.localdomain' `
              -DirectorUser         'icingaadmin' `
              -DirectorPassword     'icinga' `
              -DirectorHostObject   '{"object_name":"&hostname_placeholder&","object_type":"object","vars":{"os":"Windows"},"imports":["Icinga Agent"],"address":"&hostname_placeholder&","display_name":"&hostname_placeholder&"}' `
              -CAServer             'icinga2a-master.localdomain' `
              -DirectorDeployConfig $TRUE `
              -ParentZone           'icinga2-master-zone' `
              -ParentEndpoints      'icinga2a-master.localdomain', 'icinga2b-master.localdomain' `

    exit $icinga.installMonitoringComponents()          
```