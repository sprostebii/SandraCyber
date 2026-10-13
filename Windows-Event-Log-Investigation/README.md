# 🔍 Windows Event Log Investigation

## Overview

This project documents a hands-on investigation of Windows authentication events using Windows Event Viewer.

The lab was designed to generate controlled failed logon attempts and analyze the resulting Windows Security events from a SOC analyst perspective.

---

## 🎯 Objective

The objectives of this investigation were to:

- Generate controlled failed authentication attempts
- Identify the corresponding Windows Security Event
- Analyze the account, logon type, source address, and failure reason
- Determine whether repeated failed logons are sufficient to classify the activity as a brute-force attack

---

## 🖥️ Environment

- Windows virtual machine
- Windows Event Viewer
- Command Prompt
- Windows Security Log

---

## 🧪 Lab Scenario

Three controlled failed authentication attempts were generated from the local Windows machine using:

```cmd
An invalid password was entered during each attempt.
The purpose was to observe how failed authentication activity appears in the Windows Security Log.
🔎 Evidence 1 — Failed Logon Event
Windows Event Viewer recorded:
Event ID: 4625 — An account failed to log on
Key information observed:
Field	Value
Event ID	4625
Account Name	FakeSOCUser
Logon Type	2
Failure Reason	Unknown user name or bad password
Workstation Name	PC1
Source Network Address	::1


Analysis
Event ID 4625 indicates a failed logon attempt.
The target account was FakeSOCUser.
The event recorded Logon Type 2, which represents an interactive logon.
The source address was ::1, the IPv6 loopback address. This indicates that the authentication request originated locally from the same machine rather than from a remote host.
The failure reason was:
Unknown user name or bad password.

Three failed attempts occurred in a short period of time. Repeated authentication failures can be an indicator of brute-force activity; however, three failed attempts alone are not sufficient to confirm a brute-force attack.
Additional context and authentication events would be required before classifying the activity as malicious.
🧠 Analyst Assessment
Initial classification: Suspicious authentication activity
Brute-force confirmed: No
Reason: Multiple failed logons were observed, but the number of attempts and available evidence are insufficient to conclusively identify automated password guessing.
Further investigation should include:
- Reviewing additional Event ID 4625 events
- Checking the frequency and timing of failed attempts
- Identifying whether multiple usernames were targeted
- Reviewing source addresses
- Checking for a successful Event ID 4624 following the failures
📚 What I Learned
Through this investigation, I practiced:
- Windows Security Event analysis
- Event ID 4625 investigation
- Authentication log analysis
- Understanding Windows Logon Types
- Identifying IPv6 loopback traffic
- Distinguishing suspicious activity from confirmed malicious activity
- Making evidence-based SOC conclusions
🚧 Next Step
Analyze successful authentication events (Event ID 4624) and correlate them with the failed logon activity.
