# Static Routing — Three Router Triangle Topology

## Overview
A three-router triangle topology built in Cisco Packet Tracer with full 
inter-LAN reachability using manually configured static routes.

## Topology
- Router0 ↔ Router1 (top link)
- Router0 ↔ Router2 (left link)
- Router1 ↔ Router2 (right link)
- Three LANs: one behind each router

## IP Addressing
| Device  | Interface | IP Address    | Subnet Mask       | Purpose          |
|---------|-----------|---------------|-------------------|------------------|
| Router0 | Gi0/0     | 192.168.1.1   | 255.255.255.0     | Blue LAN         |
| Router0 | Gi0/1     | 10.0.0.1      | 255.255.255.252   | Link to Router1  |
| Router0 | Gi0/2     | 10.0.0.5      | 255.255.255.252   | Link to Router2  |
| Router1 | Gi0/0     | 10.0.0.2      | 255.255.255.252   | Link to Router0  |
| Router1 | Gi0/1     | 192.168.2.1   | 255.255.255.0     | Green LAN        |
| Router1 | Gi0/2     | 10.0.0.9      | 255.255.255.252   | Link to Router2  |
| Router2 | Gi0/0     | 10.0.0.6      | 255.255.255.252   | Link to Router0  |
| Router2 | Gi0/1     | 10.0.0.10     | 255.255.255.252   | Link to Router1  |
| Router2 | Gi0/2     | 192.168.3.1   | 255.255.255.0     | Third LAN        |

## Static Routes Configured
**Router0**
ip route 192.168.2.0 255.255.255.0 10.0.0.2

ip route 192.168.3.0 255.255.255.0 10.0.0.6

**Router1**
ip route 192.168.1.0 255.255.255.0 10.0.0.1

ip route 192.168.3.0 255.255.255.0 10.0.0.10

**Router2**
ip route 192.168.1.0 255.255.255.0 10.0.0.5

ip route 192.168.2.0 255.255.255.0 10.0.0.9

## Errors Encountered
- **Bad mask /30 for address 10.0.0.3** — accidentally used the broadcast address of the first /30 block. Fixed by moving to the next block (10.0.0.4/30).
- **Overlapping subnet error** — tried assigning an address that fell inside an already configured interface range. Fixed by properly sizing each /30 block.

## What I Learned
- Every router only knows its own directly connected networks by default.
- Static routes have to be added manually on every router — both directions.
- Router-to-router links should use /30 subnets (only 2 usable addresses needed).
- `do show ip route` and `do show ip interface brief` are essential verification commands.
- The pain of manual static routing makes you genuinely appreciate why dynamic protocols like OSPF exist.

## Screenshots
<img width="1365" height="702" alt="Screenshot_2026-06-22_14-24-21" src="https://github.com/user-attachments/assets/e1919a02-2298-4cb7-87a5-673515725ec3" />
<img width="703" height="485" alt="Screenshot_2026-06-22_14-26-59" src="https://github.com/user-attachments/assets/8b4f43c1-0f07-471d-ba9c-e684fdaa4b4d" />
<img width="705" height="478" alt="Screenshot_2026-06-22_14-27-48" src="https://github.com/user-attachments/assets/e2f36775-2ea1-4f14-bd4e-98f61e8dba8d" />
<img width="705" height="484" alt="Screenshot_2026-06-22_14-28-45" src="https://github.com/user-attachments/assets/42cc8273-1849-4517-b233-b6d373982187" />




