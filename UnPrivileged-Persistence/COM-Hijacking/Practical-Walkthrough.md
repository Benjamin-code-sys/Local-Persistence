<h1>COM Hijacking (Practical-Walkthrough)</h1>

First just like in DLL-Hijacking we need to enumerate for a hijackable COM Object  

Our Payload candidate should be triggered either automatically or triggered by user, registry-runkey or task-schedular ocassionally

On most occasions good candidates for COM Hijacking can be found in task-schedular   

So we need to extract all information about tasks in an xml file format with the command below  
      ◇ <mark>schtasks /query /xml > Path\To\Saved.xml</mark>  
      
From the xml output we are looking for two conditions    

Exec section should have `ComHandler` as an entry   

Triggers section should have `LogonTrigger` as an entry for persistence

<img src="https://imgur.com/Jz4DwgA.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<img src="https://imgur.com/dfpPexC.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

Then we query the registry to see how this COM Object looks with the command below  
       ◇ <mark>reg query "HKCR\CLSID\{97D47D56-3777-49FB-8E8F-90D7E30E1A1E}"</mark>

<img src="https://imgur.com/462j4At.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<img src="https://imgur.com/NaxbX2H.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

To determine in which hive the COM Object is actually found we query both the Current User & Local machine as shown below

<img src="https://imgur.com/ckdNEZO.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<img src="https://imgur.com/8KSrYFb.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

From the above result its quite obvious that we can hijack this COM Object by placing a malicious one in the `HKEY_CURRENT_USER` hive

<mark>Note</mark> that microsoft requires every COM Object to export atlease one function, for our case specifically DllGetClassObject function which is exported from a `.def` file

<img src="https://imgur.com/biNIj84.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<h2>Abuse</h2>

We first need to export the original COM Object to disk with the command below  
<mark> reg export "HKLM\software\classes\CLSID\{97D47D56-3777-49FB-8E8F-90D7E30E1A1E}" New\Path\To\Reg_Orig.reg /reg:64 /y</mark>

<img src="https://imgur.com/WvW1dYV.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<img src="https://imgur.com/RLEN1n7.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

We need to complile our custom `DLL Source-Code` shown below fior it to proxy over to the original WorkFoldersShell.dll after running our malware trojan as shown below

<img src="https://imgur.com/tVm07b1.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

We need to modify the reg file we imported in step one by changing its location to point to our malicious custom DLL & also to be save in the `HKEY_CURRENT_USER` registry hive so that it becomes hijackable

<img src="https://imgur.com/N9TNWDk.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

 Finally we need to import the registry file as is to the registry with the command below then confirm by querying the registry  
   ◇ <mark>reg import Reg_Orig.reg /reg:64</mark>

<img src="https://imgur.com/ktqU9kx.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<img src="https://imgur.com/BJSHoEZ.png" height="70%" width="70%" alt="COM Hijacking Steps"/>












































