# Network-security-project

## Objective

Our objective is to simulate a network in a 3 floor office building with three VLANs, with one switch per floor. wWhile enhancing their security posture through the implementation of firewalls and DMZs (Demilitarized Zones).

### Skills Learned

- Learned how to implement VLANs
- configure firewalls
- Configure DMZ

## Steps

Step 1:
Create the network layout

Firstly we add our two routers with 3 switches for each router. We set up our layout like below.
 
![(1)routerswitcheslayout](https://github.com/user-attachments/assets/94e0821f-c7b9-4cb4-bcca-58cfeaf37cfd)


##

We then add our end devices. we'll only be using PCs for this project. There will be 9 PCs in total, 3 for each switch on each floor. We have them set up like below.


 ![(2)add all end devices](https://github.com/user-attachments/assets/aee8ca2e-60d7-4ad0-b660-0b77d20bc941)


##

Here, I have made all the connections for all the devices and oranized all the PCs into deparments. There will be one pc for every department on each floor. the connections go like this:<br>
Site 1 router Gig 0/0 to Core switch 1 Gig 0/1<br>
Main switch fa 0/1 to (s1) Floor 1 switch Gig 0/1<br>
Main switch fa 0/2 to (s1) Floor 2 switch Gig 0/1<br>
Main switch fa 0/3 to (s1) Floor 3 switch Gig 0/1<br>

Every PC in the accounting department will be connected to port fa 0/1 of every switch on their floor.<br>
All the PCs in Sales will be connected to fa 0/2 for every switch.<br>
Lastly, the Delivery PCs will be connected to fa 0/3 on each switch.

i added some color to the layout to help organize things.

![(3)connections added](https://github.com/user-attachments/assets/0e08d06f-6b36-4ac8-96e9-23fc6f0d2d69)



##

As you have probably noticed by now all the light connections are lit up green except the routers to core switches. Here we enable both of our routers essentially turning them on. below we type in the following code to do so:

#Router>en (enable)<br>
#Router#config t (configure terminal)<br>
#Router (config)#int gig0/0 (the connection to our core switch)<br>
#Router (config-if)#no shutdown (turns on interface)<br> 
#do wr (saves our changes)<br>
#Router(config-if)#exit 

![(4)router enables](https://github.com/user-attachments/assets/5d944e46-fdc5-4c39-a8d3-aa7e277afe0a)

##

After doing this step the orange dots from our routers will turn into green flashing triangles letting us know our router is activated. You will also notice that i have added our VLANS down below. <BR>

For accounting we have VLAN 10: 192.168.10.0 <BR>
For sales we have VLAN 20: 192.168.20.0<BR>
And for delivery VLAN 30: 192.168.30.0<br>

![(5 5)vlans added](https://github.com/user-attachments/assets/75e18e52-107e-4ddb-b27c-1dcbc8c0b881)

##

Step 2:
Configure our devices.

In this step we be configuring our routers, switches, and end-devices.

##

First we'll start with our routers. We click on our router and head over to the cli tab. Here we create Subinterfaces for each of our VLANS and then assigning them a ip address.<br>

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
#exit<br>
#do wr<br>
#exit

## 

After making those changes we can now double check that the sub interfaces are asigned properly and are up. <br>
We do this by typing in:

#en<br>
#show ip interface brief

Down below you'll see an example of what it should look like if completed.

![(8)ipbrief](https://github.com/user-attachments/assets/2794b869-793a-4beb-adec-f251e5f10a6e)

##

Next, we create our VLANs on our main switch connected to our router. We head over to the CLI tab. Here we type the following commands.<br>

For accounting:<br>
#en<br>
#config t<br>
#vlan 10<br> 
#name accounting<br>

![(9)accountingvlan](https://github.com/user-attachments/assets/258cb7f6-a2ab-41f1-9d3b-cdc61645c2e5)

For sales:<br>
#en<br>
#config t<br>
#vlan 20<br> 
#name sales<br>

![(10)sales vlan](https://github.com/user-attachments/assets/5c5c9419-809a-413a-be58-0309b4bda32a)

For delivery:<br>
#en<br>
#config t<br>
#vlan 30<br> 
#name delivery<br>
#exit
#do wr

![(11)delivery vlan](https://github.com/user-attachments/assets/aeb1c39a-b0fc-45c6-baad-8d12e261cf82)

you will wat to make sure all these configurations we are making are also being saved(#do wr).

##

Then we will be enabling trunk mode on our main switch which would allow our us to extend VLANs across the entire network. To do this we type:<rb>
#en<br>
#config t<br>
#interface range fa 0/1-3<br>
#switchport mode trunk<br>

After this, the states of the interfaces will go down but back up right after as seen below.

![(13)switchport mode trunk](https://github.com/user-attachments/assets/c218cd0f-9f57-4e60-a318-5797c23ceb79)

make sure we exit and save our changes.

##

Next we check our VLANs, to do so we type: show vlan brief 

![(14)vlan brief after trunk](https://github.com/user-attachments/assets/f6d679bd-710a-41cd-8135-42615ee7e87c)

here we can see that our fa ports 1-3 are no longer on the active list. But, if we type: show interface trunk

![(15)show interfacestrunk](https://github.com/user-attachments/assets/f4c62460-35f6-456c-aaa6-25500ed90991)

You will see that our ports are there and our vlans that are allowed and active on the trunk are also there.

##

Next, on every floor switch we will create our vlans. we go to our switch and type:<br>
#en<br>
#config t<br>
#vlan 10<br>
#name accounting<br>
#vlan 20<br>
#name sales<br>
#vlan 30<br>
#name delivery<br>
#exit<br>
#do wr<br>

You can see an example down below. We do this to every switch on each floor.

![(16)switchvlanscreation](https://github.com/user-attachments/assets/f511e3d5-4ff0-4593-8cd5-d11b7eca4251)

Next, to check if our vlans were sucessfully created we type: <br>
show vlan brief

if done correctly we should see our vlans appear. You can see my example below 

![(17)show vlan brief](https://github.com/user-attachments/assets/3005cd75-ccd8-4193-97bd-fa02473736cc)

##

Now, we move onto assigning our vlans to their ports. We do this for every switch on each floor. We type: <br>
#en<br>
#config t<br>
#interface fa 0/1<br>
#switchport mode access<br>
#switchport access vlan 10<br>
#exit<br>
#do wr<br>
#interface fa 0/2<br>
#switchport mode access<br>
#switchport access vlan 20<br>
#exit<br>
#do wr<br>#interface fa 0/3<br>
#switchport mode access<br>
#switchport access vlan 30<br>
#exit<br>
#do wr<br>

Like below.

![(19)switch2vlansports](https://github.com/user-attachments/assets/7904952f-74da-4fd4-922b-56b7d8c5629c)

We have fa 0/1 for our accounting vlan, fa 0/2 for sales, and fa 0/3 for delivery. This means those specific ports can only be used by their respective vlans.

##

we check this by typing: #show vlan brief<br>

Below we can see each vlan we previously created have the ports they were assigned to next to them. We do this for every floor switch on each site 


![(20)vlanbriefs2](https://github.com/user-attachments/assets/863e3bcc-81d1-4f75-9802-52f4f4a9b788)

##

Next, we wil move to IP configurations on our PCs.

First we will be on PC0, click on the 'Desktop' table and head over to IP configuration. For this project will be setting using a static IPV4 addres.

For my IPv4 Address i set it to: 192.168.10.4 (this will be the address for this device)

For Subnet Mask i gave it: 255.255.255.0 ()

For Default Gateway i set it as: 192.168.10.1

It should look similar to below 

![(28 5)switchaddedandupdated look](https://github.com/user-attachments/assets/0278cc80-6a0e-492a-aa26-9437de6c42a0)

Now i will be configuring PC3 for its IPv4 Address i set it to: 192.168.10.5 (this will be the address for this device)

For Subnet Mask i gave it: 255.255.255.0 ()

For Default Gateway i set it as: 192.168.10.1

It should look similar to below 

![(22)pc3ipconfig](https://github.com/user-attachments/assets/0bf90c22-19c2-4533-be53-a877f668916b)

##

Here we check if PC3 can communicate with PC0. To do this, on PC3 we head over to the desktop tab enter the command promnpt. We type:<br>
ping 192.168.10.4

after doing so we should get a reply from PC0 tellling us that we did indeed configure our PCs correctly and they have successfully communicated with each other. The reply should look similar to the image below.

![(23)pc3pingpc0](https://github.com/user-attachments/assets/1ad382e0-d885-4263-9c2e-51048a6c2660)

##









