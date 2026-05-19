# ansible-mdadm

An [Ansible](https://www.ansible.com) role to install and manage [mdadm](https://linux.die.net/man/8/mdadm) software RAID arrays.

> Used by [OpenStack Kayobe](https://docs.openstack.org/kayobe/latest/) for software RAID management.

## Ansible Galaxy

```bash
ansible-galaxy install mrlesmithjr.mdadm
```

> **Note:** As of December 2025, the canonical Galaxy name is `mrlesmithjr.mdadm`.
> If you were using `mrlesmithjr.ansible-mdadm`, update your `requirements.yml`.

<details>
<summary>Historical download statistics</summary>

| Role Name | Downloads (as of Dec 2025) |
|-----------|---------------------------|
| `mrlesmithjr.mdadm` | 632,067 |
| `mrlesmithjr.ansible-mdadm` | 8,439 |
| **Combined** | **640,506** |

Download counts reset when roles are re-imported to Galaxy. These figures represent actual historical usage.
</details>

## Supported Platforms

| Platform | Versions |
|----------|----------|
| Ubuntu | 20.04, 22.04, 24.04 |
| Debian | 11, 12 |
| Rocky Linux / RHEL | 8, 9 |
| Fedora | 39+ |

## Requirements

- Available unpartitioned disk devices to assign to arrays
- Root / `become: true`

## Quick Start

### RAID 1 (Mirror)

```yaml
---
- hosts: all
  become: true
  vars:
    mdadm_arrays:
      - name: md0
        devices:
          - /dev/sdb
          - /dev/sdc
        filesystem: ext4
        level: '1'
        mountpoint: /mnt/md0
        state: present
  roles:
    - role: mrlesmithjr.mdadm
```

### RAID 5

```yaml
mdadm_arrays:
  - name: md0
    devices:
      - /dev/sdb
      - /dev/sdc
      - /dev/sdd
    filesystem: ext4
    level: '5'
    mountpoint: /mnt/md0
    state: present
```

## Key Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `mdadm_arrays` | `[]` | List of RAID array definitions (see below) |

### `mdadm_arrays` Structure

```yaml
mdadm_arrays:
  - name: md0              # Array device name (/dev/md0)
    devices:               # Block devices to include
      - /dev/sdb
      - /dev/sdc
    filesystem: ext4       # Filesystem to create: ext4 | xfs | etc.
    level: '1'             # RAID level: 0 | 1 | 4 | 5 | 6 | 10
    mountpoint: /mnt/md0   # Where to mount the array
    state: present         # present | absent
    opts: noatime          # Mount options (optional)
    assume_clean: true     # Avoid initial resync
```

See [defaults/main.yml](defaults/main.yml) for the full variable reference.

## Testing

```bash
pip install molecule molecule-docker
molecule test
```

## Support This Project

This role has been downloaded over **640,000 times** from Ansible Galaxy.
If your organization depends on it in production, consider
[sponsoring its maintenance](https://github.com/sponsors/mrlesmithjr).
Enterprise support tiers are available.

## License

BSD

## Author

Larry Smith Jr. — [everythingshouldbevirtual.com](http://everythingshouldbevirtual.com) · [mrlesmithjr@gmail.com](mailto:mrlesmithjr@gmail.com)
