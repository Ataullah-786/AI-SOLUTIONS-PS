# PLE - Tenant Rules

**Product:** PLE
**Target Table:** `Tenant`
**Schema File:** `/PLE/Schema/Tenant.json`
**Source Workbook:** `TENANT_tem.xlsx`
**Source Worksheet:** `Template`

These rules are taken from the supplied PLE template workbook. They describe how
intake columns must be populated and validated before data is integrated into the PLE `Tenant` table.

They are **additional to** the structural rules in `/PLE/Schema/Tenant.json`.
Where the workbook and JSON schema disagree on a physical type or length, the JSON
schema remains the source of truth for storage and the rules below define the business/intake expectation.

---

## Field Rules

| Intake Label | PLE Field | Format | Default | Rule / Description | Source | Comment |
| --- | --- | --- | --- | --- | --- | --- |
| Operations List | TCMP_COMP_REF_LIST | String(1000) | - | Comma separated list of Operation References for which the given Tenant should be activated | - | - |
| Customer Reference | TNNT_REF | String(8) | - | Primary Key | - | - |
| Level | TNNT_LEVEL | String(3) | 3 | Code of Type: 'CUL' (Customer Level) | - | - |
| Customer Reference | TNNT_GROUP_TNNT_REF | String(8) | - | Foreign Key - tenant | - | - |
| Trading As | TNNT_TRADE_NAME | String(60) | - | - | - | - |
| Address Reference | TNNT_ADDR_REF | String(8) | - | Address Ref | - | - |
| Valid Demands | TNNT_VALID_DEMANDS | String(1) | L | Flag: (B)oth, (L)ease, (N)on-Lease | - | - |
| Customer Type | TNNT_TYPE_CODE | String(3) | - | Code of Type: 'TNT' (CUSTOMER TYPE) | - | - |
| Status | TNNT_STATUS_CODE | String(3) | - | Code of Type: 'TES' (Customer Status) | - | - |
| User Code | TNNT_USER_CODE | String(3) | - | User Code | - | - |
| Customer Currency Code | TNNT_CUR_CODE | String(3) | - | Code of Type: 'CUR' (Currency Codes) | - | - |
| Agent Code | TNNT_AGENT_CODE | String(3) | - | Code of Type: 'OPA' (OPERATION AGENT) | - | - |
| Doc Lan Code | TNNT_DOC_LAN_CODE | String(3) | 1 | Code of Type: 'LAN' (User Languages) | - | - |
| E-Mail Correspondence | TNNT_EMAIL_CORRES_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Automated E-Mail Correspondence | TNNT_EMAIL_INVOICE_FLAG | String(1) | N | Flag: (N)o, (Y)es. Can Y only if addr_email is not null | - | - |
| Teri Code | TNNT_TERI_CODE | String(3) | - | Code of Type: 'TER' (Territory) | - | - |
| Legal Name | TNNT_LEGAL_NAME | String(60)<br>Max Len: 60 | - | Defaults to Name of Address | - | - |
| External Ref | TNNT_EXT_REF | String(20) | {TNNT_REF} | - | - | - |
| Message | TNNT_MESS | String(100)<br>Max Len: 100 | - | - | - | - |
| Demand Type Flag | TNNT_DEMAND_TYPE_FLAG | String(1) | S | Flag: (P)roforma, (R)ent Statment, (S)tandard | - | - |
| Discount Allowed | TNNT_DISC_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Discount Percentage | TNNT_DISC_RATE | Number(5,2)<br>Min Val: 0<br>Max Val: 100.00 | - | Mandatory If Discount Allowed Is Y Else NULL | - | - |
| Discount Days to Pay | TNNT_DISC_DAYS | Number(3)<br>Min Val: 0<br>Max Val: 999 | - | Mandatory If Discount Allowed Is Y Else NULL | - | - |
| Int On Late Payment | TNNT_INT_ON_ARR_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Auto Generate | TNNT_AUTO_GENERATE | String(1) | N | Flag: (N)o, (Y)es. Must Be N If Interest On Late Payment Is N | - | - |
| Base Rate Num | TNNT_BASE_RATE_NUM | String(3) | - | Bank Code. Mandatory If Interest On Late Payment Is Y Else NULL | - | - |
| Above Base Amount | TNNT_ABOVE_BASE_AMT | Number(4,2)<br>Min Val: -99.99<br>Max Val: 99.99 | - | NULL If Int On Late Payment Is N | - | - |
| Days Grace | TNNT_GRACE_NUM | Number(3)<br>Min Val: 0<br>Max Val: 999 | - | NULL If Int On Late Payment Is N | - | - |
| Invoice Due Days | TNNT_INV_DUE_DAYS | Number(3)<br>Min Val: 0<br>Max Val: 999 | - | Default From Skyc_Tnnt_Inv_Due_Days | - | - |
| Credit Limit | TNNT_CREDIT_LIMIT | Number(14,2)<br>Min Val: 0<br>Max Val: 99999999999.99 | - | - | - | - |
| Composite Bill Flag | TNNT_COMPOSITE_BILL_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Extraction Code | TNNT_EXTRACT_CODE | String(3) | - | Code of Type: 'EXT' (Extraction Type) | - | - |
| Invoice Format | TNNT_SSRS_INV_LOCATION | String(250) | - | - | - | - |
| Bill Outsort Flag | TNNT_BILL_OUTSORT_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Rem Flag | TNNT_REM_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Rmls Cdgn Ref | TNNT_RMLS_CDGN_REF | String(3) | - | Code of Type: 'RLT' (Reminder Letter Types) | - | - |
| Prnt Flag | TNNT_PRNT_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Prnt By Code | TNNT_PRNT_BY_CODE | String(3) | - | User Code | - | - |
| Prnt By Date | TNNT_PRNT_BY_DATE | Date | - | - | - | - |
| Prnt By Desc | TNNT_PRNT_BY_DESC | String(30) | - | - | - | - |
| Rcve Flag | TNNT_RCVE_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Rcve By Code | TNNT_RCVE_BY_CODE | String(3) | - | User Code | - | - |
| Rcve By Date | TNNT_RCVE_BY_DATE | Date | - | - | - | - |
| Rcve By Desc Code | TNNT_RCVE_BY_DESC_CODE | String(3) | - | Code of Type: 'CRR' (Cust. Receive Payment Reason) | - | - |
| Relief Flag | TNNT_RELIEF_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Mort Bill Agent | TNNT_MORT_BILL_AGENT | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Mort Agent Address Ref | TNNT_MORT_AGENT_ADDR_REF | String(8) | - | Address Ref | - | - |
| Print Rcpt | TNNT_PRINT_RCPT | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Bank Stmt Desc | TNNT_BKST_DESC | String(100) | - | - | - | - |

