# PLE - Demise Rules

**Product:** PLE
**Target Table:** `Demise`
**Schema File:** `/PLE/Schema/Demise.json`
**Source Workbook:** `DEMISE_tem.xlsx`
**Source Worksheet:** `Template`

These rules are taken from the supplied PLE template workbook. They describe how
intake columns must be populated and validated before data is integrated into the PLE `Demise` table.

They are **additional to** the structural rules in `/PLE/Schema/Demise.json`.
Where the workbook and JSON schema disagree on a physical type or length, the JSON
schema remains the source of truth for storage and the rules below define the business/intake expectation.

---

## Field Rules

| Intake Label | PLE Field | Format | Default | Rule / Description | Source | Comment |
| --- | --- | --- | --- | --- | --- | --- |
| Property Ref | DMSE_PROP_REF | String(8) | - | Foreign Key - property | - | - |
| Rental Space Ref | DMSE_REF | String(8) | - | Primary Key. Unique | - | - |
| Description | DMSE_DESC | String(60) | - | - | - | - |
| Ext Ref | DMSE_EXT_REF | String(20) | {DMSE_REF} | Unique. Default Is Rental Space Ref | - | - |
| Status Code | DMSE_STATUS_CODE | String(3) | VAC | Code of Type: 'DLS' (Demise Status) | - | - |
| Type Code | DMSE_TYPE_CODE | String(3) | - | Code of Type: 'DT' (Demise Type) | - | - |
| User Code | DMSE_USER_CODE | String(3) | - | User Code | - | - |
| Vacancy Reason | DMSE_VAC_REASON_CODE | String(3) | - | Code of Type: 'DVR' (Vacancy Reasons) | - | - |
| Comment | DMSE_COMMENT | String(1000) | - | - | - | - |

---

## Validation Rules

### Table-Level Validations

Each expression identifies the condition that makes a row invalid. Report the workbook's stated message when the expression evaluates to true.

| Message | Validation |
| --- | --- |
| dmse_ref contains prohibited characters | invalid if (:dmse_ref is not Null) and (:dmse_ref matches Regex('[^a-zA-Z0-9/.:%!$*_+&^-]')) |

### Field-Level Validation and Derivation

| Label | PLE Field | Mode | Validation | Derivation |
| --- | --- | --- | --- | --- |
| Group Ref | DMSE_GROP_REF | Derived | Must be: groups.grop_ref | property(dmse_prop_ref).prop_grop_ref |
| Operation Ref | DMSE_COMP_REF | Derived | Must be: company.comp_ref | property(dmse_prop_ref).prop_comp_ref |
| Property Ref | DMSE_PROP_REF | Client Data | Must be: property.prop_ref | - |
| Rental Space Ref | DMSE_REF | Client Data | Primary Key: demise.dmse_ref | - |
| Vac Pa Flag | DMSE_VAC_PA_FLAG | Derived | Must be: Flag: (O)ccupied, (V)acant | if (codesgen(cdty_ref: 'DLS', cdgn_ref: :dmse_status_code).cdgn_process_flag = 1) then 'O' else 'V' |
| Status Code | DMSE_STATUS_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'DLS' | - |
| Type Code | DMSE_TYPE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'DT' | - |
| User Code | DMSE_USER_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Vacancy Reason | DMSE_VAC_REASON_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'DVR' | - |
| Currency Code | DMSE_CUR_CODE | Derived | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUR' | property(:dmse_prop_ref).prop_currency_code |
| Usage Code | DMSE_USAGE_CODE | System Default | Usage Code | - |

### Uniqueness Rules

| Scope | Name | Restriction | Fields |
| --- | --- | --- | --- |
| Maximum | DEMISEI2 | None | DMSE_PROP_REF, DMSE_REF |
| Maximum | Primary Key | None | DMSE_REF |
| Maximum | Validation Index 1 | None | DMSE_EXT_REF |

## Internal Derived Fields

These fields are calculated or checked internally during processing; they are not intake columns.

| Field | Timing | Derivation |
| --- | --- | --- |
| TERI_CODE | Default | if (skyconf.skyc_teri_flag = 'Y') then (company(:dmse_comp_ref).comp_teri_code) |

## Additional Processing Rules

Apply these workbook-defined tasks at the stated processing line or trigger.

| Id | Name | Line | Type | Triggers | Details | Internal Fields | Variables | Variable Calculators |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 39 | Validation - Occupied Demise with no Live Rental Lease | 0 | Run Criteria | - | Always runnable | - | - | - |
| 39 | Validation - Occupied Demise with no Live Rental Lease | 01 | Cursor | - | SELECT dmse_status_code, dmse_ref, qcid<br>FROM demise<br>WHERE qcid IN {demise_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 39 | Validation - Occupied Demise with no Live Rental Lease | 01.01 | Criteria | - | IF ((codesgen(cdty_ref: 'DLS', cdgn_ref: :dmse_status_code).cdgn_process_flag = 1) and (not (lease(dmse_ref: :dmse_ref, rental_flag: 'Y', status_code_process_flag: 1).Existent))) | - | - | - |
| 39 | Validation - Occupied Demise with no Live Rental Lease | 01.01.01 | Comment | - | 'Demise is Occupied but there is no Live Rental Lease associated with it' | - | - | - |

## Reference Code Types

Fields whose descriptions identify a code type must contain a value from that code type. The workbook's `Codes` and `LOVs` worksheets provide the corresponding lookup values.

| Code Type | Name | Desc |
| --- | --- | --- |
| CUR | Currency Codes | Currency Codes |
| DLS | Demise Status | Rental Space Status<br>PROCESS FLAG 0:<br>Disposed<br>Excluded when status filtering ON.<br>PROCESS FLAG 1:<br>Occupied<br>Used when the 'Tenant Move In' process is completed.<br>Will not be available at the start of the 'Tenant Move In' process.<br>PROCESS FLAG 2:<br>Vacant<br>Used when the 'Tenant Move Out' process is completed.<br>PROCESS FLAG 9:<br>Provisional<br>Excluded when status filtering ON.<br>Used during the 'Tenant Move In' process. |
| DT | Demise Type | Rental Space Type<br>PROCESS FLAG 0: Historic (filtered out by status filtering)<br>PROCESS FLAG 1: Standard live type<br>PROCESS FLAG 2: Multi-let space (can be rented out more than once at the same time)<br>PROCESS FLAG 3: Licenses (can be rented out with no units attached)<br>PROCESS FLAG 4: Rental Space Only (no units attached) and Multi-Let |
| DVR | Vacancy Reasons | Rental Space Vacancy Reasons<br>PROCESS FLAG 1:<br>Let<br>Used when the 'Tenant Move In' process is completed.<br>PROCESS FLAG 2:<br>Vacant<br>Used when the 'Tenant Move Out' process is completed. |

---

## Source Notes

* `-` means the workbook cell is blank and does not add a rule or default.
* Validation and derivation expressions are preserved verbatim so implementation-specific PLE functions and field names are not reinterpreted.
* Code descriptions in field rules identify the required lookup family; use the workbook's `Codes` / `LOVs` worksheets or the target PLE database to validate the current allowed values.
* References to related PLE entities require the corresponding table data or target database. If that data is unavailable, report `Warning / REQUIRES DATABASE VERIFICATION` rather than claiming the reference is valid or invalid.
