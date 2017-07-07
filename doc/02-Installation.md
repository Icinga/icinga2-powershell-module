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