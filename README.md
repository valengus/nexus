# Ansible Role: Sonatype Nexus

This Ansible role installs and configures Sonatype Nexus Repository Manager 3.

## Requirements

* Ansible 2.15 or higher
* Supported operating systems:
    * OracleLinux 9

## Variables
* `nexus_version`: The version of Nexus to install (default: 3.76.1-01)

## Playbook example
```yaml
---
- hosts: all
  become: yes

  tasks:

  - ansible.builtin.include_role:
      name: nexus

```

## Test
```bash
molecule test --all
```