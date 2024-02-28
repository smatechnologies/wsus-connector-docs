# Reference Information

### WSUS Connector Messages

The WSUS Connector can exit with the following codes:

:::info Note

For exit codes, the retrieve update list setting determines whether or not the connector will apply Windows updates.

:::

### Exit Codes

| Exit Code | Description |
| --------- | ----------- |
| Retrieve Update List = FALSE | This indicates that updates are to be downloaded and installed. |
| 0000 | No updates available for the Server. |
| 0005 | No updates available for the Server and one or more warning messages were returned. |
| 0009 | An update failed to install after the machine was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| 0010 | No updates available for the Server and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| 0015 | No updates available for the Server and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) Additional warn- ing messages were returned. |
| 0100 | Updates available for the Server and installed with no reboot. |
| 0105 | Updates available for the Server and installed. Server was not rebooted and one or more warning messages were returned. |
| 0110 | Updates available for the Server and installed. The Server was rebooted. |
| 0115 | Updates available for the Server and installed. The Server was rebooted and there were warnings returned. |
| Retrieve Update List = TRUE | This indicates that the connector is to check for updates but not install them. |
| 1000 | No updates available for the Server. |
| 1005 | No updates available for the Server and one or more warning messages were returned.
1010 | No updates available for the Server and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| 1015 | No updates available for the Server and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) Additional warn- ing messages were returned. |
| 1100 | Updates available for the Server. |
| 1105 | Updates available for the Server and one or more warning messages were returned. |
| 1110 | Updates are available for the Server and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) | 
| 1115 | Updates are available for the Server and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) Additional warn- ing messages were returned. |

The WSUS Connector can fail with the following code:

| Failure Code | Description |
| ------------ | ----------- |
| -1 | 1 or more updates were not successfully installed on the Server. Use View Job Output to review what happened. |