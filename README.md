Ubuntu Autoinstall Scripts
==========================

By [Andy Sayler](https://www.andysayler.com)\
August 2020

* **Ubuntu Server Version:** 20.04
* **Default Username:** `setup`
* **Default Password:** `setup`
* **Default Encryption Key:** `setup`

Contents
--------
* `user-data-base`: Basic autoinstall file that configures a server
  for SSH and used the default partition scheme.
* `user-data-storage`: Builds on `user-data-basic` to define a custom
  partition scheme for the first NVMe device on the system.
* `user-data-encrypted`: Builds on `user-data-storage` to add LUKS
  full disk encryption to the partition scheme. **NOTE: change the LUKS
  password after first boot. Default LUKS password is above.**

Build
-----
1. Customize appropriate `user-data-XXXX` file as needed
2. Build cloudinit iso: `cloud-localds ./autoinstall.iso ./user-data-XXXX ./meta-data`
3. Mount both `autoinstall.iso` and [Ubuntu 20.04 server iso](https://releases.ubuntu.com/20.04/)
4. Boot system to Ubuntu server installer and select `yes` when prompted to start autoinstall
5. Profit

References
----------
* https://ubuntu.com/server/docs/install/autoinstall
* https://ubuntu.com/server/docs/install/autoinstall-reference
* https://curtin.readthedocs.io/en/latest/topics/storage.html
