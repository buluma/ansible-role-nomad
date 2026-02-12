# [Ansible role nomad](#ansible-role-nomad)

Install and configure Nomad.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-nomad/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-nomad/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-nomad/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-nomad)|[![downloads](https://img.shields.io/ansible/role/d/buluma/nomad)](https://galaxy.ansible.com/buluma/nomad)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-nomad.svg)](https://github.com/buluma/ansible-role-nomad/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-nomad/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

  pre_tasks:
    - name: Update apt cache.
      apt: update_cache=yes cache_valid_time=600
      when: ansible_os_family == 'Debian'
      changed_when: false

  roles:
    - role: buluma.core_dependencies
    - role: buluma.hashicorp
    - role: buluma.nomad
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-nomad/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  gather_facts: false
  become: true

  roles:
    - role: buluma.bootstrap
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-nomad/blob/master/defaults/main.yml):

```yaml
---
# defaults file for nomad

# You can install nomad using a package in this role. If you have installed
# nomad manually, set this to `false`.
nomad_install_package: true

# Set this to "true" for a server.
nomad_server: true

# Configuration items for the Nomad server
nomad_server_data_dir: /tmp/server
nomad_server_bind_addr: "0.0.0.0"
nomad_server_log_level: INFO

# How many servers and agents are expected?
nomad_server_bootstrap_expect: 1

# This this to "true" for an agent.
nomad_agent: false

# Configuration items for the Nomad agent
nomad_agent_log_level: INFO
nomad_agent_data_dir: /tmp/agent
nomad_agent_name: "{{ inventory_hostname }}"

nomad_agent_servers:
  - name: "127.0.0.1"
    port: 4647
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-nomad/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-core_dependencies)|
|[buluma.hashicorp](https://galaxy.ansible.com/buluma/hashicorp)|[![Build Status GitHub](https://github.com/buluma/ansible-role-hashicorp/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-hashicorp/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-hashicorp/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-hashicorp)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-nomad/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-nomad/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-nomad/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

