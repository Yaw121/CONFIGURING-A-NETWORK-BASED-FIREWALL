### CONFIGURING A NETWORK BASED FIREWALL


<B>OBJECTIVE</B>
The objective of this lab is to develop hands-on expertise in configuring and managing a network-based firewall using pfSense. This includes securing network communication by controlling ICMP traffic, redirecting traffic to internal hosts, managing SSH connections, and setting up a robust VPN system for secure remote access and connectivity.


## Key Configurations
1. **ICMP Configuration**
   - Block ICMP requests on the firewall to enhance network security.

2. **Traffic Redirection**
   - Redirect traffic to internal hosts securely.
   - Configure pfSense to allow specific ports and redirect requests.

3. **SSH Connection Management**
   - Retarget and manage SSH connections through the firewall.

4. **VPN Configuration**
   - Configure a VPN server on pfSense to establish secure communication.
   - Export VPN client data for secure connectivity.
   - Configure and connect VPN clients.
   - Manage and troubleshoot VPN connections.

## Technologies and Tools Used
- **pfSense:** Network firewall and router platform.
- **Ubuntu:** Linux distribution for testing and deployment.
- **Kali Linux:** Security-focused Linux distribution for testing and monitoring.



<b>Experience Gained:</b>

- <b>Firewall Configuration:</b> Proficiency in configuring ICMP rules to control and secure network traffic.
Skills in redirecting traffic to internal hosts and setting up port forwarding effectively.
Secure Connectivity:


- <b>Secure Connectivity:</b> Experience in retargeting and managing SSH connections through a firewall.
  Understanding the principles of securing remote access using encryption protocols


- <b>VPN Setup and Management:</b> Practical knowledge in configuring a VPN server on pfSense to establish secure communication channels.
Expertise in exporting VPN client data and configuring client devices for seamless connectivity.
Skills in managing and troubleshooting VPN connections to ensure reliability and security.


- <b>Network Security Best Practices:</b> Understanding the role of firewalls and VPNs in protecting network infrastructure.
Hands-on experience in applying security measures to prevent unauthorized access.


- <b>Technical Proficiency:</b> Familiarity with tools such as pfSense, Ubuntu, and Kali Linux for network administration and security tasks.
Enhanced problem-solving skills through diagnosing and resolving configuration issues.
This lab provides foundational knowledge and practical skills for securing and managing network infrastructures in real-world environments.


## Instructions
1. **ICMP Configuration**
   - Navigate to the firewall settings in pfSense.
   - Set up rules to block ICMP requests.

2. **Traffic Redirection**
   - Define port forwarding rules in pfSense.
   - Redirect traffic to internal hosts as needed.

3. **SSH Configuration**
   - Retarget SSH traffic to specific internal hosts.
   - Verify SSH connection functionality.

4. **VPN Setup**
   - Configure a VPN server in pfSense.
   - Export the VPN client data.
   - Install and configure the VPN client.
   - Test and manage VPN connections.