---

## Validation Rules

### Table-Level Validations

Each expression identifies the condition that makes a row invalid. Report the workbook's stated message when the expression evaluates to true.

| Message | Validation |
| --- | --- |
| Discount is not set but % rate is not blank | invalid if (NVL(:tnnt_disc_flag, 'N') = 'N') and (:tnnt_disc_rate is not Null) |
| Discount is not set but Days To Pay is not blank | invalid if (NVL(:tnnt_disc_flag, 'N') = 'N') and (:tnnt_disc_days is not Null) |
| Discount is set but % rate is blank | invalid if (:tnnt_disc_flag = 'Y') and (:tnnt_disc_rate is Null) |
| Discount is set but Days To Pay is blank | invalid if (:tnnt_disc_flag = 'Y') and (:tnnt_disc_days is Null) |
| Email flag can be Y only if an Email Address exists | invalid if (:tnnt_email_invoice_flag = 'Y') and (:addr_email is Null) |
| If Level is 1 then Group Tenant must be null | invalid if (:tnnt_level = '1') and (:tnnt_group_tnnt_ref is not Null) |
| If Level is 1 then Tenant must be the Group Tenant of a level 2 Tenant | invalid if (:tnnt_level = '1') and (tenant(group_tnnt_ref: :tnnt_ref, level: '2').Inexistent) |
| If Level is 2 then Group Tenant must be a level 1 Tenant | invalid if (:tnnt_level = '2') and ((:tnnt_group_tnnt_ref is not Null) and (tenant(ref: :tnnt_group_tnnt_ref, level: '1').Inexistent)) |
| If Level is 3 then Group Tenant must be a level 2 Tenant | invalid if (:tnnt_level = '3') and ((:tnnt_group_tnnt_ref is not Null) and (tenant(ref: :tnnt_group_tnnt_ref, level: '2').Inexistent)) |
| Int On Arrears is not set but % above/below rate is not blank | invalid if (NVL(:tnnt_int_on_arr_flag, 'N') = 'N') and (:tnnt_above_base_amt is not Null) |
| Int On Arrears is not set but Auto Generate is set | invalid if (NVL(:tnnt_int_on_arr_flag, 'N') = 'N') and (:tnnt_auto_generate = 'Y') |
| Int On Arrears is not set but Bank is not blank | invalid if (NVL(:tnnt_int_on_arr_flag, 'N') = 'N') and (:tnnt_base_rate_num is not Null) |
| Int On Arrears is not set but Grace Days is not blank | invalid if (NVL(:tnnt_int_on_arr_flag, 'N') = 'N') and (:tnnt_grace_num is not Null) |
| Int On Arrears is set but Bank is blank | invalid if (:tnnt_int_on_arr_flag = 'Y') and (:tnnt_base_rate_num is Null) |
| tcmp_comp_ref_list contains an invalid Operation Reference | invalid if (:tcmp_comp_ref_list is not Null) and (company(comp_ref in: :tcmp_comp_ref_list).AllExistent is False) |
| Tenant is a level 2 Tenant, but not the Group Tenant of a level 3 Tenant | warning if (:tnnt_level = '2') and (tenant(group_tnnt_ref: :tnnt_ref, level: '3').Inexistent) |
| tnnt_email_corres_flag can be Y only if an Email Address exists | invalid if (:tnnt_email_corres_flag = 'Y') and (:addr_email is Null) |
| tnnt_ref contains prohibited characters | invalid if (:tnnt_ref is not Null) and (:tnnt_ref matches Regex('[^a-zA-Z0-9/.:%!$*_+&^-]')) |
| tnnt_teri_code must be same as Address's Territory if Territorialisation is enabled and Address's Territory is not null | invalid if (skyconf.skyc_teri_flag = 'Y') and (:addr_teri_code is not Null) and ((:tnnt_teri_code is Null) or (:tnnt_teri_code <> :addr_teri_code)) |

