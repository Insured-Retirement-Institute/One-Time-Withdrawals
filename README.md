
# IRI One-Time-Withdrawals API

## Overview
This repository consolidates three key withdrawal transactions for annuity and retirement products under the **IRI Digital First vision**:

- **Partial Withdrawals**
- **Full Surrender**
- **One-Time RMD (Required Minimum Distribution)**

The initiative modernizes legacy XML/SOAP-based In-Force Transactions (IFT) into RESTful APIs for secure, scalable, and interoperable processing. It leverages industry standards and provides a unified approach for carriers, distributors, and solution providers.

---

## Business Case
### Problem Statement
- Legacy XML/SOAP systems are inefficient, lack modern security, and are nearing end-of-life.
- REST APIs provide real-time, lightweight, and secure data exchange.

### Objectives
- Transition all IFT processing to RESTful API architecture.
- Reduce payload size and processing time.
- Improve integration velocity and security.
- Ensure long-term support and interoperability.

### Key Features
- Modular RESTful APIs with JSON payloads and OAuth 2.0 authentication.
- OpenAPI/Swagger documentation for easy onboarding.
- Accelerated development using validated payload structures.
- Standardized testing framework for early and consistent validation.
- Open contribution to IRI standards for industry-wide adoption.
- OpenAPI 3.x specifications with example payloads and conditional validation.
- Data Dictionary for field-level definitions and code lists.
- Unified endpoint with transactionType routing.

---

## Supported Transactions

### 1. Partial Withdrawals
Handles scenarios where a policyholder withdraws a portion of their funds while keeping the policy active.  
**Folder:** `./partialwithdrawal/`

#### User Stories
- As a Policy Administrator, I want to validate all required fields before submitting a transaction so that I can avoid processing delays.  
- As a System Integrator, I want to map the schema to our internal data model so that we can automate the transaction flow.  
- As a Financial Advisor, I want to confirm the payee’s bank and address details so that I can ensure accurate disbursement.  

#### Personas
**Policy Administrator**  
Goals: Ensure accurate and timely processing of partial withdrawals.  
Needs: Clear schema definitions, validation rules, and integration guidance.  
Pain Points: Manual data entry errors, inconsistent formats, lack of traceability.  

**System Integrator**  
Goals: Implement schema into backend systems and APIs.  
Needs: JSON/XML schema formats, sample payloads, field-level documentation.  
Pain Points: Ambiguous field definitions, missing required attributes.  

**Financial Advisor**  
Goals: Guide clients through partial withdrawal processes.  
Needs: Clear understanding of payment forms, tax implications, and payee details.  
Pain Points: Confusing terminology, paper process.  

---

### 2. Full Surrender
Handles scenarios where a policyholder withdraws the entire balance, effectively terminating the policy.  
**Folder:** `./fullsurrender/`

#### User Stories
- As a Policy Administrator, I want to validate all required fields before submitting a transaction so that I can avoid processing delays.  
- As a System Integrator, I want to map the schema to our internal data model so that we can automate the transaction flow.  
- As a Financial Advisor, I want to confirm the payee’s bank and address details so that I can ensure accurate disbursement.  

#### Personas
**Policy Administrator**  
Goals: Ensure accurate and timely processing of full withdrawals.  
Needs: Clear schema definitions, validation rules, and integration guidance.  
Pain Points: Manual data entry errors, inconsistent formats, lack of traceability.  

**System Integrator**  
Goals: Implement schema into backend systems and APIs.  
Needs: JSON/XML schema formats, sample payloads, field-level documentation.  
Pain Points: Ambiguous field definitions, missing required attributes.  

**Financial Advisor**  
Goals: Guide clients through full withdrawal processes.  
Needs: Clear understanding of payment forms, tax implications, and payee details.  
Pain Points: Confusing terminology, paper process.  

---

### 3. One-Time RMD
Handles scenarios where a policyholder takes a one-time RMD as per regulatory requirements.  
**Folder:** `./onetimermd/`

#### User Stories
- As a Policy Administrator, I want to validate all required fields before submitting a transaction so that I can avoid processing delays.  
- As a System Integrator, I want to map the schema to our internal data model so that we can automate the transaction flow.  
- As a Financial Advisor, I want to confirm the payee’s bank and address details so that I can ensure accurate disbursement.  

#### Personas
**Policy Administrator**  
Goals: Ensure accurate and timely processing of RMD withdrawals.  
Needs: Clear schema definitions, validation rules, and integration guidance.  
Pain Points: Manual data entry errors, inconsistent formats, lack of traceability.  

