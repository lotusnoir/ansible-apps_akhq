# Ansible Role: ansible-apps_akhq


## Description

[![Build Status](https://travis-ci.com/lotusnoir/ansible-apps_akhq.svg?branch=master)](https://travis-ci.com/lotusnoir/ansible-apps_akhq)[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)[![Ansible Role](https://img.shields.io/badge/ansible%20role-apps__akhq-blue)](https://galaxy.ansible.com/lotusnoir/ansible-apps_akhq/)[![GitHub tag](https://img.shields.io/badge/version-latest-blue)](https://github.com/lotusnoir/ansible-apps_akhq/tags)

Deploy [akhq](https://github.com/tchiotludo/akhq) kafka admin system using ansible.


## Role variables

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `akhq_version` | 0.15.0 | akhq version |
| `akhq_install_dir` | /opt/akhq | Installation path for jar file |
| `akhq_admin_passwd` | "securepassword" | admin password to access akhq |
| `kafka_bootstrap_servers` | "" | list of kafka servers |

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

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
