# offboarding-as-code

## Problem
Manual user offboarding in multiple systems was time consuming and prone to errors.

## Solution
Centralized offboarding pipeline based on Ansible and GitLab CI.

## Structure
- `ansible/playbooks/offboard_user.yml` orchestration playbook.
- `ansible/roles/*` per-system roles with `tasks/main.yml` and `defaults/main.yml`.
- `ansible/group_vars/all.yml` non-secret configuration overrides.
- `ansible/group_vars/secrets.example.yml` example secrets (copy to `secrets.yml` and use vault or CI vars).

## Usage
```bash
ansible-playbook ansible/playbooks/offboard_user.yml -e email=user@example.com
```
