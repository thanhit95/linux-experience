# SYSTEMCTL

## WHAT IS SYSTEMCTL?

> The systemctl command is a utility which is responsible for examining and controlling the systemd system and service manager. It is a collection of system management libraries, utilities and daemons which function as a successor to the System V init daemon. The new systemctl commands have proven quite useful in managing a servers services. It provides detailed information about specific systemd services, and others that have server-wide utilization.

&nbsp;

## COMMANDS

### List all services

`systemctl list-units --type=service`

Notes:

- Parameter `list-units` can be omitted. That means the shorten command is:
  - `systemctl --type=service`
- To list all services with its unit files:
  - `systemctl list-unit-files --type=service`

### List all running services

`systemctl --type=service --state=running`

### Manage a service

```text
systemctl start httpd.service
systemctl restart httpd.service
systemctl stop httpd.service
systemctl reload httpd.service
systemctl status httpd.service
systemctl is-active httpd.service
systemctl enable httpd.service
systemctl disable httpd.service
systemctl mask httpd.service
systemctl unmask httpd.service
systemctl kill httpd.service
```

Where `httpd.service` is an example of service name.

### Check which services take most time

`systemd-analyze blame`

or

`systemd-analyze critical-chain`

&nbsp;

## COMPARISON: `systemctl disable` VS. `systemctl mask`

When a service X is disabled, it will not load at the next system boot. However, the service X can be loaded when another service Y, which depends on X, is started.

When a service X is masked, it is impossible to load X, even if it is required by another service.

In detail:

- There a several symlinks (in `/etc/systemd/system`) pointing to service unit files (in `/lib/systemd/system`). These symlinks will be called in the system boot.
- Disabling a service causes the symlinks to be deleted.
- Masking a service causes the service unit file points to `/dev/null`.

&nbsp;

## REFERENCES

- <https://www.liquidweb.com/kb/what-is-systemctl-an-in-depth-overview>
