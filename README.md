# Ansible Role: traffic control

## Description

Install and configure trafic control using ansible.

## Requirements

- Ansible >= 2.5 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `tc_script_path` | /usr/local/bin | Define tc script path |
| `tc_config_interface` | eth0 | Define tc interface |
| `tc_config_speed` | "10000000.0kbit" | Define interface default speed |
| `tc_config_burst` | "15k" | Define interface burst |
| `tc_vip_ip` | "{{ ansible_vip_ip }}" | Defined IP-Address for tc |
| `tc_config_filters` | [] | Defined source ip filters |
| `tc_config_classes` | [] | Defined speed classes |

## Example

```yaml
---
# Define tc config
tc_config_filters:
  - id: 0 # Set unique id for filter
    source: "10.62.2.128/25" # Define source network
    prio: 1 # Set priority for folter
    class: 18 # Which config classes yre used
  - id: 1 # Set unique id for filter
    source: "10.62.0.128/25" # Define source network
    prio: 2 # Set priority for folter
    class: 16 # Which config classes yre used
```

### Playbook

```yaml
---
- hosts: all
  roles:
  - ansible-role-traffic-control
```

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
