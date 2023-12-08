# Azure-Virtual-Machine
# Virtual Machine Deployment and Web Server Configuration in Azure

## Introduction

In this project, I will be demonstrating how to create a Virtual Machine (VM) and deploy a Web Server in Microsoft Azure. I will be creating a Virtual Machine, connecting it to a subnet, and protecting the virtual network through inbound and outbound rules via Network Security Groups in the Azure environment. I will demonstrate how to use Bastion to connect to the virtual machine via SSH while limiting external exposure and install a Nextcloud Server. This will then be made available by opening a public IP and a DNS label.

## Objectives
- Create a Resource Group
- Create a Virtual Network and a subnet
- Protect a subnet using a Network Security Group
- Deploy Bastion to connect to a Virtual Machine
- Create an Ubuntu Server Virtual Machine
- Install Nextcloud by connecting via SSH using Bastion
- Publish an IP
- Create a DNS label

## Azure Setup

In this step, we will be setting up the Azure environment. This will involve creating/logging into an Azure account and setting up our Resource Group. This will help to group all of our resources related to the project in the same place for a streamlined process.

- **Sign up for an Azure account if not already done.**

- Once logged in, click on **"Create a resource"** in the selected area below.<img src="https://i.imgur.com/oSFDsrY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Search **"Resource Group"** in the search bar <img src="https://i.imgur.com/1pjg2oh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Select **Resource Group** and select **Create** <img src="https://i.imgur.com/0zeKydv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Use the dropdowns to select the correct subscription and region as applicable and choose a name for your Resource Group.Select **Review and Create** once done.

 <img src="https://i.imgur.com/Xl6pbHg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once Validation has passed, select **Create** again to deploy your Resource Group.<img src="https://i.imgur.com/X45cknW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- You will receive a notification once deployent is successful, click **Go to Resource Group**<img src="https://i.imgur.com/h9gzrqX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Virtual Network and Subnet Creation

In this step, we will be creating a Virtual Network inside of the Resource Group. The virtual network will allow the resources to securely communicate with each other, as if they were physically connected. It will also aid in filtering connections between our internal resources and the Internet.

- Once inside your Resource Group, click **Create**<img src="https://i.imgur.com/708HEXO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Search **"Virtual Network"** and select the option highlighted below named **Virtual Network**<img src="https://i.imgur.com/wsPp34U.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Create**

<img src="https://i.imgur.com/e9GqAty.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Use the dropdowns to select the appropriate Subscription, Resource Group, and Region **previously used** and choose a name for your Virtual Network.

<img src="https://i.imgur.com/gQ3ofky.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **IP addresses** and click **Delete address space** as shown in the highlighted areas below

<img src="https://i.imgur.com/a9L5NoU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once deleted, click **Add IPv4 address space** and replace the default IP address with **172.10.0.0/16**

<img src="https://i.imgur.com/XsjJIBX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Add a subnet** and choose a name for the subnet. Verify the IPV4 address matches the previous one entered and Select **/24(256 addresses)** from the **Size** dropdown and click **ADD**

<img src="https://i.imgur.com/21xh9Hv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Review and Create**

<img src="https://i.imgur.com/0c8GDF4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once validation has passed, click **Create**<img src="https://i.imgur.com/UEC0hD2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- When deployment is complete, click **Go to resource**. This may take a few minutes to complete.<img src="https://i.imgur.com/3wfi6YV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Implement Network Security Groups (NSG's)

In this step, we will be creating a Network Security Group around our subnet. This enables us with the ability to allow or deny inbound and outbound traffic to and from various Azure resources and/or the Internet.

- From the Virtual Network, click on the name of your resource group to return back to the resource group area.<img src="https://i.imgur.com/dJhedCn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Create**
<img src="https://i.imgur.com/7zSxdgw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Search **"Network Security Group"** in the search bar and select **Network Security Group** as shown below<img src="https://i.imgur.com/nDYCMud.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Create**
<img src="https://i.imgur.com/m5Cv5Kt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Use the dropdowns to select the appropriate Subscription, Resource Group, and Region as **previously used**, and select a name for your Network Security Group. Click **Review and Create**.
<img src="https://i.imgur.com/Yb8Mqkv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once validation has passed, click **Create**. This may take a few minutes. <img src="https://i.imgur.com/xIhFfnP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- After deployment is successful, click **Go to resource**<img src="https://i.imgur.com/MmIKhuv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Here, we can see our Network Security Group is active and currently using the default Inbound and Outbound Security Rules. Click on the name of your resource group to return back to the resource group area.
<img src="https://i.imgur.com/mLtDQ2G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- When returned to the Resource Group, select your Virtual Network as shown below.<img src="https://i.imgur.com/Fk2bL42.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- From the Virtual Network, select **Subnets**<img src="https://i.imgur.com/au4uiFy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click on your Subnet
<img src="https://i.imgur.com/ZevJnfO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Go to **Network Security Group** and select the Network Security Group previously created. Click **Save** once complete.<img src="https://i.imgur.com/gDXlNS9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Connect to a Virtual Machine using Bastion

