Role Name
=========

An opinionated role that installs [Just](https://just.systems)

Requirements
------------

This role requires two separate tools be installed.

First it requires the 'ansible.utils' collection be installed from Ansible-Galaxy via:

```shell
ansible-galaxy collection install ansible.utils
```

Secondly it requires the `jsonschema` Python package be installed via:

```shell
pip3 install jsonschema
```


Role Variables
--------------

`just` : [mapping] (required) contains the following fields:

* `versions` : [array of strings] (optional)

    A list of valid Just versions that should be fetched and extracted to `just_path`.

* `default` : [string] (optional)

    The version that should be set as system default. If the version does not exist the task will fail.

* `trim`: [boolean] (optional)

    If true indicates that all non linked directories under `just_path` that do not correspond to version numbers defined inside `versions` should be removed.


`just_path` : [string] (optional) The path at which `Just` will be extracted to.

Example:

```yaml
- just:
    - trim: true
    - default: "1.1.1"
    - versions:
      - "1.1.1"
      - "1.2.2"
 ```


Dependencies
------------

None, other then previously stated requirements.

Setup
-----

Before the role can be used it needs to be added to the machine running the playbook, and as of writing this, this role is not hosted on Ansible-Galaxy only on Github.

1. Create a `requirements.yml` file in the root directory of the playbook being worked on.

2. Add the following definition inside the `requirements.yml` file:

```yml
- name: hth-just
  src: https://github.com/hrafnthor/ansible-just.git
  scm: git
```

3. Install the requirements by executing

```shell
ansible-galaxy install -r .requirements.yml
```

This will allow any playbook run from this machine to use the role `hth-just`


Example Playbook
----------------


```yaml
- hosts: all
    vars:
    - just:
      - trim: true
      - default: "1.1.1"
      - versions:
        - "1.1.1"
        - "1.2.2"
  roles:
     - hth-just
```


License
-------

MIT license. See attached license file.

Author Information
------------------

Hrafn Thorvaldsson
Find me at https://www.hth.is
