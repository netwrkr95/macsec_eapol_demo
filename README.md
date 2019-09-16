## Using Ansible to Quickly Modify WAN MACsec Configurations in Cisco IOS-XE 

This demonstration offers simplified Ansible playbooks to accelerate the demonstration of new enhancements for those customers running WAN MACsec in Cisco IOS-XE solutions.  The content included in this repo offers a vast amount of dynamically adding/modifying/deleting WAN MACsec functionality commands, including key-exchange transport, enabling MACsec on the interface, as well as modifying key-chain rollover timers.  While there are multiple capabilities available, the focus is specicially around the key initiation enhancements Cisco has in their WAN MACsec solution, specifically around EAPoL commands that enhance key exchange seamlessly over any form of public Ethernet transport provider. [1]

### What is WAN MACsec

To gather a more in-depth understanding of WAN MACsec, how it benefits network designs, and key areas operators should be understanding, see key reference material below [2] that will aid in understanding the vital concept for securing high speed data networks.


### Overview and Use Case

The purpose of this demonstration is to leverage Ansible to automate the enabling of certain WAN MACsec commands in IOS-XE to show a "before" and "after" affect of key features and capabilities of the Cisco IOS-XE solution.  The original purpose of the demo is demonstrating the before/after of enabling/disabling certain EAPoL commands that allow MACsec to run over public Ethernet Metro providers, allowing mandatory key-exchange processes for MACsec, before any traffic can be transfered between two or more end-points (routers).  In this demonstration, the operator can quickly enable these commands and view connectivity before/after, via an Ansible playbook.  Prior to these EAPoL enhancements and before these commands were introduced, end-points running MACsec over public providers and certain layer-2 switching elements, were not able to set up the necessary connections using the MACsec Key Agreement (MKA) protocol.  These playbooks allow the operator to quickly enable (or delete) the necessary commands (posted below in the demonstation example) to enable this EAPoL enhancements.  

#### vManage Policy Example

Below is an example of the two primary enhancement commands to the EAPoL key exchange transport:

```
interface TenGigabitEthernet0/0/0
...
 eapol destination-address broadcast-address
 eapol eth-type 876F
 ...
 macsec
!
```
The first of these commands, the "eapol destination-address broadcast-address" command, allows the EAPoL destination MAC address to be modified, using a broadcast address.  This allows the Layer-2 transport network to treat the EAPoL traffic as a standard broadcast type packet, and more importantly, flooding it to all receivers. The second command, "eapol eth-type 876F", modifies the ether-type of the EAPoL frame to an ether-type that is not "well known" encoding, changing the behavior of how the public Ethernet transport, in essence, ignoring this ether-type for the key-exchange process. The "macsec" command simply enables MACsec on that interface.

It should be noted that not all Ethernet transports and/or provider backbone bridges react on EAPoL related identifiers, specifically MAC address or ether-types, so in these cases, the operator can ignore enabling these commands on the MACsec interface.  As a best practice, these EAPoL commands are recommended, as it provides a deterministic MAC address/ether-type for the EAPoL packets that are ingnored by all transports and bridges/switches.


#### Getting Started

This demonstration is leveraging the following version of code:

```
IOS-XE = 16.6.2
Ansible = version 2.6.12
```

#### References

[1] Cisco IOS-XE EAPoL Documentation: https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/macsec/configuration/xe-3s/macsec-xe-3s-book.html#task_1573E9C7150F4451981F493D0B7859CB

[2] WAN MACsec Overview - White Paper:  https://www.cisco.com/c/dam/en/us/td/docs/solutions/Enterprise/Security/MACsec/WP-High-Speed-WAN-Encrypt-MACsec.pdf 




