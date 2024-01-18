# HOW-TO: DropBox

#### Dropbox Headless Install via command line

The Dropbox daemon works fine on all 32-bit and 64-bit Linux servers. To install, run the following command in your Linux terminal.

32-bit:

`cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86" | tar xzf -`

64-bit:

`cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -`

Next, run the Dropbox daemon from the newly created `.dropbox-dist` folder.

`~/.dropbox-dist/dropboxd`

#### How to run Dropbox daemon in background?

When you run `~/.dropbox-dist/dropboxd` — Dropbox works and stuff. Problem is that when I close terminal or, even worse — reboot, Dropbox stops working and I need to run that daemon again.

How can I have the computer automatically start that daemon in the background?

If you're running the daemon from your own account, start it at boot time with **Cron**. Run `crontab -e` to edit your crontab file and add the line

`@reboot ~/.dropbox-dist/dropboxd`

