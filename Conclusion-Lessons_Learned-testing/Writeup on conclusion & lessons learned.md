# Linux Administration Project

## 1. Summary

This project is a practical Linux administration lab created to demonstrate the use of Linux users, groups, permissions, ownership, Access Control Lists (ACLs), and directory management in a realistic environment.

Instead of only practicing individual Linux commands, I created a small company-like environment inside Kali Linux where different users represent different teams. Each team has its own resources and access requirements.

The main purpose of the project was to apply the Linux administration commands I learned to a realistic scenario and then test the configuration to verify that users could access the resources they were authorized to use while being restricted from resources they should not access.

---

## 2. Objective

The objective of this project is to demonstrate practical Linux administration skills by:

* Creating and managing users and groups.
* Creating a structured directory hierarchy.
* Assigning ownership to users and groups.
* Configuring Linux file and directory permissions.
* Using ACLs with `setfacl` to provide additional access when required.
* Creating a shared directory for common resources.
* Testing access restrictions using different users.
* Verifying that the configured permissions behave as intended.

The project focuses on applying Linux access-control concepts to a realistic environment rather than simply demonstrating individual commands.

---

## 3. Environment

The project was created inside a Kali Linux virtual machine running through VMware Workstation.

### Environment

* **Operating System:** Kali Linux
* **Virtualization:** VMware Workstation
* **Environment Type:** Local virtual machine
* **Main workspace:** `/home/company/`

The virtual machine provides an isolated environment where users, groups, permissions, ownership, and ACL configurations can be safely created and tested.

---

## 4. System Architecture

The Linux environment was designed to represent a small company with multiple teams.

The main workspace is:

```text
/home/company/
├── Management/
├── Developers/
├── Developers-kit/
├── Security/
└── shared_files/
```

Each directory represents a different type of company resource.

### Management

Contains resources intended for the management team.

### Developers

Contains resources intended for the development team.

### Developers-kit

Contains development-related tools and resources that require controlled access.

### Security

Contains resources intended for the security team.

### shared_files

Provides a common location for resources that need to be accessible by multiple users.

The Security user was configured as the owner of the main company directory structure, while ACLs were used to provide additional access to other users where required.

---

## 5. Users and Groups

Multiple users and groups were created to represent different roles within the company environment.

The users were organized into groups based on their responsibilities.

Using groups makes it possible to manage permissions according to roles instead of configuring every user individually.

The general structure was:

```text
Users
 │
 ├── Management
 ├── Developers
 └── Security
       │
       ▼
   Company Resources
```

This demonstrates how Linux groups can be used to organize and control access within an environment.

---

## 6. Directory Structure and Ownership

The `/home/company/` directory was created as the central workspace for the environment.

The directories inside it were then configured with different ownership and permission settings depending on their purpose.

Directory ownership and permissions were inspected using commands such as:

```bash
ls -la
```

and:

```bash
ls -ld /home/company/*
```

The Security user was given ownership of the main company resources, allowing the security role to manage the environment.

This also provided a practical example of how ownership affects access to Linux resources.

---

## 7. Linux Permissions

Linux permissions were used as the basic mechanism for controlling access to the company directories.

Linux permissions are divided into three categories:

```text
User     → Owner
Group    → Members of the group
Others   → Everyone else
```

The three main permissions are:

```text
r → Read
w → Write
x → Execute
```

For directories, the execute permission is particularly important because it allows a user to enter or traverse the directory.

Permissions were inspected using:

```bash
ls -l
```

For example:

```text
drwxr-x---
```

can be interpreted as:

```text
Owner  → rwx
Group  → r-x
Others → ---
```

This gives the owner full access, allows the group to read and enter the directory, and prevents other users from accessing it.

Permissions were configured using commands such as:

```bash
chmod
```

This allowed different directories to have different levels of access depending on their intended purpose.

---

## 8. ACL Configuration

Standard Linux permissions are sometimes not flexible enough when a specific user needs additional access without changing the main ownership structure.

To solve this, Access Control Lists (ACLs) were used.

The `setfacl` command was used to give specific users additional permissions.

For example:

```bash
setfacl -m u:dev01:rwx /home/company/Developers
```

The resulting ACL configuration can be inspected using:

```bash
getfacl /home/company/Developers
```

ACLs allowed the project to provide additional permissions to individual users while keeping the existing owner and group configuration.

This demonstrates a more flexible approach to Linux access control compared with relying only on the traditional owner/group/other permission model.

---

## 9. Shared Directory

A `shared_files` directory was created to represent resources that need to be accessible by multiple users.

Unlike the more restricted team directories, this directory was intentionally configured with highly permissive access.

The permissions were verified using:

```bash
ls -ld /home/company/shared_files
```

This provided a practical example of the difference between restricted resources and resources designed for general sharing.

The shared directory also demonstrated how permissions can be intentionally configured based on the purpose of a resource.

---

## 10. Testing Methodology

After configuring the users, groups, ownership, permissions, and ACLs, the environment was tested from the perspective of the different users.

The goal of the testing was not simply to confirm that the commands executed successfully, but to verify that the final access behavior matched the intended design.

Users were switched between and tested against different directories.

For example, a user who should have access to the Developers directory was tested by attempting to enter it:

```bash
cd /home/company/Developers
```

Users were also tested against directories they should not have access to.

