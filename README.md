# NETWORK-new-office-build-configuration

![2024-10-07 21_59_30-New Office - GNS3](https://github.com/user-attachments/assets/70044d9e-96c6-4cae-8ab9-4a6c1c34f4ca)

We've been tasked with setting up a brand-new office we want to keep online 24/7. First is Layer 2 management & network maintenance. Once we've enabled LLDP to help identify Devices's capabilities later, We then created vlans to segment how data is transferred so their fewer chances of it being eavesdropped & Vlan 3 itself has a management interface on each switch enabled so we remote into those later. since we're introducing Vlans, we implemented MSTP so each of them will have an better idea on what path to choose. Just to be safe no random
switch overwrites all the others one day, we also set VTP to transparent mode. finally, it is only a matter of setting up the trunk and assigning ports to its intended segments.

![image](https://github.com/user-attachments/assets/22d4f0de-d2ac-4452-b1eb-6f81a33a09b8)

see video for [complete layer 2 setup](https://www.linkedin.com/posts/xaviar-cordova_ccnp-lab-1-part-1-layer-2-in-this-project-activity-7049029223138684928-3dPh?)

Let's now began with IP routing &services. As a GNS3’s VM, technically our gateway of last resort is our home network that act as a WAN as we’ll enable NAT overload that'll keep our network separate. This site is one of many,which after setting up OSPF & assigning it under area 5 it'll allow all current and future locations to ability to learn & reach it later. Once we set the ACL rule & specify the in/outgress interfaces for NATing, We’ll setup a standby router using VRRP so in case a router fails, the other one will take control. We want the OSPF to use router 1 as the default best path so we changed the metric for the standby (in this case since we're not connected to an ABR we're
pretending it'll process on it). We wanted a Window server to hand out DHCP leases, so we set the Helper address to 10.0.3.254 right after enabling the sub-interfaces for the VLANs.

![2024-10-07 22_33_33-Post _ Feed _ LinkedIn](https://github.com/user-attachments/assets/85f5909f-0b17-4a72-a9c6-e4e38a1daa73)

see video [complete routing setup](https://www.linkedin.com/posts/xaviar-cordova_ccnp-lab-1-part-2-routing-setup-we-can-activity-7053586788103188480-2qJp?)

As I've mentioned this new Office becoming apart of the Enterprise's network, this would be currently the configured OSPF environment and a new ABR would be needed and a new area assigned to. This is a separate project where it was created prior, the route summarized in the backbone, and all set to route to area 0 as their default gateway route for the ISP's network![image](https://github.com/user-attachments/assets/ee3bd9ce-b7cc-4b9a-8822-c920eeb84d77)
[Tthis last video is to audit it configuration](https://www.linkedin.com/posts/xaviar-cordova_ccnp-lab-2-ospf-multi-area-activity-7062887970281816064-bRIT?)
 
