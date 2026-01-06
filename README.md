# offboarding-as-code

## Problem
Manual user offboarding in multiple systems was time consuming and prone to errors.

## Solution
Centralized offboarding pipeline based on Ansible and GitLab CI.

## Structure
- `ansible/offboard_user.yml` orchestration playbook.
- `ansible/tasks/*` per-system tasks.
- `ansible/group_vars/all.example.yml` example non-secret configuration (copy to `all.yml`).
- `ansible/group_vars/secrets.example.yml` example secrets (copy to `secrets.yml` and use vault or CI vars).

## Usage
```bash
ansible-playbook ansible/offboard_user.yml -e email=user@example.com
```

## Variables
- Required: `email` or `OFFBOARD_EMAIL`.
- RocketChat: `rocketchat_url`, `rocketchat_auth_token`, `rocketchat_auth_user_id`, `rocketchat_page_size`.
- Redmine: `redmine_url`, `redmine_api_key`, `redmine_page_size`, `redmine_max_pages`.
