# Environment

The project was implemented inside an isolated virtual machine using VMware Workstation. The virtualized environment was used to simulate a small organization's Linux-based internal system and provide a safe environment for configuring and testing users, groups, permissions, ownership, and access control.

## Virtual Machine

| Component        | Configuration      |
| ---------------- | ------------------ |
| Hypervisor       | VMware Workstation |
| Operating System | Kali Linux 2026.2  |
| Architecture     | AMD64              |
| Memory           | 2 GB               |
| Processors       | 4                  |
| Storage          | 80.1 GB            |
| Network          | NAT                |
| Disk Controller  | SCSI               |

## Organizational Environment

The Linux system was designed to represent a community consisting of multiple teams with different responsibilities and access requirements.

The main roles in the environment are:

* **Management Team** — handles management-related resources.
* **Developers Team** — handles development-related resources.
* **Security Team** — responsible for security and administration, with broader access across the environment.

The main organizational directory is located at:

`/home/company/`

Within this directory, separate resources were created for the different teams along with shared resources.

## Linux Administration

The environment uses standard Linux administration and access-control mechanisms to manage the system, including:

* **Users and groups** — to represent organizational roles.
* **File and directory ownership** — to establish primary control over resources.
* **Linux permissions** — to control read, write, and execute access.
* **Access Control Lists (ACLs)** — to provide additional permissions to specific users when standard ownership and group permissions are insufficient.
* **Shared directories** — to provide controlled collaboration between users.

The environment was intentionally isolated inside a virtual machine so that the configuration and permission model could be safely implemented, modified, and tested without affecting the host operating system.
