<h1>1. Homework M1: Introduction to Windows Server</h1>
Main goal is to do a test installation of Windows Server 2016/2019/2022 Standard Core
<h2>Machine specifications</h2>

Create a virtual machine with the following parameters:
1. 1 vCPU
2. 1024 MB RAM
3. 32 GB HDD (thin provisioned)
4. 1 Network card

<h2>Post-installation tasks</h2>

After the installation you should tune the following parameters:
1. Set the name of the host to: SRV-CORE
2. Set the workgroup to WSA
3. Change the time zone to Bulgaria
4. Create new administrator user named *admin* with password *Password* and full name Admin

<h1>2. Solution</h1>

<h2>Create Virtual Machine in Hyper-V</h2>

+  Open Hyper-V Manager
+  Initiate new VM creation by clicking on Action > New > Virtual Machine or by picking the same option, but from the actions section on your right
+  Click Next
+  Specify a name for the VM. Click Next
+  Choose either Generation 1 or Generation 2 (generally speaking, Generation 1 virtual machines are BIOS based,
while Generation 2 are UEFI based) and click Next
+  Set the amount of Startup memory to the desired value or accept its default value of 1024MB and click Next
+  Leave the Connection parameter to Not Connected and click Next
+  Size of the virtual hard disk make 32 GB
+  Click Next
+  On the summary screen, click Finish

<h2>Solution, following the PowerShell principles, could be:</h2>

+  Rename the computer with:<br>
*Rename-Computer -NewName "SRV-CORE" -Restart*
+  Change the workgroup with:<br>
*Add-Computer -WorkGroupName "WSA" -Restart*
+  In order to check what are the valid options for a time zone we must execute:<br>
*Get-TimeZone -ListAvailable*
+  Then to set the desired time zone we can execute:<br>
*Set-TimeZone -Name "FLE Standard Time"*
+  As first step we create a user with password set in an interactive way:<br>
*New-LocalUser -Name "admin" -FullName "Admin" -Password (ConvertToSecureString -AsPlain "Password" -Force)*
+  Then we make it a member of the Administrators group:<br>
*Add-LocalGroupMembers -Group "Administrators" -Member "admin"*
