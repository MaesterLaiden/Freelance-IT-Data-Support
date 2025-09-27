# Freelance IT & Data Support (Remote) — Case Study & Experience  
**Muhammad Abdulazeez Elladan**  
**Role:** Freelance IT & Data Support (Remote)  
**Period:** 2024 – 2025  
**Mode:** Chat / Email / Ticket-based support, remote clients (small businesses / individual clients)

---

## Overview
This document summarizes my freelance IT & data support work completed between 2024 and 2025. The work focused on Tier-1 helpdesk functions delivered via chat and email, accurate data entry, and maintaining escalation and documentation standards similar to enterprise helpdesks. It is presented as a set of case studies, reproducible lab notes, knowledge base artifacts, and templates that demonstrate practical helpdesk competency.

> **Objective:** Provide reliable, documented remote IT support (chat/email/ticket) while applying security-aware practices and producing repeatable troubleshooting documentation.

---

## Tools & Technologies
- **Operating Systems:** Windows 10/11, Windows Server (Domain Controller), basic Linux
- **Directory & Accounts:** Active Directory (AD), Office 365 / Microsoft 365 (user provisioning + login support)
- **Ticketing & Collaboration:** ServiceNow / Zendesk style workflows (simulated), Slack, Microsoft Teams, email
- **Troubleshooting Tools:** ipconfig, ping, tracert, nslookup, Event Viewer, PowerShell (Get-ADUser, Reset-ADAccountPassword), printer driver utilities
- **Security / Monitoring:** Basic SOC awareness, phishing detection steps, logs review
- **Documentation & KB:** Markdown, Google Docs, Notion

---

## Key Responsibilities
- Provide chat / email / ticket triage for user account and application access issues.
- Manage Active Directory test environment: user provisioning, password resets, group memberships.
- Troubleshoot connectivity, printer and application issues; escalate as needed.
- Perform accurate data entry and system updates.
- Document solutions and write knowledge base (KB) articles for recurring issues.
- Simulate Tier-1 → Tier-2 handoffs with clear escalation artifacts.

---

## Case Study 1 — Account Setup & Office 365 Access (Typical Ticket)
**Ticket Summary:** New user cannot access Office 365 apps after onboarding.  
**Symptoms:** User receives authentication error when opening Outlook & Teams.  
**Initial Triage (first 10–15 minutes):**
1. Confirm user identity and business email via chat.  
2. Check recent onboarding actions in the HR/client spreadsheet.  
3. Verify account exists in AD: `Get-ADUser -Identity "j.doe"` (PowerShell) or check AD Users console.  
4. Check if account is enabled and not locked.  
5. Ask user to try a web sign-in (https://portal.office.com) and report exact error message.

**Common Causes:** Not yet licensed in Office 365, password expired, MFA not registered, or AD sync delay.

**Resolution Steps (example):**
1. If account disabled → enable account in AD and instruct user to attempt sign-in.  
2. If password expired/locked → reset password in AD and force user to change on next sign-in (communicate temporary password securely).  
3. If MFA not set up → send MFA enrollment steps (clear instructions with screenshots).  
4. Verify license assignment in Office 365 admin and assign if missing.  
5. Confirm user can access Outlook/Teams; create KB: *“Onboarded user cannot access Office 365 — Quick Troubleshooting”*.

**Escalation (if unresolved):**
- Provide Tier-2 with: user email, screenshots of errors, AD user attributes, recent sync logs (AAD Connect status), and steps already done.

**Ticket Closure Note (example):**
> Resolved — user able to sign in to Office 365 web and desktop apps. Root cause: license not assigned. Assigned license, reset password, guided MFA setup. User tested Teams & Outlook — working. KB created and linked to ticket.

---

## Case Study 2 — Password Reset & MFA Troubleshooting
**Scenario:** User locked out after multiple failed attempts and MFA prompts failing.  
**Triage Checklist:**
- Confirm username and organ. unit.
- Check AD lockout status: `Search-ADAccount -LockedOut` or AD Users console.
- Review account last logon and failed logon events in Event Viewer (Windows Security event IDs 4625 / 4740 etc.).
- Verify whether AAD Connect has any sync errors (if hybrid).

**Steps to Resolve:**
1. Unlock account and reset temporary password.  
2. Walk user through MFA verification flow (SMS/app) — provide step-by-step chat instructions.  
3. If MFA app lost → remove existing MFA registration from admin portal and re-provision using secure process.  
4. Document all steps in ticket and note the escalation if suspicious failed logons indicate a security event.

**KB Snippet:**  
**Title:** Resetting a locked AD account and re-enrolling MFA  
**Steps:** 1) Confirm identity 2) Unlock & reset password 3) Re-provision MFA -> verify sign-in.

