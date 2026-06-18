# Group Policy Management Lab - Walkthrough

## Step 1 – Create a Test Organizational Unit

1. Open Active Directory Users and Computers.
2. **Right-click** the domain.
3. Select **New** → **Organizational Unit**.
4. Name the OU: `GPO-Test`
5. Click OK.

## Step 2 – Move a Test User into the OU

1. Locate an existing test user. (`Test User` was created in the `Sales` OU in the original AD lab)
2. **Right-click** the user and select **Move**.
3. **Select**: `GPO-Test`
4. Click OK.

## Step 3 – Create and Link a Group Policy Object

1. Open Group Policy Management.
2. Expand/Navivate to the domain:

```
Forest
 └─ Domains
     └─ adlab.local
```

3. **Right-click** the GPO-Test OU.
4. Select: **Create a GPO in this domain, and Link it here...**
5. Name the policy: `GPO-Test-User-Restrictions`
6. Click OK.

## Step 4 – Configure the Policy

1. Right-click the new GPO.
2. Select **Edit**.
3. Navigate to:

```
User Configuration
 └─ Policies
     └─ Administrative Templates
         └─ Control Panel
```

4. Open: **Prohibit access to Control Panel and PC setting**
5. Select **Enabled**.
6. Click Apply and OK.

## Step 5 – Force a Group Policy Update

On the client workstation, open Command Prompt and run the command: `gpupdate /force`

Verify that both Computer Policy and User Policy update successfully.

## Step 6 – Test Policy Enforcement

While logged in as the test user:

1. Attempt to open Control Panel: `Windows + I`
2. Attempt to open Windows Settings.

Expected result:

```
This operation has been cancelled due to restrictions in effect on this computer.
Please contact your system administrator.
```

## Step 7 – Verify Policy Application

Open Command Prompt and run the command: `gpresult /r`

Verify the following policy appears under Applied Group Policy Objects:

```
GPO-Test-User-Restrictions
```

## Outcome

The Group Policy Object was successfully deployed, applied to the target user, and enforced on the client workstation. Policy application was confirmed using the commands `gpupdate` and `gpresult`.
