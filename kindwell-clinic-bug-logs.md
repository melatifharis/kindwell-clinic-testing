# Bug Logs

### Defect Report Example 1: Business Logic / API Integration Bug

| Field | Details |
| --- | --- |
| **Bug ID** | DEF-KW-001 |
| **Project** | Kindwell Clinic (Medirecords Integration)

 |
| **Severity / Priority** | High / High |
| **Environment** | Staging / Web Browser |
| **Module** | Booking & Stripe Payment Flow

 |
| **Title** | Returning Patients with Completed Appointments Incorrectly Charged Initial Consultation Price |

#### **Description**

When a registered patient with a previous appointment status marked as `Completed` in Medirecords books a follow-up consultation using the same email and phone number, the checkout system incorrectly charges the full Initial Consultation price instead of the discounted Review Consultation rate.

#### **Pre-conditions**

1. Patient has a registered account and at least one prior appointment with a status explicitly set to `Completed` in the Medirecords backend.


2. User is attempting to book a Review Consultation/Follow-up of the exact same consultation type.



#### **Steps to Reproduce**

1. Navigate to the Kindwell Clinic booking portal.
2. Enter the details of a patient who has a historical `Completed` appointment.
3. Select a Review Consultation / Follow-up session type.


4. Proceed to the checkout/Stripe payment screen and review the pricing breakdown.

#### **Expected Result**

The system should query Medirecords, recognize the prior completed appointment, and apply the correct **Review Consultation pricing tier** at checkout.

#### **Actual Result**

The payment gateway calculates and charges the **Initial Consultation fee**, ignoring the patient's history.

---

### Defect Report Example 2: Data Payload / Mapping Bug

| Field | Details |
| --- | --- |
| **Bug ID** | DEF-KW-002 |
| **Project** | Kindwell Clinic (Medirecords Integration)

 |
| **Severity / Priority** | Medium / High |
| **Environment** | Staging / Web Browser |
| **Module** | Patient Registration Form / API Payload

 |
| **Title** | Selecting "Female" Gender Overwrites Patient Profile Data with Default Dummy Record |

#### **Description**

When filling out the booking form and selecting `Female` for the patient gender, the backend payload mapping or Medirecords API response forces a gender override to `Male` and automatically replaces the input name with a default dummy record (`Adam Adamson`). Selecting `Males` processes data correctly.

#### **Pre-conditions**

User is on the patient information form during the booking flow.

#### **Steps to Reproduce**

1. Access the Kindwell booking flow and fill out patient details.
2. Set the **Gender** dropdown field to **Female**.


3. Complete the form submission and check the created patient record in the database or Medirecords dashboard.

#### **Expected Result**

The system should successfully capture and create a patient profile corresponding to the input gender and user-provided name details.

#### **Actual Result**

The patient gender defaults to `Male` and the name is automatically overwritten with the system default value (`Adam Adamson`).

---

### 💡 Portfolio Presentation Tips:

* **Add Evidence:** In a real portfolio, attach screenshots or short screen recordings (GIFs) showing the step-by-step reproduction of the bug.
* **Highlight Impact:** Emphasize *why* the bug matters (e.g., *"Prevented incorrect patient billing charges"* or *"Ensured data integrity for medical record synchronization"*).
