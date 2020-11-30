### About

*linux-browser-installer* is a Bourne shell script to install Linux versions of
the Chrome or Brave browser under FreeBSD into a Linux (Ubuntu Bionic) jail.
They allow you to use web services like *Netflix*, *Prime Video*, or *Spotify*
which require [Widevine](https://en.wikipedia.org/wiki/Widevine).
The script is based on the excellent [Howto](https://forums.freebsd.org/threads/linuxulator-how-to-run-google-chrome-linux-binary-on-freebsd.77559/) by @[patovm04](https://github.com/patovm04).

If not defined otherwise, Ubuntu Bionic (`$ubuntu_version`) is installed under
`/compat/ubuntu` (`$jail_path`). A modified version of FreeBSD's linux rc-script
(`rc.d/ubuntu`) is used to start the *linuxulator*, and to mount the jail's
filesystems.

### System requirements

FreeBSD 12.2-RELEASE or 13-CURRENT

### Please Note
I use the term *jail* here for a directory to which you can `chroot`. It has
nothing to do with FreeBSD jails.

You can't run different Linux jails at the same time. If you want to run
CentOS-based applications under `/compat/linux`, you have to set
`sysctl compat.linux.emul_path=/compat/linux`, and start the linux rc-script
(`service linux onestart`). Depending on which jail you intend to use by
default, set either (not both) `linux_enable="YES"` or `ubuntu_enable="YES"`
in `/etc/rc.conf`.

### Usage
#### Install Chrome or Brave browser

````
# ./linux-browser-installer install chrome
````

and/or

````
# ./linux-browser-installer install brave
````

If the jail is not existing yet, it will be created first.

Run `/usr/local/bin/linux-chrome` (`/usr/local/bin/linux-brave`) to start
Chrome (Brave).

#### Deinstall Chrome or Brave browser

````
# ./linux-browser-installer deinstall chrome
````

and/or

````
# ./linux-browser-installer deinstall brave
````

This command deinstalls the browser, and removes its wrapper
scripts from `/usr/local/bin` and `$jail_path/bin` along with its
desktop file.

#### Create jail

````
# ./linux-browser-installer jail create
````

#### Upgrade software installed in the jail

````
# ./linux-browser-installer jail upgrade
````

#### Delete jail

````
# ./linux-browser-installer jail delete
````

Before deleting the entire jail under `$jail_path`, this command
unmounts all the jail's filesystems, deletes the rc script, and removes its
variable(s) from `/etc/rc.conf`.

#### Update symlinks
- - -

**Note**: Symlinks to files outside the jail will not work when `chroot`'ing.

- - -

##### For icons

````
# ./linux-browser-installer symlink icons
````

This command updates the symlinks from `$prefix/share/icons` to
`$jail_path/usr/share/icons`. Use this after installing new icons
to make them available to applications in the jail.

##### For themes
````
# ./linux-browser-installer symlink themes
````

This command updates the symlinks from `$prefix/share/themes` to
`$jail_path/usr/share/themes`. Use this after installing new themes
to make them available to applications in the jail.

#### Delete working files from current directory
````
# ./linux-browser-installer clean
````
