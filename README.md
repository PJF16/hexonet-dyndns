# HEXONET DynDNS
Python DynDNS Script for Usage with HEXONET's DNS API.

## Description
This script uses HEXONET's API to update one of the DNS Zones in your HEXONET account with the external IP the script is being exectued from. HEXONET's API is very fast and reliable and DNS updates propagate quickly - you also are able to manipulate the TTL of a DNS record which makes this solution pretty neat. No other services but HEXONET's API are being used to acquire your external IP as well as update the respective subdomain in your account.

The script is tailored to work with OT&E DNS Zones out of the box (given a valid DNS Zone in test.user's account). For testing purposes, you can launch the script with ```DDNS_HOSTNAME=ddns.hexonet.net``` and no other parameters to test this in OT&E.

## Parameters
* **DDNS_HOSTNAME** - The hostname you want to use as your DDNS Hostname (*Required*)
* **ISPAPI_USER** - Your HEXONET User (Defaults to: *test.user*)
* **ISPAPI_PASS** - Your HEXONET Password (Defaults to: *test.passw0rd*)
* **ISPAPI_API** - Desired URL of HEXONET's API you want to use (Defaults to: *https://api.ispapi.net/api/call.cgi*)
* **ISPAPI_ENTITY** - API Entity; 1234 for OT&E, 54cd for PRODUCTION (Defaults to: *1234*)

## Usage
### Manual
```
ISPAPI_USER="HEXONET USER" -e ISPAPI_PASS="HEXONET PASS" -e DDNS_HOSTNAME="home.example.com" -e ISPAPI_ENTITY="54cd" ./hexonet-dyndns  
```

### Docker
```
docker build -t hexonet-dyndns .
docker run -it --rm --name hexonet-dyndns -e ISPAPI_USER="HEXONET USER" -e ISPAPI_PASS="HEXONET PASS" -e DDNS_HOSTNAME="home.example.com" -e ISPAPI_ENTITY="54cd" hexonet-dyndns
```

## OT&E Quick Start
To test if this works you can simply execute the script with nothing provided but ```DDNS_HOSTNAME="ddns.hexonet.net"```. This will run all commands with default credentials against HEXONET'S OT&E Environment and updates A-Record "ddns" in DNS Zone "hexonet.net." with your current IP. Be aware that this doesn't have any influence on actual DNS resolution. It's a testing environment.

```
DDNS_HOSTNAME="ddns.hexonet.net" ./hexonet-dyndns.py
2018-05-12 08:37:32,226 - INFO - Created A-Record 'ddns' in DNS Zone 'hexonet.net.': 0.0.0.0 => 46.82.111.145
```

Run it again to see what changed

```
DDNS_HOSTNAME="ddns.hexonet.net" ./hexonet-dyndns.py
2018-05-12 10:46:29,076 - INFO - Given Subdomain 'ddns' exists in DNS Zone 'hexonet.net.'
2018-05-12 10:46:29,076 - INFO - No Update necessary, IPs still match :)
```

## Remarks
* You need a Production HEXONET Account and a valid DNS Zone for this to work. You'll get a free DNS Zone with every Domain you buy at HEXONET, but you're also able to just register external DNS Zones and use HEXONET's DNS while your domain is with a different registrar.
*
