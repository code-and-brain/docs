# ZARISH-HIS IMPLEMENTATION GUIDE (IG)
**Author:** Mohammad Ariful ISLAM  
**Contact:** zarishsphere@gmail.com  
**Platform:** ZARISH SPHERE  
**Date:** 04 January 2026  
**Time:** 03:00 PM  

---

## 1. INTRODUCTION

This **ZARISH-HIS Implementation Guide (IG)** serves as the definitive technical reference for all developers and system integrators working on the ZARISH SPHERE platform. It formalizes the data validation and interoperability requirements using the **HL7 FHIR R4** standard, ensuring compliance with the **ZARISH-HIS Gold Standard** documentation.

## 2. FHIR PROFILES (StructureDefinitions)

FHIR Profiles are used to constrain base FHIR resources to meet the specific needs of ZARISH-HIS.

### 2.1. ZarishPatient Profile

| Element | Constraint | Details |
| :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/StructureDefinition/ZarishPatient` | **Base Resource:** `Patient` |
| **Identifier** | **Mandatory** | Must include the unique ZARISH-HIS Patient ID. |
| **ID Format** | **Regex Pattern** | `^ZSH-\d{4}-\d{5}$` (e.g., ZSH-2026-00001) |
| **Mandatory Fields** | **Cardinality 1..1** | `name`, `gender`, `birthDate` |
| **Phone Number** | **Regex Pattern** | `^\+880\d{10,12}$` (Enforces Bangladesh country code) |
| **Status** | **Mandatory Extension** | `Patient.extension:status` bound to `ZarishPatientStatusVS` |

### 2.2. ZarishTriageVitals Profile

| Element | Constraint | Details |
| :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/StructureDefinition/ZarishTriageVitals` | **Base Resource:** `Observation` |
| **Temperature** | **Range Constraint** | `34.0` to `42.0` (unit: `Cel`) |
| **SpO2** | **Range Constraint** | `50` to `100` (unit: `%`) |
| **Triage Priority** | **Mandatory Extension** | `Observation.extension:triage` bound to `ZarishTriagePriorityVS` |

## 3. FHIR TERMINOLOGY (CodeSystems and ValueSets)

Controlled vocabularies ensure consistent data entry and reporting.

### 3.1. Triage Priority

| Resource | URL | Purpose |
| :--- | :--- | :--- |
| **CodeSystem** | `http://zarishsphere.org/fhir/CodeSystem/ZarishTriagePriorityCS` | Defines codes: `red`, `yellow`, `green` |
| **ValueSet** | `http://zarishsphere.org/fhir/ValueSet/ZarishTriagePriorityVS` | Used to constrain the Triage Vitals Profile. |

### 3.2. Patient Status

| Resource | URL | Purpose |
| :--- | :--- | :--- |
| **CodeSystem** | `http://zarishsphere.org/fhir/CodeSystem/ZarishPatientStatusCS` | Defines codes: `refugee`, `resident`, `staff`, `other` |
| **ValueSet** | `http://zarishsphere.org/fhir/ValueSet/ZarishPatientStatusVS` | Used to constrain the ZarishPatient Profile. |

### 3.3. Diagnosis Coding

| Standard | FHIR Resource | Constraint |
| :--- | :--- | :--- |
| **ICD-11** | `Condition.code` | **Required** binding to the official ICD-11 CodeSystem. |

## 4. WORKFLOW AND INTEROPERABILITY

### 4.1. Clinical Workflow Validation

The core clinical workflow logic is enforced through FHIR resource relationships:

| Workflow Step | FHIR Resource | Constraint |
| :--- | :--- | :--- |
| **Orders Linked to Diagnosis** | `ServiceRequest` | **Mandatory Reference** (`reasonReference`) to a `Condition` resource. |
| **Medication Orders** | `MedicationRequest` | **Mandatory Reference** (`subject`) to a `ZarishPatient` resource. |

### 4.2. System Linkages (EMR-EHR-HIS)

All data exchange between the EMR, EHR, and HIS components **MUST** use the FHIR resources constrained by this Implementation Guide. This ensures that all data aggregated for the HIS (reporting) is validated at the source (EMR).

## 5. NEXT STEPS FOR DEVELOPMENT TEAMS

1.  **Download and Implement:** Developers must download the FHIR artifacts (StructureDefinitions, ValueSets) and integrate them into their client-side and server-side validation logic.
2.  **Testing:** All data submission endpoints must be tested against the FHIR Validator using the profiles defined in this IG.
3.  **Maintenance:** This IG will be versioned and maintained as ZARISH-HIS evolves.

---

> "This Implementation Guide is the technical manifestation of the ZARISH-HIS Gold Standard, ensuring that every data point contributes to a reliable and interoperable health information system."
