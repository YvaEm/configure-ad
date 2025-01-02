<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines. The following will show how to create Organizational Units, RDP into systems, Create User Accounts and GP
<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)



<h2>Deployment and Configuration Steps</h2>

<p>
On DC-1 install Active Directory Domain Services 

Press add roles and features

</p>

![Screenshot 2025-01-01 183922](https://github.com/user-attachments/assets/78079e4c-8291-4958-8c38-917d58db2030)


<br />

<p>
Select Active Directory Domain Services 

Press  next and add features then Install
  
![Screenshot 2025-01-01 183957](https://github.com/user-attachments/assets/20271187-b846-4d35-82be-d354b48eaf84)

![Screenshot 2025-01-01 184011](https://github.com/user-attachments/assets/36f83f87-f1a1-4dd0-968a-ecbb3a1bdd5f)

![Screenshot 2025-01-01 184043](https://github.com/user-attachments/assets/3e76c2ba-5309-48e1-acd6-8de6a563fb81)

 
</p>
<br />


<p>
Promote DC-1 into a Domain Controller 

```
  Press the flag with the yellow sign on it
  Press "Promote this server to a doamain controller"
```
![Screenshot 2025-01-01 184203](https://github.com/user-attachments/assets/ff0488e1-a1eb-4141-8105-e7a0e3f7792f)

![Screenshot 2025-01-01 184214](https://github.com/user-attachments/assets/51c7adcd-ef5a-410c-9cd9-a57f2b38e84c)



</p>
<br />

<p>
Add a new forest and name it accordingly

  
![Screenshot 2025-01-01 184238](https://github.com/user-attachments/assets/5d824243-cee8-4630-ba5a-98c5585d2463)

Type in a password

![Screenshot 2025-01-01 184540](https://github.com/user-attachments/assets/5dd52577-1a84-4a0d-9497-521304e4effd)

Uncheck Create DNS delegation

![Screenshot 2025-01-01 184555](https://github.com/user-attachments/assets/00499d38-195f-4ccc-888f-f9adb0d3ad67)



</p>
<br />

<p>
Log into DC-1 as a domain user(I spelled "mydomain" wrong make sure you spell your domain name correctly) 

![Screenshot 2025-01-01 185243](https://github.com/user-attachments/assets/fac09a6f-596e-477e-8c08-6a18961eb296)


</p>
<br />

<p>
Create two Organizational Units

```
  _EMPLOYEES
  _ADMINS
```

![Screenshot 2025-01-01 185700](https://github.com/user-attachments/assets/f72c4c16-e099-4f69-aeb5-c79b0be1a238)
![Screenshot 2025-01-01 185808](https://github.com/user-attachments/assets/3557f455-9ec2-4c2f-a70e-f8a0cfb641bb)


</p>
<br />

<p>
Create a User in the Domain under the _ADMINS OU

```
  Fill out user credentials page
  Create a password for user
```
  
![Screenshot 2025-01-01 185902](https://github.com/user-attachments/assets/9f0c26cd-bd12-4088-8178-1474b75f2244)

![Screenshot 2025-01-01 185923](https://github.com/user-attachments/assets/d2267ba1-5c0d-45e6-8334-c44c379476f4)

![Screenshot 2025-01-01 185950](https://github.com/user-attachments/assets/ecbc11ab-86b2-41a4-b271-b9ee59e5b665)



</p>
<br />

<p>
Make the user a admin in the domain


Right click the user and select properties 

![Screenshot 2025-01-01 190026](https://github.com/user-attachments/assets/9c03d03b-224b-4606-8fc6-616f3e58d9f5)

In properties go to the member of tab and type in domain admins press check names then ok

![Screenshot 2025-01-01 190118](https://github.com/user-attachments/assets/e0d737cd-adf7-4104-b5fd-07920111818c)

Press ok

![Screenshot 2025-01-01 190134](https://github.com/user-attachments/assets/29f08bc3-e454-4b70-902f-412481b954d7)

RDP back into DC-1 as the new User account

![Screenshot 2025-01-01 190259](https://github.com/user-attachments/assets/4a08e379-da50-49b7-8e49-2fa29e4bf07a)



  
</p>
<br />

<p>

Login into Client-1 as local user and join the PC to the domain

![Screenshot 2025-01-01 190510](https://github.com/user-attachments/assets/3fe0b38b-5acb-4aed-9640-978ed0381aee)

Open the settings and go to the about page on the right side of the screen select Rename the pc (advanced)

![Screenshot 2025-01-01 190638](https://github.com/user-attachments/assets/d6ca2651-1b51-4b6c-9bbb-8c95940873ce)

On the System Properties window under the computer name tab press change

![Screenshot 2025-01-01 190712](https://github.com/user-attachments/assets/0c3a8ac2-2c73-489c-a1d2-f1161f4b3fdf)

Type in your domain name and enter the credentials of the user account you created

![Screenshot 2025-01-01 190819](https://github.com/user-attachments/assets/bf414c9a-a639-4bc3-be5a-6649a9618f60)

Success

![Screenshot 2025-01-01 190904](https://github.com/user-attachments/assets/f8be1719-fca8-4a61-99ae-181da3dcaf18)


</p>
<br />

<p>
In Active Directory check the computers folder and you should see Client-1

![Screenshot 2025-01-01 191023](https://github.com/user-attachments/assets/068626d5-b82f-4627-b2c1-0843cca80201)

Create a _CLIENTS OU and put Client-1 in it 

![Screenshot 2025-01-01 191118](https://github.com/user-attachments/assets/98de1d45-8042-4c20-9842-4cb312868ad6)

</p>
<br />


<p>
Allow Domain users to access Remote Desktop on Client-1


RDP into client-1 as the User Account you created
  
Open settings, type in remote desktop and under User Accounts press select users that can remotely access this pc

![Screenshot 2025-01-01 191905](https://github.com/user-attachments/assets/82ea0a52-2080-4f3b-8f6f-119208125934)

Press Add

![Screenshot 2025-01-01 191932](https://github.com/user-attachments/assets/895b6c26-a90f-414e-8577-7810d25dcf72)

Type in Domain users and press check names

![Screenshot 2025-01-01 192034](https://github.com/user-attachments/assets/093040af-9370-46f9-949d-9d2a3c7f8bfa)

Press OK

![Screenshot 2025-01-01 192043](https://github.com/user-attachments/assets/9da570fd-1552-49be-b14f-70701f24bffe)



</p>
<br />


</p>
Create more user accounts in the domain and add them to the domain users group 

![Screenshot 2025-01-01 192538](https://github.com/user-attachments/assets/1cbc3f2f-e16a-4e97-8f67-c30c4cfe7767)

Put the users in the _EMPLOYEES OU
![Screenshot 2025-01-01 193008](https://github.com/user-attachments/assets/6d943f1d-0522-4abb-9d4f-d0d8195263fa)



Remote desktop into Client-1 as a random user 

![Screenshot 2025-01-01 193100](https://github.com/user-attachments/assets/5adf8ff8-49bf-48c6-a98e-d5915b9bcd00)
![Screenshot 2025-01-01 193115](https://github.com/user-attachments/assets/73fd44fe-6df8-46d6-b011-90fbdae36903)





<br />

