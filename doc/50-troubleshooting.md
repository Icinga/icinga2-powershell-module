Troubleshooting
==============

It might come the time on which you require to review your Icinga 2 Agent setup and to get further informations from the current configuration and objects loaded by Icinga 2. The module will assist you with this as well and provides two arguments to query all required informations.

## -DumpIcingaConfig
In case the agent is installed on the system, this argument will allow you to dump the current icinga2.conf to the PowerShell console or to a logfile by adding the argument -ModuleLogFile in addition.

Example:
```powershell
    Icinga2AgentModule -DumpIcingaConfig
```

## -DumpIcingaObjects
Besides the configuration of Icinga 2, it might become handy to receive an output of all objects loaded by the Icinga 2 Agent. The module will automaticly locate the icinga2.exe from your system and query the objects, printing them to the console. In addition you can specify a logfile path with the -ModuleLogFile argument.

Example:
```powershell
    Icinga2AgentModule -DumpIcingaObjects
```

### Additional notes
Like already mentioned above, writing the result to a logfile is possible as well including the combination of both arguments. This is just a example to output both configurations and write them into a custom logfile in addition:
```powershell
    Icinga2AgentModule           `
              -DumpIcingaConfig  `
              -DumpIcingaObjects `
              -ModuleLogFile     'C:\icinga2_settings.txt'
```