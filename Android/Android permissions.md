To do certain tasks within android you may require permissions. This provides transparency on what sensitive functionality an app has access to, helping support user privacy. 

On android, there are install permissions and runtime permissions.
## Install time permission
Install time permissions are granted automatically when the user installs your app. These permissions are defined in the apps manifest. These permissions show on the app store on the apps details page. Typically install time permissions are for things that minimally affect the system and provide minimal risk to users privacy. 

Note: Permissions defined by an app sharing the same signature are granted signature permissions which is a type of runtime permission.
## Runtime permission

Runtime permissions are permissions that are requested as the app is running, and are granted by the user. Runtime permissions request access to restricted data/ functionality, or lets your app perform actions that substantially affect the system. 

Runtime permissions in android can be requested by the app, which prompts the user to grant the permission or not. 

When designing an app, you should try and only disable functionality due to permissions when absolutely necessary. For example, a weather forecast app may want to get access to the users location to show them the weather forecast for their local area, if the user however denys this permission, the app can still function, showing weather for a given location the user inputs. 

There is various ways an permission might be granted, and you shouldn't assume that since you where granted a permission once, it will always be granted. for example: 
A permission can be granted while the app is in use, blocking the permission for background operations. 
A permission may be only granted for a one time user
A permission may be revoked from the app in the settings
