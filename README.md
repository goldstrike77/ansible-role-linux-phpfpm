![](https://img.shields.io/badge/Ansible-php-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_php.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [PHP Versions](#PHP-versions)
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
PHP is a general-purpose scripting language that is especially suited to web development.

## Requirements
### Operating systems
This Ansible role installs PHP on linux operating system, including establishing a filesystem structure and server configuration with some common operational features, Will works on the following operating systems:

  * CentOS 7

### PHP versions

The following list of supported the PHP releases:

  * PHP 5.6, 7.x

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `php_version`: Specify the php-fpm version.

##### Listen port
* `php_fpm_port`: php-fpm instance.
* `php_fpm_exporter_port`: Prometheus exporter.

##### PHP Variables
* `php_allow_url_fopen`: Whether to allow accessing URL object like files.
* `php_allow_url_include`: Whether to allow use of URL-aware with the include/require functions.
* `php_date_timezone`: The default timezone used by all date/time functions.
* `php_default_socket_timeout`: Default timeout for socket based streams in seconds.
* `php_error_log`: Send an error message to the defined error handling routines.
* `php_expose_php`: Exposes to the world that PHP is installed on the server.
* `php_file_uploads`: Whether or not to allow HTTP file uploads.
* `php_max_execution_time`: Script maximum time is allowed to run before it is terminated by the parser in seconds.
* `php_max_file_uploads`: The maximum number of files allowed to be uploaded via single request.
* `php_max_input_time`: Script maximum time is allowed to parse input data in seconds.
* `php_memory_limit`: The maximum amount of memory in megabyte that a script is allowed to allocate.
* `php_post_max_size`: The maximum size in megabyte of post data allowed.
* `php_realpath_cache_size`: The maximum size in megabyte of the realpath cache to be used by PHP.
* `php_upload_max_filesize`: The maximum size in megabyte of files allowed to be uploaded.
* `php_upload_tmp_dir`: The temporary directory used for storing files when doing file upload.

##### PHP-FPM Variables
* `php_emergency_restart_interval`: Interval of time to determine when a graceful restart in seconds.
* `php_emergency_restart_threshold`: Number of child processes exit with SIGSEGV or SIGBUS signal.
* `php_log_level`: Error log level.
* `php_process_control_timeout`: Time limit for child processes to wait for a reaction on signals from master in seconds.

##### PHP-FPM POOL Variables
* `php_user`: Unix user of processes.
* `php_group`: Unix group of processes.
* `php_listen_backlog`: The maximum rate at which a server can accept new TCP connections on a socket.
* `php_listen_owner`: Listen owner user.
* `php_listen_group`: Listen owner group.
* `php_listen_mode`: Listen permissions.
* `php_pm`: Child process control manager.
* `php_pm_max_requests`: The number of requests each child process should execute before respawning.

##### Service Mesh
* `environments`: Define the service environment.
* `datacenter`: Define the DataCenter.
* `domain`: Define the Domain.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_prot`: The consul Hypertext Transfer Protocol.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
- Ansible versions >= 2.8
- Python >= 2.7.5

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' php_version='56'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  roles:
     - role: ansible-role-linux-phpfpm
       php_version: '56'
```

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

```yaml
php_version: '56'
php_fpm_port: '9000'
php_fpm_exporter_port: '9253'
php_allow_url_fopen: 'On'
php_allow_url_include: 'Off'
php_date_timezone: 'Asia/Shanghai'
php_default_socket_timeout: '60'
php_error_log: 'syslog'
php_expose_php: 'Off'
php_file_uploads: 'On'
php_max_execution_time: '60'
php_max_file_uploads: '20'
php_max_input_time: '60'
php_memory_limit: '256'
php_post_max_size: '2'
php_realpath_cache_size: '16'
php_upload_max_filesize: '5'
php_upload_tmp_dir: '/tmp'
php_emergency_restart_interval: '60'
php_emergency_restart_threshold: '20'
php_log_level: 'notice'
php_process_control_timeout: '10'
php_user: 'nobody'
php_group: 'nobody'
php_listen_backlog: '16384'
php_listen_owner: 'nobody'
php_listen_group: 'nobody'
php_listen_mode: '0660'
php_pm: 'dynamic'
php_pm_max_requests: '300'
environments: 'Development'
datacenter: 'dc01'
domain: 'local'
tags:
  subscription: 'default'
  owner: 'nobody'
  department: 'Infrastructure'
  organization: 'The Company'
  region: 'China'
exporter_is_install: false
consul_public_register: false
consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
consul_public_http_prot: 'https'
consul_public_http_port: '8500'
consul_public_clients:
  - '127.0.0.1'
```

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
