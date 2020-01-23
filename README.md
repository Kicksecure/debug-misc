# Enables verbose output during boot #

Ships a /etc/default/grub.d/30_output_verbose.cfg configuration file, that
removes "quiet" from the GRUB_CMDLINE_LINUX_DEFAULT variable.

For better usability, so it doesn't look like boot hangs on slow systems and
to ease debugging in case of issues.
## How to install `debug-misc` using apt-get ##

1\. Download [Whonix's Signing Key]().

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

## How to Build deb Package ##

Replace `apparmor-profile-torbrowser` with the actual name of this package with `debug-misc` and see [instructions](https://www.whonix.org/wiki/Dev/Build_Documentation/apparmor-profile-torbrowser).

## Contact ##

* [Free Forum Support](https://forums.whonix.org)
* [Professional Support](https://www.whonix.org/wiki/Professional_Support)

## Donate ##

`debug-misc` requires [donations](https://www.whonix.org/wiki/Donate) to stay alive!
