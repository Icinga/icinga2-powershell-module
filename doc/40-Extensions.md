Writing custom extensions
==============

The module itself is designed to provide a basic framework which is designed to be extended 
on demand, without modifying this module at all. The easiest way for this is to install it as 
PowerShell module. Below you will find an example for extending the PowerShell module with an 
own code snippet.

```powershell
function extendIcinga {

    #
    # Parameters you require to specify for this function
    #
    param(
        # Agent setup
        [string]$AgentName,
        [string]$Ticket,
        [string]$InstallAgentVersion,
        [array]$ParentEndpoints
    )

    #
    # Initialse an object with the Icinga2AgentModule
    # and add parameters including values for initialising
    #
    $agent = Icinga2AgentModule `
             -AgentName $AgentName `
             -Ticket $Ticket `
             -ParentEndpoints $ParentEndpoints `
             -InstallAgentVersion $InstallAgentVersion `
             -ParentZone 'icinga-parent-zone';
    
    #
    # Add a custom function doing the installation
    # and update of the icinga 2 Agent
    #
    $agent | Add-Member -membertype ScriptMethod -name 'customInstallFunction' -value {
        
        if ($this.isAgentInstalled()) {
            if (-Not $this.isAgentUpToDate()) {
                $this.updateAgent();
                $this.cleanupAgentInstaller();
            } else {
                $this.info('The Icinga Agent is up-to-date. No custom actions required.');
            }
        } else {
            $this.installAgent();
            $this.cleanupAgentInstaller();
        }
        
        $this.generateIcingaConfiguration();
        $this.applyPossibleConfigChanges();
        $this.flushIcingaApiDirectory();        
        
        # Some custom function calls
        $this.validateAgainstInternalSystem();
        
        return 0;
    }

    #
    # Another custom function we defined
    #
    $agent | Add-Member -membertype ScriptMethod -name 'validateAgainstInternalSystem' -value {
        # do some stuff
    }

    #
    # Return our extended Icinga object
    #
    return $agent;
}

$icinga = extendIcinga `
          -AgentName           'windows-host' `
          -Ticket              '43543534253453453453453435435' `
          -InstallAgentVersion '2.4.10' `
          -ParentEndpoints     'icinga2a', 'icinga2b';


exit $icinga.customInstallFunction()
```