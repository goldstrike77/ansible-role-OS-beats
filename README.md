![](https://img.shields.io/badge/Ansible-filebeat-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_beat.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Filebeat Versions](#filebeat-versions)
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
This Ansible role installs Filebeat on operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### Filebeat versions

The following list of supported the Filebeat releases:

* Filebeat 6.8+, 7.1+

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `filebeat_version`: Specify the Filebeat version.
* `filebeat_selinux`: SELinux security policy.
* `filebeat_configset`: Specific configuration set by instances of this.
* `filebeat_configver`: Specific configuration set versions.

##### Listen port
* `filebeat_port_arg`: list of service port.

##### Service Mesh
* `environments`: Define the service environment.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_port`: The consul HTTP API port.
* `consul_public_clients`: List of public consul clients.

##### Elasticsearch Variables
* `filebeat_elastic_hosts`: List of Elasticsearch hosts Filebeat should connect to.
* `filebeat_elastic_port_rest`: Elasticsearch REST port.
* `filebeat_elastic_auth`: A boolean value, Enable or Disable Elasticsearch authentication.
* `filebeat_elastic_pass`: Elasticsearch authenticated password.
* `filebeat_elastic_user`: Elasticsearch authenticated user.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
There are no dependencies on other roles.

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' filebeat_version='6.8.1'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-OS-filebeat
           filebeat_version: '6.8.1'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    filebeat_version: '6.8.1'
    filebeat_selinux: false
    filebeat_configset: 'wazuh'
    filebeat_configver: '3.9.2'
    filebeat_port_arg:
      http: '5066'
      exporter: '9479'
    filebeat_elastic_hosts:
      - '127.0.0.1'
    filebeat_elastic_port_rest: '9200'
    filebeat_elastic_auth: true
    filebeat_elastic_pass: 'password'
    filebeat_elastic_user: 'elastic'
    environments: 'SIT'
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_http_port: '8500'
    consul_public_clients:
      - '127.0.0.1'

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
