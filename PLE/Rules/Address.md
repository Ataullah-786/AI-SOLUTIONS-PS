# PLE - Address Rules

**Product:** PLE
**Target Table:** `Address`
**Schema File:** `/PLE/Schema/Address.json`
**Source Workbook:** `ADDRESS_tem.xlsx`
**Source Worksheet:** `Template`

These rules are taken from the supplied PLE template workbook. They describe how
intake columns must be populated and validated before data is integrated into the PLE `Address` table.

They are **additional to** the structural rules in `/PLE/Schema/Address.json`.
Where the workbook and JSON schema disagree on a physical type or length, the JSON
schema remains the source of truth for storage and the rules below define the business/intake expectation.

---

## Field Rules

| Intake Label | PLE Field | Format | Default | Rule / Description | Source | Comment |
| --- | --- | --- | --- | --- | --- | --- |
| Operations List | ACMP_COMP_REF_LIST | String(1000) | - | Comma separated list of Operation References for which the given Address should be activated | - | - |
| Address Reference | ADDR_REF | String(8) | - | Primary Key | - | - |
| Address Name | ADDR_NAME | String(60) | - | - | - | - |
| Property Name | ADDR_PROP_NAME | String(60) | - | - | - | - |
| Address Line 1 | ADDR_L1 | String(30) | - | - | - | - |
| Address Line 1 | ADDR_L2 | String(30) | - | - | - | - |
| Town | ADDR_TOWN | String(30) | - | - | - | - |
| County | ADDR_COUNTY | String(30) | - | Desc of Code of Type: 'COU' (State/Province) | - | - |
| Postcode | ADDR_POSTCODE | String(12) | - | - | - | - |
| Country | ADDR_COUNTRY | String(30) | - | Desc of Code of Type: 'ISO' (Country Codes) | - | - |
| Phone | ADDR_PHONE | String(20) | - | - | - | - |
| Email | ADDR_EMAIL | String(320) | - | - | - | - |
| Fax | ADDR_FAX | String(20) | - | - | - | - |
| Web | ADDR_WEB | String(60) | - | - | - | - |
| Agent Code | ADDR_AGENT_CODE | String(3) | - | Code of Type: 'OPA' (OPERATION AGENT) | - | - |
| Tax Number | ADDR_VAT_NUM | String(25) | - | - | - | - |
| Tax Id | ADDR_TAX_ID | String(25) | - | - | - | - |
| Tax Code | ADDR_CDGN_VAT_CREF | String(3) | - | Code of Type: 'VTC' (VAT Country) | - | - |
| Address Territory | ADDR_TERI_CODE | String(3) | - | Code of Type: 'TER' (Territory) | - | - |
| Operation Reg Num | ADDR_COMP_REG_NUM | String(25) | - | - | - | - |
| NI Number | ADDR_NI_NUMBER | String(13) | - | - | - | - |

---

## Validation Rules

### Table-Level Validations

Each expression identifies the condition that makes a row invalid. Report the workbook's stated message when the expression evaluates to true.

| Type | Message | Validation (invalid if true) |
| --- | --- | --- |
| Error | acmp_comp_ref_list contains an invalid Operation Reference | (:acmp_comp_ref_list is not Null) and (company(comp_ref in: :acmp_comp_ref_list).AllExistent is False) |
| Error | addr_ni_number can only be specified if ITSA is enabled | (:addr_ni_number is not Null) and (skyconf.skyc_itsa_flag <> 'Y') |
| Error | addr_ref contains prohibited characters | (:addr_ref is not Null) and (:addr_ref matches Regex('[^a-zA-Z0-9/.:%!$*_+&^-]')) |

### Field-Level Validation and Derivation

| Label | PLE Field | Mode | Validation | Derivation |
| --- | --- | --- | --- | --- |
| Address Reference | ADDR_REF | Client Data | Primary Key: address.addr_ref | - |
| County | ADDR_COUNTY | Client Data | Must be: codesgen.cdgn_desc_long with cdgn_cdty_ref = 'COU' | - |
| Country | ADDR_COUNTRY | Client Data | Must be: codesgen.cdgn_desc_long with cdgn_cdty_ref = 'ISO' | - |
| Agent Code | ADDR_AGENT_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'OPA' | - |
| Status | ADDR_STATUS_CODE | System Default | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ADS' | - |
| Tax Code | ADDR_CDGN_VAT_CREF | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'VTC' | - |
| Address Territory | ADDR_TERI_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'TER' | - |
| NI Number | ADDR_NI_NUMBER | Client Data | - | Upper(Replace(str: :addr_ni_number, match_val: ' ', rep_val: '')) |
| Country Code | ADDR_COUNTRY_ISO_CODE | Derived | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ISO' | codesgen(cdgn_desc_long = addr_country, cdgn_cdty_ref = 'ISO').cdgn_ref |
| Entity Usage Code | ADDR_USAGE_CODE | System Default | Usage Code | - |

### Uniqueness Rules

| Scope | Name | Restriction | Fields |
| --- | --- | --- | --- |
| Maximum | Primary Key | None | ADDR_REF |

## Internal Derived Fields

These fields are calculated or checked internally during processing; they are not intake columns.

| Field | Timing | Derivation |
| --- | --- | --- |
| TERI_CODE | Default | :addr_teri_code |

## Additional Processing Rules

Apply these workbook-defined tasks at the stated processing line or trigger.

