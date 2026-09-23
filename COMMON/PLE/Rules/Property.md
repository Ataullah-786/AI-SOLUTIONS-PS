# PLE - Property Rules

**Product:** PLE
**Target Table:** `Property`
**Schema File:** `/COMMON/PLE/Schema/Property.json`
**Source Workbook:** `PROPERTY_tem.xlsx`
**Source Worksheet:** `Template`

These rules are taken from the supplied PLE template workbook. They describe how
intake columns must be populated and validated before data is integrated into the PLE `Property` table.

They are **additional to** the structural rules in `/COMMON/PLE/Schema/Property.json`.
Where the workbook and JSON schema disagree on a physical type or length, the JSON
schema remains the source of truth for storage and the rules below define the business/intake expectation.

---

## Field Rules

| Intake Label | PLE Field | Format | Default | Rule / Description | Source | Comment |
| --- | --- | --- | --- | --- | --- | --- |
| Group Ref | PROP_GROP_REF | String(8) | - | Foreign Key - groups | - | - |
| Operation Reference | PROP_COMP_REF | String(8) | - | Foreign Key - company | - | - |
| Site Reference | PROP_HPRP_REF | String(8) | - | Foreign Key - headprop | - | - |
| Parent Ref | PROP_PARENT_REF | String(8) | - | Foreign Key - property. Must Not Be Attached To A Parent Property. Currency And Operation Of Parent Property Must Be Same As The Property. | - | - |
| Property Reference | PROP_REF | String(8) | - | Primary Key. Unique | - | - |
| Sub-Property Flag | PROP_SUB_PROP_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Acquisition Reference | PROP_ACQU_REF | String(8) | - | Foreign Key - acquire | - | - |
| Prsl Ref | PROP_PRSL_REF | String(8) | - | Foreign Key - propsale | - | - |
| Property Name | PROP_NAME | String(60) | - | - | - | - |
| Address (Line 1) | PROP_ADDR_L1 | String(30) | - | - | - | - |
| Address (Line2) | PROP_ADDR_L2 | String(30) | - | - | - | - |
| Town | PROP_TOWN | String(30) | - | - | - | - |
| County | PROP_COUNTY | String(30) | - | Desc of Code of Type: 'COU' (State/Province) | - | - |
| Postcode | PROP_POSTCODE | String(12) | - | - | - | - |
| Country | PROP_COUNTRY | String(30) | - | Desc of Code of Type: 'ISO' (Country Codes) | - | - |
| External Ref | PROP_EXT_REF | String(20) | {PROP_REF} | Unique | - | - |
| Type of Property | PROP_TYPE_CODE | String(3) | - | Code of Type: 'PT' (PROPERTY TYPE) | - | - |
| Asset Type | PROP_ELMT_TYPE | String(3) | - | Code of Type: 'ETY' (Property Element Type) | - | - |
| Tenure | PROP_TENURE_CODE | String(3) | - | Code of Type: 'TNR' (TENURE) | - | - |
| Letting Status | PROP_LET_STATUS_CODE | String(3) | LIV | Code of Type: 'PLS' (LETTING STATUS) | - | - |
| Manager | PROP_MNGR_CODE | String(3) | - | User Code | - | - |
| Surveyor | PROP_SURVEY_CODE | String(3) | - | User Code | - | - |
| Region | PROP_REGION_CODE | String(3) | - | Code of Type: 'REG' (Region Code) | - | - |
| Reporting Category | PROP_REP_CAT_CODE | String(3) | - | Code of Type: 'MSA' (Region Codes) | - | - |
| Property Book Cost | PROP_BOOK_COST | Number(13,2)<br>Min Val: -99999999999.99<br>Max Val: 99999999999.99 | - | - | - | - |
| Comment | PROP_COMMENT | String(1000) | - | - | - | - |
| Plan Name | PROP_PLAN_DESC | String(30) | - | - | - | - |
| Plan Status | PROP_PLAN_CODE | String(3) | - | Code of Type: 'LPS' (LOC PLAN STS) | - | - |
| S106 Agreement | PROP_S106 | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Conservation Area | PROP_CON_AREA | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Listed Building | PROP_LB_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Grade of Listed Building | PROP_LB_CODE | String(3) | - | Code of Type: 'LIB' (LISTED BLDG). NULL If Listed Building Is N | - | - |
| Obligations - Insurance | PROP_OBLG_INSR_CODE | String(3) | - | Code of Type: 'OBL' (Clause Obligations) | - | - |
| Obligations - Rating | PROP_OBLG_RATE_CODE | String(3) | - | Code of Type: 'OBL' (Clause Obligations) | - | - |
| Obligations - Internal Repairs | PROP_OBLG_INTR_CODE | String(3) | - | Code of Type: 'OBL' (Clause Obligations) | - | - |
| Obligations - External Repairs | PROP_OBLG_EXTN_CODE | String(3) | - | Code of Type: 'OBL' (Clause Obligations) | - | - |
| Local Auth Supplier Ref | PROP_LOCAL_AUTH_SUPP_REF | String(8) | - | Foreign Key - supplier. Supllier Must Be A Local Authority | - | - |
| Measure Code | PROP_MEASURE_CODE | String(3) | - | Measurement Code | - | - |
| NIA | PROP_NIA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Gross Internal Area | PROP_GIA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Area | PROP_NEA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Gross External Area | PROP_GEA | Number(10,2)<br>Min Val: 0<br>Max Val: 9999999.99 | - | NULL If Measure Code Is NULL | - | - |
| Cad Ref | PROP_CAD_REF | String(50) | - | - | - | - |
| Cad Area | PROP_CAD_AREA | Number | - | - | - | - |
| Construction Year | PROP_CNSTR_DATE | Number(4)<br>Min Val: 0<br>Max Val: 9999 | - | - | - | - |
| Expected Life (Years) | PROP_EXPECT_LIFE | Number(4)<br>Min Val: 0<br>Max Val: 9999 | - | - | - | - |
| Parking Spaces | PROP_CAR_PARK_SPACES | Number(5)<br>Min Val: 0<br>Max Val: 99999 | - | - | - | - |
| Disabled Access | PROP_DISABLED_ACCESS | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Mortgage Ala | PROP_MORT_ALA | Number(13,2)<br>Min Val: 0<br>Max Val: 99999999999.99 | - | - | - | - |
| Mortgage Rel Amount | PROP_MORT_REL_AMT | Number(13,2)<br>Min Val: 0<br>Max Val: 99999999999.99 | - | - | - | - |
| Mortgage Rel Prem | PROP_MORT_REL_PREM | Number(8,5)<br>Min Val: 0<br>Max Val: 99.99999 | - | - | - | - |
| Alternative Reference | PROP_EXT_REF2 | String(20) | - | - | - | - |
| Latitude | PROP_LATITUDE | Number(13,10)<br>Min Val: -90.0000000000<br>Max Val: 90.0000000000 | - | - | - | - |
| Longitude | PROP_LONGITUDE | Number(13,10)<br>Min Val: -180.0000000000<br>Max Val: 180.0000000000 | - | - | - | - |
| Ranl Recharge Type | PROP_RANL_RECHARGE_TYPE | String(3) | - | Code of Type: 'PRM' (Property Recharge Model) | - | - |
| Rate Freq Code | PROP_RATE_FREQ_CODE | String(3) | - | Frequency Code. Mandatory if Skyc_Review_Flag is R else ANN | - | - |
| Public Holiday | PROP_PBLC_HLDY_CODE | String(3) | - | Code of Type: 'PHC' (Business Day Country) | - | - |
| Invoice Message | PROP_MESS | String(100)<br>Max Len: 100 | - | - | - | - |
| Regular Task End Date | PROP_RTSU_END_DATE | Date | - | - | - | - |
| Importance | PROP_IMP_CODE | String(3) | - | Code of Type: 'MIM' (Maintenance Importance). For future use by FM | - | - |
| Working Week | PROP_WOWE_CODE | String(3) | - | Code of Type: 'WOW' (Working Week) | - | - |
| Organisation Ref | PROP_ORGN_REF | String(8) | - | Foreign Key - organisation | - | - |
| Export to VTS | PROP_EXPORT_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Accounting Status | PROP_STATUS_CODE | String(3) | LIV | Code of Type: 'PS' (ACCT STATUS) | - | - |
| Currency | PROP_CURRENCY_CODE | String(3) | {System Currency Code} | Code of Type: 'CUR' (Currency Codes) | - | - |
| Contracted Currency | PROP_CONT_CURR_CODE | String(3) | {System Currency Code} | Code of Type: 'CUR' (Currency Codes) | - | - |
| Tax Option Taken | PROP_TAX_OPTION_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Tax Date | PROP_TAX_OPTION_DATE | Date | - | Mandatory If Tax Option Is Y Else NULL. Must Be On Or After 1st August 1989. | - | - |
| Third Party Bank Ref | PROP_THIRD_PARTY_BANK_REF | String(8) | - | Foreign Key - bankac | - | - |
| Mixed Use | PROP_MIXED_USE_FLAG | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Invoice Approval Value | PROP_INV_NET_GROSS_FLAG | String(1) | N | Flag: (G)ross, (N)et of VAT | - | - |
| SC Frequency Code | PROP_SC_FRQ_CODE | String(3) | - | Frequency Code | - | - |
| S/C From Date | PROP_SC_FRM_DATE | Date | - | Mandatory If S/C Freq Code Is Not NULL Else NULL | - | - |
| Schedule Type 1 | PROP_SCHEDULE_TYPE | String(3) | - | Foreign Key - exprecanal | - | - |
| On Account Frequency 1 | PROP_ON_AC_FRQ_CODE | String(3) | - | Frequency Code | - | - |
| On Acc Rule | PROP_ON_ACC_RULE | String(1) | T | Flag: (F)rom Date, (T)o Date | - | - |
| Landlord Liability Tenant Ref | PROP_SC_VOID_TNNT_REF | String(8) | - | Foreign Key - tenant | - | - |
| Expense Rec Annual Tax Return | PROP_SC_ANN_TAX_FLAG | String(1) | N | Flag: (N)o, (Y)es. Defualts to Y if Country requires Annual Tax Returns to be enabled by default | - | - |
| On Acct Standard VAT Flg | PROP_ON_AC_STD_VAT_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Mandatory Recovery by Schedule | PROP_MAN_REC_SU_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Tantieme Flag | PROP_TANTIEME_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Shares By Percentage | PROP_SC_PERCENT_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Wfa Rule Code | PROP_WFA_RULE_CODE | String(3) | - | Code of Type: 'WFC' (WFA Calculation Rule). Must be Null if Shares By Percentage is Y | - | - |
| Schedule Type 2 | PROP_SCHEDULE_TYPE2 | String(3) | - | Foreign Key - exprecanal | - | - |
| On Account Frequency 2 | PROP_ON_AC_FRQ_CODE2 | String(3) | - | Frequency Code | - | - |
| Shares By Percentage 2 | PROP_SC_PERCENT_FLAG2 | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Wfa Rule Code2 | PROP_WFA_RULE_CODE2 | String(3) | - | Code of Type: 'WFC' (WFA Calculation Rule). Must be Null if Shares By Percentage 2 is Y | - | - |
| Schedule Type 3 | PROP_SCHEDULE_TYPE3 | String(3) | - | Foreign Key - exprecanal | - | - |
| On Account Frequency 3 | PROP_ON_AC_FRQ_CODE3 | String(3) | - | Frequency Code | - | - |
| Shares By Percentage 3 | PROP_SC_PERCENT_FLAG3 | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Wfa Rule Code3 | PROP_WFA_RULE_CODE3 | String(3) | - | Code of Type: 'WFC' (WFA Calculation Rule). Must be Null if Shares By Percentage 3 is Y | - | - |
| Schedule Type 4 | PROP_SCHEDULE_TYPE4 | String(3) | - | Foreign Key - exprecanal | - | - |
| On Account Frequency 4 | PROP_ON_AC_FRQ_CODE4 | String(3) | - | Frequency Code | - | - |
| Shares By Percentage 4 | PROP_SC_PERCENT_FLAG4 | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Wfa Rule Code4 | PROP_WFA_RULE_CODE4 | String(3) | - | Code of Type: 'WFC' (WFA Calculation Rule). Must be Null if Shares By Percentage 4 is Y | - | - |
| Schedule Type 5 | PROP_SCHEDULE_TYPE5 | String(3) | - | Foreign Key - exprecanal | - | - |
| On Account Frequency 5 | PROP_ON_AC_FRQ_CODE5 | String(3) | - | Frequency Code | - | - |
| Shares By Percentage 5 | PROP_SC_PERCENT_FLAG5 | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Wfa Rule Code5 | PROP_WFA_RULE_CODE5 | String(3) | - | Code of Type: 'WFC' (WFA Calculation Rule). Must be Null if Shares By Percentage 5 is Y | - | - |
| Mortgage Flag | PROP_MORTGAGE_FLAG | String(1) | N | Flag: (M)ortgaged, (N)ot Morgaged | - | - |
| Maintain Funding Accounts at Property Level | PROP_BANK_ACCTS_FLAG | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Retain VAT Flag | PROP_RETAIN_VAT_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Allow Approval of Unreconciled Invoices | PROP_APP_UNRECONCILED_INV | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Unit Trial Balance | PROP_UNIT_TB_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Create Overhead Unit | CREATE_OVERHEAD_UNIT | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Overhead Unit Ref | PROP_OVERHEAD_UNIT_REF | String(8) | - | Unit Ref (see: Additional Task 50 for validation logic) | - | - |
| Default EFT Cash Account | PROP_DFLT_EFT_BANK_REF | String(8) | - | Foreign Key - bankac | - | - |
| Revaluation Calculation Level | PROP_REVAL_LEVEL_FLAG | String(1) | P | (P)roperty), (U)nit | - | - |
| Aggregate Journals at Property Level | PROP_REVAL_AGGREGATE_FLAG | String(1) | N | Flag: (N)o, (Y)es. Only applicable if Reval Calc Level is U | - | - |
| SLM Site Code | PROP_SLM_SITE_CODE | String(10) | - | - | - | - |
| SLM Town Code | PROP_SLM_TOWN_ID | String(8) | - | - | - | - |
| SLM Location Code | PROP_SLM_LOCATION_ID | String(8) | - | - | - | - |

