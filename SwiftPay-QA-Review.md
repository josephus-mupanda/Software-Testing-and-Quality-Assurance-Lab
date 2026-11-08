# Swift Pay QA Review: "Scan to Pay" (QR)

| | |
|---|---|
| **QA reviewer** | Josephus Mupanda |
| **Date** | 8 November 2026 |
| **Feature** | FS-P2M-v1.0: "Scan to Pay" (QR), version 1.0 |
| **Artifacts reviewed** | Feature specification and UI mock-up (Figma: *Payswift Ambiguity flow (QAs)*) |

---

## Section 1: Positive Test Case

| Field | Details |
|---|---|
| **Test Case ID** | TC-POS-01 |
| **Title** | Successful QR scan and payment to a merchant (QR code without an embedded amount) |
| **Preconditions** | 1. A registered Swift Pay user is logged in and has a 4-digit transaction PIN (1212).<br>2. The wallet balance is GHS 150.00.<br>3. Camera permission is granted and the device is online.<br>4. The merchant "Kofi's Cafe" has a valid QR code with no embedded amount. |
| **Steps** | 1. On the home screen, tap the **Scan** icon.<br>2. Point the camera at Kofi's Cafe's QR code.<br>3. On the Payment Confirmation screen, enter the amount **15.00**.<br>4. Tap **Confirm Payment**.<br>5. Enter the PIN **1212**. |
| **Expected Result** | 1. The camera opens in scan mode (AC-01).<br>2. The QR code is decoded and the Payment Confirmation screen opens with **"Kofi's Cafe"** at the top (AC-02, AC-03).<br>3. The amount is accepted and **Confirm Payment** becomes active (AC-04).<br>4. The user is asked for the 4-digit PIN; the prompt shows the amount **GHS 15.00** and the payee **Kofi's Cafe** (AC-05).<br>5. The payment is processed and a success message shows **GHS 15.00** and **Kofi's Cafe** (AC-06, AC-07). The balance becomes GHS 135.00. |

## Section 2: Negative / Edge Test Case

| Field | Details |
|---|---|
| **Test Case ID** | TC-NEG-01 |
| **Scenario** | The user enters an **incorrect transaction PIN** when paying a merchant by QR code. |
| **Steps** | 1. Tap **Scan** and scan Kofi's Cafe's QR code.<br>2. Enter the amount **15.00** and tap **Confirm Payment**.<br>3. Enter a wrong PIN, **1111** (the correct PIN is 1212). |
| **Expected Result** | 1. The payment is **not** processed and no money is debited (balance stays GHS 150.00).<br>2. A clear error message is displayed, e.g. "Incorrect PIN. Please try again." (AC-08).<br>3. The user is returned to the Payment Confirmation screen (AC-08) with the merchant and the amount **15.00** still filled in, so they can retry. |

## Section 3: Bug Report

| Field | Details |
|---|---|
| **Bug ID** | BUG-001 |
| **Title** | PIN prompt asks the user to authorise a payment to "MTN … Request Service" instead of the scanned merchant (Kofi's Cafe) |
| **Severity** | **Critical**: the user approves the payment with their PIN on a screen that names a different payee and service. Either the user cannot make an informed decision, or the money goes to the wrong recipient. |
| **Priority** | **P1 – High**: must be fixed before development; the PIN screen cannot be built as designed. |
| **Environment** | UI mock-up *Payswift Ambiguity flow (QAs)* in Figma Present mode (Windows 11), page *Prototypes*, frame *Enter pin*, device frame 393 × 852 px · Specification FS-P2M-v1.0 · No app build yet (design stage) |
| **Steps to Reproduce** | 1. Open the prototype in Present mode.<br>2. On the *Send Money* screen, tap **Scan to Pay**.<br>3. Let the scan finish. The Payment Confirmation screen lists **Kofi's Cafe**.<br>4. Enter the amount **15** and tap **Confirm Payment**.<br>5. Read the text of the PIN prompt.<br>(The same happens in the flow where the amount is embedded in the QR code.) |
| **Expected Result** | The PIN prompt shows the same payee and amount as the confirmation screen, e.g. "Pay **GHS 15.00** to **Kofi's Cafe**. Enter your 4-digit PIN.", with **Cancel** and **Pay** buttons. |
| **Actual Result** | The prompt says: "Authorize payment of GHS15 Fee:"GHS0.00" Tax:0 from your account to **MTN** for your **Request Service**. Enter your pin to continue". The payee is **MTN**, not Kofi's Cafe, although the confirmation screen before it and the success screen after it ("Paid to: Kofi's Cafe") both name Kofi's Cafe. The confirm button is also labelled **"Reply"**. |

## Section 4: Process Improvement Suggestion

| Field | Details |
|---|---|
| **What could have been done earlier** | Before the specification was signed off and handed to design, QA should have reviewed it together with the Product Owner and a developer (a "Three Amigos" session). In that review, each acceptance criterion is checked for testability and rewritten as a concrete example, and every screen of the mock-up must match one. The PIN step would then get the criterion that is missing today:<br>*Given I scanned the QR code of "Kofi's Cafe" and entered GHS 15.00,*<br>*When I tap "Confirm Payment",*<br>*Then the PIN prompt shows "Pay GHS 15.00 to Kofi's Cafe" and asks for my 4-digit PIN.* |
| **How it would prevent the issue** | AC-05 today only says "user is prompted to enter 4-digit transaction PIN"; it never says what the prompt must show, so the "MTN … Request Service" text had nothing to fail against. With the criterion above, checking the *Enter pin* screen against it reveals the wrong payee in minutes, at the design stage, before anyone builds it. |
| **Relation to Shift Left Testing** | Shift Left means testing as early as possible in the lifecycle. Reviewing requirements and designs is the earliest form of testing: it needs no code, and a defect found in a sentence of the spec or a text in the mock-up costs minutes to fix. Found after development, the same defect needs code changes, re-testing and a new release; found in production, it can cost real money and customer trust in a payment app. QA moves from finding the defect to preventing it. |
