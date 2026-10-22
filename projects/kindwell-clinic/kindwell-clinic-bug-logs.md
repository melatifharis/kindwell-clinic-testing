# Kindwell Clinic — Project Task & Defect Tracking Log

This log tracks development tasks, integration issues, and bug resolution cycles managed alongside the engineering team for the Kindwell Clinic web application and Medirecords booking flow.

| ID | Type | Summary / Description | Priority | Status | Target Date | Notes / Resolution |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **KW-01** | TASK | Project Initialization & Environment Setup | Medium | Done | 14/07/2026 | Base repository setup. |
| **KW-02** | TASK | Develop Landing Page & UI Components | High | Done | 15/07/2026 | Pending photo asset revisions. |
| **KW-03** | TASK | Requirements Alignment & Analysis | Medium | Done | 11/08/2026 | Scope review for booking integration. |
| **KW-04** | TASK | Develop Booking Flow & Medirecords Integration | High | Done | 07/09/2026 | Blocked temporarily awaiting Stripe/Add-on confirmation. |
| **KW-05** | BUG | Bug Fix: Form Submission Error & Cron Job sync | High | Done | 10/09/2026 | Resolved payload mapping errors. |
| **KW-06** | ISSUE | Revision Feedback: Dynamic Pricing Adjustments | Medium | Done | 21/09/2026 | Updated Stripe pricing tiers for review consultations. |
| **KW-07** | TASK | Setup Stripe Products & Payment Gateways | Medium | Done | 28/09/2026 | Production payment gateway configuration. |

---

## Detailed Defect Reports (Kindwell Clinic)

### Defect 1: Returning Patients Charged Initial Price Instead of Review Rate
* **ID:** BUG-KW-01
* **Severity:** High
* **Module:** Booking & Payment Flow (Stripe / Medirecords Integration)
* **Description:** When a registered patient with a previous appointment status marked as `Completed` in Medirecords books a follow-up consultation using the same phone/email, the checkout system incorrectly calculates the full Initial Consultation price instead of the discounted Review/Follow-up rate.
* **Steps to Reproduce:**
  1. Access the Kindwell Clinic booking portal.
  2. Input details for a patient with a historical `Completed` appointment in Medirecords.
  3. Select a Review Consultation session type.
  4. Proceed to the Stripe payment screen.
* **Expected Result:** The system queries Medirecords, detects the prior completed appointment, and applies the Review Consultation pricing tier.
* **Actual Result:** The system charges the Initial Consultation fee.
* **Resolution / Verification:** Verified that appointment status must be explicitly synchronized as `Completed` in the Medirecords backend for the discount logic to trigger successfully.

---

### Defect 2: Gender Selection Overwrites Patient Profile Data
* **ID:** BUG-KW-02
* **Severity:** Medium
* **Module:** Patient Information Form / API Payload
* **Description:** Selecting `Female` as the patient gender during booking forces an automatic override to `Male` in the backend payload and replaces the input name with a default dummy record (`Adam Adamson`). Selecting `Males` processes data correctly.
* **Steps to Reproduce:**
  1. Navigate to the patient booking form.
  2. Fill out user details and set **Gender** to **Female**.
  3. Submit the form and inspect the created patient record.
* **Expected Result:** The system creates a patient profile matching the input gender and user-provided name.
* **Actual Result:** The profile defaults to `Male` with the name "Adam Adamson".
* **Resolution:** Investigated payload mapping logic (`titleCode` / gender integer mapping where Female returns 1, Male returns 2) and deployed a fix to align with Medirecords API requirements.

---

### Defect 3: Postcode and City Code Validation Mismatch
* **ID:** BUG-KW-03
* **Severity:** Medium
* **Module:** Address & Shipping Validation
* **Description:** Entering valid Australian cities with certain postcodes triggered a rule validation error (`City Code does not exist for this Postcode`) because the frontend form fields did not dynamically restrict or match Medirecords' strict regional validation rules.
* **Resolution:** Added form input rules and validation handling for Australian phone numbers (`+614` / `04xxx`, numeric, max 10 digits) and coordinated postcode/city alignment.
