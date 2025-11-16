# Modified Services
⇒&nbsp;&nbsp; This technique involves setting up persistance via `windows services`  
⇒&nbsp;&nbsp; For this technique we can either create a new service or modify an existing one   
⇒&nbsp;&nbsp; Note that by default when we create a service it'll be running as `LocalSystem`  

## Abuse

### Creating a Service
From an elevated shell we need to invoke the simple command below to create the service & the one after to query it  
```cmd
sc create <service_name> binpath="Path\To\Payload.exe"
```
<img src="https://imgur.com/qZukMih.png" height="40%" width="75%" alt="modified services Steps"/>

```cmd
sc query <service_name>
```
<img src="https://imgur.com/y0asCFo.png" height="40%" width="75%" alt="modified services Steps"/>

We start the services with the command
```cmd
sc start <service_name>
```
<img src="https://imgur.com/oVKBY8e.png" height="40%" width="75%" alt="modified services Steps"/>

⇒&nbsp;&nbsp; As seen from the command output above our service started but immedietly stopped, this is because our payload binary isn't a service & therefore cannot be understood by the `SCM` leading to a crash  
⇒&nbsp;&nbsp; To bypass this hurdle we need to generate a service payload & it so happens i have the perfect `Source-Code` for this in my archives which i've provided above

<img src="https://imgur.com/Qp8Gy46.png" height="80%" width="75%" alt="modified services Steps"/>

<img src="https://imgur.com/RsYcT9G.png" height="80%" width="75%" alt="modified services Steps"/>

Now with the compatible binary we re-create the service. Note that the spaces before binpath & start-type are vital
```cmd
 sc create UpdateService binpath=" path\to\implantsrv.exe" start= auto
```
<img src="https://imgur.com/4E2ORhZ.png" height="40%" width="75%" alt="modified services Steps"/>

Finally we start the service 
```cmd
 sc start UpdateService
```
<img src="https://imgur.com/c1ekiPX.png" height="40%" width="75%" alt="modified services Steps"/>  

And after the specified sleep time we can confirm our implant service was executed and is running 

<img src="https://imgur.com/qmyvKIO.png" height="40%" width="75%" alt="modified services Steps"/>

### Modifying a Service
If good opsec is our goal we can modify an existing service using sc.exe tool with the config command
<img src="https://imgur.com/6XWPeeU.png" height="40%" width="75%" alt="modified services Steps"/>
