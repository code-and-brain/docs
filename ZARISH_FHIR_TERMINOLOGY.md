# ZARISH-HIS FHIR TERMINOLOGY (CodeSystems and ValueSets)
**Author:** Mohammad Ariful ISLAM  
**Contact:** zarishsphere@gmail.com  
**Platform:** ZARISH SPHERE  
**Date:** 04 January 2026  
**Time:** 02:45 PM  

---

## 1. TRIAGE PRIORITY STANDARDS

This terminology enforces the standardized Triage Priority categories (Red/Yellow/Green) as defined in the ZARISH-HIS clinical workflow.

### 1.1. CodeSystem: `ZarishTriagePriorityCS`

| Element | Constraint | Details |
| :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/CodeSystem/ZarishTriagePriorityCS` | Unique identifier for the CodeSystem. |
| **Name** | `ZarishTriagePriorityCodeSystem` | Human-readable name. |
| **Content** | `complete` | All codes are defined here. |

| Code | Display | Definition |
| :--- | :--- | :--- |
| `red` | Red (Emergency) | Immediate, life-saving intervention required. Time-critical. |
| `yellow` | Yellow (Urgent) | Serious condition requiring intervention within a few hours. |
| `green` | Green (Routine) | Non-urgent condition. Can wait for routine consultation. |

### 1.2. ValueSet: `ZarishTriagePriorityVS`

| Element | Constraint | Details |
| :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/ValueSet/ZarishTriagePriorityVS` | Unique identifier for the ValueSet. |
| **Name** | `ZarishTriagePriorityValueSet` | Human-readable name. |
| **Inclusion** | Includes all codes from `ZarishTriagePriorityCS`. | Used to bind to the `Observation.extension:triage` element. |

---

## 2. PATIENT STATUS STANDARDS

This terminology enforces the mandatory "Status of Patient" field required for all registrations, crucial for humanitarian reporting.

### 2.1. CodeSystem: `ZarishPatientStatusCS`

| Element | Constraint | Details |
| :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/CodeSystem/ZarishPatientStatusCS` | Unique identifier for the CodeSystem. |
| **Name** | `ZarishPatientStatusCodeSystem` | Human-readable name. |
| **Content** | `complete` | All codes are defined here. |

| Code | Display | Definition |
| :--- | :--- | :--- |
| `refugee` | Refugee/Displaced Person | Individual registered as a refugee or displaced person in the response area. |
| `resident` | Local Resident | Individual registered as a permanent resident of the host community. |
| `staff` | Health Staff | Individual is a staff member of the health facility or partner organization. |
| `other` | Other/Unknown | Status is not one of the defined categories. |

### 2.2. ValueSet: `ZarishPatientStatusVS`

| Element | Constraint | Details |
| :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/ValueSet/ZarishPatientStatusVS` | Unique identifier for the ValueSet. |
| **Name** | `ZarishPatientStatusValueSet` | Human-readable name. |
| **Inclusion** | Includes all codes from `ZarishPatientStatusCS`. | Used to bind to the `Patient.extension:status` element. |

---

## 3. DIAGNOSIS CODING STANDARD

ZARISH-HIS mandates the use of **ICD-11** for all diagnosis coding to ensure global comparability and interoperability.

| Standard | FHIR Use | Details |
| :--- | :--- | :--- |
| **ICD-11** | **CodeSystem Reference** | The `Condition.code` element must be bound to the official ICD-11 CodeSystem URI. |
| **FHIR Resource** | `Condition` | Used to record the patient's diagnosis. |
| **Constraint** | **Terminology Binding** | The binding strength should be **Required** to enforce the use of ICD-11 codes. |

---

> "These CodeSystems and ValueSets provide the controlled vocabulary necessary to ensure that all ZARISH-HIS data is consistently and accurately recorded, forming the foundation of reliable health reporting."
