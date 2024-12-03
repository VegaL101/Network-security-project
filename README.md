# Network-security-project

## Objective

Our objective is to simulate two networks separated by three VLANs per site, while enhancing their security posture through the implementation of firewalls, DMZs (Demilitarized Zones), and site-to-site VPNs. 

### Skills Learned

- Learned how to implement VLANs
- configure firewalls
- Configure DMZ
- Configure site-to-site VPN

## Steps

Step 1:
Create the network layout

Firstly we add our two routers with 3 switches for each router. We set up our layout like below.
 
![(1)routerswitcheslayout](https://github.com/user-attachments/assets/855dfab8-c967-434a-8cbb-6ae8581f033b)

##

We then add our end devices. we'll only be using PCs for this project. There will be 12 PCs in total, 3 for a switch on each floor. We have them set up like below.

![(2)add all end devices](https://github.com/user-attachments/assets/90da6bad-c85d-4433-b8a0-25b887320e75)


##

Here, I have made all the connections for all the devices and oranized all the PCs into deparments. There will be one pc for every department on each floor. the connections go like this:<br>
Site 1 router Gig 0/0 to Core switch 1 Gig 0/1<br>
Core switch fa 0/1 to (s1) Floor 1 switch Gig 0/1<br>
Core switch fa 0/2 to (s1) Floor 2 switch Gig 0/1<br>
Core switch fa 0/3 to (s1) Floor 3 switch Gig 0/1<br>

Every PC in the accounting department will be connected to fa 0/1 of every switch that is on their floor.<br>
All the PCs in Sales will be connected to fa 0/2for their switch.<br>
And then the Delivery PCs will be connected to fa 0/3 on their respective floor.

i added some color to the layout to help organize things.

![(3)connections added](https://github.com/user-attachments/assets/1e699768-2e36-41b1-82bd-95d7e006eea1)


##

As you have probably noticed by now all the light connections are lit up green except the routers to core switches. Here we enable both of our routers essentially turning them on. below we type in the following code to do so:

Router>en (enable)
Router#config t (configure terminal)
Router (config)#int gig0/0 (the connection to our core switch)
Router (config-if)#no shutdown (turns on interface) 
do wr (saves our changes)
Router(config-if)#exit 

![(4)router enables](https://github.com/user-attachments/assets/5d944e46-fdc5-4c39-a8d3-aa7e277afe0a)

##

After doing this step the orange dots from our routers will turn into green flashing triangles letting us know our router is activated. You will also notice that i have added our VLANS down below. <BR>

For accounting we have VLAN 10: 192.168.10.0 <BR>
For sales we have VLAN 20: 192.168.20.0<BR>
And for delivery VLAN 30: 192.168.30.0

![(5 5)vlans added](https://github.com/user-attachments/assets/416c9c79-5b8f-4374-b0d8-1a012b623361)


##

Step 2:
Configure our devices.

In this step we be configuring our routers, switches, and end-devices.

##

First we'll start with our routers. We click on our Site 1 router and head over to the cli tab. Here we be creating Subinterfaces for each of our VLANS and then assigning them a ip address.<br>

Below we have created and assigned our interface for VLAN 10. We did this by typing in:

#en<br>
#config t<br>
#interface gig0/0.10<br>
#encapsulation dot1Q 10<br>
#ip address 192.168.10.1 255.255.255.0<br>
#exit

![(7)VLAN router10](https://github.com/user-attachments/assets/dba0d86d-2522-44e8-8f64-c6bce489649d)

So, after configuring our router for VLAN 10 we proceed to do this with VLAN 20 and 30. 

For VLAN 20:

#en<br>
#config t<br>
#interface gig0/0.20<br>
#encapsulation dot1Q 20<br>
#ip address 192.168.20.1 255.255.255.0<br>
#exit

For VLAN 30:

#en<br>
#config t<br>
#interface gig0/0.30<br>
#encapsulation dot1Q 30<br>
#ip address 192.168.30.1 255.255.255.0<br>
#exit

## 

For site router 2 we will be using the next available IPS in the VLANs to assign to our subinterfaces.

For VLAN 10:

#en<br>
#config t<br>
#interface gig0/0.10<br>
#encapsulation dot1Q 10<br>
#ip address 192.168.10.2 255.255.255.0<br>
#exit

VLAN 20:

#en<br>
#config t<br>
#interface gig0/0.20<br>
#encapsulation dot1Q 10<br>
#ip address 192.168.20.2 255.255.255.0<br>
#exit

VLAN 30:

#en<br>
#config t<br>
#interface gig0/0.30<br>
#encapsulation dot1Q 30<br>
#ip address 192.168.30.2 255.255.255.0<br>
#exit
