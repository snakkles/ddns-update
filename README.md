# ddns-update
DDNS update utility, written for mythic beasts DDNS API v2, but easily modifiable.

Currently compatible with Linux systems and shells only

**Note:** Must have credentials in `~/.netrc` in the form of:
```
machine ipv4.api.mythic-beasts.com
login KEYID
password SECRET
```

See below for full usage instructions

## Dependencies:
* python3
* python3-pip
* curl
* netifaces: `pip3 install netifaces`

## Usage
1. Install dependencies (above)
1. Edit `update-ddns.sh` to reference your own hostname(s)
1. Add your account credentials to `~/.netrc`
1. `chmod 600 ~/.netrc`
### Command line
```
Usage: ./check-and-update-ddns -i|--iface (interface_name) (-v|--verbose)
```
### via Cron (recommended)
Add script to cron. Suggested crontab:
```
5 * * * * /home/you/ddns-update/check-and-update-ddns -i eth1
```

Scheduled regularly through cron or run manually, this script will check the current IP of the given network interface with that of the previous run. If different, a shell script will be called.

Currently that shell script (`update-ddns.sh`) calls the [Mythic Beasts](https://www.mythic-beasts.com/) [DDNS API v2](https://www.mythic-beasts.com/support/api/dnsv2/dynamic-dns) to update the dynamic IP stored in your account.

For this to work you **must** have account credentials stored in the default curl location: `~/.netrc`:
```
machine ipv4.api.mythic-beasts.com
login KEYID
password SECRET
```

You can obtain these values by [creating a new DDNS API key at Mythic Beasts](https://www.mythic-beasts.com/customer/api-users/create)

## Modification for other DDNS providers

Modify `update-ddns.sh` to update your preferred supplier's DDNS record for your domain.

