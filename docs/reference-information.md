---
sidebar_label: 'Reference information'
title: WSUS Connector reference information
description: "Reference for the WSUS Connector exit codes and failure code, including the meaning of each code with Retrieve Update List on or off."
tags:
  - Reference
  - Operations Staff
  - System Administrator
  - Connectors
---

# Reference Information

## What is it?

This reference lists the exit codes that the WSUS Connector can return and the meaning of each code. Use it to interpret job results and to drive OpCon Events for follow-up actions.

Use this page to:

* Investigate a Failed WSUS job.
* Define OpCon Events that react to specific exit codes.
* Interpret Job Output from a CheckOnly run versus an install run.

## How to read an exit code

The exit code follows a pattern that signals what the connector did and what was found:

| Position | Meaning |
| -------- | ------- |
| Leading digit | `0` — install run (Retrieve Update List = FALSE) <br /> `1` — check-only run (Retrieve Update List = TRUE) |
| Middle digits | `00` — no updates available <br /> `10` — server was rebooted from a prior update <br /> `01` — install failed after a reboot <br /> `100` — updates available (and installed on a `0`-run) |
| Trailing digit | `0` — clean result <br /> `5` — one or more warnings were returned <br /> `9` — install failed after a reboot |

:::info Note

The **Retrieve Update List** setting determines whether the connector applies Windows updates or only checks for them.

:::

## Exit codes — install run

These codes apply when **Retrieve Update List = FALSE** (updates are downloaded and installed).

| Exit Code | Description |
| --------- | ----------- |
| `0000` | No updates available for the Server. |
| `0005` | No updates available for the Server, and one or more warning messages were returned. |
| `0009` | An update failed to install after the machine was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| `0010` | No updates available for the Server, and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| `0015` | No updates available for the Server, and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) Additional warning messages were returned. |
| `0100` | Updates available for the Server and installed with no reboot. |
| `0105` | Updates available for the Server and installed. Server was not rebooted, and one or more warning messages were returned. |
| `0110` | Updates available for the Server and installed. The Server was rebooted. |
| `0115` | Updates available for the Server and installed. The Server was rebooted, and there were warnings returned. |

## Exit codes — check-only run

These codes apply when **Retrieve Update List = TRUE** (the connector checks for updates without installing them).

| Exit Code | Description |
| --------- | ----------- |
| `1000` | No updates available for the Server. |
| `1005` | No updates available for the Server, and one or more warning messages were returned. |
| `1010` | No updates available for the Server, and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| `1015` | No updates available for the Server, and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) Additional warning messages were returned. |
| `1100` | Updates available for the Server. |
| `1105` | Updates available for the Server, and one or more warning messages were returned. |
| `1110` | Updates are available for the Server, and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| `1115` | Updates are available for the Server, and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) Additional warning messages were returned. |

## Failure code

The WSUS Connector can also fail with the following code:

| Failure Code | Description |
| ------------ | ----------- |
| `-1` | One or more updates were not successfully installed on the Server. Use **View Job Output** to review what happened. |

## FAQs

**How do I tell whether updates were installed or only checked?**
Look at the leading digit of the exit code. Codes starting with `0` are install runs. Codes starting with `1` are check-only runs.

**What does exit code `-1` mean?**
At least one update did not install successfully on the target server. Open the Job Output to review the cause.

**What does the trailing digit signal in an exit code?**
A `5` indicates one or more warnings. A `9` indicates an install failure after a reboot. A `0` indicates a clean result for that case.

## Glossary

| Term | Definition |
| ---- | ---------- |
| Exit code | The numeric result returned by the WSUS Connector on completion. OpCon uses the exit code to determine the job's final status. |
| Retrieve Update List | The connector option that controls whether updates are installed (FALSE) or only checked (TRUE). |
| Restart Server | The connector option that allows the connector to reboot the target server when an update requires it. |
| OpCon Event | An automated action OpCon fires in response to a job status, including specific exit codes. |
