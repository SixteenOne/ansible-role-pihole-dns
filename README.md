# Ansible Role: sixteenone.pihole-dns

This role manages DNS and CNAME records for PiHole.

## Requirements

- A running PiHole instance
- Ansible 2.9 or higher

## Tasks
This role performs the following tasks:

1. Creates DNS records in `/etc/pihole/custom.list`
2. Creates CNAME records in `/etc/dnsmasq.d/05-pihole-custom-cname.conf`
3. Restarts the FTL service when changes are made

## Role Variables

Define your DNS and CNAME records in the following variables:

```yaml
pihole_dns_records:
  - { domain: "example.com", ip: "192.168.1.100" }

pihole_cname_records:
  - { alias: "www.example.com", domain: "example.com" }
```

## Example Playbook

> Note: These files are created everytime, any original data that currently exists on your PiHole server will be lost, the Variables are the "source of truth"

It is easier to maintain if you put all of the DNS & CNAME's into an external file, in the format specified in the Role Variable section above. Then reference the file in your Playbook against the Role.

```
- name: Add DNS & CNAMES to PiHole Servers
  hosts: pihole_servers
  become: true
  gather_facts: false
  vars_files:
    - dns.yml
  roles:
    - sixteenone.pihole-dns
```

## License

MIT

## Author Information

This Role was created by [SixteenOne](https://twitter.com/sixteenone)