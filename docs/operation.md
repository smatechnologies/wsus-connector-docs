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
| **Include List** | No | Text file listing the updates to install. If provided, only updates matching an entry in this list are installed (and only if needed on the machine). See "Include and Exclude lists" below. |
| **Exclude List** | No | Text file listing the updates to skip. If provided, the connector installs all needed updates except those matching an entry in this list. See "Include and Exclude lists" below. |
| **Restart** | No | Allows the connector to reboot the machine when an update requires it. See "Restart behavior" below. |

### Include and Exclude lists

Each list is a plain text file with **one entry per line**. Entries are matched against the **title** of each available update as a substring, so an entry does not have to be a complete KB identifier — it matches if the update's title contains it.

:::caution Do not supply both lists
If both an Include List and an Exclude List are provided, **the Exclude List is ignored**. The connector applies the inclusion filter to the full set of available updates, discarding the exclusion result. Use one list or the other, and keep the single list authoritative.
:::

Because matching is a substring test, write entries carefully:

| Write | Not | Why |
| ----- | --- | --- |
| `KB5001330` | `5001330` | The full KB form is what appears in update titles. |
| One KB per line | `Security` | A short or generic entry matches every update whose title contains it. |

:::caution A blank line matches every update
An empty line matches every title. A blank line in an Exclude List therefore excludes **all** updates, and a blank line in an Include List includes all of them. Check that the file has no empty lines.
:::

A list that matches nothing is not reported as an error. The connector finds no updates to install and the job **finishes successfully having installed nothing**. The Job Output records the number of updates before and after each list is applied, which is the way to confirm a list did what you intended.

### Restart behavior

When **Restart** is enabled and an update requires a reboot:

1. The connector reboots the machine.
2. The connector pings the machine, waiting for it to stop answering and then answer again, for up to **30 minutes**.
3. Once the machine is answering again, the connector waits a further three minutes for it to settle, then finishes successfully.
4. If that has not happened within 30 minutes, the connector reports the job as Failed so a person can check the machine manually.

## FAQs

**Why a Multi-Instance job?**
A single Multi-Instance job lets one definition apply updates to many servers, with one built job per server. Each built job is named after the server it updates and reports its status independently.

**What happens if a target server fails to come back online after a reboot?**
The connector waits up to 30 minutes for the machine to stop answering and then answer again. If that has not happened in that time, the connector reports the job as Failed so a person can check the machine manually.

**Where do I see the list of updates the connector found in CheckOnly mode?**
In the Job Output for the WSUS job. The list of required updates is captured there when **Retrieve Update List** is selected.

## Glossary

| Term | Definition |
| ---- | ---------- |
| CheckOnly mode | The WSUS Connector mode enabled by **Retrieve Update List**. The connector reports available updates without installing them. |
| Include List | A text file, one entry per line, that limits the connector to installing updates whose title contains one of the entries. |
| Exclude List | A text file, one entry per line, that prevents the connector from installing updates whose title contains one of the entries. Ignored if an Include List is also supplied. |
| Multi-Instance job | An OpCon job definition with one or more instance properties. OpCon produces one built job per instance when the schedule is built. |
| Instance property | A property whose value differs across the instances of a Multi-Instance job — for the WSUS Connector, typically the target Server Name. |
| Job Output | The output captured by OpCon for a built job, accessible via the **View Job Output** action. |
