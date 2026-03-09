# CAPTCHA Activation Rules

## Overview

This document explains the rules used by the system to determine when a CAPTCHA challenge is displayed.  
It is intended for **non-developer technical specialists**, including:

- QA engineers
- Support teams
- Product analysts
- Operations staff

Understanding these rules helps teams:

- Investigate unexpected CAPTCHA behavior
- Diagnose user complaints
- Monitor potential abuse or automated attacks
- Verify whether CAPTCHA triggers are functioning correctly

---

## What is CAPTCHA?

CAPTCHA is a **challenge-response security mechanism** designed to distinguish human users from automated scripts or bots.

Because CAPTCHA can interrupt the user experience and reduce user retention, the system displays it **only when specific risk conditions are detected**.

[Placeholder: Link to "CAPTCHA Fundamentals"]

---

## CAPTCHA Trigger Conditions (Summary)

The following table summarizes all rules that may trigger a CAPTCHA challenge.

| Rule | Condition | Threshold | Purpose |
|-----|-----|-----|-----|
| High request volume | Requests from a single IP within a short time window | >500 requests in 20 minutes | Prevent request flooding |
| Blacklisted IP | Request originates from a blocked IP | Immediate | Block known malicious sources |
| Traffic spike detection | Traffic significantly exceeds historical baseline | >2× average requests for the same hour over the last 14 days | Detect abnormal activity |
| Repeated payload submission | Identical payload sent multiple times | >5 times within 30 seconds | Prevent automated form abuse |
| Manual activation | CAPTCHA enabled by administrators | Configurable | Incident response and manual control |

If **any rule is satisfied**, the system displays a CAPTCHA challenge.

---

## Rule Details

### 1. High Request Volume from a Single IP

A CAPTCHA is triggered when:

- More than **500 requests**
- Are received from the **same IP address**
- Within a **20-minute time window**

This rule helps prevent automated request flooding from a single source.

**Example**

A bot repeatedly submits a form hundreds of times in a short period.

---

### 2. Blacklisted IP Address

If a request originates from an IP address that is included in the **internal blacklist**, the system immediately triggers a CAPTCHA challenge.

This rule helps block traffic from **known malicious or abusive sources**.

[Placeholder: Link to "Managing the IP Blacklist"]

---

### 3. Traffic Spike Detection

The system monitors request patterns based on historical traffic.

A CAPTCHA is triggered when:

- The number of requests in the **current hour**
- Exceeds **twice the average number of requests**
- Observed during the same hour over the **previous 14 days**

This rule helps detect **abnormal spikes in activity**, which may indicate automated scanning or large-scale attacks.

[Placeholder: Chart showing baseline vs. current traffic]

---

### 4. Repeated Identical Payloads

A CAPTCHA is triggered when:

- The **same request payload**
- Is received **more than 5 times**
- Within a **30-second window**

This rule helps prevent automated repeated submissions.

**Example**

A script attempts to brute-force a form by sending identical data multiple times.

---

### 5. Manual CAPTCHA Activation

Administrators can manually enable CAPTCHA through the **admin panel** for specific request types or endpoints.

This feature is typically used during:

- Security incidents
- Suspicious traffic spikes
- Temporary protective measures

[Placeholder: Admin panel screenshot]

---

## Rule Evaluation Logic

CAPTCHA rules are evaluated **independently** for each incoming request.

If **any rule condition is satisfied**, the system immediately triggers a CAPTCHA challenge.

Rules are designed to detect different types of suspicious behavior, including:

- High request frequency
- Known malicious sources
- Abnormal traffic spikes
- Automated repeated submissions

---

## Troubleshooting Unexpected CAPTCHA

If users report unexpected CAPTCHA challenges, verify the following:

1. **Check request volume**
   - Confirm whether the IP exceeded the request threshold.

2. **Inspect the IP blacklist**
   - Verify whether the user's IP address is listed.

3. **Review traffic metrics**
   - Determine whether the current traffic exceeds the historical baseline.

4. **Check payload duplication**
   - Identify repeated identical requests within short intervals.

5. **Review admin panel settings**
   - Confirm whether CAPTCHA was manually enabled.

---

## Decision Flow

The following diagram illustrates how the system evaluates CAPTCHA conditions.

[Placeholder: CAPTCHA evaluation flow diagram]

---

## Related Documentation

- CAPTCHA configuration
- Managing the IP blacklist
- Monitoring traffic spikes
- Admin panel security settings