# rfid_tuer_ansible

This role sets up the rfid_tuer repository with a system daemon to control access to a door by using rfid tags.

## Requirements
This role requires an apt based system.

## Role Variables

| Name                             | Required/Default | Description                                                     |
|:---------------------------------|:----------------:|:----------------------------------------------------------------|
| `rfid_tuer_ansible_install_path` | `/opt/door`      | Install path where to script and config file will be placed.    |
| `rfid_tuer_ansible_vars`         | see below        | Variable holding all other variables for the configuration file |
| `rfid_tuer_ansible_user`         | `door`           | Default user under which the service is running                 |
| `rfid_tuer_ansible_group`        | `door`           | Default group under which the service is running                |


## `rfid_tuer_ansible_vars`

| Name                               | Required/Default   | Description                                                |
|:-----------------------------------|:------------------:|:-----------------------------------------------------------|
| `door_relay_number`                | `0`                | Relay number that is used for opening and closing the door |
| `door_state_input_pin`             | `1`                | Input pin which is connected to the door input state       |
| `door_switch_input_pin`            | `0`                | Input switch number where the door switch is connected to  |
| `door_switch_green_led_output_pin` | `0`                | Output pin where the green switch led is connected to      |
| `door_switch_red_led_output_pin`   | `1`                | Output pin where the red switch led is connected to        |
| `rfid_reader_green_led_output_pin` | `2`                | Output pin where the green rfid reader led is connected to |
| `rfid_reader_red_led_output_pin`   | `3`                | Output pin where the red rfid reader led is connected to   |
| `ldap_port`                        | `389`              | LDAP port number                                           |
| `ldap_use_ssl`                     | `true`             | To enable or disable SSL on LDAP connections               |
| `ldap_server`                      | :heavy_check_mark: | URL to for the LDAP server that should be queried          |
| `ldap_base_dn`                     | :heavy_check_mark: | Base DN for LDAP search                                    |
| `ldap_user`                        | :heavy_check_mark: | DN of user used for bind                                   |
| `ldap_user_secret`                 | :heavy_check_mark: | Password of the user for bind                              |
| `ldap_match_attr`                  | :heavy_check_mark: | Attribute that should be looked up                         |
| `ldap_owner_attr`                  | :heavy_check_mark: | Attribute that contains the card owner (used for looging)  |

## Example Playbook

```yml
hosts: all
  become: true
  vars:
    ldap_server: example.de
    ldap_base_dn: dc=default,dc=example,dc=de
    ldap_user: uid=test,ou=people,dc=example,dc=de
    ldap_user_secret: password
    ldap_match_attr: "rfidTags"
  roles:
    - rfid_tuer_ansible
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
