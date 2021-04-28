---

title: "What to do when Linux becomes unresponsive"

date: 2019-03-26T08:47:11+01:00

draft: false

---

One of the biggest Questions I had as a new linux user
was about what exactly to do when your Linux system 
hangs up.

If you find yourself in a similar situation, 
try using these steps.


## xkill


 If the GUI is still responding, killing programs are really easy. If you are in an X enviornment, open up a terminal and type

```sh
xkill
```
If you are not able to open a terminal, 
most Operating Systems has a handy shotcut 

```bash
Ctrl+Alt+Esc
```

When executed, the cursor changes to a skull and crossbones or to an X mark.

Hover the cursor above the window to be killed and click on it, it will be instantly killed.

![xkill.gif](/assets/gifs/xkill.GIF)

## TTYs 


If your GUI is not working, the next best methord is to log into a tty and kill
the application form there.

What are tty's? 
check out [this](http://www.linusakesson.net/programming/tty/index.php) article to get a better understanding of them.

To log into one, use the shortcut 

```bash
Ctrl+Alt+F2
```

While there, you'll be greeted with a login screen.
Enter your username and passsword.

![tty.gif](/assets/gifs/tty.GIF)

After you get into it, you'll get a shell to work with.
You could execute all the commands you do in a terminal emulator here.

Now, use a command line process manager like top or htop and send a sigterm to kill the process which is hanging up your system.

![htop.gif](/assets/gifs/htop.gif)

## The holy Kernel

If all else fails, you could directly talk to the Linux Kernel from your keyboard.


For terminating all processes, use 

```bash
Alt+SysRq+E
```

The SysRq key is the same as the PrintScreen Key.

For Rebooting the system, use

```bash
Alt+SysRq+B
```

Here is a list of some usefull commands :

|Alt+SysRq+ | 	Action| 	Uses|
|    :---    |    :----:   |    :---    |
|E 	|Term 	|Sends SIGTERM signal to all processes.|
|
|I 	|Kill 	|Kills (sends SIGKILL signal to) all processes.|
|
|B 	|Reboot 	|Will immediately reboot without syncing or unmounting any disks. Before using this use Alt+SysRq+S and Alt+SysRq+U to avoid data loss.|
|
|O 	|PowerOff 	|Turns off the computer without syncing or unmounting disks. Before using this use Alt+SysRq+S and Alt+SysRq+U to avoid data loss.|
|
|N 	|Nice 	|Make real-time processes nice-able.|
|
|H 	|Help 	|Prints some help|
|
|R 	|UnRaw 	|Turns off keyboard raw mode. This allows input from the keyboard even if X-Window has crashed.|
|
|S 	|Sync 	|Attempts to sync all filesystems. This lessens the chance of data loss and fscking. Syncing is complete when "done" or "OK" is printed.|
|
|U 	|Umount 	|Attempts to remount all filesystems as read-only. Umounting is complete when "done" or "OK" is printed.|
|
|P 	|ShowPc 	|Attempts to dump all registers and pointers to console.|
|
|T 	|ShowTasks 	|Attempts to dump a list of all tasks to console.|
|
|M 	|ShowMemoryInfo 	|Displays memory info to console|
|
|F 	|OOM |Kill 	Calls oom_kill to kill a memory hog process|

For an extensive list of these SysReq functions, check out [this](https://en.wikipedia.org/wiki/Magic_SysRq_key) 
wikipedia article.

Most distributions disable the access to some of SysRq functions via 
key combinations.

To check what are the available functions in your run this 
command in your terminal.

```bash
cat /proc/sys/kernel/sysrq

16
```

A number would be displayed to the console.

|Number |  Info  |
|    :---    |    :---    |
|0 | disable sysrq completely |
|1 | enable all functions of sysrq |
|2 | enable control of console logging level |
|4 | enable control of keyboard (SAK, unraw) |
|8 | enable debugging dumps of processes etc. |
|16 | enable sync command |
|32 | enable remount read-only |
|64 | enable signaling of processes (term, kill, oom-kill) |
|128 | allow reboot/poweroff |
|256 | allow nicing of all RT tasks |

If you wish to change the SysReq value, you can do so.
But be very carefull if you decide to enable it.

To change the SysReq value, first deicide on which value to 
change it to.
For this example, I'm using the the value 4

```bash
sudo echo 4 > /proc/sys/kernel/sysrq 
```

To check if the changes are saved, run the cat command again

```bash
cat /proc/sys/kernel/sysrq

4
```

You should get the value you supplied earlier.

### Conclusion

Thanks for sticking around till the end!
If you liked this read, share it to your friends.

### References

1. <https://linuxconfig.org/how-to-enable-all-sysrq-functions-on-linux>
2. <https://sites.google.com/site/syscookbook/rhel/rhel-sysrq-key>
3. <https://en.wikibooks.org/wiki/Linux_Guide/Freezes>



