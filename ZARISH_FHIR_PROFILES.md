# ZARISH-HIS FHIR PROFILES (StructureDefinitions)
**Author:** Mohammad Ariful ISLAM  
**Contact:** zarishsphere@gmail.com  
**Platform:** ZARISH SPHERE  
**Date:** 04 January 2026  
**Time:** 02:30 PM  

---

## 1. ZARISH-HIS PATIENT PROFILE (`ZarishPatient`)

This profile constrains the base FHIR R4 `Patient` resource to enforce the mandatory registration rules and unique identifier format for ZARISH-HIS.

| Element | Constraint | Details |
| :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/StructureDefinition/ZarishPatient` | Unique identifier for the profile. |
| **Base Resource** | `Patient` | Constrains the standard FHIR Patient resource. |
| **`Patient.identifier`** | **Cardinality: 1..*** | Must have at least one identifier. |
| **`Patient.identifier.system`** | **Fixed Value** | Must be `http://zarishsphere.org/fhir/sid/patient-id` |
| **`Patient.identifier.value`** | **Pattern Constraint** | Must match the regex: `^ZSH-\d{4}-\d{5}$` (e.g., ZSH-2026-00001). |
| **`Patient.name`** | **Cardinality: 1..1** | Patient name is mandatory. |
| **`Patient.gender`** | **Cardinality: 1..1** | Gender is mandatory. |
| **`Patient.birthDate`** | **Cardinality: 1..1** | Date of Birth is mandatory. |
| **`Patient.telecom`** | **Pattern Constraint** | `telecom.value` must match regex for Bangladesh country code: `^\+880\d{10,12}$`. |
| **`Patient.extension:status`** | **Mandatory Extension** | Custom extension to capture the mandatory "Status of Patient" (e.g., Refugee, Resident). Binds to `ZarishPatientStatus` ValueSet. |

## 2. ZARISH-HIS OBSERVATION PROFILE (`ZarishTriageVitals`)

This profile constrains the base FHIR R4 `Observation` resource to enforce the standardized collection of Triage Vitals.

| Element | Constraint | Details | |
| :--- | :--- | :--- | :--- |
| **URL** | `http://zarishsphere.org/fhir/StructureDefinition/ZarishTriageVitals` | Unique identifier for the profile. |
| **Base Resource** | `Observation` | Constrains the standard FHIR Observation resource. |
| **`Observation.code`** | **Fixed Value Set** | Must be bound to a ValueSet containing required LOINC codes for Temperature, BP, Heart Rate, and SpO2. |
| **`Observation.valueQuantity`** | **Range Constraint** | **Temperature:** Value must be between 34.0 and 42.0 (unit: `Cel`). |
| **`Observation.valueQuantity`** | **Range Constraint** | **SpO2:** Value must be between 50 and 100 (unit: `%`). |
| **`Observation.extension:triage`** | **Mandatory Extension** | Custom extension to capture the Triage Priority (Red/Yellow/Green). Binds to `ZarishTriagePriority` ValueSet. |

---

> "These StructureDefinitions form the technical contract for data submission, ensuring that all data entering the ZARISH-HIS system is validated against the defined 'Gold Standard' rules."