| Id | Name | Line | Type | Triggers | Details | Internal Fields | Variables | Variable Calculations |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Default | 0 | Run Condition | - | Always runnable | - | - | - |
| - | Default | 01 | Cursor | - | SELECT ht.acmp_comp_ref_list, bt.addr_teri_code, bt.addr_agent_code, bt.addr_ref, bt.addr_ni_number, bt.qcid<br>FROM address bt<br>INNER JOIN address_h1_01 ht ON ht.qcid = bt.qcid<br>WHERE (inserted during parent run)<br>ORDER BY bt.qcid | - | - | - |
| - | Default | 01.01.01 | Condition | - | IF :acmp_comp_ref_list is Null | - | skyc_acmp_active_for_mig = if (fwpackage.fw_create_active_addr = 'A') then ('Y') else ('N')<br>skyc_teri_flag = skyconf.skyc_teri_flag<br>skyc_use_agent_code = skyconf.skyc_use_agent_code | - |
| - | Default | 01.01.01.01.01 | Condition | - | IF (:skyc_teri_flag = 'Y') or (:skyc_use_agent_code = 'Y') | - | - | - |
| - | Default | 01.01.01.01.01.01 | Cursor | - | SELECT comp_ref, comp_teri_code, comp_agent_code, qcid<br>FROM company<br>ORDER BY qcid | active = if (:comp_ref = 'SYSTEM') then 'N' else if (:skyc_teri_flag = 'Y') then (if (:addr_teri_code = :comp_teri_code) then ('Y') else if (:addr_teri_code is Null) then ('Y') else ('N')) else if (:skyc_use_agent_code = 'Y') then (if (:addr_agent_code = :comp_agent_code) then ('Y') else ('N')) | - | - |
| - | Default | 01.01.01.01.01.01.01 | Condition | - | IF (version of target is older than '10.1.16.0') or (:active = 'Y') | - | - | - |
| - | Default | 01.01.01.01.01.01.01.01 | Insert | - | INSERT INTO addrcomp:<br>acmp_addr_ref = :addr_ref<br>acmp_comp_ref = :comp_ref<br>acmp_active = :active | - | - | - |
| - | Default | 01.01.01.01.02 | Condition | - | ELSE | - | - | - |
| - | Default | 01.01.01.01.02.01 | Condition | - | IF (version of target is older than '10.1.16.0') or (:skyc_acmp_active_for_mig = 'Y') | - | - | - |
| - | Default | 01.01.01.01.02.01.01 | Insert | - | FOR EACH RECORD IN company<br>WHERE<br>comp_ref <> 'SYSTEM'<br>INSERT INTO addrcomp:<br>acmp_addr_ref = :addr_ref<br>acmp_comp_ref = :comp_ref<br>acmp_active = :skyc_acmp_active_for_mig | - | - | - |
| - | Default | 01.01.01.01.02.02 | Condition | - | IF version of target is older than '10.1.16.0' | - | - | - |
| - | Default | 01.01.01.01.02.02.01 | Insert | - | INSERT INTO addrcomp:<br>acmp_addr_ref = :addr_ref<br>acmp_comp_ref = 'SYSTEM'<br>acmp_active = 'N' | - | - | - |
| - | Default | 01.01.02 | Condition | - | ELSE | - | comp_ref = Null | - |
| - | Default | 01.01.02.01 | Loop | - | Begin Loop until (:comp_ref is Null) | - | Initialized all cycles of loop:<br>comp_teri_code = company(:comp_ref).comp_teri_code<br>comp_agent_code = company(:comp_ref).comp_agent_code<br>active = if (:comp_ref = 'SYSTEM') then 'N' else if (:skyc_teri_flag = 'Y') then (if (:addr_teri_code = :comp_teri_code) then ('Y') else if (:addr_teri_code is Null) then ('Y') else ('N')) else if (:skyc_use_agent_code = 'Y') then (if (:addr_agent_code = :comp_agent_code) then ('Y') else ('N')) else 'Y' | comp_ref = List(Str: :acmp_comp_ref_list, Separator(s): ', ').Item_At_Position(Loop_Idx) |
| - | Default | 01.01.02.01.01 | Condition | - | IF (version of target is older than '10.1.16.0') or (:active = 'Y') | - | - | - |
| - | Default | 01.01.02.01.01.01 | Insert | - | INSERT INTO addrcomp:<br>acmp_addr_ref = :addr_ref<br>acmp_comp_ref = :comp_ref<br>acmp_active = :active | - | - | - |
| - | Default | 01.02 | Condition | - | IF :addr_ni_number is not Null | - | - | - |
| - | Default | 01.02.01 | Insert | - | INSERT INTO vat_indi:<br>vati_ni_number = :addr_ni_number | - | - | - |

## Reference Code Types

Fields whose descriptions identify a code type must contain a value from that code type. The workbook's `Codes` and `LOVs` worksheets provide the corresponding lookup values.

| Code Type | Name | Desc |
| --- | --- | --- |
| ADS | Address Status | Address Status.<br>PROCESS FLAG 1: Live/Current address<br>PROCESS FLAG 2: Obsolete address. |
| COU | STATE/COUNTY | State/County |
| ISO | Country Codes | ISO Standard 2 character Country Codes<br>PROCESS FLAG 2: Auto-allocation of receipts is against Service Charge first followed by Rent.<br>PROCESS FLAG 3: Annual Tax Returns enabled by default. |
| OPA | OPERATION AGENT | Operation Agent |
| TER | Territory | Used to restrict access to various codes and config by country or territory/jurisdiction/country. |
| VTC | VAT Country | Country of VAT Registration |

---

## Source Notes

* `-` means the workbook cell is blank and does not add a rule or default.
* Validation and derivation expressions are preserved verbatim so implementation-specific PLE functions and field names are not reinterpreted.
* Code descriptions in field rules identify the required lookup family; use the workbook's `Codes` / `LOVs` worksheets or the target PLE database to validate the current allowed values.
* References to related PLE entities require the corresponding table data or target database. If that data is unavailable, report `Warning / REQUIRES DATABASE VERIFICATION` rather than claiming the reference is valid or invalid.
