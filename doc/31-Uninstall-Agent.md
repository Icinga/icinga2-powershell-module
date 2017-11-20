Uninstalling the Icinga 2 Agent
==============

While it is quite handy to automaticly install and configure the Icinga 2 Agent, it might also become
necessary to remove the Agent from the system, including all components installed.

For this reason the module also provides the possibility to uninstall the Agent and to remove the
Program Data directory from the system in which certificates and configurations are stored.

### Full uninstallation

This example will uninstall the Agent and remove the Program Data Directory as well. If you want to keep
that, you can remove the argument '-FullUninstallation'

```powershell
    $icinga = Icinga2AgentModule -FullUninstallation

    exit $icinga.uninstall();
```

**Shorten the call**
```powershell
    exit Icinga2AgentModule -FullUninstallation -RunUninstaller;
```