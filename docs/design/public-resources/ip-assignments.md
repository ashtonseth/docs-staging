# Public IP Address Assignments

## Overview

Documentation of public IPv4 and IPv6 address space allocated by ARIN and utilized in the homelab environment.

!!! abstract "Resource Summary"
    **IPv4 Allocation**: X.X.X.0/24 (256 addresses)  
    **IPv6 Allocation**: 2001:XXXX::/48 (65,536 /64 subnets)  
    **Registry**: ARIN (American Registry for Internet Numbers)  
    **Assignment Type**: End-Site / Direct Allocation

---

## IPv4 Allocation

### Block Information

| Attribute | Value |
|-----------|-------|
| **Prefix** | X.X.X.0/24 |
| **Netmask** | 255.255.255.0 |
| **Total IPs** | 256 addresses |
| **Usable IPs** | 254 addresses (excluding network/broadcast) |
| **Allocation Date** | [YYYY-MM-DD] |
| **Registry** | ARIN |
| **AS Origin** | AS[XXXXX] |

### WHOIS Information

```bash
# Query IP block information
whois -h whois.arin.net X.X.X.0/24

# Expected output:
NetRange:       X.X.X.0 - X.X.X.255
CIDR:           X.X.X.0/24
NetName:        [YOUR-NET-NAME]
NetHandle:      NET-X-X-X-0-1
Parent:         NET-X-0-0-0-0 (NET-X-0-0-0-1)
NetType:        Direct Allocation
OriginAS:       AS[XXXXX]
Organization:   [Your Organization] (ORGID-ARIN)
RegDate:        [YYYY-MM-DD]
Updated:        [YYYY-MM-DD]
```

### Address Utilization Plan

```
IPv4 Block: X.X.X.0/24 (256 total addresses)

├── X.X.X.0         - Network Address (Reserved)
├── X.X.X.1         - Primary Gateway / Router
├── X.X.X.2-9       - Network Infrastructure
│   ├── X.X.X.2     : Secondary Router (HA)
│   ├── X.X.X.3     : Primary DNS Server
│   ├── X.X.X.4     : Secondary DNS Server
│   ├── X.X.X.5     : Load Balancer VIP
│   └── X.X.X.6-9   : Reserved Infrastructure
│
├── X.X.X.10-29     - Web Services
│   ├── X.X.X.10    : Primary Web Server (web01.yourdomain.com)
│   ├── X.X.X.11    : Secondary Web Server (web02.yourdomain.com)
│   ├── X.X.X.15    : Reverse Proxy / CDN Origin
│   └── X.X.X.20    : Load Balancer for Web Tier
│
├── X.X.X.30-49     - Mail Services
│   ├── X.X.X.30    : Primary Mail Server (mail.yourdomain.com)
│   ├── X.X.X.31    : Secondary Mail Server
│   └── X.X.X.35    : Webmail Interface
│
├── X.X.X.50-99     - VPN & Remote Access
│   ├── X.X.X.50    : WireGuard VPN Server
│   ├── X.X.X.51    : OpenVPN Server
│   ├── X.X.X.52    : Site-to-Site VPN Gateway
│   └── X.X.X.60-99 : VPN User Pool
│
├── X.X.X.100-149   - Application Services
│   ├── X.X.X.100   : API Gateway
│   ├── X.X.X.110   : Database Public Interface (read-only)
│   ├── X.X.X.120   : Monitoring Dashboard (public)
│   └── X.X.X.130   : File Transfer Server
│
├── X.X.X.150-199   - DNS & Anycast Services
│   ├── X.X.X.150   : Authoritative DNS Server 1
│   ├── X.X.X.151   : Authoritative DNS Server 2
│   └── X.X.X.160   : Anycast Node (future)
│
├── X.X.X.200-249   - Reserved / Future Use
│   └── Available for expansion
│
├── X.X.X.250-254   - Network Management
│   ├── X.X.X.250   : Network Monitoring External Interface
│   ├── X.X.X.251   : Router Management (SSH)
│   └── X.X.X.252   : Emergency Access Interface
│
└── X.X.X.255       - Broadcast Address (Reserved)
```

### Current Utilization

<div class="grid cards" markdown>

-   **Allocated**
    
    ---
    
    **256 addresses** total  
    254 usable addresses

