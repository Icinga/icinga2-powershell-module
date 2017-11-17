Installing the Module
=====================================

This project can be used in two different ways. As simple PowerShell Script is beeing installed as 
PowerShell module within the Windows environment.

Install the module as real PowerShell module
--------------

At first we need to obtain folders in which we can install the module. For this type the following into 
your PowerShell
```powershell
    echo $env:PSModulePath
```    

Depending on your requirements who will be allowed to execute functions from the module, install it 
inside one of the provided folders. On demand you can also modify your path variable inside the Windows 
settings to add another module location.

While inside the modules folder, simply clone this repository or create a folder, named exactly like the 
.psm1 file and place it inside. Once done restart your PowerShell and validate the correct installation 
of the module by writing
```powershell
    Get-Module -ListAvailable
```    

You might require to scroll a bit to locate your module directory with the installed Icinga 2 module. 
Once it's there, the installation was successfull

If you are done, you might want to take a look on the [example page](30-Examples.md).

## Important note for PowerShell version 2 environments

In order to get the module working, it is **not** enough to copy it into a module directory as described above for PowerShell version 2. Before you can use it, you will require to **import** the module with the following command for each PowerShell session:

```powershell
    Import-Module Icinga2Agent
```

If you design your own script or execute the commands over PowerShell remote execution, the import command is always required as first command.

A working example looks like this:
```powershell
    Import-Module Icinga2Agent;
    exit $icinga = Icinga2AgentModule `
                   -DirectorUrl       'https://icinga2-master.example.com/icingaweb2/director/' `
                   -DirectorAuthToken '34086b3480965b083476c08346c34980' `
                   -RunInstaller;
```

This is only required for PowerShell Version 2. Version 3 and above will import the module automaticly once a PowerShell console is beeing opened.