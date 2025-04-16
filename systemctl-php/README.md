# Issue

After upgrading arch linux recently, php-fpm was not able to write to folders, specifically in my `/home/web` subfolders.

# Root cause

Systemctl disallows write access to folders with the recent updates. Specifically, lighttpd has the ProtectHome set.

# Solution

Allow lighttpd to write to the folders via `systemctl edit lighttpd.service`:

Put the following:
```
[Service]
ReadWritePaths=/home/web/
```

and then restart the services via  `systemctl restart lighttpd; systemctl restart php-fpm.service`

# More info

For more info, check [here](https://wiki.archlinux.org/title/Systemd/Sandboxing)