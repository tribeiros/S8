# S8 restart itself on doze and standby
This issue is caused by a malfunction on android Power management on samsung S8  

First some of links about how it works, and last, how to resolve this issue  


### Power Management
This link explain how to android management the power
https://developer.android.com/about/versions/pie/power

### Doze & standby
This link explain how to android work on doze and standby, its here on S8 restart itself
https://developer.android.com/training/monitoring-device-state/doze-standby


### WakeLock
This link explain how wakelock works
https://developer.android.com/reference/android/os/PowerManager.WakeLock

### Wakelock adb shell
https://developer.android.com/studio/command-line/dumpsys

## Resolve Issue
**Resolve** this issueis necessary an application enable wakelock function for you S8 dont enter in doze mode  
Because the issue occurred when S8 is on `doze` mode and enter in a `maintenance window`

### How to
I used termux application because termux have easy access a this feature

Install termux on playstore  
Open termux  
In terminal type it `termux-wake-lock`

After this, your S8 will scape `doze mode` when the display off and lock, this is necessary every time your phone reboot or shutdown  
There are other ways with `adb shell` like this   https://www.xda-developers.com/stop-wakelocks-android-without-root/


## Conclusion
Waiting for samsung resolve this issue, meanwhile ...
