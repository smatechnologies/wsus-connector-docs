---
sidebar_label: 'WSUS Connector'
title: WSUS Connector overview
description: "Conceptual overview of the WSUS Connector, including scope, audience, and Windows file name considerations."
tags:
  - Conceptual
  - System Administrator
  - Connectors
---

# Overview

## What is it?

The WSUS Connector (Version 21.0.0) lets OpCon monitor, download, and install Windows updates on Microsoft Servers as part of a workflow. Servers can be optionally rebooted after updates are applied.

Use this connector to:

* Automate Windows update checks and installs across many servers from a single OpCon job.
* Apply or exclude specific Knowledge Base (KB) updates using inclusion or exclusion lists.
* Reboot target servers after installing updates, with verification that each server returns online.

## Scope

This documentation covers basic and advanced, conceptual and procedural information for running the WSUS Connector.

Out of scope:

* Running the central OpCon components. For OpCon details, see [Concepts](https://help.smatechnologies.com/opcon/core/components) in the OpCon documentation.

## Audience

This documentation is written for users with:

* A working knowledge of the Windows Server Update Services (WSUS) program.
* A basic understanding of automated job scheduling concepts.

## Windows File Names

Some systems will not allow long file names (for example, `C:\Program Files\OpConxps\`). To work around this limitation, use the 8.3 short-name format.

In 8.3 format, the 7th character becomes a tilde followed by `1`:

| Long name | 8.3 short name |
| --------- | -------------- |
| `C:\Program Files\OpConxps\` | `C:\Progra~1\OpConxps\` |

## Glossary

| Term | Definition |
| ---- | ---------- |
| WSUS | Windows Server Update Services. Microsoft's program for managing the distribution of updates released through Microsoft Update to Windows servers and workstations. |
| WSUS Connector | The OpCon component that monitors, downloads, and installs Windows updates on target servers from within an OpCon workflow. |
| Server component | The piece of the WSUS Connector scheduled by OpCon as a WSUS Windows sub-type job (`SMAWSUS.exe`). |
| Client component | The piece of the WSUS Connector that processes, downloads, and installs Windows updates on the target server (`SMAMSUpdate.exe`). |
| Multi-Instance job | An OpCon job definition with one or more instance properties. A single definition can be reused across multiple target servers. |
| Sub-type | A specialized job definition screen that simplifies generating the command line for a connector. |
