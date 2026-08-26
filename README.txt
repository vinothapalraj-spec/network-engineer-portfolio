# DHCP Snooping - Cisco Packet Tracer Lab

## Project Overview

This lab demonstrates the configuration and verification of
DHCP Snooping on a Cisco Layer 2 switch.

The objective is to protect the network from unauthorized or
rogue DHCP servers.

## Objective

- Configure DHCP Snooping on a Cisco switch
- Enable DHCP Snooping for the required VLAN
- Configure the legitimate DHCP server interface as trusted
- Keep user-facing interfaces untrusted
- Verify DHCP Snooping operation
- Verify DHCP bindings
- Simulate a rogue DHCP server scenario
- Troubleshoot DHCP-related connectivity issues

## Network Topology

![Network Topology](images/topology.png)

## IP Addressing

| Device | IP Address | Role |
|---|---|---|
| DHCP Server | 192.168.1.2 | Legitimate DHCP Server |
| Rogue DHCP Server | 192.168.1.3 | Unauthorized DHCP Server |
| PC1 | DHCP | Client |
| PC2 | DHCP | Client |
| Default Gateway | 192.168.10.1 | Gateway |

## VLAN Configuration

| VLAN | Name | Purpose |
|---|---|---|
| 1 | USERS | User devices |

## Network Requirements

1. PC1 and PC2 should obtain IP addresses dynamically.
2. The legitimate DHCP server should provide DHCP services.
3. The legitimate DHCP server interface should be trusted.
4. User-facing switch ports should remain untrusted.
5. DHCP Snooping should protect VLAN 1 from rogue DHCP responses.

## Configuration

DHCP Snooping was enabled globally and for VLAN 1.

The interface connected to the legitimate DHCP server was
configured as a trusted interface.

User-facing interfaces were configured as untrusted.

DHCP rate limiting was also configured on access ports.

## Verification

### show ip dhcp snooping

![DHCP Snooping Status](images/dhcp-snooping-status.png)

### Show ip dhcp binding

![DHCP Binding Table](images/dhcp-binding.png)

### Client IP Address

![Client IP Address](images/client-ip.png)

## Troubleshooting Scenario

### Problem

A rogue DHCP server was connected to an untrusted switch port.

The rogue DHCP server attempted to provide DHCP responses
to network clients.

### Risk

Clients could receive incorrect:

- IP address
- Default gateway
- DNS information
- Network configuration

### Root Cause

An unauthorized DHCP server was connected to the user network.

### Solution

DHCP Snooping was enabled on the switch.

Only the interface connected to the legitimate DHCP server
was configured as trusted.

User-facing interfaces remained untrusted.

### Result

The legitimate DHCP server was allowed to provide DHCP
responses, while DHCP responses received through untrusted
interfaces were subject to DHCP Snooping validation.

## Verification Commands

```text
show ip dhcp snooping
show ip dhcp snooping binding
show vlan brief

