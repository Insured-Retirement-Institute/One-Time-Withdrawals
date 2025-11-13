# Full Withdrawals Attribute Specification

This document outlines the modernization of full withdrawal (full surrender) transactions in the annuity and retirement industry. The initiative transitions legacy XML/SOAP-based In-Force Transactions (IFT) to RESTful APIs, enabling secure, scalable, and interoperable processing. The approach leverages industry standards and aligns with the IRI Digital First vision.

## Get started
Steps to Begin:

1. Review the Business Case: Understand the rationale for moving from XML/SOAP to RESTful APIs.
2. Familiarize with the Data Model: Examine the required schema for full withdrawal transactions.
3. Access API Documentation: Use OpenAPI/Swagger specs for endpoints, payloads, and integration guides.
4. Set Up Testing: Utilize the standardized Swagger-based testing environment with sample payloads.
5. Collaborate: Engage with working group firms and contribute to the IRI API standards repository.

## Business Case

Problem Statement:

- Legacy XML/SOAP systems are end-of-life, inefficient, and lack modern security.
- REST APIs offer real-time, lightweight, and secure data exchange.


Objectives:

- Transition all IFT processing to RESTful API architecture.
- Reduce payload size and processing time.
- Improve integration velocity and security.
- Ensure long-term support and interoperability.


Key Features:

- Modular RESTful APIs with JSON payloads and OAuth 2.0 authentication.
- OpenAPI/Swagger documentation for easy onboarding.
- Accelerated development using validated payload structures.
- Open contribution to IRI standards for industry-wide adoption.
- Standardized testing framework for early and consistent validation.

## User Stories, personna - supporting documents for the business case
- As a Policy Administrator, I want to validate all required fields before submitting a transaction so that I can avoid processing delays.
- As a System Integrator, I want to map the schema to our internal data model so that we can automate the transaction flow.
- As a Compliance Analyst, I want to extract tax jurisdiction and exemption data so that I can verify regulatory compliance.
- As a Financial Advisor, I want to confirm the payee’s bank and address details so that I can ensure accurate disbursement.

1. Policy Administrator

- Goals: Ensure accurate and timely processing of partial withdrawals.
- Needs: Clear schema definitions, validation rules, and integration guidance.
- Pain Points: Manual data entry errors, inconsistent formats, lack of traceability.

2. System Integrator

- Goals: Implement schema into backend systems and APIs.
- Needs: JSON/XML schema formats, sample payloads, field-level documentation.
- Pain Points: Ambiguous field definitions, missing required attributes.

3. Compliance Analyst

- Goals: Ensure transactions meet regulatory standards.
- Needs: Audit trails, jurisdictional tax details, exemption tracking.
- Pain Points: Incomplete data, lack of standardization.

4. Financial Advisor

- Goals: Guide clients through a full withdrawal processes.
- Needs: Clear understanding of payment forms, tax implications, and payee details.
- Pain Points: Confusing terminology, paper process.

## Schema Overview
The schema for full withdrawal transactions is defined in the data model and includes the following key components:
Root Attributes

- correlationId: Unique transaction ID (string, required)
- effectiveDate: Transaction date (string, required, format: yyyy-mm-dd)
- reverseInitiator: Indicates reversal source (boolean, optional)
- override: Rule override flag (boolean, optional)

Tax Withholding Instructions

- party: Payee/beneficiary details (ID, name, organization)
- taxWithholdingType: Type of tax withholding (string, required)
- taxRateToUse: Payment mode for tax withholding (string, required)
- dollar/percentage/exemptions: Requested values (optional)
- taxJurisdiction: Jurisdiction for tax purposes (optional)

Payee/Beneficiary Details

- partyId, firstName, lastName, organizationName: Identification fields
- paymentForm: Type of payment (string, optional)
- allocationPercent: Allocation percentage (number, optional)
- bank: Bank details (account number, routing number, etc.)
- address: Physical/mailing address details

Parties

- partyRole, partyId, firstName, lastName, organizationName
- paymentForm, allocationPercentage
- bank, address: Financial and contact details

Charges

- chargeType, chargeWaiverIndicator, chargeWaiverReason

Producer

- producerNumber, npn, crdNumber, associatedFirmId, NSCCparticipantID

Transaction Amounts

- amountType, disbursementType, disbursementPaymentForm

## Business Owners 
- Carrier Business Owner: digitalfirst@brighthousefinancial.com
- Distributor Business Owner: contact
- Solution Provider Business Owner: contact

## How to engage, contribute, and give feedback
- These working groups are occuring on ....
- Please contact the business owners or IRI (hpikus@irionline.org) to get added to the working group discussions. 

## Change subsmissions and reporting issues and bugs

Security issues and bugs should be reported directly to Katherine Dease kdease@irionline.org. Issues and bugs can be reported directly within the issues tab of a repository. Change requests should follow the standards governance workflow outlined on the [main page](https://github.com/Insured-Retirement-Institute).

## Code of conduct

See [style guide](https://github.com/Insured-Retirement-Institute/Style-Guide)
