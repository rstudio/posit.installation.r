# Ansible Role: R Installation (posit.installation.r)

This Ansible role installs R on Ubuntu, RHEL, and SUSE Linux Enterprise Server (SLES) systems using the official Posit repositories.

## Requirements

- Ansible 2.9 or higher
- Supported operating systems:
  - Ubuntu 22.04 (Jammy)
  - Ubuntu 24.04 (Noble)
  - RHEL 8
  - RHEL 9
  - SLES 15 SP6

## Role Variables

### Required Variables

- `r_version`: The primary R version to install (e.g., "4.3.3"). This version will be added to the system PATH.
- `r_version_alt`: An alternative R version to install alongside the primary version (optional).

### Default Variables

```yaml
r_version: "4.3.3"
r_version_alt: ""
```

## Dependencies

None.

## Example Playbook

### Install a single R version:

```yaml
---
- hosts: servers
  become: yes
  roles:
    - role: r-install
      vars:
        r_version: "4.3.3"
```

### Install multiple R versions:

```yaml
---
- hosts: servers
  become: yes
  roles:
    - role: r-install
      vars:
        r_version: "4.3.3"
        r_version_alt: "4.2.3"
```

## What This Role Does

1. **Detects the operating system** and applies the appropriate installation method
2. **Configures repositories** based on the specific OS version:
   - RHEL 8: https://cdn.rstudio.com/r/centos-8/pkgs
   - RHEL 9: https://cdn.rstudio.com/r/rhel-9/pkgs
   - Ubuntu 22.04: https://cdn.rstudio.com/r/ubuntu-2204/pkgs
   - Ubuntu 24.04: https://cdn.rstudio.com/r/ubuntu-2404/pkgs
   - SLES 15 SP6: https://cdn.posit.co/r/opensuse-156/pkgs
3. **Installs dependencies** required for R
4. **Downloads and installs** the specified R version(s)
5. **Creates symlinks** for the primary R version to make it available on the system PATH
6. **Upgrades R tools** for all installed R versions

## Directory Structure

```
r-install/
├── defaults/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   ├── main.yml
│   ├── ubuntu.yml
│   ├── rhel.yml
│   └── suse.yml
└── README.md
```

## License

BSD

## Author Information

This role was created in 2025 for automated R installation across multiple Linux distributions.