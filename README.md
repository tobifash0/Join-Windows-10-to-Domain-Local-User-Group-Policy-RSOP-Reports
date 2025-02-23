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


10. 
