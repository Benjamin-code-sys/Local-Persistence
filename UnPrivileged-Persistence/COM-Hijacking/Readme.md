<h1>Component Object Model Hijacking</h1>
 
COM-Hijacking modifies a Windows COM registration so a malicious DLL/EXE is loaded when a legitimate application instantiates the COM class.  

It's effective because it runs during normal app usage (stealthy) and persists without obvious startup artifacts; defenders should monitor COM registration changes and unexpected DLLs, enforce code-signing/integrity, and restrict write access to COM/registry locations.

COM is a platform-independent, distributed, object-oriented system for creating binary software components that can interact with each other 

In simple terms COM is a dedicated system for developers to create libraries that can co-operate with other applications developed in other languages  

In example a developer can create a DLL written in C++ that can be used by a C# application  

COM has the following features:  
  
      ◇ Language Agnostic  -   Since it ensures the apps are compatible on binary level
      ◇ Application Binary interface (ABI)  -    Since it ensures the apps are compatible on binary level
      ◇ Complicated & Powerful
      ◇ Usually lives in DLL, sometimes as a EXE
      ◇ Recognised using GUID (Class ID)
      ◇ Can live on a remote machine without the application knowing

<h2>COM Loading (In process)</h2>

This is the process where by the COM Objected is implimented as a DLL

<h2>Abuse</h2>

When an Application that uses COM functionality is launched it'll call from OLE32.DLL Library either of these two Functions with a specific GUID of the COM it needs  
        ◇ CoCreateInstance()  
        ◇ CoGetClassObject()

Then OLE32.DLL passes this request of accessing the COM Object to the Sevice Control Manger (SCM)
   
SCM will take this info and begin querying the HKEY_CLASSES_ROOT registry which is actually composed of infomation from both HKEY_CURRENT_USER hive & HKEY_LOCAL_MACHINE hive

So first from the HKEY_CLASSES_ROOT registry hive it queries if the COM Object from the GUID provided exists in the HKEY_CURRENT_USER under the Classes directory from the software directory
 
If its not found then it'll Query the same Classes directory from the software directory in the HKEY_LOCAL_MACHINE hive

If found it'll take the information from the registry key which is usually a Path-To-DLL which wll then be loaded to the Application, hence enabling the application to call the functions embeded in that DLL

<img src="https://imgur.com/yWDwMWd.png" height="60%" width="45%" alt="COM Hijacking Steps"/>  <img src="https://imgur.com/jiF2r8d.png" height="60%" width="45%" alt="COM Hijacking Steps"/>

<img src="https://imgur.com/UpPfb2C.png" height="60%" width="45%" alt="COM Hijacking Steps"/>  <img src="https://imgur.com/kupM6L8.png" height="60%" width="45%" alt="COM Hijacking Steps"/>

<h2>COM Hijacking (Methodology)</h2>

From the COM-Loading process we as non admins can hijack step four when its querying the HKEY_CURRENT_USER hive and place our malicious custom COM Object that points to our malicious DLL since we have modify permissions in this registry hence the process will look like this:

<img src="https://imgur.com/ICqYP8t.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<h2>COM Loading (Local Server)</h2>

This is when the COM is implemented as an EXE   
Steps of abuse is pretty much the same as that of In-Process as shown in the fig below  

<img src="https://imgur.com/IuItIeT.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<h2>COM Loading (Remote Server)</h2>

This process of loading is diffrent in a way that Local SCM will call the Remote-Machine SCM via Remote Procude Call requesting the COM Object it needs as shown in the fig below

<img src="https://imgur.com/Zm214cS.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<h1>COM-Objects Location (In-Registry)</h1>

 COM Objects are usually find in either of these three hives in the Registry key  
      ◇ HKEY_CLASSES_ROOT  
      ◇ HKEY_CURRENT_USER  
      ◇ HKEY_LOCAL_MACHINE  

For example in the HKEY_CLASSES_ROOT hive under the CLSID directory each Class ID (which is unique to itself) hold information about a path to a binary, so when queried by an application it'll provide that path to the application   

<img src="https://imgur.com/1MC3tZQ.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

 In HKEY_CURRENT_USER hive under the Classes directory from the software directory, we'll find a CLSID directory with a short list of GUIDs 
<img src="https://imgur.com/07ActOE.png" height="70%" width="70%" alt="COM Hijacking Steps"/>

<img src="https://imgur.com/Y5NOwza.png" height="70%" width="70%" alt="COM Hijacking Steps"/>










































