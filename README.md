<!--
SPDX-FileCopyrightText: 2021 Helmholtz Centre for Environmental Research (UFZ)
SPDX-FileCopyrightText: 2021 Helmholtz-Zentrum Dresden-Rossendorf (HZDR)

SPDX-License-Identifier: Apache-2.0
-->

# Netplan Role

Ansible role to install and configure Netplan.

## Requirements

None.

## Role Variables

### Mandatory Variables to be Set that are Not Set with Defaults

#### Sample Network Configuration

Sample configuration to set up networking with Netplan:

```yaml
netplan_ethernets:
  - interface_name: 'eth0'
    dhcp4: 'no'
    gateway4: '10.1.0.1'
    addresses:
      - '10.1.0.10/24'
    nameservers:
      addresses:
        - '8.8.8.8'
        - '9.9.9.9'
      search:
        - 'domain.local'
        - 'domain.name'
```

### Variables that are Set with Defaults

#### Flag to delete any pre-existing Netplan configuration files

Flag decides on whether pre-existing Netplan configuration files should be deleted:

```yaml
netplan_remove_existing_configs: true
```

#### Name of the Netplan Configuration File Template

Name of the template providing the Netplan configuration file:

```yaml
netplan_configuration_file_template: 'config.yaml.j2'
```

#### Directory of the Netplan Configuration Files

Directory of the Netplan configuration files:

```yaml
netplan_configuration_dir: '/etc/netplan'
```

#### Name of the Netplan Configuration File

Name of the Netplan configuration file:

```yaml
netplan_configuration_file: 'config.yaml'
```

#### Path to the Netplan Configuration File

Path to the Netplan configuration file:

```yaml
netplan_configuration_file_path: "{{ (netplan_configuration_dir, netplan_configuration_file) | path_join }}"
```

#### Packages to be Installed

List of packages that need to be installed:

```yaml
netplan_packages:
  - 'netplan.io'
```

#### Flag to Uninstall Package ifupdown

Flag to decide whether package 'ifupdown' should be uninstalled:

```yaml
netplan_uninstall_ifupdown: true
```

## Troubleshooting

### Cleaning Up: Please Uninstall Package ifupdown Manually

In order to switch from package ifupdown to netplan the whole installation
and configuration process of the networking need to finish successfully
before package ifupdown can be uninstalled safely, otherwise role execution
will hang if package ifupdown would be uninstalled too early.
For that reason package ifupdown is not uninstalled during execution of the
role and need to be uninstalled manually after role has been executed
successfully.
In case that package ifupdown is installed a message is outputted at the
beginning of the role that you can uninstall package ifupdown safely after
role Netplan has been executed successfully.

## Dependencies

None.

## License

[Apache-2.0](LICENSES/Apache-2.0.txt)

## Author Information

[HIFIS Software Team](https://software.hifis.net)
