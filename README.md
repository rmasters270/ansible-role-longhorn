# DEPRECATED: Longhorn

***This role will be depreciated use the collection, [rmasters270.kubernetes](https://github.com/rmasters270/ansible-collection-kubernetes).***

Install Longhorn on a Kubernetes cluster.

[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-longhorn-blue.svg)](https://galaxy.ansible.com/ui/standalone/roles/rmasters270/longhorn)

## Requirements

### Default Storage Class

Longhorn will be set as the default storage class. The role can remove previously defined default StorageClasses, however, system StorageClasses will be reassigned to default after the cluster is rebooted.  To disable the local-storage class use `--disable local-storage` when installing k3s.

### Localhost

The role is intended to run from the Ansible controller.  If the playbook is executed on a different host it will fail because the templates must be copied to the target host.

### Kube Config

The host and user running the playbook must have kube config configured.

### Helm

The host must have the Helm package manager installed.

## Role Variables

| Variable                 | Required | Default                      | Comments                                                                                                                                                                                             |
| ------------------------ | -------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| longhorn_namespace       | yes      | longhorn-system              | Kubernetes namespace                                                                                                                                                                                 |
| longhorn_repo_name       | yes      | longhorn                     | Helm repository name                                                                                                                                                                                 |
| longhorn_repo_url        | yes      | <https://charts.longhorn.io> | Helm repository URL                                                                                                                                                                                  |
| longhorn_repo_version    | yes      | 1.5.1                        | Helm chart version                                                                                                                                                                                   |
| longhorn_default_storage | yes      | false                        | Longhorn will automatically be set as the default.  Change this value to `true` to remove the the default status from other StorageClasses. System default storage classes will return after reboot. |

## Dependencies

Use `rmasters270.helm` role or install `kubernetes cli` and `helm` manually on the host.

Setup `kube config` for the user account and host.

## Example Playbook

```yaml
- hosts: k3s_nodes

  roles:
    - rmasters270.longhorn_node

- hosts: localhost

  roles:
    - rmasters270.helm
    - rmasters270.longhorn
```

## License

MIT

## Author Information

Ryan Masters
