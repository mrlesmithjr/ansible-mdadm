# mrlesmithjr.mdadm

An [Ansible](https://www.ansible.com) role to install and manage [mdadm](https://linux.die.net/man/8/mdadm) raid arrays.

## Requirements

- Available unpartitioned disk devices

## Role Variables

[defaults/main.yml](defaults/main.yml)


## Dependencies

None

## Example Playbook

### Manual configuration
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
  roles:
    - role: ansible-mdadm
```

### Auto-detection mode
```yaml
- hosts: all
  become: true
  vars:
    mdadm_auto_detect_arrays: true
    mdadm_auto_detect_config:
      - name: md200
        filesystem: lvm
        level: 5
        state: present
        min_disks: 3
  roles:
    - role: ansible-mdadm
```

Note: Auto-detection will automatically use all unused disks (not mounted, not in RAID, not in LVM, not formatted) if `mdadm_arrays` is empty and `mdadm_auto_detect_arrays` is true.

## License

BSD

## Author Information

Larry Smith Jr.

- [@mrlesmithjr](https://twitter.com/mrlesmithjr)
- [mrlesmithjr@gmail.com](mailto:mrlesmithjr@gmail.com)
- [http://everythingshouldbevirtual.com](http://everythingshouldbevirtual.com)

<a href="https://www.buymeacoffee.com/mrlesmithjr" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
