A user can kill a process by using the application manager under the settings.

The System can also kill a process when it needs to free up ram. The likelihood of this depends on the state of the process. You can see these likelihoods below:

| Likelihood of being killed | Process state | Activity State |
| -------------------------- | ------------- | -------------- |
| Lowest                     | Foreground    | Resumed        |
| Low                        | Visible       | Started        |
| Higher                     | Background    | Stopped        |
| Highest                    | Empty         | Destroyed      |

The system never kills an [[Android Activity|Activity]] to free up ram but instead kills the process that runs it, destroying not only the activity but everything else in that process as well. 
[See more](https://developer.android.com/guide/components/activities/activity-lifecycle#asem)