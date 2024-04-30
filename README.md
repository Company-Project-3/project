1. What is the purpose of this custom Windows image creation and what are required
2. Step-by-step guide for creating images with MDT
3. Creating and customizing images with unnattend.xml-files
4. What we found and what to look out for
5. Custom windows installation will allow you to add and delete software, applications and drivers to your personalized operating system.

---

Software needed to create Microsoft Windows custom images:

-WinPE (Due to compatibility issues older version of WinPE was used in this project: https://go.microsoft.com/fwlink/?linkid=2120253 )

-WinADK
-MDT
-Virtual machine (Hyper-V was used in this example)
-x64 ISO image file ( Official Microsoft download link: https://www.microsoft.com/en-us/software-download/windows11 )

## 2. Step-by-step guide for creating images with MDT

Download Windows ADK (accesment and deployment kit)

- https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install

WinPE add-on(Preinstallation environment) :

- https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install

(Under that previously mentioned link you'll find the latest version of winPE at the end of the article)

Windows operating system as an ISO-file

- https://www.microsoft.com/en-us/software-download/windows11

And Virtual machine of your choise

<details>
<summary>  Installation guide  </summary>

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

We shall come back to this after adding applications to this custom image. In this example we are going to use Google Chrome installation bundle

https://support.google.com/chrome/a/answer/7650032?hl=en

After downloading the bundle, extract it from its compressed file and look for "installers"-folder. It should look like this and in this example we are going to use the "GoogleStandaloneEnterprise64.msi"-installer

![ChromeInstaller](https://github.com/Company-Project-3/project/assets/70267456/051ed9b1-e627-41a9-bfd9-7f614e15443a)

Create a new folder for it and move this installer there

![image](https://github.com/Company-Project-3/project/assets/70267456/1c6acdfa-2807-43ca-977f-5d854dee8326)

Go back to your WorkBench and add a new application

![image](https://github.com/Company-Project-3/project/assets/70267456/53a2c1a9-542f-403c-998e-359e8ba1b78d)

Choose "Application with source files"

![AppInstall1](https://github.com/Company-Project-3/project/assets/70267456/da5accf0-dde9-479d-a286-66c0ffb6f5c4)

Name the Application

![AppInstall2](https://github.com/Company-Project-3/project/assets/70267456/40980e39-55fa-440b-ad9e-9dd716c9043c)

Browse to the installer folder we previously created and give it here is a directory path

![AppInstallFolder](https://github.com/Company-Project-3/project/assets/70267456/b943b5b7-8006-4078-9b10-16d70546fdda)

Check that the application name is correct in "destination"-page.
On the "Command details"-page write the following command to install this software silently:

`msiexec /l GoogleChromeStandaloneEnterprise64.msi /qn`

![image](https://github.com/Company-Project-3/project/assets/70267456/aa171e4a-bd7c-43f7-b6a4-edd182cc1554)

Check that everything seems correct on "Summary"-page and click "Next". Let application wizard finish the job and now you should have an application in the "applications"-folder of WorkBench

![image](https://github.com/Company-Project-3/project/assets/70267456/93767ce9-2871-4147-a08b-e4d8732b966c)

In this "applications"-folder you can also check your applications properties, by right-clicking the application and adjust things like command line as well as on which platforms this app should run on.

![image](https://github.com/Company-Project-3/project/assets/70267456/361d7905-dfb4-4571-9521-168d524be7db)

Let's go back to "Task Sequences"-folder and check your task sequences properties

![TSProperties](https://github.com/Company-Project-3/project/assets/70267456/554dec0c-aefc-4098-ad7d-800e0e39fcd2)

## Task Sequences

Task sequence is a set of actions excuted in a linear order.

#### Create a new Task Sequence.

1. ![alt text](<Screenshot 2024-04-24 142617.png>)

- Input task ID sequence ID
- Input task seqence name
- input sequence comments(if any)
- Select the next icon

2. ![alt text](<Screenshot 2024-04-24 144308.png>)

- Select the Standard Client Task Sequence template.
- select the next icon

3. ![alt text](<Screenshot 2024-04-24 145319.png>)

- Select the needed opearting system.
- select the next icon

4. ![alt text](<Screenshot 2024-04-24 145619.png>)

- Specify a product key if applicable, for this task we opted for the **do not specify product key at this time** option.

5. ![alt text](<Screenshot 2024-04-24 151139.png>)

- Specify OS settings.
  - Add the Full name
  - Add your Organization
  - Add default browser page.
- Select the next icon

6. ![alt text](<Screenshot 2024-04-24 151537.png>)

- Specify the local admin password for the task sequence if applicable.
- Select the next icon

7. ![alt text](<Screenshot 2024-04-24 151608.png>)

- Confirm your selections in the summary
- Select the next icon
- Select the finish icon

8. ![alt text](<Screenshot 2024-04-24 151759.png>)

- Select the created task sequence and navigate to the properties page.
- Leave the general tab on the default settings page

**NOTE:** IF you have many task sequences you can disable the one that is not needed by toggling **the Enable this task sequence option**.

- Select the task sequence tab

9. ![alt text](<Screenshot 2024-04-24 151819.png>)

- On the task sequence page, you can toogle between each steps to activate or de-activate certain tasks.
- Expand the state restore option and select the windows update (pre-application installation), navigate to the options menu and tick the **Disable this step** option and apply changes
- Select the windows update (post-application installation), navigate to the options menu and tick the **Disable this step** option and apply changes.
- Select the OK icon.

</details>

<details>
<summary> Testing image in Virtual machine </summary>

This guide will tell you about setting up the image in virtual environment. We used Hyper-V manager as the Virtual machine, since it has kernel level access to host device and it was provided by Microsoft.

The ISO-image used in this example was previously built and renamed, but you'll learn where you can find the ISO-image you just created.

After Updating your deployment share, you should have this x64-iso image here in "Boot"-folder of your deployment share.

![Alt text](image.png)

Open your Virtual Machine manager, and start the installation process, by creating a new virtual machine. Screenshot taken in Hyper-V manager.

![Alt text](image-1.png)

Give your Virtual Machine a name, and choose a place to store it in your device

![Alt text](image-2.png)

Choose which generation of Virtual machine you want

![Alt text](image-3.png)

It is recommended to give atleast 2 megabytes of RAM to this device. In this tutorial I decided to give 4 MB of RAM

![Alt text](image-4.png)

Here you can choose whether your device should have internet connection or not. This can be changed later.

![Alt text](image-5.png)

Here you can choose how much memory your virtual device will have. For our case, 127 GB is enough

![Alt text](image-6.png)

This is the most important part, where we choose our operating system. This can be done later, but I'll add it here next.

![Alt text](image-7.png)

After checking your summary click "Finish" and let virtual machine manager set up the environment.

![StartButton](https://github.com/Company-Project-3/project/assets/70267456/13562c8a-6e5d-48f8-90e1-ddb97a897e57)

Now, by connecting to your device you will see a "start"-button. By clicking that button you will start the set up for your own custom Windows 11 image, and in this virtual environment you can test, and check out the features that you have added.

</details>

## 3. Creating and customizing images with unnattend.xml-files

### Tools

Windows Assessment and Deployment Kit ([ADK](https://learn.microsoft.com/en-us/windows-hardware/get-started/))

Windows Preinstallation Environment ([WinPE](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-intro?view=windows-11))

### Working with Answer files

Note: Example of autounattend.xml is added to this repository.

### Windows System Image Manager (SIM)

SIM helps with creation of Answer files (unattend.xml) that can be used to modify the Windows installation.

### Extract the official ISO

1. First thing first download the Windows ISO. [LINK](https://www.microsoft.com/software-download/windows11)
2. Extract ISO contents to some folder

### Automate windows setup

[microsoft docs: Automate Windows Setup](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/automate-windows-setup?view=windows-11)

[microsoft docs: Automate OOBE](https://learn.microsoft.com/en-us/windows-hardware/customize/desktop/automate-oobe)

<details>
<summary>Disable TPM, Secure boot and RAM checks</summary>

```xml
<settings pass="windowsPE">
    <component name="Microsoft-Windows-Setup" ... >
        <RunSynchronous>
            <RunSynchronousCommand wcm:action="add">
                <Order>1</Order>
                <Path>reg add HKLM\SYSTEM\Setup\LabConfig /v BypassTPMCheck /t REG_DWORD /d 1 /f</Path>
            </RunSynchronousCommand>
            <RunSynchronousCommand wcm:action="add">
                <Order>2</Order>
                <Path>reg add HKLM\SYSTEM\Setup\LabConfig /v BypassSecureBootCheck /t REG_DWORD /d 1 /f</Path>
            </RunSynchronousCommand>
            <RunSynchronousCommand wcm:action="add">
                <Order>3</Order>
                <Path>reg add HKLM\SYSTEM\Setup\LabConfig /v BypassRAMCheck /t REG_DWORD /d 1 /f</Path>
            </RunSynchronousCommand>
        </RunSynchronous>
    </component>
</settings>
```

</details>

<details>
<summary>Microsoft-Windows-International-Core-WinPE</summary>

```xml
<settings pass="windowsPE">
    <component name="Microsoft-Windows-International-Core-WinPE" ... >
        <UILanguage>en-US</UILanguage>
        <SystemLocale>en-US</SystemLocale>
        <UserLocale>fi-FI</UserLocale>
        <InputLocale>fi-FI</InputLocale>
        <UILanguageFallback>en-US</UILanguageFallback>
    </component>
</settings>
```

</details>

<details>
<summary>Microsoft-Windows-Setup UserData ProductKey AcceptEula</summary>

```xml
<settings pass="windowsPE">
    <component name="Microsoft-Windows-Setup" ... >
        <UserData>
            <ProductKey>
                <!-- generic product key to automate choosing Windows PRO license  -->
                <Key>VK7JG-NPHTM-C97JM-9MPGT-3V66T</Key>
                <WillShowUI>OnError</WillShowUI>
            </ProductKey>
            <AcceptEula>true</AcceptEula>
        </UserData>
    </component>
</settings>
```

</details>

<details>
<summary>Microsoft-Windows-Setup ImageInstall OSImage InstallTo</summary>

```xml
<settings pass="windowsPE">
    <component name="Microsoft-Windows-Setup" ... >
        <ImageInstall>
            <OSImage>
                <InstallFrom>
                    <MetaData wcm:action="add">
                        <Key>/IMAGE/INDEX</Key>
                        <Value>6</Value>
                    </MetaData>
                </InstallFrom>
                <InstallTo>
                    <DiskID>0</DiskID>
                    <PartitionID>3</PartitionID>
                </InstallTo>
                <WillShowUI>OnError</WillShowUI>
            </OSImage>
        </ImageInstall>
        <DiskConfiguration>
            <Disk wcm:action="add">
                <DiskID>0</DiskID>
                <WillWipeDisk>true</WillWipeDisk>
                <CreatePartitions>
                    <CreatePartition wcm:action="add">
                        <Order>1</Order>
                        <Type>EFI</Type>
                        <Size>100</Size>
                    </CreatePartition>
                    <CreatePartition wcm:action="add">
                        <Order>2</Order>
                        <Type>MSR</Type>
                        <Size>128</Size>
                    </CreatePartition>
                    <CreatePartition wcm:action="add">
                        <Order>3</Order>
                        <Type>Primary</Type>
                        <Extend>true</Extend>
                    </CreatePartition>
                </CreatePartitions>
                <ModifyPartitions>
                    <ModifyPartition wcm:action="add">
                        <PartitionID>1</PartitionID>
                        <Order>1</Order>
                        <Label>System</Label>
                        <Format>FAT32</Format>
                    </ModifyPartition>
                    <ModifyPartition wcm:action="add">
                        <Order>2</Order>
                        <PartitionID>2</PartitionID>
                    </ModifyPartition>
                    <ModifyPartition wcm:action="add">
                        <Order>3</Order>
                        <PartitionID>3</PartitionID>
                        <Label>OS</Label>
                        <Letter>C</Letter>
                        <Format>NTFS</Format>
                    </ModifyPartition>
                </ModifyPartitions>
            </Disk>
        </DiskConfiguration>
    </component>
</settings>
```

</details>

<details>
<summary>Bypass Microsoft account requirement</summary>

```xml
<settings pass="specialize">
    <component name="Microsoft-Windows-Deployment" ... >
        <RunSynchronous>
            <RunSynchronousCommand wcm:action="add">
                <Order>1</Order>
                <Path>reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\OOBE /v BypassNRO /t REG_DWORD /d 1 /f</Path>
            </RunSynchronousCommand>
        </RunSynchronous>
    </component>
</settings>
```

</details>

<details>
<summary>Microsoft-Windows-International-Core</summary>

```xml
<component name="Microsoft-Windows-International-Core-WinPE" ... >
    <UILanguage>fi-FI</UILanguage>
    <SystemLocale>fi-FI</SystemLocale>
    <UserLocale>fi-FI</UserLocale>
    <InputLocale>fi-FI</InputLocale>
    <UILanguageFallback>en-US</UILanguageFallback>
</component>
```

</details>

<details>
<summary>Microsoft-Windows-Shell-Setup/UserAccounts</summary>

```xml
<settings pass="oobeSystem">
    <component name="Microsoft-Windows-Shell-Setup" ...>
        <UserAccounts>
            <LocalAccounts>
                <LocalAccount wcm:action="add">
                    <Password>
                        <Value></Value>
                        <PlainText>true</PlainText>
                    </Password>
                    <Description>add local account</Description>
                    <DisplayName>user</DisplayName>
                    <Name>user</Name>
                    <Group>Administrators</Group>
                </LocalAccount>
            </LocalAccounts>
        </UserAccounts>
    </component>
</settings>
```

</details>

<details>
<summary>Microsoft-Windows-Shell-Setup/OOBE</summary>

```xml
<settings pass="oobeSystem">
    <component name="Microsoft-Windows-Shell-Setup" ... >
        <OOBE>
            <HideEULAPage>true</HideEULAPage>
            <HideOEMRegistrationScreen>true</HideOEMRegistrationScreen>
            <HideOnlineAccountScreens>true</HideOnlineAccountScreens>
            <HideWirelessSetupInOOBE>true</HideWirelessSetupInOOBE>
            <HideLocalAccountScreen>true</HideLocalAccountScreen>
            <ProtectYourPC>3</ProtectYourPC>
        </OOBE>
    </component>
</settings>
```

</details>

<details>
<summary>Microsoft-Windows-Shell-Setup/AutoLogon</summary>

```xml
<settings pass="oobeSystem">
    <component name="Microsoft-Windows-Shell-Setup" ... >
        <AutoLogon>
            <Username>user</Username>
            <Enabled>true</Enabled>
        </AutoLogon>
    </component>
</settings>
```

</details>

### Disable automatic updates

<details>
<summary>unattended.xml</summary>

```xml
<settings pass="oobeSystem">
    <component name="Microsoft-Windows-Shell-Setup" ... >
        <FirstLogonCommands>
            <SynchronousCommand wcm:action="add">
                <Description>disable automated updates</Description>
                <Order>2</Order>
                <RequiresUserInput>false</RequiresUserInput>
                <CommandLine>reg add HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU /v NoAutoUpdate /t REG_DWORD /d 1 /f</CommandLine>
            </SynchronousCommand>
        </FirstLogonCommands>
    </component>
</settings>
```

</details>

### Install 3rd party apps

Applications can be added to the ISO, after which they can be executed with unattended file.

1. Create directory for your applications in the extracted ISO contents directory
   ```ps
   MkDir c:\pathto\apps
   ```
2. Add your 3rd party application .EXE or .MSI installers to that directory
3. Use unattended to run the application installer in silent mode

   <details>
   <summary>unattended.xml</summary>

   ```xml
   <settings pass="oobeSystem">
       <component name="Microsoft-Windows-Shell-Setup" ... >
           <FirstLogonCommands>
               <SynchronousCommand wcm:action="add">
                   <Description>install Firefox</Description>
                   <Order>1</Order>
                   <RequiresUserInput>false</RequiresUserInput>
                   <CommandLine>D:\apps\FirefoxSetup124.0.2.exe /S</CommandLine>
               </SynchronousCommand>
           </FirstLogonCommands>
       </component>
   </settings>
   ```

   </details>

### Removing Preinstalled Applications

#### Option 1: Powershell during OOBE with unattended

during OOBE you can use PowerShell with unattended file to remove applications.

<details>
<summary>unattended.xml</summary>

```xml
<settings pass="oobeSystem">
    <component name="Microsoft-Windows-Shell-Setup" ... >
            <SynchronousCommand wcm:action="add">
                <Description>remove clipchamp</Description>
                <Order>3</Order>
                <RequiresUserInput>false</RequiresUserInput>
                <CommandLine>powershell.exe Remove-AppxPackage Clipchamp.Clipchamp_2.2.8.0_neutral__yxz26nhyzhsrt</CommandLine>
            </SynchronousCommand>
        </FirstLogonCommands>
    </component>
</settings>
```

</details>

#### Option 2: Mounting Image with DISM

Alternatively, you can mount the image and remove applications with DISM.

1. Get index for desired Windows image:
   ```ps
   dism /get-imageinfo /ImageFile:"C:\pathto\sources\install.wim"
   ```
2. Create folder for where to mount the image:
   ```ps
   MkDir c:\mount
   ```
3. Mount windows image (index 6 for Pro image):
   ```ps
   dism /Mount-Image /ImageFile:"C:\pathto\sources\install.wim" /Index:6 /MountDir:"C:\mount"
   ```
4. List all applications in the mounted image:
   ```ps
   dism /Image:C:\mount /Get-ProvisionedAppxPackages
   ```
5. Remove unwanted applications:
   ```ps
   dism /Image:C:\mount /Remove-ProvisionedAppxPackage /PackageName:Clipchamp.Clipchamp_2.2.8.0_neutral_~_yxz26nhyzhsrt
   ```
6. Unmount the image and commit changes:
   ```ps
   dism /Unmount-Image /MountDir:"C:\mount" /Commit
   ```

These modifications are now baked into your install.wim

### Build the custom ISO with Oscdimg

Note: Needs to be ran in Deployment and Imaging Tools Environment

```ps
Oscdimg -m -o -u2 -udfver102 -bootdata:2#p0,e,b"C:\pathto\boot\etfsboot.com"#pEF,e,b"C:\pathto\efi\microsoft\boot\efisys.bin" "C:\pathto\" "C:\CustomWin11.iso"
```

## 4. What we learnt, errors and unused features

In this session you will learn about potential unused features and common errors you might encounter

- Server usability in this environment

  - It is possible to deploy this to a server which has workdomain, but it would defeat the goal of **silent** installation of software.

  ![Server](https://github.com/Company-Project-3/project/assets/70267456/3ee71c43-47c9-4a54-9f06-2375a5ea74da)

- Errors regarding setting up this environment
- Windows Home edition isn't recommended
  - Windows 10 home is limited with its customization capabilities and it is also missing some key features that are present on other versions of Windows.
  - One of the biggest things missing from this operating system was Hyper-V Virtual machine support.
- Using Third-party software to create images

  - We've also explored the possibility to create images with not-Microsoft supported applications, mainly NTlite.
  - https://www.ntlite.com/

  <details>
    <summary>Screenshots of NTlite</summary>

  </details>

  - This software made creating custom images much more simplistic with their drag-and-drop app installation and we could also just disable Windows own pre-installed applications
