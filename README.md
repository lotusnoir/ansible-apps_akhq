# ansible-apps_akhq

## Description

[![Galaxy Role](https://img.shields.io/badge/galaxy-apps_akhq-purple?style=flat)](https://galaxy.ansible.com/lotusnoir/apps_akhq)
[![Version](https://img.shields.io/github/release/lotusnoir/ansible-apps_akhq.svg)](https://github.com/lotusnoir/ansible-apps_akhq/releases/latest)
![GitHub repo size](https://img.shields.io/github/repo-size/lotusnoir/ansible-apps_akhq?color=orange&style=flat)
[![downloads](https://img.shields.io/ansible/role/d/53225)](https://galaxy.ansible.com/lotusnoir/apps_akhq)
![Ansible Quality Score](https://img.shields.io/ansible/quality/53225)
[![License](https://img.shields.io/badge/license-Apache--2.0-brightgreen?style=flat)](https://opensource.org/licenses/Apache-2.0)


Deploy [akhq](https://github.com/tchiotludo/akhq) kafka admin system using ansible.

## Dependencies

You need to install java
Recommanded role is lotusnoir.apps_java

## Role variables

| Name                      | Default Value    | Description                        |
| ------------------------- | ---------------- | -----------------------------------|
| `akhq_version`            | 0.18.0           | akhq version |
| `akhq_install_dir`        | /opt/akhq        | Installation path for jar file |
| `akhq_admin_passwd`       | "securepassword" | admin password to access akhq |
| `akhq_ldap_server`        | ""               | ldap server |
| `akhq_ldap_bindn`         | ""               | ldap user bindn |
| `akhq_ldap_bindpwd`       | ""               | ldap user passwd |
| `akhq_ldap_search_base`   | ""               | ldap search base |
| `akhq_ldap_group_enable`  | ""               | ldap group check |
| `akhq_ldap_group_base`    | ""               | ldap group base |

## Examples

	---
	- hosts: apps_akhq
	  become: yes
	  become_method: sudo
	  gather_facts: yes
	  roles:
	    - role: ansible-apps_akhq
         vars:
           suffix: ':9092'
           kafka_bootstrap_servers:
             - name: kafka_cluster
               servers: "{{ groups['kafka_cluster'] | product([suffix]) | map('join') | join(',') }}"
   	  environment: 
   	    http_proxy: "{{ http_proxy }}"
   	    https_proxy: "{{ https_proxy }}"
   	    no_proxy: "{{ no_proxy }}

## License

This project is licensed under Apache License. See [LICENSE](/LICENSE) for more details.
