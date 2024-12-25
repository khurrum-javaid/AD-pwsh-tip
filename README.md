# Active Directory Management Roadmap Project

## Overview  
This project is the result of countless cups of coffee and a relentless determination to make Active Directory (AD) management not just functional, but dare we say... delightful. Using the magic of **PowerShell**, we’ve created a roadmap that transforms tedious admin tasks into efficient, automated workflows. Welcome to the world of lazy brilliance.

---

## Features  

### **1. User Management** 
   - Automate user creation, deletion, and updates. (Because manually adding users is so 2005.)
   - Bulk user import from CSV — because who has time to type?

### **2. Group Management**
   - Create and manage security and distribution groups like a pro.
   - Assign users to groups programmatically. It’s like matchmaking, but for IT.

### **3. Organizational Unit (OU) Management**
   - Dynamically create and manage OUs to keep your AD tidy.
   - Set permissions and policies so you’re the boss, literally.

### **4. Audit and Reporting**
   - Generate detailed reports to look like you’ve been working all day.
   - Audit password expiration and login activity. No more surprises.

### **5. Policy Automation**
   - Automate Group Policy Object (GPO) creation and linking. Yes, it’s as cool as it sounds.
   - Backup and restore GPO configurations like a time-traveling admin.

---

## Tech Stack
- **PowerShell**: The wand to your wizardry.
- **Active Directory Module for Windows PowerShell**: Because AD deserves the royal treatment.
- **CSV**: The unsung hero of data wrangling.
- **Notepad++/VS Code**: Choose your weapon for script domination.

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
*Translation*: Create users faster than you can say "Active Directory."

### 2. Adding Users to Groups
```powershell
# Add users to a group
$GroupName = "HR_Team"
Import-Csv -Path "group_users.csv" | ForEach-Object {
    Add-ADGroupMember -Identity $GroupName -Members $_.SamAccountName
}
```
*Translation*: Group hug for your users, digitally speaking.

### 3. Reporting on Expired Passwords
```powershell
# Find users with expired passwords
Search-ADAccount -UsersOnly -PasswordExpired | Select-Object Name, SamAccountName, LastLogonDate
```
*Translation*: Keep expired passwords on a tight leash.

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
*Tip*: Save money and impress finance by turning off those idle VMs.

---

## How to Use  
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/active-directory-roadmap.git
   ```
2. Review the `README.md` in each feature directory for script details.
3. Run the scripts in a PowerShell environment with administrative privileges. (And yes, you’ll feel powerful.)

---

## Future Enhancements  
- Integration with CI/CD pipelines for automated AD deployments. (Let’s automate the automation.)
- Advanced security audits using PowerShell and third-party tools. (Because paranoia pays.)
- Comprehensive dashboards for AD insights using PowerShell scripts and Power BI. (Make your reports look fancier than they need to be.)

---

## Acknowledgements  
Shoutout to the PowerShell community for being the Yoda to our Jedi journey. 💡

Feel free to explore, contribute, or tell us how we’re doing it all wrong! 😊
