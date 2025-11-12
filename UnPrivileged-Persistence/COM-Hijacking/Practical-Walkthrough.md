<h1>COM Hijacking (Practical-Walkthrough)</h1>

First just like in DLL-Hijacking we need to enumerate for a hijackable COM Object  

Our Payload candidate should be triggered either automatically or triggered by user, registry-runkey or task-schedular ocassionally

On most occasions good candidates for COM Hijacking can be found in task-schedular   

So we need to extract all information about tasks in an xml file format with the command below  
      ◇ <mark>schtasks /query /xml > Path\To\Saved.xml</mark>  
      
From the xml output we are looking for two conditions    

Exec section should have `ComHandler` as an entry   

Triggers section should have `LogonTrigger` as an entry for persistence
