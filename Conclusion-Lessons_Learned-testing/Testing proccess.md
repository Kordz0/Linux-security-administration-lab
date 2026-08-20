# Testing Process

The environment was tested using the different user accounts created for each team. The purpose of the testing process was to verify that the configured ownership, permissions, groups, and ACLs behaved as intended.

## 1. User and Group Verification

The first test verified that users were assigned to the correct groups and roles.

```bash
id dev01
id manager01
id security01
```

**Expected result:** Each user should belong to the appropriate team or security group.

*Screenshot: user/group verification*

---

## 2. Directory Permission Verification

The directory structure, ownership, and standard permissions were inspected using:

```bash
ls -la /home/company
```

**Expected result:** Each directory should have the expected owner, group, and permission configuration.

*Screenshot: directory ownership and permissions*

---

## 3. ACL Verification

ACL configuration was inspected using:

```bash
getfacl /home/company/<directory>
```

**Expected result:** The configured users or groups should appear in the ACL entries with their intended permissions.

*Screenshot: ACL configuration*

---

## 4. Authorized Access Test

A user was switched into an account that should have access to its assigned team directory.

```bash
su - dev01
cd /home/company/Developers
ls
```

**Expected result:** The user should successfully access the directory.

*Screenshot: successful authorized access*

---

## 5. Unauthorized Access Test

A user without the required permissions was used to attempt access to a restricted directory.

```bash
su - manager01
cd /home/company/Developers
```

**Expected result:** Access should be denied.

*Screenshot: Permission denied*

---

## 6. Security Team Access Test

The Security user was used to verify its broader access across the environment.

**Expected result:** The Security user should be able to access the resources required by its administrative role.

*Screenshot: Security team access*

---

## 7. Shared Resource Test

The shared directory was tested using multiple users to verify that the resource could be accessed according to its intended configuration.

**Expected result:** Authorized users should be able to access and work with the shared resource.

*Screenshot: shared resource access*

## Testing Result

The tests were used to verify that the final permission model matched the intended architecture. Both successful and denied access attempts were recorded to demonstrate that permissions were being enforced rather than simply configured.
