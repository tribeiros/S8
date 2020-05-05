# S8 restart itself on doze and standby
This issue is caused by a malfunction on android Power management on samsung S8  

First some links how about it works, and last, how to resolve this issue  


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
This link explain adb shell dumpsys  
https://developer.android.com/studio/command-line/dumpsys

## Resolve Issue
To **Resolve** this issue is necessary an application with enable wakelock function for you S8 dont enter in doze mode  
Because the issue occurred when S8 is on `doze` mode and enter in a `maintenance window`

### How to
I used termux application on this tutorial, because termux have easy access to this feature for non dev IT dudes  

Install termux on playstore  
Open termux  
In terminal type it `termux-wake-lock`

#### What termux-wake-lock do | developer section
```
#!/bin/sh

if [ $# != 0 ]; then
	echo 'usage: termux-wake-lock'
	echo 'Acquire the Termux wake lock to prevent the CPU from sleeping.'
	exit 1
fi

am startservice \
	--user 0 \wa
	-a com.termux.service_wake_lock \
	com.termux/com.termux.app.TermuxService \
	> /dev/null
```

After this, your S8 will scape `doze mode` when the display turn off and lock, and dont will restart itself anymore  
This is necessary every time your phone reboot or shutdown, unless you have root privilegies, termux-boot or adb shell  
There are other ways with `adb shell` like this  https://www.xda-developers.com/stop-wakelocks-android-without-root/


## Conclusion
Waiting for samsung resolve this issue, meanwhile ...
