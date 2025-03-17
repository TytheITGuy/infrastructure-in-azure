<p align="center">
<img src="https://i.imgur.com/aMMGyHQ.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Preparing Active Directory Infrastructure in Azure</h1>


<h2>Description</h2>
In this project I create two VMs (Virtual Machines), one running Windows Server, to act as a Domain Controller. The other VM will act as a client, running Windows 10 that will join the domain. In later projects I will deploy AD, run a script that will create users in the domain, which I can log into from the client VM, then manage the accounts and update the group policies, all to simulate a real life IT environment!  <br/>
<br />


<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>


<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10</b>

<h2>Project Walk-through:</h2>

<p align="center">
Navigate to Microsoft Azure and create a resource group: 

![1-Creating Resource Group](https://github.com/user-attachments/assets/3111fb89-54ba-41f7-9862-022c8caa0580)

<p align="center">
Next, create a virtual network like so: 

![2- Creating a Virtual Network](https://github.com/user-attachments/assets/f86b7bd5-84f4-49bf-bd99-bd9ef8a32041)

<p align="center">
Once my resource group and network is created, I'll create and set up the virtual machine that will act as our Domain Controller. For the image, make sure you use Windows Server:  <br/>

![3-Creating the Virtual Machine](https://github.com/user-attachments/assets/aa31d8c3-141d-438d-aad0-12da4eeda1cf)


![4- Creating the Virtual Machine Part 2](https://github.com/user-attachments/assets/67524106-5249-454f-b3c3-48a72074b0ac)


Now, I'll create another VM that will serve as the client. The image for this machine should be Windows 10, NOT Windows Server like I did for the previous machine:  

![5- Creating the client virtual machine](https://github.com/user-attachments/assets/9a1f4a12-2021-4f7d-a25e-02649c27c545)

I now need to set DC-1 (Domain Controller) private IP address to "static" as by default it is set to "dynamic". I want this to be static, because this DC will double as a DNS (Domain Name System) server, which I will tell our client to use as a DNS server later. If the IP allocation setting were set to dynamic, the IP address could change leaving the DNS configuration of our client invalid. So, I'll go to the network settings of the DC and switch the IP allocation to static:  

![6- dc-1 overview](https://github.com/user-attachments/assets/db2cfe66-e6da-42ff-91d0-9be949473747)


![7- setting dc-1 to static IP](https://github.com/user-attachments/assets/d1b7dde4-8fc2-4ca2-85d7-325e2159c63a)


Next, I'll use Remote Desktop Connection to connect to the DC using its public IP and the log in credentials I created when setting up this machine:  

![8- Logging into the DC VM](https://github.com/user-attachments/assets/663a5576-df86-48ab-94a4-f030141e8ab2)


Once I'm logged in, the following screen will appear with the Server Manager open. Next, I'm going to disable the firewall (you probably wouldn't do this in real lfe, but for the sake of this lab where nothing is at stake, I'll go ahead and do it). So, to disable the firewall I'll right click on the "Start" button and select "Run". Then type "wf.msc":  

![9- Windows Server Firewall](https://github.com/user-attachments/assets/fed4deb6-9e05-4157-9bf8-32a64fd69723)


Click on "Windows Defender Firewall Properties" then on the, "Domain Profile", "Private Profile, and the "Public Profile" tabs, turn the firewall state off:  

![10-Windows Firewall is off](https://github.com/user-attachments/assets/564490c4-0df5-44fc-bce0-1233f7f26bef)


Next, I need configure our clients DNS settings to the DC. Back in Azure, I'll grab the DCs private IP address. Then, I'll go to the network setting of the client machine. click on the NIC (Network Interface Card). 

![11-Client-1 Settings](https://github.com/user-attachments/assets/aee7008f-216d-45a4-9dfd-5d1b3b06c454)


Go to settings, then DNS servers and switch from "Inherit from virtual network" to "Custom". Input the DCs private IP here and save: 

![12- Client 1 Custom DNS](https://github.com/user-attachments/assets/49d3506b-d1a5-4268-b613-41fd2c834536)


After that's saved, I'll restart the client machine: 

![13- Restart Client 1](https://github.com/user-attachments/assets/3b1ffde4-a039-4480-ab68-6ade05a34984)



Once the machine as restarted, I'll use Remote Desktop connection to connect to the client machine using its public IP and the log in credentials I created while setting up this machine: 

![14- Log in to Client 1](https://github.com/user-attachments/assets/80f8ad6b-ece9-45a7-9e26-b27a09aeb115)


Now that I'm logged in, I will open Powershell and attempt to ping the DC using the ping command and its private IP address. In my case it'll look like this. 

![15 Pinging DC 1 from Client 1](https://github.com/user-attachments/assets/4ce0ae58-4c58-4184-b0e4-f5e10cbf59f5)



While I'm here I can double check that the DNS server settings are pointing to the DC. I'll run "ipconfig /all" and look for the "DNS Servers" and it should point to our DC if everything is set up properly:  

![16- Servers were set up correctly](https://github.com/user-attachments/assets/9a084011-28f4-4280-a06a-5fae0204de8a)


<h2>Active Directory Infrastructure is Now Prepared! </h2>

<b>We've successfully created two VMs (Virtual Machines), one running Windows Server, to act as a Domain Controller. The other VM as a client, running Windows 10. Don't forget: In later projects I will deploy AD, run a script that will create users in the domain, which I can log into from the client VM, then manage the accounts and update the group policies, all to simulate a real life environment!  </b>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
