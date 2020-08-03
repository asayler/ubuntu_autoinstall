Ubuntu Autoinstall Scripts
==========================

[Andy Sayler](https://www.andysayler.com)
August 2020

* **Ubuntu Server Version:** 20.04
* **Default Username:** `setup`
* **Default Password:** `setup`
* **Default Encryption Key:** `setup`

Description
-----------
* `user-data-base`: Basic autoinstall file that configures a server
   for SSH and used the default partition scheme.

Build
-----
1. Customize appropriate `user-data` file as needed
2. Build cloudinit iso: `cloud-localds ./autoinstall.iso ./user-data ./meta-data`
3. Mount both `autoinstall.iso` and [Ubuntu 20.04 server iso](https://releases.ubuntu.com/20.04/)
4. Boot system to Ubuntu server installer and select `yes` when prompted to start autoinstall
5. Profit

References
----------
* https://ubuntu.com/server/docs/install/autoinstall
* https://ubuntu.com/server/docs/install/autoinstall-reference
* https://curtin.readthedocs.io/en/latest/topics/storage.html
