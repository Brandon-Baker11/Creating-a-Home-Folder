![what-is-active-directory-and-why-is-it-used](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/2facaf12-f88b-414f-b128-109c98a993f9)

# Creating-a-Home-Folder (OracleVM VirtualBox)
This tutorial will walk you through the steps of creating a Home Folder using Active Directory within a VirtualBox VM environment

##Environments and Technologies Used
-OracvleVM Virtual Box
-Active Directory Domain Services
-Group Policy Management

##Operating Systems Used
-Windows Server 2019
-Windows 10 (22H2)

## Configuration Steps
In this lab, we will walk through the process of creating a home folder for a user. We will create a user, create a folder that will be shared on the network,
-Create a user
-Create a folder that will be shared on the network
-Redirect the location that the user's data will be saved to

This method of storing data centralizes the management of a user's files by storing them on a server instead of on their local machine. So in case they accidentally delete a file or can no longer access it, a system administrator can backup their lost data. And if the user uses a laptop that is often taken home and is not connected to the network, you can apply certain settings that allow them to make changes to their files offline and update to the server when it is connected to the network.



Okay, so we are going to log into our DC as an administrator, and we will open the server manager application and select ***Tools*** in the top right-hand corner, and then select ***Active Directory Users and Computers*** from the drop-down menu.
![Screenshot1](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/34ef2feb-a39c-445c-9eba-700cccfb655c)


In the ***Active Directory Users and Computers*** window, right-click any blank space there is in the details pane to the right and select ***New*** and then select ***Group***
![Screenshot0](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/f72f086c-a053-4187-b3c4-3f215aa6679b)


In the ***New Object-Group*** dialogue box, type "Folder Redirect" into the ***Group name*** field

Click ***OK***
![Screenshot01](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/58244e12-7942-4fac-aec6-041bee14ca5b)-->


In the ***Active Directory Users and Computers*** window, right-click any blank space there is in the details pane to the right and select ***New*** and then select ***User***
![Screenshot2](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/8b6f7e89-87a2-4e0a-a7d8-1c5172cac459)


In the ***New Object-User*** dialogue box, type "testuser" into the ***First name*** and ***User logon name*** fields

Click ***Next***
![Screenshot3](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/27827024-dfe7-4078-a002-d07479d0f721)


