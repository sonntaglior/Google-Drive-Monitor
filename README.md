# Google-Drive-Monitor

This script provides automated monitoring of file uploads to your Google Drive account in near real-time, offering immediate insights into the sharing status of each file. It is specifically designed to enhance privacy by modifying the permissions of files uploaded to publicly accessible folders, setting them to private to ensure data confidentiality.

## Requirements:
* Python version 3.10.7 or higher.
* The pip package management tool.
* An active Google Cloud project.
* A Google account with Google Drive enabled.

### Google Drive API and OAuth Configuration:
Before running the script, enable the Google Drive API for your Google Cloud project and set up OAuth credentials for a desktop application. Store the generated credentials locally as **_credentials.json_**. Detailed setup instructions can be found here:
https://developers.google.com/drive/api/quickstart/python#set_up_your_environment

Ensure that the OAuth consent screen scope is configured as:
**https://www.googleapis.com/auth/drive**
![image](https://github.com/sonntaglior/Google-Drive-Monitor/assets/40151842/90e20221-ee06-46a4-a113-6c282ae35bc2)


Note that while the OAuth consent screen status is set to "Testing", only designated test users will have app access. Please add your Google account to the "Test Users" list.

![image](https://github.com/sonntaglior/Google-Drive-Monitor/assets/40151842/c55ce6a6-3416-44f3-8210-33c0fa0705b0) 

## Dependencies:
The requirements.txt file should list all Python libraries that the script depends on, and they will be installed using:
```
pip3 install -r requirements.txt
```
## Execution:
Place the **_credentials.json_** file in the same directory as the script. Run the script using:
```
python3 monitor.py
```
Upon the initial launch, a web-based authentication prompt will allow you to grant the application permission to access your Drive account. After successful authentication, the script will commence monitoring your Google Drive.

## Usage and Output:
When a file is uploaded to a non-public folder, the script outputs its current sharing permissions (Type and Role).
If a file is uploaded to a publicly accessible folder, thereby making the file public, the script will display its permissions before modifying them to private, enhancing security by limiting unwarranted exposure.
This script ensures a higher level of privacy and security for your Google Drive files, especially in shared or public folders, by proactively managing file permissions.
![image](https://github.com/sonntaglior/Google-Drive-Monitor/assets/40151842/db51dd79-bdb7-4dc2-8c71-26bae83c74be)

## Potential Security Risks in Google Drive API Usage:
### Exploitation of OAuth Consent:
If a victim grants consent to a malicious OAuth application with a highly sensitive scope (e.g., https://www.googleapis.com/auth/drive), the attacker could gain extensive access to the victim's Google Drive and execute high privileged actions on behalf of it. This level of access might enable various harmful operations.
### Ransomware Attacks via Permission Modification:
An attacker, leveraging the permissions.create API, could add themselves as editors of files owned by the victim. They could then potentially transfer the ownership of these files to themselves using the same API. Once ownership is transferred, the attacker could use the permissions.delete API to revoke all other users' access, effectively locking out the legitimate owner and other users.
### Destructive Actions:
Attackers might engage in destructive operations, such as using the files.delete API to completely erase files or folders from the victim's Drive.
### Risks of Read-Only Access:
Even less privileged scopes like https://www.googleapis.com/auth/drive.readonly pose significant risks. Such access could enable adversaries to exfiltrate sensitive data by using the files.get API to download any file from the Drive account, potentially leading to data breaches.
