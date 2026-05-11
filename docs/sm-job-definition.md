---
sidebar_label: 'Solution Manager job definition'
title: WSUS job definition in Solution Manager
description: "Define a WSUS job in Solution Manager using the WSUS job type and the ExecuteClient task type."
tags:
  - Procedural
  - Automation Engineer
  - Connectors
  - Jobs
  - Solution Manager
---

# Solution Manager Job Definition

## What is it?

The WSUS job type in Solution Manager generates the command line for you and exposes the WSUS-specific options on the **Task Details** section.

Use this page to:

* Define WSUS jobs in Solution Manager.
* Associate a WSUS job with an integration that points at the target WSUS machine.
* Configure `ExecuteClient` task options for a target server.

## Define a WSUS job

To define a WSUS job, complete the following steps:

1. Select **WSUS** in the **Job Type** field.
2. Select the required Task Type from the list.

WSUS supports the following task types:

* `ExecuteClient`

## Integration selection

| Field | Description |
| ----- | ----------- |
| **Integrations** or **Integration Group** | Defines the WSUS machine that is associated with the connector. |

## Task details

### ExecuteClient

The `ExecuteClient` task performs the selected instructions on a target server.

| Field | Required | Description |
| ----- | -------- | ----------- |
| **Server Name** | Yes | The server on which updates are to be checked or installed. |
| **Application Path** | Yes | The path to the Client component — either on the local target server or as a shared UNC network path. |
| **Inclusion List** | No | Tells the connector to install only the updates listed in this file. |
| **Exclusion List** | No | Tells the connector to install all updates for this server except those listed in this file. |
| **Check Only** | No | Tells the connector to retrieve a list of available updates without installing them. If cleared, applicable updates are downloaded and installed. |
| **Restart** | No | Tells the connector to restart the server after the updates are applied if a restart is required. |

## FAQs

**Which task type should I use for a standard update job?**
`ExecuteClient`. It is the only task type currently supported by the WSUS job type.

**How do I check for updates without applying them?**
Select the **Check Only** option in the `ExecuteClient` task. The connector reports the list of available updates without installing them.

**How do I apply different inclusion or exclusion lists to different servers?**
Use a separate inclusion or exclusion list file per group of servers, and reference the appropriate file in each task definition.

## Glossary

| Term | Definition |
| ---- | ---------- |
| Integration | A Solution Manager construct that represents an external system the connector communicates with — for the WSUS Connector, the WSUS machine. |
| ExecuteClient | The WSUS task type that runs the client component on a target server to check, download, install, and optionally restart for Windows updates. |
| Inclusion List | A text file that limits the connector to installing only the updates listed in the file. |
| Exclusion List | A text file that prevents the connector from installing the updates listed in the file. |
