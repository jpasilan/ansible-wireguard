# Ansible Wireguard

This contains Ansible playbooks to install a WireGuard VPN server and generate the client configuration. The playbook that installs the VPN server performs the following:

* Install the WireGuard packages and Linux headers when necessary.
* Install UFW to manage firewall rules and allow traffic only on SSH and WireGuard ports. UFW logging is turned off.
* Generate the required WireGuard crypto keys.
* Generate the WireGuard server configuration. This includes iptable rules for IPv4/IPv6 forwarding and NAT masquerade.
* Add WireGuard as a systemd service.
* Update sysctl to enable IPv4/IPv6 forwarding.

The client playbook to generates a configuration that is already complete with the necessary crypto keys and addresses.

# Works In

This was tested in the following 64-bit distros:

* Debian 10, 9
* Ubuntu 20,18, 16

# Setup

Prior to running the playbooks, create the inventory named `hosts.yml` and the vars file, `vars.yml`. Sample files are provided for reference.
Also, create the `clients` directory in the parent directory. This is where the client configuration files will be downloaded.

# Usage

Run first the playbook for the WireGuard server, like so:

`ansible-playbook wg-server-playbook.yml`

Then, generate the client configuration file with:

`ansible-playbook wg-client-playbook.yml`
