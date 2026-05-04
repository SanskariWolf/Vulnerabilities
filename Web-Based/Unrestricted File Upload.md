# Description
Unrestricted File Upload is a vulnerability that occurs when a web application allows users to upload files without properly validating their type, content, size, or destination. This can enable attackers to upload malicious files (e.g., web shells, scripts) and execute them on the server.

This issue often arises due to:
- Lack of file type validation    
- Trusting client-side checks
- Improper MIME type validation
- Storing uploads in executable directories
As a result, attackers may gain unauthorized access or execute arbitrary commands on the server.
# Steps
### 1. Identify Upload Functionality
Locate file upload features such as:
- Profile picture upload
- Document submission
- Media upload forms
### 2. Intercept Request (Optional)
Use a proxy tool like Burp Suite to capture the upload request.
### 3. Prepare Malicious File
Create a file with executable content:
Example (PHP web shell):
```php
<?php system($_GET['cmd']); ?>
```
Save as:
```
shell.php
```
### 4. Attempt File Upload
Upload the malicious file through the application.
If blocked, try bypass techniques:
- Change extension (`shell.php.jpg`)
- Modify MIME type (`image/jpeg`)
- Use case variations (`shell.pHp`)
### 5. Locate Uploaded File
Find the file path:
```
http://example.com/uploads/shell.php
```
### 6. Execute Payload
Access the uploaded file:
```
http://example.com/uploads/shell.php?cmd=id
```
If command output is shown → vulnerability confirmed
# Impact
Unrestricted File Upload can lead to:
- Remote Code Execution (RCE)
- Full server compromise
- Upload of web shells or backdoors
- Data theft or modification
- Malware distribution
- Privilege escalation
# Remediation
1. Use a **whitelist of allowed file types**
2. Validate file **content**, not just extension
3. Rename uploaded files to random names
4. Store files outside the web root
5. Disable execution in upload directories
6. Enforce strict file size limits
7. Validate MIME types server-side
8. Use secure frameworks for file handling
# Severity

**Critical**
- Direct path to Remote Code Execution
- Often requires no authentication
- Leads to full system compromise
# CVSS (v3.1)
```id="uf2"
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)
