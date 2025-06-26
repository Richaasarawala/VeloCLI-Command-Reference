#	--lan_side_nat

##	Description
This command displays the configured LAN-side Network Address Translation (NAT) rules on the VeloCloud Edge. It shows rules for both Source NAT (SNAT) / Destination NAT (DNAT) and combined Source and Destination NAT. These rules are typically configured on the VeloCloud Orchestrator and dictate how private IP addresses on the LAN are translated to public IP addresses (or other private IP addresses) for traffic going towards the WAN or other segments, and vice-versa for incoming traffic.

##  Arguments (optional)
| Argument | Description |
|---|---|
| none | This command does not take any arguments. |

##  Example usage
```
example_com:velocli> debug --lan_side_nat
====================== Source or Destination NAT ====================
Type     Segment ID  Inside Cidr IP  Outside Cidr IP  Source Route  Destination Route  Identity  Force PAT  Hits
source            0   172.30.1.0/24      10.0.0.0/24           N/A                any         0       None     0


====================== Source and Destination NAT ====================
Segment ID   SrcInsideIp  SrcOutsideIp  DestInsideIp  DestOutsideIp  Identity  Force PAT  Hits
```

##  Field descriptions

The output is divided into two sections: "Source or Destination NAT" and "Source and Destination NAT".

###	Source or Destination NAT Table
| Column | Description |
|---|---|
| Type | Specifies the type of NAT rule, typically 'Source' for SNAT or 'Destination' for DNAT. |
| Segment ID | The identifier of the network segment to which this NAT rule applies. |
| Inside Cidr IP | The IP address (or CIDR block) on the internal (LAN) side of the network that is subject to NAT. |
| Outside Cidr IP | The IP address (or CIDR block) on the external (WAN or translated) side of the network. For SNAT, this is the translated source IP. For DNAT, this is the public IP that maps to an internal IP. |
| Source Route | Information related to the source routing for this NAT rule. |
| Destination Route | Information related to the destination routing for this NAT rule. |
| Identity | An identifier for the NAT rule or the entity it applies to. |
| Force PAT | Indicates whether Port Address Translation (PAT) is forcibly enabled for this rule (True/False or Yes/No). PAT allows multiple inside IP addresses to share a single outside IP address by using different port numbers. |
| Hits | The number of times this NAT rule has been matched by traffic. |

###	Source and Destination NAT Table
This table displays rules where both source and destination IP addresses are translated simultaneously.

| Column | Description |
|---|---|
| Segment ID | The identifier of the network segment to which this NAT rule applies. |
| SrcInsideIp | The original source IP address on the internal (LAN) side. |
| SrcOutsideIp | The translated source IP address on the external (WAN) side. |
| DestInsideIp | The translated destination IP address on the internal (LAN) side (after NAT). |
| DestOutsideIp | The original destination IP address on the external (WAN) side (before NAT). |
| Identity | An identifier for the NAT rule or the entity it applies to. |
| Force PAT | Indicates whether Port Address Translation (PAT) is forcibly enabled for this rule (True/False or Yes/No). |
| Hits | The number of times this NAT rule has been matched by traffic. |
