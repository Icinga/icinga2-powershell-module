Icinga Director Arguments
==============

The Icinga Director support allows to achieve more goals with the module, as there is a way to 
[fully automate](20-Automation.md) the script, making the installation and configuration alot easier.

## Secure automation (recommended)

The following two arguments provide the prefered way to automate the installation of the Icinga 2 Agent 
in combination with the Icinga Director in Windows systems. It is the recommended and most secure way.

### -DirectorUrl
This argument will tell the PowerShell where the Icinga Director can be found. Please specify the entire 
path to the Icinga Director!
Example: https://example.com/icingaweb2/director/

### -DirectorAuthToken
API key for specific host templates, allowing the configuration and creation of host objects within the 
Icinga Director without password authentication. This is the API token assigned to a host template. 
Hosts created with this token, will automaticly receive the Host-Template assigned to the API key. 
Furthermore this token allows to access the Icinga Director Self-Service API to fetch basic arguments 
for the module.

**Note: This argument requires Icinga Director API Version 1.4.0 or higher**

## Simple automation

The following arguments can be used to customize and access more features from the Icinga Director, 
is however **not recommended** because of the security issue caused by the requirement to add user and 
password data to the script. In addition to the following arguments, you will require the -DirectorUrl 
as well.

### -DirectorUser
To fetch the Ticket for a host, creating host objects or deploying the configuration you will have to 
authenticate against the Icinga Director. This parameter allows to set the User we shall use to login.

### -DirectorPassword
To fetch the Ticket for a host, creating host objects or deploying the configuration you will have to 
authenticate against the Icinga Director. This parameter allows to set the Password we shall use to login.

### -DirectorHostObject
This argument allows you to parse an JSON formated, compressed (flat) string to the PowerShell Module, 
allowing the module to connect to the Icinga Director API to create it.
Example:
```json
    {"object_name":"&hostname_placeholder&","object_type":"object","vars":{"os":"Windows"},"imports":["Icinga Agent"],"address":"&hostname_placeholder&","display_name":"&hostname_placeholder&"}
```

For a simplier configuration in certain cases, you can use the placeholder **&hostname_placeholder&** 
which will be replaced internally by either the -AgentName, -FetchAgentName or -FetchAgentFQDN parameter 
defined hostname.

### -DirectorDeployConfig
If this parameter is set to **$TRUE**, the PowerShell module will tell the Icinga Director to deploy 
outstanding configurations. This parameter can be used in combination with -DirectorHostObject, to 
create objects and deploy them right away. This argument requires the user and password argument and 
will not work with the Self Service api.

**Caution: If set, all outstanding deployments inside the Icinga Director will be deployed. Use with 
caution!!!**

Default value: **$FALSE**