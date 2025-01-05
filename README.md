# Ansible Pycharm

This role will download, extract and configure Jetbrains PyCharm.

---

## Requirements


This role requires two separate tools be installed.

First it requires the 'ansible.utils' collection be installed from Ansible-Galaxy via:

```shell
ansible-galaxy collection install ansible.utils
```

Secondly it requires the `jsonschema` Python package be installed via:

```shell
pip install jsonschema
```

## Setup

Before the role can be used it needs to be added to the machine running the playbook, and as of writing this, this role is not hosted on Ansible-Galaxy only on Github.

1. Create a requirements.yml file in the root directory of the playbook being worked on.

2. Add the following definition inside the requirements.yml file:

```yaml
- name: hth-jetbrains-pycharm
  src: https://github.com/hrafnthor/ansible-jetbrains-pycharm.git
  scm: git
````

3. Install the requirements by executing

```yaml
ansible-galaxy install -r .requirements.yml
```

This will allow any playbook run from this machine to use the role hth-jetbrains-pycharm.

### Variables


All variables are optional unless otherwise stated.

```yaml
pycharm:
  remove: [boolean] If present, will remove all installation and configuration made by the role
  location:
    path: [string]  The installation location where community and professional versions will be installed. Defaults to '/opt/jetbrains/pycharm'
    owner: [string] The owner of the installation location. Defaults to 'root'.
    group: [string] The group owning the installation location. Defaults to 'root'
    mode: [string]  The mode for the installation location. Defaults to '0755'
  clients:
    professional:
      version: [string] The version to install. Find it at https://www.jetbrains.com/pycharm/download/other.html [required if installing]
      checksum: [string] The checksum of the version archive. See below. [required if installing]
      remove: [boolean] Indicates if this edition should be removed.
      desktop: [boolean] Indicates if a desktop entry should be created
    community:
      version: [string] The version to install. Find it at https://www.jetbrains.com/pycharm/download/other.html [required if installing]
      checksum: [string] The checksum of the version archive. See below. [required if installing]
      remove: [boolean] Indicates if this edition should be removed.
      desktop: [boolean] Indicates if a desktop entry should be created
    cli:
      edition: [community, professional] Indicates the edition that should be linked
      remove: [boolean] Indicates if the cli link should be removed

```

Checksums for versions can be found by locating the appropriate tar archive [here](https://www.jetbrains.com/pycharm/download/other.html) and navigating to the url linked with `.sha256` appended (for example https://download.jetbrains.com/python/pycharm-professional-2024.3.1.1.tar.gz.sha256).

#### Example Playbook


```yaml
 - hosts: all
      vars:
        pycharm:
          location:
            group: "developers"
            mode: "2774"
          clients:
            professional:
              version: "2024.3.1.1"
              checksum: "5698131d93d00a261c720a31ec54ef1c850581c274be6938dd923e8c0383da25"
              desktop: true
          cli:
            edition: professional
      roles:
         - hth-jetbrains-pycharm
```

License
-------

Apache License 2.0. See attached license file.

Author Information
------------------

Hrafn Thorvaldsson.
http://www.hth.is
