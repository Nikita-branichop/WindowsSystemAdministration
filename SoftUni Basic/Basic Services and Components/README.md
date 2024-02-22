<h1>Homework M2: Basic Services and Components</h1>
<h2>Software and Services Management</h2>
Main goal is to download, install, and start a 3rd party service on a Windows Server 2016/2019 Standard.
You are expected to do the following tasks:
1. Download the service archive from https://zahariev.pro/files/WSA-M2-Service.zip
You can use the following (sample) command wget -Uri http://example.com/file.zip -OutFile
C:\Temp\file.zip
2. Extract it to a folder, for example C:\WSAService
You can use the following command Expand-Archive -LiteralPath C:\Temp\file.zip -DestinationPath C:\
3. Install the WSAService.exe service
4. Start the WSAService
5. Check / show the content of the C:\WSA.log file
Disk Management
Main goal is to add, initialize, and partition additional hard drive on a Windows Server 2016/2019 Standard.
You are expected to do the following tasks:
1. Create new disk with thin provision and size of 10 GB, and attach it to the VM
2. Initialize the disk with GPT partition style
3. Create one partition (approx. 60%)
4. Assign letter X
5. Format it with NTFS file system and set the label to Disk-NTFS
6. Create second partition (the remaining space)
7. Assign letter Y
8. Format it with FAT32 file system and set the label to Disk-FAT32
Network Management
Main goal is to try several of the network related cmdlets on your own. For the purpose of the lab, you can use
Windows Server 2016/2019 Standard with two network cards. One (first) connected to your existing network (nat,
bridge) and another (second) connected to an internal network.
You are expected to do the following tasks:
1. Rename your first adapter to NET-Internet
2. Rename your second network adapter to NET-Local
3. Set the profile of first adapter to Public
4. Set the profile of second adapter to Private
5. Set 192.168.220.1 as IP address of the second adapter
6. Set MAC address of the second adapter to AA-BB-CC-DD-EE-FF
7. Enable firewall rule to allow ping
8. Reset MAC address of the second adapter to its factory value
