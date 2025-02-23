# Overview: Lab 5 Join Windows 10 to Domain (Local User), Group Policy, RSOP Reports

This section of my home lab documentation demonstrates the process of joining a Windows 10 machine to a domain with a local user, configuring Group Policy settings, and generating RSOP (Resultant Set of Policy) reports to analyze the applied policies. The project focuses on how to manage and enforce policies across computers in a domain using Group Policy Objects (GPOs) and review their application using RSOP reports.

## Objectives

Join a Windows 10 PC to a domain with a local user account.
Configure and apply Group Policy Objects (GPOs) to enforce settings on domain-joined computers.
Generate RSOP (Resultant Set of Policy) reports to review and troubleshoot applied policies.
Use Group Policy Management Console (GPMC) to manage and configure GPOs.

## Documentation 

In this home lab, we will create another virtual machine running Windows 10, named Desktop2, to simulate a local user account for testing purposes. This virtual machine will represent an employee in our lab environment. For example, if this user encounters password issues, we can reset it using the Help Desk account on our primary Windows 10 virtual machine.

To create the new virtual machine, click on Machine → New, then name it Desktop2. Select the Windows ISO image from your downloads, choose Skip unattended installation, and then click Finish.

![image](https://github.com/user-attachments/assets/9ad6c793-881e-47c2-ab54-bf0e4f4092e1)

<br>

1. The process will be the same as we did for our other Windows 10 virtual machine for the Helpdesk account. Select Next → Install now → I don't have a product key.

<br> 

![image](https://github.com/user-attachments/assets/e26d1a16-948c-49d3-b069-628cc5b8e531)

<br>

2. Select Windows 10 Pro, then click Next → Custom: Install Windows only → Next.

<br>

![image](https://github.com/user-attachments/assets/98b92c4a-eb33-47b3-a03c-916be9d7de90)

<br> 

3. Continue with the same configurations as before for the Windows 10 Helpdesk account. Select Personal Use, then enter User for the name and skip the password creation.

<br>

![image](https://github.com/user-attachments/assets/4b484356-31dd-45cd-bed4-d525c5db19dd)

<br>

4. Now that Desktop2 is created, we can create a user for this computer. To do this, open up your Helpdesk PC virtual machine and sign in as Helpdesk. Keep in mind that Windows Server 2022 needs to be running in the background to provide access to Active Directory Users and Computers on our Desktop1 lab machine.

Remember, we currently have three virtual machines running: Windows Server 2022, Windows 10 Helpdesk, and our newly created Windows 10 local user account.

<br> 

![image](https://github.com/user-attachments/assets/41e9d497-a690-440f-abf4-53abb6021645)

<br>

5. Let’s open Active Directory Users and Computers on the Windows 10 Helpdesk machine. Right-click on our domain tobifash.com, then select New → Organizational Unit. Name the first Organizational Unit HR. Repeat the process and create a second Organizational Unit, naming it IT. You should now have two OUs: HR and IT.

<br> 

![Screenshot 2025-02-19 at 3 31 42 AM](https://github.com/user-attachments/assets/7ba713ca-05b5-4ed5-be78-6e3a436123a0)

<br>

6. Next, let’s create a user in Active Directory. Right-click on Users under the domain, then select New → User. Name the user Bob (first and last name) and set the Logon Name to Bob. Make sure all the options are unchecked, then set a password for Bob and click Finish to complete the user creation.

<br>

![Screenshot 2025-02-19 at 3 33 04 AM](https://github.com/user-attachments/assets/2b6374c7-c475-4c94-9e6e-b7624d5a7c37)


<br>


7. <br>

![Screenshot 2025-02-19 at 3 35 04 AM](https://github.com/user-attachments/assets/d9e18d15-ee03-495d-bc96-0ca6138b3d17)

<br>

8. Now, let's drag the newly created user Bob into the HR organizational unit (OU). When the prompt appears asking if you are sure, click Yes to confirm the action. This will successfully move Bob into the HR OU.

<br>

![Screenshot 2025-02-19 at 3 36 03 AM](https://github.com/user-attachments/assets/194d33e6-355f-4d45-b16d-97a7cd1f0b88)


<br>


9. Next, move the 'Helpdesk' user into the IT OU. After completing this, you should have 'Bob' in the HR OU and 'Helpdesk' in the IT OU. To verify the users' locations, enable 'Advanced Features' by selecting the 'View' tab at the top, then choosing 'Advanced Features'.

<br>

![Screenshot 2025-02-19 at 3 38 21 AM](https://github.com/user-attachments/assets/44b0d482-3a4a-4e93-8fda-0b33f03deefd)

<br>


10. Now, to locate the user 'Bob,' right-click on the domain tobifash.com and select 'Find.' 


<br>
<img width="898" alt="Screenshot 2025-02-22 at 10 55 07 PM" src="https://github.com/user-attachments/assets/7142302c-e769-4287-aede-ab3b883533fe" />

<br>

11. In the 'Find' window, right-click on 'Users' and choose 'Properties.' Then, select 'Entire Directory' and type 'Bob' in the search box. Double-click on his name when it appears, and navigate to the 'Objects' tab to view his details.

    <br> 

   <img width="898" alt="Screenshot 2025-02-22 at 11 02 35 PM" src="https://github.com/user-attachments/assets/af54742c-4c98-4919-a824-a5847a4292e7" />
 
<br>

12. <br>
![image](https://github.com/user-attachments/assets/5e0e3794-85e2-4d8c-b242-c56cc3051dc5)

<br>

13. In the Objects tab, you should see that Bob is part of the HR organizational unit, listed as SimoTech.com/HR/Bob.

<br>

![Screenshot 2025-02-19 at 3 39 59 AM](https://github.com/user-attachments/assets/2e334f83-2f11-4345-a481-0cb9d5f6aa90)

<br>

14. We can confirm this with Helpdesk.

<br>

![Screenshot 2025-02-19 at 3 39 59 AM](https://github.com/user-attachments/assets/aae1ac87-a2fc-4dce-a634-33451616d678)

![Screenshot 2025-02-19 at 3 41 08 AM](https://github.com/user-attachments/assets/d0f9eea1-1ef1-4101-ab7d-6edd176610d5)

<br> 

15. Let's navigate to Group Policy Management in Server Manager using our Helpdesk account. From there, go to "Tools" and select "Group Policy Management."

<br>

![image](https://github.com/user-attachments/assets/f978fbe4-e379-45a9-aa59-d383b8d5854b)

<br> 

16. This will display the group policy for our domain controller. Select "Domains" → "tobifash.com" → "Default Domain", then click "Generate Report." Next, go to "Settings" and click "Show All" in the top-right corner.

<br> 

![Screenshot 2025-02-19 at 3 47 24 AM](https://github.com/user-attachments/assets/74a75c37-154c-4e8d-b017-5fdb2e7c0c11)

<br>

17. This report offers a comprehensive view of various policies, including account policies, password policies, and account lockout policies. It is an invaluable tool for understanding the policies applied to a user. For instance, we can observe that the Account Lockout Policy is configured with a threshold of 0 invalid logon attempts. This setting poses a security risk, as it allows unlimited login attempts, making the system vulnerable to brute-force attacks.

<br>

![image](https://github.com/user-attachments/assets/f4217c84-3c8d-4cba-bacd-077740bc1d88)


<br>

18. To modify this policy, right-click on "Default Domain Policy" and select "Edit."

<br> 

<img width="898" alt="Screenshot 2025-02-22 at 11 30 33 PM" src="https://github.com/user-attachments/assets/36d94eb6-38a2-4d88-9a92-a42df05113de" />

<br> 

19. Select "Policy," navigate to "Windows Settings," then to "Security Settings," and double-click on "Account Policies."

<br>

![image](https://github.com/user-attachments/assets/67e4eeb0-dee4-4086-a57d-b58353bba3cd)

<br>

20. Double-click "Account lockout duration," enable the "Define this policy setting" option, and set it to 30 minutes.

<br> 

![image](https://github.com/user-attachments/assets/d4919d21-9fc2-4094-b99b-89e7d157aef3)

<br> 

21. Additionally, as a personal preference, you can modify the "Account lockout threshold" by double-clicking it and reducing the number of invalid logon attempts from 5 to 4.

<br> 

![image](https://github.com/user-attachments/assets/1d0a4e90-e71e-47db-82df-6a2d29267667)


<br>


22. Now, let's configure some settings in the Password Policy tab. Adjust the Maximum password age to 90 days.

<br> 

![image](https://github.com/user-attachments/assets/7cb2d106-a22b-435e-8374-902f66b20c8e)

<br>

23. After configuring the policies, let's enforce them by right-clicking on "Default Domain Policy" and selecting "Enforced."

<br>

<img width="898" alt="Screenshot 2025-02-22 at 11 42 31 PM" src="https://github.com/user-attachments/assets/3e0049ae-0c49-4638-be79-c6f7aa6c7899" />

<br>


24. To verify that our policies have been updated, open Server Manager and navigate to Tools → Group Policy Management → Default Domain Policy. Generate a report, go to Settings, and select Show All. Confirm that all changes are enforced: the Maximum password age is set to 90 days, and the Account lockout threshold and Account lockout duration reflect the configurations we applied.

<br>

<img width="898" alt="Screenshot 2025-02-22 at 11 48 54 PM" src="https://github.com/user-attachments/assets/643a6766-355c-40de-afd2-317a74bb0e1c" />

<br>

25. Let's return to the Desktop2 virtual machine and open File Explorer. Right-click on This PC and select Properties. Click on Rename this PC (Advanced) → Change, update the current computer name to "Desktop2," and then click OK to apply the change. Finally, restart the system to complete the process.

<br>

![image](https://github.com/user-attachments/assets/af9a4356-c0cb-4a94-8d6c-e5b53b9e4596)

<br>


26. After the restart, let's enable the Administrator account. Open File Explorer, right-click on This PC, and select Manage. In the Computer Management window, navigate to Local Users and Groups → Users. Right-click on Administrator, select Properties, and uncheck "Disable account". Then click Apply and OK to enable the account.

<br>

![image](https://github.com/user-attachments/assets/252af958-76eb-42d1-9932-6b915be97c1a)

<br>

27. Right-click on the Administrator account again and select Set Password. Enter the desired password for the account and confirm it. Then click OK to apply the changes.

<br>

![image](https://github.com/user-attachments/assets/578bebc3-9beb-4f5b-b375-b78d5980ba78)

<br>

28. After that, sign out of the PC and log into the administrator.

<br>

![image](https://github.com/user-attachments/assets/50e1f266-2d74-4523-a8b0-a28bb7e1cd5a)

<br>

29. To remove the User login screen, follow these steps: <br>

1. Open File Explorer and right-click on This PC.


2. Select Properties and then click on Advanced system settings.


3. Under the User Profiles section, click Settings.


4. Find and select Desktop\User from the list, then click Delete to remove the user profile.

<br>

![image](https://github.com/user-attachments/assets/06271dbc-6cc2-4fe8-b6c9-53ae76f8a2c9)

<br>

30. Next, open Control Panel and go to View Network Status and Tasks. Click on Change adapter settings, then right-click on the Ethernet connection and select Properties.
    

Double-click on Internet Protocol Version 4 (TCP/IPv4), and configure the static IP settings as follows:


IP Address: 192.168.1.102

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.1.1

Preferred DNS: 168.192.1.1


Click OK to apply the settings.

<br>

<img width="654" alt="Screenshot 2025-02-23 at 12 09 01 AM" src="https://github.com/user-attachments/assets/ce7e4e84-41d3-4e35-82b5-f72f37d8406c" />

<br>

31. Next on our virtual machine, select “Devices” → “Network” → “Network settings” → and change “NAT” to “Internal Network”.

<br>

<img width="963" alt="Screenshot 2025-02-23 at 12 14 32 AM" src="https://github.com/user-attachments/assets/758c4ede-6c43-49ec-bccd-3b5825d604dd" />

<br>

32. Now lets open Command Prompt and ping our domain, Tobifash.com.

<br>

<img width="912" alt="Screenshot 2025-02-23 at 12 17 19 AM" src="https://github.com/user-attachments/assets/f5528402-824e-478e-bfb3-94e4ae01f3a7" />

<br>

33. Now, let's add this PC to our domain by opening File Explorer, right-clicking on This PC, selecting Properties, then clicking on Rename this PC (Advanced), and finally selecting Change.

<br>

![Screenshot 2025-02-19 at 4 28 50 AM](https://github.com/user-attachments/assets/bc3e2bcd-a204-4568-918b-7c38548a8217)

<br>

34. Then, we can use our Helpdesk administrator account to join the domain. Afterward, restart the VirtualBox. Once restarted, check Active Directory Users and Computers → Computers under our Helpdesk account. You should see that Desktop2 has been successfully added to our domain, tobifash.com.

<br>

![Screenshot 2025-02-19 at 4 41 30 AM](https://github.com/user-attachments/assets/228c02ee-c382-48a8-b2cb-e4aff019af04)

<br> 

35. Now when our PC is finish restarting, lets log in as Bob on our local user account Desktop2

<br> 

![image](https://github.com/user-attachments/assets/e513448d-3544-4187-b803-2924ca1541fa)

<br> 

36. Finally, we’ll run some key command-line tools to ensure everything is functioning correctly. Using ping tobifash.com, we verify network connectivity with the domain controller. The ipconfig command confirms proper network configuration, and net use Bob /domain tests our ability to access domain resources with valid credentials. With these checks, we can confidently confirm that our setup is working as expected.

<br>

![Screenshot 2025-02-19 at 4 44 14 AM](https://github.com/user-attachments/assets/ee69ce77-5e78-49b2-8794-dd59250ef491)

<br>

![Screenshot 2025-02-19 at 4 44 33 AM](https://github.com/user-attachments/assets/99db373c-c0d9-4b13-ad73-c4854238af22)

<br>

Congratulations! We have successfully joined Desktop2 to the domain as a local user on a Windows 10 PC, configured and analyzed policy settings, and explored Group Policy Management.

For administration and troubleshooting, we utilized Command Line Tools (CMD) and generated Resultant Set of Policy (RSOP) reports to review the implemented policies.


👉 Next Lab 6 : Common Active Directory Issues, CMD Commands, PC Offline
