# Ansible collection: kangaroot.foreman_content_rocky

Collection for configuring Rocky Linux repositories and Rocky Linux OS related content in a Foreman/Katello installation.

The Rocky Linux repositories that can be configured from this collection are:

Rocky Linux standard repositories:

- Rocky Linux 8[^1]:
  - BaseOS
  - AppStream
  - Extras
  - Plus
  - PowerTools
  - HighAvailability
  - NFV
  - ResilientStorage
  - Realtime

- Rocky Linux 9[^1]:
  - BaseOS
  - AppStream
  - Extras
  - Plus
  - Code Ready Builder
  - HighAvailability
  - NFV
  - ResilientStorage
  - Realtime
  - SAP
  - SAPHANA

Rocky Linux kickstart respositories:

- Rocky Linux 8 kickstart[^2]:
  - BaseOS
  - AppStream

- Rocky Linux 9 kickstart[^2]:
  - BaseOS
  - AppStream

Rocky Linux version specific repositories:

- Rocky Linux 8[^3]:
  - 8.4
  - 8.5
  - 8.6
  - 8.7
  - 8.8
  - 8.9
  - 8.10

- Rocky Linux 9[^3]:
  - 9.0
  - 9.1
  - 9.2
  - 9.3
  - 9.4
  - 9.5

Rocky Linux SIGs:

- SIG/Core
- SIG/Cloud
- SIG/HPC
- SIG/Kernel (Rocky Linux 9 only)
- SIG/Security

[^1]: Enabled by default when enabling Rocky Linux repositories.
[^2]: Enabled by default when enabling a Rocky Linux release repository.
[^3]: All standard Rocky Linux and kickstart repositories are included for each version.

## Requirements and Dependencies

Ansible Core 2.13.0 or higher is required for the roles in the collection.

The roles in this collection must be imported by the `kangaroot.foreman` collection. It is possible to directly use the roles in this collection but not recommended.

The `kangaroot.foreman` collection requires the `theforeman.foreman` and `theforeman.operations` collections. To install the required collections, execute:

```shell
ansible-galaxy collection install -r requirements.yml
```

in the collection directory.

## Collection Variables

The group_vars directory contains example vars files for the important variables used in the collection roles.

## Usage

The variable `foreman_content_roles` from the `foreman` role in the `kangaroot.foreman` collection contains a list content roles to import.

Add this collection content role to the `foreman_content_roles` list of content roles to import in your playbook project variables.

For example, add the `foreman_content_roles` variable in your `group_vars/foreman.yml` file of your playbook project:

```yaml
# Foreman content roles to include
foreman_content_roles:
  # Package only content
  - ...

  # OS content
  - kangaroot.foreman_content_rocky.foreman_content_rocky
  - ...

  # Builtin content
  - kangaroot.foreman_content_builtin.foreman_content_builtin
```

Also ensure that the Rocky Linux repositories are enabled and additional Rocky Linux version and/or SIG repositories as well by setting the appropriate enable variables:

```yaml
foreman_enable_rocky: true
```

In your playbook, add a task to execute the `kangaroot.foreman.foreman` role:

```yaml
- name: Run kangaroot.foreman roles
  hosts: foreman
  roles:
    - kangaroot.foreman.foreman
```

