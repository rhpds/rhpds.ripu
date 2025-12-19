# enable_upgrade_repos

Enable upgrade repositories for RHEL In-Place Upgrade (RIPU) workflows.

## Description

This role enables access to higher RHEL version repositories on hosts to support in-place upgrades using Leapp:

- RHEL 7 hosts → enables RHEL 8 repos
- RHEL 8 hosts → enables RHEL 9 repos
- RHEL 9 hosts → enables RHEL 10 repos

## Requirements

- Host must be registered to Red Hat Satellite
- `host_satellite_repositories` role must run first to configure Satellite registration
- Entitlement certificates must be present in `/etc/pki/entitlement/`

## Role Variables

### Defaults

| Variable | Default | Description |
|----------|---------|-------------|
| `enable_upgrade_repos_enabled` | `true` | Enable or disable this role |

### Required Variables (from host_satellite_repositories role)

| Variable | Description |
|----------|-------------|
| `host_satellite_repositories_hostname` | Satellite server hostname |
| `host_satellite_repositories_org` | Satellite organization name |

## Dependencies

- `host_satellite_repositories` - Must run before this role

## Example Playbook

```yaml
- hosts: all
  roles:
    - host_satellite_repositories
    - rhpds.ripu.enable_upgrade_repos
```

## AgnosticV Integration

Add to your AgnosticV `common.yaml`:

```yaml
pre_software_workloads:
  all:
    - host_satellite_repositories
    - rhpds.ripu.enable_upgrade_repos
```

## License

GPLv3

## Author

Mitesh Sharma (msharma@redhat.com)
Red Hat Demo Platform (RHDP)
