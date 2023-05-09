# Red Hat Console ImageBuilder collection for Ansible

This collection contains a single role for using Red Hat Image Builder from console.redhat.com.

## Requirements

An Execution Environment with the required collections/libraries can be found [here](https://quay.io/repository/rh_ee_baddicks/image-builder-ee).

### Python Libraries

```txt
jmespath
```

### Ansible Collections

```yaml
- community.general
```

### Installation

```bash
ansible-galaxy collection install brianaddicks.rh_console_imagebuilder
```

## Usage

Generate a Red Hat offline api token [here](https://access.redhat.com/management/api). This value can either be provided as the variable `rhsm_offline_token` or the environment variable `REDHAT_API_OFFLINE_TOKEN`.

### Example AWS Build

```yaml
- name: Create image from console.redhat.com
  hosts: localhost
  connection: local
  gather_facts: no
  vars:
    - rhsm_offline_token: "MYTOKEN"
    - imagebuilder_distribution: rhel-9
    - imagebuilder_image_name: rhel9_aws
    - imagebuilder_image_type: aws
    - imagebuilder_image_packages:
      - python39
    - imagebuilder_architecture: x86_64
    - imagebuilder_activation_key: MY_RH_ACTIVATION_KEY
    - imagebuilder_organization_id: MY_RH_ORG_ID
    - imagebuilder_aws_account_number: MY_AWS_ACCOUNT_ID

  tasks:
    - ansible.builtin.import_role:
        name: brianaddicks.rh_console_imagebuilder.rh_console_imagebuilder
```
