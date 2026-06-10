# README.md

# Threat Hunt: Internet-Exposed Windows Endpoint Subjected to Brute Force Activity

<p align="center">
  <img src="images/threat_hunt_summary.png" width="1000">
</p>

## Overview

This project documents a threat hunting investigation performed against a Windows 11 virtual machine that was inadvertently exposed to the public internet. The objective was to determine whether external attackers successfully gained access through brute-force authentication attempts.

The investigation was conducted using Microsoft Defender XDR Advanced Hunting and Kusto Query Language (KQL).

## Scenario

During routine security monitoring, a Windows 11 endpoint was identified as internet-facing. Because exposed systems are frequently targeted by automated scanning and credential attacks, a threat hunt was initiated to determine:

* Whether the device had been exposed to the internet
* Whether external entities attempted authentication
* Whether any brute-force attacks succeeded
* Whether unauthorized access occurred
* Which MITRE ATT&CK techniques were observed

## Environment

| Component      | Value                         |
| -------------- | ----------------------------- |
| Platform       | Microsoft Defender XDR        |
| Endpoint       | Windows 11                    |
| Device Name    | Win11-Jared-VM                |
| Data Sources   | DeviceInfo, DeviceLogonEvents |
| Query Language | KQL                           |

## Investigation Methodology

### 1. Preparation

Hypothesis:

> During the period that the endpoint was exposed to the internet, attackers may have attempted to gain access through password guessing or brute-force authentication attacks.

### 2. Data Collection

Relevant telemetry:

* DeviceInfo
* DeviceLogonEvents

### 3. Analysis

Performed the following activities:

* Verified internet exposure
* Identified failed logon attempts
* Investigated suspicious IP addresses
* Correlated successful logons
* Validated user activity
* Mapped findings to MITRE ATT&CK

### 4. Investigation Findings

#### Finding 1: Internet Exposure

The endpoint remained internet-facing for several days.

Risk:

* Increased attack surface
* Exposure to internet-wide scanners
* Potential brute-force activity

#### Finding 2: Failed Authentication Attempts

Numerous failed authentication attempts were observed from external IP addresses.

Assessment:

* Consistent with password-guessing activity
* Consistent with automated brute-force attacks

#### Finding 3: No Successful Authentication From Suspicious Sources

Analysis of the highest-volume source IP addresses revealed no successful logons.

Assessment:

* Brute-force attempts unsuccessful

#### Finding 4: Legitimate User Activity

All successful network logons originated from the expected user account.

Assessment:

* No evidence of unauthorized access
* No anomalous geolocation activity identified

## MITRE ATT&CK Mapping

| Technique                      | ATT&CK ID |
| ------------------------------ | --------- |
| Active Scanning                | T1595     |
| Brute Force: Password Guessing | T1110.001 |
| Valid Accounts (Attempted)     | T1078     |

## Remediation

Implemented:

* Network Security Group hardening
* Restricted RDP access
* Account lockout policies
* Multi-Factor Authentication (MFA)

## Outcome

The endpoint was exposed to the public internet and received multiple brute-force login attempts.

No evidence was identified indicating:

* Successful brute-force authentication
* Unauthorized access
* Persistence
* Privilege escalation
* Lateral movement

The incident was determined to be unsuccessful attacker activity.

## Skills Demonstrated

* Threat Hunting
* Incident Investigation
* KQL Development
* Microsoft Defender XDR
* ATT&CK Mapping
* Detection Engineering
* Security Documentation
* Security Hardening
