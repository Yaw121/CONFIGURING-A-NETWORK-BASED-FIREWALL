### CONFIGURING A NETWORK BASED FIREWALL


OBJECTIVE

<details>
<summary><b>Configure ICMP on the Firewall </b></summary>

  <b>Blocking ICMP Requests on pfSense </b>
Firstly, we will be using the UbuntuSRV virtual machine. Lunch the VM and open the terminal

  ![image](https://github.com/user-attachments/assets/151dbfd1-2b16-4f09-b6c9-a62a0f2756af)

  2. To check the connectivity to the Kali system with the IP address 203.0.113.2, use the ping command. Type the following command into the terminal: ping -c4 203.0.113.2
   Then, press Enter to initiate the ping. This will send a request to the specified IP address and allow you to verify if the Kali system is reachable and responding to network requests.
![image](https://github.com/user-attachments/assets/27629e87-1416-474e-b384-28466355c819)

2. Once the ping request is successfully received and you confirm connectivity, proceed by launching the Kali virtual machine. This will allow you to begin further work or analysis on the Kali system as needed for your lab. Open a new terminal window by clicking on the terminal icon located in the top toolbar.
  ![image](https://github.com/user-attachments/assets/affd0bd1-71f5-4f96-85ee-ccb361e54cc5)

3. From the Kali terminal, send a ping request to the UbuntuSRV system: 172.16.1.10. 
 ![image](https://github.com/user-attachments/assets/fc83d855-f683-425b-9c23-07a0c7d4ddb0)

4. After the successful ping, change focus to the UbuntuSRV system and open the Firefox web browser. In the address space, type http://172.16.1.1. Press Enter
   ![image](https://github.com/user-attachments/assets/ce22a4d2-6efa-4a19-b858-8b1104cbfd4c)

 5. Type the username sysadmin and password NDGlabpass123!. Click the SIGN IN button
    ![image](https://github.com/user-attachments/assets/ba9abfb7-578d-4654-9cf6-cb53cf4de312)

6. Once in the pfSense management graphical user interface, navigate to Firewall > Rules.
   ![image](https://github.com/user-attachments/assets/86aacf48-608c-461b-a74a-fe980b827299)

7. While viewing the WAN tab, click the Add rule to the top of the list icon on the bottom-right to add 
a new rule.
![image](https://github.com/user-attachments/assets/1fbfe73f-4982-4f8c-a414-b285fadb0333)

8.  On the newly opened page, click the dropdown box next to Action and select Block.
   ![image](https://github.com/user-attachments/assets/9de2da4b-de83-4c63-ad2a-0ed6f494a2ce)

9. Select ICMP as the Protocol selection, and leave the ICMP Subtypes as is.
   ![image](https://github.com/user-attachments/assets/bb72354e-b71f-44a4-a43c-282aa42199a8)

10. In the Destination section, set the network as the DMZ net, which is the 172.16.1.1/28 mask
    ![image](https://github.com/user-attachments/assets/08d3a72b-0629-42de-8f85-fda313c72b4a)

11.  Leave all other options as defaults. Click the Save button located towards the bottom of the page.
    ![image](https://github.com/user-attachments/assets/d040eb80-283d-4fb7-9f3c-48da555e2dc8)

12. When brought back to the Firewall: Rules page, notice the warning message. Select Apply Changes.
    ![image](https://github.com/user-attachments/assets/c10cdc69-35e2-409e-80fe-340455b65eab)

14. Verify that the firewall rules table looks like the image below for the WAN interface.
    ![image](https://github.com/user-attachments/assets/0e7c2013-96d4-48c4-81f0-78631d59dbb4)

15. Switch focus to the Kali system and open the Terminal window. In the Terminal, type the following command to attempt pinging the UbuntuSRV system: ping -c4 172.16.1.10
     After pressing Enter, you should see that the ping does not succeed, indicating that the Kali system is unable to reach the UbuntuSRV system.
    ![image](https://github.com/user-attachments/assets/7d73520b-9819-4556-89c0-fa0eb512f0ff)
</details>





<details>
<summary><b>Redirecting Traffic to Internal Hosts on the Network </b></summary>

  <b>Configuring pfSense to Allow Port and Redirect Requests</b>

  1. While on the Kali system, enter the command below to scan for open ports on the firewall 
appliance. nmap 203.0.113.1
![image](https://github.com/user-attachments/assets/12361094-cbba-4c7a-9d8e-0f2ca8f41299)

2. Change focus to the Firefox window on the UbuntuSRV system. In the pfSense management 
interface, navigate to Firewall > NAT.
![image](https://github.com/user-attachments/assets/3db9b08d-a666-4475-b2d5-f1adbd435424)


3. On the Firewall / NAT / Port Forward interface, click the Add rule to the top of the list button to 
add a new rule.
![image](https://github.com/user-attachments/assets/b150febe-1954-4143-bb14-4e1d950ab12b)


4. While on the Firewall / NAT / Port Forward / Edit interface, make the following changes: 
  a. Change Destination port range to SSH for both From port and To port from the dropdown 
menu.
![image](https://github.com/user-attachments/assets/5513a92c-b98c-4d3a-9549-9d10cd3ea2fb)

  b. Change Redirect target IP to 172.16.1.10.
![image](https://github.com/user-attachments/assets/b7365313-a5c2-4670-8ae8-211f6229e1ba)

  c. Change Redirect target port to SSH from the dropdown menu.
  ![image](https://github.com/user-attachments/assets/d6222bc2-7ab2-4a67-a7e7-140b43ec56db)


  d. Click the Save button located towards the bottom of the page 

5. For the new configuration to take place, click the Apply changes button.
![image](https://github.com/user-attachments/assets/d153676e-fde7-42cb-91ff-76e066a76aa0)
</details>



<details>
<summary><b>RETARGETED SSH CONNECTION</b></summary>

1.  Change focus to the Kali system and initiate a quick scan against the firewall appliance using the 
terminal: nmap 203.0.113.1... This command will perform a scan on the firewall appliance at the IP address 203.0.113.1, providing details about open ports and services running on the system. After executing the command, you will see the results of the scan in the terminal.
![image](https://github.com/user-attachments/assets/e2d3fd65-c415-4d91-b12e-cad5a737a989)
Notice the change of open ports on the system; SSH is now open.


2. To verify the SSH configuration on the firewall, open the Terminal on your Kali system and type the following command: ssh sysadmin@203.0.113.1. 
When prompted, answer "yes" to accept the fingerprint. If asked for a password, enter the password for your KALI.
![image](https://github.com/user-attachments/assets/0f9d4f7f-3d0f-4992-bf7f-05a936eebf71)


3. When you see the Secure Shell (SSH) prompt indicating you're logged in as sysadmin on the ubuntusrv machine, you can confirm you're on the correct system by using the ifconfig command: This command will display the network configuration of the system, including the IP address and network interfaces. Check the IP address to ensure it matches the expected address for the ubuntusrv machine, confirming you're on the right system.
   
![image](https://github.com/user-attachments/assets/56b3990f-609b-4834-b8d6-f6991f3df821)



4. To examine the default gateway on the system, type the <b>route</b> command.
   This will display the routing table, including the default gateway under the "Gateway" column. The default gateway is typically listed as 0.0.0.0 in the destination column and shows the IP address of the gateway.
![image](https://github.com/user-attachments/assets/fad42aa3-1fc8-4a71-a9d8-89137f5a9170)


5. To leave the active SSH connection, simply type the <b>exit</b> command
   This will terminate the SSH session and return you to the local machine's command prompt.
![image](https://github.com/user-attachments/assets/200ba411-fc70-4109-8904-05c3dda96a02)

</details>


<details>

<summary><b>CONFIGURING VPN ON PFSENSE</b></summary>

<b>CONFIGURING VPN SERVER</b>

1. Change focus to the UbuntuSRV system and focus on the Firefox web browser. If you are not 
already logged into the pfSense firewall management interface, do so now


2. While logged in, navigate to System > Cert Manager.
  ![image](https://github.com/user-attachments/assets/e13d2ee0-fbcc-4b43-948f-e07d4b233192)



3. On the System / Certificate Manager / CAs page, while on the CAs tab, click on the + Add button.
   ![image](https://github.com/user-attachments/assets/5f39edae-a4a1-413e-a5af-37d84e78ce0f)


4. A new page should open; fill in the necessary fields.  
a. Descriptive Name: MyCA 
b. Method:  Create an internal Certificate Authority
![image](https://github.com/user-attachments/assets/8ff78d76-1ecd-488d-9581-b6bc90fdb37d)


c. Key Length:  2048 bits 
d. Lifetime:  365 days 
![image](https://github.com/user-attachments/assets/1b3f6f71-a649-4c9d-8b46-b0259328ad7c)

 e. Distinguished Name: 
i. 
Common Name: internal-ca 
ii. Country Code:  US 
iii. State or Province: Texas
iv. City: Austin 
v. Organization: XYZ Security  
</details>
![image](https://github.com/user-attachments/assets/b24d4067-6217-4301-82bf-e67e57dd18ef)




