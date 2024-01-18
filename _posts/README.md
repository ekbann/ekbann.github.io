#### Hello World!

This *website* is using Markdown. Let's see if the **H4 header** overrides the title... NO

Renamed *index.md* to *README.md*

```
for (i=0; i<10; i++) {
	printf("hello\n");
}
```

Another dream computer: **Sun Microsystems SPARCstation 20** (SS20)

- introduced March 1994 for US$12,195 (US$21,300 in 2020)
- 200MHz Ross hyperSPARC
- sun4m SuperSPARC architecture
- 512MB maximum RAM
- 2GB SCSI hard disk
- OpenBoot PROM cannot boot past the 2 gigabyte mark
- integrated 10baseT Ethernet
- 1280x1024x24 (8MB) framebuffer
- SunOS 4.1.3_U1B onwards or Solaris 2.3 to 9

Here's something useful: Setting up a new Git Repo

```
mkdir myDirName    #this is the name of your directory
cd /myDirName
git init
touch readME.md   #this is to create an initial file to push
git commit -m "enter commit message here"
git remote add origin git@github.com:YOUR_USERNAME/myDirName.git

curl -u USERNAME:PASSWORD https://api.github.com/user/repos -d '{"name":"myDirName"}' #this will create the repo in github.

# if you haven't generated and SSH key for github access then follow these steps, otherwise you're good to push your shit to github.
eval $(ssh-agent -s)
ssh-keygen -t rsa -b 4096 -C "email@yourdomain.com" #this should be your github email address
## you'll be prompted to a couple of times. Press enter for the first prompt. choose a passphrase for the second prompt, or press enter twice for no passphrase
ssh-add ~/.ssh/id_rsa   #this is your private key
cat ~/.ssh/id_rsa.pub   # copy the output of this command. this is your SSH public key
curl -u USERNAME:PASSWORD https://api.github.com/user/keys -d '{"title":"KEY_NAME", "key":"YOUR_RSA_PUBLIC_KEY_HERE"}'   #the value you copied earlier and your keyname. I recommend using a combination of machine name and app (My-laptop (Git CLI)
git push -u origin master
```

You can certainly change the order of steps and do the curl commands ssh generation first to create the repo and push the keys, but I used this flow just because.

That's it folks!
