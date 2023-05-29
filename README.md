# mrlesmithjr.mdadm

An [Ansible](https://www.ansible.com) role to install and manage [mdadm](https://linux.die.net/man/8/mdadm) raid arrays.

## Requirements

- Available unpartitioned disk devices

## Role Variables

[defaults/main.yml](defaults/main.yml)


## Dependencies

None

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-mdadm
  tasks:
```

## License

BSD

## Author Information

Larry Smith Jr.

- [@mrlesmithjr](https://twitter.com/mrlesmithjr)
- [mrlesmithjr@gmail.com](mailto:mrlesmithjr@gmail.com)
- [http://everythingshouldbevirtual.com](http://everythingshouldbevirtual.com)

<a href="https://www.buymeacoffee.com/mrlesmithjr" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