### Field-Level Validation and Derivation

| Label | PLE Field | Mode | Validation | Derivation |
| --- | --- | --- | --- | --- |
| Customer Reference | TNNT_REF | Client Data | Primary Key: tenant.tnnt_ref | - |
| Level | TNNT_LEVEL | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUL' | - |
| Customer Reference | TNNT_GROUP_TNNT_REF | Client Data | Must be: tenant.tnnt_ref | - |
| Address Reference | TNNT_ADDR_REF | Client Data | Must be: address.addr_ref | - |
| Valid Demands | TNNT_VALID_DEMANDS | Client Data | Must be: Flag: (B)oth, (L)ease, (N)on-Lease | - |
| Customer Type | TNNT_TYPE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'TNT' | - |
| Status | TNNT_STATUS_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'TES' | - |
| User Code | TNNT_USER_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Customer Currency Code | TNNT_CUR_CODE | Client Data (Derived if Null) | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUR' | If null....<br>mig_config.mcfg_dflt_nc_cur_code |
| Agent Code | TNNT_AGENT_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'OPA' | - |
| Doc Lan Code | TNNT_DOC_LAN_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LAN' | - |
| E-Mail Correspondence | TNNT_EMAIL_CORRES_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Automated E-Mail Correspondence | TNNT_EMAIL_INVOICE_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Teri Code | TNNT_TERI_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'TER' | if (:tnnt_teri_code is Null) then :addr_teri_code |
| Legal Name | TNNT_LEGAL_NAME | Client Data (Derived if Null) | - | If null....<br>address(:tnnt_addr_ref).addr_name |
| Demand Type Flag | TNNT_DEMAND_TYPE_FLAG | Client Data | Must be: Flag: (P)roforma, (R)ent Statment, (S)tandard | - |
| Discount Allowed | TNNT_DISC_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Int On Late Payment | TNNT_INT_ON_ARR_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Auto Generate | TNNT_AUTO_GENERATE | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Base Rate Num | TNNT_BASE_RATE_NUM | Client Data | Must be: codebank.cdbk_code | - |
| Invoice Due Days | TNNT_INV_DUE_DAYS | Client Data | - | if (:tnnt_inv_due_days is Null) then (skyconf.skyc_tnnt_inv_due_days) |
| Composite Bill Flag | TNNT_COMPOSITE_BILL_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Extraction Code | TNNT_EXTRACT_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'EXT' | - |
| Bill Outsort Flag | TNNT_BILL_OUTSORT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rem Flag | TNNT_REM_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rmls Cdgn Ref | TNNT_RMLS_CDGN_REF | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'RLT' | - |
| Prnt Flag | TNNT_PRNT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Prnt By Code | TNNT_PRNT_BY_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Rcve Flag | TNNT_RCVE_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rcve By Code | TNNT_RCVE_BY_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Rcve By Desc Code | TNNT_RCVE_BY_DESC_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CRR' | - |
| Relief Flag | TNNT_RELIEF_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Mort Bill Agent | TNNT_MORT_BILL_AGENT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Mort Agent Address Ref | TNNT_MORT_AGENT_ADDR_REF | Client Data | Must be: address.addr_ref | - |
| Print Rcpt | TNNT_PRINT_RCPT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Entity Usage Code | TNNT_USAGE_CODE | System Default | Usage Code | - |
| Int On Sc Flag | TNNT_INT_ON_SC_FLAG | System Default | Must be: Flag: (N)o, (Y)es | - |
| Proc By Gdpr Flag | TNNT_PROC_BY_GDPR_FLAG | System Default | Must be: Flag: (N)o, (Y)es | - |

