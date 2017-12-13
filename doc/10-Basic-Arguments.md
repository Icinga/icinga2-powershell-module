Basic Arguments
==============

To use the module a bunch of arguments are available to entirely configure the Icinga 2 Agent, 
ensuring it will correctly communicate with the Icinga 2 instances it should connect to and to 
create the required certificates for a secure communication.

## -AgentName
This is in general the name of your Windows host. It will have to match with your Icinga configuration, 
as it is part of the Icinga 2 Ticket and Certificate handling to ensure a valid certificate is generated

**Ignored by:** -FetchAgentFQDN, -FetchAgentName

**-AgentName or -FetchAgentName or -FetchAgentFQDN are required for Icinga 2 configuration
generation**

## -Ticket
The Ticket you will receive from your Icinga 2 CA. In combination with the Icinga Director, it will 
tell you which Ticket you will require for your host

**Required for Icinga 2 certificate generation**

## -InstallAgentVersion
You can either leave this parameter or add it to allow the module to install or update the Icinga 2 
Agent on your system. It has to be a string value and look like this for example:
```powershell
    -InstallAgentVersion '2.8.0'
```

**Important:** This argument is required in order to install, update or downgrade the Icinga 2
Agent on the system.

## -FetchAgentName
Instead of setting the Agent Name with -AgentName, the PowerShell module is capable of retreiving 
the information automaticly from Windows. Please note this is **not** the FQDN.

Default value: **$FALSE**

**Ignored by:** -FetchAgentFQDN

**Ignores:** -AgentName

**-AgentName or -FetchAgentName or -FetchAgentFQDN are required for Icinga 2 configuration
generation**

## -FetchAgentFQDN
Like -FetchAgentName, this argument will ensure the hostname is set inside the script, will however 
include the domain to provide the FQDN internally.

Default value: **$FALSE**

**Ignores:** -AgentName, -FetchAgentName

**-AgentName or -FetchAgentName or -FetchAgentFQDN are required for Icinga 2 configuration
generation**

## -TransformHostname (optional)
Allows to transform the hostname to either lower or upper case if required.
0: Do nothing
1: To lower case
2: To upper case

Defalut value: **0**

**Requires:** -AgentName or -FetchAgentName or -FetchAgentFQDN

## -AgentListenPort (optional)

This variable allows to specify on which port the Icinga 2 Agent will listen on

Default value: **5665**

## -ParentZone
Each Icinga 2 Agent is in general forwarding it's check results to a parent master or satellite zone. 
Here you will have to specify the name of the parent zone

**Required for Icinga 2 configuration generation**

## -AcceptConfig (optional)
Icinga 2 internals to make it configurable if the Agent is accepting configuration from the Icinga 
config master.

Default value: **$TRUE**

## -IcingaEnableDebugLog (optional)

This argument will define if the Icinga 2 debug log will be enabled or disabled.

Default value: **$FALSE**

## -AgentAddFirewallRule (optional)

Allows to specify if the PowerShell Module will add a firewall rule, allowing Icinga 2 masters or
Satellites to connect to the Icinga 2 Agent on the defined port

Default value: **$FALSE**

## -ParentEndpoints

This parameter requires an array of string values, to which endpoints the Agent should in general 
connect to. If you are only having one endpoint, only add one. You will have to specify all endpoints 
the Agent requires to connect to. Examples:
```powershell
    -ParentEndpoints 'icinga2a'
    -ParentEndpoints 'icinga2a', 'icinga2b'
    -ParentEndpoints 'icinga2a', 'icinga2b', 'icinga2c'
```

**Required for Icinga 2 configuration generation**

## -EndpointsConfig (optional)

While -ParentEndpoints will define the name of endpoints by an array, this parameter will allow to 
assign IP address and port configuration, allowing the Icinga 2 Agent to directly connect to parent 
Icinga 2 instances. To specify IP address and port, you will have to seperate these entries by using 
';' without blank spaces. The order of the config has to match the assignment of -ParentEndpoints. 
You can specify the IP address only without a port definition by just leaving the last part.
If you wish to not specify a config for a specific endpoint, simply add an empty string to the correct 
location.

