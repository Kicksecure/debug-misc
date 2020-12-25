# Enables miscellaneous debug settings #

Ships a `/etc/default/grub.d/45_debug-misc.cfg` configuration file,
that removes `quiet`, `loglevel=0` and `debugfs=off` from the
`GRUB_CMDLINE_LINUX_DEFAULT` variable and adds `debug=vc` to the kernel
boot parameter to enable verbose output during the initial ramdisk boot
phase.

Undo debugging related `sysctl` settings by package `security-misc`.

Enables persistent systemd journal log.

Disables `/lib/systemd/coredump.conf.d/disable-coredumps.conf` by package
`security-misc` by creating a symlink from
`/etc/systemd/coredump.conf.d/disable-coredumps.conf` to `/dev/null`.
`debian/debug-misc.links`

Disables `panic-on-oops`, `remove-system.map` by package `security-misc`.

`config-package-dev` `hide` `/etc/sysctl.d/30_silent-kernel-printk.conf` which
kernel.printk to default as if security-misc would not have lowered verbosity.

Configure systemd `getty` service to not clear `tty`.
`/lib/systemd/system/getty@tty.service.d/30_debug-misc.conf`

Coredumps are enabled.
`/etc/security/limits.d/40_debug-misc.conf`

Coredumps may contain important information such as encryption keys or
passwords. Package `security-misc` disables coredumps. Package `debug-misc`
re-enables coredumps.

Contains a helper tool to cause a segfault for testing purposes.
`segfault-build` creates `segfault-run`. Running `segfault-run` results in
`segfault-run` terminating with a segfault. This is useful to test if
coredump files are being generated when an application crashes.
`/usr/sbin/segfault-build`
`/usr/share/debug-misc/segfault.c`

For better usability, to ease debugging in case of issues.

For better security, this package should only be installed on specific
machines that require debugging. Unfortunately, security and debugging are
conflicting optimization goals.
## How to install `debug-misc` using apt-get ##

1\. Download Whonix's Signing Key.

```
wget https://www.whonix.org/patrick.asc
```

Users can [check Whonix Signing Key](https://www.whonix.org/wiki/Whonix_Signing_Key) for better security.

2\. Add Whonix's signing key.

```
sudo apt-key --keyring /etc/apt/trusted.gpg.d/whonix.gpg add ~/patrick.asc
```

3\. Add Whonix's APT repository.

```
echo "deb https://deb.whonix.org buster main contrib non-free" | sudo tee /etc/apt/sources.list.d/whonix.list
```

4\. Update your package lists.

```
sudo apt-get update
```

5\. Install `debug-misc`.

```
sudo apt-get install debug-misc
```

## How to Build deb Package from Source Code ##

Can be build using standard Debian package build tools such as:

```
dpkg-buildpackage -b
```

See instructions. (Replace `generic-package` with the actual name of this package `debug-misc`.)

* **A)** [easy](https://www.whonix.org/wiki/Dev/Build_Documentation/generic-package/easy), _OR_
* **B)** [including verifying software signatures](https://www.whonix.org/wiki/Dev/Build_Documentation/generic-package)

## Contact ##

* [Free Forum Support](https://forums.whonix.org)
* [Professional Support](https://www.whonix.org/wiki/Professional_Support)

## Donate ##

`debug-misc` requires [donations](https://www.whonix.org/wiki/Donate) to stay alive!
