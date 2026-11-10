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
.
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
├── roles
│   └── gts_package_installer
│       ├── defaults
│       │   └── main.yml
│       └── tasks
│           └── main.yml
└── satellite-mirror
    ├── api
    │   └── v2
    │       └── organizations
    ├── keys
    │   └── RPM-GPG-KEY-gts-automation
    ├── nginx.conf
    └── repos
        └── release
            ├── repodata
            │   ├── primary.xml
            │   ├── primary.xml.gz
            │   └── repomd.xml
            └── test-pkg-1.0-1.el9.x86_64.rpm
=======
