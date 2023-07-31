![what-is-active-directory-and-why-is-it-used](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/2facaf12-f88b-414f-b128-109c98a993f9)

# Creating-a-Home-Folder (OracleVM VirtualBox)
This tutorial will walk you through the steps of creating a Home Folder using Active Directory within a VirtualBox VM environment

## Environments and Technologies Used
- OracvleVM Virtual Box
- Active Directory Domain Services
- Group Policy Management

## Operating Systems Used
- Windows Server 2019
- Windows 10 (22H2)

## Configuration Steps
In this lab, we will walk through the process of creating a home folder for a user. We will:
- Create a user
- Create a Group Policy Object for the folder redirection
- Apply rules and permissions to that security group
- Create a folder that will be shared on the network
- Redirect the user's data location to the network share drive

This method of storing data centralizes the management of a user's files by storing them on a server instead of on their local machine. So in case they accidentally delete a file or can no longer access it, a system administrator can backup their lost data. And if the user uses a laptop that is often taken home and is not connected to the network, you can apply certain settings that allow them to make changes to their files offline and update to the server when it is connected to the network.



Okay, so we are going to log into our DC as an administrator, and we will open the server manager application and select ***Tools*** in the top right-hand corner, and then select ***Active Directory Users and Computers*** from the drop-down menu.
![Screenshot1](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/00bec27e-df56-47d0-9d65-3d54731fb6a0)


In the ***Active Directory Users and Computers*** window, right-click any blank space there is in the details pane to the right and select ***New*** and then select ***Group***
![Screenshot0](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/e3baa9c0-982a-4062-bf3c-0ee6e3dae239)


In the ***New Object-Group*** dialogue box, type "Folder Redirect" into the ***Group name*** field

Click ***OK***
![Screenshot01](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/cefc873a-79ef-48ef-99bf-5c8c9d007e54)


In the ***Active Directory Users and Computers*** window, right-click any blank space there is in the details pane to the right and select ***New*** and then select ***User***
![Screenshot2](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/10e5a82b-6fc5-47cd-89d7-24246d971e1c)


In the ***New Object-User*** dialogue box, type "testuser" into the ***First name*** and ***User logon name*** fields

Click ***Next***
![Screenshot3](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/52c2b11c-25e0-469a-b9fb-03a19d7ebeeb)


Type "Password1" into the ***Password*** and ***Confirm Password fields (This isn't the strongest password I know, but this is just for demonstration purposes). Then disable ***User must change password at next logon*** and enable ***Password never expires*** 

Click ***Next***
![Screenshot4](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/aaeea923-2931-482b-9441-e1999889655b)


Click ***Finish***
![Screenshot5](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/ee6cca69-0c13-451b-bb64-ddfbb4f5a588)


Now, back on the ***Active Directory Users and Computers*** window, right-click the group we just created, ***Folder Redirect***, and select ***Properties***
![Screenshot6](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/42a4232e-b6ec-43b9-a7cf-e1ca0e38fd35)


From the ***Folder Redirect Properties*** dialogue box, select the ***Members*** tab and click ***Add***
![Screenshot7](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/9ed81855-adc4-41c2-b184-6e2e64886c67)


In the ***Select Users, Contacts, Computers, Service Accounts, or Groups*** dialogue box, type "testuser" in the ***Enter the object names to select*** field and click ***Check Names*** and click ***OK***
> The user's username will populate once you click the ***Check Names*** button
![Screenshot8](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/85daaca3-fddc-46bc-8ffa-bf7876fccbf9)


The user ***testuser*** is now added as a member of the ***Folder Redirect*** group

Click ***OK***
![Screenshot9](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/47780a89-23b7-4004-93b2-e6a36ffad4d9)


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

Click ***OK***


Now on the ***Group Policy Management Editor*** under ***User Configuration*** expand the nodes ***Policies***, ***Windows Settings***, and click ***Folder Redirection***. We will select the ***Documents*** folder to be redirected to the home folder. Right-click the ***Documents*** folder and select ***Properties***
![Screenshot030](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/d3917c7a-6347-4db2-af5c-55e917b37c2e)


In the ***Documents Properties*** dialogue box select ***Basic -  Redirect everyone's folder to the same location*** setting option and under ***Root Path*** type ***\\\yourserver\home folder testuser***

Click ***OK***


Click ***Yes*** on the ***Warning*** pop-up
![Screenshot932](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/cea8dcf3-6391-4271-9d34-39e0ebb52da0)


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


Now notice in the ***Home Folder testuser Properties*** window the folder is now shared. Highlight the network path, right click it and select ***Copy***

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

<!---
Now we will restore the ***Server Manager*** from the taskbar click ***Tools*** and select ***Group Policy Management***
![Screenshot030](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/753b2a49-3026-4fa1-be32-14a385fa802d)
--->

Now we are going to perform a gpupdate on that users machine, but before that we are going to check the location of ***testuser's*** document folder. Log in to your client machine as ***testuser*** and open up the ***File Explorer*** right-click ***Documents*** and select ***Properties***
![Screenshot933](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/475566a6-2eb1-447e-8808-2ae4d0b95022)


In the ***Documents Properties*** dialogue box click ***Location*** and notice that the location of the folder is in the user's account
![Screenshot944](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/69622187-0ec7-4b01-9fe2-f423ac826c69)


Right-click the Windows ***Start*** charm and open ***Windows PowerShell***
![Screenshot935](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/1436cf5a-590b-47c0-af00-e086761c6b18)


In the ***Windows PowerShell*** window type the command ***gpupdate /force*** to update all group policy changes that have been made

Press ***Enter***
![Screenshot936](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/a874383e-d31f-4fbd-a825-1f978dd22875)


For the warning that is displayed in Windows PowerShell after running the gpupdate type ***Y***. This warning is basically stating that the user must be logged out before certain policies can be applied.
![Screenshot937](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/6ed30b75-a4c3-4226-ba53-d6360e135e33)


Once logged back in as testuser we are will check the location of the ***Documents*** folder by opening ***File Explorer*** from the taskbar right-clicking the ***Documents*** folder and selecting ***Properties***
![Screenshot938](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/026d793b-9b3c-4e6e-9365-218d879ae807)


In the ***Documents Properties*** dialogue box click ***Location*** and now you can see that the folder's location has changed to ***\\\yourserver\home folder testuser\Documents***
![Screenshot939](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/b4d88a2a-63a3-40a3-aed0-9b85d3e4f3df)







<!---
In the ***Settings-About*** scroll down and select ***Advanced system settings***
![Screenshot31](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/0cfabeb8-bb54-4747-a2da-dc8470196d68)


In the ***System Properties*** dialogue box select the ***Remote*** tab and click ***Select Users***
![Screenshot32](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/0db9eb93-a435-49fd-93d7-43e7043669ba)


Click ***Add*** on the ***Remote Desktop Users*** tab and type ***testuser*** in the ***Enter Object Name to Select*** field and click ***Check Names***

Click ***OK*** on the ***Select Users or Groups***, ***Remote Desktop Users***, and ***System Properties*** windows
![Screenshot33](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/a69cb9a4-fffa-468e-9856-1c31d9d78126)


Right-click on the Windows ***Start*** charm and select ***Sign-out***
![Screenshot34](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/b34a7723-2da8-4b0c-8d8d-d463d03584eb)


On the sign-in screen select ***Other user*** in the bottom left and use the username ***testuser*** and the password you assigned to the account
![Screenshot35](https://github.com/Brandon-Baker11/Creating-a-Home-Folder/assets/140644499/4fe5414d-7652-4848-ac23-8636ac7c50cc)
--->














































