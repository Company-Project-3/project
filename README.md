## Tools
Windows Assessment and Deployment Kit ([ADK](https://learn.microsoft.com/en-us/windows-hardware/get-started/)) 

Windows Preinstallation Environment ([WinPE](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-intro?view=windows-11))


## Working with Answer files
Note: Example of autounattended.xml is added to this repository.
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