In this step, we will be creating a Bastion instance to connect to a future Virtual Machine.

- From within our Virtual Network, click **Subnets**.<img src="https://i.imgur.com/au4uiFy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click the button shown below to add a new Subnet.<img src="https://i.imgur.com/y5IfkY6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Under Name, type **AzureBastionSubnet**. Click **Save** once done.<img src="https://i.imgur.com/Ri1i46l.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Now, we should be able to see the new Subnet added under the name **AzureBastionSubnet**. Click **Overview**. <img src="https://i.imgur.com/PGXvXcC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

From here, click the name of your Resource Group to return to the resource group area.<img src="https://i.imgur.com/dJhedCn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Create**
<img src="https://i.imgur.com/VkupO4L.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Search **"Bastion"** in the search bar and click **Bastion** as shown below.<img src="https://i.imgur.com/fZV4FX4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Create**
<img src="https://i.imgur.com/boVHYuZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Use the dropdowns to select the appropriate Subscription, Resource Group, and Virtual Network as **previously used**. Choose a name for the Bastion Instance and Public IP address. Selecy **Review and Create** once done.
<img src="https://i.imgur.com/rWcijQT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once validation has passed, select **Create**. This may take a few minutes.
  <img src="https://i.imgur.com/mXICHpH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Create an Ubuntu Server Virtual Machine

In this step, we will be creating the Virtual Machine that will be connected to our previously created Bastion instance.

- Click the name of your Resource Group to return to the resource group area.<img src="https://i.imgur.com/DxOKYs3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- From within the Resource Group, click **Create**.<img src="https://i.imgur.com/mO1QUEf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

-Search **"UbuntuServer 18.04 LTS"** in the search bar and select the option shown below.<img src="https://i.imgur.com/Oa8aE55.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Create**
<img src="https://i.imgur.com/fg1SKQh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Use the dropdowns to select the appropriate Subscription, Resource Group, and Region as **previously used**. Choose a name for the Virtual Machine and select **Zones 1** for **Availability Zones**.
<img src="https://i.imgur.com/XLLuaK2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Scroll down to **Size** and select **"Standard_B1s- 1 vcpu, 1 GiB memeory"** and create a username. Under **Inbound port rules**, select **None** for **Public inbound ports**. Once completed, select **"Next:Disks"**
<img src="https://i.imgur.com/vqVqvGj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- For OS disk size, select **Image default(30 GiB)**. Select **"Next: Networking"** once done.
<img src="https://i.imgur.com/I6BOgor.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Under **"Public IP"**, select **None**. Click **Review and Create** once done.<img src="https://i.imgur.com/LjFwpSj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once validation has passed, click **Create**.<img src="https://i.imgur.com/jMUSDpW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- A message will appear titled **Generate new key pair**. Click **"Download private key and create resource"** when prompted and save to your local device for **future use**.
<img src="https://i.imgur.com/UhXlPKw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Install Nextcloud

In this step, we are going to connect our Virtual Machine to our Bastion Instance via SSH and install Nextcloud on our virtual machine.

- Once the Virtual Machine has completed deployment, click **Go to resource**<img src="https://i.imgur.com/CZvr3fZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- From there, click **Connect**, and then click **Connect via Bastion** from the dropdown menu.<img src="https://i.imgur.com/n6xV3xt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Go to **Authentication Type** and use the dropdown menu to select **SSH Private Key from Local File.
<img src="https://i.imgur.com/li0jgx2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Enter the username used when creating the Virtual Machine and select the blue folder button to upload the **SSH Private Key** previously saved to our local device. Click **Connect** once done.
  <img src="https://i.imgur.com/wT6e8Qg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

 - Once connected, a new window will open similiar to the photo shown below. Enter the command **sudo snap install nextcloud**. This will install Nextcloud and may take a few minutes to complete.

