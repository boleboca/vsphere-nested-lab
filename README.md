# vsphere-nested-lab
Nested ESXi 7.0 home-lab build and notes.
# vSphere Nested Lab

Nested ESXi 7.0.3 lab built on an isolated network for practicing vSphere.

## Lab design
- Isolated standard vSwitch, no uplink, promiscuous mode / MAC changes / forged transmits set to Accept
- Nested ESXi VM: 4 vCPU, 16 GB RAM, 40 GB OS disk + 100 GB data disk (thin)
- Management VM: Windows Server 2019 (Desktop Experience), static IP 192.168.99.10
- Nested ESXi management IP: 192.168.99.11/24, no gateway

## Build steps
1. Isolated network
2. Nested ESXi VM (hardware virtualization exposed to guest)
3. ESXi install
4. Management IP in the DCUI
5. Management VM and browser
6. VMFS datastore
7. Test VMs, port groups and VLAN tags, snapshots

## Problems and fixes
- Installer saw no disk: the LSI Logic Parallel controller isn't supported by ESXi 7, so I switched to VMware Paravirtual.
- Server Core got installed: I picked the wrong edition. Reinstall with Desktop Experience.
- IE11 can't render the ESXi Host Client: I installed Chrome from an offline MSI via an ISO.
- DHCP lookup failed on the isolated network: expected, so I set a static IP.

