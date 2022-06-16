# Longhorn

Install Longhorn on a Kubernetes cluster.

## Requirements

### Default Storage Class

Longhorn will be set as the default storage class. The role can remove previously defined default StorageClasses, however, system StorageClasses will be reassigned to default after the cluster is rebooted.  To disable the local-storage class use `--no-deploy=local-storage` when installing k3s.

### Localhost

The role is intended to run from the Ansible controller.  If the playbook is executed on a different host it will fail because the templates must be copied to the target host.

### Kube Config

The host and user running the playbook must have kube config configured.

### Helm

The host must have the Helm package manager installed.

## Role Variables

### longhorn_namespace

Change the Kubernetes namespace for Longhorn.

default: `longhorn`

### longhorn_default_storage

Longhorn will automatically be set as the default.  Change this value to `true` to insure Longhorn is the default and the default status is removed from all other StorageClasses.

default: `false`

### longhorn_repo_name

Name of the Helm repository.

default: `longhorn-system`

### longhorn_repo_url

Url pointing to the Helm repository.

default: `https://charts.longhorn.io`

### longhorn_repo_version

Chart version in the repository.

The default value is pinned to the latest version at the time of writing.  Use `helm search repo longhorn` to list all versions of the chart.

default: `1.2.4`

## Dependencies

Use `rmasters270.helm` role or install `kubernetes cli` and `helm` manually on the host.

Setup `kube config` for the user account and host.

## Example Playbook

```yaml
- hosts: localhost

  roles:
    - rmasters270.helm
    - rmasters270.longhorn
```

## License

MIT

## Author Information

Ryan Masters