**System Integrator**  
Goals: Implement schema into backend systems and APIs.  
Needs: JSON/XML schema formats, sample payloads, field-level documentation.  
Pain Points: Ambiguous field definitions, missing required attributes.  

**Financial Advisor**  
Goals: Guide clients through RMD withdrawal processes.  
Needs: Clear understanding of payment forms, tax implications, and payee details.  
Pain Points: Confusing terminology, paper process.  

---

## Schema Overview
Sample of what most schemas includes (one-time-rmd would differ from partial-withdrawal and full-surrender:
- **Root Attributes:** correlationId , effectiveDate, isOverride, associatedFirmId, nsccParticipantId, allocationOption (for partial withdrawals)
- **Producer Info:** producerNumber, npn, crdNumber.
- **Transaction Amounts:** amountType (AMOUNT/PERCENTAGE), disbursementType (GROSS/NET), disbursementPaymentForm.
- **Payee Details:** partyId, paymentForm, bank, address (modeled via payeeOrBeneficiary[]).
- **Parties:** parties[] as a direct array of party objects.
- **Fund Distributions:** fundDistributions[] with fundId, fundName, amounts/percentages, optional fundDistributionSegment.
- **Tax Withholding Instructions:** taxWithholdingType, taxRateToUse, taxJurisdiction, filingStatus, percentage/dollar, associated party.
- **Charges:** chargeType, chargeWaiverIndicator, chargeWaiverReason.
- **RMD Info:** rmdTaxYear, rmdRequestedAmount, rmdCalculationMethod, rmdPriorYearEndValue, optional rmdSpouseDoB.

Detailed schemas for each transaction are available in their respective folders.

---

# Error Schema Overview

All API operations—across synchronous and asynchronous processing models—adhere to a unified **Error schema**. This ensures consistent error handling, predictable integration behavior, and standardized troubleshooting across all transaction types.

## Success Response Expectations

### Synchronous APIs
- Return **HTTP 200** for successful, completed processing.

### Asynchronous APIs
- Return **HTTP 202** to acknowledge the request has been accepted for processing but not yet completed.

---

## Standard Error Schema
Every error response—regardless of transaction type—includes:
- An HTTP status code in the **400–599** range
- A structured and validated **error code**
- A **timestamp** of when the error was generated
- A developer‑focused **technical message** (`message`)
- A safe, user‑friendly **userMessage**
- A **correlationId** for cross‑system tracing
- Optional **field‑level** or **rule‑level** error collections

---

## Key Fields

| Field | Description |
|-------|-------------|
| **httpStatus** | Numeric HTTP status code (400–599) representing the type and severity of the failure. |
| **code** | Structured identifier in the enforced format: `domain.category.subcategory`. Enables machine‑readable error handling. |
| **message** | Technical diagnostic detail for developers, logs, or support teams. |
| **userMessage** | End‑user‑friendly explanation, safe to show in portals or consumer‑facing apps. |
| **correlationId** | Carries forward the inbound request’s correlation ID header to enable end‑to‑end traceability. |
| **validationErrors** (optional) | Array describing field‑level validation issues (e.g., missing required fields, incorrect formats). |
| **businessErrors** (optional) | Array describing domain/business rule violations; each entry requires its own code and message. |

---

## Purpose & Benefits
This standardized error structure ensures:
- A **predictable experience** across all APIs (synchronous + asynchronous)
- Clear differentiation between **developer diagnostics** and **user‑safe messages**
- Enhanced **traceability** for carriers, distributors, and integrators
- Support for granular **validation feedback** and complex business rule logic
- Easier **monitoring, logging, and cross‑system troubleshooting**

---

## OpenAPI Specs
Unified Swagger documentation for all endpoints is available in the `openapi-specs/` folder.

---

## Change Submissions and Reporting Issues

- Issues and bugs can be reported directly within the **Issues** tab of this repository.
- **Security issues** should be reported directly to Katherine Dease at **kdease@irionline.org**.
- Change requests should follow the **standards governance workflow** outlined on the main page.

---
## Versioning ##
- Follow semantic versioning for spec updates.
- Document changes in commit messages and changelogs to support integrator adoption.
---

## Code of Conduct

Please review and adhere to the **Code of Conduct** and **Style Guide** provided in the repository to ensure consistency and professionalism.

---

## How to Contribute

- Fork the repo and submit pull requests.
- Report issues via the **Issues** tab.
- Join working groups: **hpikus@irionline.org**.

---

## Business Owners

- **Carrier Business Owner:** digitalfirst@brighthousefinancial.com  
- **Distributor Business Owner:** [contact]  
- **Solution Provider Business Owner:** [contact]  
