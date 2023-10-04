# Ansible role for shairport-sync
This role deploys and configures mikebrady/shairport-sync to
run in a docker container.

Features:
- shairport-sync in docker container
- docker container runs in bridge network mode (default, more secure) or host network mode
- ipv6 support (if your docker is configured for ipv6)

# Requirements
Provisioning host:
- ansible 2.9 or later

Host that will run pihole:
- Ubuntu 18.04 or later
- docker
 - An ansible role for installing docker is available from https://github.com/elgeeko1/elgeeko1-docker-ansible.git

# How to use this role
### Method 1: Install using ansible-galaxy

The most robust way to install this role is to use ansible-galaxy,
which is installed with ansible by default. ansible-galaxy is effectively a package manager for ansible. It installs roles
from the community, or from private git repos, into your local machine for use in your playbooks.

Start by adding this role to an ansible-galaxy dependency file. Typically this file lives alongside your playbook file and by convention is named `requirements.yml`.

Add the following section to `requirements.yml`:

```
roles:
  - name: elgeeko1-shairport-sync-ansible
    src: https://github.com/elgeeko1/elgeeko1-shairport-sync-ansible
    version: main
```

If there is already a `roles` section, simply append this role to
add it as a dependency.

Then, install the role using ansible-galaxy:

`ansible-galaxy install -r requirements.yml -v`

### Method 2: Clone this repository into a `roles` directory

Use this method if you plan to modify this role, or if for some
reason the ansible-galaxy method fails.

Starting from your playbook directory, change into the `roles`
directory and clone:

```
$ ls
 > playbook.yml
 > roles/
$ cd roles/
roles$ git clone https://github.com/elgeeko1/elgeeko1-shairport-sync-ansible
```

# Configuring
Configurable variables are defined in `defaults/main.yml`.

# Security

### Bridged network mode (default)
By default, shairport will run in a docker container within the default docker bridge network.
This is the most secure as it has the most restrictive network access, however it can be more difficult to debug issues.

Bridged network mode is set with the role variable
`shairport_network_mode: bridge`

### Host network mode
This is less secure but is a more surefire configuration.

Host network mode is set with the role variable
`shairport_network_mode: host`
