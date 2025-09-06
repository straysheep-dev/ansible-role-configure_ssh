role_name
=========

![molecule workflow](https://github.com/straysheep-dev/ansible-role-configure_ssh/actions/workflows/molecule.yml/badge.svg) ![ansible-lint workflow](https://github.com/straysheep-dev/ansible-role-configure_ssh/actions/workflows/ansible-lint.yml/badge.svg)

This role configures both, the ssh server and it's components as well as the ssh default client configuration.

You can either run the "minimal" tasks to just enforce public key auth, or run the "compliance" tasks to apply a number of security options suggested by CIS, STIG, and other configuration guides. It also installs a [custom login banner](files/issue). The default setting is "compliance".

The following resources were used to build [files/sshd_config](files/sshd_config):

- [github.com/ComplianceAsCode/content](https://github.com/ComplianceAsCode/content)
- [Ubuntu 22.04 Server CIS Level 2 Guide](https://static.open-scap.org/ssg-guides/ssg-ubuntu2204-guide-cis_level2_server.html#!)
- [Ubuntu 20.04 STIG Guide](https://static.open-scap.org/ssg-guides/ssg-ubuntu2004-guide-stig.html#!)
- [github.com/drduh/config/sshd_config](https://github.com/drduh/config/blob/main/sshd_config)

> [!IMPORTANT]
> **Git Submodules & CI**: The dockerfiles for molecule tests are maintained in a [monorepo](https://github.com/straysheep-dev/docker-configs) as submodules for maintainability / repeatability across all roles. Because of this, the CI workflow requires `actions/checkout` to have `submodules: 'recursive'`.

Requirements
------------

None.

Role Variables
--------------

All variables are in [defaults/main.yml](defaults/main.yml).

**regenerate_hostkeys**

You can choose to force a regeneration of the SSH host keys. This is useful on preconfigured virtual machine images to ensure your keys are unique.

- `regenerate_hostkeys: false`, set to `true` to regenerate host keys.

**ssh_port**

Set a unique port for SSH to listen on. Default is 22.

- `ssh_port: 22`

**ssh_config_choice**

Options are `"compliance"` (default) or `"minimal"`.

- `ssh_config_choice: minimal`, Just enforces public key authentication by revoking password authentication.
- `ssh_config_choice: comliance`, Applies a mix of CIS Level 2, STIG, and other changes to lock SSH down without sacrificing usability.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yml
- name: "Default Playbook"
  hosts: all
    #some_group
  vars:
    ssh_config_choice: "compliance"
  roles:
    - role: straysheep_dev.configure_ssh
```


License
-------

- [MIT](./LICENSE)
- [github.com/drduh/config: MIT](https://github.com/drduh/config/blob/main/LICENSE)
- [github.com/ComplianceAsCode/content: BSD-3-Clause](https://github.com/ComplianceAsCode/content/blob/master/LICENSE)

Author Information
------------------

[straysheep-dev/ansible-configs](https://github.com/straysheep-dev/ansible-configs)
