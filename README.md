# offboarding-as-code

## Problem
Manual user offboarding in multiple systems was time consuming and prone to errors.

## Solution
Centralized offboarding pipeline based on Ansible, with an optional GitLab CI job.

## Structure
- `ansible/offboard_user.yml` orchestration playbook.
- `ansible/tasks/*` per-system tasks.
- `ansible/group_vars/all.example.yml` example non-secret configuration (copy to `all.yml`).
- `ansible/group_vars/secrets.example.yml` example secrets (copy to `secrets.yml` and use vault or CI vars).
- `.gitlab-ci.yml` example CI job.

## Supported systems (current playbook)
- RocketChat
- Redmine
- GitLab
- Atlassian (organization level)

## Usage (local)
```bash
ansible-playbook -i localhost ansible/offboard_user.yml -e email=user@example.com
```

## Usage (GitLab CI)
- Set CI variables: `OFFBOARD_EMAIL` and `ANSIBLE_VAULT_PASSWORD`.
- Run the `offboard_user` job from the pipeline.

## Vault (local)
- Create `ansible/group_vars/secrets.yml` and encrypt it with `ansible-vault`.
- Provide the password with `--vault-password-file` (same approach as in CI).

## Run only selected systems
- Use tags, for example:
```bash
ansible-playbook -i localhost ansible/offboard_user.yml -e email=user@example.com --tags gitlab
```

## Variables
- Required: `email` or `OFFBOARD_EMAIL`.
- RocketChat: `rocketchat_url`, `rocketchat_auth_token`, `rocketchat_auth_user_id`, `rocketchat_page_size`.
- Redmine: `redmine_url`, `redmine_api_key`, `redmine_page_size`, `redmine_max_pages`.
- GitLab: `gitlab_url`, `gitlab_api_key`.
- Atlassian: `atlassian_url`, `atlassian_org_id`, `atlassian_dir_id`, `atlassian_api_key`.
