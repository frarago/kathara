Bundle completo (lab.conf + *.startup + cartelle /etc/frr + pagine web)

Scelta chiave per il tuo errore su 'vtep5010':
- Nel lab VXLAN Kathara il VTEP IP è una loopback /32 (lo) e bgpd.conf redistribuisce SOLO la loopback:
  route-map LOOPBACKS ... match interface lo
  Quindi qui i leaf.startup creano 192.168.0.1/32, .2/32, .3/32 su lo e creano vtep5010 con local = 192.168.0.x.

Cosa controllare se 'ip -d link show vtep5010' fallisce:
- che il file leafX.startup esista e sia eseguibile
- che il device si chiami esattamente leaf1/leaf2/leaf3 in lab.conf
- che nel leaf non ci sia errore di sintassi (es. 'bridge' command non trovato)

Origine template (dal tuo Kathara-Labs.zip):
- daemons VXLAN: main-labs/data-center-routing/data-center-vxlan/.../leaf_1_0_1/etc/frr/daemons
- stile leaf.startup VXLAN (loopback+vtep+br100+vlan_filtering): leaf_1_0_1.startup
- daemons/vtysh BGP edge: main-labs/interdomain-routing/frr/bgp-simple-peering/.../router1/etc/frr/