### Uniqueness Rules

| Scope | Name | Restriction | Fields |
| --- | --- | --- | --- |
| Maximum | Primary Key | None | TNNT_REF |
| Maximum | Validation Index 1 | None | TNNT_EXT_REF |
| Maximum | Validation Index 2 | None | TNNT_LEGAL_NAME |
| Maximum | Validation Index 3 | None | TNNT_TRADE_NAME |

## Internal Derived Fields

These fields are calculated or checked internally during processing; they are not intake columns.

| Field | Timing | Derivation |
| --- | --- | --- |
| ADDR_EMAIL | Default | address(:tnnt_addr_ref).addr_email |
| ADDR_TERI_CODE | Default | if (:tnnt_addr_ref is not Null) then (address(:tnnt_addr_ref).addr_teri_code) |
| TERI_CODE | Default | :tnnt_teri_code |

## Additional Processing Rules

Apply these workbook-defined tasks at the stated processing line or trigger.

| Id | Name | Line | Type | Triggers | Details | Internal Fields | Variables | Variable Calculations |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Default | 0 | Run Condition | - | Always runnable | - | - | - |
| - | Default | 01 | Cursor | - | SELECT ht.tcmp_comp_ref_list, bt.tnnt_teri_code, bt.tnnt_agent_code, bt.tnnt_ref, bt.tnnt_addr_ref, bt.tnnt_group_tnnt_ref, bt.tnnt_level, bt.qcid<br>FROM tenant bt<br>INNER JOIN tenant_h1_01 ht ON ht.qcid = bt.qcid<br>WHERE (inserted during parent run)<br>ORDER BY bt.qcid | skyc_teri_flag = (skyconf.skyc_teri_flag) | - | - |
| - | Default | 01.01.01 | Condition | - | IF (:tcmp_comp_ref_list is Null) | - | skyc_tcmp_active_for_mig = (if ((fwpackage.fw_create_active_tnnt) = 'A') then ('Y') else ('N'))<br>skyc_teri_flag = (skyconf.skyc_teri_flag)<br>skyc_use_agent_code = (skyconf.skyc_use_agent_code) | - |
| - | Default | 01.01.01.01.01 | Condition | - | IF ((:skyc_teri_flag = 'Y') or (:skyc_use_agent_code = 'Y')) | - | - | - |
| - | Default | 01.01.01.01.01.01 | Cursor | - | SELECT comp_ref, comp_teri_code, comp_agent_code, qcid<br>FROM company<br>ORDER BY qcid | active = (if (:comp_ref = 'SYSTEM') then 'N' else if (:skyc_teri_flag = 'Y') then (if (:tnnt_teri_code = :comp_teri_code) then ('Y') else if (:tnnt_teri_code is Null) then ('Y') else ('N')) else if (:skyc_use_agent_code = 'Y') then (if (:tnnt_agent_code = :comp_agent_code) then ('Y') else ('N'))) | - | - |
| - | Default | 01.01.01.01.01.01.01 | Condition | - | IF ((version of target is older than '10.2.1.0') or (:active = 'Y')) | - | - | - |
| - | Default | 01.01.01.01.01.01.01.01 | Insert | - | INSERT INTO tnntcomp:<br>tcmp_tnnt_ref = :tnnt_ref<br>tcmp_comp_ref = :comp_ref<br>tcmp_active = :active | - | - | - |
| - | Default | 01.01.01.01.02 | Condition | - | ELSE | - | - | - |
| - | Default | 01.01.01.01.02.01 | Condition | - | IF ((version of target is older than '10.2.1.0') or (:skyc_tcmp_active_for_mig = 'Y')) | - | - | - |
| - | Default | 01.01.01.01.02.01.01 | Insert | - | FOR EACH RECORD IN company<br>WHERE<br>comp_ref <> 'SYSTEM'<br>INSERT INTO tnntcomp:<br>tcmp_tnnt_ref = :tnnt_ref<br>tcmp_comp_ref = :comp_ref<br>tcmp_active = :skyc_tcmp_active_for_mig | - | - | - |
| - | Default | 01.01.01.01.02.02 | Condition | - | IF (version of target is older than '10.2.1.0') | - | - | - |
| - | Default | 01.01.01.01.02.02.01 | Insert | - | INSERT INTO tnntcomp:<br>tcmp_tnnt_ref = :tnnt_ref<br>tcmp_comp_ref = 'SYSTEM'<br>tcmp_active = 'N' | - | - | - |
| - | Default | 01.01.02 | Condition | - | ELSE | - | comp_ref = Null | - |
| - | Default | 01.01.02.01 | Loop | - | Begin Loop until (:comp_ref is Null) | - | Initialized all cycles of loop:<br>comp_teri_code = (company(:comp_ref).comp_teri_code)<br>comp_agent_code = (company(:comp_ref).comp_agent_code)<br>active = (if (:comp_ref = 'SYSTEM') then 'N' else if (:skyc_teri_flag = 'Y') then (if (:tnnt_teri_code = :comp_teri_code) then ('Y') else if (:tnnt_teri_code is Null) then ('Y') else ('N')) else if (:skyc_use_agent_code = 'Y') then (if (:tnnt_agent_code = :comp_agent_code) then ('Y') else ('N')) else 'Y') | comp_ref = (List(Str: :tcmp_comp_ref_list, Separator(s): ', ').Item_At_Position(Loop_Idx)) |
| - | Default | 01.01.02.01.01 | Condition | - | IF ((version of target is older than '10.2.1.0') or (:active = 'Y')) | - | - | - |
| - | Default | 01.01.02.01.01.01 | Insert | - | INSERT INTO tnntcomp:<br>tcmp_tnnt_ref = :tnnt_ref<br>tcmp_comp_ref = :comp_ref<br>tcmp_active = :active | - | - | - |
| - | Default | 01.02 | Insert | - | INSERT INTO addruse:<br>adus_code = 'TE1'<br>adus_addr_ref = :tnnt_addr_ref<br>adus_ref = :tnnt_ref | - | - | - |
| - | Default | 01.03 | Condition | - | IF (:tnnt_group_tnnt_ref is not Null) | - | - | - |
| - | Default | 01.03.01 | Update | - | UPDATE tenant<br>SET:<br>tnnt_level_1_ref = if ((:tnnt_group_tnnt_ref is not Null) and (:tnnt_level = '2')) then :tnnt_group_tnnt_ref else if ((:tnnt_group_tnnt_ref is not Null) and (:tnnt_level = '3')) then (tenant(:tnnt_group_tnnt_ref).tnnt_group_tnnt_ref)<br>tnnt_level_2_ref = if ((:tnnt_group_tnnt_ref is not Null) and (:tnnt_level = '3')) then :tnnt_group_tnnt_ref<br>WHERE:<br>qcid IN {tenant_h1_01(inserted during parent run).qcid} AND qcid = {Cursor qcid} | - | - | - |
| - | Default | 01.04.01 | Condition | - | IF ((:skyc_teri_flag = 'Y') and (:tnnt_teri_code is not Null)) | - | - | - |
| - | Default | 01.04.01.01 | Insert | - | FOR EACH RECORD IN groups<br>WHERE<br>grop_teri_code = :tnnt_teri_code<br>INSERT INTO tnntgrop:<br>tgrp_tnnt_ref = :tnnt_ref<br>tgrp_grop_ref = :grop_ref<br>tgrp_control_ac_code = :grop_inc_ctl_ac_code<br>tgrp_dpst_ac_code = :grop_dpst_ac_code<br>WHERE tnntgrop record does not exist satisfying:<br>tgrp_tnnt_ref = :tnnt_ref<br>tgrp_grop_ref = :grop_ref | - | - | - |
| - | Default | 01.04.02 | Condition | - | ELSE | - | - | - |
| - | Default | 01.04.02.01 | Insert | - | FOR EACH RECORD IN groups<br>INSERT INTO tnntgrop:<br>tgrp_tnnt_ref = :tnnt_ref<br>tgrp_grop_ref = :grop_ref<br>tgrp_control_ac_code = :grop_inc_ctl_ac_code<br>tgrp_dpst_ac_code = :grop_dpst_ac_code<br>WHERE tnntgrop record does not exist satisfying:<br>tgrp_tnnt_ref = :tnnt_ref<br>tgrp_grop_ref = :grop_ref | - | - | - |
| - | Default | 01.05 | Condition | - | IF ((skyconf.skyc_nldm_all_props_flag <> 'Y') and (Nvl((skyconf.skyc_auto_gen_tprp), 'N') = 'Y')) | - | - | - |
| - | Default | 01.05.01 | Cursor | - | SELECT tcmp_comp_ref, qcid<br>FROM tnntcomp<br>WHERE tcmp_tnnt_ref = :tnnt_ref AND tcmp_active = 'Y'<br>ORDER BY qcid | - | - | - |
| - | Default | 01.05.01.01 | Cursor | - | SELECT prop_ref, qcid<br>FROM property<br>WHERE prop_comp_ref = :tcmp_comp_ref<br>ORDER BY qcid | - | - | - |
| - | Default | 01.05.01.01.01 | Insert | - | INSERT INTO tnntprop:<br>tprp_tnnt_ref = :tnnt_ref<br>tprp_prop_ref = :prop_ref<br>tprp_comp_ref = :tcmp_comp_ref<br>tprp_active = fwpackage.fw_create_active_tprp | - | - | - |

