# Operation

SMA Technologies recommends defining the WSUS job as a Multi-Instance job with Server Name as an Instance property. The list of servers that want to use this job can be defined in Instance Definition. When the job is built this way, the individual job names automatically use the first instance property name, and each WSUS job gets identified by the server it is going to update, as shown in this next table.

### Operation Parameters

The WSUS Connector supports the following parameters:

| Argument | Required | Value |
| -------- | -------- | ----- |
| Server Name | Y | The machine on which the Microsoft updates are to be checked or installed. |
| Application Path | Y | The path to the location of SMAMSUpdate.exe to be used (on the local machine or shared UNC path on the network, e.g., `\\<SharedServer- >\WSUS\SMAMSUpdate.exe`) |
| Retrieve Updated List | Optional | This option specifies to check only for updates and not download or install them. The list of required updates is available in the JobOutput after the job is run in CheckOnly mode. |
| Include List | Optional | A text file containing a list of updates you want installed on the machine. If an inclusion list is provided, only updates from this list will be installed, provided they are needed for the machine. |
| Exclude List | Optional | A text file containing a list of updates you do not want installed on the machine. If an exclusion list is provided, the program will check for available updates for the machine and then exclude the ones from the provided list and install the rest. |
| Restart | Optional | Restart specifies an update requires a reboot of the machine. If a machine is restarted by the program, the program will wait to verify that the machine comes back online successfully (for up to 10 minutes) and then finish suc- cessfully. If the machine fails to come back online, the program will report as failed so the user can check the machine status manually. |