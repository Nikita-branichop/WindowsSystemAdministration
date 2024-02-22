<h1>1. Homework M2: Basic Services and Components</h1>
<h2>Software and Services Management</h2>

1. Download the service archive from http://example.com/file.zip
You can use the following (sample) command wget -Uri http://example.com/file.zip -OutFile
C:\Temp\file.zip
2. Extract it to a folder, for example C:\WSAService
You can use the following command Expand-Archive -LiteralPath C:\Temp\file.zip -DestinationPath C:\
3. Install the WSAService.exe service
4. Start the WSAService
5. Check / show the content of the C:\WSA.log file
<h2>Disk Management</h2>

1. Create new disk with thin provision and size of 10 GB, and attach it to the VM
2. Initialize the disk with GPT partition style
3. Create one partition (approx. 60%)
4. Assign letter X
5. Format it with NTFS file system and set the label to Disk-NTFS
6. Create second partition (the remaining space)
7. Assign letter Y
8. Format it with FAT32 file system and set the label to Disk-FAT32
<h2>Network Management</h2>

1. Rename your first adapter to NET-Internet
2. Rename your second network adapter to NET-Local
3. Set the profile of first adapter to Public
4. Set the profile of second adapter to Private
5. Set 192.168.220.1 as IP address of the second adapter
6. Set MAC address of the second adapter to AA-BB-CC-DD-EE-FF
7. Enable firewall rule to allow ping
8. Reset MAC address of the second adapter to its factory value

<h1>2. Solution</h1>
<h2>Software and Services Management</h2>

+  Download the file from a remote URL:<br>
*wget -Uri http://example.com/file.zip -OutFile
C:\WSAService.zip*
+  Because we don't know what is inside the archive, we can extract its content to a temporary location first:<br>
*Expand-Archive -Path WSAService.zip -DestinationPath C:\temp*
+  Then, we can enter the destination folder and inspect what is there:<br>
*cd temp*
+  Now, check what we have here:<br>
*dir*
+  It appears that the result of the extraction process is a WSAService folder. Let's move it to C<br>
*Move-Item -Path WSAService -Destination C*
+  Install the service by creating a definition for a new service:<br>
*New-Service -Name WSAService -BinaryPathName C:\WSAService\WSAService.exe*
+  Start the service:<br>
*Start-Service WSAService*
+  Check if there is C:\WSA.log file and what it contains:<br>
*Get-Content C:\WSA.log*

<h2>Disk Management</h2>

+  After we created and attached the virtual hard disk and the machine is up and running, we could start
PowerShell and check the disks that the OS sees:<br>
*Get-Disk*
+  Then we can initialize the newly added disk:<br>
*Initialize-Disk -Number 1 -PartitionStyle GPT*
+  Next, we can create a 6GB partition:<br>
*New-Partition -DiskNumber 1 -Size 6GB*
+  And assign a drive letter:<br>
*Set-Partition -DiskNumber 1 -PartitionNumber 2 -NewDriveLetter X*
+  As final step we must format it:<br>
*Format-Volume -DriveLetter X -FileSystem NTFS -NewFileSystemLabel Disk-NTFS*
+  Now we can create one more partition:<br>
*New-Partition -DiskNumber 1 -UseMaximumSize*
+  Then assign a letter:<br>
*Set-Partition -DiskNumber 1 -PartitionNumber 3 -NewDriveLetter Y*
+  And finally, we can format it:<br>
*Format-Volume -DriveLetter Y -FileSystem FAT32 -NewFileSystemLabel Disk-FAT32*

<h2>Network Management</h2>

+  As very first step we can check installed network adapters:<br>
*Get-NetAdapter*
+  Then we can continue with renaming of the first adapter:<br>
*Rename-NetAdapter -Name "Ethernet" -NewName "NET-Internet"*
+  Now the second one:<br>
*Rename-NetAdapter -Name "Ethernet 2" -NewName "NET-Local"*
+  Change profile of the first adapter:<br>
*Set-NetConnectionProfile -InterfaceAlias "NET-Internet" -NetworkCategory Public*
+  Then on the second:<br>
*Set-NetConnectionProfile -InterfaceAlias "NET-Local" -NetworkCategory Private*
+  Set IP address:<br>
*New-NetIPAddress -InterfaceAlias "NET-Local" -IPAddress 192.168.220.1 -
PrefixLength 24*
+  Change MAC address:<br>
*Set-NetAdapter -Name "NET-Local" -MacAddress AA-BB-CC-DD-EE-FF*
+  Enable firewall rule:<br>
*Enable-NetFirewallRule -Name FPS-ICMP4-ERQ-In*
+  Reset MAC address:<br>
*Set-NetAdapter -Name "NET-Local" -MacAddress ""*
