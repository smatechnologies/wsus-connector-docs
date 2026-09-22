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

The exit code is a **total**, not a set of positions. The connector starts from `0`, or from `-1` when an update failed to install, and adds a value for each condition that applied:

| Add | When |
| --- | ---- |
| `1000` | The run was check-only (Retrieve Update List = TRUE). |
| `100` | Updates were available, or were installed. |
| `10` | The server was rebooted. |
| `5` | One or more warnings were returned. |

So `1110` is a check-only run (1000) where updates were available (100) on a server that had been rebooted (10). And `0009` is a failed install (`-1`) on a server that was rebooted (`+10`) — which is why it does not follow the pattern of the other codes.

The tables below list the combinations you are most likely to see. Any code not listed can be read with the rule above.

:::info Note

The **Retrieve Update List** setting determines whether the connector applies Windows updates or only checks for them.

:::

## Exit codes — install run

These codes apply when **Retrieve Update List = FALSE** (updates are downloaded and installed).

| Exit Code | Description |
| --------- | ----------- |
| `0000` | No updates available for the Server. |
| `0004` | An update failed to install, and one or more warning messages were returned. (`-1` plus `5`.) |
| `0005` | No updates available for the Server, and one or more warning messages were returned. |
| `0009` | An update failed to install after the machine was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) (`-1` plus `10`.) |
| `0010` | No updates available for the Server, and it was rebooted. ('Restart Server' option set and a reboot was required from a previous update.) |
| `0014` | An update failed to install after the machine was rebooted, and warning messages were returned. (`-1` plus `10` plus `5`.) |
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
| `-1` | The connector ended with an error. This includes an update that failed to install, and also errors that stop the connector before it reaches an update — an invalid command line, a target server it cannot reach, or a scheduling or communication failure. Use **View Job Output** to see which. |

## FAQs

**How do I tell whether updates were installed or only checked?**
Check-only runs add `1000`, so any code of `1000` or more is a check-only run. Anything below that is an install run.

**What does exit code `-1` mean?**
The connector ended with an error. That may be an update that failed to install, or a failure earlier than that — a bad command line, an unreachable target server, or a scheduling or communication problem. The Job Output identifies which, and is the first place to look.

**How do I read a code that is not in the tables?**
Subtract the components: `1000` for a check-only run, `100` for updates available or installed, `10` for a reboot, `5` for warnings. What remains is `0` for a clean run or `-1` for a failed install. Refer to [How to read an exit code](#how-to-read-an-exit-code).

## Glossary

| Term | Definition |
| ---- | ---------- |
| Exit code | The numeric result returned by the WSUS Connector on completion. OpCon uses the exit code to determine the job's final status. |
| Retrieve Update List | The connector option that controls whether updates are installed (FALSE) or only checked (TRUE). |
| Restart Server | The connector option that allows the connector to reboot the target server when an update requires it. |
| OpCon Event | An automated action OpCon fires in response to a job status, including specific exit codes. |
