# Winlogon (shell & userinit)

⇒ &nbsp;&nbsp;Winlogon as a persistence technique is quite popular amoung adversaries.

⇒ &nbsp;&nbsp;We can find its configuration on the following location of the registry key `"HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon"`  

⇒ &nbsp;&nbsp;On this registry we are actually intrested on two of its values which are `shell` & `userinit` 

<img src="https://imgur.com/YlyJ0FH.png" height="65%" width="75%" alt="modified services Steps"/>

## Abuse
⇒ &nbsp;&nbsp;We can abuse this entries since they can store more than one value

⇒ &nbsp;&nbsp;As a proof of concept lets first add our payload binary to the shell key, but before this we need to ensure our payload is in the system32 directory since we can only specify the name and not the full path. For this we can make use of the command below:  
```cmd
      ◇ reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon" /V "Shell" /T REG_SZ /D "explorer.exe,implant.exe" /F  
```

<img src="https://imgur.com/IDlALmq.png" height="65%" width="75%" alt="modified services Steps"/>

<img src="https://imgur.com/QpSOuBL.png" height="65%" width="75%" alt="modified services Steps"/>

⇒ &nbsp;&nbsp;As an alternative we can target userinit entry by editing the value to also point to our payload's path as shown below:

<img src="https://imgur.com/QucCwLv.png" height="65%" width="75%" alt="modified services Steps"/>

<img src="https://imgur.com/nFNdpvj.png" height="65%" width="75%" alt="modified services Steps"/>

## CleanUp
⇒ &nbsp;&nbsp;To clean we just revert the changes we made back to how they were using the two commands below:
<img src="https://imgur.com/Ipa4SQG.png" height="65%" width="75%" alt="modified services Steps"/>

<img src="https://imgur.com/qP0n46P.png" height="65%" width="75%" alt="modified services Steps"/>

































