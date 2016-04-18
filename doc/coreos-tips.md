# CoreOS Tips

### CoreOS Reboot

CoreOS is set to update automatically.  This means the server will seemingly 'randomly' reboot itself.

A proper way to deal with this would be to implement a restart strategy.  We've chosen to deal with this by preventing the machine from rebooting after an update.  The assumption is that you will be manually rebooting the system to take advantage of these updates (some of which are security improvements).

To 'turn off' reboot, you'll need to modify the ```/etc/coreos/update.conf``` file. 

Change the contents to look something like this:

```
GROUP=stable
REBOOT_STRATEGY=off
```

To apply these changes:

```
sudo systemctl restart update-engine
```

Don't think that simply setting your containers to restart automatically will solve the problem - you'll still have the issue of your data storage drives being detached.

### Attack logging

When logging into CoreOS, you may be 'lucky' enough to notice a series of entries documenting login attempts.  The most likely assumption is that you were attacked.  The system logs data such as the IP the login attempt came from, and the port that it tried to access.

First... check to make sure that the attackers were not successful.  Use Google.  I don't know how to determine this other than checking your server traffic for abnormalities.

Second, to clear this list so that you do not see it every time you Putty in to your server, run:

```
sudo systemctl reset-failed
```
