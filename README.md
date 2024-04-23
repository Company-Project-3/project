1. What is the purpose of this custom Windows image creation and what are required
2. Creating custom images with MDT
3. Creating and customizing images with unnattend.xml-files
4. What we found and what to look out for


1. 
Custom windows installation will allow you to add and delete software, applications and drivers to your personalized operating system.

Software needed to create Microsoft Windows custom images:

	
 -WinPE (Due to compatibility issues older version of WinPE was used in this project: https://go.microsoft.com/fwlink/?linkid=2120253 )

-WinADK
	
 -MDT
	
 -Virtual machine (Hyper-V was used in this example)
	
 -x64 ISO image file ( Official Microsoft download link: https://www.microsoft.com/en-us/software-download/windows11 )

2.
Download Windows ADK (accesment and deployment kit)
	- https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install
WinPE add-on (Preinstallation environment)
	- https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install
 	(Under that previously mentioned link you'll find the latest version of winPE at the end of the article)
Windows operating system as an ISO-file
	-  https://www.microsoft.com/en-us/software-download/windows11
And Virtual machine of your choise


Open Deployment Workbench

![MDT-WorkBench](https://github.com/Company-Project-3/project/assets/70267456/efb00053-3b97-4859-9752-95b075fe2a2c)

Create Deployment Share

![CreateDeploymentShare](https://github.com/Company-Project-3/project/assets/70267456/af1743ed-e8ac-4948-8b85-159355054a73)

For completely automated process we recommend you uncheck every box here

![DeploymentOptions](https://github.com/Company-Project-3/project/assets/70267456/9404db91-ea5e-4b24-899d-7ea710b10cea)

After creating the Deployment Share we need to mount the Windows Operating system ISO-file 

![MountImage](https://github.com/Company-Project-3/project/assets/70267456/7e01ee72-985b-4296-af2a-31aa2b2a17c5) 

Mounted Image should appear as a DVD-drive

![ImageAsADrive](https://github.com/Company-Project-3/project/assets/70267456/1ce39b43-a232-4987-9ed3-f9c446e5d9ae)

Let's go back to WorkBench and add this operating system to be customized

![ImportOS](https://github.com/Company-Project-3/project/assets/70267456/8cb9ebb0-5761-481a-9fff-840e0f9635e5)

Choose "Full set of source files" 

![FullSetOfSF](https://github.com/Company-Project-3/project/assets/70267456/7d7c67fc-57c8-4839-9bb9-b9fb7b1e8533)

This Mounted operating system should appear under "This PC" as a DVD-drive

![ThisPC](https://github.com/Company-Project-3/project/assets/70267456/212e02a8-b31c-4cb8-b541-6632e0c4c585)

You can name this operating system whatever you want under the "Destination Directory Name", but automatically it will choose one of the available Windows operating systems randomly and name it after one of those.

On the "Summary"-view you should click "Finish" and let the "Import operating system wizard" finish the rest.

After adding your operating system your "Operating systems"-folder should have updated

![UpdatedOSFolder](https://github.com/Company-Project-3/project/assets/70267456/11f7fd74-1212-4a27-b53d-47a3d98781c8)

Next we will add a "Task sequence"

![AddTaskSequence](https://github.com/Company-Project-3/project/assets/70267456/95ab8a34-d7b5-4d52-a61f-2f62b64d30f1)

Again you can name the file whatever you want, but the Task sequence ID should be something you can remember easily

![NameTaskSequence](https://github.com/Company-Project-3/project/assets/70267456/1db519f4-e6e3-4608-80c2-815eae985214)

We will be using "Standard Client Task Sequence" as template 

![TaskSequenceTemplate](https://github.com/Company-Project-3/project/assets/70267456/03faffd5-ef13-4e5b-ba8b-28b7078c76d1)

Choose whatever Windows 11-operating system you want, except "Home"

![ChooseOS](https://github.com/Company-Project-3/project/assets/70267456/6a59a830-2546-4ce7-b1ce-7591001597d9)

We do not want to add a product key. 

![NoProductKey](https://github.com/Company-Project-3/project/assets/70267456/b3320d72-ced4-4dc0-8fb3-6cd974998df6)

You can choose your own credentials here for the "User" and the "Organization"

![OSSettings](https://github.com/Company-Project-3/project/assets/70267456/26656fb3-d072-4809-9737-009340ab14ec)

Do not specify Admin Password 

![AdminPassword](https://github.com/Company-Project-3/project/assets/70267456/2872709b-bbe9-474b-8242-aebfe8323681)

After "Summary" click "Next" and let Task Sequence Wizard finish the job. After this You should have a new task sequence in this list

![TaskSequenceList](https://github.com/Company-Project-3/project/assets/70267456/dfe7f2f9-600e-4c72-b090-d8787dda6c4a)







