Employee Management System - Deployment Guide
Below is the complete deployment guide. Use the Copy button (if available) at the top-right corner of this code block to copy all the steps at once.

# 0. Prepare and Upload the Publish Archive

Connect ec2 machine via ssh

```
ssh -i "D:\.net_dev\EmployeeAdminPortal\EmployeeManagementSystem\EMS.pem" ec2-user@52.66.255.111
```

Delete any previous publish directory and archive on the server:

```bash
rm -rf ~/publish
rm publish.zip
```

Kill any running application started with nohup (if any):

```bash
sudo netstat -tulnp | grep :5000
```

```
[ec2-user@ip-172-31-5-37 ~]$ sudo netstat -tulnp | grep :5000
tcp6       0      0 :::5000                 :::*                    LISTEN      263788/dotnet
[ec2-user@ip-172-31-5-37 ~]$
```

```bash
kill -9 <PID>
```

Compress the publish directory on the local system:

```powershell
Compress-Archive -Path "./publish" -DestinationPath "D:\.net_dev\EmployeeAdminPortal\EmployeeManagementSystem\EmployeeManagementSystem.Server\publish.zip"
```

Upload the archive to your server (example for EC2) via a different terminal:

```bash
scp -i "/mnt/d/.net_dev/EmployeeAdminPortal/EmployeeManagementSystem/EMS.pem" "/mnt/d/.net_dev/EmployeeAdminPortal/EmployeeManagementSystem/EmployeeManagementSystem.Server/publish.zip" ec2-user@52.66.255.111:~
```

1. Compress the Published Files
   After extracting the publish.zip and verifying the application, compress the deployment files to save them for future use:

2. Extract the Published Files
   Extract the published files using:

```bash
unzip -o publish.zip -d ~/publish
```

3. Navigate to the Publish Directory
   Move into the extracted folder:

```bash
cd ~/publish
```

4. Stop the Running Application
   Find the process running on port 5000:

```bash
sudo netstat -tulnp | grep :5000
```

Identify the process ID (PID) and terminate it:

```bash
kill -9 <Process_ID>
```

Confirm that the application is no longer running:

```bash
sudo netstat -tulnp | grep :5000
```

5. Set Environment Variables
   Ensure the application listens on the correct URL and port by setting:

```bash
export ASPNETCORE_URLS="http://*:5000"
```

6. Start the Application
   Launch the application in the background:

```bash
nohup dotnet EmployeeManagementSystem.Server.dll > output.log 2>&1 &
```

Verify that it's running successfully:

```bash
sudo netstat -tulnp | grep :5000
```

7. Monitor Logs (Optional)
   Check the logs to ensure there are no errors:

```bash
tail -f output.log
```

Conclusion
After completing these steps, your application should be successfully redeployed and accessible on port 5000. The updated publish.zip archive can be used for future deployments.
