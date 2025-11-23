# NETWORK-new-office-build-configuration


![image](https://github.com/user-attachments/assets/f5de322a-6624-4c03-838d-f776abc51112)

We've been tasked with setting up a brand-new office we want to keep online 24/7. First is Layer 2 management & network maintenance. Once we've enabled LLDP to help identify
Devices' capabilities later, We then created VLANs to segment how data is transferred so there is fewer chances of it being eavesdropped & Vlan 3 itself has been set with a management interface enabled on each switch so we can SSH remote into those later. since we're introducing Vlans, we implemented MSTP so each of them will have a better idea on what paths to choose, but kept all vlan in group 0 for now. Just to be safe no random Cisco switch overwrites all the others one day, we also set VTP to transparent mode. finally, it is only a matter of setting up the trunk and assigning ports to its intended segments.


![Layer 2 Config](https://github.com/user-attachments/assets/4b93fd98-5f6a-465f-aa07-ddd1a1992d60)


See video for [complete layer 2 setup](https://www.linkedin.com/posts/xaviar-cordova_ccnp-lab-1-part-1-layer-2-in-this-project-activity-7049029223138684928-3dPh?)

Let's now begin with IP routing & services. As a GNS3’s VM, technically our gateway of last resort is our home network that acts as a WAN as we’ll enable NAT overload that'll keep our network separate. This site is one of many, which after setting up OSPF & assigning it under area 5 it'll allow all current and future locations the ability to learn & reach it later. Once we set the ACL rule & specify the in/outgress interfaces for NATing, We’ll setup a standby router using VRRP so in case a router fails, the other one will take control. We want the OSPF to use router 1 as the default best path so we changed the metric for the standby (in this case since we're not connected to an ABR we're
pretending it'll process on it). We wanted a Window server to hand out DHCP leases, so we set the Helper address to 10.0.3.254 right after enabling the sub-interfaces for the VLANs.


![2024-11-10 01_19_53-CSR1000v-1](https://github.com/user-attachments/assets/fe6aa377-e396-4a61-b5bd-eeb899da9148)
![2024-11-10 14_30_13-QEMU (PC-3) - TightVNC Viewer](https://github.com/user-attachments/assets/b2c08fa1-0ff4-4374-ad13-d41aedaa8154)

See video for [complete routing setup](https://www.linkedin.com/posts/xaviar-cordova_ccnp-lab-1-part-2-routing-setup-we-can-activity-7053586788103188480-2qJp?)

As I've mentioned this new Office becoming apart of the Enterprise's network, this would be currently the configured OSPF environment and a new ABR would be needed and a new area assigned to. This is a separate project where it was created prior, the route summarized in the backbone, and all set to route to area 0 as their default gateway route for the ISP's network

![2024-11-09 22_23_46-OSPF locations - GNS3](https://github.com/user-attachments/assets/4329bfcc-1b7c-44dc-a49e-1ded173d3c8f)

[This last video is to audit it configuration and test it functionality](https://www.linkedin.com/posts/xaviar-cordova_ccnp-lab-2-ospf-multi-area-activity-7062887970281816064-bRIT?)
 
