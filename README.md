# turing-pi-ansible

An example Playbook (with Roles) to automate the provisioning of K3s and ancillary tooling on a Turing Pi cluster.

## Tasks Performed:

1. Format and mount NVME drive to `/mnt/data`
2. Install K3s (1 Server, 3 Agents)
3. Install Gateway API CRD's
4. Install Cilium with BGP Peering
5. Install Cert Manager
6. Install ArgoCD (used for long term management)

## Diagram

![Diagram of environment](/images/turing-pi.drawio.png)

## Run

Initiate the install:

* `ansible-playbook ./playbooks/bootstrap.yml -i ./inventory/hosts.ini --ask-vault-pass`

Delegate management of the cluster to ArgoCD:

* `ansible-playbook ./playbooks/delegate.yml -i ./inventory/hosts.ini`

## Removal

To remove K3s and contents of `/mnt/data` run `ansible-playbook ./playbooks/uninstall.yml -i ./inventory/hosts.ini`