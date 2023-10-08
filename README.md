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
* `bird.ipv6_local`
    * Abgehende IPv6 für eigene Pakete
* bird.routerid
* bird_kernelmain
    * default true, use main kernel table
* bird.scantime
* bird.net_cix: []
* bird.static: []
    * static ipv4 route annoucements
* bird.static6: []
    * static ipv6 route annoucements
* bird.filter:
    * TODO: dictionary with filters consisting of lines 
* bird.filter.bgprouting: []
    * TODO: content of filter named bgprouting
* %.config.bird.ospf: {}
    * Areas IPv4 OSPFv2
* %.config.bird.ospf.X.import_filter: import filter
* %.config.bird.ospf.X.export_filter: export filter
* %.config.bird.ospf.X.interface: {}
    * Interfaces in Area
* %.config.bird.ospf.X.interface.X.cost:
    * cost
* %.config.bird.ospf3: {}
    * Areas IPv6 OSPFv3
* %.config.bird.ospf3.X.import_filter: import filter
* %.config.bird.ospf3.X.export_filter: export filter
* %.config.bird.ospf3.X.interface: {}
    * Interfaces in Area
* %.config.bird.ospf3.X.interface.X.cost:
    * cost

