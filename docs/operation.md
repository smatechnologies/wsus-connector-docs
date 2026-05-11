---
sidebar_label: 'Operation'
title: WSUS Connector operation
description: "Reference for the WSUS Connector operation parameters that drive update checks, installation, and target-server reboot behavior."
tags:
  - Reference
  - Automation Engineer
  - Operations Staff
  - Connectors
---

# Operation

## What is it?

This page describes the runtime parameters the WSUS Connector accepts and the recommended pattern for applying updates to many servers from a single OpCon job definition.

Use this page to:

* Look up what each WSUS Connector parameter controls.
* Configure a Multi-Instance WSUS job for multiple target servers.
* Understand how the connector handles inclusion lists, exclusion lists, and reboots.

## Recommended pattern

SMA Technologies recommends defining the WSUS job as a **Multi-Instance job** with Server Name as an instance property. List the target servers in the Instance Definition.

With this pattern:

* OpCon builds one job per server.
* Each built job is automatically named after the server it updates.
* Each built job runs and reports independently.

## Operation parameters

The WSUS Connector supports the following parameters:

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| **Server Name** | Yes | The machine on which the Microsoft updates are to be checked or installed. |
| **Application Path** | Yes | The path to `SMAMSUpdate.exe`. Use the local path on the target machine or a shared UNC path on the network. Example: `\\<SharedServer>\WSUS\SMAMSUpdate.exe` |
| **Retrieve Update List** | No | Checks for updates without downloading or installing them. The list of required updates appears in the Job Output after the job is run in CheckOnly mode. |
| **Include List** | No | Text file listing the updates to install. If provided, only updates from this list are installed (and only if needed on the machine). |
| **Exclude List** | No | Text file listing the updates to skip. If provided, the connector installs all needed updates except those listed. |
| **Restart** | No | Allows the connector to reboot the machine when an update requires it. See "Restart behavior" below. |

### Restart behavior

When **Restart** is enabled and an update requires a reboot:

1. The connector reboots the machine.
2. The connector waits up to **10 minutes** for the machine to come back online.
3. If the machine returns within 10 minutes, the connector finishes successfully.
4. If the machine does not return within 10 minutes, the connector reports the job as Failed so a person can check the machine manually.

## FAQs

**Why a Multi-Instance job?**
A single Multi-Instance job lets one definition apply updates to many servers, with one built job per server. Each built job is named after the server it updates and reports its status independently.

**What happens if a target server fails to come back online after a reboot?**
The connector waits up to 10 minutes. If the machine does not return, the connector reports the job as Failed so a person can check the machine manually.

**Where do I see the list of updates the connector found in CheckOnly mode?**
In the Job Output for the WSUS job. The list of required updates is captured there when **Retrieve Update List** is selected.

## Glossary

| Term | Definition |
| ---- | ---------- |
| CheckOnly mode | The WSUS Connector mode enabled by **Retrieve Update List**. The connector reports available updates without installing them. |
| Multi-Instance job | An OpCon job definition with one or more instance properties. OpCon produces one built job per instance when the schedule is built. |
| Instance property | A property whose value differs across the instances of a Multi-Instance job — for the WSUS Connector, typically the target Server Name. |
| Job Output | The output captured by OpCon for a built job, accessible via the **View Job Output** action. |