---

## Validation Rules

### Table-Level Validations

Each expression identifies the condition that makes a row invalid. Report the workbook's stated message when the expression evaluates to true.

| Message | Validation |
| --- | --- |
| Area Fields should be null when Measure code is null | invalid if (:prop_measure_code is Null) and ((:prop_nia is not Null) or (:prop_nea is not Null) or (:prop_gia is not Null) or (:prop_gea is not Null)) |
| Currency of Landlord Liability Tenant must be same as currency of Property | invalid if (:prop_sc_void_tnnt_ref is not Null) and (tenant(:prop_sc_void_tnnt_ref).tnnt_cur_code <> :prop_currency_code) |
| Currency, Operation and Group of Parent Property must be same as the Property | invalid if (:prop_parent_ref is not Null) and (property(:prop_parent_ref).prop_currency_code <> :prop_currency_code or property(:prop_parent_ref).prop_comp_ref <> :prop_comp_ref or property(:prop_parent_ref).prop_grop_ref <> :prop_grop_ref) |
| Expense Recovery End Date is before Start Date | invalid if (:prop_sc_frq_code is not Null) and (:prop_sc_to_date < :prop_sc_frm_date) |
| Expense Recovery is not set, but Expense Recovery End Date is not blank | invalid if (:prop_sc_frq_code is Null) and (:prop_sc_to_date is not Null) |
| Expense Recovery is not set, but Expense Recovery Start Date is not blank | invalid if (:prop_sc_frq_code is Null) and (:prop_sc_frm_date is not Null) |
| Expense Recovery is set, but 1st Schedule Type is blank | invalid if (:prop_sc_frq_code is not Null) and (:prop_schedule_type is Null) |
| Expense Recovery is set, but Expense Recovery End Date is blank | invalid if (:prop_sc_frq_code is not Null) and (:prop_sc_to_date is Null) |
| Expense Recovery is set, but Expense Recovery Start Date is blank | invalid if (:prop_sc_frq_code is not Null) and (:prop_sc_frm_date is Null) |
| Invalid From Date for Frequency | invalid if (:prop_sc_frm_date is not Null) and (:prop_sc_frq_code is not Null) and (:prop_sc_frm_date is not a valid start date for frequancy code: :prop_sc_frq_code) |
| Invalid Local Authority Reference | invalid if (:prop_local_auth_supp_ref is not Null) and (supplier(:prop_local_auth_supp_ref).supp_local_auth_flag = 'N') |
| Landlord Liability Tenant must be a valid non-lease tenant | invalid if (:prop_sc_void_tnnt_ref is not Null) and (tenant(:prop_sc_void_tnnt_ref).tnnt_valid_demands not in ('B', 'N')) |
| Landlord Liability Tenant must be active for Property's Operation if operational security enabled | invalid if (skyconf.skyc_comp_sec = 'Y') and (tnntcomp(tnnt_ref: :prop_sc_void_tnnt_ref, comp_ref: :prop_comp_ref, active: 'Y').Inexistent) |
| Landlord Liability Tenant must be Current or Provisional | invalid if (tenant(:prop_sc_void_tnnt_ref).tnnt_status_code is not Null) and (codesgen(cdty_ref: 'TES', cdgn_ref: (tenant(:prop_sc_void_tnnt_ref).tnnt_status_code)).cdgn_process_flag not in (1, 9)) |
| Listed Building is not set, but LB Grade is not blank | invalid if (NVL(:prop_lb_flag, 'N') = 'N') and (:prop_lb_code is not Null) |
| Overhead Unit cannot be created if Auto Gen of Overhead Unit from Property is not enabled | invalid if (:create_overhead_unit = 'Y') and (skyconf.skyc_unit_overhead_auto_gen <> 'Y') |
| Overhead Unit cannot be created if auto-referencing is not enabled for Units | invalid if (:create_overhead_unit = 'Y') and (autoref('UNI').auto_active <> 'Y') |
| Parent Property is aleady itself attached to a Parent Property | invalid if (:prop_parent_ref is not Null) and (property(ref: :prop_parent_ref, parent_ref not null).Existent) |
| prop_app_unreconciled_inv must be Y if Create Actual Transactions is checked on Integrations Administration screen | invalid if (:prop_app_unreconciled_inv = 'N') and (skyconf.skyc_scanning_trans_flag = 'Y') |
| prop_dflt_eft_bank_ref cannot be used in the context of this Property | invalid if (:prop_dflt_eft_bank_ref is not Null) and (not (((bankcomp(bank_ref: :prop_dflt_eft_bank_ref, comp_ref: :prop_comp_ref).Existent is True) and (bankgrop(bank_ref: :prop_dflt_eft_bank_ref, grop_ref: :prop_grop_ref).Existent is True)) or (:prop_dflt_eft_bank_ref in (:bcgp_deb_ac_ref, :bcgp_pay_ac_ref, :bcgp_deb_sac_ref, :bcgp_deb_rac_ref)))) |
| prop_on_ac_frq_code must be a recurring frequency | invalid if codefreq(code: :prop_on_ac_frq_code, type_flag: N, add_months: 0, add_days: 0).Existent or codefreq(code: :prop_on_ac_frq_code, type_flag: Y, (valid_months: Null or valid_days: Null or prev_seq_num: Null or next_seq_num: Null or freq_count: Null)).Existent |
| prop_on_ac_frq_code must be null if prop_sc_frq_code is null | invalid if (:prop_on_ac_frq_code is not Null) and (:prop_sc_frq_code is Null) |
| prop_on_ac_frq_code must be null if the 1st Schedule Type is null, or the 1st Tenant On Account and Landlord Liability On Account Analysis Codes are both null | invalid if (:prop_on_ac_frq_code is not Null) and ((:prop_schedule_type is Null) or ((exprecanal(:prop_schedule_type).eran_on_ac_cdmj_ref is Null) and (exprecanal(:prop_schedule_type).eran_void_on_ac_cdmj_ref is Null))) |
| prop_on_ac_frq_code2 must be a recurring frequency | invalid if codefreq(code: :prop_on_ac_frq_code2, type_flag: N, add_months: 0, add_days: 0).Existent or codefreq(code: :prop_on_ac_frq_code2, type_flag: Y, (valid_months: Null or valid_days: Null or prev_seq_num: Null or next_seq_num: Null or freq_count: Null)).Existent |
| prop_on_ac_frq_code2 must be null if prop_sc_frq_code is null | invalid if (:prop_on_ac_frq_code2 is not Null) and (:prop_sc_frq_code is Null) |
| prop_on_ac_frq_code2 must be null if the 2nd Schedule Type is null, or the 2nd Tenant On Account and Landlord Liability On Account Analysis Codes are both null | invalid if (:prop_on_ac_frq_code2 is not Null) and ((:prop_schedule_type2 is Null) or ((exprecanal(:prop_schedule_type2).eran_on_ac_cdmj_ref is Null) and (exprecanal(:prop_schedule_type2).eran_void_on_ac_cdmj_ref is Null))) |
| prop_on_ac_frq_code3 must be a recurring frequency | invalid if codefreq(code: :prop_on_ac_frq_code3, type_flag: N, add_months: 0, add_days: 0).Existent or codefreq(code: :prop_on_ac_frq_code3, type_flag: Y, (valid_months: Null or valid_days: Null or prev_seq_num: Null or next_seq_num: Null or freq_count: Null)).Existent |
| prop_on_ac_frq_code3 must be null if prop_sc_frq_code is null | invalid if (:prop_on_ac_frq_code3 is not Null) and (:prop_sc_frq_code is Null) |
| prop_on_ac_frq_code3 must be null if the 3rd Schedule Type is null, or the 3rd Tenant On Account and Landlord Liability On Account Analysis Codes are both null | invalid if (:prop_on_ac_frq_code3 is not Null) and ((:prop_schedule_type3 is Null) or ((exprecanal(:prop_schedule_type3).eran_on_ac_cdmj_ref is Null) and (exprecanal(:prop_schedule_type3).eran_void_on_ac_cdmj_ref is Null))) |
| prop_on_ac_frq_code4 must be a recurring frequency | invalid if codefreq(code: :prop_on_ac_frq_code4, type_flag: N, add_months: 0, add_days: 0).Existent or codefreq(code: :prop_on_ac_frq_code4, type_flag: Y, (valid_months: Null or valid_days: Null or prev_seq_num: Null or next_seq_num: Null or freq_count: Null)).Existent |
| prop_on_ac_frq_code4 must be null if prop_sc_frq_code is null | invalid if (:prop_on_ac_frq_code4 is not Null) and (:prop_sc_frq_code is Null) |
| prop_on_ac_frq_code4 must be null if the 4th Schedule Type is null, or the 4th Tenant On Account and Landlord Liability On Account Analysis Codes are both null | invalid if (:prop_on_ac_frq_code4 is not Null) and ((:prop_schedule_type4 is Null) or ((exprecanal(:prop_schedule_type4).eran_on_ac_cdmj_ref is Null) and (exprecanal(:prop_schedule_type4).eran_void_on_ac_cdmj_ref is Null))) |
| prop_on_ac_frq_code5 must be a recurring frequency | invalid if codefreq(code: :prop_on_ac_frq_code5, type_flag: N, add_months: 0, add_days: 0).Existent or codefreq(code: :prop_on_ac_frq_code5, type_flag: Y, (valid_months: Null or valid_days: Null or prev_seq_num: Null or next_seq_num: Null or freq_count: Null)).Existent |
| prop_on_ac_frq_code5 must be null if prop_sc_frq_code is null | invalid if (:prop_on_ac_frq_code5 is not Null) and (:prop_sc_frq_code is Null) |
| prop_on_ac_frq_code5 must be null if the 5th Schedule Type is null, or the 5th Tenant On Account and Landlord Liability On Account Analysis Codes are both null | invalid if (:prop_on_ac_frq_code5 is not Null) and ((:prop_schedule_type5 is Null) or ((exprecanal(:prop_schedule_type5).eran_on_ac_cdmj_ref is Null) and (exprecanal(:prop_schedule_type5).eran_void_on_ac_cdmj_ref is Null))) |
| prop_on_ac_std_vat_flag cannot be Y if prop_sc_ann_tax_flag is not Y | invalid if (:prop_on_ac_std_vat_flag = 'Y') and (:prop_sc_ann_tax_flag <> 'Y') |
| prop_overhead_unit_ref cannot be entered if create_overhead_unit is Y | invalid if (:prop_overhead_unit_ref is not Null) and (:create_overhead_unit = 'Y') |
| prop_ref contains prohibited characters | invalid if (:prop_ref is not Null) and (:prop_ref matches Regex('[^a-zA-Z0-9/.:%!$*_+&^-]')) |
| prop_reval_aggregate_flag cannot be Y if prop_reval_level_flag is not U | invalid if (:prop_reval_level_flag <> 'U') and (:prop_reval_aggregate_flag = 'Y') |
| prop_rtsu_end_date must be equal to Parent Property's Regular Task End Date if it is not null | invalid if (:parent_rtsu_end_date is not Null) and (:prop_rtsu_end_date <> :parent_rtsu_end_date) |
| prop_sc_percent_flag must be N if prop_schedule_type is null | invalid if (:prop_sc_percent_flag <> 'N') and (:prop_tantieme_flag = 'N') and (:prop_schedule_type is Null) |
| prop_sc_percent_flag must be N if prop_tantieme_flag is Y | invalid if (:prop_sc_percent_flag <> 'N') and (:prop_tantieme_flag = 'Y') |
| prop_sc_percent_flag2 must be N if prop_schedule_type2 is null | invalid if (:prop_sc_percent_flag2 <> 'N') and (:prop_tantieme_flag = 'N') and (:prop_schedule_type2 is Null) |
| prop_sc_percent_flag2 must be N if prop_tantieme_flag is Y | invalid if (:prop_sc_percent_flag2 <> 'N') and (:prop_tantieme_flag = 'Y') |
| prop_sc_percent_flag3 must be N if prop_schedule_type3 is null | invalid if (:prop_sc_percent_flag3 <> 'N') and (:prop_tantieme_flag = 'N') and (:prop_schedule_type3 is Null) |
| prop_sc_percent_flag3 must be N if prop_tantieme_flag is Y | invalid if (:prop_sc_percent_flag3 <> 'N') and (:prop_tantieme_flag = 'Y') |
| prop_sc_percent_flag4 must be N if prop_schedule_type4 is null | invalid if (:prop_sc_percent_flag4 <> 'N') and (:prop_tantieme_flag = 'N') and (:prop_schedule_type4 is Null) |
| prop_sc_percent_flag4 must be N if prop_tantieme_flag is Y | invalid if (:prop_sc_percent_flag4 <> 'N') and (:prop_tantieme_flag = 'Y') |
| prop_sc_percent_flag5 must be N if prop_schedule_type5 is null | invalid if (:prop_sc_percent_flag5 <> 'N') and (:prop_tantieme_flag = 'N') and (:prop_schedule_type5 is Null) |
| prop_sc_percent_flag5 must be N if prop_tantieme_flag is Y | invalid if (:prop_sc_percent_flag5 <> 'N') and (:prop_tantieme_flag = 'Y') |
| prop_schedule_type and prop_schedule_type2 must be different | invalid if :prop_schedule_type = :prop_schedule_type2 |
| prop_schedule_type and prop_schedule_type3 must be different | invalid if :prop_schedule_type = :prop_schedule_type3 |
| prop_schedule_type and prop_schedule_type4 must be different | invalid if :prop_schedule_type = :prop_schedule_type4 |
| prop_schedule_type and prop_schedule_type5 must be different | invalid if :prop_schedule_type = :prop_schedule_type5 |
| prop_schedule_type must be null if prop_sc_frq_code is null | invalid if (:prop_schedule_type is not Null) and (:prop_sc_frq_code is Null) |
| prop_schedule_type2 and prop_schedule_type3 must be different | invalid if :prop_schedule_type2 = :prop_schedule_type3 |
| prop_schedule_type2 and prop_schedule_type4 must be different | invalid if :prop_schedule_type2 = :prop_schedule_type4 |
| prop_schedule_type2 and prop_schedule_type5 must be different | invalid if :prop_schedule_type2 = :prop_schedule_type5 |
| prop_schedule_type2 must be null if prop_sc_frq_code is null | invalid if (:prop_schedule_type2 is not Null) and (:prop_sc_frq_code is Null) |
| prop_schedule_type3 and prop_schedule_type4 must be different | invalid if :prop_schedule_type3 = :prop_schedule_type4 |
| prop_schedule_type3 and prop_schedule_type5 must be different | invalid if :prop_schedule_type3 = :prop_schedule_type5 |
| prop_schedule_type3 must be null if prop_sc_frq_code is null | invalid if (:prop_schedule_type3 is not Null) and (:prop_sc_frq_code is Null) |
| prop_schedule_type4 and prop_schedule_type5 must be different | invalid if :prop_schedule_type4 = :prop_schedule_type5 |
| prop_schedule_type4 must be null if prop_sc_frq_code is null | invalid if (:prop_schedule_type4 is not Null) and (:prop_sc_frq_code is Null) |
| prop_schedule_type5 must be null if prop_sc_frq_code is null | invalid if (:prop_schedule_type5 is not Null) and (:prop_sc_frq_code is Null) |
| prop_slm_location_id must not be populated if skyc_slm_interface is not Y | invalid if (NVL(skyconf.skyc_slm_interface, 'N') = 'N') and (:prop_slm_location_id is not Null) |
| prop_slm_site_code must not be populated if skyc_slm_interface is not Y | invalid if (NVL(skyconf.skyc_slm_interface, 'N') = 'N') and (:prop_slm_site_code is not Null) |
| prop_slm_town_id must not be populated if skyc_slm_interface is not Y | invalid if (NVL(skyconf.skyc_slm_interface, 'N') = 'N') and (:prop_slm_town_id is not Null) |
| prop_sub_prop_flag must be Y if prop_parent_ref is not null | invalid if (:prop_parent_ref is not Null) and (:prop_sub_prop_flag <> 'Y') |
| prop_unit_tb_flag cannot be Y if Unit Trial Balancing is not enabled | invalid if (:prop_unit_tb_flag = 'Y') and (skyconf.skyc_unit_trial_bal <> 'Y') |
| prop_wfa_rule_code must be null if prop_schedule_type is null | invalid if (:prop_wfa_rule_code is not Null) and (:prop_tantieme_flag = 'Y') and (:prop_schedule_type is Null) |
| prop_wfa_rule_code must be null if prop_tantieme_flag is N | invalid if (:prop_wfa_rule_code is not Null) and (:prop_tantieme_flag = 'N') |
| prop_wfa_rule_code should be null when corresponding Shares By % flag is Y | invalid if (:prop_sc_percent_flag = 'Y') and (:prop_wfa_rule_code is not Null) |
| prop_wfa_rule_code2 must be null if prop_schedule_type2 is null | invalid if (:prop_wfa_rule_code2 is not Null) and (:prop_tantieme_flag = 'Y') and (:prop_schedule_type2 is Null) |
| prop_wfa_rule_code2 must be null if prop_tantieme_flag is N | invalid if (:prop_wfa_rule_code2 is not Null) and (:prop_tantieme_flag = 'N') |
| prop_wfa_rule_code2 should be null when corresponding Shares By % flag is Y | invalid if (:prop_sc_percent_flag2 = 'Y') and (:prop_wfa_rule_code2 is not Null) |
| prop_wfa_rule_code3 must be null if prop_schedule_type3 is null | invalid if (:prop_wfa_rule_code3 is not Null) and (:prop_tantieme_flag = 'Y') and (:prop_schedule_type3 is Null) |
| prop_wfa_rule_code3 must be null if prop_tantieme_flag is N | invalid if (:prop_wfa_rule_code3 is not Null) and (:prop_tantieme_flag = 'N') |
| prop_wfa_rule_code3 should be null when corresponding Shares By % flag is Y | invalid if (:prop_sc_percent_flag3 = 'Y') and (:prop_wfa_rule_code3 is not Null) |
| prop_wfa_rule_code4 must be null if prop_schedule_type4 is null | invalid if (:prop_wfa_rule_code4 is not Null) and (:prop_tantieme_flag = 'Y') and (:prop_schedule_type4 is Null) |
| prop_wfa_rule_code4 must be null if prop_tantieme_flag is N | invalid if (:prop_wfa_rule_code4 is not Null) and (:prop_tantieme_flag = 'N') |
| prop_wfa_rule_code4 should be null when corresponding Shares By % flag is Y | invalid if (:prop_sc_percent_flag4 = 'Y') and (:prop_wfa_rule_code4 is not Null) |
| prop_wfa_rule_code5 must be null if prop_schedule_type5 is null | invalid if (:prop_wfa_rule_code5 is not Null) and (:prop_tantieme_flag = 'Y') and (:prop_schedule_type5 is Null) |
| prop_wfa_rule_code5 must be null if prop_tantieme_flag is N | invalid if (:prop_wfa_rule_code5 is not Null) and (:prop_tantieme_flag = 'N') |
| prop_wfa_rule_code5 should be null when corresponding Shares By % flag is Y | invalid if (:prop_sc_percent_flag5 = 'Y') and (:prop_wfa_rule_code5 is not Null) |
| Rate Freq Code is Mandatory when System Review type is R | invalid if (skyconf.skyc_review_flag = 'R') and (:prop_rate_freq_code is Null) |
| Tax Option not taken, but Tax Date is not blank | invalid if (NVL(:prop_tax_option_flag, 'N') = 'N') and (:prop_tax_option_date is not Null) |
| Tax Option taken, but Tax Date is blank | invalid if (:prop_tax_option_flag = 'Y') and (:prop_tax_option_date is Null) |

