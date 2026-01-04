# ZARISH-HIS: TECHNICAL IMPLEMENTATION PLAN FOR DATA VALIDATION
**Author:** Mohammad Ariful ISLAM  
**Contact:** zarishsphere@gmail.com  
**Platform:** ZARISH SPHERE  
**Date:** 04 January 2026  
**Time:** 02:00 PM  

---

## 1. EXECUTIVE SUMMARY

This document outlines the technical strategy for implementing the **ZARISH-HIS** data validation rules using the **HL7 FHIR** (Fast Healthcare Interoperability Resources) standard. FHIR Profiles, specifically **StructureDefinitions**, will be the primary mechanism to enforce the "Gold Standard" data quality defined in `STANDARDIZATION.md`.

## 2. FHIR PROFILING FOR ZARISH-HIS STANDARDS

FHIR allows for the creation of **Profiles** to constrain base resources (like `Patient`, `Observation`, `Encounter`) to meet specific local, national, or project requirements.

### 2.1. Universal Data Rules Enforcement

The following table maps the ZARISH-HIS Universal Data Rules to their corresponding FHIR Profile constraints:

| ZARISH-HIS Rule | FHIR Resource | FHIR Element | Constraint Type | Implementation Detail (StructureDefinition) |
| :--- | :--- | :--- | :--- | :--- |
| **Patient ID Format** (`ZSH-YYYY-XXXXX`) | `Patient` | `Patient.identifier` | Pattern Constraint | Use a **regular expression** (`^ZSH-\d{4}-\d{5}$`) on the `value` element of the identifier with a specific `system` URI. |
| **Phone Numbers** (`+880`) | `ContactPoint` | `ContactPoint.value` | Pattern Constraint | Apply a regex (`^\+880\d{10,12}$`) to enforce the Bangladesh country code and number length. |
| **Mandatory Fields** (Name, Gender, DOB, Status) | `Patient` | `Patient.name`, `Patient.gender`, `Patient.birthDate`, `Patient.extension:status` | Cardinality | Set the minimum cardinality (`min`) to **1** for these elements. |
| **Dates Format** (`DD MMMM YYYY`) | All | All Date/DateTime | Data Type | While FHIR uses ISO 8601, a **custom extension** can be used to enforce the display format, and the system must ensure the underlying data is stored as a valid FHIR `date` or `dateTime`. |

### 2.2. Clinical Workflow Logic Enforcement

| ZARISH-HIS Logic | FHIR Resource | Constraint Type | Implementation Detail (StructureDefinition) |
| :--- | :--- | :--- | :--- |
| **Triage Priority** (Red/Yellow/Green) | `Observation` | Value Set Binding | Create a **ValueSet** (e.g., `ZarishTriagePriority`) and bind it to the `Observation.valueCodeableConcept` element, allowing only the specified codes. |
| **Diagnosis Coding** (ICD-11) | `Condition` | Terminology Binding | Bind the `Condition.code` element to a **CodeSystem** representing the ICD-11 standard, ensuring only valid codes are used. |
| **Orders Linked to Diagnosis** | `ServiceRequest` | Reference Constraint | Set a mandatory reference (`min=1`) from `ServiceRequest.reasonReference` to a `Condition` resource, enforcing the link between the order and the diagnosis. |

## 3. RECOMMENDED TECHNOLOGY STACK

A modern, open-source, and FHIR-native stack is recommended to ensure scalability, interoperability, and compliance.

| Layer | Technology | Rationale |
| :--- | :--- | :--- |
| **Data Standard** | **HL7 FHIR R4/R5** | Global standard for interoperability, supporting all required data models. |
| **Database/Server** | **HAPI FHIR Server** (Java) or **Firely Server** (.NET) | Open-source, robust FHIR implementation with built-in validation engine. |
| **Validation Engine** | **FHIR Validator** (Built-in to HAPI/Firely) | Automatically checks incoming resources against the defined ZARISH-HIS Profiles. |
| **Frontend/UI** | **React/TypeScript** with **FHIR SDKs** | Provides a modern, type-safe interface for data entry, with client-side validation using the same FHIR Profiles. |
| **Deployment** | **Docker/Kubernetes** | Ensures scalability and easy deployment in various environments (e.g., cloud, on-premise, humanitarian field settings). |

## 4. IMPLEMENTATION ARCHITECTURE

The validation process will be implemented at three critical points to ensure data quality:

1.  **Client-Side Validation (Frontend):** The user interface (UI) will use the FHIR Profiles to provide immediate feedback to the user upon data entry (e.g., real-time regex check for the Patient ID format). This prevents unnecessary network traffic and improves user experience.
2.  **Server-Side Validation (FHIR Server):** Every resource submitted to the FHIR server **MUST** be validated against the corresponding ZARISH-HIS Profile before being persisted to the database. If validation fails, the server returns an `OperationOutcome` resource detailing the errors.
3.  **Data Warehouse Validation (ETL/ELT):** A final check can be performed during the Extract, Transform, Load (ETL) process into the HIS data warehouse, ensuring that all data used for reporting and public health analysis (EMR to HIS linkage) is clean and compliant.

## 5. NEXT STEPS

The next phase involves formally defining and publishing the **ZARISH-HIS Implementation Guide (IG)**, which will contain all the necessary FHIR StructureDefinitions, ValueSets, and CodeSystems. This IG will be the single technical reference for all development teams.

---

> "By adopting a FHIR-native approach, ZARISH-HIS ensures that its 'Gold Standard' data quality is not just a policy, but a technically enforced reality, ready for global interoperability."
