# kindwell-clinic-testing
Manual QA testing for Kindwell Clinic AU

# 🏥 End-to-End QA Testing: Medicare Intake Form & MediRecords Integration

> **Employer:** Milkyano Creative Media  
> **Client:** Kindwell Clinic  
> **Integrated Systems:** MediRecords EHR API, Stripe Payment Gateway  
> **Role:** QA Engineering Intern  
> **Testing Type:** Manual Functional Testing, API Inspection, Cross-Browser Testing  

## 🛠️ Project Ecosystem

`Milkyano Creative Media` (Agency)  
  └── Built & Tested for ➔ `Kindwell Clinic` (Client)  
        └── Integrates via API ➔ `MediRecords` (EHR Backend) & `Stripe` (Payment Gateway)

---

## Summary
This case study covers end-to-end quality assurance for Kindwell Clinic's digital patient application form. The application captures patient demographic details, validates Australian valid address and Medicare information, syncs records into MediRecords EHR, and processes payment authorizations via Stripe.

### Primary Objectives:
- Guarantee 100% data fidelity between frontend inputs and MediRecords API payloads.
- Enforce strict Australian Medicare format and checksum rules before submission.
- Ensure zero exposure of sensitive Patient Health Information (PHI) or credit card details (PCI compliance) in client-side logs.

---

## Key QA Methodologies & Focus Areas

### 1. DevTools Network Payload Inspection
- Monitored HTTP requests (`POST /api/v1/patients/sync`) in **Chrome DevTools Network Tab**.
- Validated request payload schemas to ensure exact mapping of fields (`medicareNumber`, `irn`, `dob`, `address`).
- Verified HTTP status codes (`200 OK`, `400 Bad Request`, `402 Payment Required`, `500 Internal Error`).
- Ensured proper user-facing error banners were rendered when API endpoints timed out or returned errors.

### 2. Boundary Value Analysis (BVA) & Validation
- **Medicare Card Numbers:** Tested 10-digit base lengths, invalid character inputs, and edge cases.
- **Individual Reference Number (IRN):** Applied boundary rules ($1 \le \text{IRN} \le 9$) to catch off-by-one bugs.
- **Age / DOB Validation:** Enforced valid patient age ranges and handled future date boundary checks.

### 3. Integration & Security Testing
- **MediRecords Endpoint:** Verified duplicate patient record detection to prevent double-entry creation in EHR.
- **Stripe Sandbox:** Tested test credit cards (declined, insufficient funds, successful tokenization) ensuring raw card details never hit backend logs.

---

## Key Artifacts & Documentation
[coming soon]

---

## Tools & Tech Stack
`Chrome DevTools`
