# Microsoft Entra ID Administration Lab Walkthrough

## Step 1: Access Microsoft Entra ID

1. Sign in to the Azure Portal.
2. Search for **Microsoft Entra ID**.
3. Open the default tenant.

## Step 2: Review Tenant Configuration

1. Open the **Overview** page.
2. Review the tenant name, primary domain, and licensing information.
3. Verify Security Defaults are enabled - default MFA deployed since October 2025.

### Why This Matters

Before making changes, administrators should understand the environment they're working in and verify that baseline security settings are in place.

## Step 3: Create User Accounts

Navigate to:

```text
Users → New User
```

Create the following users:

* Alex Admin
* Sarah Helpdesk
* John Employee

Use the automatically generated passwords.

## Step 4: Create Security Groups

Navigate to:

```text
Groups → New Group
```

Create the following Security Groups:

* Help Desk
* HR
* IT Admins

### Why This Matters

Security Groups are how we assign permissions at scale.

Instead of giving permissions directly to individual users, permissions are assigned to groups, and users are placed into those groups.

## Step 5: Assign Group Memberships

Add users to the following groups:

 Sarah Helpdesk -> Help Desk 
 Alex Admin     -> IT Admins 
 John Employee  -> HR        

If an employee leaves and a new one joins, administrators only need to update group memberships instead of rebuilding permissions.

## Step 6: Assign an Administrative Role

Navigate to:

```text
Roles and administrators
```

Assign the following role:

 Sarah Helpdesk -> Helpdesk Administrator 

### Why This Matters

Groups and Roles are not the same thing.

```text
Group = What resources can I access?

Role = What administrative actions can I perform?
```

Administrative roles determine what management tasks a user can perform inside Entra ID.

## Step 7: Review Authentication Methods

Navigate to:

```text
Users → Sarah Helpdesk → Authentication Methods
```

Review available authentication methods:

* Email
* Phone Number
* QR Code
* Temporary Access Pass

### Why This Matters

Authentication methods support Multi-Factor Authentication (MFA) and account recovery.

## Step 8: Simulate User Offboarding

Navigate to:

```text
Users → John Employee
```

Edit account settings and change:

```text
Account Enabled = No
```

### Why This Matters

Disabling access prevents sign-ins while preserving user records, logs, and audit history.

## Step 9: Remove Group Memberships

Navigate to:

```text
Users → John Employee → Groups
```

Remove the user from the HR group.

### Why This Matters

Removing group memberships removes permissions.

```text
Disable Account
= Can't Log In

Remove Groups
= Loses Access
```

Both actions are commonly included in an employee offboarding process.

## Conclusion

This lab demonstrated the complete user lifecycle within Microsoft Entra ID:

* User Creation
* Group Management
* Access Assignment
* Role Assignment
* Authentication Review
* Account Offboarding

These are common tasks performed by Help Desk Technicians, Identity Administrators, and System Administrators in Microsoft cloud environments.
