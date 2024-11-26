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

![(3)connections added](https://github.com/user-attachments/assets/02863713-bb14-432f-9f79-df35ff33375f)

##


