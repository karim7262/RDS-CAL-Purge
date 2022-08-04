# RDS-CAL-Purge
RDS CAL Full Perge Steps for Windows Server


Remove RDS CALs from RDS Server
Posted on August 31, 2017 by Managed WordPress Migration User
Background

There are many circumstances where you will need to remove a RDS CALs from an RDS Server, or in some cases you want to rebuild the entire RD licensing database.  Microsoft allows you to remove an individual CAL license pack using powershell, or rebuild the entire database.  However, if neither of those work, it’s quite easy to manually rebuild the RD licensing database.  I’ve included directions for all 3 methods below, and have tested this on Windows Server 2008, 2008R2, 2012, 2012R2, and 2016.

Remove An Individual RDS CAL License Pack Using Powershell (User or Device CAL)

Open powershell elevated as an administrator
Type the following command to list the RDS Licenses and note the KeyPackID
Alternatively, open RD Licensing Manager and note the Keypack ID
Get-WmiObject Win32_TSLicenseKeyPack
Run the below command to remove the licenses pack from your RD Server
Replace KEYPACKID with the number you obtained above
wmic /namespace:\\root\CIMV2 PATH Win32_TSLicenseKeyPack CALL UninstallLicenseKeyPackWithId KEYPACKID

 

Rebuild the RD Licensing Database
Microsoft provides directions on how to do this automatically, via a web browser, or via the phone:

https://technet.microsoft.com/en-us/library/dd851428.aspx

 

Manually Rebuild the Licensing Database (Guaranteed to Work if the Previous 2 methods Fail)

Make sure you have documentation of your MS License agreement that includes Authorization number, License number, License type (User/Device CAL), and Quantity before proceeding
Stop the Remote Desktop Licensing service
Stop Remote Desktop Licensing Service

Rename C:\Windows\System32\lserver\TLSLic.edb to C:\Windows\System32\lserver\TLSLic.old
Start the Remote Desktop Licensing service
All licenses will now be cleared out of RD Licensing Manager, and you’ll need to re-install the licenses you want to add back in
