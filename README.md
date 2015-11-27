# User

[![Ansible Galaxy](http://img.shields.io/badge/galaxy-GROG.user-660198.svg?style=flat)](https://galaxy.ansible.com/list#/roles/4730)
[![Build Status](https://travis-ci.org/GROG/ansible-role-user.svg?branch=master)](https://travis-ci.org/GROG/ansible-role-user)

A role for managing users.

Following roles where designed to neatly work together with this role:

- [authorized-key](https://galaxy.ansible.com/list#/roles/4737), for managing
  authorized-keys.
- [sudo](https://galaxy.ansible.com/list#/roles/4765), for managing sudo
  rights.

The [management-user](https://galaxy.ansible.com/list#/roles/4793) role
combines all these roles in one easy to use role.

## Requirements

- Hosts should be bootstrapped for ansible usage (have python,...)
- Root privileges, eg `become: yes`
- `useradd`, `userdel` and `usermod` should be available on the host

## Role Variables

| Variable | Description | Default value |
|----------|-------------|---------------|
| `user_list` | List of users **(see details!)** | `[]` |
| `user_list_host`| List of users **(see details!)**  | `[]` |
| `user_list_group` | List of users **(see details!)** | `[]` |
| `user_append` | Default value for `append` | `no` |
| `user_createhome` | Default value for `createhome` | `yes` |
| `user_force` | Default value for `force` | `no` |
| `user_generate_ssh_key` | Default value for `generate_ssh_key` | `no` |
| `user_move_home` | Default value for `move_home` |`no` |
| `user_none_unique` | Default value for `none_unique` | `no` |
| `user_remove` | Default value for `remove` | `no` |
| `user_shell` | Default value for `shell` | '/bin/sh' |
| `user_ssh_key_bits` | Default value for `ssh_key_bits` | 4096 |
| `user_ssh_key_file` | Default value for `ssh_key_file` | '.ssh/id_rsa' |
| `user_state` | Default user `state` | `present` |
| `user_system` | Default value for `system` | `no` |
| `user_update_password` | Default value for `update_password` | `always` |

#### `user_list` details

`user_list`, `user_list_host` and `user_list_group` are merged when
managing the users. You can use the host and group lists to specify
users per host or group off hosts.

The user list allows you to define which users must be managed. Each item in
the list can have following attributes:

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `append` | Only append to groups? | no | `user_append` |
| `comment` | User description (aka GECOS) | no | / |
| `createhome` | Create home directory? | no | `user_createhome` |
| `expires` | Expiry data | no | / |
| `force` | Use --force option when deleting a user | no | `user_force` |
| `generate_ssh_key` | Generate ssh key?  | no | `user_generate_ssh_key` |
| `group` | Users primary group | no | / |
| `groups` | List of groups for the user | no | / |
| `home` | Home directory for the user | no | / |
| `login_class` | Login class for BSD systems | no | / |
| `move_home` | Move home directory | no | `user_move_home` |
| `name` | User name | yes | / |
| `non_unique` | Allow none unique uid | no | `user_none_unique` |
| `password` | Password for the user | no | / |
| `remove` | Use --remove option when deleting a user | no | `user_remove` |
| `shell` | Users shell | no | `user_shell` |
| `ssh_key_bits` | SSH key size | no | `user_ssh_key_bits` |
| `ssh_key_comment` | SSH key comment | no | / |
| `ssh_key_file` | SSH key file | no | `user_ssh_key_file` |
| `ssh_key_passphrase` | SSH key passphrase | no | / |
| `ssh_key_type` | SSH key type | no | rsa |
| `state` | User state | no | `user_state` |
| `system` | System account? | no | `user_system` |
| `uid` | User id | no | / |
| `update_password` | Update password if changed? | no | `user_update_password` |

###### Example `user_list`

```yaml
user_list:
  - name: user1
  - name: user2
    uid: 1001
    groups:
      - test
      - sudo
  - name: user3
    uid: 1002
    state: absent
```

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: servers
  roles:
  - { role: GROG.user, become: yes }
```

Inside `group_vars/servers.yml`:

```yaml
user_list_group:
  - name: user
    uid: 1001
  - name: test
    state: absent
```

## License

LGPLv3

## Contributing

All assistance, changes or ideas [welcome](https://github.com/GROG/ansible-role-user/issues)!

## Author Information

By [G. Roggemans](https://github.com/groggemans)
