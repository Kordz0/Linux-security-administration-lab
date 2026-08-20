# Testing Process

The environment was tested using the different user accounts created for each role within the company environment. The purpose of the testing process was to verify that the configured ownership, permissions, groups, and ACLs behaved as intended.

## 1. User and Group Verification

The first test verified that the created users were assigned to the correct groups and that their identities were configured correctly.

```bash
id managmentteam
id security
id dev01
id dev02
```

**Expected result:** Each user should belong to the appropriate group and have the expected user and group IDs.

*Screenshot: user and group verification*

---

## 2. Directory Permission Verification

The directory structure, ownership, and standard permissions were inspected using:

```bash
ls -la /home/kali/company
```

The individual directories were also checked to verify their ownership and permission settings.

**Expected result:** Each directory should have the expected owner, group, and permission configuration based on its intended role.

*Screenshot: directory ownership and permissions*

---

## 3. ACL Verification

ACL configurations were inspected using:

```bash
getfacl /home/kali/company/<directory>
```

**Expected result:** The configured users should appear in the ACL entries with the additional permissions assigned to them.

*Screenshot: ACL configuration*

---

## 4. Authorized Access Test

A user was switched into an account that should have access to its assigned team directory.

For example:

```bash
su - dev01
cd /home/kali/company/Developers
ls
```

**Expected result:** `dev01` should successfully access the Developers directory.

The same testing approach was used with `dev02` to verify its assigned access.

*Screenshot: successful authorized access*

---

## 5. Unauthorized Access Test

A user was switched into an account that should not have access to a restricted team directory.

For example:

```bash
su - dev01
cd /home/kali/company/Security
```

**Expected result:** Access should be denied if `dev01` does not have the required permissions.

Similar tests were performed against other restricted directories to verify that users could not access resources outside their assigned permissions.

*Screenshot: Permission denied*

---

## 6. Security User Access Test

The `security` user was tested to verify that it could access the resources assigned to the Security role.

```bash
su - security
cd /home/kali/company/Security
ls
```

The user was also tested against other resources where additional access had been granted through ownership or ACL configuration.

**Expected result:** The `security` user should be able to access the resources required for its administrative role.

*Screenshot: Security user access*

---

## 7. Management User Access Test

The `managmentteam` user was tested against the Management directory.

```bash
su - managmentteam
cd /home/kali/company/Managment
ls
```

**Expected result:** The `managmentteam` user should successfully access the Management resources while being restricted from directories intended for other teams.

*Screenshot: Management access*

---

## 8. Shared Resource Test

The `shared_files` directory was tested using the different user accounts to verify that the shared resource could be accessed according to its configured permissions.

For example:

```bash
su - dev01
cd /home/kali/company/shared_files
ls
```

The same test was performed using other users.

**Expected result:** Users should be able to access the shared resource according to its intended configuration.

*Screenshot: shared resource access*

---

## Testing Result

The tests were used to verify that the final permission model matched the intended architecture. Authorized users were able to access the resources assigned to their roles, while unauthorized access attempts were denied.

The testing process confirmed that ownership, groups, standard Linux permissions, and ACLs were being enforced correctly rather than simply being configured without verification.


The tests were used to verify that the final permission model matched the intended architecture. Both successful and denied access attempts were recorded to demonstrate that permissions were being enforced rather than simply configured.
