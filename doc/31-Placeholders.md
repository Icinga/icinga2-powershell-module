Description of possible placeholders
==============

The PowerShell module provides a range of placeholders which can be defined within a JSON-String
to allow a more dynamic management on how hosts are created within the Icinga Director.
Below you will find a range of placeholders, including a detailed description.

### &hostname_placeholder&

This variable is the default placeholder and is build by the provided arguments

* -AgentName
* -FetchAgentFQDN
* -FetchAgentName
* -TransformHostname

Depending on the above settings, the output will differ.

### &hostname&

This variable contains the name of the host only, without a possible domain.
In addition this variable allows the transformation by extending the name with

* .lowerCase
* .upperCase

Some examples can look like

```
    $json = '{ "display_name": "&hostname&" }'
```

```
    $json = '{ "display_name": "&hostname.lowerCase&" }'
```

```
    $json = '{ "display_name": "&hostname.upperCase&" }'
```

### &fqdn&

This variable contains the name of the host including the domain.
In addition this variable allows the transformation by extending the name with

* .lowerCase
* .upperCase

Some examples can look like

```
    $json = '{ "display_name": "&fqdn&" }'
```

```
    $json = '{ "display_name": "&fqdn.lowerCase&" }'
```

```
    $json = '{ "display_name": "&fqdn.upperCase&" }'
```

### &ipaddress&

By default the module will try to fetch **ALL** IP-Addresses available on the system, making them
accessable on runtime. This placeholder will be replaced with a found IPv4 address.

As a host could contain multiple IPv4 addresses, there are several ways to specify which one you
wanna use:

Use the first found IPv4 address from the host
```
    $json = '{ "address": "&ipaddress&" }'
```

Use a specific IPv4 address from an array index
```
    $json = '{ "address": "&ipaddress[1]&" }'
```

**Note:** If there are multiple addresses found and you wish to use the first address, it doesnt
matter if you are using &ipaddress& or &ipaddress[0]&

### &ipaddressV6&

By default the module will try to fetch **ALL** IP-Addresses available on the system, making them
accessable on runtime. This placeholder will be replaced with a found IPv6 address.

As a host could contain multiple IPv6 addresses, there are several ways to specify which one you
wanna use:

Use the first found IPv6 address from the host
```
    $json = '{ "address": "&ipaddressV6&" }'
```

Use a specific IPv6 address from an array index
```
    $json = '{ "address": "&ipaddressV6[1]&" }'
```

**Note:** If there are multiple addresses found and you wish to use the first address, it doesnt
matter if you are using &ipaddressV6& or &ipaddressV6[0]&