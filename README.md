# dnsmasq-restarter
Watch for changes in /etc/dnsmasq.d/ and restart dnsmasq accordingly in a time-coalesced fashion

## Why you need it

Let's say you have a dnsmasq server and you allow other admins to perform changes [via SFTP for example] to custom dnsmasq files such as /etc/dnsmasq.d/block or /etc/dnsmasq.d/hijack with some custom rules to perform DNS poisoning [don't get me started on such practice - but they'll ask you to do so eventually if you work for anyone but yourself] and you need dnsmasq to gracefully restart after every edit, but only once [without restarting it a thousand times in a minute if they make a thousand changes].

## How it works

It watches for changes in the /etc/dnsmasq.d/ directory and schedules a dnsmasq restart between 60 and 120 seconds after the initial and last edit are performed.

## Installation [as root] [tested on ubuntu 16.04]

```
apt update
apt -y install git
git clone https://github.com/nikksno/dnsmasq-restarter
```
```
mkdir scripts
mv dnsmasq-restarter/script scripts/dnsmasq-restarter
```

Add this to your crontab [```crontab -e``` and copy paste]
```
@reboot scripts/dnsmasq-restarter/script.sh
````
