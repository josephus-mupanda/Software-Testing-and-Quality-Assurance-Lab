# Quality Review for "Swift Pay"

---

## Overview

This capstone requires learners to apply skills from across the module to a realistic feature review.

### Scenario

A fictional Ghanaian fintech startup, **Swift Pay**, is adding a **"Scan to Pay" QR code** feature to its mobile app.

### Artifacts

A one-page feature specification with:

- Acceptance criteria
- UI mockup of the feature [the Figma file](https://www.figma.com/design/vNUbDzjQUDSgwrI9woam1g/Payswift-Ambiguity-flow--QAs-?node-id=11-17613&p=f). Click on the 'Present' icon on far top right corner to start testing.

The artifacts intentionally contain ambiguities and potential issues.

---

## Task Requirements

Learners must complete a structured **QA Review Template** containing the following:

### 1. Positive Test Case

Write one **happy path** test case to verify the core functionality.

**Example:**

- Successful QR scan and payment completion

### 2. Negative / Edge Case Test Case

Write one test case for an unexpected scenario.

**Examples:**

- Scanning an invalid QR code
- Network failure during transaction
- Incorrect transaction PIN

### 3. Bug Report

Identify a potential bug from:

- An ambiguity in the specification, **OR**
- A flaw in the UI mockup

Write a complete bug report for the issue.

### 4. Process Improvement Suggestion

From your specialization's viewpoint, suggest one action the **Swift Pay** team could have taken earlier to prevent the issue.

This reinforces the **Shift Left Testing** mindset.

---

## Feature Specification

### Document Information

| Field | Value |
|-------|-------|
| Document Title | FS-P2M-v1.0: "Scan to Pay" (QR) |
| Date | 2025-10-16 |
| Version | 1.0 |
| Author | Product Team |

---

## 1. Feature Name

**"Scan to Pay"**

---

## 2. User Story

As a Swift Pay user, I want to scan a merchant's QR code, so that I can pay for goods and services quickly and securely without needing cash.

---

## 3. Feature Description

This feature allows a registered Swift Pay user to initiate a payment to a merchant by scanning a QR code using their smartphone camera from within the Swift Pay app.

### Flow

1. User scans merchant QR code
2. User enters payment amount (if amount is not embedded)
3. User confirms transaction
4. User enters PIN
5. Transaction is processed

---

## 4. Out of Scope

The following are **NOT** included in this feature:

- **Generating QR codes for merchants** — handled by the Merchant App team
- **Peer-to-Peer (P2P) QR payments** — this feature supports only Peer-to-Merchant (P2M)

---

## 5. Acceptance Criteria (AC)

| ID | User Action | System Response |
|----|-------------|----------------|
| AC-01 | User taps the "Scan" icon from the app home screen | The app opens the phone camera in scan mode |
| AC-02 | User points camera at a valid merchant QR code | System decodes QR code and navigates to Payment Confirmation screen |
| AC-03 | On the Payment Confirmation screen | Merchant name (e.g., "Kofi's Cafe") is displayed at the top |
| AC-04 | User enters amount to pay | User can input amount and "Confirm Payment" button becomes active |
| AC-05 | User taps "Confirm Payment" | User is prompted to enter 4-digit transaction PIN |
| AC-06 | User enters correct PIN | Transaction is processed quickly |
| AC-07 | Upon successful transaction | Success message appears showing amount and merchant name |
| AC-08 | Upon failed transaction (e.g., incorrect PIN) | Error message displayed and user returned to confirmation screen |
| AC-09 | QR code contains embedded amount | User cannot edit the amount |

---

## QA Review Submission Requirement

Use the provided **Swift Pay QA Review Template.docx** to submit your final review.

---

## Suggested Structure for Your Submission

### Section 1: Positive Test Case

- Test Case ID
- Title
- Preconditions
- Steps
- Expected Result

### Section 2: Negative / Edge Test Case

- Test Case ID
- Scenario
- Steps
- Expected Result

### Section 3: Bug Report

Include:

- Bug ID
- Title
- Severity
- Priority
- Environment
- Steps to Reproduce
- Expected Result
- Actual Result

### Section 4: Process Improvement Suggestion

Explain:

- What could have been done earlier
- How it would prevent the issue
- Relation to Shift Left Testing

---

## End of Lab

Good luck! Focus on:

- Clear test scenarios
- Accurate bug reporting
- Strong QA reasoning
- Real-world testing practices