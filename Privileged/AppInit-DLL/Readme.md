# AppInit DLL

⇒ &nbsp;&nbsp;AppInit DLL, like AppCert DLLs are also loaded when a new process is created and its settings reside in the registry key on the location below `"HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Windows"`

<img src="https://imgur.com/vUQ0dXh.png" height="40%" width="75%" alt="AppInit-DLL Steps"/>

⇒ &nbsp;&nbsp;As shown above its value is empty & disabled by default. To enable it we need to assing a path to our payload binary to it, furthermore we also need to set LoadAppinit_DLL's value to 1 (by default is 0)

## How It Works
⇒ &nbsp;&nbsp;During process creation, intrestingly use32.dll library is the one responsible for checking whether or not LoadAppinit_DLL's value is to 1, if so it'll attempt to load those DLLs from that value  
<img src="https://imgur.com/86HwZEQ.png" height="40%" width="75%" alt="AppInit-DLL Steps"/>

⇒ &nbsp;&nbsp;For this, we can use any DLL, but we have to be mindful of the once that call createprocess function to launch our payload, we need to avoid them in order to avoid infinite loop of process created since the process created will also load our dll and create another process and on and on eventually leading to a system crash.  

## Abuse
⇒ The first step is to add the path to our DLL as a value to AppInit_DLLs. For this we'll use the command syntax below:  
```cmd
      ◇ reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Windows" /V "AppInit_DLLs" /T REG_SZ /D "c:\rto\pers\implant\implant.dll" /F
```
<img src="https://imgur.com/BMlQ8YS.png" height="40%" width="75%" alt="AppInit-DLL Steps"/>

⇒ Next we need to enable LoadAppinit_DLL's that is responsible for loading of our DLL by setting its value to 1 using the command syntax below:  
```cmd
      ◇ reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Windows" /V "LoadAppInit_DLLs" /T REG_DWORD /D "0x1" /F
```

<img src="https://imgur.com/Rsqxe3S.png" height="40%" width="75%" alt="AppInit-DLL Steps"/>

<img src="https://imgur.com/V6zewUi.png" height="40%" width="75%" alt="AppInit-DLL Steps"/>

⇒ &nbsp;&nbsp;Now if we launch any process and inspect its loaded DLLs we find that our DLL is loaded as well for example with ProcessHacker as shown below  

<img src="https://imgur.com/3uZBU4g.png" height="40%" width="75%" alt="AppInit-DLL Steps"/>

## CleanUp
⇒ &nbsp;&nbsp;To clean we just revert the changes we made back to how they were using the two commands below
<img src="https://imgur.com/HWAKl62.png" height="40%" width="75%" alt="AppInit-DLL Steps"/>


























