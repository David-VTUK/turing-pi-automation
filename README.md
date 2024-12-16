# turing-pi-ansible

An example Playbook (with Roles) to automate the provisioning of K3s and ancillary tooling on a Turing Pi cluster.

## Tasks Performed:

1. Format and mount NVME drive to `/mnt/data`
2. Install K3s (1 Server, 3 Agents)
3. Install Gateway API CRD's
4. Install Cilium with BGP Peering
5. Install Cert Manager

## Diagram

![Diagram of environment](/images/turing-pi.drawio.png)

## Run

To run - `ansible-playbook ./playbooks/site.yml -i ./inventory/hosts.ini --ask-vault-pass`

## Reversal

To remove K3s and contents of `/mnt/data` run `ansible-playbook ./playbooks/site.yml -i ./inventory/hosts.ini --tags uninstall --ask-vault-pass`