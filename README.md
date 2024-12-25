# Active Directory Management Roadmap Project

## Overview  
This project provides a step-by-step roadmap for managing Active Directory (AD) environments using **PowerShell**. It includes sample scripts and best practices to automate common AD tasks, making administration efficient and scalable.

---

## Features  

### **1. User Management** 
   - Automate user creation, deletion, and updates.
   - Bulk user import from CSV.

### **2. Group Management**
   - Create and manage security and distribution groups.
   - Assign users to groups programmatically.

### **3. Organizational Unit (OU) Management**
   - Create and manage OUs dynamically.
   - Set permissions and policies at the OU level.

### **4. Audit and Reporting**
   - Generate detailed reports for user activities, group memberships, and policy applications.
   - Audit password expiration and login activity.

### **5. Policy Automation**
   - Automate Group Policy Object (GPO) creation and linking.
   - Backup and restore GPO configurations.

---

## Tech Stack
- **PowerShell**: Core scripting language.
- **Active Directory Module for Windows PowerShell**: For managing AD environments.
- **CSV**: For data import/export.
- **Notepad++/VS Code**: Recommended editors for script development.

---

## Sample Script Examples

### 1. Bulk User Creation
```powershell
# Import users from CSV and create accounts
Import-Csv -Path "users.csv" | ForEach-Object {
    New-ADUser -Name $_.Name -GivenName $_.GivenName -Surname $_.Surname \
               -UserPrincipalName $_.UserPrincipalName -SamAccountName $_.SamAccountName \
               -Path "OU=Users,DC=example,DC=com" -AccountPassword (ConvertTo-SecureString $_.Password -AsPlainText -Force) \
               -Enabled $true
}
```

### 2. Adding Users to Groups
```powershell
# Add users to a group
$GroupName = "HR_Team"
Import-Csv -Path "group_users.csv" | ForEach-Object {
    Add-ADGroupMember -Identity $GroupName -Members $_.SamAccountName
}
```

### 3. Reporting on Expired Passwords
```powershell
# Find users with expired passwords
Search-ADAccount -UsersOnly -PasswordExpired | Select-Object Name, SamAccountName, LastLogonDate
```

### 4. Azure Daily Admin Tip
```powershell
# List all running VMs in an Azure subscription
Get-AzVM | Where-Object { $_.PowerState -eq "VM running" } | Select-Object Name, ResourceGroupName

# Output example:
# Name            ResourceGroupName
# ----            -----------------
# WebServer01     ResourceGroupA
# SQLDatabaseVM   ResourceGroupB
```
*Tip*: Use this to ensure no unnecessary costs are incurred by idle VMs.

---

## How to Use  
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/active-directory-roadmap.git
   ```
2. Review the `README.md` in each feature directory for script details.
3. Run the scripts in a PowerShell environment with administrative privileges.

---

## Future Enhancements  
- Integration with CI/CD pipelines for automated AD deployments.
- Advanced security audits using PowerShell and third-party tools.
- Comprehensive dashboards for AD insights using PowerShell scripts and Power BI.

---

## Acknowledgements  
Special thanks to the PowerShell community for their excellent documentation and script examples. 💡

Feel free to explore, contribute, or provide suggestions for improvement! 😊
