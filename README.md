![](https://img.shields.io/badge/Ansible-beats-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_beat.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Beats Versions](#beats-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs elastic Beats on operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### Beats versions

The following list of supported the Beats releases:

* Beats 6.8+, 7.1+

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `beats_version`: Specify the Beats.
* `beats_type`: Which kinds of beats are installs.

##### Filebeat parameters
* `filebeat_configset`: Specific configuration set by instances of this.
* `filebeat_configver`: Specific configuration set versions.

##### Auditbeat parameters
* `auditbeat_audit_rules`: Specific audit rules list.
* `auditbeat_drop_fields`: Specific which fields to drop.

##### Listen port
* `beats_port_arg.http`: Port for Beats http.
* `beats_port_arg.exporter`: Port for prometheus exporter.

##### Output Variables
* `beats_output_type`: Configure what output to use when sending the data collected by the Beats.
* `beats_output_host`: The list of known servers to connect to.
* `beats_output_port`: Servers communication port.
* `beats_output_auth`: A boolean value, Enable or Disable authentication.
* `beats_output_pass`: Authenticated password.
* `beats_output_user`: Authenticated user.

##### Service Mesh
* `subscription`: Define the service subscription.
* `region`: Define the service region.
* `environments`: Define the service environment.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_port`: The consul HTTP API port.
* `consul_public_http_prot`: The consul Hypertext Transfer Protocol.
* `consul_public_clients`: List of public consul clients.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
- Ansible versions >= 2.8
- Python >= 2.7.5

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' beats_version='6.8.1'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-OS-beats
           beats_version: '6.8.1'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    beats_version: '7.1.1'
    beats_type: 'file'
    filebeat_configset: 'wazuh'
    filebeat_configver: '3'
    beats_port_arg:
      http: '5066'
      exporter: '9479'
    beats_output_type: 'elasticsearch'
    beats_output_host:
      - '127.0.0.1'
    beats_output_port: '9200'
    beats_output_auth: false
    beats_output_pass: 'password'
    beats_output_user: 'elastic'
    environments: 'Development'
    tags:
      subscription: 'default'
      owner: 'nobody'
      department: 'Infrastructure'
      organization: 'The Company'
      region: 'IDC01'
    exporter_is_install: false
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_http_port: '8500'
    consul_public_http_prot: 'https'
    consul_public_clients:
      - '127.0.0.1'

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
