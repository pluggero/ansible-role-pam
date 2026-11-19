# Ansible Role: PAM (Pluggable Authentication Modules)

[![CI](https://github.com/pluggero/ansible-role-pam/actions/workflows/ci.yml/badge.svg)](https://github.com/pluggero/ansible-role-pam/actions/workflows/ci.yml) [![Ansible Galaxy downloads](https://img.shields.io/ansible/role/d/pluggero/pam?label=Galaxy%20downloads&logo=ansible&color=%23096598)](https://galaxy.ansible.com/ui/standalone/roles/pluggero/pam)

An Ansible Role that configures PAM authentication, password policy, and account lockout.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
pam_install_method: "package"
```

The method used to install PAM packages. The following methods are available:

- `package`: Installs from the package manager of the distribution

```yaml
pam_pwquality_retry: 3
```

Number of retries allowed when setting a new password before returning an error.

```yaml
pam_pwquality_minlen: 15
```

Minimum acceptable password length.

```yaml
pam_pwquality_difok: 5
```

Minimum number of characters that must differ from the previous password.

```yaml
pam_pwquality_minclass: 4
```

Minimum number of character classes required (uppercase, lowercase, digits, symbols).

```yaml
pam_pwhistory_remember: 400
```

Number of previous passwords to remember. Users cannot reuse any of the remembered passwords.

```yaml
pam_faillock_deny: 5
```

Number of consecutive failed login attempts before the account is locked.

```yaml
pam_faillock_unlock_time: 1800
```

Time in seconds after which a locked account is automatically unlocked.

```yaml
pam_faillock_even_deny_root: true
```

Apply the lockout policy to the root account as well.

```yaml
pam_password_aging_enabled: true
```

Enable password aging (`/etc/login.defs` and `/etc/shadow`).

```yaml
pam_pass_max_days: 365
pam_pass_warn_age: 14
```

Maximum password age and warning days before expiry. Applied to
`/etc/login.defs` (new accounts) and `/etc/shadow` (all existing accounts with a password).
Accounts whose password is older than `pam_pass_max_days` expire immediately.

```yaml
pam_password_aging_exclude_users:
  - root
```

Accounts whose `/etc/shadow` aging is left unchanged.

**Note:** Setting this variable replaces the default list. Add `root` again to keep it excluded:

```yaml
pam_password_aging_exclude_users:
  - root
  - svc_backup
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - pluggero.pam
```

## License

MIT / BSD

## Author Information

This role was created in 2026 by pluggero.