**Examples:**
```powershell
    -ParentEndpoints 'icinga2a' -EndpointsConfig 'icinga2a.localhost;5665'
    -ParentEndpoints 'icinga2a', 'icinga2b' -EndpointsConfig 'icinga2a.localhost;5665', 'icinga2b.localhost'
    -ParentEndpoints 'icinga2a', 'icinga2b', 'icinga2c' -EndpointsConfig 'icinga2a.localhost;5665', 'icinga2b.localhost', 'icinga2c.localhost;5665'
    -ParentEndpoints 'icinga2a', 'icinga2b', 'icinga2c' -EndpointsConfig 'icinga2a.localhost;5665', '', 'icinga2c.localhost;5665'
```

## -GlobalZones (optional)

Allows to specify global zones, which will be added into the icinga2.conf.

**Note:** In case no global zone will be defined, ***director-global*** will be added by default. If
you specify zones by yourself, please ensure to add **director-global** as this is not done automaticly
when adding custom global-zones.

**Example:**
```powershell
    -GlobalZones 'global-linux', 'global-windows', 'global-commands'
    -GlobalZones 'director-global', 'global-linux', 'global-windows', 'global-commands'
```

## -IcingaServiceUser (optional)

This argument will allow to override the user the Icinga 2 service is running with. Windows provides
some basic users already which can be configured:

* LocalSystem
* NT AUTHORITY\NetworkService (Icinga default)
* NT AUTHORITY\LocalService

If you require an own user, you can add that one as well for the argument. If a password is required
for the user to login, seperate username and password with a ':'.

Example: jdoe:mysecretpassword

Furthermore you can also use domains in combination and pass them over.

Example: icinga\jdoe:mysecretpassword

## -DownloadUrl

With this parameter you can define a download Url or local directory from which the module will 
download/install a specific Icinga 2 Agent MSI Installer package. Please ensure to **only define the 
base download Url / Directory**, as the Module **will generate the MSI file name based on your operating 
system architecture and the version to install**. The Icinga 2 MSI Installer name is internally build 
as follows: *Icinga2-v[InstallAgentVersion]-[OSArchitecture].msi*

Full example: Icinga2-v2.8.0-x86_64.msi

Default value: **https://packages.icinga.com/windows/**

**Requires:** -InstallAgentVersion

## -AgentInstallDirectory (optional)

Allows to specify in which directory the Icinga 2 Agent will be installed into. In case of an
Agent update you can specify with this argument a new directory the new Agent will be
installed into. The old directory will be removed caused by the required uninstaller process.

**Examples:**
```powershell
    -AgentInstallDirectory 'C:\MyIcinga2Agent'
    -AllowUpdates -InstallAgentVersion '2.8.0' -AgentInstallDirectory 'C:\MyNewIcinga2Agent'
```

## -AllowUpdates (optional)

In case the Icinga 2 Agent is already installed on the system, this parameter will allow you to 
configure if you wish to upgrade / downgrade to a specified version with the *-InstallAgentVersion* parameter as well. If none of both parameters is defined, the module will not update or downgrade the agent.

If argument *-AgentInstallDirectory* is not specified, the Icinga 2 Agent will be installed into
the same directory as before. In case defined, the PowerShell Module will use the new directory
as installation target.

Default value: **$FALSE**

**Requires:** -InstallAgentVersion

## -InstallerHashes (optional)

To ensure downloaded packages are build by the Icinga Team and not compromised by third parties, you 
will be able to provide an array of SHA1 hashes here. In case you have defined any hashses, the module 
will not continue with updating / installing the Agent in case the SHA1 hash of the downloaded MSI 
package is not matching one of the provided hashes of this parameter.

**Example:**
```powershell
    -InstallerHashes 'hash1'
    -InstallerHashes 'hash1', 'hash2'
    -InstallerHashes 'hash1', 'hash2', 'hash3'
```    

