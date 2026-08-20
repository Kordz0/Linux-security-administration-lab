# System Architecture

The Linux environment is structured to represent a small organization with multiple teams, where each team has its own responsibilities and access requirements.

The architecture is centered around the `/home/company/` directory. This directory contains the resources used by the different teams and acts as the main workspace for the environment.

## Directory Structure

```text
/home/company/
├── Management/
├── Developers/
├── Developers-kit/
├── Security/
└── shared_files/
```

Each directory serves a different purpose and is controlled through Linux ownership, groups, standard permissions, and ACLs.

## Team Access Model

### Management

The `Management/` directory contains resources intended for the management team.

Access is controlled so that management users can work with their assigned resources without automatically receiving access to restricted team directories.

### Developers

The `Developers/` directory contains development-related resources.

Developers are able to read and modify resources within their assigned development areas. The `Developers-kit/` directory provides additional resources intended to be shared between developers.

### Security

The `Security/` directory represents the administrative and security side of the environment.

The Security team has broader access across the `/home/company/` hierarchy, allowing it to manage and monitor resources belonging to the different teams. This represents a realistic administrative role where the security team requires greater visibility and control than regular users.

### Shared Resources

The `shared_files/` directory contains resources that need to be accessible by multiple users.

Unlike the team-specific directories, this resource is designed for collaboration rather than restricting access to a single team.

## Permission Model

The architecture combines several Linux access-control mechanisms:

* **User ownership** determines the primary owner of a resource.
* **Group ownership** allows permissions to be assigned to an entire team.
* **Standard Linux permissions** control read, write, and execute access for the owner, group, and other users.
* **ACLs** provide additional permissions for specific users or groups without changing the primary ownership structure.

This combination allows the environment to provide both restricted team-specific resources and controlled cross-team access.

## Security Principle

The architecture follows the principle of giving users access according to their responsibilities.

Regular users should only have the permissions required for their role, while the Security team has broader administrative access. Access is therefore intentionally different between users rather than giving every account unrestricted access to the entire system.

## Testing and Validation

The final configuration is validated through practical permission testing. Users are switched between accounts and access attempts are performed against different directories and resources.

Tests include:

* Accessing directories that the user should be allowed to access.
* Attempting to access restricted directories.
* Creating and modifying files where write permissions are expected.
* Verifying access to shared resources.
* Testing additional permissions granted through ACLs.
* Confirming that unauthorized users are denied access.

This testing demonstrates that the configured ownership, groups, permissions, and ACLs work as intended.
