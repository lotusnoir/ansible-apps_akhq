# ansible-apps_akhq

## Description

[![Galaxy Role](https://img.shields.io/badge/galaxy-apps_akhq-purple?style=flat)](https://galaxy.ansible.com/lotusnoir/apps_akhq)
[![Version](https://img.shields.io/github/release/lotusnoir/ansible-apps_akhq.svg)](https://github.com/lotusnoir/ansible-apps_akhq/releases/latest)
![GitHub repo size](https://img.shields.io/github/repo-size/lotusnoir/ansible-apps_akhq?color=orange&style=flat)
[![downloads](https://img.shields.io/ansible/role/d/53225)](https://galaxy.ansible.com/lotusnoir/apps_akhq)
![Ansible Quality Score](https://img.shields.io/ansible/quality/53225)
[![License](https://img.shields.io/badge/license-Apache--2.0-brightgreen?style=flat)](https://opensource.org/licenses/Apache-2.0)

Deploy [akhq](https://github.com/tchiotludo/akhq) kafka admin system using ansible.

## Requirements

You need to install java - lotusnoir.apps_java

## Role variables

See [variables](/defaults/main.yml) for more details.

## Examples

        ---
        - hosts: apps_akhq
          become: true
          become_method: sudo
          gather_facts: true
          roles:
            - role: ansible-apps_akhq
          vars:
            suffix: ':9092'
            kafka_bootstrap_servers:
              - name: kafka_cluster
                servers: "{{ groups['kafka_cluster'] | product([suffix]) | map('join') | join(',') }}"



## License

This project is licensed under Apache License. See [LICENSE](/LICENSE) for more details.

