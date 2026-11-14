# GTS Custom RPM Deployment & Simulation Framework

This repository provides a fully automated local simulation environment for deploying custom RPM packages to a RHEL/Rocky Linux client container using **Ansible** and a mock **Nginx-based repository mirror**.

---

## Architecture Overview

* **Orchestration**: Ansible (manages configuration, repository setup, and package installation via `delegate_to`).
* **Target Environment**: Podman container simulating a RHEL-based client (`sim-target-client`).
* **Repository Mirror**: Local directory (`./satellite-mirror/repos/release/`) served via Nginx, containing custom `.rpm` files and pre-indexed repository metadata (`repomd.xml`, `primary.xml.gz`).

---

## Project Directory Structure

```text
satellite-ansible-sim/
├── ansible.cfg
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
├── group_vars/
│   └── all/
│       ├── main.yml
│       └── vault.yml
├── rpm/
│   ├── SOURCES/
│   │   └── trs-node-audit
│   └── SPECS/
│       └── trs-ops-toolkit.spec
├── roles/
│   └── trs_package_installer/
│       ├── defaults/
│       │   └── main.yml
│       ├── tasks/
│       │   └── main.yml
│       └── templates/
│           └── nexus.repo.j2
└── satellite-mirror/
    ├── api/
    ├── keys/
    ├── nginx.conf
    └── repos/
=======
