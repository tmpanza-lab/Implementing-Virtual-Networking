# Implementing Virtual Networking

## Objective

This lab is the first of three labs that focuses on virtual networking. In this lab, I learnt the basics of virtual networking and subnetting. I learnt how to protect your network with network security groups and application security groups. I also learnt about DNS zones and records.

*Ref 1: Architecture diagram*
 ![image](https://github.com/user-attachments/assets/fbc9ee60-5b5c-45d0-bde7-cccee29ec998)


### Job Skills Learned

- Creating a virtual network with subnets using the portal.
- Creating a virtual network and subnets using a template.
- Creating and configuring communication between an Application Security Group and a Network Security Group.
- Configuring public and private Azure DNS zones.


### Tools Used

- Azure portal - https://portal.azure.com


## Steps

## Task 1: Create a virtual network with subnets using the portal
The organization plans a large amount of growth for core services. In this task, you create the virtual network and the associated subnets to accommodate the existing resources and planned growth. In this task, you will use the Azure portal.
1.	Sign in to the Azure portal - https://portal.azure.com.
2.	Search for and select Virtual Networks.
3.	Select Create on the Virtual networks page.
4.	Complete the Basics tab for the CoreServicesVnet.
![image](https://github.com/user-attachments/assets/2a5beb93-298b-48c1-ad38-bef89a7f5cb1)
 
5.	Move to the IP Addresses tab.
6.	Select + Add a subnet. Complete the name and address information for each subnet. Be sure to select Add for each new subnet. Be sure to delete the default subnet - either before or after creating the other subnets.
![image](https://github.com/user-attachments/assets/b92858ca-e03e-44b7-82d6-eaa8ad6fc8ff)
![image](https://github.com/user-attachments/assets/7f4e31df-2629-419e-9d22-aac4ead176a4)
 
 
7.	To finish creating the CoreServicesVnet and its associated subnets, select Review + create.
8.	Verify your configuration passed validation, and then select Create.
9.	Wait for the virtual network to deploy and then select Go to resource.
![image](https://github.com/user-attachments/assets/9d208158-cb65-491a-990d-e10b5c1825ea)
 
10.	Take a minute to verify the Address space and the Subnets. Notice your other choices in the Settings blade.
 ![image](https://github.com/user-attachments/assets/7a854cde-737d-47e9-a5c6-88cd18d7d1fd)
![image](https://github.com/user-attachments/assets/a1e017e8-f847-49a1-b6f1-4b3733cda9e1)

 
11.	In the Automation section, select Export template, and then wait for the template to be generated.
 ![image](https://github.com/user-attachments/assets/4c3d3a7b-9c91-4433-83f3-eaba9dc87814)

12.	Download the template.
13.	Navigate on the local machine to the Downloads folder and Extract all the files in the downloaded zip file.
14.	Before proceeding, ensure you have the template.json file. You will use this template to create the ManufacturingVnet in the next task.
![image](https://github.com/user-attachments/assets/fca5ae3e-2bf7-4498-95a7-6e0c3884d3c1)
 

## Task 2: Create a virtual network and subnets using a template

In this task, you create the ManufacturingVnet virtual network and associated subnets. The organization anticipates growth for the manufacturing offices so the subnets are sized for the expected growth. For this task, you use a template to create the resources.

1.	Locate the template.json file exported in the previous task. It should be in your Downloads folder.
2.	Edit the file using the editor of your choice. Many editors have a change all occurrences feature. If you are using Visual Studio Code be sure you are working in a trusted window and not in the restricted mode. Consult the architecture diagram to verify the details.
![image](https://github.com/user-attachments/assets/6c142c37-f2d8-49af-95b3-a7f3808e54bd)
 
Make changes for the ManufacturingVnet virtual network
1.	Replace all occurrences of CoreServicesVnet with ManufacturingVnet.
2.	Replace all occurrences of 10.20.0.0 with 10.30.0.0.
Make changes for the ManufacturingVnet subnets
1.	Change all occurrences of SharedServicesSubnet to SensorSubnet1.
2.	Change all occurrences of 10.20.10.0/24 to 10.30.20.0/24.
3.	Change all occurrences of DatabaseSubnet to SensorSubnet2.
4.	Change all occurrences of 10.20.20.0/24 to 10.30.21.0/24.
5.	Read back through the file and ensure everything looks correct.
![image](https://github.com/user-attachments/assets/854af255-0b39-4db1-b62a-13140b2d03db)
 
6.	Be sure to Save your changes.

Make changes to the parameters file

1.	Locate the parameters.json file exported in the previous task. It should be in your Downloads folder.
2.	Edit the file using the editor of your choice.
3.	Replace the one occurrence of CoreServicesVnet with ManufacturingVnet.
4.	Save your changes.
![image](https://github.com/user-attachments/assets/249d748b-341a-445a-85f5-c5f3a7185bb6)
 
Deploy the custom template
1.	In the portal, search for and select Deploy a custom template.
2.	Select Build your own template in the editor and then Load file.
![image](https://github.com/user-attachments/assets/716fc24a-8f28-479d-ae52-c4f98e08f423)
 
3.	Select the templates.json file with your Manufacturing changes, then select Save.
4.	Select Review + create and then Create.
5.	Wait for the template to deploy, then confirm (in the portal) the Manufacturing virtual network and subnets were created.
![image](https://github.com/user-attachments/assets/e3cdca3d-d745-422b-b50d-9a6cf7d809a3)
 
## Task 3: Create and configure communication between an Application Security Group and a Network Security Group

In this task, we create an Application Security Group and a Network Security Group. The NSG will have an inbound security rule that allows traffic from the ASG. The NSG will also have an outbound rule that denies access to the internet.

Create the Application Security Group (ASG)
1.	In the Azure portal, search for and select Application security groups.
2.	Click Create and provide the basic information.
![image](https://github.com/user-attachments/assets/625c6bc4-06fd-4ce8-ab39-a74cd4fbd6c7)

 
3.	Click Review + create and then after the validation click Create.
Create the Network Security Group and associate it with the ASG subnet
1.	In the Azure portal, search for and select Network security groups.
2.	Select + Create and provide information on the Basics tab.
![image](https://github.com/user-attachments/assets/0f610c78-f0a8-43e9-bd3d-4aa5598db9a4)
 
3.	Click Review + create and then after the validation click Create.
4.	After the NSG is deployed, click Go to resource.
5.	Under Settings click Subnets and then Associate.
![image](https://github.com/user-attachments/assets/f320a742-23f7-49f1-933c-4867da84bd46)

6.	Click OK to save the association.

Configure an inbound security rule to allow ASG traffic
1.	Continue working with your NSG. In the Settings area, select Inbound security rules.
2.	Review the default inbound rules. Notice that only other virtual networks and load balancers are allowed access.
3.	Select + Add.
4.	On the Add inbound security rule blade, use the following information to add an inbound port rule. This rule allows ASG traffic. When you are finished, select Add.
![image](https://github.com/user-attachments/assets/af17c905-9bce-47a4-bf75-79029c3f550e)
 
 

Configure an outbound NSG rule that denies Internet access
1.	After creating your inbound NSG rule, select Outbound security rules.
2.	Notice the AllowInternetOutboundRule rule. Also notice the rule cannot be deleted and the priority is 65001.
3.	Select + Add and then configure an outbound rule that denies access to the internet. When you are finished, select Add.
![image](https://github.com/user-attachments/assets/199afe25-e712-4518-ae15-ce08d711002f)
![image](https://github.com/user-attachments/assets/60374cf5-a30c-4de1-a6cc-4ea285066016)

 
 
## Task 4: Configure public and private Azure DNS zones

In this task, you will create and configure public and private DNS zones.
Configure a public DNS zone
You can configure Azure DNS to resolve host names in your public domain. For example, if you purchased the contoso.xyz domain name from a domain name registrar, you can configure Azure DNS to host the contoso.com domain and resolve www.contoso.xyz to the IP address of your web server or web app.

1.	In the portal, search for and select DNS zones.
2.	Select + Create.
3.	Configure the Basics tab.
![image](https://github.com/user-attachments/assets/bab4a72c-7820-4ae7-b9b7-a6438156e582)
 
4.	Select Review create and then Create.
5.	Wait for the DNS zone to deploy and then select Go to resource.
![image](https://github.com/user-attachments/assets/7ee8c9aa-7166-4855-b49d-cc2d8547a444)
 
6.	On the Overview blade notice the names of the four Azure DNS name servers assigned to the zone. Copy one of the name server addresses. You will need it in a future step.
![image](https://github.com/user-attachments/assets/30bc5ce1-980e-4a84-b9be-b7eb4d6806a9)
 
7.	Select + Record set. You add a virtual network link record for each virtual network that needs private name-resolution support.
![image](https://github.com/user-attachments/assets/1d9dca56-039c-4fe7-a482-84be6c87eb31)

 
1.	Select OK and verify sky29.co.za has an A record set named www.
2.	Open a command prompt, and run the following command:
3.	Verify the host name www.contoso.com resolves to the IP address you provided. This confirms name resolution is working correctly.


Configure a private DNS zone
A private DNS zone provides name resolution services within virtual networks. A private DNS zone is only accessible from the virtual networks that it is linked to and can’t be accessed from the internet.
1.	In the portal, search for and select Private dns zones.
2.	Select + Create.
3.	On the Basics tab of Create private DNS zone, enter the information as listed in the table below:
![image](https://github.com/user-attachments/assets/f9897331-96d7-49be-a827-092f9ed268da)
 
4.	Select Review create and then Create.
![image](https://github.com/user-attachments/assets/faa50f16-8986-4ec2-a576-3d0b52901adb)
 
5.	Wait for the DNS zone to deploy and then select Go to resource.
6.	Notice on the Overview blade there are no name server records.
7.	Select DNS Management and then select Virtual network links. Configure the link.
![image](https://github.com/user-attachments/assets/f40b3128-1870-4e90-8b02-e72bc09c12cb)
 
8.	Select Create and wait for the link to create.
 ![image](https://github.com/user-attachments/assets/ce0fa45c-e9b5-4054-8d57-789691437335)

9.	From the DNS Management blade select + Recordsets. You would now add a record for each virtual machine that needs private name-resolution support.
 ![image](https://github.com/user-attachments/assets/79cbe5e9-0924-49bf-9940-4988f314a22e)