<img src="https://i.imgur.com/oSReK28.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Once finished, we will begin setting up our username and password.
- Type **sudo nextcloud.manual-install** as shown in **RED** below. Followed by **YOUR UNIQUE** username and password shown in **BLUE** below. Hit the **enter** key to proceed with installation. This may take a few minutes.
In my case, I have used **admin** as my username and **admin** as my password FOR TEST PURPOSES.
<img src="https://i.imgur.com/w93ymAc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- After installlation is complete, type **sudo nextcloud.enable-https self-signed** and hit enter<img src="https://i.imgur.com/mDA4HUW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once finished, type **exit** and hit the enter key<img src="https://i.imgur.com/aYfqGfT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- A message will appear saying **You have been discnnected**. Click close to exit the browser and return to the Azure environemnt.<img src="https://i.imgur.com/fVx870y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

With this, our Virtual Machine has been connected using Bastion via SSH and we have succesfully installed the Nextcloud server!

## Publish the IP

In this step, we will create a public IP and only allow HTTPS connections.

- After exiting the browser, click on **Network Settings** as shown below.<img src="https://i.imgur.com/2haHQ2C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Go to **Network Interface** and click on the link as shown below.<img src="https://i.imgur.com/RDR5Wi0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click on **IP Configurations**
<img src="https://i.imgur.com/CKgRVqB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click on the **ipconfig1** link
  <img src="https://i.imgur.com/6xjI7kY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Create a public IP address**, enter a name for the new public  IP address, select **Standard** for SKU, click **OK** and then **Save** to complete editting settings. This may take a few moments to complete. 
  <img src="https://i.imgur.com/wpqcdmF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Our newly create Public IP Address is now active.  <img src="https://i.imgur.com/9rWPnQ1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Next, we will edit our inbound security rules to only allow inbound HTTPS traffic from our current IP address. This will be different for everyone. Go to whatsmyip.com and copy your IP address.

Once you have your IP address, go back to Azureand click **Network Settings** as shown below to return to that area.
<img src="https://i.imgur.com/ipxKHMR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- From there, click **Create port rule** and select **Inbound port rule** from the dropdown.<img src="https://i.imgur.com/YuJIbTe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Using the dropdown, Change **Source** to **IP Addresses**. Under **Source IP Addresses**, add your unique IP address that we copied through whatsmyip.com. Using the dropdown again, change the **Destination** to **Private IP Address** as shown below. Change **Service** to **HTTPS** and choose a name for the new rule. CLick **ADD** once done. This may take a few minutes.

<img src="https://i.imgur.com/iX4ugPf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

With this, we have succesfully associated a Public IP to our Nextcloud Server. 

## Create a DNS Label

In this step, we will be setting up a DNS entry for our Public IP in order to access our Nextcloud Server successfully.

To do this, we need to return to our resource group. You can do that by clicking on the name of you resource roup as shown below. The name of your resource group will be different. <img src="https://i.imgur.com/85HEL8q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

From the Resource Group, click the link to the **Public IP Address**<img src="https://i.imgur.com/sj8xJYQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click **Configuration**
<img src="https://i.imgur.com/RIK1wZW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Enter a name under **DNS name label** and click **Save** when done.<img src="https://i.imgur.com/JMGD5pp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Once saved, click **Overview**
<img src="https://i.imgur.com/Oy7rsF6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Here, we can see the DNS name has been added successfully.<img src="https://i.imgur.com/3tvccGM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click the name of your Resource Group to return to the resource group area.<img src="https://i.imgur.com/ahTcpcH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click on the link of your Virtual Machine.<img src="https://i.imgur.com/3PgxBNi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click on **Connect** and then click on **Connect Bastion** from the dropdown and log in to Bastion as done prevously.
  <img src="https://i.imgur.com/gyyN5UG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- After logging in, type **sudo nextcloud.occ config:system:set trusted_domains 1 --value=** followed by **YOUR UNIQUE** dns name previously created as shown below. Hit enter key once don and exit bastion.exit

  <img src="https://i.imgur.com/puf15Md.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- After exiting, open a new tab in your browser and enter **https://** followed by the DNS name previously used to access Nextcloud.

The website should load and ask for an username and password. Fill that out using the credentials previously created in Bastion and log in.
  <img src="https://i.imgur.com/PWv78YN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

After logging in, the site will load succesfully.   <img src="https://i.imgur.com/D3ujpL9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

This completes the project. Following these steps, we have successfully completed each objective to fully create a Virtual Machine, deploy a Web Server, install Nextcloud using Bastion via SSH, published an IP, and created a DNS label.
