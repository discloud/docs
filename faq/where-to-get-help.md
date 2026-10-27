---
description: >-
  Channels and best practices for getting help with Discloud: community forums,
  chat, donor areas, and direct staff support.
icon: bullseye-arrow
---

# Where to Get Help

## 🧾 Overview

Multiple support surfaces exist depending on what you need: community troubleshooting, platform usage questions, billing / account issues, or private escalation. This page explains where to post and how to ask effectively.

{% hint style="info" %}
Staff focuses on Discloud platform issues (deployment, hosting behavior, account, billing). General coding questions are community-driven.
{% endhint %}

***

## 🗂️ Support Channels

| Channel                                                                                         | Type                      | Audience        | Typical Use                                       |
| ----------------------------------------------------------------------------------------------- | ------------------------- | --------------- | ------------------------------------------------- |
| [Modmail Ticket (Direct)](https://discord.com/channels/@me/930852077045940224/)                 | Private                   | You ↔ Staff     | Billing, account, sensitive data, policy concerns |
| [english-chat](https://discord.com/channels/584490943034425391/1051124538995392573)             | Public chat               | All users       | Quick platform questions, light discussion        |
| [dev-help-english (Forum)](https://discord.com/channels/584490943034425391/1350912554733539418) | Public threaded           | All users       | Community help with code / configs                |
| [donators-chat](https://discord.com/channels/584490943034425391/1051124971763679232)            | Public (donor‑restricted) | Paid plan users | Donor community discussion                        |
| [donators-support (Forum)](https://discord.com/channels/584490943034425391/1051124971763679232) | Public (donor‑restricted) | Paid plan users | Plan-related technical questions                  |
| [Documentation](https://docs.discloud.com/en)                                                   | Self-serve                | Everyone        | Official guides & references                      |

***

## 🎫 Modmail (Direct Staff Ticket)

Use modmail for issues that should not be public:

* Billing or subscription management
* Account-specific errors (suspensions, access anomalies)
* Security or abuse reports
* Sensitive logs / PII that must stay private

{% stepper %}
{% step %}
Open a DM with [Discloud’s Modmail](https://discord.com/channels/@me/930852077045940224/) to start a ticket.
{% endstep %}

{% step %}
Provide concise summary: issue type + affected app ID / plan.
{% endstep %}

{% step %}
Attach relevant (non-sensitive) logs or screenshots.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Do not send raw tokens, API keys, or full environment variable dumps in tickets. Redact secrets before attaching.
{% endhint %}

***

## 🤝 Community Forum: dev-help-english

Peer-to-peer Q\&A. Staff may occasionally reply, but responses are not guaranteed.

### ✅ Post Effectively

<table><thead><tr><th width="300">Element</th><th>Why It Matters</th></tr></thead><tbody><tr><td>Clear goal</td><td>Helps others understand desired outcome</td></tr><tr><td>Repro steps</td><td>Enables validation and reproduction</td></tr><tr><td>Error snippet</td><td>Focuses attention (paste minimal portion)</td></tr><tr><td>Environment basics</td><td>Language, runtime version, plan tier (if relevant)</td></tr><tr><td>What you tried</td><td>Avoids duplicate suggestions</td></tr></tbody></table>

### 🚫 Avoid

<table><thead><tr><th width="300">Pitfall</th><th>Better Approach</th></tr></thead><tbody><tr><td>Vague: "Doesn't work"</td><td>Describe expected vs actual result</td></tr><tr><td>Huge unformatted logs</td><td>Provide relevant lines</td></tr><tr><td>Off-topic platform comparisons</td><td>Keep scope to resolving your issue</td></tr><tr><td>Irrelevant multi-language tags</td><td>Only tag technologies actually used</td></tr></tbody></table>

{% hint style="success" %}
Search existing threads first, your answer may already exist.
{% endhint %}

***

## 🔐 Protect Sensitive Data

Never publicly share:

| Data Type         | Example                                        |
| ----------------- | ---------------------------------------------- |
| Tokens / API Keys | Bot token, service keys                        |
| Passwords         | Database / dashboard credentials               |
| Private URLs      | Internal callback endpoints containing secrets |
| Personal Info     | Email, billing identifiers                     |

Use placeholders: `YOUR_TOKEN_HERE`, `example-db-host`.

{% hint style="danger" %}
If you accidentally leaked a credential, revoke / rotate it immediately and notify staff if risk extends beyond your account.
{% endhint %}

***

## 📚 Learn & Upskill

Recommended free learning partners / content:

{% tabs %}
{% tab title="JavaScript" %}
{% embed url="https://www.youtube.com/watch?list=PL9tY_tDo_Q0C0hs1aGgtJbEH1EBlyzZdG&v=lQAJ-T1QTYc" %}
{% endtab %}

{% tab title="TypeScript" %}
{% embed url="https://www.youtube.com/watch?list=PL9tY_tDo_Q0DOAzTaPnWYsryfNLsz1K6U&v=4pIo-p6pX34" %}
{% endtab %}
{% endtabs %}

***

## 🚀 Before Asking, Check

| Item                                                                                     | Why                                  |
| ---------------------------------------------------------------------------------------- | ------------------------------------ |
| Checked the docs?                                                                        | Feature may already be documented    |
| Recent changelog / announcements                                                         | Behavior could be intentional change |
| Existing [FAQ](general-questions/) / [troubleshooting](troubleshooting-solutions/) pages | Common answers covered               |
| [Plan limits](https://discloud.com/plans)                                                | Some errors are quota-related        |
