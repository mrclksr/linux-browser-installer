### About

*linux-browser-installer* is Bourne shell script to install Linux versions of
the Chrome or Brave browser under FreeBSD into a Linux (Ubuntu Bionic) jail.
The script is based on the excellent [Howto](https://forums.freebsd.org/threads/linuxulator-how-to-run-google-chrome-linux-binary-on-freebsd.77559/) by @[patovm04](https://github.com/patovm04).

If not defined otherwise, Ubuntu Bionic (`ubuntu_version`) is installed under
`/compat/ubuntu` (`jail_path`). A modified version of FreeBSD's linux rc-script
(`rc.d/ubuntu`) is used to start the *linuxulator*.

### Please Note

You can't run different Linux jails at the same time. If you want to run
CentOS-based applications under `/compat/linux`, you have to set
`sysctl compat.linux.emul_path=/compat/linux`, and start the linux rc-script
(`service linux onestart`). Depending on which jail you intend to use by
default, set either (not both) `linux_enable="YES"` or `ubuntu_enable="YES"`
in `/etc/rc.conf`.

### Usage

````
# ./linux-browser-installer install chrome
````

and/or

````
# ./linux-browser-installer install brave
````

