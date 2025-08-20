# Enables miscellaneous debug settings #

Ships a `/etc/default/grub.d/45_debug-misc.cfg` configuration file.
This removes `quiet`, `loglevel=0`, and `rhgb` from the
`GRUB_CMDLINE_LINUX_DEFAULT` variable. It also removes `debugfs=off`,
`efi_pstore.pstore_disable=1`, and `erst_disable` from the
`GRUB_CMDLINE_LINUX` variable. Finally, it adds `debug=vc` to the
`GRUB_CMDLINE_LINUX` variable to enable verbose output during the
initial ramdisk boot phase.

Undo debugging related `sysctl` settings by package `security-misc`.

Enables persistent systemd journal log.

Disables `/usr/lib/systemd/coredump.conf.d/30_security-misc.conf` by package
`security-misc` using `debian/debug-misc.links` by creating a symlink from
`/etc/systemd/coredump.conf.d/30_security-misc.conf` to `/dev/null`.

Disables `/usr/lib/systemd/pstore.conf.d/30_security-misc.conf` by package
`security-misc` using `debian/debug-misc.links` by creating a symlink from
`/etc/systemd/pstore.conf.d/30_security-misc.conf` to `/dev/null`.

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

1\. Download the APT Signing Key.

```
wget https://www.kicksecure.com/keys/derivative.asc
```

Users can [check the Signing Key](https://www.kicksecure.com/wiki/Signing_Key) for better security.

2\. Add the APT Signing Key.

```
sudo cp ~/derivative.asc /usr/share/keyrings/derivative.asc
```

3\. Add the derivative repository.

```
echo "deb [signed-by=/usr/share/keyrings/derivative.asc] https://deb.kicksecure.com trixie main contrib non-free" | sudo tee /etc/apt/sources.list.d/derivative.list
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

See instructions.

NOTE: Replace `generic-package` with the actual name of this package `debug-misc`.

* **A)** [easy](https://www.kicksecure.com/wiki/Dev/Build_Documentation/generic-package/easy), _OR_
* **B)** [including verifying software signatures](https://www.kicksecure.com/wiki/Dev/Build_Documentation/generic-package)

## Contact ##

* [Free Forum Support](https://forums.kicksecure.com)
* [Premium Support](https://www.kicksecure.com/wiki/Premium_Support)

## Donate ##

`debug-misc` requires [donations](https://www.kicksecure.com/wiki/Donate) to stay alive!
