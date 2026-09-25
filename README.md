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
function onSubmit() {
    if (g_form.getValue('impact') == '1' && g_form.getValue('assigned_to') == '') {
        g_form.showErrorBox('assigned_to', 'Assigned To is mandatory for High impact Incidents.');
        return false;
    }
    return true;
}
- Purpose: High Impact incident ku Assigned To illana form submit aagathu da.

### Task 5 - onCellEdit Client Script (Prevent State list edit)
- Name: Prevent State list edit
- Table: Incident [incident]
- Type: onCellEdit
- Field Name: State
- Active: true
- Script:
function onCellEdit(sysIDs, table, oldValues, newValue, callback) {
    alert('State cannot be updated using list editing. Please open the Incident.');
    callback(false);
}
- Purpose: List view la State ah edit panna vidathu da.
 