Type "Password1" into the ***Password*** and ***Confirm Password fields (This isn't the strongest password I know, but this is just for demonstration purposes). Then disable ***User must change password at next logon*** and enable ***Password never expires*** 

Click ***Next***
![Screenshot4](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/6c082d30-cae2-4e0f-a86b-251c14c29172)


Click ***Finish***
![Screenshot5](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/e1cefbfe-e931-48f9-ab74-fc5e9cdc61d2)


Now, back on the ***Active Directory Users and Computers*** window, right-click the group we just created, ***Folder Redirect***, and select ***Properties***
![Screenshot6](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/8c3ec0a6-d362-498b-b377-8c0d9d463c3f)


From the ***Folder Redirect Properties*** dialogue box, select the ***Members*** tab and click ***Add***
![Screenshot7](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/a4e87993-daf7-4f7c-b84e-e6174ed873cd)


In the ***Select Users, Contacts, Computers, Service Accounts, or Groups*** dialogue box, type "testuser" in the ***Enter the object names to select*** field and click ***Check Names*** and click ***OK***
> The user's username will populate once you click the ***Check Names*** button
![Screenshot8](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/3de5519a-d83a-4625-b83e-958762559fba)


The user ***testuser*** is now added as a member of the ***Folder Redirect*** group

Click ***OK***
![Screenshot9](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/e8492b10-beb3-4632-bdad-da6619c6dd71)


Next, we will be applying permissions and rules for the ***Folder Redirect*** group. Restore server manager and go to ***Tools*** in the top right-hand corner and select ***Group Policy Management***
![Screenshot1](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/4f39428f-bd8f-42ad-be6b-f464942db46e)


In the ***Group Policy Management*** window under your domain, right-click on ***Group Policy Objects*** and select ***New***
![Screenshot2](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/b4f002ec-3677-41fc-ad79-b04b156c3698)


Now in the ***New GPO*** dialogue box, type ***Folder Redirection*** in the ***Name*** field

Click ***OK***


Expand the ***Group Policy Objects*** node and right-click ***Folder Redirection*** and select ***Edit***
![Screenshot3](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/0d50a783-aac6-4809-a3db-f652a21e6aff)


In the ***Group Policy Management Editor*** window, expand the nodes: ***User Configuration > Administrative Templates > System*** and select ***Folder Redirection*** and on the ***Folder Redirection*** pane right-click ***Do not automatically make all redirected folders available offline*** and select ***Edit***
![Screenshot4](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/19e9f7d6-5280-42b5-83bb-9ccd645b9af2)
![Screenshot5](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/919af6a6-483f-4789-9020-3869cb909062)


In the ***Do not automatically make all redirected folders available offline*** window select the ***Disabled*** option. This will make it so every redirected folder is automatically made available offline as well as all of the subfolders within the redirected folder

Click the ***Next Setting*** button 
![Screenshot6](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/fc6a5e10-bc16-4620-877a-efb41812c189)


In the ***Do not automatically make specific redirected folders available offline*** window select ***Enabled*** and select the folders ***Pictures, Music,*** and ***Videos*** in the ***Options*** section. This setting makes a user manually select the files they want to make available offline.
![Screenshot7](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/5b85a58f-6428-463d-b871-16e38f09226b)


In the ***Enable optimized move of contents in Offline Files cache on Folder Redirection server path change*** select ***Disabled***

Click ***Next Setting***
![Screenshot8](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/b521878b-24d1-453d-b619-2d6a538b11c8)


In the ***Use localized subfolder names when redirecting Start Menu and My Documents*** window select ***Enabled***

Click ***Next Setting***
![Screenshot9](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/95ea9175-da98-4ea2-9e63-9f9cef56b498)


In the ***Redirect folders on primary computers only*** window select ***Disabled*** 

Click ***OK*** and close the ***Group Policy Management Editor*** window


Now back on the ***Group Policy Management*** window, select ***Folder Redirection*** and in the ***Folder Redirection*** pane click ***Add***
![Screenshot11](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/60c7eca6-4e15-45be-a9c7-4c38534f15e8)


In the ***Select User, Computer, or Group*** dialogue box type ***Folder Redirect*** in the ***Name*** field and click ***Check Names***, and the group we made earlier will be found

Click ***OK***
![Screenshot12](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/184885a5-a006-4203-8951-eee84738caeb)


Right-click the name of your domain and select ***Link an existing GPO*** select ***Folder Redirection*** and click ***OK*** and close the ***Group Policy Management*** window
![Screenshot13](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/a6ee93d7-934b-4ea5-b368-427e278a90ad)
![Screenshot14](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/071f4240-86b8-4365-ab96-27e609b8c7ef)


And now we will set up a home folder for the user we created. Minimize all windows that are currently open and open the ***File Explorer***
![Screenshot15](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/e7558aaf-b309-404e-a887-19fd040546f0)


In the ***File Explorer*** click ***Local Disk (C:)*** in the left-hand pane, right-click anywhere in the details pane, and select ***New > Folder***. Once created right-click the new folder and rename it to ***Home Folder testuser***
![Screenshot16](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/dbe51e11-b74e-4d79-a87e-c9fbc46c2564)
![Screenshot17](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/9fdc1890-e7b3-45ba-a74d-11cfe3ee88c7)


Right-click ***Home Folder testuser*** and select properties and then select the ***Sharing*** tab in the ***Home Folder testuser Properties*** dialogue box

Click ***Advanced Sharing***
![Screenshot18](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/cf3c3d3d-8d73-453c-8f40-46709501f6db)
![Screenshot19](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/63207d70-30fd-4828-b6a1-4a2b9f3abc0b)


In the ***Advanced Sharing*** dialogue box enable the ***Share this folder*** option and click ***Permissions***
![Screenshot20](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/4a1d105f-36b7-4d94-8fe0-4a26d50dd3c2)


Click ***Add*** in the Permissions for Home Folder testuser*** dialogue box and then type ***testuser*** in the ***Select Users, Computers, Service Accounts, or Groups*** dialogue box

Click ***OK***
![Screenshot21](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/7318ac08-1c75-462e-9e75-c9118840ae27)
![Screenshot22](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/64f2eabd-7e93-4962-80de-72e4156fa24d)


On the ***Permissions for Home Folder testuser*** dialogue box make sure that ***testuser*** is highlighted and enble ***Full Control*** in the ***Allow*** column below

Click ***OK*** and then click ***OK*** again on the ***Advance Sharing*** dialogue box
![Screenshot23](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/3eb5cdd3-988f-4209-9e32-7e79c92de6c5)
![Screenshot24](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/3eadf858-a9a3-49a8-a37a-913babac6fc3)


Now notice in the ***Home FOlder testuser Properties*** window the folder is now shared. Highlight the network path, right click it and select ***Copy***

CLose the ***Home Folder testuser Properties*** window
![Screenshot25](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/5ec5f4a8-dfc0-4171-a471-cbd92a08caeb)


Restore the ***Server Manager*** window from the taskbar and click ***Tools*** and select ***Active Directory Users and Computers***. Click the ***Users*** node and right-click ***testuser*** and select ***Properties***
![Screenshot26](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/1854746d-a4bc-4060-877f-9e5d03b9954e)
![Screenshot27](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/37c4b816-fb35-472c-9d58-6a5ad7c59b86)


In the ***testuser Properties*** dialogue box select the ***Profile*** tab
![Screenshot28](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/c56669d7-8dcb-4047-b0ef-aceffeed7cec)


In the ***Profile*** tab click the ***Connect*** option under the ***Home folder*** section and select an available drive letter and paste the network path that you copied from the ***Home Folder testuser Properties*** tab

Click ***OK*** and click ***OK*** for the ***Active Directory Domain Services*** pop-up as well
![Screenshot29](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/64a8ac5a-51e0-4ac4-93fd-4cf2a97b4b07)






























