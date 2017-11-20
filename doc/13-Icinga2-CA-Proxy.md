CA-Proxy Arguments
==============

The Icinga 2 CA-Proxy is a new feature available since version 2.8.0. This will allow an Agent to create own certificates and wait for a Icinga 2 Master or Icinga 2 Satellite to establish connection. The request is then send from the Agent through all Parents to the Icinga 2 CA. There you will be able to sign the certificates, allowing the Agent to properly communicate with the Icinga 2 environment

## -CAProxy
In order to use the module with the CA-Proxy, simply use it as before. Instead of the **-Ticket** argument, use this one to tell the module to use the CA-Proxy feature.

Full Example:

```powershell
    Icinga2AgentModule                                    `
              -InstallAgentVersion 2.8.0                  `
              -AllowUpdates                               `
              -ParentZone          'icinga-master'        `
              -ParentEndpoints     'icinga2a', 'icinga2b' `
              -FetchAgentFQDN                             `
              -CAProxy                                    `
              -CACertificatePath   'C:\certs\ca.crt'      `
              -RunInstaller;
```
Default value: **$FALSE**

## -CACertificatePath
In order for the CA-Proxy to sign your certificate and to allow the entire process to succeed, you will have to copy the CA certificate to the certificate directory of Icinga 2. To make this as easy as possible, you can deploy the Icinga 2 CA certificate file either to a shared volume or by Group Policies to a specific director within your Windows machine.

The name of the file does not matter, has however be specified within the argument.

Example:
```powershell
    -CACertificatePath   'C:\Userdata\Administrator\certificates\Icinga 2 CA.crt'
```

This will copy the file **Icinga 2 CA.crt** to the location
```
    C:\ProgramData\icinga2\var\lib\icinga2\certs\ca.crt
```

The name is automaticly changed to ca.crt which is the required name for Icinga 2.

### Notes for Icinga 2
In order to complete the process for the certificate signing, you will have to log into your Icinga 2 system on which the CA server is specified. Now use the command

```bash
    icinga2 ca list
```

to get a list of all requests you have received from your Agents. The list is splitted into 4 tables (Fingerprint, Timestamp, Signed and Subject). The subject is the name of the Agent specified during the script run and the timestamp for the request. If a certificate is already signed, the column Signed is flagged with a **\***.

To sign a certificate, you will require to copy the fingerprint into the following command:

```bash
    icinga2 ca sign 23fa49d320c26c04b5d4d5d9d02d36bdae1aeb28a2bd51cc101925f0b2ec57f8
```

Once done, the Agent is now fully operational and integrated into your Icinga 2 infrastructure.