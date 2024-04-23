1. What is the purpose of this custom Windows image creation and what are required
2. Creating custom images with MDT
3. Creating and customizing images with unnattend.xml-files
4. What we found and what to look out for


1. 
Custom windows installation will allow you to add and delete software, applications and drivers to your personalized operating system.

Software needed to create Microsoft Windows custom images:
	-WinPE (The latest version of WinPE doesn't support Windows 11. Download link to WinPE version used in this example: https://go.microsoft.com/fwlink/?linkid=2120253 )
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