## -FlushApiDirectory (optional)

In case the Icinga Agent will accept configuration from the parent Icinga 2 system, it will possibly 
write data to /var/lib/icinga2/api/* By adding this parameter to your script call, all content inside the api 
directory will be flushed once a change is detected by the module which requires a restart of the 
Icinga 2 Agent

Default value: **$FALSE**

## -CAServer

Here you can provide a string to the Icinga 2 CA or any other CA responsible to generate the required 
certificates for the SSL communication between the Icinga 2 Agent and it's parent

**Required for Icinga 2 certificate generation**

## -CAPort (optional)

Here you can specify a custom port in case your CA Server is not listening on 5665

Default value: **5665**

## -ForceCertificateGeneration (optional)

The module will generate the certificates in general only if one of the required files is missing. By 
adding this parameter to your call, the module will force the re-creation of the certificates.

Default value: **$FALSE**

## -CAFingerprint (optional)

This option will allow the validation of the trusted-master.crt generated during certificate generation, 
to ensure we are connected to the correct endpoint to prevent possible man-in-the-middle attacks.

## -FullUninstallation (optional)

This argument is only used by the function 'uninstall' and will remove
the remaining content from 'C:\Program Data\icinga2' to prepare a clean setup of the Icinga 2
infrastrucure.

Default value: **$FALSE**

## -RemoveNSClient (optional)

When this argument is set, the installed NSClient++ will be removed from the system as well.
This argument is only used by calling the function 'uninstall'

Default value: **$FALSE**

## -DebugMode (optional)

This is simply for development purposes and is barely used inside the module. Might change in the future.

Default value: **$FALSE**

## -ModuleLogFile (optional)

Specify a path to either a directory or a file to write all output from the PowerShell module into a
file for later debugging. In case a directory is specified, the script will automaticly create a new
file with a unique name into it. If a file is specified which is not yet present, it will be created.

**Examples:**
```powershell
    -ModuleLogFile 'C:\mylogs'
    -ModuleLogFile 'C:\mylogs\mylogfile.log'
```

## -RunInstaller (optional)

This argument allows to shorten the entire call of the module, not requiring to define
a custom variable and executing the installation function of the monitoring components.

**Instead of**
```powershell
    $icinga = Icinga2AgentModule `
              -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
              -DirectorAuthToken '34086b3480965b083476c08346c34980';

    exit $icinga.install();
```

**You can use**
```powershell
    exit Icinga2AgentModule `
              -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
              -DirectorAuthToken '34086b3480965b083476c08346c34980' `
              -RunInstaller;
```

Which has in the result the same effect.

## -RunUninstaller (optional)

This argument allows to shorten the entire call of the module, not requiring to define
a custom variable and executing the uninstallation function of the monitoring components.

**Instead of**
```powershell
    $icinga = Icinga2AgentModule  `
              -FullUninstallation `
              -RemoveNSClient

    exit $icinga.uninstall();
```

**You can use**
```powershell
    exit Icinga2AgentModule `
              -FullUninstallation `
              -RemoveNSClient     `
              -RunUninstaller;
```

Which has in the result the same effect.

**NOTE:** You can also combine both arguments *-RunInstaller* and *-RunUninstaller* in the same
call. The **uninstaller** function is **always called before** to the **installation** function.

## -IgnoreSSLErrors (optional)

In certain cases it could be required to ingore SSL certificate validations from the
Icinga Web 2 installation (for example in case self-signed certificates are used). By default
the PowerShell Module is validating SSL certificates and throws an error if the validation fails.

In case self-signed certificates are used and not included to the local certificate store
of the Windows machine, the module will fail. By providing this argument, validation will
always be valid and the script will execute as if the certificate was valid.

**Example:**
```powershell
    exit Icinga2AgentModule
              -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
              -DirectorAuthToken '34086b3480965b083476c08346c34980' `
              -IgnoreSSLErrors `
              -RunInstaller;