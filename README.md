# Ansible Role: Sonatype Nexus

This Ansible role installs and configures Sonatype Nexus Repository Manager 3.

## Requirements

* Ansible 2.15 or higher
* Supported operating systems:
    * OracleLinux 9

## Variables
* `nexus_version`: The version of Nexus to install (default: 3.76.1-01).
* `nexus_admin_password`: Password for the Sonatype Nexus administrator account (default: password).
* `nexus_bind_port`: Port for incoming connections (default: 8081).

## Playbook example
```yaml
---
- hosts: all
  become: yes

  tasks:

  - ansible.builtin.include_role:
      name: nexus
    vars:
      nexus_admin_password: "password"
      nexus_bind_port: 8081
      nexus_anonymous_access: "true"
      nexus_yum_proxy_repositories:
      - name: hashicorp-rhel-proxy
        url: https://rpm.releases.hashicorp.com/RHEL
      nexus_docker_proxy_repositories:
      - name: dockerhub-proxy
        url: https://registry-1.docker.io 
        index_type: "HUB"
      nexus_docker_groups:
      - name: docker-proxy-all
        members: ['dockerhub-proxy']
        http_port: 5000
      nexus_pypi_proxy_repositories:
      - name: pypi-proxy
        url: https://pypi.org
      nexus_raw_proxy_repositories:
      - name: flatcar-stable-proxy
        url: https://stable.release.flatcar-linux.net

```

## Test
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install pip --upgrade
pip install -r requirements.txt

molecule test --all
```