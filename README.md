ansible-role-backup-kvm_lvm
=========

Templates in a script that is used with Commvault to take backup of LVM based logical volumes using snapshots.

*When messing with filesystems - always be careful.*

After the logical volumes and the VMs are created this role can be added, make sure to specify the variables

This has only been tested in RHEL6 and 7 derivatives (SL6 and CentOS7 to be precise) with libvirt0.10 and lvm2, but as long as the lvm and virsh commands exist and output the same this should work on most distributions. Testing is welcome, if you want to add an OS to be supported send a PR / message.

The kvm_lvm_backup.sh.j2 was in use with a version before Commvault 10, 8 or 9.

The commvault10 scripts in templates/ with Commvault 10.

To use the commvault 10 scripts define backup_scripts variable, see the defaults/main.yml.

Basic functionality of the script (not Commvault 10):
 - pre-scan ($1 == 1) - first argument to the script == 1
  - suspend
  - snapshot
  - resume
  - mount snapshot
 - post-backup ($1 == 2) - first argument to the script == 2
  - unmount snapshot
  - remove snapshot

Requirements
------------

 - A machine that runs KVM (or at least something that uses virsh commands, so libvirt?)
 - LVM - This has only been tested with VMs that have their OS disks stored in .img files on a filesystem inside an LVM

Role Variables
--------------

See defaults/main.yml

There are variables that must be defined.

By default this role does not do anything. You must specify

Dependencies
------------


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: ansible-role-backup-kvm_lvm }

License
-------

MIT

Author Information
------------------
