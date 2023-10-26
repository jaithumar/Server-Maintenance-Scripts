# Best Work Examples

## 1. Automating Server Maintenance
- **Client's Needs:** A client needed an efficient way to automate routine server maintenance tasks, including log cleanup and database backups.
- **Solution:** Developed a PowerShell script that automated these tasks, improving server performance and reducing the risk of data loss. The script was scheduled to run at optimal times, saving the client valuable hours.
- **PowerShell Script to Clean Logs and Perform Database Backups:**
  ```powershell
   # Log cleanup
   Get-ChildItem -Path "C:\Logs\" -Recurse | Where-Object { $_.LastWriteTime -lt (Get-Date).AddDays(-30) } | Remove-Item -Force

   # Database backup
   $backupPath = "D:\Backups\"
   $databaseName = "MyDatabase"
   Backup-SqlDatabase -ServerInstance "SQLServerInstance" -Database $databaseName -BackupFile "$backupPath\$databaseName.bak"
   ```

## 2. Active Directory User Management
- **Client's Needs:** A company required an easier way to manage their Active Directory users, from onboarding to offboarding.
- **Solution:** Created a suite of PowerShell scripts that streamlined user provisioning and deprovisioning, reducing the workload on IT staff and ensuring consistent user management practices.
- **PowerShell Script for User Onboarding:**
   
   ```powershell
   New-ADUser -Name "John Doe" -SamAccountName "johndoe" -UserPrincipalName "johndoe@company.com" -Enabled $true -Path "OU=Users,DC=company,DC=com" -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force)
   ```

## 3. SharePoint Integration Tool
- **Client's Needs:** An organization needed to integrate data from SharePoint into their internal systems for reporting and analysis.
- **Solution:** Crafted a custom PowerShell module that allowed the client to extract, transform, and load data from SharePoint into their databases seamlessly. This improved data accuracy and reporting efficiency.
- **PowerShell Script to Extract Data from SharePoint:**

   ```powershell
   $spWebURL = "https://sharepoint.site.com"
   $listName = "Documents"
   $query = New-Object Microsoft.SharePoint.Client.CamlQuery
   $query.ViewXml = "<View><Query><Where><Geq><FieldRef Name='ID'/><Value Type='Number'>1</Value></Geq></Where></Query></View>"

   $spContext = New-Object Microsoft.SharePoint.Client.ClientContext($spWebURL)
   $spList = $spContext.Web.Lists.GetByTitle($listName)
   $spItems = $spList.GetItems($query)

   $spContext.Load($spItems)
   $spContext.ExecuteQuery()

   foreach ($item in $spItems) {
       # Process SharePoint data and load into internal systems
   }
   ```

## 4. Azure Automation for Cost Control
- **Client's Needs:** A startup was looking for ways to control costs in their Azure cloud environment.
- **Solution:** Developed a set of PowerShell scripts and Azure Automation runbooks to automate scaling and resource management, ensuring they only paid for what they used and saving them money in the long run.
- **Azure Automation Runbook to Scale Resources:**

   ```powershell
   $resourceGroup = "MyResourceGroup"
   $vmName = "MyVM"
   $location = "East US"
   $desiredCount = 2

   $vmss = Get-AzVmss -ResourceGroupName $resourceGroup -VMScaleSetName $vmName
   $vmss.Sku.Capacity = $desiredCount

   Update-AzVmss -ResourceGroupName $resourceGroup -Name $vmName -VirtualMachineScaleSet $vmss
   ```

## 5. AD Security Auditing
- **Client's Needs:** A security-conscious organization required robust Active Directory security auditing to detect and mitigate potential threats.
- **Solution:** Designed a PowerShell script that regularly scanned the Active Directory for suspicious activities and reported on security events. This improved the client's security posture and helped them stay compliant with industry regulations.
- **PowerShell Script for Active Directory Security Auditing:**

   ```powershell
   # Enable Audit Policy
   Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system" -Name "Audit" -Value 3

   # Monitor Security Events
   $securityEvents = Get-WinEvent -LogName Security -MaxEvents 50 | Where-Object { $_.Id -eq 4740 }
   
   # Send Alert or Log Events
   foreach ($event in $securityEvents) {
       # Send alert or log event for further analysis
   }
   ```