---

## Case Study 3 — Printer Connectivity & Driver Issues
**Symptoms:** User prints but receives error “printer driver not found” or print jobs stuck in queue.  
**Troubleshooting Steps:**
1. Confirm network connectivity (ping print server, check IP).  
2. Ask for exact error (screenshot or copy/paste).  
3. Clear local print queue & restart Print Spooler: `net stop spooler` → clear %systemroot%\System32\spool\PRINTERS → `net start spooler`.  
4. Reinstall printer driver using vendor installer or use universal driver as fallback.  
5. If network printer, ensure correct DNS resolution & firewall ports open (9100 / 631 etc.).  
6. Final test: test print & confirm.

**Escalation:** If print server issues or driver package policy needed, escalate to server admin with spooler logs and print server event IDs.

---

## Case Study 4 — Software Access / Licensing Issue
**Scenario:** User cannot activate licensed desktop app.  
**Triage:**
1. Confirm license assignment & user’s entitlement.
2. Review activation error codes and vendor KB.
3. If single-sign-on failure, check SSO logs and AD attributes.
4. If license server unreachable, escalate to license admin/ vendor.

**Resolution:** Reassign license in admin console, clear cached credentials, guide user through re-auth; document in KB.

---

## Case Study 5 — Malware Alert (Simulated) & Escalation Process
**Context:** Simulated detection of suspicious process on a client workstation (red-team simulation).  
**Immediate Actions (isolate):**
1. Instruct user to disconnect from network (or isolate machine via endpoint console).  
2. Capture process list, running services, and recent binary path.  
3. Collect relevant logs (Windows Security / Sysmon if available) and a sample list of running processes.  
4. Escalate to incident response (Tier-2/IR) with collected artifacts, timestamps, and user activity.  
5. Document follow-up remediation steps and reimaging if required.

> **Note:** For freelance work, all malware investigations were simulated or coordinated with consent for learning and documentation purposes.

---

## Ticket Handling Workflow (Template)
**Ticket Intake (Chat/Email):** Greeting → Identify user → Confirm urgency → Ask for screenshots → Immediate triage steps.  
**Priority Mapping:** Low (info/requests) / Medium (user impact) / High (service outage / security).  
**Triage Checklist:** reproduce issue, gather logs, advise user of temporary workaround, apply fix or escalate.  
**Escalation Template:**  
- **Subject:** Escalation: [Ticket ID] — [Short summary]  
- **Description:** Steps attempted, logs attached, user impact, urgency, recommended next steps, business owner.  

---

## Knowledge Base (KB) Article — Template
**Title:** Short descriptive title (e.g., “Reset AD Account & Re-enroll MFA”)  
**Symptoms:** One-liner.  
**Pre-requisites:** admin rights, user validation.  
**Resolution Steps:** Numbered steps with screenshots (when possible).  
**Verification:** How to confirm issue resolved.  
**Related KB / Links:** internal references.  
**Tags:** AD, MFA, Office365.

**Example KB excerpt (Markdown):**
```markdown
### Reset AD Account & Re-enroll MFA
**Symptoms:** User cannot sign in and receives MFA prompt errors.
**Resolution:**
1. Validate user identity via [secure checklist].
2. Unlock account in AD and reset temporary password.
3. Instruct user to sign in to `https://portal.office.com` and complete MFA enrollment.
4. Verify successful sign-in to Outlook / Teams.
