# Miscellaneous stuff

[![License: GPLv2](https://img.shields.io/badge/license-GPLv2-brightgreen.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
[![License: GPLv3](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)](https://www.gnu.org/licenses/gpl-3.0)

Nothing but random stuff here.

## Contents

* [ansible.cfg](ansible.cfg)
  * Example Ansible configuration with optimizations
* [fedora-init.yml](fedora-init.yml)
  * Ansible playbook to initialize a Fedora system after installation
* [qcow2-to-box](qcow2-to-box)
  * A simple script to create Vagrant boxes from Qcow2 images
* [rhel-7-base.ks](rhel-7-base.ks)
  * RHEL 7 base installation kickstart example
* [rhel-8-base.ks](rhel-8-base.ks)
  * RHEL 8 base installation kickstart example (see below)
* [rhel-8-init.yml](rhel-8-init.yml)
  * Ansible playbook to initialize a RHEL 8 system after installation
* [vagrant.ks](vagrant.ks)
  * Kickstart snippet to make Fedora/RHEL installation Vagrant-ready

## RHEL 7 Footprint Comparison

The following table illustrates RHEL 7 image footprint with various
installation options.

_Last updated for RHEL 7.6 Server (later releases may have slightly
different characteristics)_.

1. RHEL Server default installation (using all defaults with the GUI
   installer)
2. Red Hat RHEL 7 Qcow2 image (from https://access.redhat.com/downloads/)
   (has no `firewalld` running)
3. [rhel-7-base.ks](rhel-7-base.ks) based kickstart installation
4. [rhel-7-base.ks](rhel-7-base.ks) "ultra lean" installation
   (using __--excludedocs__ and other `%packages` options listed in the
   file, `firewalld`, `kdump`, and `tuned` services disabled, using
   `network.service` instead of `NetworkManager`,
   all custom packages omitted)
5. [rhel-7-base.ks](rhel-7-base.ks) "ultra lean" with SELinux disabled

NB. The _linux-firmware_ package takes 176M on disk if installed, it
is removed by the kickstart `%post` script but in case of kernel update
it will be installed again, even if not needed on VMs.

| Variant    |    1   |    2   |    3   |    4   |    5   |
|------------|:------:|:------:|:------:|:------:|:------:|
| RPMs       |   342  |   345  |   267  |   198  |   194  |
| Disk usage | 1176M  |  950M  |  581M  |  421M  |  400M  |
| RAM usage  |  102M  |   76M  |   90M  |   43M  |   40M  |

## RHEL 8 Footprint Comparison

The following table illustrates RHEL 8 image footprint with various
installation options.

_Last updated for RHEL 8.0 Beta (later releases may have slightly
different characteristics)_.

1. RHEL Server default installation (using all defaults with the GUI
   installer)
2. Red Hat RHEL 8 Qcow2 image (from https://access.redhat.com/downloads/)
   (has no `firewalld` running)
3. [rhel-8-base.ks](rhel-8-base.ks) based kickstart installation
4. [rhel-8-base.ks](rhel-8-base.ks) "ultra lean" installation
   (using __--excludedocs__ and other `%packages` options listed in the
   file, `firewalld`, `kdump`, and `tuned` services disabled, using
   `network.service` instead of `NetworkManager`,
   all custom packages omitted)
5. [rhel-8-base.ks](rhel-8-base.ks) "ultra lean" with SELinux disabled
   (see https://bugzilla.redhat.com/show_bug.cgi?id=1660142)

NB. The _linux-firmware_ package takes 291M on disk if installed, it
is removed by the kickstart `%post` script but in case of kernel update
it will be installed again, even if not needed on VMs.

| Variant    |    1   |    2   |    3   |    4   |    5   |
|------------|:------:|:------:|:------:|:------:|:------:|
| RPMs       |   382  |   433  |   327  |   228  |   222  |
| Disk usage | 1386M  | 1295M  |  736M  |  540M  |  490M  |
| RAM usage  |  145M  |  129M  |  138M  |   85M  |   55M  |

## License

GPLv2+
