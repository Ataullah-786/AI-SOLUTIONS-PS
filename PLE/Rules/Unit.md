# PLE - Unit Rules

**Product:** PLE
**Target Table:** `Unit`
**Schema File:** `/PLE/Schema/Unit.json`
**Source Workbook:** `UNIT_tem.xlsx`
**Source Worksheet:** `Template`

These rules are taken from the supplied PLE template workbook. They describe how
intake columns must be populated and validated before data is integrated into the PLE `Unit` table.

They are **additional to** the structural rules in `/PLE/Schema/Unit.json`.
Where the workbook and JSON schema disagree on a physical type or length, the JSON
schema remains the source of truth for storage and the rules below define the business/intake expectation.

---

## Field Rules

| Intake Label | PLE Field | Format | Default | Rule / Description | Source | Comment |
| --- | --- | --- | --- | --- | --- | --- |
| Property Reference | UNIT_PROP_REF | String(8) | - | Foreign Key - property | - | - |
| Floor | UNIT_FLOR_FLOOR_CODE | String(3) | - | Code of Type: 'FLR' (Floor Type). Must be associated with the Property | - | - |
| Acquisition Reference | UNIT_ACQU_REF | String(8) | - | Foreign Key - acquire. Acqu_Acquire_As_Flag= U | - | - |
| Zone Ref | UNIT_ZONE_REF | String(8) | - | Foreign Key - zone | - | - |
| Importance | UNIT_IMP_CODE | String(3) | - | Code of Type: 'MIM' (Maintenance Importance) | - | - |
| Unit Reference | UNIT_REF | String(8) | - | Primary Key. Unique | - | - |
| Unit Description | UNIT_DESC | String(60) | - | - | - | - |
| External Ref | UNIT_EXT_REF | String(20) | {UNIT_REF} | Unique.   Default Is Unit Ref. | - | - |
| Prsl Ref | UNIT_PRSL_REF | String(8) | - | Foreign Key - propsale | - | - |
| Type | UNIT_TYPE_CODE | String(3) | - | Code of Type: 'UT' (UNIT TYPE) | - | - |
| Unit Start Date | UNIT_START_DATE | Date | - | - | - | - |
| Unit End Date | UNIT_END_DATE | Date | - | Must Be After Start Date | - | - |
| Main Unit | UNIT_MAIN_UNIT_FLAG | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Status | UNIT_STATUS_CODE | String(3) | - | Code of Type: 'STA' (Unit Status) | - | - |
| Physical Sector | UNIT_PHYSICAL_SECTOR | String(3) | - | Code of Type: 'UPS' (Unit Physical Sector) | - | - |
| Elmt Type | UNIT_ELMT_TYPE | String(3) | - | Code of Type: 'ETY' (Property Element Type) | - | - |
| Initial Book Cost | UNIT_BOOK_COST | Number(13,2) | - | - | - | - |
| Lnld Ref | UNIT_LNLD_REF | String(8) | - | Foreign Key - supplier. Landlord Flag On Supplier Must Be Y | - | - |
| Hlse Ref | UNIT_HLSE_REF | String(8) | - | Foreign Key - headleas. Must Belong To The Same Property | - | - |
| Dmse Ref | UNIT_DMSE_REF | String(8) | - | Foreign Key - demise. Must Belong To The Same Property | - | - |
| Measure Code | UNIT_MEASURE_CODE | String(3) | - | Measurement Code | - | - |
| Net Internal Area | UNIT_NIA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Gross Land Area | UNIT_GIA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Area | UNIT_NEA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Gross External Area | UNIT_GEA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Space Type | UNIT_SPACE_TYPE | String(3) | - | Code of Type: 'UST' (Unit Space Type) | - | - |
| Cad Ref | UNIT_CAD_REF | String(50) | - | - | - | - |
| Cad Area | UNIT_CAD_AREA | Number<br>Min Val: 0<br>Max Val: 9999999.99 | - | - | - | - |
| Primary Use | UNIT_PRIMARY_USE | String(3) | - | Code of Type: 'UOU' (Unit Organisation Usage) | - | - |
| Alienability Code | UNIT_ALIENABILITY_CODE | String(3) | - | Code of Type: 'ALI' (Alienability Status) | - | - |
| User Code | UNIT_USER_CODE | String(3) | - | User Code | - | - |
| Expected Life (Years) | UNIT_EXPECT_LIFE | Number(4)<br>Min Val: 0<br>Max Val: 9999 | - | - | - | - |
| Disabled Access | UNIT_DISABLED_ACCESS | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Max Employees | UNIT_MAX_EMPLOYEES | Number(8)<br>Min Val: 0<br>Max Val: 99999999 | - | - | - | - |
| Max Workstations | UNIT_MAX_WORKSTATIONS | Number(8)<br>Min Val: 0<br>Max Val: 99999999 | - | - | - | - |
| Parking Spaces | UNIT_CAR_PARK_SPACES | Number(5)<br>Min Val: 0<br>Max Val: 99999 | - | - | - | - |
| External Reference 2 | UNIT_EXT_REF2 | String(20) | - | - | - | - |
| Regular Task End Date | UNIT_RTSU_END_DATE | Date | - | - | - | - |
| Exclude from Expense Recovery | UNIT_EX_EXP_REC_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Expense Recovery Area | UNIT_ER_AREA | Number(13,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | - | - | - |
| Expense Class | UNIT_ER_CLASS_CODE | String(3) | - | Code of Type: 'ERC' (Expense Recovery Class) | - | - |
| Comment | UNIT_COMMENT | String(1000) | - | - | - | - |
| Unit Name | UNIT_NAME | String(60) | - | Default Is Property Name | - | - |
| Address (Line 1) | UNIT_ADDR_L1 | String(60) | - | Default Is Property Address L1 | - | - |
| Address (Line 2) | UNIT_ADDR_L2 | String(30) | - | Default Is Property Address L2 | - | - |
| Town | UNIT_TOWN | String(30) | - | Default Is Property Town | - | - |
| County | UNIT_COUNTY | String(30) | - | Desc of Code of Type: 'COU' (State/Province). Default Is Property County | - | - |
| Postcode | UNIT_POSTCODE | String(12) | - | Default Is Property Postcode | - | - |
| Country | UNIT_COUNTRY | String(30) | - | Desc of Code of Type: 'ISO' (Country Codes). Default Is Property Country | - | - |
| Available From Date | UNIT_AVAIL_DATE | Date | - | - | - | - |
| Number of Beds | UNIT_NO_BEDS | Number(2)<br>Min Val: 0<br>Max Val: 99 | - | - | - | - |
| Number of Baths | UNIT_NO_BATHS | Number(2)<br>Min Val: 0<br>Max Val: 99 | - | - | - | - |
| Number of Receptions | UNIT_NO_RECEPTIONS | Number(2)<br>Min Val: 0<br>Max Val: 99 | - | - | - | - |
| Tax Recoverable | UNIT_TAX_OPTION_FLAG | String(1) | - | Flag: (N)o, (Y)es | - | - |

---

## Validation Rules

### Table-Level Validations

Each expression identifies the condition that makes a row invalid. Report the workbook's stated message when the expression evaluates to true.

| Message | Validation |
| --- | --- |
| Acqusition Ref was not acquired as a unit | invalid if (:unit_acqu_ref is not Null) and (acquire(:unit_acqu_ref).acqu_acquire_as_flag <> 'U') |
| Demise belongs to a different Property | invalid if (:unit_dmse_ref is not Null) and (demise(ref: :unit_dmse_ref, prop_ref <> :unit_prop_ref).Existent) |
| End date must be after Start Date | invalid if (:unit_end_date is not Null) and (:unit_end_date <= :unit_start_date) |
| End Date must not be populated on the Main Unit when Unit Trial Balancing is enabled at system level | invalid if (:unit_end_date is not Null) and (:unit_main_unit_flag = 'Y') and (skyconf.skyc_unit_trial_bal = 'Y') |
| Floor Code must be associated with the Property | invalid if (:unit_flor_floor_code is not Null) and (floor(prop_ref: :unit_prop_ref, floor_code: :unit_flor_floor_code).Inexistent) |
| Lease Payable belongs to a different Property | invalid if (:unit_hlse_ref is not Null) and (headleas(ref: :unit_hlse_ref, prop_ref <> :unit_prop_ref).Existent) |
| Measure Code must not be null if any of the Area fields are not null | invalid if (:unit_measure_code is Null) and ((:unit_nia is not Null) or (:unit_nea is not Null) or (:unit_gia is not Null) or (:unit_gea is not Null)) |
| Rental Space must be populated on the Main Unit | invalid if (:unit_dmse_ref is Null) and (:unit_main_unit_flag = 'Y') |
| Tax only recoverable if Tax Option taken at Property level | invalid if (property(:unit_prop_ref).prop_tax_option_flag <> 'Y') and (:unit_tax_option_flag = 'Y') |
| Unit must not be occupied if Demise is not occupied | invalid if (:unit_dmse_ref is not Null) and (:unit_status_code_process_flag = 1) and (:dmse_status_code_process_flag <> 1) |
| Unit must not be vacant if Demise is occupied and there are no other units belonging to it that are occupied | invalid if (:unit_dmse_ref is not Null) and (:unit_status_code_process_flag = 2) and (:dmse_status_code_process_flag = 1) and (not (unit(dmse_ref: :unit_dmse_ref, unit_status_code_process_flag: 1).Existent)) |
| unit_avail_date can only differ from default if SLM Interface is installed | invalid if (skyconf.skyc_slm_interface <> 'Y') and (:unit_avail_date_in_template is not Null) and (:unit_avail_date_in_template <> :unit_avail_date_default) |
| unit_no_baths must not be populated if skyc_slm_interface is not Y | invalid if (NVL(skyconf.skyc_slm_interface, 'N') = 'N') and (:unit_no_baths is not Null) |
| unit_no_beds must not be populated if skyc_slm_interface is not Y | invalid if (NVL(skyconf.skyc_slm_interface, 'N') = 'N') and (:unit_no_beds is not Null) |
| unit_no_receptions must not be populated if skyc_slm_interface is not Y | invalid if (NVL(skyconf.skyc_slm_interface, 'N') = 'N') and (:unit_no_receptions is not Null) |
| unit_ref contains prohibited characters | invalid if (:unit_ref is not Null) and (:unit_ref matches Regex('[^a-zA-Z0-9/.:%!$*_+&^-]')) |

### Field-Level Validation and Derivation

| Label | PLE Field | Mode | Validation | Derivation |
| --- | --- | --- | --- | --- |
| Group Ref | UNIT_GROP_REF | Derived | Must be: groups.grop_ref | property(unit_prop_ref).prop_grop_ref |
| Operation Reference | UNIT_COMP_REF | Derived | Must be: company.comp_ref | property(unit_prop_ref).prop_comp_ref |
| Property Reference | UNIT_PROP_REF | Client Data | Must be: property.prop_ref | - |
| Floor | UNIT_FLOR_FLOOR_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'FLR' | - |
| Acquisition Reference | UNIT_ACQU_REF | Client Data | Must be: acquire.acqu_ref | - |
| Zone Ref | UNIT_ZONE_REF | Client Data | Must be: zone.zone_ref | - |
| Importance | UNIT_IMP_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'MIM' | - |
| Unit Reference | UNIT_REF | Client Data | Primary Key: unit.unit_ref | - |
| Prsl Ref | UNIT_PRSL_REF | Client Data | Must be: propsale.prsl_ref | - |
| Type | UNIT_TYPE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'UT' | - |
| Main Unit | UNIT_MAIN_UNIT_FLAG | Client Data (Derived if Null) | Must be: Flag: (N)o, (Y)es | If null....<br>if ((:unit_dmse_ref is not Null) and (:unit_end_date is Null) and (not (Unit(dmse_ref: :unit_dmse_ref).Other_Existent))) then 'Y' else 'N' |
| Status | UNIT_STATUS_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'STA' | - |
| Physical Sector | UNIT_PHYSICAL_SECTOR | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'UPS' | - |
| Elmt Type | UNIT_ELMT_TYPE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ETY' | - |
| Lnld Ref | UNIT_LNLD_REF | Client Data | Must be: supplier.supp_ref | - |
| Hlse Ref | UNIT_HLSE_REF | Client Data | Must be: headleas.hlse_ref | - |
| Dmse Ref | UNIT_DMSE_REF | Client Data | Must be: demise.dmse_ref | - |
| Measure Code | UNIT_MEASURE_CODE | Client Data | Must be: codeconv.cdcv_ref with cdcv_cdms_ref = 'USM' | - |
| Space Type | UNIT_SPACE_TYPE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'UST' | - |
| Primary Use | UNIT_PRIMARY_USE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'UOU' | - |
| Alienability Code | UNIT_ALIENABILITY_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ALI' | - |
| User Code | UNIT_USER_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Disabled Access | UNIT_DISABLED_ACCESS | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Exclude from Expense Recovery | UNIT_EX_EXP_REC_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Expense Class | UNIT_ER_CLASS_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ERC' | - |
| Unit Name | UNIT_NAME | Client Data | - | if (:check_1 = True) then (property(:unit_prop_ref).prop_name) |
| Address (Line 1) | UNIT_ADDR_L1 | Client Data | - | if (:check_1 = True) then (property(:unit_prop_ref).prop_addr_l1) |
| Address (Line 2) | UNIT_ADDR_L2 | Client Data | - | if (:check_1 = True) then (property(:unit_prop_ref).prop_addr_l2) |
| Town | UNIT_TOWN | Client Data | - | if (:check_1 = True) then (property(:unit_prop_ref).prop_town) |
| County | UNIT_COUNTY | Client Data | Must be: codesgen.cdgn_desc_long with cdgn_cdty_ref = 'COU' | if (:check_1 = True) then (property(:unit_prop_ref).prop_county) |
| Postcode | UNIT_POSTCODE | Client Data | - | if (:check_1 = True) then (property(:unit_prop_ref).prop_postcode) |
| Country | UNIT_COUNTRY | Client Data | Must be: codesgen.cdgn_desc_long with cdgn_cdty_ref = 'ISO' | if (:check_1 = True) then (property(:unit_prop_ref).prop_country) |
| Floor Ref | UNIT_FLOR_REF | Derived | Must be: floor.flor_ref | if (:unit_flor_floor_code is not Null) then (floor(prop_ref: :unit_prop_ref, floor_code: :unit_flor_floor_code).flor_ref) |
| Entity Usage Code | UNIT_USAGE_CODE | System Default | Usage Code | - |
| Currency Code | UNIT_CUR_CODE | Derived | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUR' | property(:unit_prop_ref).prop_currency_code |
| Country Code | UNIT_COUNTRY_ISO_CODE | Derived | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ISO' | codesgen(cdgn_desc_long = unit_country, cdgn_cdty_ref = 'ISO').cdgn_ref |
| Live In Vts | UNIT_LIVE_IN_VTS | System Default | Must be: Flag: (N)o, (Y)es | - |
| Available From Date | UNIT_AVAIL_DATE | Client Data (Derived if Null) | - | If null....<br>:unit_avail_date_default |
| Tax Recoverable | UNIT_TAX_OPTION_FLAG | Client Data (Derived if Null) | Must be: Flag: (N)o, (Y)es | If null....<br>Nvl((property(:unit_prop_ref).prop_tax_option_flag), 'N') |

### Uniqueness Rules

| Scope | Name | Restriction | Fields |
| --- | --- | --- | --- |
| Maximum | Primary Key | None | UNIT_REF |
| Maximum | UNITI1 | None | UNIT_COMP_REF, UNIT_PROP_REF, UNIT_REF |
| Maximum | UNITI7 | None | UNIT_PRSL_REF, UNIT_PROP_REF, UNIT_REF |
| Maximum | Validation Index 1 | None | UNIT_EXT_REF |

### Fixed-Count Rules

| Scope | Name | Restriction | Required Count | Fields |
| --- | --- | --- | --- | --- |
| Maximum | Fixed-Count Index - Violated if more than one main unit | None | COUNT (UNIT_MAIN_UNIT_FLAG = 'Y') = 0 or 1 | UNIT_DMSE_REF |

## Internal Derived Fields

These fields are calculated or checked internally during processing; they are not intake columns.

| Field | Timing | Derivation |
| --- | --- | --- |
| CHECK_1 | Default | if (All of the following are Null: (:unit_name, :unit_addr_l1, :unit_addr_l2, :unit_town, :unit_county, :unit_postcode, :unit_country)) then True else False |
| DMSE_STATUS_CODE_PROCESS_FLAG | Default | codesgen(cdty_ref: 'DLS', cdgn_ref: (demise(:unit_dmse_ref).dmse_status_code)).cdgn_process_flag |
| TERI_CODE | Default | if (skyconf.skyc_teri_flag = 'Y') then (company(:unit_comp_ref).comp_teri_code) |
| UNIT_AVAIL_DATE_DEFAULT | Default | if (:unit_start_date < Today) then Today else :unit_start_date |
| UNIT_AVAIL_DATE_IN_TEMPLATE | Beginning | :unit_avail_date |
| UNIT_STATUS_CODE_PROCESS_FLAG | Default | codesgen(cdty_ref: 'STA', cdgn_ref: :unit_status_code).cdgn_process_flag |

## Additional Processing Rules

Apply these workbook-defined tasks at the stated processing line or trigger.

| Id | Name | Line | Type | Triggers | Details | Internal Fields | Variables | Variable Calculations |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Default | 0 | Run Condition | - | Always runnable | - | - | - |
| - | Default | 01 | Cursor | - | SELECT unit_dmse_ref, unit_comp_ref, unit_prop_ref, unit_ref, unit_start_date, unit_end_date, qcid<br>FROM unit<br>WHERE qcid IN {unit_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| - | Default | 01.01 | Condition | - | IF ((:unit_dmse_ref is not Null) and (mig_sky_tables('UNITDMSE').skyt_mig_flag <> 'Y')) | - | - | - |
| - | Default | 01.01.01 | Insert | - | INSERT INTO unitdmse:<br>unde_comp_ref = :unit_comp_ref<br>unde_prop_ref = :unit_prop_ref<br>unde_unit_ref = :unit_ref<br>unde_dmse_ref = :unit_dmse_ref<br>unde_start_date = :unit_start_date<br>unde_end_date = :unit_end_date | - | - | - |
| - | Default | 01.02 | Insert | - | INSERT INTO unitoccu:<br>unoc_comp_ref = :unit_comp_ref<br>unoc_prop_ref = :unit_prop_ref<br>unoc_unit_ref = :unit_ref<br>unoc_status_flag = 'V'<br>unoc_start_reason = 'CRV'<br>unoc_start_date = :unit_start_date<br>unoc_end_date = Null<br>unoc_leas_ref = Null<br>unoc_tnnt_ref = Null | - | - | - |
| 32 | Unit Rental Space History | 0 | Run Condition | - | Always runnable | - | - | - |
| 32 | Unit Rental Space History | 01 | Cursor | - | SELECT unit_dmse_ref, unit_prop_ref, unit_ref, unit_start_date, unit_end_date, qcid<br>FROM unit<br>WHERE qcid IN {unit_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 32 | Unit Rental Space History | 01.01 | Condition | - | IF (:unit_dmse_ref is not Null) | - | - | - |
| 32 | Unit Rental Space History | 01.01.01 | Insert | - | INSERT INTO unitdmse:<br>unde_comp_ref = property(:unit_prop_ref).prop_comp_ref<br>unde_prop_ref = :unit_prop_ref<br>unde_unit_ref = :unit_ref<br>unde_dmse_ref = :unit_dmse_ref<br>unde_start_date = :unit_start_date<br>unde_end_date = :unit_end_date<br>WHERE unitdmse record does not exist satisfying:<br>unde_unit_ref = :unit_ref | - | - | - |

## Reference Code Types

Fields whose descriptions identify a code type must contain a value from that code type. The workbook's `Codes` and `LOVs` worksheets provide the corresponding lookup values.

| Code Type | Name | Desc |
| --- | --- | --- |
| ALI | Alienability Status | Alienability Status.<br>PROCESS FLAG 1: Alienable for Investment - The property/land ownership can be transferred by being sold/bought<br>PROCESS FLAG 2: Inalienable - The property/land cannot be bought or sold, usually ownership can only be transferred by inheritance or similar if at all. |
| COU | STATE/COUNTY | State/County |
| CUR | Currency Codes | Currency Codes |
| ERC | Expense Recovery Class | Allows the Expense Recovery WFA rule to be overridden for certain classes of unit. |
| ETY | Element Types | Element Type Codes |
| FLR | Floor Type | Definition of the different levels found within a building. |
| ISO | Country Codes | ISO Standard 2 character Country Codes<br>PROCESS FLAG 2: Auto-allocation of receipts is against Service Charge first followed by Rent.<br>PROCESS FLAG 3: Annual Tax Returns enabled by default. |
| MIM | Maintenance Importance | Maintenance Importance<br>PROCESS FLAG 1 : High<br>PROCESS FLAG 2 : Medium<br>PROCESS FLAG 3 : Low |
| STA | UNIT STATUS | Unit Status:<br>PROCESS FLAG 0: Internally occupied, De-Activated or Disposed.  Excluded when status filtering ON.<br>PROCESS FLAG 1: Occupied; Used when the 'Tenant Move In' process is completed.  Will not be available at the start of the Tenant Move In process.<br>PROCESS FLAG 2: Vacant; Used when the 'Tenant Move Out' process is completed.<br>PROCESS FLAG 9: Provisional; Excluded when status filtering ON. Used during the 'Tenant Move In' process. |
| UOU | Unit Organisation Usage | Usage type of unit by organisation.  Process flag set according to:<br>1 = Vacant<br>2 = Occupied |
| UPS | Unit Physical Sector | Codes for unit physical sectors |
| UST | Unit Space Type | Unit Space Type |
| UT | UNIT TYPE | The type of unit to be defined within a property. For Reporting Purposes<br>PROCESS FLAG 0:<br>Not Available<br>PROCESS FLAG 1:<br>Subtenant type<br>PROCESS FLAG 9:<br>Restricted re Area population - Only Common Area (NEA) may be populated |

---

## Source Notes

* `-` means the workbook cell is blank and does not add a rule or default.
* Validation and derivation expressions are preserved verbatim so implementation-specific PLE functions and field names are not reinterpreted.
* Code descriptions in field rules identify the required lookup family; use the workbook's `Codes` / `LOVs` worksheets or the target PLE database to validate the current allowed values.
* References to related PLE entities require the corresponding table data or target database. If that data is unavailable, report `Warning / REQUIRES DATABASE VERIFICATION` rather than claiming the reference is valid or invalid.
