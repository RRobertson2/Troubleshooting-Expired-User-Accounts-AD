# Troubleshooting-Expired-User-Accounts-AD

### Objective
Troubleshoot and resolve a user login issue in Active Directory caused by an expired account attribute. This project demonstrates account-level diagnostics and administrative remediation using Active Directory Users and Computers (ADUC) on Windows Server.

### Skills Learned
- Troubleshooting user authentication failures in a domain environment
- Navigating and using Advanced Features in Active Directory Users and Computers
- Identifying and modifying user account expiration attributes
- Applying organizational policies to individual accounts without affecting domain-wide settings
- Validating successful remediation through user verification<br>
  <br>
### Tools Used
- Windows Server 2022
- Active Directory Users and Computers (ADUC)
- Attribute Editor (via Advanced Features in ADUC)
- Server Manager<br>

<hr style="border: 0.15px solid rgba(0, 0, 0, 0.05);">
  
### Step 1: User Report: Password Expired

A user reports they are unable to log in. The system returns a message: "Your password has expired." This is a common issue caused by Active Directory account settings where the password expiration policy is enforced.<br>
<br>
- User is locked out due to an expired password.
- Password expiration policy is active on the domain.
- Begin by verifying the user's AD account status.<br>
<br>
<img src="https://github.com/user-attachments/assets/5c8d285d-da6e-4070-b688-6278e5b0c267" width="1000"><br>
<br>

<hr style="border: 0.15px solid rgba(0, 0, 0, 0.05);">

### Step 2: Launch Active Directory Users and Computers

Open Server Manager → go to Tools → select Active Directory Users and Computers. Once launched, go to the top menu and select View → Advanced Features.<br>
<br>
- Accesses full administrative controls and advanced tabs.
- Enables visibility into additional tabs like "Attribute Editor" which are essential for diagnosing account issues.
- Allows discovery of the user’s full OU path and hidden attributes.<br>
<br>
<img src="https://github.com/user-attachments/assets/9ca3f486-72f6-4d6c-ac79-b6c3710bf6fc" width="1000"><br>
<br>
<img src="https://github.com/user-attachments/assets/ef4f3f58-73ca-4db0-9071-8bf2f108be73" width="1000"><br>

<hr style="border: 0.15px solid rgba(0, 0, 0, 0.05);">

### Step 3: Locate User in OU and Review Attribute Editor
Now that you have the full path to the user account, navigate back to Active Directory Users and Computers and expand the correct Organizational Unit. In this case, go to the Engineering OU and locate Peter Parker.
Double-click on the user account to open Properties, then go to the Attribute Editor tab. Within the Attribute Editor, scroll to find the account Expires attribute.<br>
<br>
It shows the account expired on 8/1/2025, which is 3 days ago—confirming this is the cause of the login failure.<br>
Note: The Attribute Editor tab is only accessible when viewing a user object directly from the Active Directory Users and Computers console. It will not appear if accessed through the "Find Users, Contacts, and Groups" search tool.
<br>
- Located the user account directly in the correct OU and reviewed expiration details.
- The Attribute Editor provides granular user account settings required to verify expiration.
- Accessing the user through the correct OU view ensures all advanced tabs, including Attribute Editor, are visible.<br>
<br>
<img src="https://github.com/user-attachments/assets/eafcb768-3dee-456c-9347-12196c225a6b" width="1000"><br>
<br>

<hr style="border: 0.15px solid rgba(0, 0, 0, 0.05);">

### Step 4: Update Expired Account to Never Expire
In the Account tab of the user's properties, update the account settings:<br>
<br>
- Uncheck "Account expires"
- Select "Never"
<br>
Peter Parker is now a full-time employee, and his account should not expire.
- Changed account expiration policy to “Never”.
- Ensures the user maintains uninterrupted access as a full-time employee.
- Prevents future expiration without disabling password expiration policy across the domain.<br>
<br>
<img src="https://github.com/user-attachments/assets/6ce505e9-ef62-40c7-8c15-69a7308fd129" width="1000"><br>
<br>
<hr style="border: 0.15px solid rgba(0, 0, 0, 0.05);">

### Step 5: Verify User Access
Have the user log in again. The account now works as expected. No more password expiration errors.<br>
<br>
- User regains access.
- Proper administrative troubleshooting resolved the issue.
- The fix was targeted, using directory attribute adjustments, not a global policy change.<br>
<br>
<img src="https://github.com/user-attachments/assets/e1dd18f9-69d9-4a71-bf69-1b1ed9a61583" width="1000"><br>
<br>
