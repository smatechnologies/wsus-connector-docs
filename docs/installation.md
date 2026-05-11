---
sidebar_label: 'Installation'
title: WSUS Connector installation
description: "Install, configure, and upgrade the WSUS Connector, including the Enterprise Manager and Solution Manager sub-types."
tags:
  - Procedural
  - System Administrator
  - Connectors
  - Installation
---

# Installation

## What is it?

Installing the WSUS Connector puts the components OpCon needs to run Windows Update jobs in place. The installation has three independent parts:

| Part | When you need it |
| ---- | ---------------- |
| WSUS Connector | Always. Provides the server and client components. |
| Enterprise Manager sub-type | If you define WSUS jobs in the **Enterprise Manager** UI. |
| Solution Manager sub-type | If you define WSUS jobs in the **Solution Manager** UI. |

You only need the sub-type that matches the OpCon UI you use.

## Requirements

Before beginning the installation, ensure the system requirements are met:

* Any supported version of Windows with **.NET Framework 4.5** installed.
* A supported version of the **Microsoft Agent** installed on the machine.

## Install the WSUS Connector

This is the base install. Complete this section before installing either sub-type.

### Step 1: Install the connector

To install the WSUS Connector, complete the following steps:

1. Log in to the Windows machine where the connector will be installed as a Local Administrator.
2. Download the files from [http://files.smatechnologies.com/](http://files.smatechnologies.com/).
3. Enter your username and password and select **Login**.
4. Go to **Root Folder > Connectors > Add-ons > Connectors > WSUS**.
5. Open `SMA OpCon WSUS Connector Install.exe`. The Select Language screen displays.
6. Select the desired language and select **OK**. The Welcome screen displays.
7. Select **Next**.
8. Complete the remaining wizard screens.
9. On the last wizard screen, select **Done**.

### Step 2: Configure the WSUSPath global property

The `WSUSPath` global property tells OpCon where `SMAWSUS.exe` lives on the Windows machine.

To configure the global property, complete the following steps:

1. Log in to the Enterprise Manager.
2. Open **Global Properties** under the Administration topic in the Navigation Panel. The Global Properties screen displays.
3. Select **Add** on the Global Properties toolbar.
4. In the **Name** text box, enter `WSUSPath`.
5. In the **Documentation** text box, enter documentation for the property.
6. In the **Value** text box, enter the path to `SMAWSUS.exe`.

   :::caution

   Do **not** include a trailing backslash in the path.

   :::

   :::tip Example

   `C:\Program Files\OpConxps\WSUS`

   :::

7. Select **Save** on the Global Properties toolbar.

## Install the Enterprise Manager sub-type

Install this sub-type only if you define WSUS jobs in Enterprise Manager.

### Step 1: Install the WSUS sub-type

To install the WSUS sub-type, complete the following steps:

1. Log in to the machine where the Enterprise Manager is installed.
2. Go to the EnterpriseManager folder in Windows Explorer.

   :::tip Example

   `C:\Program Files\OpConxps\EnterpriseManager x64`

   :::

3. Confirm the `dropins` folder exists. If it does not, right-click the EnterpriseManager folder, select **New > Folder**, and name the new folder `dropins`.
4. Go to the location where you installed the WSUS Connector.

   :::tip Example

   `C:\Program Files\OpConxps\WSUS`

   :::

5. Open the **EMPlugins** folder and copy the jar file.

   :::tip Example

   `com.sma.ui.core.jobdetails.wsus_1.0.0.yyyymmddhhss.jar`

   :::

6. Paste the jar file into the `EnterpriseManager\dropins` folder on the Enterprise Manager machine.

   :::tip Example

   `C:\Program Files\OpConxps\EnterpriseManager x64\dropins\com.sma.ui.core.jobdetails.wsus_1.0.0.yyyymmddhhss.jar`

   :::

### Step 2: Verify the sub-type is registered

To verify the sub-type loaded into Enterprise Manager, complete the following steps:

1. Log in to the Enterprise Manager.
2. Open **Job Master** under the Administration topic in the Navigation Panel. The Job Master screen displays.
3. Select a schedule in the **Schedule** list.
4. Select **Add** on the Job Master toolbar.
5. Under Job Properties in the Job Details frame, select **Windows** in the **Job Type** list.
6. Select **WSUS** in the **Job Sub-Type** list to confirm that the sub-type is installed.

### Agent configuration

For information about agent configuration and how to share the Client folder, see [Configuration](configuration#client-configuration).

## Install the Solution Manager sub-type

Install this sub-type only if you define WSUS jobs in Solution Manager.

:::info Note

All interactions with the Solution Manager sub-type can only be completed using Solution Manager.

:::

### Step 1: Deploy the plug-in files

To deploy the plug-in files, complete the following steps:

1. Download `ACSWSUS.zip` from the ftp site under **OpCon Releases > Integrations > WSUS**.
2. Extract the `ACSWSUS` directory and copy it into the `\SAM\plugins` folder for OpCon and relay installations.
3. Restart the appropriate services:

   | Environment | Services to restart |
   | ----------- | ------------------- |
   | OpCon | **SMA OpCon RestAPI** and **SMA OpCon Service Manager** |
   | Relay | **Relay Service** |

### Step 2: Create the scripts

Two scripts are required when using the Solution Manager sub-type:

* A **Connector.config** script that holds the connector configuration.
* A script that holds the list information.

To create the scripts, complete the following steps in Solution Manager:

1. Go to **Library > Scripts**.
2. Create the script type:
    1. Select **Script Types** from the upper right corner, then **+Add**.
    2. In the **Name** field, enter `ACSWSUS`.
    3. In the **File Extension** field, enter `txt`.
    4. In the **Description** field, enter `Used for ACSWSUS Integration`.
    5. Select **Save**.
3. Create the script runner:
    1. Select **Script Runners** from the upper right corner, then **+Add**.
    2. In the **Name** field, enter `ACSWSUS`.
    3. In the **OS** field, select `WSUS` from the list.
    4. In the **Type** field, select `ACSWSUS` from the list.
    5. In the **Command** field, enter `cmd.exe /c`.
    6. Select **Save**.
4. Create the **Connector.config** script:
    1. Select **Scripts** from the upper right corner, then **+Add**.
    2. In the **Name** field, enter a name for the script. SMA Technologies suggests using the proposed agent name with `_config` appended.
    3. In the **Type** field, select `ACSWSUS` from the list.
    4. Assign the required roles.
    5. In the **Script** field, paste the contents of the created Connector.config file.
    6. Select **Save**.

### Step 3: Create the WSUS agent definition

To create the agent definition, complete the following steps in Solution Manager:

1. Go to **Library > Agents**.
2. Select **+Add**.
3. In the **Name** field, enter the name of the agent.
4. In the **Type** list, select `WSUS`.
5. In the **SAP Data Services Settings** section, enter the required information.
6. In the **Client Information** section:
    * In the **Directory** field, enter the installation directory of the AzureVM Connector.
    * In the **Name** field, enter `SMAWSUS.exe` (default value).
    * In the **Config File Name** field, enter `Connector.config` (default value).
7. In the **Config Script** section:
    * In the **Script Runner** list, select `ACSWSUS`.
    * In the **Script** list, select the config script you previously created.
8. Select **Save**.

## Upgrade an existing installation

To upgrade the WSUS Connector, install the new package over the previous installation. The installation package preserves your configuration files automatically.

For installation steps, see [Install the WSUS Connector](#install-the-wsus-connector).

## Silent mode

To install the WSUS Connector in silent mode, see [Silent Mode](https://help.smatechnologies.com/opcon/core/installation/components#silent-mode) in the OpCon Installation documentation.

## FAQs

**What if the Enterprise Manager `dropins` folder does not exist?**
Create it. Right-click the EnterpriseManager folder, select **New > Folder**, and name the folder `dropins`.

**Do I need both the Enterprise Manager and Solution Manager sub-types?**
No. Install only the sub-type that matches the OpCon UI you use to define WSUS jobs.

**Where do I install the client component?**
Either on each target server, or once in a shared UNC location accessible to all target servers. The path is provided to the connector at job submission time.

**What happens to my configuration during an upgrade?**
The installation package preserves your existing configuration files automatically when installed to the same directory.

## Glossary

| Term | Definition |
| ---- | ---------- |
| Connector | The OpCon component that integrates with an external system. The WSUS Connector integrates with Windows Server Update Services. |
| Sub-type | A specialized job definition screen that simplifies generating the command line for a connector. |
| Global Property | A named value managed in OpCon and referenced by jobs and connectors at run time. `WSUSPath` is the global property used by the WSUS Connector. |
| dropins | The Enterprise Manager folder where plug-in jar files are placed so that Enterprise Manager loads them on start. |
