# Ansible Role: ansible-apps_akhq


## Description

[![Build Status](https://travis-ci.com/lotusnoir/ansible-apps_akhq.svg?branch=master?style=flat)](https://travis-ci.com/lotusnoir/ansible-apps_akhq)
[![License](https://img.shields.io/badge/license-Apache--2.0-brightgreen?style=flat)](https://opensource.org/licenses/Apache-2.0)
[![Ansible Role](https://img.shields.io/badge/galaxy-apps_akhq-purple?style=flat)](https://galaxy.ansible.com/lotusnoir/apps_akhq)
![GitHub repo size](https://img.shields.io/github/repo-size/lotusnoir/ansible-apps_akhq?color=orange&style=flat)
![Ansible Quality Score](https://img.shields.io/ansible/quality/52300)
[![downloads](https://img.shields.io/ansible/role/d/52300)](https://galaxy.ansible.com/lotusnoir/apps_akhq)
[![Version](https://img.shields.io/github/release/lotusnoir/ansible-apps_akhq.svg)](https://github.com/lotusnoir/ansible-apps_akhq/releases/)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=lotusnoir_ansible-apps_akhq&metric=alert_status)](https://sonarcloud.io/dashboard?id=lotusnoir_ansible-apps_akhq)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=lotusnoir_ansible-apps_akhq&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=lotusnoir_ansible-apps_akhq)
[![Reliability Rating](https://sonarcloud.io/api/project_badges/measure?project=lotusnoir_ansible-apps_akhq&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=lotusnoir_ansible-apps_akhq)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=lotusnoir_ansible-apps_akhq&metric=security_rating)](https://sonarcloud.io/dashboard?id=lotusnoir_ansible-apps_akhq)

Deploy [akhq](https://github.com/tchiotludo/akhq) kafka admin system using ansible.

## Dependencies

You need to install java
Recommended role is geerlingguy.java

## Role variables

| Name                      | Default Value    | Description                        |
| ------------------------- | ---------------- | -----------------------------------|
| `akhq_version`            | 0.15.0           | akhq version |
| `akhq_install_dir`        | /opt/akhq        | Installation path for jar file |
| `akhq_config_dir`         | /etc/akhq        | Configuration path for application |
| `akhq_jar_file`           | akhq.jar         | Name of the jar file |
| `akhq_admin_passwd`       | "securepasswd"   | admin password to access akhq |
| `akhq_reader_passwd`      | "readpasswd"     | read-only password to access akhq |
| `akhq_ldap_server`        | ""               | ldap server |
| `akhq_ldap_bindn`         | ""               | ldap user bindn |
| `akhq_ldap_bindpwd`       | ""               | ldap user passwd |
| `akhq_ldap_search_base`   | ""               | ldap search base |
| `akhq_ldap_group_enable`  | ""               | ldap group check |
| `akhq_ldap_group_base`    | ""               | ldap group base |
| `akhq_ldap_enabled`		| false			   | enable ldap authorization |
| `akhq_listener_port` 		| 8081			   | port for the listener to use |
| `akhq_listener_ssl`		| false			   | whether to enable SSL |
| `akhq_listener_ssl_self_signed` | false      | whether to use a self-signed certificate for SSL |
| `java_bin`       			| /bin/java 	   | location of java; typically /bin/java or /usr/bin/java |

## Examples

	---
	- hosts: apps_akhq
	  become: yes
	  become_method: sudo
	  gather_facts: yes
	  roles:
	    - role: ansible-apps_akhq
      vars:
	  	# enable SSL
	  	akhq_listener_port: 9443
		akhq_listener_ssl: true
		akhq_listener_ssl_self_signed: true
		akhq_admin_passwd: myAdminPwd
		akhq_reader_passwd: myReaderPwd
        suffix: ':9092'
        kafka_bootstrap_servers:
          - name: kafka_cluster
            servers: "{{ groups['kafka_cluster'] | product([suffix]) | map('join') | join(',') }}"
			custom_properties:
			  security.protocol: SSL
			  ssl.truststore.location: /var/ssl/private/truststore.jks
			  ssl.truststore.password: trustStorePwd
			  ssl.keystore.location: /var/ssl/private/keystore.jks
			  ssl.keystore.password: keyStorePwd
			  ssl.key.password: KeyStorePwd
	  environment: 
	    http_proxy: "{{ http_proxy }}"
	    https_proxy: "{{ https_proxy }}"
	    no_proxy: "{{ no_proxy }}"

## License

This project is licensed under Apache License. See [LICENSE](/LICENSE) for more details.
