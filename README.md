
This is the traditional _"Last login:"_ message on steroids!

Parses the output from [`last`](http://man7.org/linux/man-pages/man1/last.1@@util-linux.html) and displays the following data:

 * The date and host of your last login that is now closed (alternatively, a notice if this is your first time logging in)
 * The list of all sessions that are still logged in
 
The library also includes the ability to print the host names in a more "friendly" format; instead of printing out something non-descriptive like `Last login from dsl-123-53.geneseo.net`, you can adjust the script to print `Last login from work` instead. See `friendly-hostnames` for more details.

The script ignores all non-remote connections, and _only_ displays the last connections via `ssh` (or whatever other types of connections that are logged to `/var/log/wtmp`, such as `getty/login` and `ftpd`). Connections such as `ssh localhost` will show up in the history, while opening up a terminal window on the machine will not.

All of these features should make spotting "unwanted" connections **much** easier.

### Example output:

Let's connect to this computer, then disconnect again immediately:

```
$ ssh localhost
[localhost] Welcome to Ubuntu 13.10 (GNU/Linux 3.11.0-23-generic i686)
[localhost] $ exit
$ last-login
Last logged in 3 seconds ago from this computer
```

In this case, it looks like I forgot to log out of my SSH session at work:

```
$ last-login
Last logged in 3 hours ago from home
You are still logged in on the following machines:
  * Logged in 2 hours ago from work on pts/17
```

Uh oh, I don't recognize that host name; looks like some "malicious user" logged into my server without my knowledge. Better change my password!

```
$ last-login
Last logged in 3 days ago from 172.56.2x.yz
```


