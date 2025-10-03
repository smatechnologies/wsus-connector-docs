# Installation

### Requirements

Before beginning the installation, ensure the system requirements are met. The supported software levels include:

* Any supported version o fWindows with .NETF ramework 4.5i nstalled. 
* A supported version of the MSLSAM installed on the machine.

### New Installation

To install a new WSUS Connector, complete the procedures in this section.

#### WSUS Connector Installation

1. Log in to the machine as a Local Administrator on the Windows machine where the connector will be installed.
2. Download the files from the [http://files.smastechnologies.com/](http://files.smatechnologies.com/) site.
3. Enter your valid username and password and click Login.
4. Navigate to `Root Folder/Connectors` and `Add-ons/Connectors/WSUS`.
5. Double-click the `SMA OpCon WSUS Connector Install.exe`. The Select Language screen displays.
6. Select the desired language for the installation screens and click OK. The Welcome screen displays.
7. Click Next.
8. In the remaining wizard screens: Complete the wizard.
9. In the last wizard screen: Click Done.

#### WSUSPath Global Property Configuration

1. Log in to the Enterprise Manager on the Windows machine where an Enterprise Manager is installed.
2. Double-click on **Global Properties** under the Administration topic in the Navigation Panel. The Global Properties screen displays.
3. Click **Add** on the Global Properties toolbar.
4. Enter **WSUSPath** in the Name text box.
5. Enter the documentation in the Documentation text box.
6. In the **Value** text box: Enter the *path to the SMAWSUS.exe* on the Windows machine. **Do not** include the trailing backslash in the path.

:::tip Example

`C:\Program Files\OpConxps\WSUS`

:::

7. Click Save on the Global Properties toolbar. 

### Enterprise Manager Sub-Type Installation

If you need to update the Enterprise Manager with a screen to define the WSUS jobs, you will need to install the WSUS Sub-Type.

#### WSUS Sub-Type Installation

1. Log in to the machine where the Enterprise Manager is installed.
2. Navigate to the EnterpriseManager folder in Windows Explorer.

:::tip Example

`C:\Program Files\OpConxps\EnterpriseManager x64`

:::

3. Confirm the dropins folder exists. If the folder does not exist, right-click in the EnterpriseManager folder, select **New > Folder**, and name the folder **dropins**.
4. Navigate to the location where you installed the WSUS Connector.

:::tip Example

`C:\Program Files\OpConxps\WSUS`

:::

5. Open the **EMPlugins** folder and copy the jar file.

:::tip Example

`com.sma.ui.core.jobdetails.wsus_1.0.0.yyyymmddhhss.jar`

:::

6. Paste the *jar file* to the **EnterpriseManager\dropins** folder on the Enterprise Manager machine.

:::tip Example

`C:\Program Files\OpConxps\EnterpriseManager x64\dropins\com.sma.ui.core.jobdetails.wsus_1.0.0.yyyymmddhhss.jar`

:::

7. Log in to the Enterprise Manager on the Windows machine where an Enterprise Manager is installed.
8. Double-click on Job Master under the Administration topic in the Navigation Panel. The Job Master screen displays.
9. Select a schedule in the Schedule drop-down list.
10. Click **Add** on the Job Master toolbar.
11. Under Job Properties in the Job Details frame: Select **Windows** in the **Job Type** drop-down list.
12. Select **WSUS** in the **Job Sub-Type** drop-down list to confirm that the sub-type is installed.

#### Client Configuration

For more information on Client configuration and how to share the Client folder, refer to [Client Configuration](configuration#client-configuration). 

### Solution Manager Sub-Type Installation

It should be noted that all interactions with the Solution Manager sub-type can only be completed using Solution Manager.

Download the ACSWSUS.zip file from the ftp site under **OpCon Releases\\Integrations\\WSUS**.

Extract the **ACSWSUS** directory and copy this into the **\\SAM\\plugins** for OpCon and relay installations.

For OpCon installations stop and restart the **SMA OpCon RestAPI** and **SMA OpCon Service Manager** services, for Relay stop and restart the **Relay Service**.

## Create the scripts
When using the Solution Manager sub-type, two scripts must be created. The first script contains the Connector.config information and the second script contains the drop-down list information.

Using Solution Manager
- Select **Library**.
- Select **Scripts**.
- Select **Script Types** from the upper right hand corner. 
    - Select **+Add**
    - In the ***Name*** field enter **ACSWSUS**.
    - In the ***File Extension field*** enter **txt**.
    - In the ***Description*** field enter **Used for ACSWSUS Integration**.
    - Select Save.
- Select **Script Runners** from the upper right hand corner. 
    - Select **+Add**
    - In the ***Name*** field enter **ACSWSUS**.
    - In the ***OS*** field select **WSUS** from the drop-down list.
    - In the ***Type*** field select **ACSWSUS** from the drop-down list.
    - In the ***Command*** field enter **cmd.exe /c**.
    - Select Save.
- Select **Scripts** from the upper right hand corner.
    - Create the Connector.config script.
    - Select **+Add**.
    - In the ***Name*** field enter a name for the script. It is suggested using the proposed agent name and append **_config** to the name. 
    - In the ***Type*** field select **ACSWSUS** from the drop-down list.
    - Assign the required roles.
    - In the ***Script*** paste the contents of the created Connector.config file.
    - Select Save.
 
## Create WSUS Agent Definition

Using Solution Manager
- Select **Library**.
- Select **Agents**.
    - Select **+Add**
    - In the ***Name*** field enter the name of the agent.
    - Select **WSUS** from the ***Type*** drop-down list.
    - In the ***SAP Data Services Settings*** section enter the required information.
    - In the ***Client Information*** section
        - In the ***Directory*** field enter the installation directory of the AzureVM Connector.
        - In the ***Name*** field insert **SMAWSUS.exe** (default value).
        - In the ***Config File Name*** field insert **Connector.config** (default value).
    - In the ***Config Script*** section
        - Select **ACSWSUS** from the ***Script Runner*** drop-down list.
        - Select the config script you previously created from the ***Script*** drop-down list.

- Select **Save**.

### Upgrade Installation

To upgrade the WSUS Connector, simply install the new package to the same directory as the previous install- ation. The installation package will preserve your configuration files automatically. For installation instructions, refer to [New Installation](#new-installation).

### Silent Mode

To learn how to install the WSUS Connector in silent mode, refer to [Silent Mode](https://help.smatechnologies.com/opcon/core/installation/components#silent-mode) in the OpCon Installation documentation.