# ZARISH-HIS: NON-CLINICAL & SUPPORT SERVICES
**Author:** Mohammad Ariful ISLAM  
**Contact:** zarishsphere@gmail.com  
**Platform:** ZARISH SPHERE  
**Date:** 04 January 2026  
**Time:** 12:30 PM  

---

## 1. OVERVIEW OF SUPPORT SERVICES

Non-clinical services are the backbone of **ZARISH-HIS**, ensuring that clinical teams have the resources, data, and infrastructure needed to provide care.

### 1.1. Key Support Modules

| Module | Function | System Role |
| :--- | :--- | :--- |
| **Inventory Management** | Tracking medical supplies and drugs. | HIS - Logistics |
| **Staff Management** | Rostering and performance tracking. | HIS - HR |
| **Facility Management** | Maintenance and utility tracking. | HIS - Admin |
| **Reporting & Analytics** | Generating health indicators and trends. | HIS - Intelligence |

---

## 2. DETAILED SERVICE DEFINITIONS

### 2.1. Pharmacy & Supply Chain
Ensures the availability of essential medicines.

#### Form: Stock Requisition
- **Purpose:** To request supplies from the central warehouse.
- **Key Fields:**
    - `Item Name`: Dropdown (Linked to Master List)
    - `Quantity Requested`: Numeric
    - `Current Stock Level`: Numeric (Auto-calculated)
    - `Urgency`: Dropdown (Routine, Urgent, Emergency)

#### Form: Medication Dispensing
- **Purpose:** To record the delivery of medicine to a patient.
- **Key Fields:**
    - `Patient ID`: Text (Linked to EMR)
    - `Prescription ID`: Text (Linked to EMR)
    - `Quantity Dispensed`: Numeric
    - `Pharmacist Instructions`: Text

---

### 2.2. Laboratory & Imaging Administration
Managing the workflow of diagnostic tests.

#### Form: Lab Result Entry
- **Purpose:** To digitize laboratory findings.
- **Key Fields:**
    - `Test Type`: Dropdown (CBC, Glucose, etc.)
    - `Result Value`: Numeric/Text
    - `Reference Range`: Text (Auto-populated)
    - `Flag`: Dropdown (Normal, High, Low, Critical)

---

### 2.3. Community Outreach Administration
Tracking health promotion activities outside the facility.

#### Form: Community Session Log
- **Purpose:** To document health education sessions.
- **Key Fields:**
    - `Topic`: Dropdown (Hygiene, Nutrition, NCDs)
    - `Location`: Text (Block/Community Center)
    - `Number of Participants`: Numeric (Male/Female/Children)
    - `Key Feedback`: Text

---

## 3. DATA INTEGRITY & SECURITY

Non-clinical data must be handled with the same level of security as clinical data.

1. **Role-Based Access Control (RBAC):**
    - Pharmacists can only access Pharmacy and Medication modules.
    - Lab Technicians can only access Lab Order and Result modules.
    - Administrators have view-only access to clinical summaries for reporting.
2. **Audit Trails:**
    - Every change to stock levels or staff records is logged with a timestamp and User ID.
3. **Data Backup:**
    - All HIS data is backed up daily to secure, encrypted off-site servers.

---

## 4. SYSTEM LINKAGES (HIS-EMR)

| Linkage | Description | Benefit |
| :--- | :--- | :--- |
| **Pharmacy to EMR** | Real-time stock alerts during prescribing. | Prevents prescribing out-of-stock items. |
| **Lab to EMR** | Automatic result notification to doctors. | Speeds up clinical decision-making. |
| **HR to EMR** | Linking staff IDs to clinical notes. | Ensures accountability for every entry. |

---

> "By integrating non-clinical services into the ZARISH-HIS ecosystem, we create a truly comprehensive Health Information System that supports both the patient and the provider."
