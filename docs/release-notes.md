---
sidebar_label: 'Release notes'
title: WSUS Connector release notes
description: "Version history and change details for the WSUS Connector, including new features, improvements, and bug fixes."
tags:
  - Reference
  - System Administrator
  - Connectors
---

# WSUS Connector release notes

## Compatibility

This version of the WSUS Connector is compatible with OpCon Release(s) 16.1.2 and higher.

## 21

### 21.0.0

2021 August

#### Fixes

:white_check_mark: Fixed an issue in WSUS Connector where on Windows 2019, the connector job would keep running and never reboot the server on which the updates are to be applied.

## 16

### 16.1.0.0

2016 November

#### Fixes

:white_check_mark: Fixed an issue where the WSUS Connector failed to get updates if Include List or Exclude List were defined under WSUS Job Details.

:white_check_mark: Fixed an issue with the connector where WSUS updates would not get installed on machines in a different time zone.
