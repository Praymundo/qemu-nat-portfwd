# QEMU Port-Forward hook

QEMU hook to port-forward when using NAT network.  
This script aims to be easy to use / change and not fail proof.  

## How-to-use

- Stop all VMs
- Place the file on the LibVirt's hooks folder
  - `/etc/libvirt/hooks/qemu`
    - **qemu** is the file name
- Give the file execution permission
  - `chmod +x /etc/libvirt/hooks/qemu`
- Modify the script to your needs changing the calls to `create_chain` and `create_rule`
- Start your VMs

## Check chain / rules

You can check the iptables chain / rules created using the command:
- `iptables -vnL -t nat`
- `iptables -vnL`

## Motivation / Caveat

My main motivation for this script is the usage with firewall (e.g. CSF) that reset iptable chain / rules when they restart (after an update, for example).  
If this is your environment just restart libvirt daemon after your firewall rebuild it's iptable rules and libvirt should rebuild your VMs chain / rules.
