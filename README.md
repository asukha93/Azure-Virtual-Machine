# Azure-Virtual-Machine
# Virtual Machine Deployment and Web Server Configuration in Azure

## Introduction

In this project, I will be demonstrating how to create a Virtual Machine (VM) and deploy a Web Server in Microsoft Azure. I will be creating a Virtual Machine, connecting it to a subnet, and protecting the virtual network through inbound and outbound rules via Network Security Groups in the Azure environment. I will demonstrate how to use Bastion to connect to the virtual machine via SSH while limiting external exposure and install a Nextcloud Server. This will then be made available by opening a public IP and a DNS label. This approach aligns with cloud computing principles, enabling organizations to build scalable, cost-effective, and secure web applications.

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


Once validation has passed, click **Create**.<img src="https://i.imgur.com/jMUSDpW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Install Nextcloud

In this step, we are going to connect our Virtual Machine to our Bastion Instance via SSH and install Nextcloud on our virtual machine.

