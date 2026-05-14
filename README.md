# OpenSMTPD Mailrelay Ansible Role (ansible-role-mailrelay-opensmtpd) from Blunix GmbH

This Ansible role installs and configures OpenSMTPD as a mail relay for servers, and optionally configures an SMTP‑to‑Matrix integration for monitoring.

It is designed for reliable, repeatable deployments in production environments.

The Ansible Role is written and actively maintained by <a href="https://www.blunix.com" target="_blank">Blunix GmbH</a>.
It is used in the Blunix <a href="https://www.blunix.com/linux-managed-hosting.html" target="_blank">Linux Managed Hosting</a> Stack.
Its usage is documented at our <a href="https://www.blunix.com/manual" target="_blank">Linux Managed Hosting Documentation</a>.


## Features

- Installs OpenSMTPD and required tooling.
- Manages `/etc/smtpd.conf` and table files under `/etc/smtpd/tables/`.
- Configures mailname via `/etc/mailname`.
- Installs and configures an SMTP‑to‑Matrix bridge using Python packages and a systemd service.
- Sends test mails and checks the OpenSMTPD queue.


## Requirements

- Ansible: **>= 2.20.0**
- Managed operating systems:
  - Debian **trixie**



## Role variables and example playbook

The full example is split under `example/`:

- <a href="https://github.com/Blunix-GmbH/ansible-role-mailrelay-opensmtpd/blob/main/example/inventory/group_vars/mailrelays.yml" target="_blank">`example/inventory/group_vars/mailrelays.yml`</a> — mailrelay settings, SMTP relays, Matrix bridge, and test recipient.
- <a href="https://github.com/Blunix-GmbH/ansible-role-mailrelay-opensmtpd/blob/main/example/play.yml" target="_blank">`example/play.yml`</a> — mailrelay play using the role.

### Required templates

The role itself ships templates under `roles/role-mailrelay-opensmtpd/templates/`.  
In most setups you will not override these, but you **must provide values** for all
referenced variables as shown above.

Templates used:

- `/etc/smtpd.conf` from `templates/etc/smtpd.conf.j2`
- `/etc/smtpd/tables/relay_secrets` from `templates/etc/smtpd/tables/relay_secrets.j2`
- `/etc/smtpd/tables/monitoring_from` from `templates/etc/smtpd/tables/monitoring_from.j2`
- `/etc/smtpd/tables/monitoring_recipients` from `templates/etc/smtpd/tables/monitoring_recipients.j2`
- `/etc/mailname` from `templates/etc/mailname.j2`
- `/usr/local/bin/smtp-to-matrix.py` from `templates/usr/local/bin/smtp-to-matrix.py`
- `/etc/smtp-to-matrix/config.yml` from `templates/etc/smtp-to-matrix/config.yml.j2`
- `/etc/systemd/system/smtp-to-matrix.service` from `templates/etc/systemd/system/smtp-to-matrix.service.j2`

You generally do not need to copy these templates; just ensure the variables they
use are defined in your `group_vars` / `host_vars` (especially the mailrelay_*
and monitoring_* variables shown in the example).


## Author Information

Blunix GmbH Berlin  

`root@Linux:~# Support | Consulting | Hosting | Training`

Blunix GmbH provides 24/7/365 Linux emergency support and consulting, Service Level Agreements for Debian Linux managed hosting using Ansible Configuration Management as well as Linux trainings and workshops.

Learn more at <a href="https://www.blunix.com" target="_blank">https://www.blunix.com</a>.

## Contact Information

Click here to see our <a href="https://www.blunix.com/#contact" target="_blank">Contact Information</a>.

For bug reports and feature requests, please open an issue in this repository’s GitHub issue tracker.


## License

Apache-2.0

Please refer to the `LICENSE` file in the root of this repository.

### Tests

The directory `test/` contains an example `play.yml` as well as `inventory/group_vars/`, if applicable to the role. the script `example/run-tests.sh` creates a IONOS cloud instance with terraform, uses the example inventory and playbook to run the role and then run pytest tests located in `example/tests/`. Destroy the terraform using `./run-tests.sh -d`.
