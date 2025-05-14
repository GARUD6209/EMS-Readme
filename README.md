# EMS-Readme

elow is a complete Markdown file. When you view it on GitHub (or many other platforms), a Copy button will appear at the top right of the code block—letting you copy the entire deployment guide in one click.

Simply copy the content below and save it (for example as deployment-guide.md) in your GitHub repository.

markdown
# Employee Management System - Deployment Guide

Below is the complete deployment guide. Use the **Copy** button (if available) at the top-right corner of this code block to copy all the steps at once.

---

```markdown
# Employee Management System - Deployment Guide

## 1. Compress the Published Files
After extracting the `publish.zip` and verifying the application, compress the deployment files to save them for future use:

```powershell
Compress-Archive -Path "./publish/*" -DestinationPath "D:\.net_dev\EmployeeAdminPortal\EmployeeManagementSystem\EmployeeManagementSystem.Server\publish.zip"
2. Extract the Published Files
Extract the published files using:

bash
unzip -o publish.zip -d ~/publish
> Note: You can ignore warnings about backslashes being used as path separators.

3. Navigate to the Publish Directory
Move into the extracted folder:

bash
cd ~/publish
4. Stop the Running Application
Find the process running on port 5000:

bash
sudo netstat -tulnp | grep :5000
Identify the process ID (PID) and terminate it:

bash
kill -9 <Process_ID>
Confirm that the application is no longer running:

bash
sudo netstat -tulnp | grep :5000
5. Set Environment Variables
Ensure the application listens on the correct URL and port by setting:

bash
export ASPNETCORE_URLS="http://*:5000"
6. Start the Application
Launch the application in the background:

bash
nohup dotnet EmployeeManagementSystem.Server.dll > output.log 2>&1 &
Verify that it's running successfully:

bash
sudo netstat -tulnp | grep :5000
7. Monitor Logs (Optional)
Check the logs to ensure there are no errors:

bash
tail -f output.log
Conclusion
After completing these steps, your application should be successfully redeployed and accessible on port 5000. The updated publish.zip archive can be used for future deployments.


---

Simply paste this file into your GitHub repository, and you'll have a convenient, single-copy deployment guide.
Now you have a Markdown file with a single code block; GitHub’s native functionality will display a Copy button that lets users copy the entire guide in one click. Enjoy!