-   **Assigned**
    
    ---
    
    **115 addresses** in use  
    45% utilization

-   **Reserved**
    
    ---
    
    **50 addresses** reserved  
    Infrastructure & future

-   **Available**
    
    ---
    
    **89 addresses** free  
    35% available for growth

</div>

---

## IPv6 Allocation

### Block Information

| Attribute | Value |
|-----------|-------|
| **Prefix** | 2001:XXXX::/48 |
| **Block Size** | /48 (65,536 /64 subnets) |
| **Subnet Count** | 65,536 subnets |
| **Hosts per /64** | 18,446,744,073,709,551,616 |
| **Allocation Date** | [YYYY-MM-DD] |
| **Registry** | ARIN |
| **AS Origin** | AS[XXXXX] |

### WHOIS Information

```bash
# Query IPv6 block
whois -h whois.arin.net 2001:XXXX::/48

# Expected output:
NetRange:       2001:XXXX:0:0:0:0:0:0 - 2001:XXXX:0:FFFF:FFFF:FFFF:FFFF:FFFF
CIDR:           2001:XXXX::/48
NetName:        [YOUR-NET-NAME-V6]
NetHandle:      NET6-2001-XXXX-1
Parent:         NET6-2001-XX00-0-0 (NET6-2001-XX00-1)
NetType:        Direct Allocation
OriginAS:       AS[XXXXX]
Organization:   [Your Organization] (ORGID-ARIN)
```

### IPv6 Addressing Hierarchy

```
IPv6 Master Block: 2001:XXXX::/48 (65,536 /64 subnets)

Hierarchical Structure:
2001:XXXX:[SITE:FUNC:SUBNET]::/64

Where:
- SITE (8 bits): Physical or logical site identifier
- FUNC (4 bits): Function/service type
- SUBNET (4 bits): Subnet within function

Example Structure:

├── 2001:XXXX:0000::/52 - Primary Site Infrastructure
│   ├── 2001:XXXX:0000::/64 - Transit & Routing
│   ├── 2001:XXXX:0001::/64 - Management Network
│   ├── 2001:XXXX:0010::/64 - Web Services
│   ├── 2001:XXXX:0020::/64 - Mail Services
│   ├── 2001:XXXX:0030::/64 - VPN Services
│   └── 2001:XXXX:0040::/64 - DNS Services
│
├── 2001:XXXX:0100::/52 - Secondary Site (if applicable)
│   └── Similar structure
│
├── 2001:XXXX:1000::/52 - DMZ / Public Services
│   ├── 2001:XXXX:1000::/64 - Public Web Servers
│   ├── 2001:XXXX:1010::/64 - Public Mail Servers
│   └── 2001:XXXX:1020::/64 - Public DNS Servers
│
├── 2001:XXXX:2000::/52 - Internal Networks (Dual-Stack)
│   ├── 2001:XXXX:2000::/64 - User Network
│   ├── 2001:XXXX:2010::/64 - Server Network
│   └── 2001:XXXX:2020::/64 - Storage Network
│
└── 2001:XXXX:F000::/52 - Reserved / Future Use
    └── 61,440 /64 subnets available
```

### Current IPv6 Utilization

| Category | /64 Subnets Used | Percentage |
|----------|------------------|------------|
| **Infrastructure** | 5 | <0.01% |
| **Public Services** | 8 | 0.01% |
| **Internal Networks** | 12 | 0.02% |
| **Testing/Lab** | 3 | <0.01% |
| **Total Used** | 28 | 0.04% |
| **Available** | 65,508 | 99.96% |

!!! success "IPv6 Capacity"
    With a /48 allocation, there's effectively unlimited address space for any foreseeable homelab expansion, including multi-site deployments, extensive subnetting, and service segmentation.

---

## DNS Records

### Forward DNS Zones

#### Primary Domain (yourdomain.com)

