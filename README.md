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
