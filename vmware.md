[ref1](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2013763)

```
C:\Users\wujie\AppData\Roaming\VMware\preferences.ini
```

```
To add the necessary flag to the Workstation preference.ini file: 
Ensure that all virtual machines are powered off and VMware Workstation is closed.
Navigate to folders below:
For most Windows - C:\Users\<username>\AppData\Roaming\VMware\
For Windows Vista, Windows 7, Windows Server 2008, Windows 8 and Windows Server 2012  - %USERPROFILE%\AppData\Roaming\VMware\
Open the preference.ini file using a plain text editor.
Add this line at the bottom of file:

pref.allowHideControls = "TRUE"

Save and close the file. 
Run this command to launch the virtual machine with controls hidden:

"C:\Program Files\VMware\VMware Workstation\vmware.exe" -B -q -x path_to_vmx"
```
