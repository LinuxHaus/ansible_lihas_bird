# lihas_bird
## Role Name

Install and configure bird routing daemon

Currently supported protocols:
* bgp
* ospf
* radv
* static

Files managed by this role:
* `bird_filters_ansible.conf`
* `/etc/bird/bird_filters_ansible.conf`
* `/etc/bird/bird_protocols_bgp.conf`
* `/etc/bird/bird_protocols_ospf.conf`
* `/etc/bird/bird_protocols_static.conf`
* `/etc/bird/bird_protocols_radv.conf`
* `/etc/bird/bird_debug.conf`
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

All the dictionbaries `%.config.bird:` are merged, in the end bird: is merged,

The result can be viewed in `/etc/bird/bird_debug.conf`

### global variables / defaults
* lihas_bird_version:
    * Bird version, default 1, set 2 for bird 2.x
    * bird1 is deprecated, new features are only available for bird2+
* bird.as: Default ASN
* `bird.ipv6_local`
    * Abgehende IPv6 für eigene Pakete
* bird.routerid
* bird_kernelmain
    * default true, use main kernel table
* bird.scantime
* bird.bfd.use: bfd on/off
    * Set global default for BFD
* bird.net_cix: []
### Functions
* bird.functions: bird2+ only
* bird.functions.X.header: []
    * Filter X, header lines
* bird.functions.X.parameters:
    * whatever is in the parameters definition of the function
* bird.functions.X.returntype:
    * return type, e.g. bool
* bird.functions.X.body: []
    * Filter X, bodylines
### Filters
* bird.filter: bird2+ only
* bird.filter.X.header: []
    * Filter X, header lines
* bird.filter.X.body: []
    * Filter X, bodylines
* bird.filter.X: []
    * simple filter X
### Protocol static
* bird.staticnamed.X.channel: ipv4 or ipv6, default ipv4
* bird.staticnamed.X.check_link: optional on/off
* bird.staticnamed.X.preference: optional route preference
* bird.staticnamed.X.table: optional alternative bird table
* bird.staticnamed.X.routes: []
    * list of routes
* bird.static: []
    * static ipv4 route annoucements, simple routes
* bird.static6: []
    * static ipv6 route annoucements, simple routes
### Protocol bgp
* bird.bgp: {}
    * BGP
* bird.bgp.X.as: ASN
* bird.bgp.X.import_filter: import filter
* bird.bgp.X.export_filter: export filter
* bird.bgp.X.import_filter6: import filter ipv6
* bird.bgp.X.export_filter6: export filter ipv6
* bird.bgp.X.bfd: bfd on/off
* bird.bgp.X.neighbor.ip: neighbor IPv4
* bird.bgp.X.neighbor.ip6: neighbor IPv6
* bird.bgp.X.neighbor.as: neighbor ASN
* bird.bgp.X.sourceip: IPv4
* bird.bgp.X.sourceip6: IPv6
* bird.bgp.X.extra: []
### Protocol ospf v2/v3
* bird.ospf: {}
    * Areas IPv4 OSPFv2
* bird.ospf.X.table: optional alternative bird table
* bird.ospf.X.preference: optional ospf preference
* bird.ospf.X.import_filter: import filter
* bird.ospf.X.export_filter: export filter
* bird.ospf.X.area: {}
* bird.ospf.X.area.X.interface: {}
    * Interfaces in Area
* bird.ospf.X.area.X.interface.X.cost:
    * cost
* bird.ospf3: {}
    * Areas IPv6 OSPFv3
* bird.ospf3.X.import_filter: import filter
* bird.ospf3.X.export_filter: export filter
* bird.ospf3.X.interface: {}
    * Interfaces in Area
* bird.ospf3.X.interface.X.cost:
    * cost
### Protocol radv
* bird.radv.X.interfaces: {}
    * Interfaces
* bird.radv.X.interfaces.X.prefix: []
* bird.radv.X.rdnss: []
* bird.radv.X.dnssl: []


