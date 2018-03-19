ansible-swapfile
================

This role configures a swapfile (/swapfile) with the (default) size of 1024MB.

## Dependencies

None.

## Variables

* `swapfile_size` [default: `1024MB`]: the size of the swapfile to create in the format that `fallocate` expects:

    The  length and offset arguments may be followed by binary (2^N) suffixes KiB, MiB, GiB, TiB, PiB and EiB (the "iB" is optional, e.g. "K" has the same meaning as "KiB") or decimal (10^N) suffixes KB, MB, GB, PB and EB.

* `swapfile_location` [default: `/swapfile`]: the location of where the swapfile will be created

### Optional

The following variables are set to `False` by default and will not have any effect on your hosts. Setting them to any value other than `False` will update your hosts' sysctl.conf file.

* `swapfile_swappiness` [default: `False`]: the swappiness percentage (vm.swappiness) -- the lower it is, the less your system swaps memory pages

## Usage

```yaml
- hosts: swapfile_enabled_hosts
  roles:
  - { role: coreos-swapfile-ansible, when: ansible_distribution == "CoreOS" }
```

or:

```yaml
- hosts: swapfile_enabled_hosts
  roles:
  - { role: coreos-swapfile-ansible, when: ansible_distribution == "CoreOS", swapfile_size: 1GB, swapfile_swappiness: 10 }
```

You can also set the variables described above in `group_vars` or `host_vars` (see `defaults/main.yml`).