```dns
; IPv4 A Records
@               IN  A       X.X.X.10
www             IN  A       X.X.X.10
mail            IN  A       X.X.X.30
vpn             IN  A       X.X.X.50
api             IN  A       X.X.X.100
ns1             IN  A       X.X.X.150
ns2             IN  A       X.X.X.151

; IPv6 AAAA Records
@               IN  AAAA    2001:XXXX:1000::10
www             IN  AAAA    2001:XXXX:1000::10
mail            IN  AAAA    2001:XXXX:1010::30
vpn             IN  AAAA    2001:XXXX:0030::50
api             IN  AAAA    2001:XXXX:1000::100
ns1             IN  AAAA    2001:XXXX:0040::150
ns2             IN  AAAA    2001:XXXX:0040::151

; Mail Exchange Records
@               IN  MX  10  mail.yourdomain.com.
@               IN  MX  20  mail-backup.yourdomain.com.

; Service Records
_imaps._tcp     IN  SRV  0 1 993 mail.yourdomain.com.
_submission._tcp IN SRV  0 1 587 mail.yourdomain.com.
```

### Reverse DNS Zones

#### IPv4 Reverse Zone (X.X.X.in-addr.arpa)

```dns
; X.X.X.in-addr.arpa
$ORIGIN X.X.X.in-addr.arpa.
$TTL 86400

@       IN  SOA ns1.yourdomain.com. hostmaster.yourdomain.com. (
            2024011501  ; Serial
            7200        ; Refresh
            3600        ; Retry
            1209600     ; Expire
            86400 )     ; Minimum

        IN  NS  ns1.yourdomain.com.
        IN  NS  ns2.yourdomain.com.

; PTR Records
1       IN  PTR router.yourdomain.com.
10      IN  PTR web01.yourdomain.com.
11      IN  PTR web02.yourdomain.com.
30      IN  PTR mail.yourdomain.com.
50      IN  PTR vpn.yourdomain.com.
100     IN  PTR api.yourdomain.com.
150     IN  PTR ns1.yourdomain.com.
151     IN  PTR ns2.yourdomain.com.
```

#### IPv6 Reverse Zone (X.X.X.X.1.0.0.2.ip6.arpa)

```dns
; X.X.X.X.1.0.0.2.ip6.arpa (delegated by ARIN)
$ORIGIN X.X.X.X.1.0.0.2.ip6.arpa.
$TTL 86400

@       IN  SOA ns1.yourdomain.com. hostmaster.yourdomain.com. (
            2024011501
            7200
            3600
            1209600
            86400 )

        IN  NS  ns1.yourdomain.com.
        IN  NS  ns2.yourdomain.com.

; PTR Records for key services
; Format: reverse nibbles of full IPv6 address
0.1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.1    IN  PTR web01.yourdomain.com.
0.3.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.1.0.1    IN  PTR mail.yourdomain.com.
```

---

## NAT Configuration

### Public-to-Private Mapping

#### 1:1 Static NAT (for specific services)

```cisco
! Static NAT for web server
ip nat inside source static 10.0.96.10 X.X.X.10

! Static NAT for mail server
ip nat inside source static 10.0.96.30 X.X.X.30

! Static NAT for VPN gateway
ip nat inside source static 10.0.97.50 X.X.X.50
```

#### Port Forwarding (PAT)

```cisco
! HTTP/HTTPS to internal web servers
ip nat inside source static tcp 10.0.96.10 80 X.X.X.10 80
ip nat inside source static tcp 10.0.96.10 443 X.X.X.10 443

! SMTP/IMAP/Submission to mail server
ip nat inside source static tcp 10.0.96.30 25 X.X.X.30 25
ip nat inside source static tcp 10.0.96.30 587 X.X.X.30 587
ip nat inside source static tcp 10.0.96.30 993 X.X.X.30 993

! WireGuard VPN
ip nat inside source static udp 10.0.97.50 51820 X.X.X.50 51820
```

### IPv6 (No NAT)

IPv6 uses direct end-to-end connectivity without NAT:

```cisco
! IPv6 firewall rules instead of NAT
ipv6 access-list IPV6-IN
 permit tcp any host 2001:XXXX:1000::10 eq 80
 permit tcp any host 2001:XXXX:1000::10 eq 443
 permit tcp any host 2001:XXXX:1010::30 eq 25
 permit tcp any host 2001:XXXX:1010::30 eq 587
 permit tcp any host 2001:XXXX:1010::30 eq 993
 deny ipv6 any any log
!
interface GigabitEthernet0/0
 description Internet Facing
 ipv6 traffic-filter IPV6-IN in
```

---

## Subnet Delegation

### Reverse DNS Delegation

ARIN delegated reverse DNS zones to personal nameservers:

**IPv4 Reverse**:
```
Zone: X.X.X.in-addr.arpa
Nameservers:
  - ns1.yourdomain.com (X.X.X.150)
  - ns2.yourdomain.com (X.X.X.151)
```

**IPv6 Reverse**:
```
Zone: X.X.X.X.1.0.0.2.ip6.arpa
Nameservers:
  - ns1.yourdomain.com (2001:XXXX:0040::150)
  - ns2.yourdomain.com (2001:XXXX:0040::151)
```

### Authoritative DNS Configuration

```bind
; BIND9 Configuration for Reverse Zones
zone "X.X.X.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.X.X.X.in-addr.arpa";
    allow-transfer { 
        X.X.X.151;           # Secondary NS
        2001:XXXX:0040::151; # Secondary NS IPv6
    };
    notify yes;
};

zone "X.X.X.X.1.0.0.2.ip6.arpa" {
    type master;
    file "/etc/bind/zones/db.2001.XXXX.ip6.arpa";
    allow-transfer { 
        X.X.X.151;
        2001:XXXX:0040::151;
    };
    notify yes;
};
```

---

## IP Reputation Management

### Email Deliverability

**SPF Record**:
```dns
yourdomain.com.  IN  TXT  "v=spf1 ip4:X.X.X.30 ip6:2001:XXXX:1010::30 -all"
```

**DKIM Configuration**:
```dns
default._domainkey.yourdomain.com.  IN  TXT  "v=DKIM1; k=rsa; p=MIGfMA0GCSq..."
```

**DMARC Policy**:
```dns
_dmarc.yourdomain.com.  IN  TXT  "v=DMARC1; p=quarantine; rua=mailto:dmarc@yourdomain.com"
```

### Blacklist Monitoring

Regular checks against common RBLs:
- Spamhaus (zen.spamhaus.org)
- Barracuda (b.barracudacentral.org)
- SORBS (dnsbl.sorbs.net)
- SpamCop (bl.spamcop.net)

```bash
# Check IP reputation
host X.X.X.30.zen.spamhaus.org
# Expected: NXDOMAIN (not listed)

# Automated monitoring
0 */6 * * * /usr/local/bin/check-rbl.sh X.X.X.30
```

---

## Security Considerations

### DDoS Protection

**Rate Limiting**:
```cisco
! Rate limit incoming connections
class-map match-all RATE-LIMIT-HTTP
 match access-group name HTTP-TRAFFIC

policy-map RATE-LIMIT-POLICY
 class RATE-LIMIT-HTTP
  police 10000000 bps conform-action transmit exceed-action drop

interface GigabitEthernet0/0
 service-policy input RATE-LIMIT-POLICY
```

**Geographic Filtering**:
```cisco
! Block traffic from specific countries (example)
ip access-list extended GEO-FILTER
 deny ip geoip country CN any
 deny ip geoip country RU any
 permit ip any any
```

### Abuse Contact

**WHOIS Abuse Contact**:
```
abuse@yourdomain.com
Phone: +1-XXX-XXX-XXXX
Response Time: 24-48 hours
```

---

## Cost Analysis

### Annual IP Address Fees

| Resource | Annual Fee | Notes |
|----------|-----------|-------|
| IPv4 /24 | $250-500 | ARIN maintenance fee |
| IPv6 /48 | Included | No additional charge |
| **Total** | **$250-500** | Based on organization size |

### Cost per IP

- **IPv4**: ~$1-2 per address per year
- **IPv6**: Effectively $0 (unlimited addresses)

### ROI Justification

**Professional Development Value**:
- Hands-on experience with public IP management
- Real-world DNS and email configuration
- Understanding of IP reputation and deliverability
- Direct applicability to enterprise email/web hosting

**Technical Capabilities**:
- Host public services without cloud providers
- Full control over DNS and reverse DNS
- Custom mail server configuration
- VPN and remote access solutions

---

## Related Documentation

- [ASN Allocation](asn-allocation.md) - Autonomous System Number
- [BGP Routing](bgp-routing.md) - BGP configuration and policies
- [RIR Documentation](rir-documentation.md) - ARIN procedures
- [IPv4 Hierarchy](../addressing/ipv4-hierarchy.md) - Internal addressing
- [IPv6 Strategy](../addressing/ipv6-strategy.md) - IPv6 deployment

---

*Last Updated: {{ git_revision_date_localized }}*