# Quality Assurance test plan:

**Intern Name:** Melati F.H
**Supervisor Name:** Michael S.
**Testing duration til deadline:** 2 weeks

# The criteria needed for success:
- Appropriate pricing for different patient types
- Valid Australian phone number
- Valid Australian address, complete with zip code
- Smooth payment experience through Stripe API

# Workflow:
```mermaid
flowchart TD
    %% Entry Point
    Start([Click 'Book Now']) --> ServiceChoice{Select Service Category}

    %% Branch 1: Alternative Medicine
    ServiceChoice -->|Alternative Medicine| AltMedFlow[Contact Info: Mobile & Email]
    AltMedFlow --> ConsultationType{Select Consultation Type}
    ConsultationType -->|Online| PatientCheck
    ConsultationType -->|In-Person| PatientCheck

    %% Branch 2: Smoking Cessation
    ServiceChoice -->|Smoking Cessation| SmokeCessationFlow[Contact Info: Mobile & Email]
    SmokeCessationFlow -->|In-Person Only| PatientCheck

    %% Patient Eligibility Check
    PatientCheck{Returning Patient?} -->|Yes| FastTrack[Fast-Track Booking]
    PatientCheck -->|No / New Patient| DoctorSelection[Display Available Doctors]

    %% Patient & Contact Details
    DoctorSelection --> SelectDoctor[Choose Practitioner]
    FastTrack --> SelectDoctor
    SelectDoctor --> PersonalDetails[Input Name, Gender & Honorifics]
    PersonalDetails --> AddressValidation[Input Australian Address, State & Postcode]
    AddressValidation --> EmergencyContact[Input Emergency Contact: Name, Relationship & Phone]

    %% Medicare Verification
    EmergencyContact --> MedicareInput[Input Medicare Card Number]
    MedicareInput --> MedicareRebate{Verify Medicare Rebate Eligibility}
    
    %% Checkout & Stripe Integration
    MedicareRebate --> PaymentPage[Display Checkout Page: 15-Min Session Limit]
    PaymentPage --> StripeGateway[Process Payment via Stripe]
    StripeGateway --> Confirmation([Booking Confirmed])
```
