Ubuntu Autoinstall Scripts
==========================

By [Andy Sayler](https://www.andysayler.com)\
July 2026

[![Validate Autoinstall](https://github.com/asayler/ubuntu_autoinstall/actions/workflows/validate-autoinstall.yml/badge.svg)](https://github.com/asayler/ubuntu_autoinstall/actions/workflows/validate-autoinstall.yml)

* **Ubuntu Server Version:** 26.04 (previously tested with 20.04, 22.04)
* **Default Username:** `setup`
* **Default Password:** `setup`
* **Default Encryption Key:** `setup`

Contents
--------
* [user-data-base](user-data-base): Basic autoinstall file that
  configures a server for SSH and used the default partition scheme.
* [user-data-storage-btrfs](user-data-storage-btrfs): Builds on
  `user-data-basic` to define a custom partition scheme for the
  first NVMe device on the system using the btrfa filesystem.
* [user-data-encrypted-btrfs](user-data-encrypted-btrfs): Builds on
  `user-data-storage` to add LUKS full disk encryption to the
  partition scheme. **NOTE: Please change the LUKS password after
  first boot. Default LUKS password is above.**
* [user-data-encrypted-ext4](user-data-encrypted-ext4): Same as the
  previous version, but using ext4 instead of btrfs.  **NOTE: Please
  change the LUKS password after first boot. Default LUKS password is
  above.**
* [user-data-encrypted-zfs-auto](user-data-encrypted-zfs-auto): Alternate to
  `user-data-encrypted-btrfs` using the guided ZFS layout with native ZFS
  encryption instead of manual LUKS partitioning. **NOTE: Please
  change the encryption passphrase after first boot. Default
  passphrase is above.** (**UNTESTED**)
* [user-data-encrypted-zfs-manual](user-data-encrypted-zfs-manual):
  Same encrypted-ZFS scheme as the previous version, but built
  from low-level `zpool`/`zfs` storage actions on a fixed partition
  layout instead of the guided layout. **NOTE: Please change the
  encryption passphrase after first boot. Default passphrase is
  above.** (**UNTESTED**)

Build
-----
1. Customize appropriate `user-data-XXXX` file as needed
2. Build cloudinit iso: `cloud-localds ./autoinstall.iso ./user-data-XXXX ./meta-data`
3. Mount both `autoinstall.iso` and [Ubuntu 26.04 server.iso](https://releases.ubuntu.com/26.04/)
(I tend to use the IPMI console to do this on headless servers,
but doing it via VM commands or actual media on a physical server
should all work as well.)
4. Boot system to Ubuntu server installer and select `yes` when prompted to start autoinstall
5. Profit

Notes
-----
* Generate Crypted Password: `openssl passwd -6`

Validation
----------
Every `user-data-*` file is checked on push/PR by a
[GitHub Actions workflow](.github/workflows/validate-autoinstall.yml) that
runs Subiquity's own `validate-autoinstall-user-data.py` against it (see the
[autoinstall validation howto](https://canonical-subiquity.readthedocs-hosted.com/en/latest/howto/autoinstall-validation.html)).
This is not a local pre-commit check since the validator needs a full
Subiquity checkout and `sudo apt-get install`-ed dependencies.

References
----------
* https://ubuntu.com/server/docs/install/autoinstall
* https://ubuntu.com/server/docs/install/autoinstall-reference
* https://curtin.readthedocs.io/en/latest/topics/storage.html
* https://canonical-subiquity.readthedocs-hosted.com/en/latest/howto/autoinstall-validation.html
