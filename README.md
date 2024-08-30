# turing-pi-ansible

An example Playbook (with Roles) to automate the provisioning of K3s and ancillary tooling on a Turing Pi cluster.

## Tasks Performed:

1. Format and mount NVME drive to `/mnt/data`
2. Install K3s (1 Server, 3 Agents)
3. Install Gateway API CRD's
4. Install Cilium with BGP Peering
5. Install Cert Manager
6. Expose `Cillium's` Hubble UI via API Gateway

## Diagram

![Diagram of environment](/images/turing-pi.drawio.png)