# CS-Labs

I'm using this repo to keep track of the cybersecurity work I'm doing while I build toward a junior SOC / security analyst role.

The goal here isn't to make every lab look like a finished corporate report. I want to document what I actually did, what I noticed, what I got wrong at first, and what I learned from fixing it.

## Current lab

### Windows Authentication Event Log Analysis

My first lab was focused on Windows Security logs and successful logons.

I used Event Viewer and PowerShell to look through Event ID 4624 activity and compare a few different logon types. The biggest thing I learned was that reading the event correctly matters more than just memorizing the Event ID. Fields like **Subject**, **New Logon**, **Logon Type**, **Process Name**, and **Source Network Address** change the story.

[Read the Windows authentication lab](windows-event-log-analysis/README.md)

## Tools I've used so far

- Windows Event Viewer
- PowerShell
- Git / GitHub

## What I'm working on next

I'm still building the fundamentals, so this repo will grow as I get more hands-on practice with:

- failed Windows logons and account activity
- Linux logs and authentication
- networking and Wireshark
- Splunk / SIEM searches
- alert triage and incident notes

I'll update the repo as I actually complete the work.
