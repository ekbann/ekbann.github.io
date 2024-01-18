# HOW-TO: Plerd

After following the [normal installation](https://github.com/jmacdotorg/plerd), I have encountered a few problems which required a few extra steps.

```
$ sudo apt install cpanminus
$ cpanm Plerd
```

After the long compilation and installation I found out that `plerdall` was not in my command path. A simple `find` found it at `/home/username/perl5/bin` so we simply edit `~/.bashrc` and add the following line at the end:

```
export PATH="/home/ebann/perl5/bin:$PATH"
```

Restart your terminal shell and check your path:

```
$ echo $PATH
/home/username/perl5/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
```

Try `plerdall` again:

`$ plerdall --init`

>**Can't locate Plerd.pm in** @INC (you may need to install the Plerd module) (@INC contains: **/home/username/perl5/bin/../lib** /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.32.1 /usr/local/share/perl/5.32.1 /usr/lib/x86_64-linux-gnu/perl5/5.32 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.32 /usr/share/perl/5.32 /usr/local/lib/site_perl) at /home/username/perl5/bin/plerdall line 13.
BEGIN failed--compilation aborted at /home/username/perl5/bin/plerdall line 13.

Notice the highlighted path for the `@INC` variable. `plerdall` expects to find `Plerd.pm` at `/home/username/perl5/bin/../lib` which is simply `/home/username/perl5/lib`. Let's take a look there:

```
$ la ~/perl5/lib/
perl5
```

Nope. Not there but there is another sub-directory `perl5`. Let's check that one:

```
$ la ~/perl5/lib/perl5/
5.32.0        Coerce    HTML     Module          ok.pm     Specio      Term                           YAML
5.32.1        Data      HTTP     Mojo            Package   Specio.pm   Test                           YAML.pm
App           DateTime  JSON     Mojolicious     Params    Spiffy      Test2                          YAML.pod
AppConfig     Devel     JSON.pm  Mojolicious.pm  Path      Spiffy.pm   Test2.pm
AppConfig.pm  Dist      Log      Mojo.pm         Plerd     Spiffy.pod  Text
auto          Eval      match    MooseX          Plerd.pm  String      URI
Carp          ExtUtils  Method   MooX            Safe      Sub         Web
Class         File      MIME     ojo.pm          Scope     Sysadm      x86_64-linux-gnu-thread-multi
```

There it is! Let's move everything inside `~/perl5/lib/perl5/` back to `~/perl5/lib/`:

```
$ cd ~/perl5/lib/perl5/
$ mv * ../
```

Now let's try `plerdall` one last time:

```
$ plerdall --init
No directory provided, so using default location
(/home/username/Dropbox/plerd).
I have created and populated a new Plerd working directory at
/home/username/Dropbox/plerd. Your next step involves updating the
configuration file at /home/username/Dropbox/plerd/plerd.conf.
For full documentation, links to mailing lists, and other stuff, please
visit http://plerd.jmac.org/. Enjoy!
```

Success!

## Usage

Configure the webserver of your choice such that it treats the docroot subdirectory (which you created as part of the first step) as your new blog's own docroot.

When running in its basic mode, Plerd does not provide a webserver; it simply generates static HTML & XML files, ready for some other process to serve up.

Run `plerdall` with no arguments to initially populate your blog's docroot, and at any other time you wish to manually regenerate your blog's served files.

`plerdwatcher` runs a daemon that monitors the Dropbox-synced source directory for changes, republishing files as necessary.

To start writing a new blog post, just create a new Markdown file somewhere *outside of your blog's source directory*. (Recall that any change to the source directory instantly republishes the blog, something you won't want to do with a half-written entry on top.) You can name this file whatever you like, so long as the filename ends in either `.markdown` or `.md`.

You must also give your post a title, sometime before you're ready to publish it. You define the title simply by having the first line of your entry say `title: whatever`, followed by two newlines, followed in turn by the body of your post.

To publish a post, simply move it to Plerd's source directory.

Plerd will, once it notices the new file, give the file a timestamp recording the date and time of its publication. This timestamp will appear in its own line, after the title line.

Normally, Plerd will set the publication time to the moment that you added the file to the source directory. Plerd recognizes two exceptions to this rule:

- If you manually give your post a `time:` timestamp, and it's in W3C date-time format, then Plerd will leave that timestamp alone.
- If you leave the timestamp out, and include in your post's filename a date of yesterday or earlier (e.g. `1994-06-10-i-like-ace-of-base.md`), then Plerd will set the post's timestamp to midnight (in the local time zone) of that date. This allows you to batch-backdate many posts at once -- useful, perhaps, for populating a new blog with existing writing.

## Deployment using GitHub Pages

Create a new GitHub repository named `username/username.github.io` which will be used to host our files. Leave it empty or with just a `LICENSE` of your liking.

```
$ git clone https://github.com/username/username.github.io
$ cd username.github.io
$ plerdall --init
```

Edit the `plerd/conf/plerd.conf` to your liking. By default, GitHub Pages uses Jekyll to process your website pages so we want to disable that. We do this by adding an empty file called `.nojekyll` in every directory starting from the *root* directory:

```
$ touch .nojekyll
$ touch conf/.nojekyll
$ touch db/.nojekyll
$ touch docroot/.nojekyll
$ touch log/.nojekyll
$ touch run/.nojekyll
$ touch source/.nojekyll
$ touch templates/.nojekyll
```

We also need to fix a symbolic link so that GitHub Pages doesn't choke during each update build and deployment:

```
$ cd docroot
$ rm index.html
$ ln -s recent.html index.html
```

Now we can stage and push our changes