If the permissions were correctly configured, Linux prevented the unauthorized operation and returned a permission error.

ACL-configured users were also tested to confirm that their additional permissions worked as intended.

---

## 11. Access Control Tests

Several different access scenarios were tested.

### Authorized Access

A user was tested against a directory they were supposed to access.

**Expected result:** Access is granted.

### Unauthorized Access

A user was tested against a restricted directory they were not supposed to access.

**Expected result:** Access is denied.

### ACL Access

A user with additional ACL permissions was tested against a directory where their standard permissions would not normally provide the required access.

**Expected result:** The additional ACL permissions allow the intended access.

### Shared Resource Access

Different users were tested against the `shared_files` directory.

**Expected result:** Users can access the shared resource according to its permissive configuration.

These tests were used to verify that the implemented permission model was working as intended.

---

## 12. Verification Commands

Several Linux commands were used during the configuration and testing process.

### Check the current user

```bash
whoami
```

### Display user and group information

```bash
id
```

### View directory permissions

```bash
ls -ld /home/company/*
```

### View ACL configuration

```bash
getfacl /home/company/Developers
```

### Modify ACL permissions

```bash
setfacl
```

### Change ownership

```bash
chown
```

### Change permissions

```bash
chmod
```

### Switch between users

```bash
su
```

These commands were used to configure the environment and verify that the resulting access controls behaved correctly.

---

## 13. Results

The final environment successfully demonstrated a basic Linux access-control system.

Different users were given different levels of access based on their roles. Standard Linux permissions were used to control the general access model, while ACLs were used to provide additional permissions to specific users when required.

Testing showed that authorized users could access the resources intended for them, while unauthorized users were prevented from accessing restricted directories.

The `shared_files` directory also demonstrated how a resource can be intentionally configured for broader access.

Overall, the tests confirmed that the configured ownership, permissions, groups, and ACLs worked together to enforce the intended access structure.

---

## 14. Lessons Learned

This project helped connect individual Linux commands with a realistic administration scenario.

Instead of learning commands independently, I was able to understand how they work together to create an access-control system.

The main concepts reinforced through the project were:

* Linux users and groups.
* File and directory ownership.
* Read, write, and execute permissions.
* Directory traversal permissions.
* `chmod` and `chown`.
* ACLs using `setfacl` and `getfacl`.
* Switching between users.
* Testing permissions from different user perspectives.
* Troubleshooting permission-related problems.
* Verifying configurations instead of assuming they work.

One of the main lessons from the project was that configuring permissions is only part of Linux administration. Testing the configuration from the perspective of different users is necessary to confirm that the intended security model is actually being enforced.

---

## 15. Conclusion

This project demonstrates my practical understanding of Linux administration by applying users, groups, ownership, permissions, ACLs, and directory management to a realistic company-style environment.

The purpose was to move beyond simply learning Linux commands and use them to solve an actual administration problem: controlling which users can access specific resources.

By creating the environment, configuring access, and testing both authorized and unauthorized actions, I was able to verify that the permission model behaved as intended.

Overall, the project provided practical experience with Linux access control and demonstrated how fundamental Linux administration concepts can be combined to create a structured and controlled environment.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Conclusion

This project was created to put the Linux administration concepts I learned into a practical and realistic environment. Instead of practicing commands individually, I used them to build a small company-style Linux environment with multiple users, groups, directories, ownership rules, permissions, ACLs, and shared resources.

The main goal was to control access to different resources based on the responsibilities of each user and group. The Security user was configured to manage the main company directory, while other users were given access according to their roles. ACLs were also used when standard Linux permissions were not enough to provide the required level of access.

After configuring the environment, I tested the permissions by switching between users and attempting to access different directories. Authorized users were able to access the resources assigned to them, while unauthorized users were denied access. These tests helped verify that the configured permissions and ACLs were working as intended.

Overall, the project allowed me to demonstrate that I can apply Linux administration concepts to a practical scenario rather than simply knowing the commands themselves.

# Lessons Learned

One of the most important things I learned from this project is that Linux permissions are not just commands such as `chmod` and `chown`. They are part of an access-control system where ownership, groups, permissions, and ACLs work together.

I also learned the importance of testing configurations after making changes. Instead of assuming that a permission or ACL was configured correctly, I verified the result by using different users and attempting both authorized and unauthorized actions.

The project also improved my understanding of the difference between standard Linux permissions and ACLs. Standard permissions provide the basic owner, group, and other access model, while ACLs allow more specific permissions to be assigned to individual users when needed.

Another important lesson was understanding how Linux directory permissions affect access. In particular, the execute permission on a directory is necessary for users to traverse and access its contents.

Most importantly, this project changed the way I approach Linux administration. Rather than learning commands separately, I learned to think about **why** a command is being used, **what security purpose it serves**, and **how to verify that the result is correct**.

# Future Improvements

Although the project demonstrates the core Linux administration concepts I have learned so far, it can be expanded in the future.

Possible improvements include:

* Adding Bash scripting to automate repetitive administration tasks.
* Implementing centralized logging and monitoring.
* Exploring SSH hardening and additional server security controls.
* Adding Linux auditing tools.
* Expanding the environment with additional services.
* Introducing more advanced access-control scenarios.

These improvements represent the next steps I can take as I continue developing my Linux administration and cybersecurity skills.