### Field-Level Validation and Derivation

| Label | PLE Field | Mode | Validation | Derivation |
| --- | --- | --- | --- | --- |
| Group Ref | PROP_GROP_REF | Client Data | Must be: groups.grop_ref | - |
| Operation Reference | PROP_COMP_REF | Client Data | Must be: company.comp_ref | - |
| Site Reference | PROP_HPRP_REF | Client Data | Must be: headprop.hprp_ref | - |
| Parent Ref | PROP_PARENT_REF | Client Data | Must be: property.prop_ref | - |
| Property Reference | PROP_REF | Client Data | Primary Key: property.prop_ref | - |
| Sub-Property Flag | PROP_SUB_PROP_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Acquisition Reference | PROP_ACQU_REF | Client Data | Must be: acquire.acqu_ref with acquire.acqu_comp_ref = prop_comp_ref | - |
| Prsl Ref | PROP_PRSL_REF | Client Data | Must be: propsale.prsl_ref | - |
| County | PROP_COUNTY | Client Data | Must be: codesgen.cdgn_desc_long with cdgn_cdty_ref = 'COU' | - |
| Country | PROP_COUNTRY | Client Data | Must be: codesgen.cdgn_desc_long with cdgn_cdty_ref = 'ISO' | - |
| Type of Property | PROP_TYPE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'PT' | - |
| Asset Type | PROP_ELMT_TYPE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ETY' | - |
| Tenure | PROP_TENURE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'TNR' | - |
| Letting Status | PROP_LET_STATUS_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'PLS' | - |
| Manager | PROP_MNGR_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Surveyor | PROP_SURVEY_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Region | PROP_REGION_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'REG' | - |
| Reporting Category | PROP_REP_CAT_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'MSA' | - |
| Plan Status | PROP_PLAN_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LPS' | - |
| S106 Agreement | PROP_S106 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Conservation Area | PROP_CON_AREA | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Listed Building | PROP_LB_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Grade of Listed Building | PROP_LB_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LIB' | - |
| Obligations - Insurance | PROP_OBLG_INSR_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'OBL' | - |
| Obligations - Rating | PROP_OBLG_RATE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'OBL' | - |
| Obligations - Internal Repairs | PROP_OBLG_INTR_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'OBL' | - |
| Obligations - External Repairs | PROP_OBLG_EXTN_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'OBL' | - |
| Local Auth Supplier Ref | PROP_LOCAL_AUTH_SUPP_REF | Client Data | Must be: supplier.supp_ref | - |
| Measure Code | PROP_MEASURE_CODE | Client Data | Must be: codeconv.cdcv_ref with cdcv_cdms_ref = 'USM' | - |
| Disabled Access | PROP_DISABLED_ACCESS | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Ranl Recharge Type | PROP_RANL_RECHARGE_TYPE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'PRM' | - |
| Rate Freq Code | PROP_RATE_FREQ_CODE | Client Data | Must be: codefreq.cdfq_code | if (skyconf.skyc_review_flag <> 'R') then 'ANN' |
| Public Holiday | PROP_PBLC_HLDY_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'PHC' | - |
| Regular Task End Date | PROP_RTSU_END_DATE | Client Data (Derived if Null) | - | If null....<br>:parent_rtsu_end_date |
| Importance | PROP_IMP_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'MIM' | - |
| Working Week | PROP_WOWE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'WOW' | - |
| Organisation Ref | PROP_ORGN_REF | Client Data | Must be: organisation.orgn_ref | - |
| Export to VTS | PROP_EXPORT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Accounting Status | PROP_STATUS_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'PS' | - |
| Currency | PROP_CURRENCY_CODE | Client Data (Derived if Null) | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUR' | If null....<br>if ((mig_config.mcfg_dflt_cur_code) = 'CONTEXT') then ((groups(:prop_grop_ref).grop_cur_code)) else ((mig_config.mcfg_dflt_cur_code)) |
| Contracted Currency | PROP_CONT_CURR_CODE | Client Data (Derived if Null) | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUR' | If null....<br>if ((mig_config.mcfg_dflt_cont_curr_code) = 'CONTEXT') then ((groups(:prop_grop_ref).grop_cur_code)) else ((mig_config.mcfg_dflt_cont_curr_code)) |
| Tax Option Taken | PROP_TAX_OPTION_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Third Party Bank Ref | PROP_THIRD_PARTY_BANK_REF | Client Data | Must be: bankac.bank_ref | - |
| Mixed Use | PROP_MIXED_USE_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Mandatory PO on Invoice | PROP_PO_REQUIRED | Derived | Must be: Flag: (N)o, (Y)es | skyconf.skyc_po_required |
| Invoice Approval Value | PROP_INV_NET_GROSS_FLAG | Client Data | Must be: Flag: (G)ross, (N)et of VAT | - |
| SC Frequency Code | PROP_SC_FRQ_CODE | Client Data | Must be: codefreq.cdfq_code | - |
| S/C  To Date | PROP_SC_TO_DATE | Derived | - | (Day before :prop_sc_nxt_date) |
| Use Paid Amts Only in Bal Calc | PROP_EXP_REC_PAID_FLAG | System Default | Must be: Flag: (N)o, (Y)es | - |
| Schedule Type 1 | PROP_SCHEDULE_TYPE | Client Data | Must be: exprecanal.eran_schedule_type | - |
| On Account Frequency 1 | PROP_ON_AC_FRQ_CODE | Client Data | Must be: codefreq.cdfq_code | - |
| On Acc Rule | PROP_ON_ACC_RULE | Client Data | Must be: Flag: (F)rom Date, (T)o Date | - |
| SC Next Due Date | PROP_SC_NXT_DATE | Derived | - | if ((:prop_sc_frm_date is not Null) and (:prop_sc_frq_code is not Null)) then (Period(Date: :prop_sc_frm_date, freq_code: :prop_sc_frq_code).Next.From_Date) |
| Landlord Liability Tenant Ref | PROP_SC_VOID_TNNT_REF | Client Data | Must be: tenant.tnnt_ref | - |
| Expense Rec Annual Tax Return | PROP_SC_ANN_TAX_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | if (codesgen(cdty_ref: 'ISO', cdgn_ref: :prop_country_iso_code).cdgn_process_flag = 3) then 'Y' |
| On Acct Standard VAT Flg | PROP_ON_AC_STD_VAT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Mandatory Recovery by Schedule | PROP_MAN_REC_SU_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Tantieme Flag | PROP_TANTIEME_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Shares By Percentage | PROP_SC_PERCENT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Wfa Rule Code | PROP_WFA_RULE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'WFC' | - |
| Schedule Type 2 | PROP_SCHEDULE_TYPE2 | Client Data | Must be: exprecanal.eran_schedule_type | - |
| On Account Frequency 2 | PROP_ON_AC_FRQ_CODE2 | Client Data | Must be: codefreq.cdfq_code | - |
| Shares By Percentage 2 | PROP_SC_PERCENT_FLAG2 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Wfa Rule Code2 | PROP_WFA_RULE_CODE2 | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'WFC' | - |
| Schedule Type 3 | PROP_SCHEDULE_TYPE3 | Client Data | Must be: exprecanal.eran_schedule_type | - |
| On Account Frequency 3 | PROP_ON_AC_FRQ_CODE3 | Client Data | Must be: codefreq.cdfq_code | - |
| Shares By Percentage 3 | PROP_SC_PERCENT_FLAG3 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Wfa Rule Code3 | PROP_WFA_RULE_CODE3 | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'WFC' | - |
| Schedule Type 4 | PROP_SCHEDULE_TYPE4 | Client Data | Must be: exprecanal.eran_schedule_type | - |
| On Account Frequency 4 | PROP_ON_AC_FRQ_CODE4 | Client Data | Must be: codefreq.cdfq_code | - |
| Shares By Percentage 4 | PROP_SC_PERCENT_FLAG4 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Wfa Rule Code4 | PROP_WFA_RULE_CODE4 | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'WFC' | - |
| Schedule Type 5 | PROP_SCHEDULE_TYPE5 | Client Data | Must be: exprecanal.eran_schedule_type | - |
| On Account Frequency 5 | PROP_ON_AC_FRQ_CODE5 | Client Data | Must be: codefreq.cdfq_code | - |
| Shares By Percentage 5 | PROP_SC_PERCENT_FLAG5 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Wfa Rule Code5 | PROP_WFA_RULE_CODE5 | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'WFC' | - |
| Mortgage Flag | PROP_MORTGAGE_FLAG | Client Data | Must be: Flag: (M)ortgaged, (N)ot Morgaged | - |
| Country Code | PROP_COUNTRY_ISO_CODE | Derived | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'ISO' | codesgen(cdgn_desc_long = prop_country, cdgn_cdty_ref = 'ISO').cdgn_ref |
| Entity Usage Code | PROP_USAGE_CODE | System Default | Usage Code | - |
| Maintain Funding Accounts at Property Level | PROP_BANK_ACCTS_FLAG | Client Data (Derived if Null) | Must be: Flag: (N)o, (Y)es | If null....<br>if (skyconf.skyc_prop_bank_accts = 'Y') then 'Y' else 'N' |
| Retain VAT Flag | PROP_RETAIN_VAT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Allow Approval of Unreconciled Invoices | PROP_APP_UNRECONCILED_INV | Client Data (Derived if Null) | Must be: Flag: (N)o, (Y)es | If null....<br>if (skyconf.skyc_scanning_trans_flag = 'Y') then 'Y' else (if (groups(:prop_grop_ref).grop_vat_registration_flag = 'Y') then 'Y' else 'N') |
| Unit Trial Balance | PROP_UNIT_TB_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Create Overhead Unit | CREATE_OVERHEAD_UNIT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Overhead Unit Ref | PROP_OVERHEAD_UNIT_REF | Client Data | Unit Ref (see: Additional Task 50 for validation logic) | - |
| Default EFT Cash Account | PROP_DFLT_EFT_BANK_REF | Client Data | Must be: bankac.bank_ref | - |
| Revaluation Calculation Level | PROP_REVAL_LEVEL_FLAG | Client Data | Must be: (P)roperty), (U)nit | - |
| Aggregate Journals at Property Level | PROP_REVAL_AGGREGATE_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |

