<h1>PowerShell-automation-on-administrative-tasks</h1>


<h2>Description</h2>
This repository contains PowerShell scripts developed to automate common IT administrative tasks on Windows systems. It includes automation for system event monitoring, user management, file backups, and network configuration. The project demonstrates practical scripting skills to streamline IT operations and enhance system management efficiency.
<br />


<h2>Languages and Utilities Used</h2>

- PowerShell – Primary scripting language for automating IT tasks
- Batch (CMD) – For launching scripts or basic system commands (if applicable)
= Windows Script Host (WSH) – Underlying engine for script execution (implicit)
- Visual Studio Code or Notepad – For script development and editing
- Windows Event Viewer – For event log analysis (referenced in the script logic)
- VirtualBox – To run the Windows VM environment for testing
- Windows 11 Pro – Operating System environment for running and testing scripts


<h2>Environments Used </h2>

- <b>macOS Ventura 13.7.4</b> (21H2)
- Hypervisor: VirtualBox (for running the Windows VM)
- Windows 11 Pro Virtual Machine
- PowerShell Terminal
- Notepad (or any basic text editor)

<h2>Step-by-Step Explanation:</h2>

<p align="center">
On Windows, open the Notepad (or any basic text editor). Type the below mentioned script inside the Notepad then select File in Notepad and click on Save As:

#Script to monitor system events for security logs
$BeginTime = (Get-Date).AddHours(-24)
Get-EventLog -LogName Security -After $BeginTime |
Where-Object { $_.EntryType -eq "SuccessAudit" -or $_.EntryType -eq "FailureAudit" } |
Select-Object TimeGenerated, EventID, EntryType, Message | Format-Table -AutoSize |
Out-File "$env:USERPROFILE\Desktop\SecurityLogReport.txt": <br/>
<img src="https://i.imgur.com/wqzxf9M.png"/>
<br />
<br />
Select Desktop and name the file MonitorSystemEvents.ps1 and click on Save to save it:  <br/>
<img src="https://i.imgur.com/WchZSdU.png"/>
<br />
<br />
Type PowerShell on the search menu and right-click on its icon to select Run as administrator: <br/>
<img src="https://i.imgur.com/VLKIio4.png"/>
<br />
<br />
Run the following command to navigate to the script location:

cd $HOME\Desktop <br/>
<img src="https://i.imgur.com/idjb7na.png"/>
<br />
<br />
Run the following command to execute the script:

.\MonitorSystemEvents.ps1  <br/>
<img src="https://i.imgur.com/psUhV53.png"/>
<br />
<br />
Minimize the PowerShell window and browse for a file named SecurityLogReport.txt containing the filtered security events:  <br/>
<img src="https://i.imgur.com/SLPY0rd.png"/>
<br />
<br />
Next step, analyze methods to optimize user management. Click Start, type PowerShell Ise and Run as Administrator:  <br/>
<img src="https://i.imgur.com/PXE2Qcc.png"/>
<br />
<br />
Click on the New Script icon on the top left side of PowerShell to open a new script:  <br/>
<img src="https://i.imgur.com/bO2RLUQ.png"/>
<br />
<br />
Type the following script to add multiple users, set their passwords, and assign them to groups, then click File and save it in Desktop as ManageUsers.ps1:

#Script to add and remove users

$Users = @(
    @{ Name = "JohnDoe"; Password = "P@ssw0rd1"; Group = "Administrators" },
    @{ Name = "JaneSmith"; Password = "P@ssw0rd2"; Group = "Users" }
)

#Add new users
foreach ($User in $Users) {
    New-LocalUser -Name $User.Name -Password (ConvertTo-SecureString $User.Password -AsPlainText -Force)
    Add-LocalGroupMember -Group $User.Group -Member $User.Name
}
 <br/>
<img src="https://i.imgur.com/xeXzxAR.png"/> 
<br />
<br />
Run the program to execute the script: 

.\ManageUsers.ps1  <br/>
<img src="https://i.imgur.com/Db9RFPu.png"/>
<br />
<br />
Next step, create a streamlined process for file management. Click on File Explorer in the menu tab to create a dummy data folder:  <br/>
<img src="https://i.imgur.com/1TslN9U.png"/>
<br />
<br />
Navigate to This PC and open C Drive then right-click on blank space and select New and click on Folder. Name the folder as ImportantFiles and save it:  <br/>
<img src="https://i.imgur.com/UXTYDVi.png"/>
<br />
<br />
Navigate back to PowerShell and type the following script to implement file backup, the save it in Desktop as BackupFiles.ps1:

#Script to backup files
$SourceDir = "C:\ImportantFiles"
$BackupDir = "D:\Backups\$(Get-Date -Format 'yyyy-MM-dd')"

#Create backup directory
New-Item -ItemType Directory -Path $BackupDir -Force
Write-Host "Backup directory created at: $BackupDir"

#Copy files
Copy-Item -Path "$SourceDir\*" -Destination $BackupDir -Recurse -Force
Write-Host "Files copied from $SourceDir to $BackupDir"

<br/>
<img src="https://i.imgur.com/0jgLuCT.png"/>
<br />
<br />
Run the following command to execute the script of backing up files of the C drive to the D drive having the current date:

.\BackupFiles.ps1  <br/>
<img src="https://i.imgur.com/sCPsHqk.png"/>
<br />
<br />
Next step, design an approach for network configuration, on Powershell ISE write the script for performing network configuration then save it on Desktop as ConfigureNetwork.ps1:

#Script to configure network settings
$InterfaceAlias = "Ethernet"
$IPAddress = "192.168.1.100"
$SubnetMask = "255.255.255.0"
$DefaultGateway = "192.168.1.1"
$DNSServer = "8.8.8.8"

#Set IP address and gateway
New-NetIPAddress -InterfaceAlias $InterfaceAlias -IPAddress $IPAddress -PrefixLength 24 -DefaultGateway $DefaultGateway

#Set DNS server
Set-DnsClientServerAddress -InterfaceAlias $InterfaceAlias -ServerAddresses $DNSServer
<br/>
<img src="https://i.imgur.com/JAHFY4S.png"/>
<br />
<br />
Run the following command to execute the script that updates the network adapter settings with the new IP configuration:

.\ ConfigureNetwork.ps1  <br/>
<img src="https://i.imgur.com/Y15iKMV.png"/>
<br />
<br />
Run the following command to verify the new changes:

ipconfig 
Get-NetIPAddress <br/>
<img src="https://i.imgur.com/CctaBKX.png"/>
<img src="https://i.imgur.com/KRpEREu.png"/>
<br />
<br />
This project showcases the automation of essential IT administrative tasks using PowerShell, including user management, file backups, event monitoring, and network configuration.
A foundational step toward building secure, efficient, and scalable IT environments through scripting.</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
