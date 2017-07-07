Installing the Module
=====================================

This project can be used in two different ways. As simple PowerShell Script is beeing installed as PowerShell module within the Windows environment.

Install the module as real PowerShell module
--------------

At first we need to obtain folders in which we can install the module. For this type the following into your PowerShell
```powershell
    echo $env:PSModulePath
```    

Depending on your requirements who will be allowed to execute functions from the module, install it inside one of the provided folders. On demand you can also modify your path variable inside the Windows settings to add another module location.

While inside the modules folder, simply clone this repository or create a folder, named exactly like the .psm1 file and place it inside.
Once done restart your PowerShell and validate the correct installation of the module by writing
```powershell
    Get-Module -ListAvailable
```    

You might require to scroll a bit to locate your module directory with the installed Icinga 2 module. Once it's there, the installation was successfull

Use the module as simple PowerShell script
--------------

The module is designed to work as simple PowerShell script which can either be executed from the PowerShell or by parsing the entire content into a PowerShell console.
To make the script executable from within the PowerShell, rename it from .psm1 to .ps1

Usage Examples
--------------

To use the module (or as script) you will at first have to initialise a variable with the function including parameters

```powershell
    $icinga = Icinga2AgentModule
```    

Now you will have all members and variables availalbe inside $icinga, which can be used to install the Agent for example. As we require some parameters to ensure the module knows what you are intending to do, here is a full example for installing an Agent:

```powershell
    $icinga = Icinga2AgentModule `
              -AgentName        'windows-host-name' `
              -Ticket           '3459843583450834508634856383459' `
              -ParentZone       'icinga-master' `
              -ParentEndpoints  'icinga2a', 'icinga2b' `
              -CAServer         'icinga-master'

    exit $icinga.installIcinga2Agent()          
```    