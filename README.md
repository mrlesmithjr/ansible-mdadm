# mrlesmithjr.mdadm

An [Ansible](https://www.ansible.com) role to install and manage [mdadm](https://linux.die.net/man/8/mdadm) raid arrays.

## Requirements

- Available unpartitioned disk devices

## Role Variables

[defaults/main.yml](defaults/main.yml)


## Dependencies

None

## Example Playbook

### Manual device configuration
```yaml
- hosts: all
  become: true
  vars:
    mdadm_arrays:
      - name: md200
        devices:
          - /dev/nvme0n1
          - /dev/nvme1n1
        filesystem: lvm
        level: 5
        state: present
        auto_detect: false  # default, can be omitted
  roles:
    - role: ansible-mdadm
```

### Auto-detection mode
```yaml
- hosts: all
  become: true
  vars:
    mdadm_arrays:
      - name: md200
        devices: []  # empty list for auto-detection
        filesystem: lvm
        level: 5
        state: present
        auto_detect: true
        min_disks: 3  # minimum number of disks required
  roles:
    - role: ansible-mdadm
```

### Mixed configuration
```yaml
- hosts: all
  become: true
  vars:
    mdadm_arrays:
      - name: md0
        devices:
          - /dev/sdb
          - /dev/sdc
        filesystem: ext4
        level: 1
        state: present
        auto_detect: false
      - name: md200
        devices: []
        filesystem: lvm
        level: 5
        state: present
        auto_detect: true
        min_disks: 3
  roles:
    - role: ansible-mdadm
```

**Note**: Auto-detection will automatically use all unused disks (not mounted, not in RAID, not in LVM, not formatted) when `auto_detect: true` and `devices: []`. Setting both `auto_detect: true` and defining `devices` will result in an error.

## License

BSD

## Author Information

Larry Smith Jr.

- [@mrlesmithjr](https://twitter.com/mrlesmithjr)
- [mrlesmithjr@gmail.com](mailto:mrlesmithjr@gmail.com)
- [http://everythingshouldbevirtual.com](http://everythingshouldbevirtual.com)

<a href="https://www.buymeacoffee.com/mrlesmithjr" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
