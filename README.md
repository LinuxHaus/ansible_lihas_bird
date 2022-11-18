# lihas_bird
## Role Name

Install and configure bird routing daemon

Currently supported protocols:
* bgp
* ospf
* static

Files managed by this role:
* `/etc/bird/bird_protocols_static.conf`
* `/etc/bird/bird_protocols_ospf.conf`
* `/etc/bird/bird.conf`

Additional files not managed by this role:
* `/etc/bird/bird_filters_*.conf`
* `/etc/bird/bird_templates_*.conf`
* `/etc/bird/bird_protocols_*.conf`
* `/etc/bird/bird_this_location.conf`

## Requirements
To run solo:

```
ansible-galaxy install -r requirements.yml
ansible-playbook -i localhost, bird.yml
```

## Role Variables

* bird.as: ASN
* bird.routerid
* bird.scantime
* bird.net_cix: []
* bird.static: []
    * static route annoucements
* bird.filter:
    * TODO: dictionary with filters consisting of lines 
* bird.filter.bgprouting: []
    * TODO: content of filter named bgprouting

