# Solution Manager Job Definition

## WSUS Job-Type

The SWSUS job-type simplifies the job definition process by displaying fields to generate the command line for the different supported WSUS commands.

Select **WSUS** Job Type and then select the required task Type from the drop-down list.

WSUS supports the following Task Types.
- ExecuteClient

### Integration Selection

**Integrations or Integration Group**: Defines the WSUS machine that is associated with the connector.

### Task Details

#### ExecuteClient

The ExecuteClient task performs the selected instructions.

**Server Name**       Required, defines the server on which the updates are to be checked and/or installed.
**Application Path**  Required, defines the path to the Client component, either on the local target server or, as a shared UNC network path.
**Inclusion List**    Optional, tells the connector to install only the updates in this file on the server.
**Exclusion List**    Optional,  tells the connector to install all updates for this server, except any found in the Exclude list.
**Check Only**        Optional, tells the connector to retrieve a list of updates that are available for the server. No updates are installed. If this option is not selected, then any applicable updates are downloaded and installed.
**Restart**           Optional, indicates to the connector to restart the server after the updates have been applied if this is required.