### Uniqueness Rules

| Scope | Name | Restriction | Fields |
| --- | --- | --- | --- |
| Maximum | Primary Key | None | PROP_REF |
| Maximum | PROPERTYI1 | None | PROP_COMP_REF, PROP_REF |
| Maximum | PROPERTYI9 | None | PROP_PRSL_REF, PROP_REF |
| Maximum | Validation Index 1 | None | PROP_EXT_REF |

## Internal Derived Fields

These fields are calculated or checked internally during processing; they are not intake columns.

| Field | Timing | Derivation |
| --- | --- | --- |
| BCGP_DEB_AC_REF | Default | bnkcmpgp(comp_ref: :prop_comp_ref, grop_ref: :prop_grop_ref).bcgp_deb_ac_ref |
| BCGP_DEB_RAC_REF | Default | bnkcmpgp(comp_ref: :prop_comp_ref, grop_ref: :prop_grop_ref).bcgp_deb_rac_ref |
| BCGP_DEB_SAC_REF | Default | bnkcmpgp(comp_ref: :prop_comp_ref, grop_ref: :prop_grop_ref).bcgp_deb_sac_ref |
| BCGP_PAY_AC_REF | Default | bnkcmpgp(comp_ref: :prop_comp_ref, grop_ref: :prop_grop_ref).bcgp_pay_ac_ref |
| PARENT_RTSU_END_DATE | Default | property(:prop_parent_ref).prop_rtsu_end_date |
| TERI_CODE | Default | if (skyconf.skyc_teri_flag = 'Y') then (company(:prop_comp_ref).comp_teri_code) |

