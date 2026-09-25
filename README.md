# ServiceNow - Implement Client Script & UI Policy (Incident)

## 📌 Problem Statement
Incident records often suffer from incomplete data entry affecting triage and SLA. This project enforces conditional field behavior and validation at UI level using UI Policies and Client Scripts.

## 🎯 Objective
To demonstrate how ServiceNow client-side controls enforce data integrity on Incident records by dynamically making fields mandatory, auto-populating values, and preventing invalid submissions.

## 🛠️ Skills Demonstrated
- Incident Management
- UI Policy & UI Policy Actions
- Client Scripts (onChange, onSubmit, onCellEdit)
- Form Validation

## ✅ Implementation Steps

### Task 1: Create UI Policy on Incident
- **Name:** High Impact Control
- **Table:** Incident [incident]
- **Active:** true
- **Condition:** Impact [is] 1 - High
- **Reverse if false:** true
- **Short Description:** Enforce mandatory Assignment group when Impact is High

### Task 2: Create UI Policy Action
- **UI Policy:** High Impact Control
- **Field:** Assignment group [assignment_group] -> Mandatory: true
- **Field:** Urgency [urgency] -> Read-only: true

> Verification: Set Impact = High, Urgency becomes read-only.

### Task 3: onChange Client Script - Auto set Urgency
- **Name:** Auto set urgency for high impact
- **Table:** Incident
- **Type:** onChange
- **Field:** Impact
### Task 4 - onSubmit Client Script (Validate Assigned To)
- Name: Validate Assigned To for High Impact
- Table: Incident [incident]
- Type: onSubmit
- Active: true
- Script:
- ```javascript
function onSubmit() {
    if (g_form.getValue('impact') == '1' && g_form.getValue('assigned_to') == '') {
        g_form.showErrorBox('assigned_to', 'Assigned To is mandatory for High impact Incidents.');
        return false;
    }
    return true;
}
- Purpose: If Assigned To is empty for a High Impact incident, the form will not be submitted.

### Task 5 - onCellEdit Client Script (Prevent State list edit)
- Name: Prevent State list edit
- Table: Incident [incident]
- Type: onCellEdit
- Field Name: State
- Active: true
- Script:
- ```javascript
function onCellEdit(sysIDs, table, oldValues, newValue, callback) {
    alert('State cannot be updated using list editing. Please open the Incident.');
    callback(false);
}
- Purpose: Prevents editing the State field via list view.
##screenshots <img width="1366" height="768" alt="Screenshot 2026-09-25 180536" src="https://github.com/user-attachments/assets/b9652ebe-c445-4e96-a092-9cc42e3654d0" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 180536" src="https://github.com/user-attachments/assets/b2810812-9c0d-46dd-8d82-2408a3f70b81" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 180536" src="https://github.com/user-attachments/assets/fa2495e4-ee86-4e37-97a6-23ddc7ad2c2d" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 180536" src="https://github.com/user-attachments/assets/ab2d66ca-685a-4751-89a0-d79ed98e79ed" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 180536" src="https://github.com/user-attachments/assets/5947806f-d823-4178-83c9-65b769dee214" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 182421" src="https://github.com/user-attachments/assets/32b63454-0dfa-4a84-a8fc-64bb909c0178" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 183118" src="https://github.com/user-attachments/assets/f00d6a0b-5f6e-465b-bb4a-050263644969" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 185954" src="https://github.com/user-attachments/assets/d3fe26f4-d655-4461-9d9e-5d6f71bc7508" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 190007" src="https://github.com/user-attachments/assets/0865e726-1917-4169-b530-4364f1ae9b1b" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 190725" src="https://github.com/user-attachments/assets/b03d72ca-52be-4847-a029-c3f177a52ac1" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 191849" src="https://github.com/user-attachments/assets/3288722f-8a49-469d-872b-c5e87b4ecfec" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 193104" src="https://github.com/user-attachments/assets/b66acceb-2e05-479d-9eac-e8cb80fedbed" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 193104" src="https://github.com/user-attachments/assets/7517fb9f-0551-4087-9e7d-141e56007aa7" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 194558" src="https://github.com/user-attachments/assets/d5539e64-3226-4fcc-bc41-a9bb61db69aa" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 194658" src="https://github.com/user-attachments/assets/a39da254-0ee2-47e3-9dd0-881105bc15bc" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 195258" src="https://github.com/user-attachments/assets/1e23bd3b-cfc1-4a45-87ce-841831d5803f" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 195805" src="https://github.com/user-attachments/assets/a21ae414-9a2f-4001-824c-13405259756d" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 195805" src="https://github.com/user-attachments/assets/5665880d-7b62-4ee7-9640-a285f91cf4e4" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 200412" src="https://github.com/user-attachments/assets/7479055a-aff2-40cb-aafc-953473f85603" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 200459" src="https://github.com/user-attachments/assets/28659e72-6847-4f02-a502-3659d2ea8aac" />
<img width="1366" height="768" alt="Screenshot 2026-09-25 200625" src="https://github.com/user-attachments/assets/4471b04b-a421-48cb-81ad-45a049ce469a" />
##project links
https://docs.google.com/document/d/1aAaZeb1yZVCycibm5tMpWkqX1R35JA3tjRV6Wz0MUM8/edit?usp=sharing







 
