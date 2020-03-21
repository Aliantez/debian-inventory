Ansible script to inventory debian systems to show and write to file information's:
hostname:
  IP:
  linux_version:
  kernel_version:
  apache_version: (if instaleld)
  apache_ports: (if apache work and listening)

example:
hostname: debian.localdomain
  IP: 192.168.0.5
  linux_version: 9.9
  kernel: 4.9.0-9-amd64
  apache_version: 2.4.25-3+deb9u7
  apache_ports: [80]

this script will add CA file from (default ../cert/CA.crt) local machine to remote servers and update ca-certs.

dependencies:
on the remote hosts you need installed
 - net-tools - (netstat) it's necessary to read TCP ports
 - python-apt - its important to get installed packages
 - ca-certification - its needed to update certs

usage:

In the inventory file in section [debian] define your ip adressess range

for example if you want work on 192.168.0.2 - 192.168.0.50:

[debian]
192.168.0.[2:50]

if you need more subnets only add next line bellow:

[debian]
192.168.0.[2:50]
172.16.0.[100:120]

username, password and file path was defined and explained in inventory file

for systems never connected before (ssh fingerprint is not present in know_hosts) you need ANSIBLE_HOST_KEY_CHECKING=false in variable

if you uncomment and write password for user in inventory file use command:

ANSIBLE_HOST_KEY_CHECKING=false ansible-playbook -i inventory playbooks/lookup.yml

if you don't want to present password in plaintext for user you can use option '-k'. You will be asked for password

ANSIBLE_HOST_KEY_CHECKING=false ansible-playbook -i inventory playbooks/lookup.yml -k