## Additional Processing Rules

Apply these workbook-defined tasks at the stated processing line or trigger.

| Id | Name | Line | Type | Triggers | Details | Internal Fields | Variables | Variable Calculations |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Default | 0 | Run Condition | - | Always runnable | - | - | - |
| - | Default | 01 | Cursor | Enabled on: MAP_ENTITY_PINS | SELECT bt.prop_grop_ref, bt.prop_ref, bt.prop_comp_ref, bt.prop_sc_void_tnnt_ref, bt.prop_elmt_type, bt.prop_sub_prop_flag, bt.prop_acqu_ref, ht.create_overhead_unit, bt.prop_addr_l1, bt.prop_addr_l2, bt.prop_cad_area, bt.prop_cad_ref, bt.prop_car_park_spaces, bt.prop_comment, bt.prop_country, bt.prop_country_iso_code, bt.prop_county, bt.prop_disabled_access, bt.prop_expect_life, bt.prop_overhead_unit_ref, bt.prop_gea, bt.prop_gia, bt.prop_measure_code, bt.prop_nea, bt.prop_nia, bt.prop_postcode, bt.prop_prsl_ref, bt.prop_town, bt.prop_type_code, bt.prop_survey_code, bt.prop_mngr_code, bt.prop_currency_code, bt.prop_tax_option_flag, bt.prop_longitude, bt.prop_latitude, bt.qcid<br>FROM property bt<br>INNER JOIN property_h1_01 ht ON ht.qcid = bt.qcid<br>WHERE (inserted during parent run)<br>ORDER BY bt.qcid | skyc_teri_flag = (skyconf.skyc_teri_flag)<br>skyc_use_agent_code = (skyconf.skyc_use_agent_code)<br>skyc_cda_inst = (skyconf.skyc_cda_inst)<br>skyc_bcmp_active_for_mig = (fwpackage.fw_create_active_bank)<br>grop_use_cda = (groups(:prop_grop_ref).grop_use_cda) | - | - |
| - | Default | 01.01 | Condition | Enabled on: MAP_ENTITY_PINS | IF (mig_sky_tables('PROPGROP').skyt_mig_flag <> 'Y') | - | - | - |
| - | Default | 01.01.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO propgppd:<br>pgpd_prop_ref = :prop_ref<br>pgpd_start_date = mig_config.mcfg_property_ownership_date<br>pgpd_end_date = Null<br>pgpd_owner = Null | - | - | - |
| - | Default | 01.02 | Condition | Enabled on: MAP_ENTITY_PINS | IF (mig_sky_tables('PROPGROP').skyt_mig_flag <> 'Y') | - | - | - |
| - | Default | 01.02.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO propgrop:<br>prgp_prop_ref = :prop_ref<br>prgp_grop_ref = :prop_grop_ref<br>prgp_pgpd_start_date = mig_config.mcfg_property_ownership_date<br>prgp_pgpd_end_date = Null<br>prgp_percent = 100<br>prgp_owner = 'Y' | - | - | - |
| - | Default | 01.03 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((mig_sky_tables('PROPGROP').skyt_mig_flag <> 'Y') and (version of target is same or newer than '10.1.17.0')) | - | - | - |
| - | Default | 01.03.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO gropcomp:<br>gpcp_grop_ref = :prop_grop_ref<br>gpcp_comp_ref = :prop_comp_ref<br>WHERE gropcomp record does not exist satisfying:<br>gpcp_grop_ref = :prop_grop_ref<br>gpcp_comp_ref = :prop_comp_ref | - | - | - |
| - | Default | 01.04 | Condition | Enabled on: MAP_ENTITY_PINS | IF (mig_module('012').modu_flag = 'Y') | - | - | - |
| - | Default | 01.04.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO location:<br>loca_ref = 'DEFAULT'<br>loca_description = fwmessage.fw_get_const(msgc_seqn_num: 1082)<br>loca_prop_ref = :prop_ref<br>loca_comp_ref = :prop_comp_ref | - | - | - |
| - | Default | 01.05 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((:prop_sc_void_tnnt_ref is not Null) and (skyconf.skyc_nldm_all_props_flag <> 'Y')) | - | - | - |
| - | Default | 01.05.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO tnntprop:<br>tprp_tnnt_ref = :prop_sc_void_tnnt_ref<br>tprp_prop_ref = :prop_ref<br>tprp_comp_ref = :prop_comp_ref<br>tprp_active = 'Y' | - | - | - |
| - | Default | 01.06 | Cursor | Enabled on: MAP_ENTITY_PINS | SELECT bgrp_bank_ref, qcid<br>FROM bankgrop<br>WHERE bgrp_grop_ref = :prop_grop_ref<br>ORDER BY qcid | - | Initialized on all rows of cursor:<br>bank_teri_code = (bankac(:bgrp_bank_ref).bank_teri_code)<br>bank_agent_code = (bankac(:bgrp_bank_ref).bank_agent_code)<br>comp_teri_code = (company(:prop_comp_ref).comp_teri_code)<br>comp_agent_code = (company(:prop_comp_ref).comp_agent_code)<br>active = (if (:prop_comp_ref = 'SYSTEM') then 'N' else if (:skyc_teri_flag = 'Y') then (if (:bank_teri_code = :comp_teri_code) then ('Y') else if (:bank_teri_code is Null) then ('Y') else ('N')) else if (:skyc_use_agent_code = 'Y') then (if (:bank_agent_code = :comp_agent_code) then ('Y') else ('N')) else :skyc_bcmp_active_for_mig) | - |
| - | Default | 01.06.01 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((version of target is older than '10.1.16.0') or (:active = 'Y')) | - | - | - |
| - | Default | 01.06.01.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO bankcomp:<br>bcmp_bank_ref = :bgrp_bank_ref<br>bcmp_comp_ref = :prop_comp_ref<br>bcmp_active = :active<br>WHERE bankcomp record does not exist satisfying:<br>bcmp_bank_ref = :bgrp_bank_ref<br>bcmp_comp_ref = :prop_comp_ref | - | - | - |
| - | Default | 01.07 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((:skyc_cda_inst = 'Y') and (:grop_use_cda = 'Y')) | - | - | - |
| - | Default | 01.07.01 | Cursor | Enabled on: MAP_ENTITY_PINS | SELECT cdgn_ref, qcid<br>FROM codesgen<br>WHERE cdgn_cdty_ref = 'BAT' AND cdgn_process_flag IN (7, 9)<br>ORDER BY qcid | - | - | - |
| - | Default | 01.07.01.01 | Cursor | Enabled on: MAP_ENTITY_PINS | SELECT bank_ref, bank_teri_code, bank_agent_code, qcid<br>FROM bankac<br>WHERE bank_type_flag = :cdgn_ref<br>ORDER BY qcid | - | Initialized on all rows of cursor:<br>comp_teri_code = (company(:prop_comp_ref).comp_teri_code)<br>comp_agent_code = (company(:prop_comp_ref).comp_agent_code)<br>active = (if (:prop_comp_ref = 'SYSTEM') then 'N' else if (:skyc_teri_flag = 'Y') then (if (:bank_teri_code = :comp_teri_code) then ('Y') else if (:bank_teri_code is Null) then ('Y') else ('N')) else if (:skyc_use_agent_code = 'Y') then (if (:bank_agent_code = :comp_agent_code) then ('Y') else ('N')) else :skyc_bcmp_active_for_mig) | - |
| - | Default | 01.07.01.01.01 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((version of target is older than '10.1.16.0') or (:active = 'Y')) | - | - | - |
| - | Default | 01.07.01.01.01.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO bankcomp:<br>bcmp_bank_ref = :bank_ref<br>bcmp_comp_ref = :prop_comp_ref<br>bcmp_active = :active<br>WHERE bankcomp record does not exist satisfying:<br>bcmp_bank_ref = :bank_ref<br>bcmp_comp_ref = :prop_comp_ref | - | - | - |
| - | Default | 01.08 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((:prop_comp_ref is not Null) and (:prop_grop_ref is not Null)) | - | - | - |
| - | Default | 01.08.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO bnkcmpgp:<br>bcgp_comp_ref = :prop_comp_ref<br>bcgp_grop_ref = :prop_grop_ref<br>WHERE bnkcmpgp record does not exist satisfying:<br>bcgp_comp_ref = :prop_comp_ref<br>bcgp_grop_ref = :prop_grop_ref | - | - | - |
| - | Default | 01.09 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((:prop_elmt_type is not Null) and (skyconf.skyc_elty_active = 'Y')) | - | - | - |
| - | Default | 01.09.01 | Cursor | Enabled on: MAP_ENTITY_PINS | SELECT elty_cdem_ref, elty_cdes_ref, qcid<br>FROM elmttype<br>WHERE elty_type = :prop_elmt_type<br>ORDER BY qcid | elmt_ref = (String(seqnos('ELEMENT').seqn_num + 1)) | - | - |
| - | Default | 01.09.01.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO element:<br>elmt_comp_ref = :prop_comp_ref<br>elmt_grop_ref = :prop_grop_ref<br>elmt_prop_ref = :prop_ref<br>elmt_ref = :elmt_ref<br>elmt_usage_code = 'ELE'<br>elmt_cdem_ref = :elty_cdem_ref<br>elmt_cdes_ref = :elty_cdes_ref<br>elmt_type_code = Min(codesgen(cdty_ref: 'ATY', process_flag: 2).cdgn_ref)<br>elmt_short_desc = codeelsb(cdem_ref: :elty_cdem_ref, cdes_ref: :elty_cdes_ref).cdes_long_desc<br>elmt_condition = Min(codesgen(cdty_ref: 'CND', process_flag: 0).cdgn_ref)<br>elmt_quantity = 1 | - | - | - |
| - | Default | 01.09.01.02 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO elmthist:<br>elmh_elmt_ref = :elmt_ref<br>elmh_location_entity_code = if (:prop_sub_prop_flag = 'Y') then ('SPR') else ('PRO')<br>elmh_location_entity_ref = :prop_ref<br>elmh_date = Today<br>elmh_user = skyconf.skyc_table_owner_code<br>elmh_comment = ((fwmessage.fw_get_const(msgc_seqn_num: 14317)) + ' ' + (fwmessage.fw_get_const(msgc_seqn_num: 1054))) | - | - | - |
| - | Default | 01.10 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((skyconf.skyc_nldm_all_props_flag <> 'Y') and (Nvl((skyconf.skyc_auto_gen_tprp), 'N') = 'Y')) | - | - | - |
| - | Default | 01.10.01 | Insert | Enabled on: MAP_ENTITY_PINS | FOR EACH RECORD IN tnntcomp<br>WHERE<br>tcmp_comp_ref = :prop_comp_ref<br>AND tcmp_active = 'Y'<br>INSERT INTO tnntprop:<br>tprp_tnnt_ref = :tcmp_tnnt_ref<br>tprp_prop_ref = :prop_ref<br>tprp_comp_ref = :prop_comp_ref<br>tprp_active = fwpackage.fw_create_active_tprp<br>WHERE tnntprop record does not exist satisfying:<br>tprp_tnnt_ref = :tcmp_tnnt_ref<br>tprp_prop_ref = :prop_ref | - | - | - |
| - | Default | 01.11 | Condition | Enabled on: MAP_ENTITY_PINS | IF (:prop_acqu_ref is not Null) | - | - | - |
| - | Default | 01.11.01 | Cursor | Enabled on: MAP_ENTITY_PINS | SELECT acqu_comp_ref, acqu_acquire_as_flag, qcid<br>FROM acquire<br>WHERE acqu_ref = :prop_acqu_ref<br>ORDER BY qcid | - | - | - |
| - | Default | 01.11.01.01 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((codesgen(cdty_ref: 'AQA', cdgn_ref: :acqu_acquire_as_flag).cdgn_process_flag <> 5) and (Nvl(:acqu_comp_ref, :prop_comp_ref) = :prop_comp_ref)) | - | - | - |
| - | Default | 01.11.01.01.01 | Update | Enabled on: MAP_ENTITY_PINS | UPDATE acquire<br>SET:<br>acqu_prop_ref = :prop_ref<br>acqu_comp_ref = :prop_comp_ref<br>WHERE:<br>acqu_ref = :prop_acqu_ref | - | - | - |
| - | Default | 01.12 | Condition | Enabled on: MAP_ENTITY_PINS | IF (:create_overhead_unit = 'Y') | - | - | - |
| - | Default | 01.12.01.01 | Condition | Enabled on: MAP_ENTITY_PINS | IF (skyconf.skyc_unit_overhead_auto_gen = 'Y') | - | - | - |
| - | Default | 01.12.01.01.01.01 | Condition | Enabled on: MAP_ENTITY_PINS | IF (autoref('UNI').auto_active = 'Y') | - | - | - |
| - | Default | 01.12.01.01.01.01.01 | Insert | Enabled on: MAP_ENTITY_PINS | INSERT INTO unit:<br>unit_ref = autoref('UNI').auto_seqn_num + 1<br>unit_prop_ref = :prop_ref<br>unit_acqu_ref = if ((:prop_acqu_ref is not Null) and (acquire(:prop_acqu_ref).acqu_acquire_as_flag = 'M')) then :PROP_ACQU_REF else Null<br>unit_addr_l1 = :prop_addr_l1<br>unit_addr_l2 = :prop_addr_l2<br>unit_cad_area = :prop_cad_area<br>unit_cad_ref = :prop_cad_ref<br>unit_car_park_spaces = :prop_car_park_spaces<br>unit_comment = :prop_comment<br>unit_comp_ref = :prop_comp_ref<br>unit_country = :prop_country<br>unit_country_iso_code = :prop_country_iso_code<br>unit_county = :prop_county<br>unit_disabled_access = :prop_disabled_access<br>unit_elmt_type = :prop_elmt_type<br>unit_expect_life = :prop_expect_life<br>unit_name = (:prop_ref + ' ' + (fwmessage.fw_get_const(msgc_seqn_num: 21579)))<br>unit_ext_ref = :prop_overhead_unit_ref<br>unit_ext_ref2 = :prop_overhead_unit_ref<br>unit_gea = :prop_gea<br>unit_gia = :prop_gia<br>unit_grop_ref = :prop_grop_ref<br>unit_measure_code = :prop_measure_code<br>unit_desc = (:prop_ref + ' ' + (fwmessage.fw_get_const(msgc_seqn_num: 21579)))<br>unit_nea = :prop_nea<br>unit_nia = :prop_nia<br>unit_postcode = :prop_postcode<br>unit_prsl_ref = :prop_prsl_ref<br>unit_start_date = if (:prop_acqu_ref is not Null) then (Nvl((acquire(:prop_acqu_ref).acqu_complete_date), Now)) else Now<br>unit_status_code = fwwizard.fw_get_first_status(status_type: 'STA', prov_process_flag: 2)<br>unit_town = :prop_town<br>unit_type_code = if (skyconf.skyc_teri_flag = 'Y') then (if (codesgen(cdty_ref: 'UT', cdgn_ref: :prop_type_code, teri_code: (company(:prop_comp_ref).comp_teri_code)).Existent is True) then :prop_type_code else Null) else (if (codesgen(cdty_ref: 'UT', cdgn_ref: :prop_type_code).Existent is True) then :prop_type_code else Null)<br>unit_usage_code = 'UNI'<br>unit_user_code = Nvl(:prop_survey_code, :prop_mngr_code)<br>unit_cur_code = :prop_currency_code<br>unit_dmse_ref = Null<br>unit_ex_exp_rec_flag = 'N'<br>unit_tax_option_flag = if (:prop_tax_option_flag = 'N') then 'N' else 'Y'<br>unit_main_unit_flag = 'N' | - | - | - |
| - | Default | 01.12.01.01.01.02 | Condition | Enabled on: MAP_ENTITY_PINS | ELSE | - | - | - |
| - | Default | 01.12.01.01.01.02.01 | Comment | Enabled on: MAP_ENTITY_PINS | 'Failed to create Overhead Unit because auto-referencing is not enabled for Units' | - | - | - |
| - | Default | 01.12.01.02 | Condition | Enabled on: MAP_ENTITY_PINS | ELSE | - | - | - |
| - | Default | 01.12.01.02.01 | Comment | Enabled on: MAP_ENTITY_PINS | 'Failed to create Overhead Unit because Auto Gen of Overhead Unit from Property is not enabled' | - | - | - |
| - | Default | 01.13 | Condition | Enabled on: MAP_ENTITY_PINS | IF ((:prop_longitude is not Null) and (:prop_latitude is not Null)) | - | - | - |
| - | Default | 01.13.01 | Command | Enabled on: MAP_ENTITY_PINS | EXECUTE fwmaps.fw_populate_entity_pins<br>PASSING:<br>pk_entity_code: 'PRO'<br>pk_entity_ref: :prop_ref | - | - | - |
| 7 | Current Property Ownership | 0 | Run Condition | - | Always runnable | - | - | - |
| 7 | Current Property Ownership | 01 | Cursor | - | SELECT prop_ref, prop_grop_ref, prop_comp_ref, qcid<br>FROM property<br>WHERE qcid IN {property_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 7 | Current Property Ownership | 01.01 | Insert | - | INSERT INTO propgppd:<br>pgpd_prop_ref = :prop_ref<br>pgpd_start_date = mig_config.mcfg_property_ownership_date<br>pgpd_end_date = Null<br>pgpd_owner = Null<br>WHERE propgppd record does not exist satisfying:<br>pgpd_prop_ref = :prop_ref | - | - | - |
| 7 | Current Property Ownership | 01.02 | Insert | - | INSERT INTO propgrop:<br>prgp_prop_ref = :prop_ref<br>prgp_grop_ref = :prop_grop_ref<br>prgp_pgpd_start_date = mig_config.mcfg_property_ownership_date<br>prgp_pgpd_end_date = Null<br>prgp_percent = 100<br>prgp_owner = 'Y'<br>WHERE propgrop record does not exist satisfying:<br>prgp_prop_ref = :prop_ref | - | - | - |
| 7 | Current Property Ownership | 01.03 | Condition | - | IF (version of target is same or newer than '10.1.17.0') | - | - | - |
| 7 | Current Property Ownership | 01.03.01 | Cursor | - | SELECT prgp_grop_ref, qcid<br>FROM propgrop<br>WHERE prgp_prop_ref = :prop_ref<br>ORDER BY qcid | - | - | - |
| 7 | Current Property Ownership | 01.03.01.01 | Insert | - | INSERT INTO gropcomp:<br>gpcp_grop_ref = :prgp_grop_ref<br>gpcp_comp_ref = :prop_comp_ref<br>WHERE gropcomp record does not exist satisfying:<br>gpcp_grop_ref = :prgp_grop_ref<br>gpcp_comp_ref = :prop_comp_ref | - | - | - |
| 45 | Fix Group Active Users | 0 | Run Condition | - | Always runnable | - | - | - |
| 45 | Fix Group Active Users | 01 | Cursor | - | SELECT prop_ref, qcid<br>FROM property<br>WHERE qcid IN {property_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 45 | Fix Group Active Users | 01.01 | Cursor | - | SELECT prgp_grop_ref, qcid<br>FROM propgrop<br>WHERE prgp_prop_ref = :prop_ref<br>ORDER BY qcid | - | - | - |
| 45 | Fix Group Active Users | 01.01.01 | Command | - | EXECUTE dmt_db_utils.fix_grop_active_user<br>PASSING:<br>pk_grop_ref: :prgp_grop_ref | - | - | - |
| 50 | Validation of Overhead Unit Refs | 0 | Run Condition | - | Always runnable | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01 | Cursor | - | SELECT prop_overhead_unit_ref, prop_ref, qcid<br>FROM property<br>WHERE qcid IN {property_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.01 | Condition | - | IF ((:prop_overhead_unit_ref is not Null) and (unit(:prop_overhead_unit_ref).Existent is False)) | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.01.01 | Comment | - | 'Overhead Unit does not exist' | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.02 | Condition | - | IF ((:prop_overhead_unit_ref is not Null) and (unit(:prop_overhead_unit_ref).Existent is True) and (unit(:prop_overhead_unit_ref).unit_prop_ref <> :prop_ref)) | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.02.01 | Comment | - | 'Overhead Unit must belong to this Property' | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.03 | Condition | - | IF ((:prop_overhead_unit_ref is not Null) and (unit(:prop_overhead_unit_ref).Existent is True) and (unit(:prop_overhead_unit_ref).unit_main_unit_flag = 'Y')) | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.03.01 | Comment | - | 'Overhead Unit must not be this Property's main Unit' | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.04 | Condition | - | IF ((:prop_overhead_unit_ref is not Null) and (unit(:prop_overhead_unit_ref).Existent is True) and (unit(:prop_overhead_unit_ref).unit_dmse_ref is not Null)) | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.04.01 | Comment | - | 'Overhead Unit must not belong to a Rental Space' | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.05 | Condition | - | IF ((:prop_overhead_unit_ref is not Null) and (unit(:prop_overhead_unit_ref).Existent is True) and (unit(:prop_overhead_unit_ref).unit_end_date is not Null)) | - | - | - |
| 50 | Validation of Overhead Unit Refs | 01.05.01 | Comment | - | 'Overhead Unit must not have an End Date' | - | - | - |

## Reference Code Types

Fields whose descriptions identify a code type must contain a value from that code type. The workbook's `Codes` and `LOVs` worksheets provide the corresponding lookup values.

| Code Type | Name | Desc |
| --- | --- | --- |
| COU | STATE/COUNTY | State/County |
| CUR | Currency Codes | Currency Codes |
| ETY | Element Types | Element Type Codes |
| ISO | Country Codes | ISO Standard 2 character Country Codes<br>PROCESS FLAG 2: Auto-allocation of receipts is against Service Charge first followed by Rent.<br>PROCESS FLAG 3: Annual Tax Returns enabled by default. |
| LIB | LISTED BLDG | Listed Building Code Types |
| LPS | LOC PLAN STS | Local Planning Status Codes |
| MIM | Maintenance Importance | Maintenance Importance<br>PROCESS FLAG 1 : High<br>PROCESS FLAG 2 : Medium<br>PROCESS FLAG 3 : Low |
| MSA | MSA/Prp Rep/H&S | Met. Service Area/Prop Rep Cat/Health & Safety |
| OBL | OBLIGATION | This code is used to describe who is responsible for certain activities that may be carried out on a property. |
| PHC | Business Day Country | The country, region or group of countries which determines the bank holidays to be used in calculating whether or not a given date is a business day. |
| PLS | Property Status | Process Flag 0: Disposed - Excluded when status filtering is activated. Used by the Disposal wizard.<br>Process Flag 4: Completed - Used by the New Lease Payable wizard, or the overnight processing, after finalise.<br>Process Flag 9: Provisional - Excluded when status filtering is activated. Used by the New Lease Payable wizard before finalise. |
| PRM | Property Recharge Model | Used to record the different recharge models for passing property income/expense onto landlord |
| PS | Property Accounting Status | Used to show whether the property will be included when Property Accounting processing is performed<br>Process Flag 0 : Disposed, No accounting functions can be performed and the record is excluded when status filtering ON, .<br>Process Flag 1 : Live for the purposes of all accounting functions and status filtering.<br>Process Flag 2 : Partial Accounting, all financial functions available except rent demands and Lease Payable Regular Charges.<br>Process Flag 3 : Not/Applicable, No accounting functions can be performed but visible when status filtering is applied. |
| PT | PROPERTY TYPE | Property Type codes are used to denote the varying characteristics of a building, development area etc<br>Process flags are :<br>2 - Mortgage<br>3 - Retail Centre (used by Vision). |
| REG | Region Code | Region |
| TNR | TENURE | Tenure Types |
| WFC | WFA Calculation Rule | Weighted floor area calculation rule.<br>Process flag:<br>1 - Apportioning unit area using the area on the rule as a band<br>2 - Total unit area multiplied by the minimum rule area greater than the unit area |
| WOW | Working Week | Working Week. |

---

## Source Notes

* `-` means the workbook cell is blank and does not add a rule or default.
* Validation and derivation expressions are preserved verbatim so implementation-specific PLE functions and field names are not reinterpreted.
* Code descriptions in field rules identify the required lookup family; use the workbook's `Codes` / `LOVs` worksheets or the target PLE database to validate the current allowed values.
* References to related PLE entities require the corresponding table data or target database. If that data is unavailable, report `Warning / REQUIRES DATABASE VERIFICATION` rather than claiming the reference is valid or invalid.
