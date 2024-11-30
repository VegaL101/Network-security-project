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

After doing this step on both of our routers our connection lights change from orange to green.

![(5)afteren](https://github.com/user-attachments/assets/fe54139e-c988-4291-93e9-3fa5ab68b7d2)

##


