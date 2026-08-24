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
* `/etc/bird/bird_variables.conf`
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
### Variables / Constants
* bird.variables: {} bird2+ only
* bird.variables.KEY: VALUE
### Tables
* bird.tables.X.channel: new Kernel table X with channel ipv4/ipv6
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
If `bird.bgp.X.neighbor.ip` and `bird.bgp.X.neighbor.ip6` are defined creates two BGP session, one for IPv4 and IPv6 each.

If `bird.bgp.X.channel4` and `bird.bgp.X.channel6` are defined, but only one of `bird.bgp.X.neighbor.ip` and `bird.bgp.X.neighbor.ip6`, create a multiprotocol BGP session.

* bird.bgp: {}
    * BGP
* bird.bgp.X.as: ASN
* bird.bgp.X.bfd: bfd on/off
* bird.bgp.X.channel4.export_filter: default bird.bgp.X.export_filter
* bird.bgp.X.channel4.extra: list of extra lines ion section channel4 {}
* bird.bgp.X.channel4: If present, do IPv4 announcements even on IPv6 BGP, e.g. multiprotocol
* bird.bgp.X.channel4.import_filter: default bird.bgp.X.import_filter
* bird.bgp.X.channel6.export_filter: default bird.bgp.X.export_filter6
* bird.bgp.X.channel6.extra: list of extra lines ion section channel6 {}
* bird.bgp.X.channel6: If present, do IPv6 announcements even on IPv4 BGP, e.g. multiprotocol
* bird.bgp.X.channel6.import_filter: default bird.bgp.X.import_filter6
* bird.bgp.X.export_filter6: export filter ipv6
* bird.bgp.X.export_filter: export filter
* bird.bgp.X.extra: []
* bird.bgp.X.igptable: igp table if neeeded, default bird.igptable
* bird.bgp.X.import_filter6: import filter ipv6
* bird.bgp.X.import_filter: import filter
* bird.bgp.X.neighbor.as: neighbor ASN
* bird.bgp.X.neighbor.ip6: neighbor IPv6
* bird.bgp.X.neighbor.ip: neighbor IPv4
* bird.bgp.X.neighbor.port: port, default 179
* bird.bgp.X.password: bgp password if needed
* bird.bgp.X.routerid: router id, looks like IPv4-address
* bird.bgp.X.sourceip: IPv4 BGP
* bird.bgp.X.sourceip6: IPv6 BGP
* bird.bgp.X.sourceport: IPv4 source port
### Protocol kernel
* bird.kernel: {}
* bird.kernel.X.kernel_table: OS routing table to use, if set
* bird.kernel.X.table: Bird routing table to use, if set
* bird.kernel.X.graceful_restart: Use graceful restart yes/no
* bird.kernel.X.metric: Metric in routing table
* bird.kernel.X.scantime: Time between kernel roting table scans
* bird.kernel.X.channel: ipv4/ipv6
* bird.kernel.X.channel.import_filter
* bird.kernel.X.channel.export_filter

### Protocol ospf v2/v3
* bird.ospf: {}
    * Areas IPv4 OSPFv2 or OSPFv3
* bird.ospf.X.version: v2 or v3, default v2
* bird.ospf.X.table: optional alternative bird table
* bird.ospf.X.preference: optional ospf preference
* bird.ospf.X.import_filter: import filter
* bird.ospf.X.export_filter: export filter
* bird.ospf.X.neighbors: []
    * Neighbors if needed
* bird.ospf.X.ecmp: Use ecmp, default no
* bird.ospf.X.area: {}
* bird.ospf.X.area.X.interface: {}
    * Interfaces in Area
* bird.ospf.X.area.X.interface.X.cost:
    * cost
* bird.ospf.X.area.X.interface.X.ecmp_weight
* bird.ospf.X.area.X.interface.X.authentication
* bird.ospf.X.area.X.interface.X.password
* bird.ospf.X.area.X.external: []
    * external networks, devault 0.0.0.0/0 or ::/0 matching v2/v3
* bird.ospf3: {}
    * Areas IPv6 OSPFv3
* bird.ospf3.X.import_filter: import filter
* bird.ospf3.X.export_filter: export filter
* bird.ospf3.X.interface: {}
    * Interfaces in Area
* bird.ospf3.X.interface.X.cost:
    * cost
### Protocol pipe
* bird.pipe.X: Pipe X
* bird.pipe.X.table: table
* bird.pipe.X.peer_table: peer table
* bird.pipe.X.import_filter: import filter
* bird.pipe.X.export_filter: export filter

### Protocol radv
* bird.radv.X.interfaces: {}
    * Interfaces
* bird.radv.X.interfaces.X.prefix: []
* bird.radv.X.rdnss: []
* bird.radv.X.dnssl: []