## Reference Code Types

Fields whose descriptions identify a code type must contain a value from that code type. The workbook's `Codes` and `LOVs` worksheets provide the corresponding lookup values.

| Code Type | Name | Desc |
| --- | --- | --- |
| CRR | Cust. Receive Payment Reason | Customer Receive Payment Reason |
| CUL | Customer Level | Customer Level Hierarchy (1 is the top) |
| CUR | Currency Codes | Currency Codes |
| EXT | Extraction Type | Extraction Type used by the Rent Demand process to determine order invoices printed. NOTE: Code must be a numeric value and of XXX |
| LAN | User Languages | A list of available languages in the system. |
| OPA | OPERATION AGENT | Operation Agent |
| RLT | Reminder Letter Types | Describes the rent and turnover certificate reminder letters which can be sent out to tenants.<br>PROCESS FLAG 1 : Rent reminder letters<br>PROCESS FLAG 2 : Turnover certificate reminder letters |
| TER | Territory | Used to restrict access to various codes and config by country or territory/jurisdiction/country. |
| TES | Customer Status | Customer Status<br>PROCESS FLAG 0:<br>Former Customer<br>Excluded when status filtering ON.<br>Used when the 'Customer Move Out' process is completed if the Customer has no other current Lease Assignments.<br>PROCESS FLAG 1:<br>Current<br>Used when the 'Customer Move In' process is completed.<br>PROCESS FLAG 9:<br>Provisional<br>Used during the 'Customer Move In' process if the Customer has been created within the process. |
| TNT | CUSTOMER TYPE | Type of Customer |

---

## Source Notes

* `-` means the workbook cell is blank and does not add a rule or default.
* Validation and derivation expressions are preserved verbatim so implementation-specific PLE functions and field names are not reinterpreted.
* Code descriptions in field rules identify the required lookup family; use the workbook's `Codes` / `LOVs` worksheets or the target PLE database to validate the current allowed values.
* References to related PLE entities require the corresponding table data or target database. If that data is unavailable, report `Warning / REQUIRES DATABASE VERIFICATION` rather than claiming the reference is valid or invalid.
