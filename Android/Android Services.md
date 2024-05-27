A service is an application component that can allow for long running code to run in the background. There are 3 types of services. Background, Foreground and Bound. 

A service runs on the main thread of its hosting process. It does not run in a different thread. 

## Background
A background services is a service that only runs when an app is running and isn't directly noticed by a user.
## Foreground
A foreground service performs some operation that is noticeable to the user, such as a music player. Foreground services must display a notification, even when the user isn't interacting with the app.

Note the [[WorkManager]] API offers away of scheduling tasks, and is able to run these as foreground services if needed. 
## Bound
A bound service is a service that only runs when all components its bound to are destroyed. A bound service offsets a client-server interface that components can use to interact with the service, send request, get results.

## Background Execution limits
When an app is in the foreground it can create and run both foreground and background services freely. When an app goes into the background however it has a window of several minutes in which it is allowed to create and use services. At the end of this window, the app is considered idle. This acts as if the app had called `Service.stopSelf()` its self. Foreground services will continue running even after the app is considered idle. 

Temporally an app maybe put on an allow list allowing it to freely launch background operation, as in the case of: 
- Handling a high priority Firebase Cloud Messaging (FCM) message
- Receiving a broadcast, such as an SMS MMS message
- Executing a pending intent from a notification
- Starting a VPNService before the VPN app promotes itself to the foreground
