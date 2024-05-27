As a user uses, leaves, and returns to your app, an [[Android Activity|activity]] transitions through various states. This is the activity lifecycle. 

![[Pasted image 20240522235618.png]]
## onCreate 
Upon activity creation, onCreate is called. When creating an activity you must extend onCreate, and this is where your initialisation logic belongs.
## onStart
When an activity enters the started state, the system invokes onStart. This happens when the activity is being prepared to become visible and enter the foreground. After the onStart is completed, the activity moves to the resumed state. 
## onResume
When the activity enters resumed state, it comes apart of the foreground and onResume is invoked. This is the state in which the activity can now be interacted with by the user. 
## onPause
On pause is the first indication that the user intends to leave the activity, although this does not mean the activity is being destroyed, simply that it is going out of the foreground. A paused activity may still be visible. If the activity enters back into the foreground from this state, it enters the resume state.

On pause is a good opportunity to free system resources that are not tied to UI. 
## onStop
On stop indicates that the activity is now no longer visible or in use by the user. 

on stop is a good opportunity to free system resources, no matter if they are tired to the UI or not, as the UI is no longer visible. 

From onStop an activity will either enter [[#onRestart]] or onDestroy depending on weather the user navigates back to an activity or the activity is destroyed.
## onDestroy
on destroyed is called before an activity is destroyed. This happens when the user dismisses an activity, `finish()` being invoked or when the system destroys it temporarily.

An activity is destroyed temporarily in the case of device rotation or entering multi window mode. In these cases the activity will be completely recreated with the new config, calling [[#onCreate]]

It is best practice to use a view model, that would be given to the newly created activity for the previously mentioned scenerio. A view models onCleared will be called instead if an activity is not being recreated. 

On destroy also releases all resources not cleaned up by on stop. 
## onRestart 
Called after onStop when an activity is being redisplay to the user. This will be followed by an [[#onStart]] and [[#onResume]]