<details>
<summary><b>CONFIGURE ICMP ON A FIREWALL</b></summary>

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

 5. Type your username and password. Click the SIGN IN button
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
<summary><b>REDIRECTING TRAFFIC TO INTERNAL HOST ON A NETWORK </b></summary>

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
![image](https://github.com/user-attachments/assets/1754bc82-328a-400d-8d4a-b3caa9908256)

 e. Distinguished Name: 
i. Common Name: internal-ca
ii. Country Code:  US 
iii. State or Province: Texas
iv. City: Austin 
v. Organization: XYZ Security  
![image](https://github.com/user-attachments/assets/b24d4067-6217-4301-82bf-e67e57dd18ef)

F. Click Save.


5. Add a server certificate this time by navigating to the Certificates tab. To add a new certificate, click 
on the + Add/Sign button. 
![image](https://github.com/user-attachments/assets/d845d18c-d2f9-4e1d-8ccc-6a135f17045d)


6. A new page should open; select the dropdown menu next to Method and select Create an internal 
Certificate.
  a. Descriptive Name: VPNServerCert 
  b. Certificate authority: MyCA 
  c. Key Length:  2048 bits 

![image](https://github.com/user-attachments/assets/e9fc6aed-fd6a-49c1-a2b7-27db32c1a6bb)

d. Lifetime: 365 days
![image](https://github.com/user-attachments/assets/7d76ab7a-156d-4074-8135-40a877a014ab)

e. Distinguished Name: 
i. 
Common Name:  pfsense.netlab.local 
ii. Country Code:  US 
iii. State or Province:  Texas 
iv. City:  Austin 
v. Organization:  XYZ Security 

![image](https://github.com/user-attachments/assets/6567f6d7-a99e-4efd-99c9-b2f9c9136364)

f. Certificate Type:  Server Certificate
![image](https://github.com/user-attachments/assets/e7ce739c-6b61-4e63-b521-01780bbf970d)
g. Click Save. 


8. Navigate to System > User Manager
![image](https://github.com/user-attachments/assets/bfe22f82-f81c-49b5-9ad2-ad727dcf17b2)


9. On the System: User Manager page, click the +Add icon to create a new user. 
![image](https://github.com/user-attachments/assets/6bc59764-4049-4059-abf2-e9a42787067e)

10. Fill in your username and password
   ![image](https://github.com/user-attachments/assets/8fd79b22-9bdf-4422-bea3-3ae51cb4659b)

 Check the box next to Click to create a user certificate (more options will appear). Then very 
the following information
![image](https://github.com/user-attachments/assets/9b613b77-91e5-4a00-b317-622251e5cbd5)


i. Descriptive name:  VPNUser_Cert 
ii. Certificate Authority:  MyCA
iii. Key Length:  2048 bits 
iv. Lifetime:  365 days
![image](https://github.com/user-attachments/assets/fda5ffec-a390-465c-9c6f-1cce87b9d86e)

![image](https://github.com/user-attachments/assets/7645a5e1-eb51-4b0d-a816-779b8abbdaa1)

e. Click Save. 

11. Navigate to VPN > OpenVPN.
 ![image](https://github.com/user-attachments/assets/018a4e95-b338-49c8-b58a-f8d153650f48)


12. While on the OpenVPN: Server page, click on the Wizards tab.
![image](https://github.com/user-attachments/assets/52959dff-3a23-4582-9ef5-6678d7fe4aba)


13. A new page appears; select Local User Access for Type of Server. Click Next. 
![image](https://github.com/user-attachments/assets/3bb83efa-efa6-4df7-ba5e-b955aad90e8a)

14. On the next page, select MyCA as the Certificate Authority. Click Next.
![image](https://github.com/user-attachments/assets/81bc8cf5-2a4b-4360-8ee1-9299eeb0aa7a)


15. Next, select VPNServerCert as the Certificate. Click Next.
![image](https://github.com/user-attachments/assets/d17d1d00-f0ce-42eb-978a-0ef32c3b2849)


16. On the next page, fill in all necessary fields as mentioned below (if the field is not mentioned, leave 
its default setting):
![image](https://github.com/user-attachments/assets/31e1e240-fa36-4608-9c53-fbcecce5aebf)


e. Cryptographic Settings: 
i. TLS Authentication:  Checked 
ii. Generate TLS Key:  Checked
iii. DH Parameters Length:  2048 bit 
iv. Fallback Data Encryption Algorithm:  AES-128-CBC (128-bit) 
v. Hardware Crypto:  No Hardware Crypto Acceleration

![image](https://github.com/user-attachments/assets/98d7f9a9-210d-4da8-8915-011bac41dcc4)
![image](https://github.com/user-attachments/assets/5f61f894-2e4e-409c-a460-c5873fb0fbe0)
![image](https://github.com/user-attachments/assets/aa9e660e-955a-4e41-b65b-be190946b2ae)


f. Tunnel Settings: 
i. Tunnel Network:  10.1.1.0/24 
ii. Redirect Gateway:  Checked 
iii. Local Network:  172.16.1.0/28 
iv. Concurrent Connections:  10 
v. Compression:  Disable Compression

![image](https://github.com/user-attachments/assets/f7c032c3-3ac0-44ba-92b9-ee9de2efa2e8)
![image](https://github.com/user-attachments/assets/4d8f874b-f0bd-456b-a52d-e8058b24eb0d)


g. Client Settings: 
i. Dynamic IP:  Checked, then Click Next. 
![image](https://github.com/user-attachments/assets/fa834b4c-71b2-4282-ab3c-a6b5be6336da)


17. On the Firewall Rule Configuration page, fill in the necessary fields: 
a. Firewall Rule:  Checked 
b. OpenVPN rule:  Checked 
c. Click Next.

![image](https://github.com/user-attachments/assets/1d5f6929-92dd-409c-8749-1c388a985d1f)

18. On the final configuration page, select Finish.

</details>

<details>
<summary><b>EXPORTING VPN CLIENT DATA</b></summary>


1.  Switch to the kali machine, and start a Firefox browser. Go to http://203.0.113.1 and log in as your username and password.
   ![image](https://github.com/user-attachments/assets/1373a68e-e209-47ab-9c1f-09bf91950c00)


2. Under VPN, click to go to the OpenVPN page.
   ![image](https://github.com/user-attachments/assets/66a9d968-0f3a-4d72-8128-e3205f0b5611)


3. Click on the Client Export tab. Scroll down towards the bottom where the OpenVPN Clients is presented. Underneath the Export 
column, click on the Archive link to download the bundled configurations. 
![image](https://github.com/user-attachments/assets/4e8d5e93-a3d0-4f3d-b20c-8ab06c43f1ac)

Notice that the file download is complete. 
![image](https://github.com/user-attachments/assets/0a5fd596-bf12-41cb-8b56-5ea90528a962)
</details>

<details>
<summary><b>CONFIGURING THE VPN CLIENT</b></summary>

1. While on the Kali system, open a terminal and type the command below to change to the 
Downloads directory.
![image](https://github.com/user-attachments/assets/de5a4cc6-e997-4cce-b724-2bc9ca0c32ad)


2. Unzip the downloaded zip file:  unzip pfSense-UDP4-1194-vpnuser-config.zip
 ![image](https://github.com/user-attachments/assets/0431db90-a373-4ead-9583-414c42d8db79)


3. Open the Network Manager by clicking on the network icon located on the top pane and navigate 
to VPN Connections > Add a VPN Connection. 
![image](https://github.com/user-attachments/assets/69279e4b-352c-4f67-aac1-fdcf27a1e9f3)


4. On the Choose a VPN connection Type window, select Import a saved VPN configuration option 
and click Create.
![image](https://github.com/user-attachments/assets/cb667d23-db84-48a6-ac68-4e0fdc193830)


5. In the File Manager window, select Downloads from the menu on the left. Double-click on the 
pfsense-udp-1194-vpnuser folder. Select the pfSense-UDP4-1194-vpnuser.ovpn file and click the 
Open button.
![image](https://github.com/user-attachments/assets/b281162e-c342-4ca2-b39d-47d81befa94e)


6. In the new pop-up window, leave the Connection name as is. Type username in the User name field, 
and type your in the Password field. Then, type your again in the User key 
password field. Then, click the Save button.
![image](https://github.com/user-attachments/assets/5a815fe1-eac6-4c32-a3f2-2fce8b6d02b0)



7. If prompted to create a password for the new key ring, leave the two fields empty and click 
Continue. 
![image](https://github.com/user-attachments/assets/5435aca9-3b28-4e9b-ab8a-2891422f9f34)


8. If prompted to store passwords unencrypted, click Continue. 
![image](https://github.com/user-attachments/assets/52f4bdd2-428a-4dc7-8697-c25ee495fee8)
</details>




<details>
  <summary><b>CONNECTING THE VPN CLIENT</b></summary>

1. Connect using the VPN settings by clicking on the Network Manager icon on the top pane and 
navigating to VPN Connection > pfSense-UDP4-1194-vpnuser. If prompted for a password, enter 
vpnpassword. Click OK.

![image](https://github.com/user-attachments/assets/30a53dfc-1c27-4dbc-97f2-a28e285d0334)

![image](https://github.com/user-attachments/assets/7dfb62f6-dd41-4822-8c20-0c1f01201e0d)


2. Once the connection is established, a message will pop up like so:
 ![image](https://github.com/user-attachments/assets/b71eba56-dc58-47ae-b4e3-a96e23ef34af)


3. Verify the VPN tunnel and the IP address given by entering the command below in a Terminal. 

![image](https://github.com/user-attachments/assets/21c49ffd-059b-4185-a887-a65c7f779a57)
</details>




<details>
<summary><b>MANAGING VPN CONNECTION</b></summary>

1. Once connected to the VPN server, switch to the UbuntuSRV, Firefox web browser, and navigate 
back to the pfSense Web Configurator. 
2. When logged in as admin, navigate to Status > System Logs from the top menu pane.

![image](https://github.com/user-attachments/assets/b8e4f71e-9e5a-4af0-a69f-a6301dc359fd)


3. On the new page, select the OpenVPN tab.

4. 4. Notice the authentication to the VPN server. You may have to scroll down to find it.
![image](https://github.com/user-attachments/assets/06611f84-81d9-43bb-a1d9-1813f47504ee)


  5. Navigate to Status > OpenVPN. 
6. Notice how the current active VPN connections are listed here
   ![image](https://github.com/user-attachments/assets/188fcba0-b121-4e77-94f7-3667c929be6c)

</details>






















