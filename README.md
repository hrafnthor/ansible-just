# Ansible Just

An opinionated role that installs [Just](https://just.systems)

## Requirements

This role requires two separate collections be installed.

First it requires the `ansible.utils` collection be installed from Ansible-Galaxy via:

```shell
ansible-galaxy collection install ansible.utils
```

Secondly it requires the `community.general` collection to be installed from Ansible-Galaxy via:

```shell
ansible-galaxy collection install community.general
```

It then also requires the `jsonschema` Python package be installed via:

```shell
pip3 install jsonschema
```

## Role Variables

All variables are optional unless otherwise marked as required.

```yaml
just:
  remove:     [bool]          Indicates if just should be removed
  trim:       [bool]          Indicates if non default versions should be removed
  default:    [string]        The version that should be set as default
  versions:   [string array]  A list of versions that should be installed
  completions:
    bash:     [string array]  A list of all users that should have bash completions added
    zsh:      [string array]  A list of all users that should have zsh completions added
    ohmyzsh:  [string array]  A list of all users that should have ohmyzsh completions added
    fish:     [string array]  A list of all users that should have fish completions added
```

`just` : [mapping] (required) contains the following fields:

* `versions` : [array of strings] (optional)

    A list of valid Just versions that should be fetched and extracted to `just_path`.

* `default` : [string] (optional)

    The version that should be set as system default. If the version does not exist the task will fail.

* `trim`: [boolean] (optional)

    If true indicates that all non linked directories under `just_path` that do not correspond to version numbers defined inside `versions` should be removed.

### Defaults

`just_default_path` : [string] (optional) The path at which `Just` will be extracted to. Defaults to `/opt/just`

`just_default_zsh_completion_path` : [string] (optional) The at which auto completion file will be generated for `zsh`. Is always relative to a user's home directory. Defaults to `.local/share/zsh/completions`

`just_default_ohmyzsh_completion_path` : [string] (optional) The at which auto completion file will be generated for `ohmyzsh`. Is always relative to a user's home directory. Defaults to `.oh-my-zsh/completions`

`just_default_bash_completion_path` : [string] (optional) The at which auto completion file will be generated for `bash`. Is always relative to a user's home directory. Defaults to `.local/share/bash-completion/completions`

`just_default_fish_completion_path` : [string] (optional) The at which auto completion file will be generated for `fish`. Is always relative to a user's home directory. Defaults to `.config/fish/completions`

Example:

```yaml
just:
  remove: false
  trim: true
  default: "1.1.1"
  versions:
    - "1.1.1"
    - "1.2.2"
  completions:
    bash:
      - odinn
    zsh:
      - loki
    ohmyzsh:
      - loki
      - thor
 ```


## Dependencies

None, other then previously stated requirements.

## Setup

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


## Example Playbook


```yaml
- hosts: all
    vars:
    - just:
        trim: true
        default: "1.1.1"
        versions:
        - "1.1.1"
        - "1.2.2"
        completions:
          bash:
            - odinn
          zsh:
            - loki
          ohmyzsh:
            - loki
            - thor
  roles:
     - hth-just
```


## License

```
MIT License

Copyright (c) 2023 Hrafn Þorvaldsson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### Author Information

Hrafn Thorvaldsson
Find me at https://www.hth.is
