# PLE - Lease Rules

**Product:** PLE
**Target Table:** `Lease`
**Schema File:** `/COMMON/PLE/Schema/Lease.json`
**Source Workbook:** `LEASE_tem.xlsx`
**Source Worksheet:** `Template`

These rules are taken from the supplied PLE template workbook. They describe how
intake columns must be populated and validated before data is integrated into the PLE `Lease` table.

They are **additional to** the structural rules in `/COMMON/PLE/Schema/Lease.json`.
Where the workbook and JSON schema disagree on a physical type or length, the JSON
schema remains the source of truth for storage and the rules below define the business/intake expectation.

---

## Field Rules

| Intake Label | PLE Field | Format | Default | Rule / Description | Source | Comment |
| --- | --- | --- | --- | --- | --- | --- |
| Organisation Ref | LEAS_ORGN_REF | String(8) | - | Foreign Key - organisation | - | - |
| Property Reference | LEAS_PROP_REF | String(8) | - | Foreign Key - property | - | - |
| Rental Space Ref | LEAS_DMSE_REF | String(8) | - | Foreign Key - demise. Mandatory If Rental Flag is Y else NULL | - | - |
| Lease Reference | LEAS_REF | String(8) | - | Primary Key. Unique | - | - |
| Description | LEAS_DESC | String(60) | - | - | - | - |
| Ext Ref | LEAS_EXT_REF | String(20) | {LEAS_REF} | Unique. Default Is Lease Ref | - | - |
| Tenant Reference | LEAS_TNNT_REF | String(8) | - | Foreign Key - tenant | - | - |
| Type of Lease | LEAS_TYPE_CODE | String(3) | - | Code of Type: 'LT' (LEASE TYPE) | - | - |
| Status | LEAS_STATUS_CODE | String(3) | CUR | Code of Type: 'LS' (LEASE STATUS) | - | - |
| User | LEAS_USER_CODE | String(3) | - | User Code | - | - |
| Doc Lan Code | LEAS_DOC_LAN_CODE | String(3) | 1 | Code of Type: 'LAN' (User Languages) | - | - |
| Rental Flag | LEAS_RENTAL_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Agreement Date | LEAS_AGREE_DATE | Date | - | - | - | - |
| Occupancy Date | LEAS_OCCU_DATE | Date | - | - | - | - |
| Lease Start Date | LEAS_START_DATE | Date | - | - | - | - |
| Lease End Date | LEAS_EXPIRY_DATE | Date | - | Mandatory If Continuing Occupancy Is N Else NULL. Must Be After Lease Start Date | - | - |
| Occup End Date | LEAS_TNMO_DATE | Date | - | - | - | - |
| Lease Termination Date | LEAS_TERM_DATE | Date | - | Must Be On Or After The Lease Start Date. Mandatory if Lease Status Process Flag  is 0 | - | - |
| Use Analysis Invoice Grouping | LEAS_USE_GRAD_INV_GRP_CODE | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Separate Invoices By Due Date | LEAS_SEP_INV_BY_DUE_DATE | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Separate Invoices By Trans | LEAS_SEP_INV_BY_TRANS | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Landlord and Tenant Act | LEAS_LNLD_TNNT_ACT | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Continuing Occupancy | LEAS_CONT_OCC_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Comment | LEAS_COMMENT | String(1000) | - | - | - | - |
| Inter-Company Lease Payable | LEAS_ICMP_HLSE_REF | String(8) | - | Foreign Key. Only Valid If The Head Lease Has No Inter-Lease Set | - | - |
| Is Lease Current | LEAS_CURRENT_FLAG | String(1) | C | Flag: (C)urrent, (N)o Accounting, (R)educed Accounting | - | - |
| Review Basis | LEAS_REVIEW_BASIS | String(1) | N | Flag: (I)ndexed, (M)ixed, (N)egotiated, (O)ther | - | - |
| Turnover Flag | LEAS_TURNOVER_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Demand Type | LEAS_DEMAND_TYPE_FLAG | String(1) | S | Flag: (P)roforma, (R)ent Statment, (S)tandard. If  P then Lease Vatable Flag must be Y | - | - |
| Charge Interest on Late Rent | LEAS_INT_ON_ARR_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Include Days Grace Rent | LEAS_INT_ON_GRACE_RENT | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Days Grace | LEAS_GRACE_NUM | Number(3)<br>Min Val: 0<br>Max Val: 999 | - | Can Only Be Set If Interest On Late Rent Is Y | - | - |
| % Above/Below Base for Rent | LEAS_ABOVE_BASE_AMT | Number(4,2)<br>Min Val: -99.99<br>Max Val: 99.99 | - | Can Only Be Set If Interest On Late Rent Is Y | - | - |
| Charge Interest On Late S/C | LEAS_INT_ON_SC_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Include Days Grace Non Rent | LEAS_INT_ON_GRACE_NON_RENT | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Grace Num Non Rent | LEAS_GRACE_NUM_NON_RENT | Number(3)<br>Min Val: 0<br>Max Val: 999 | - | Can Only Be Set If Interest On Late Non- Rent Is Y | - | - |
| % Above/Below Base for S/C | LEAS_SC_ABV_BEL_BASE_AMT | Number(4,2)<br>Min Val: -99.99<br>Max Val: 99.99 | - | Can Only Be Set If Interest On Late Non- Rent Is Y | - | - |
| Charge Interest on Late Review | LEAS_REV_INT_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| % Above/Below Base for Reviews | LEAS_REV_ABOVE_BASE_AMT | Number(4,2)<br>Min Val: -99.99<br>Max Val: 99.99 | - | Can Only Be Set If Interest On Late Review Is Y | - | - |
| Auto Generate | LEAS_AUTO_GENERATE | String(1) | N | Flag: (N)o, (Y)es. Can only Y  If Interest On Rent or Non-Rent Is Y  else N | - | - |
| Demand Type | LEAS_DEMAND_TYPE | String(1) | R | Flag: (I)mmediate Bill, (R)ent Demand. Default from Skyconf | - | - |
| Bank Base Rate | LEAS_BASE_RATE_NUM | String(3) | - | Bank Code. Mandatory If Interest On Arrears or Review Is Y  else NULL. Validate against Codebank | - | - |
| Reg Charge Statement | LEAS_REG_CHARGE_STATEMENT | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Is Lease VATable | LEAS_VATABLE_FLAG | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Rental Inclusive | LEAS_RENT_INC_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Privity of Contract | LEAS_PRIVITY_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Generate Zero Demands | LEAS_GENERATE_ZERO_DEMANDS | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Exchange Bank | LEAS_EXCH_CDBK_REF | String(3) | DEF | Bank Code | - | - |
| Exchange Rate | LEAS_EXCH_RATE_FLAG | String(1) | M | Flag: (M)iddle, (S)elling | - | - |
| Demand Notice | LEAS_DEMAND_NOTICE_CODE | String(3) | - | Code of Type: 'LDN' (Lease Demand Notice) | - | - |
| Straight-Line Accounting | LEAS_STR_LINE_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| S/L - Other Incentives Amount | LEAS_OTHER_INCENTIVES_AMT | Number(13,2)<br>Min Val: -99999999999.99<br>Max Val: 99999999999.99 | - | Can be set if Straight-Line Accounting Is Y, otherwise Null | - | - |
| S/L - Start Date | LEAS_STR_LINE_START | Date | - | Can be set if Straight-Line Accounting Is Y, otherwise Null | - | - |
| S/L - End Date | LEAS_STR_LINE_END | Date | - | Can be set if Straight-Line Accounting Is Y, otherwise Null | - | - |
| S/L - Ac Standard | LEAS_AC_STANDARD | String(3) | - | Code of Type: 'AS' (Accounting Standard). Can be set if Straight-Line Accounting Is Y, defaulting to Property's Group's S/L Ac Standard, otherwise Null | - | - |
| S/L - Independent Renewals | LEAS_SL_IND_RENEWAL | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Time is of Essence | LEAS_TIME_ESS_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Minimum Notice | LEAS_MIN_NTC_NUM | Number(2)<br>Min Val: 0<br>Max Val: 99 | - | Mandatory if Time is of Essence is Y. Default from Skyconf | - | - |
| Advance Notice | LEAS_ADV_NOTICE_NUM | Number(2)<br>Min Val: 0<br>Max Val: 99 | - | Mandatory if Time is of Essence is Y. Default from Skyconf | - | - |
| Demand after Expiry | LEAS_AFTR_EXP_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Extraction Type | LEAS_EXTRACT_CODE | String(3) | - | Code of Type: 'EXT' (Extraction Type) | - | - |
| Stop Bill Date | LEAS_STOPS_DATE | Date | - | Must Be After Lease Start Date | - | - |
| Stop By Code | LEAS_STOP_BY_CODE | String(3) | - | User Code | - | - |
| Stop By Description | LEAS_STOP_BY_DESC | String(120) | - | - | - | - |
| Stops Rcpt Date | LEAS_STOPS_RCPT_DATE | Date | {LEAS_STOPS_DATE} | Mandatory if Stop Bill Date is set. | - | - |
| Rem Flag | LEAS_REM_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Rmls Cdgn Ref | LEAS_RMLS_CDGN_REF | String(3) | - | Code of Type: 'RLT' (Reminder Letter Types). NULL if Send Reminders is N | - | - |
| Tenancy in Breach | LEAS_BREACH_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Breach Date | LEAS_BREACH_DATE | Date | - | NULL if Tenancy in Breach is N | - | - |
| Agreement | LEAS_AGRMT_DESC | String(30) | - | NULL if Tenancy in Breach is N | - | - |
| Print Demads | LEAS_PRNT_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Print Demand Set by | LEAS_PRNT_BY_CODE | String(3) | - | User Code | - | - |
| Print Demand Set on | LEAS_PRNT_BY_DATE | Date | - | - | - | - |
| Print Demand Reason | LEAS_PRNT_BY_DESC | String(30) | - | - | - | - |
| Receive Payment | LEAS_RCVE_FLAG | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Receive Payment set by | LEAS_RCVE_BY_CODE | String(3) | - | User Code. Mandatory if Receive Payment is N | - | - |
| Receive Payment set on | LEAS_RCVE_BY_DATE | Date | - | Mandatory if Receive Payment is N | - | - |
| Rcve By Desc Code | LEAS_RCVE_BY_DESC_CODE | String(3) | - | Code of Type: 'LRR' (Lease Receive Payment Reason). Mandatory if Receive Payment is N | - | - |
| Override Disclamer | LEAS_DISCLM_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Override Disclamer set by | LEAS_DISCLM_BY_CODE | String(3) | - | User Code | - | - |
| Override Disclamer Set On | LEAS_DISCLM_BY_DATE | Date | - | - | - | - |
| Override Disclamer Reasomn | LEAS_DISCLM_BY_DESC | String(30) | - | - | - | - |
| EARLIEST REVIEW NOTICE DUE | LEAS_RVW_ERLST_DATE | Date | - | - | - | - |
| LATEST REVIEW NOTICE DUE | LEAS_RVW_LTST_DATE | Date | - | - | - | - |
| NOTICE SERVED | LEAS_RVW_SRVD_DATE | Date | - | - | - | - |
| NOTICE ACKNOWLEDGED | LEAS_RVW_AKNL_DATE | Date | - | - | - | - |
| TENANT COUNTER NOTICE DUE | LEAS_RVW_TNNT_CNTR_BY_DATE | Date | - | - | - | - |
| TENANT COUNTER NOTICE SERVED | LEAS_RVW_TNNT_CNTR_SRVD_DATE | Date | - | - | - | - |
| RICS DUE | LEAS_RVW_RICS_BY_DATE | Date | - | - | - | - |
| RICS APPLIED | LEAS_RVW_RICS_APPL_DATE | Date | - | - | - | - |
| SOLICITOR INSTRUCTED | LEAS_RVW_SLICTR_DATE | Date | - | - | - | - |
| LAST CONTACT | LEAS_RVW_LST_CNTCT_DATE | Date | - | - | - | - |
| EARLIEST S40 NOTICE DUE | LEAS_EXP_ERLST_S40_DATE | Date | - | - | - | - |
| LATEST S40 NOTICE DUE | LEAS_EXP_LTST_S40_DATE | Date | - | - | - | - |
| EARLIEST S25 NOTICE DUE | LEAS_EXP_ERLST_S25_DATE | Date | - | - | - | - |
| LATEST S25 NOTICE DUE | LEAS_EXP_LTST_S25_DATE | Date | - | - | - | - |
| S25 NOTICE SERVED | LEAS_EXP_S25_SRVD_DATE | Date | - | - | - | - |
| S25 NOTICE ACKNOWLEDGED | LEAS_EXP_S25_AKNL_DATE | Date | - | - | - | - |
| S26 NOTICE RECEIVED | LEAS_EXP_S26_RCVD_DATE | Date | - | - | - | - |
| S27 NOTICE RECEIVED | LEAS_EXP_S27_RCVD_DATE | Date | - | - | - | - |
| SOLICITOR INSTRUCTED | LEAS_EXP_SLICTR_DATE | Date | - | - | - | - |
| LAST CONTACT | LEAS_EXP_LST_CNTCT_DATE | Date | - | - | - | - |
| Prct Rent Use Gper | LEAS_PRCT_RENT_USE_GPER | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Prct Rent Annual Payment | LEAS_PRCT_RENT_ANNUAL_PAYMENT | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Stat Freq Code | LEAS_STAT_FREQ_CODE | String(3) | - | Frequency Code | - | - |
| Prct Rent Start | LEAS_PRCT_RENT_START | Date | - | Mandatory if Use Acc Periods is Y | - | - |
| Paym Freq Code | LEAS_PAYM_FREQ_CODE | String(3) | - | Frequency Code | - | - |
| Prct Rent Stat Days | LEAS_PRCT_RENT_STAT_DAYS | Number(8)<br>Min Val: 0<br>Max Val: 99 | - | Mandatory if Use Acc Periods is Y | - | - |
| Prct Rent Year Flag | LEAS_PRCT_RENT_YEAR_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Prct Rent Start Orig | LEAS_PRCT_RENT_START_ORIG | Date | - | - | - | - |
| Prct Rent Post Flag | LEAS_PRCT_RENT_POST_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Prct Rent Credit Flag | LEAS_PRCT_RENT_CREDIT_FLAG | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Prct Rent Accrual Ac | LEAS_PRCT_RENT_ACCRUAL_AC | String(8) | - | Foreign Key - groupacc. Mandatory if Post Income is Y | - | - |
| Min Rent Ann Adj | LEAS_MIN_RENT_ANN_ADJ | Number(13,2)<br>Min Val: 0<br>Max Val: 999.99 | - | - | - | - |
| Min Rent Floor | LEAS_MIN_RENT_FLOOR | Number(13,2)<br>Min Val: 0<br>Max Val: 99999999999.99 | - | - | - | - |
| Curr Rent Floor | LEAS_CURR_RENT_FLOOR | Number(13,2)<br>Min Val: 0<br>Max Val: 99999999999.99 | - | - | - | - |
| Abs Min Rent Floor | LEAS_ABS_MIN_RENT_FLOOR | String(1) | Y | Flag: (N)o, (Y)es | - | - |
| Produce Standard Stmt Rep | LEAS_PRODUCE_STANDARD_STMT_REP | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Prct Rent Report | LEAS_PRCT_RENT_REPORT | String(30) | - | - | - | - |
| Sales Anal Rep | LEAS_SALES_ANAL_REP | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Sales Analysis Report | LEAS_SALES_ANALYSIS_REPORT | String(30) | - | - | - | - |
| Cont Curr Code | LEAS_CONT_CURR_CODE | String(3) | - | Code of Type: 'CUR' (Currency Codes). Derived from Property | - | - |
| Mortgage Flag | LEAS_MORTGAGE_FLAG | String(1) | L | Flag: (L)ease, (M)ortgage | - | - |
| Quot Ref | LEAS_QUOT_REF | String(8) | - | Foreign Key | - | - |
| Mort Type Code | LEAS_MORT_TYPE_CODE | String(3) | - | Code of Type: 'MTY' (Drawdown Type Code) | - | - |
| Include Days Grace (Mortgage) | LEAS_INT_ON_GRACE_MORT | String(1) | - | Flag: (N)o, (Y)es | - | - |
| Interest on Mortgage | LEAS_INT_ON_MORT_FLAG | String(1) | - | Flag: (N)o, (Y)es | - | - |
| %Above Margin | LEAS_MORT_ABOVE_MARGIN_AMT | Number(8,5)<br>Min Val: 0<br>Max Val: 99999999.99999 | - | - | - | - |
| Arrangement Fee | LEAS_MORT_ARRANGE_FEE | Number(13,2) | - | - | - | - |
| Borrower Hedged | LEAS_MORT_BORR_HEDGE | String(1) | - | - | - | - |
| Borrower Hedging Comment | LEAS_MORT_BORR_HEDGE_COMMENT | String(1000) | - | - | - | - |
| Lender Hedged | LEAS_MORT_LEND_HEDGE | String(1) | - | - | - | - |
| Lender Hedging Comment | LEAS_MORT_LEND_HEDGE_COMMENT | String(1000) | - | - | - | - |
| Lender Hedging Ref | LEAS_MORT_LEND_HEDGE_REF | String(20) | - | - | - | - |
| Mortgage Ref | LEAS_MORT_REF | String(8) | - | Foreign Key - mortgage | - | - |
| Mortgage Repayment Major Code | LEAS_MORT_REPAY_CDMJ | String(3) | - | Major Analysis Code | - | - |
| Mortgage Repayment Minor Code | LEAS_MORT_REPAY_CDMI | String(3) | - | Foreign Key | - | - |
| Days Grace (Mortgage) | LEAS_GRACE_NUM_MORT | Number(3)<br>Min Val: 0<br>Max Val: 999 | - | - | - | - |
| Duration Gilt | LEAS_DURATION_GILT | Number(10,5) | - | - | - | - |
| Rent Inclusive of Sched Type 1 | LEAS_RENT_INC_FLAG1 | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Rent Inclusive of Sched Type 2 | LEAS_RENT_INC_FLAG2 | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Rent Inclusive of Sched Type 3 | LEAS_RENT_INC_FLAG3 | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Rent Inclusive of Sched Type 4 | LEAS_RENT_INC_FLAG4 | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Rent Inclusive of Sched Type 5 | LEAS_RENT_INC_FLAG5 | String(1) | N | Flag: (N)o, (Y)es | - | - |
| Receivable Asset | LEAS_REC_ASSET_AC_CODE | String(8) | - | GL Account Code | - | - |
| Deferred Profit | LEAS_DEFER_PROFIT_AC_CODE | String(8) | - | GL Account Code | - | - |
| Unguaranteed Residual Asset | LEAS_UNGTD_RESID_AC_CODE | String(8) | - | GL Account Code | - | - |
| Interest Receivable | LEAS_REC_INTEREST_AC_CODE | String(8) | - | GL Account Code | - | - |
| Ungtd Asset Int Receivable | LEAS_RESID_INTEREST_AC_CODE | String(8) | - | GL Account Code | - | - |
| Sublease Gain/Loss | LEAS_SUBLEASE_PL_AC_CODE | String(8) | - | GL Account Code | - | - |
| Straight-Line B/S | LEAS_AR_ACCRUAL_AC_CODE | String(8) | - | GL Account Code | - | - |
| Straight-Line P/L | LEAS_AR_OFFSET_AC_CODE | String(8) | - | GL Account Code | - | - |
| Receivable Impairment Expense | LEAS_REC_IMPAIR_EXP_AC_CODE | String(8) | - | GL Account Code | - | - |
| Receivable Catch-up Adjustment | LEAS_REC_TRANS_ADJ_AC_CODE | String(8) | - | GL Account Code | - | - |
| Receivable GASB Lease Revenue | LEAS_GASB_INCOME_AC_CODE | String(8) | - | GL Account Code | - | - |
| Receivable Remeasure Gain/Loss | LEAS_REC_REMEAS_PL_AC_CODE | String(8) | - | GL Account Code | - | - |
| Non-Rent Income | LEAS_NON_RENT_INC_AC_CODE | String(8) | - | GL Account Code | - | - |
| Collection ID | LEAS_LI_REF | String(8)<br>Max Len: 8 | - | - | - | - |

---

## Validation Rules

### Table-Level Validations

Each expression identifies the condition that makes a row invalid. Report the workbook's stated message when the expression evaluates to true.

| Message | Validation |
| --- | --- |
| At lease one of the Rental Inclusive Flags for Schedules 1 to 5 must be Y if leas_rent_inc_flag is Y | invalid if (:leas_rent_inc_flag = 'Y') and ((:leas_rent_inc_flag1 <> 'Y') and (:leas_rent_inc_flag2 <> 'Y') and (:leas_rent_inc_flag3 <> 'Y') and (:leas_rent_inc_flag4 <> 'Y') and (:leas_rent_inc_flag5 <> 'Y')) |
| Cannot separate invoices by analysis code invoice grouping if the Lease's Demand Type is Rent Statement, or the Tenant's Composite Billing is set | invalid if (:leas_use_grad_inv_grp_code = 'Y') and ((:leas_demand_type_flag = 'R') or (:tnnt_composite_bill_flag = 'Y')) |
| Cannot separate invoices by due date if the Lease's Demand Type is Rent Statement, or the Tenant's Composite Billing is set | invalid if (:leas_sep_inv_by_due_date = 'Y') and ((:leas_demand_type_flag = 'R') or (:tnnt_composite_bill_flag = 'Y')) |
| Cannot separate invoices by transaction if the Lease's Demand Type is Rent Statement, or the Tenant's Composite Billing is set | invalid if (:leas_sep_inv_by_trans = 'Y') and ((:leas_demand_type_flag = 'R') or (:tnnt_composite_bill_flag = 'Y')) |
| Continuing Occupancy is not set, but Expiry Date is blank | invalid if (NVL(:leas_cont_occ_flag, 'N') = 'N') and (:leas_expiry_date is Null) |
| Continuing Occupancy is set, but Expiry Date is not blank | invalid if (:leas_cont_occ_flag = 'Y') and (:leas_expiry_date is not Null) |
| Currency Code must be same as the Tenant's Currency Code | invalid if (:leas_tnnt_ref is not Null) and (:leas_cur_code <> tenant(:leas_tnnt_ref).tnnt_cur_code) |
| Demand is set as Proforma, but Vatable is not set | invalid if (:leas_demand_type_flag = 'P') and (:leas_vatable_flag <> 'Y') |
| Demise of Live Rental Lease must be occupied | invalid if (:leas_dmse_ref is not Null) and (:dmse_status_code_process_flag <> 1) and (:leas_rental_flag = 'Y') and (:leas_status_code_process_flag = 1) |
| Demise of non-Live Rental Lease must be associated with a Live Rental Lease if Demise is occupied | invalid if (:leas_dmse_ref is not Null) and (:dmse_status_code_process_flag = 1) and (:leas_rental_flag = 'Y') and (:leas_status_code_process_flag = 0) and (not (lease(dmse_ref: :leas_dmse_ref, rental_flag: 'Y', status_code_process_flag: 1).Existent)) |
| Demise of Rental Lease must belong to same Property as Lease | invalid if (:leas_dmse_ref is not Null) and (demise(:leas_dmse_ref).dmse_prop_ref <> :leas_prop_ref) and (:leas_rental_flag = 'Y') |
| Expiry Date must be on or after Start Date | invalid if (:leas_expiry_date is not Null) and (:leas_expiry_date < :leas_start_date) |
| If Property is not mixed-use then Lease's Vatable Flag would normally be equal to Property's Tax Option Flag | warning if (property(:leas_prop_ref).prop_mixed_use_flag <> 'Y') and (:leas_vatable_flag <> property(:leas_prop_ref).prop_tax_option_flag) |
| Inter_company Lease is already linked to a Lease Payable | invalid if (:leas_icmp_hlse_ref is not Null) and (headleas(:leas_icmp_hlse_ref).hlse_icmp_leas_ref is not Null) |
| Interest On Late Non-Rent is not set, but Days Grace is not blank | invalid if (NVL(:leas_int_on_sc_flag, 'N') = 'N') and (:leas_grace_num_non_rent is not Null) |
| Interest On Late Rent is not set, but % Over/Below Base for Rent is not blank | invalid if (NVL(:leas_int_on_arr_flag, 'N') = 'N') and (:leas_above_base_amt is not Null) |
| Interest On Late Rent is not set, but Days Grace is not blank | invalid if (NVL(:leas_int_on_arr_flag, 'N') = 'N') and (:leas_grace_num is not Null) |
| Interest On Late Rent/SC And Review is not set, But Bank is not blank | invalid if (NVL(:leas_int_on_arr_flag, 'N') = 'N') and (NVL(:leas_rev_int_flag, 'N') = 'N') and (NVL(:leas_int_on_sc_flag, 'N') = 'N') and (:leas_base_rate_num is not Null) |
| Interest On Late Rent/SC or Review is set, but Bank (Base Rate) is blank | invalid if ((:leas_int_on_arr_flag = 'Y') or (:leas_rev_int_flag = 'Y') or (:leas_int_on_sc_flag = 'Y')) and (:leas_base_rate_num is Null) |
| Interest On Late Review is not set, but % Over/Below Base for Review is not blank | invalid if (NVL(:leas_rev_int_flag, 'N') = 'N') and (:leas_rev_above_base_amt is not Null) |
| Interest On Late SC is not set, but % Over/Below Base for SC is not blank | invalid if (NVL(:leas_int_on_sc_flag, 'N') = 'N') and (:leas_sc_abv_bel_base_amt is not Null) |
| leas_ac_standard must be blank if Straight-Line Rent is not installed or leas_str_line_flag is N | invalid if ((:skyc_lease_incentives_inst <> 'Y') or (:leas_str_line_flag = 'N')) and (:leas_ac_standard is not Null) |
| leas_ar_accrual_ac_code must be a balance sheet account in the Group's chart of accounts | invalid if chartacc(code: :leas_ar_accrual_ac_code, structure: :leas_coac_type, process flag of ac_type: 2 or 3).Inexistent |
| leas_ar_offset_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_ar_offset_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_defer_profit_ac_code must be a balance sheet account in the Group's chart of accounts | invalid if chartacc(code: :leas_defer_profit_ac_code, structure: :leas_coac_type, process flag of ac_type: 2 or 3).Inexistent |
| leas_gasb_income_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_gasb_income_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_non_rent_inc_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_non_rent_inc_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_other_incentives_amt must be blank if Straight-Line Rent is not installed or leas_str_line_flag is N | invalid if ((:skyc_lease_incentives_inst <> 'Y') or (:leas_str_line_flag = 'N')) and (:leas_other_incentives_amt is not Null) |
| leas_rec_asset_ac_code must be a balance sheet account in the Group's chart of accounts | invalid if chartacc(code: :leas_rec_asset_ac_code, structure: :leas_coac_type, process flag of ac_type: 2 or 3).Inexistent |
| leas_rec_impair_exp_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_rec_impair_exp_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_rec_interest_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_rec_interest_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_rec_remeas_pl_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_rec_remeas_pl_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_rec_trans_adj_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_rec_trans_adj_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_ref contains prohibited characters | invalid if (:leas_ref is not Null) and (:leas_ref matches Regex('[^a-zA-Z0-9/.:%!$*_+&^-]')) |
| leas_resid_interest_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_resid_interest_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_rmls_cdgn_ref must only be specified if leas_rem_flag is Y | invalid if (:leas_rem_flag <> 'Y') and (:leas_rmls_cdgn_ref is not Null) |
| leas_shared_tenancy_flag must be Y if Shared Tenancy details exist | invalid if (tnntshare(leas_ref: :leas_ref).Existent) |
| leas_sl_ind_renewal must be N if Straight-Line Rent is not installed or leas_str_line_flag is N | invalid if ((:skyc_lease_incentives_inst <> 'Y') or (:leas_str_line_flag = 'N')) and (:leas_sl_ind_renewal <> 'N') |
| leas_start_date is before earliest start date of all Units associated with Lease | invalid if (:leas_start_date is not Null) and (:leas_dmse_ref is not Null) and (:leas_start_date is before earliest unit(dmse_ref: :leas_dmse_ref).unit_start_date) |
| leas_str_line_end must be blank if Straight-Line Rent is not installed or leas_str_line_flag is N | invalid if ((:skyc_lease_incentives_inst <> 'Y') or (:leas_str_line_flag = 'N')) and (:leas_str_line_end is not Null) |
| leas_str_line_flag must be N if Straight-Line Rent is not installed | invalid if (:skyc_lease_incentives_inst <> 'Y') and (:leas_str_line_flag = 'Y') |
| leas_str_line_start must be blank if Straight-Line Rent is not installed or leas_str_line_flag is N | invalid if ((:skyc_lease_incentives_inst <> 'Y') or (:leas_str_line_flag = 'N')) and (:leas_str_line_start is not Null) |
| leas_sublease_pl_ac_code must be a profit and loss account in the Group's chart of accounts | invalid if chartacc(code: :leas_sublease_pl_ac_code, structure: :leas_coac_type, process flag of ac_type: 1).Inexistent |
| leas_ungtd_resid_ac_code must be a balance sheet account in the Group's chart of accounts | invalid if chartacc(code: :leas_ungtd_resid_ac_code, structure: :leas_coac_type, process flag of ac_type: 2 or 3).Inexistent |
| Maximum Notice is mandatory if Time Essence Flag is Y | invalid if (:leas_time_ess_flag = 'Y') and (:leas_adv_notice_num is Null) |
| Minimum Notice is mandatory if Time Essence Flag is Y | invalid if (:leas_time_ess_flag = 'Y') and (:leas_min_ntc_num is Null) |
| Number of live leases would be within 10 of exceeding maximum permitted by lease licence if all live leases were loaded | warning if (:leas_status_code_process_flag = 1) and (:live_leas_max > 0) and (:lease_licence_flag in ('C', 'S')) and (if (:lease_licence_flag = 'C') then ((not ((:live_all_in_db + :live_leas_validating) > :live_all_max)) and ((:live_all_in_db + :live_leas_validating) > (:live_all_max - 10))) else if ((not ((:live_leas_in_db + :live_leas_validating) > :live_leas_max)) and ((:live_leas_in_db + :live_leas_validating) > (:live_leas_max - 10)))) |
| Number of live leases would exceed maximum permitted by lease licence if all live leases were loaded | invalid if (:leas_status_code_process_flag = 1) and (:live_leas_max > 0) and (:lease_licence_flag in ('C', 'S')) and (if (:lease_licence_flag = 'C') then ((:live_all_in_db + :live_leas_validating) > :live_all_max) else if ((:live_leas_in_db + :live_leas_validating) > :live_leas_max)) |
| Receive Payment Fields are all mandatory when the Receive Payment Flag is N | invalid if (NVL(:leas_rcve_flag, 'N') = 'N') and ((:leas_rcve_by_code is Null) or (:leas_rcve_by_date is Null) or (:leas_rcve_by_desc_code is Null)) |
| Rent cannot be flagged as inclusive of schedule type 1 if leas_rent_inc_flag is not Y or Schedule Type 1 is not specified | invalid if (:leas_rent_inc_flag1 <> 'N') and ((:leas_rent_inc_flag <> 'Y') or (skyconf.skyc_bal1_type is Null)) |
| Rent cannot be flagged as inclusive of schedule type 2 if leas_rent_inc_flag is not Y or Schedule Type 2 is not specified | invalid if (:leas_rent_inc_flag2 <> 'N') and ((:leas_rent_inc_flag <> 'Y') or (skyconf.skyc_bal2_type is Null)) |
| Rent cannot be flagged as inclusive of schedule type 3 if leas_rent_inc_flag is not Y or Schedule Type 3 is not specified | invalid if (:leas_rent_inc_flag3 <> 'N') and ((:leas_rent_inc_flag <> 'Y') or (skyconf.skyc_bal3_type is Null)) |
| Rent cannot be flagged as inclusive of schedule type 4 if leas_rent_inc_flag is not Y or Schedule Type 4 is not specified | invalid if (:leas_rent_inc_flag4 <> 'N') and ((:leas_rent_inc_flag <> 'Y') or (skyconf.skyc_bal4_type is Null)) |
| Rent cannot be flagged as inclusive of schedule type 5 if leas_rent_inc_flag is not Y or Schedule Type 5 is not specified | invalid if (:leas_rent_inc_flag5 <> 'N') and ((:leas_rent_inc_flag <> 'Y') or (skyconf.skyc_bal5_type is Null)) |
| Rental Space is mandatory if rental flag is Y | invalid if (:leas_rental_flag = 'Y') and (:leas_dmse_ref is Null) |
| Rental Space must be blank if Rental flag is N | invalid if (:leas_rental_flag = 'N') and (:leas_dmse_ref is not Null) |
| Stop Rcpt Date is mandatory when the Stop Bill Date is set | invalid if (:leas_stops_date is not Null) and (:leas_stops_rcpt_date is Null) |
| Stops Date is before the Start Date | invalid if (:leas_stops_date is not Null) and (:leas_start_date > :leas_stops_date) |
| Termination Date must be on or after Start Date | invalid if (:leas_term_date is not Null) and (:leas_term_date < :leas_start_date) |
| Termination Date must be specified for an archived lease | invalid if (:leas_status_code is not Null) and (codesgen(cdty_ref: 'LS', cdgn_ref: :leas_status_code).cdgn_process_flag = 0) and (:leas_term_date is Null) |

### Field-Level Validation and Derivation

| Label | PLE Field | Mode | Validation | Derivation |
| --- | --- | --- | --- | --- |
| Group Ref | LEAS_GROP_REF | Derived | Must be: groups.grop_ref | property(leas_prop_ref).prop_grop_ref |
| Organisation Ref | LEAS_ORGN_REF | Client Data | Must be: organisation.orgn_ref | - |
| Operation Reference | LEAS_COMP_REF | Derived | Must be: company.comp_ref | property(leas_prop_ref).prop_comp_ref |
| Property Reference | LEAS_PROP_REF | Client Data | Must be: property.prop_ref | - |
| Rental Space Ref | LEAS_DMSE_REF | Client Data | Must be: demise.dmse_ref | - |
| Lease Reference | LEAS_REF | Client Data | Primary Key: lease.leas_ref | - |
| Performed Move Out | LEAS_PERFORMED_MOVE_OUT | Derived | Must be: Flag: (N)o, (Y)es | if (codesgen(cdty_ref: 'LS', cdgn_ref: :leas_status_code).cdgn_process_flag = 0) then 'Y' else 'N' |
| Tenant Reference | LEAS_TNNT_REF | Client Data | Must be: tenant.tnnt_ref | - |
| Type of Lease | LEAS_TYPE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LT' | - |
| Status | LEAS_STATUS_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LS' | - |
| User | LEAS_USER_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Doc Lan Code | LEAS_DOC_LAN_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LAN' | - |
| Rental Flag | LEAS_RENTAL_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Shared Tenancy Flag | LEAS_SHARED_TENANCY_FLAG | System Default | Must be: Flag: (N)o, (Y)es | - |
| Term of Lease (Years) | LEAS_TERM_YEAR_NUM | Derived | - | if ((:leas_cont_occ_flag = 'N') and (:leas_start_date is not Null) and (:leas_expiry_date is not Null)) then (Term(Start_Date: :leas_start_date, end_date: :leas_expiry_date).Years) |
| Term of Lease (Months) | LEAS_TERM_MONTH_NUM | Derived | - | if ((:leas_cont_occ_flag = 'N') and (:leas_start_date is not Null) and (:leas_expiry_date is not Null)) then (Term(Start_Date: :leas_start_date, end_date: :leas_expiry_date).Months) |
| Use Analysis Invoice Grouping | LEAS_USE_GRAD_INV_GRP_CODE | Client Data | Must be: Flag: (N)o, (Y)es | if ((:leas_demand_type_flag <> 'R') and (:tnnt_composite_bill_flag <> 'Y')) then 'Y' |
| Separate Invoices By Due Date | LEAS_SEP_INV_BY_DUE_DATE | Client Data | Must be: Flag: (N)o, (Y)es | if (:leas_sep_inv_by_due_date is Null) then 'N' |
| Separate Invoices By Trans | LEAS_SEP_INV_BY_TRANS | Client Data | Must be: Flag: (N)o, (Y)es | if (:leas_sep_inv_by_trans is Null) then 'N' |
| Term Day Num | LEAS_TERM_DAY_NUM | Derived | - | if ((:leas_cont_occ_flag = 'N') and (:leas_start_date is not Null) and (:leas_expiry_date is not Null)) then (Term(Start_Date: :leas_start_date, end_date: :leas_expiry_date).Days) |
| Landlord and Tenant Act | LEAS_LNLD_TNNT_ACT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Continuing Occupancy | LEAS_CONT_OCC_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Inter-Company Lease Payable | LEAS_ICMP_HLSE_REF | Client Data | Foreign Key | - |
| Is Lease Current | LEAS_CURRENT_FLAG | Client Data | Must be: Flag: (C)urrent, (N)o Accounting, (R)educed Accounting | - |
| Review Basis | LEAS_REVIEW_BASIS | Client Data | Must be: Flag: (I)ndexed, (M)ixed, (N)egotiated, (O)ther | - |
| Turnover Flag | LEAS_TURNOVER_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Demand Type | LEAS_DEMAND_TYPE_FLAG | Client Data | Must be: Flag: (P)roforma, (R)ent Statment, (S)tandard | - |
| Charge Interest on Late Rent | LEAS_INT_ON_ARR_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Include Days Grace Rent | LEAS_INT_ON_GRACE_RENT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Charge Interest On Late S/C | LEAS_INT_ON_SC_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Include Days Grace Non Rent | LEAS_INT_ON_GRACE_NON_RENT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Charge Interest on Late Review | LEAS_REV_INT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Auto Generate | LEAS_AUTO_GENERATE | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Demand Type | LEAS_DEMAND_TYPE | Client Data | Must be: Flag: (I)mmediate Bill, (R)ent Demand | - |
| Bank Base Rate | LEAS_BASE_RATE_NUM | Client Data | Must be: codebank.cdbk_code | - |
| Reg Charge Statement | LEAS_REG_CHARGE_STATEMENT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Is Lease VATable | LEAS_VATABLE_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | if (:leas_vatable_flag is Null) then (property(:leas_prop_ref).prop_tax_option_flag) |
| Rental Inclusive | LEAS_RENT_INC_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Privity of Contract | LEAS_PRIVITY_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Generate Zero Demands | LEAS_GENERATE_ZERO_DEMANDS | Client Data (Derived if Null) | Must be: Flag: (N)o, (Y)es | If null....<br>skyconf.skyc_generate_zero_demands |
| Exchange Bank | LEAS_EXCH_CDBK_REF | Client Data (Derived if Null) | Must be: codebank.cdbk_code | If null....<br>codebank(system_flag: 'Y').cdbk_code |
| Exchange Rate | LEAS_EXCH_RATE_FLAG | Client Data (Derived if Null) | Must be: Flag: (M)iddle, (S)elling | If null....<br>skyconf.skyc_exch_rate_flag |
| Demand Notice | LEAS_DEMAND_NOTICE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LDN' | - |
| Straight-Line Accounting | LEAS_STR_LINE_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| S/L - Ac Standard | LEAS_AC_STANDARD | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'AS' | if ((:skyc_lease_incentives_inst = 'Y') and (:leas_str_line_flag = 'Y') and (:leas_ac_standard is Null)) then (groups((property(:leas_prop_ref).prop_grop_ref)).grop_ac_standard) |
| S/L - Independent Renewals | LEAS_SL_IND_RENEWAL | Client Data (Derived if Null) | Must be: Flag: (N)o, (Y)es | If null....<br>if (:leas_str_line_flag = 'Y') then (skyconf.skyc_sl_ind_renewal) else 'N' |
| Time is of Essence | LEAS_TIME_ESS_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Minimum Notice | LEAS_MIN_NTC_NUM | Client Data (Derived if Null) | - | If null....<br>if (:leas_comp_ref is not Null) then (fwskyconf.fw_get_rvw_min_max_ntc(comp_ref: :leas_comp_ref).pk_rvw_min_ntc) |
| Advance Notice | LEAS_ADV_NOTICE_NUM | Client Data (Derived if Null) | - | If null....<br>if (:leas_comp_ref is not Null) then (fwskyconf.fw_get_rvw_min_max_ntc(comp_ref: :leas_comp_ref).pk_rvw_max_ntc) |
| Demand after Expiry | LEAS_AFTR_EXP_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Extraction Type | LEAS_EXTRACT_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'EXT' | - |
| Stop By Code | LEAS_STOP_BY_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Rem Flag | LEAS_REM_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rmls Cdgn Ref | LEAS_RMLS_CDGN_REF | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'RLT' | - |
| Tenancy in Breach | LEAS_BREACH_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Print Demads | LEAS_PRNT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Print Demand Set by | LEAS_PRNT_BY_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Receive Payment | LEAS_RCVE_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Receive Payment set by | LEAS_RCVE_BY_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Rcve By Desc Code | LEAS_RCVE_BY_DESC_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'LRR' | - |
| Override Disclamer | LEAS_DISCLM_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Override Disclamer set by | LEAS_DISCLM_BY_CODE | Client Data | Must be: codeuser.cdus_code | - |
| Prct Rent Use Gper | LEAS_PRCT_RENT_USE_GPER | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Prct Rent Annual Payment | LEAS_PRCT_RENT_ANNUAL_PAYMENT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Stat Freq Code | LEAS_STAT_FREQ_CODE | Client Data | Must be: codefreq.cdfq_code | - |
| Paym Freq Code | LEAS_PAYM_FREQ_CODE | Client Data | Must be: codefreq.cdfq_code | - |
| Prct Rent Year Flag | LEAS_PRCT_RENT_YEAR_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Prct Rent Post Flag | LEAS_PRCT_RENT_POST_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Prct Rent Credit Flag | LEAS_PRCT_RENT_CREDIT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Prct Rent Accrual Ac | LEAS_PRCT_RENT_ACCRUAL_AC | Client Data | Must be: groupacc.gacc_code with groupacc.gacc_grop_ref = leas_grop_ref | - |
| Abs Min Rent Floor | LEAS_ABS_MIN_RENT_FLOOR | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Produce Standard Stmt Rep | LEAS_PRODUCE_STANDARD_STMT_REP | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Sales Anal Rep | LEAS_SALES_ANAL_REP | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Negotiated Major | LEAS_MAIN_RENT_CDMJ_REF | System Default | Must be: codeamaj.cdmj_ref | - |
| Negotiated Minor | LEAS_MAIN_RENT_CDMI_REF | System Default | Must be: gropanal.ganl_cdmi_ref with gropanal.ganl_cdmj_ref = leas_main_rent_cdmj_ref and gropanal.ganl_grop_ref = leas_grop_ref | - |
| Cont Curr Code | LEAS_CONT_CURR_CODE | Client Data (Derived if Null) | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUR' | If null....<br>if ((mig_config.mcfg_dflt_cont_curr_code) = 'CONTEXT') then ((property(:leas_prop_ref).prop_cont_curr_code)) else ((mig_config.mcfg_dflt_cont_curr_code)) |
| Lease Currency Code | LEAS_CUR_CODE | Derived | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'CUR' | property(:leas_prop_ref).prop_currency_code |
| Entity Usage Code | LEAS_USAGE_CODE | System Default | Usage Code | - |
| Mortgage Flag | LEAS_MORTGAGE_FLAG | Client Data | Must be: Flag: (L)ease, (M)ortgage | - |
| Lease Revert Flag | LEAS_REVERT_FLAG | System Default | Must be: Flag: (N)o, (Y)es | - |
| Quot Ref | LEAS_QUOT_REF | Client Data | Foreign Key | - |
| Mort Type Code | LEAS_MORT_TYPE_CODE | Client Data | Must be: codesgen.cdgn_ref with cdgn_cdty_ref = 'MTY' | - |
| Include Days Grace (Mortgage) | LEAS_INT_ON_GRACE_MORT | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Interest on Mortgage | LEAS_INT_ON_MORT_FLAG | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Mortgage Ref | LEAS_MORT_REF | Client Data | Must be: mortgage.mort_ref | - |
| Mortgage Repayment Major Code | LEAS_MORT_REPAY_CDMJ | Client Data | Must be: codeamaj.cdmj_ref | - |
| Mortgage Repayment Minor Code | LEAS_MORT_REPAY_CDMI | Client Data | Foreign Key | - |
| Rent Inclusive of Sched Type 1 | LEAS_RENT_INC_FLAG1 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rent Inclusive of Sched Type 2 | LEAS_RENT_INC_FLAG2 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rent Inclusive of Sched Type 3 | LEAS_RENT_INC_FLAG3 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rent Inclusive of Sched Type 4 | LEAS_RENT_INC_FLAG4 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Rent Inclusive of Sched Type 5 | LEAS_RENT_INC_FLAG5 | Client Data | Must be: Flag: (N)o, (Y)es | - |
| Residential Flag | LEAS_RESIDENTIAL_FLAG | System Default | Must be: Flag: (N)o, (Y)es | - |

### Uniqueness Rules

| Scope | Name | Restriction | Fields |
| --- | --- | --- | --- |
| Maximum | LEASEI1 | None | LEAS_COMP_REF, LEAS_PROP_REF, LEAS_REF |
| Maximum | LEASEI3 | None | LEAS_PROP_REF, LEAS_REF |
| Maximum | LEASEI4 | None | LEAS_USAGE_CODE, LEAS_REF |
| Maximum | LEASEI7 | None | LEAS_QUOT_REF |
| Maximum | Primary Key | None | LEAS_REF |

## Internal Derived Fields

These fields are calculated or checked internally during processing; they are not intake columns.

| Field | Timing | Derivation |
| --- | --- | --- |
| CDMI_TERI_CODE | Default | if (skyconf.skyc_teri_flag = 'Y') then (codeamin(cdmj_ref: :leas_main_rent_cdmj_ref, cdmi_ref: :leas_main_rent_cdmi_ref).cdmi_teri_code) |
| DMSE_STATUS_CODE_PROCESS_FLAG | Default | codesgen(cdty_ref: 'DLS', cdgn_ref: (demise(:leas_dmse_ref).dmse_status_code)).cdgn_process_flag |
| LEAS_COAC_TYPE | Default | groups(:leas_grop_ref).grop_coac_type |
| LEAS_STATUS_CODE_PROCESS_FLAG | Default | codesgen(cdty_ref: 'LS', cdgn_ref: :leas_status_code).cdgn_process_flag |
| LEASE_LICENCE_FLAG | Default | fwsso_ad_site.wtss_lease_licence_flag |
| LIVE_ALL_IN_DB | Default | (:live_leas_in_db + :live_hlse_in_db) |
| LIVE_ALL_MAX | Default | (:live_leas_max + :live_hlse_max) |
| LIVE_HLSE_IN_DB | Default | Nvl((headleas(equip_lease: 'N', status_code_process_flag: 1).cnt), 0) |
| LIVE_HLSE_MAX | Default | Nvl((fwsso_ad_site.wtss_lease_pay_count), 0) |
| LIVE_LEAS_IN_DB | Default | Nvl((lease(status_code_process_flag: 1).cnt), 0) |
| LIVE_LEAS_MAX | Default | Nvl((fwsso_ad_site.wtss_lease_rec_count), 0) |
| LIVE_LEAS_VALIDATING | Default | lease(validating, status_code_process_flag: 1).count |
| SKYC_LEASE_INCENTIVES_INST | Default | skyconf.skyc_lease_incentives_inst |
| TERI_CODE | Default | if (skyconf.skyc_teri_flag = 'Y') then (if (:leas_comp_ref = 'SYSTEM') then :leas_teri_code else (company(:leas_comp_ref).comp_teri_code)) |
| TNNT_COMPOSITE_BILL_FLAG | Default | tenant(:leas_tnnt_ref).tnnt_composite_bill_flag |

## Additional Processing Rules

Apply these workbook-defined tasks at the stated processing line or trigger.

| Id | Name | Line | Type | Triggers | Details | Internal Fields | Variables | Variable Calculations |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | Default | 0 | Run Condition | - | Always runnable | - | - | - |
| - | Default | 01 | Condition | - | IF (mig_sky_tables('LERNHIST').skyt_mig_flag <> 'Y') | - | - | - |
| - | Default | 01.01 | Insert | - | FOR EACH RECORD IN lease<br>WHERE<br>qcid IN {lease_h1_01(inserted during parent run).qcid}<br>INSERT INTO lernhist:<br>lerh_comp_ref = :leas_comp_ref<br>lerh_prop_ref = :leas_prop_ref<br>lerh_usage_code = 'LEA'<br>lerh_leas_hlse_ref = :leas_ref<br>lerh_leas_ref = :leas_ref<br>lerh_start_date = :leas_start_date<br>lerh_end_date = :leas_expiry_date<br>lerh_comment = :leas_comment<br>lerh_agreed_flag = 'Y' | - | - | - |
| - | Default | 02 | Condition | - | IF (mig_sky_tables('TNNTHIST').skyt_mig_flag <> 'Y') | - | - | - |
| - | Default | 02.01 | Insert | - | FOR EACH RECORD IN lease<br>WHERE<br>qcid IN {lease_h1_01(inserted during parent run).qcid}<br>AND leas_tnnt_ref IS NOT NULL<br>INSERT INTO tnnthist:<br>tnnh_comp_ref = :leas_comp_ref<br>tnnh_prop_ref = :leas_prop_ref<br>tnnh_leas_ref = :leas_ref<br>tnnh_tnnt_ref = :leas_tnnt_ref<br>tnnh_start_date = :leas_start_date<br>tnnh_end_date = QubeCore.QCNvl(leas_term_date, CASE WHEN leas_aftr_exp_flag = 'Y' THEN NULL ELSE leas_expiry_date END)<br>tnnh_bckgrnd_insert = 'Y'<br>tnnh_ac_ref = Null<br>tnnh_bill_addr_ref = :leas_tnnh_bill_addr_ref<br>tnnh_ass_flag = 'N' | - | - | - |
| - | Default | 03 | Condition | - | IF (mig_sky_tables('TNNTSHARE').skyt_mig_flag <> 'Y') | - | - | - |
| - | Default | 03.01 | Insert | - | FOR EACH RECORD IN lease<br>WHERE<br>qcid IN {lease_h1_01(inserted during parent run).qcid}<br>AND leas_tnnt_ref IS NOT NULL<br>AND leas_shared_tenancy_flag = 'Y'<br>INSERT INTO tnntshare:<br>tnsh_comp_ref = :leas_comp_ref<br>tnsh_leas_ref = :leas_ref<br>tnsh_tnnt_ref = :leas_tnnt_ref<br>tnsh_start_date = :leas_start_date | - | - | - |
| - | Default | 04 | Cursor | - | SELECT leas_prop_ref, leas_status_code, leas_tnnt_ref, leas_dmse_ref, leas_ref, leas_start_date, leas_review_basis, leas_rental_flag, leas_comp_ref, leas_term_date, qcid<br>FROM lease<br>WHERE qcid IN {lease_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | parent_prop_ref = (property(:leas_prop_ref).prop_parent_ref)<br>agmt_prop_ref = (if (:parent_prop_ref is not Null) then :parent_prop_ref else :leas_prop_ref)<br>agmt_sub_prop_ref = (if (:parent_prop_ref is not Null) then :leas_prop_ref)<br>agmt_entity_code = (if (:parent_prop_ref is not Null) then 'SPR' else 'PRO')<br>agmt_seqn_num = (seqnos('AGREEMENTS').seqn_num + 1)<br>leas_status_code_process_flag = (codesgen(cdty_ref: 'LS', cdgn_ref: :leas_status_code).cdgn_process_flag) | - | - |
| - | Default | 04.01 | Insert | - | INSERT INTO tnntmvin:<br>tnmv_prop_ref = :leas_prop_ref<br>tnmv_tnnt_ref = :leas_tnnt_ref<br>tnmv_dmse_ref = :leas_dmse_ref<br>tnmv_leas_ref = :leas_ref<br>tnmv_start_date = :leas_start_date<br>tnmv_rview_bsis = :leas_review_basis<br>tnmv_finish_date = Today<br>tnmv_user_code = skyconf.skyc_table_owner_code<br>tnmv_agmt_seqn_num = if (:leas_rental_flag = 'Y') then Null else :agmt_seqn_num | - | - | - |
| - | Default | 04.02 | Insert | - | INSERT INTO agreements:<br>agmt_prop_ref = :agmt_prop_ref<br>agmt_comp_ref = :leas_comp_ref<br>agmt_sub_prop_ref = :agmt_sub_prop_ref<br>agmt_leas_ref = :leas_ref<br>agmt_tnnt_ref = :leas_tnnt_ref<br>agmt_dmse_ref = :leas_dmse_ref<br>agmt_seqn_num = :agmt_seqn_num<br>agmt_acc_prop_flag = 'Y'<br>agmt_start_date = :leas_start_date<br>agmt_entity_code = :agmt_entity_code<br>agmt_acc_prop_type_flag = if (:agmt_entity_code = 'SPR') then ('S') else ('P')<br>agmt_usage_code = 'LEA'<br>agmt_rental_flag = :leas_rental_flag | - | - | - |
| - | Default | 04.03 | Condition | - | IF ((:leas_rental_flag = 'Y') and (:leas_status_code_process_flag in (0, 1))) | - | - | - |
| - | Default | 04.03.01 | Insert | - | INSERT INTO dmseleas:<br>dmle_comp_ref = :leas_comp_ref<br>dmle_prop_ref = :leas_prop_ref<br>dmle_leas_ref = :leas_ref<br>dmle_dmse_ref = :leas_dmse_ref<br>dmle_seqn_num = seqnos('DMSELEAS').seqn_num + 1<br>dmle_start_date = :leas_start_date<br>dmle_end_date = if (:leas_status_code_process_flag = 0) then (:leas_term_date) else (Null) | - | - | - |
| - | Default | 04.04 | Cursor | - | SELECT unit_comp_ref, unit_prop_ref, unit_ref, unit_start_date, qcid<br>FROM unit<br>WHERE unit_dmse_ref = :leas_dmse_ref<br>ORDER BY qcid | - | - | - |
| - | Default | 04.04.01 | Insert | - | INSERT INTO unitoccu:<br>unoc_comp_ref = :unit_comp_ref<br>unoc_prop_ref = :unit_prop_ref<br>unoc_unit_ref = :unit_ref<br>unoc_status_flag = 'O'<br>unoc_start_reason = 'ASS'<br>unoc_start_date = Max(:unit_start_date, :leas_start_date)<br>unoc_end_date = Null<br>unoc_leas_ref = :leas_ref<br>unoc_tnnt_ref = :leas_tnnt_ref | - | - | - |
| - | Default | 04.05 | Cursor | - | SELECT DISTINCT unde_unit_ref<br>FROM unitdmse<br>WHERE unde_dmse_ref = :leas_dmse_ref | - | - | - |
| - | Default | 04.05.01 | Delete | - | DELETE FROM unitoccu WHERE:<br>unoc_unit_ref = :unde_unit_ref<br>unoc_start_reason = 'LNK'<br>unoc_status_flag = 'V' | - | - | - |
| - | Default | 04.05.02 | Cursor | - | SELECT unoc_comp_ref, unoc_prop_ref, unoc_unit_ref, unoc_start_date, unoc_end_date, qcid<br>FROM unitoccu<br>WHERE unoc_unit_ref = :unde_unit_ref AND unoc_start_reason <> 'CRV'<br>ORDER BY unoc_start_date | prev_unoc_end_date = (Previous(:unoc_end_date)) | - | - |
| - | Default | 04.05.02.01 | Condition | - | IF ((Not first in cursor) and (:unoc_start_date > (Day after :prev_unoc_end_date))) | - | - | - |
| - | Default | 04.05.02.01.01 | Insert | - | INSERT INTO unitoccu:<br>unoc_comp_ref = :unoc_comp_ref<br>unoc_prop_ref = :unoc_prop_ref<br>unoc_unit_ref = :unoc_unit_ref<br>unoc_start_reason = 'LNK'<br>unoc_status_flag = 'V'<br>unoc_start_date = (Day after :prev_unoc_end_date)<br>unoc_end_date = (Day before :unoc_start_date) | - | - | - |
| - | Default | 04.05.02.02 | Condition | - | IF ((Last in cursor) and (:unoc_end_date is not Null)) | - | - | - |
| - | Default | 04.05.02.02.01 | Insert | - | INSERT INTO unitoccu:<br>unoc_comp_ref = :unoc_comp_ref<br>unoc_prop_ref = :unoc_prop_ref<br>unoc_unit_ref = :unoc_unit_ref<br>unoc_start_reason = 'LNK'<br>unoc_status_flag = 'V'<br>unoc_start_date = (Day after :unoc_end_date)<br>unoc_end_date = Null | - | - | - |
| - | Default | 05 | Cursor | Enabled on: PRCTRENTPER | SELECT leas_stat_freq_code, leas_prct_rent_use_gper, leas_grop_ref, leas_comp_ref, leas_prop_ref, leas_ref, leas_prct_rent_start, leas_expiry_date, leas_term_date, leas_paym_freq_code, leas_prct_rent_annual_payment, qcid<br>FROM lease<br>WHERE qcid IN {lease_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| - | Default | 05.01 | Condition | Enabled on: PRCTRENTPER | IF ((:leas_stat_freq_code is not Null) or (:leas_prct_rent_use_gper = 'Y')) | - | - | - |
| - | Default | 05.01.01 | Command | Enabled on: PRCTRENTPER | EXECUTE fwprctrentper.fw_produce_prctrentper_recs<br>PASSING:<br>pk_grop_ref: :leas_grop_ref<br>pk_comp_ref: :leas_comp_ref<br>pk_prop_ref: :leas_prop_ref<br>pk_leas_ref: :leas_ref<br>pk_supp_ref: Null<br>pk_start_date: :leas_prct_rent_start<br>pk_end_date: :leas_expiry_date<br>pk_term_date: :leas_term_date<br>pk_freq_code: :leas_stat_freq_code<br>pk_pay_freq_code: :leas_paym_freq_code<br>pk_existing_period_num: Null<br>pk_use_group_acc_per: :leas_prct_rent_use_gper<br>pk_annual_payment: :leas_prct_rent_annual_payment<br>pk_usage_code: 'LEA' | - | - | - |
| - | Default | 06 | Update | - | UPDATE prctrentper<br>SET:<br>source = 'M'<br>WHERE:<br>qcid IN {prctrentper(inserted during this run).qcid} | - | - | - |
| 3 | Lease Tenant History | 0 | Run Condition | - | Always runnable | - | - | - |
| 3 | Lease Tenant History | 01 | Cursor | - | SELECT leas_tnnt_ref, leas_prop_ref, leas_ref, leas_start_date, leas_term_date, leas_aftr_exp_flag, leas_expiry_date, leas_tnnh_bill_addr_ref, qcid<br>FROM lease<br>WHERE qcid IN {lease_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 3 | Lease Tenant History | 01.01 | Condition | - | IF (:leas_tnnt_ref is not Null) | - | - | - |
| 3 | Lease Tenant History | 01.01.01 | Insert | - | INSERT INTO tnnthist:<br>tnnh_comp_ref = property(:leas_prop_ref).prop_comp_ref<br>tnnh_prop_ref = :leas_prop_ref<br>tnnh_leas_ref = :leas_ref<br>tnnh_tnnt_ref = :leas_tnnt_ref<br>tnnh_start_date = :leas_start_date<br>tnnh_end_date = Nvl(:leas_term_date, (if (:leas_aftr_exp_flag = 'Y') then (Null) else (:leas_expiry_date)))<br>tnnh_bckgrnd_insert = 'Y'<br>tnnh_ac_ref = Null<br>tnnh_bill_addr_ref = :leas_tnnh_bill_addr_ref<br>tnnh_ass_flag = 'N'<br>WHERE tnnthist record does not exist satisfying:<br>tnnh_leas_ref = :leas_ref | - | - | - |
| 8 | Lease Receivable Renewal History | 0 | Run Condition | - | Always runnable | - | - | - |
| 8 | Lease Receivable Renewal History | 01 | Cursor | - | SELECT leas_ref, leas_start_date, leas_expiry_date, leas_comment, leas_comp_ref, leas_prop_ref, qcid<br>FROM lease<br>WHERE qcid IN {lease_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 8 | Lease Receivable Renewal History | 01.01 | Insert | - | INSERT INTO lernhist:<br>lerh_usage_code = 'LEA'<br>lerh_leas_hlse_ref = :leas_ref<br>lerh_leas_ref = :leas_ref<br>lerh_start_date = :leas_start_date<br>lerh_end_date = :leas_expiry_date<br>lerh_comment = :leas_comment<br>lerh_comp_ref = :leas_comp_ref<br>lerh_prop_ref = :leas_prop_ref<br>lerh_agreed_flag = 'Y'<br>WHERE lernhist record does not exist satisfying:<br>lerh_usage_code = 'LEA'<br>lerh_leas_hlse_ref = :leas_ref | - | - | - |
| 47 | Shared Tenancy Records for Main Tenants | 0 | Run Condition | - | Always runnable | - | - | - |
| 47 | Shared Tenancy Records for Main Tenants | 01 | Cursor | - | SELECT leas_tnnt_ref, leas_shared_tenancy_flag, leas_comp_ref, leas_ref, leas_start_date, qcid<br>FROM lease<br>WHERE qcid IN {lease_h1_01(inserted during parent run).qcid}<br>ORDER BY qcid | - | - | - |
| 47 | Shared Tenancy Records for Main Tenants | 01.01 | Condition | - | IF ((:leas_tnnt_ref is not Null) and (:leas_shared_tenancy_flag = 'Y')) | - | - | - |
| 47 | Shared Tenancy Records for Main Tenants | 01.01.01 | Insert | - | INSERT INTO tnntshare:<br>tnsh_comp_ref = :leas_comp_ref<br>tnsh_leas_ref = :leas_ref<br>tnsh_tnnt_ref = :leas_tnnt_ref<br>tnsh_start_date = :leas_start_date<br>WHERE tnntshare record does not exist satisfying:<br>tnsh_leas_ref = :leas_ref | - | - | - |

## Reference Code Types

Fields whose descriptions identify a code type must contain a value from that code type. The workbook's `Codes` and `LOVs` worksheets provide the corresponding lookup values.

| Code Type | Name | Desc |
| --- | --- | --- |
| AS | Accounting Standard | Accounting Standard in use<br>PROCESS FLAG 1:<br>UK Generally Accepted Accounting Practice (UK GAAP) standard<br>PROCESS FLAG 2:<br>The Financial Reporting Standard applicable in the UK and Republic of Ireland (FRS 102)<br>If no Process Flag is set, International Accounting Standards (IAS) will be used. |
| CUR | Currency Codes | Currency Codes |
| EXT | Extraction Type | Extraction Type used by the Rent Demand process to determine order invoices printed. NOTE: Code must be a numeric value and of XXX |
| LAN | User Languages | A list of available languages in the system. |
| LDN | Lease Demand Notice | Legal notice to appear on Lease Demands |
| LRR | Lease Receive Payment Reason | Lease Receive Payment Reason |
| LS | LEASE STATUS | Lease Status<br>PROCESS FLAG 0 :<br>Not Live Lease<br>Excluded when status filtering ON.<br>Used when the  'Tenant Move Out' process is completed if the Lease has not been reassigned.<br>PROCESS FLAG 1:<br>Live Lease<br>Used when the 'Tenant Move In' process is completed.<br>PROCESS FLAG 5:<br>Lease Template<br>Excluded when status filtering ON.<br>PROCESS FLAG 9:<br>Provisional Lease<br>Excluded when status filtering ON.<br>Used during the 'Tenant Move In' process.<br>PROCESS FLAG 2:<br>Not Actioned<br>Used when a provisional tenancy is cancelled from SLM. |
| LT | LEASE TYPE | Lease types are denoted by the legally binding Lease Agreements.  If Pisces is to be used the process flags are used as follows :<br>1 - Fully Repairing and Insuring,<br>2 - Internal Repairing and Insuring,<br>3 - Fully Repairing, 4 - Internal Repairing.<br>Other process flags are:<br>5 - Mortgage<br>6 - Anchor Lease (for Retail Centres). |
| MRC | Drawdown Reporting Category | This code is used to record the various Drawdown Reporting Categories. |
| MTY | Drawdown Type Code | This code is used to record the various Drawdown Types.<br>PROCESS FLAG 1: Variable (Cap)<br>PROCESS FLAG 2: Variable (Floor)<br>PROCESS FLAG 3: Variable (Collar)<br>PROCESS FLAG 4: Fixed<br>PROCESS FLAG 5: Variable |
| RLT | Reminder Letter Types | Describes the rent and turnover certificate reminder letters which can be sent out to tenants.<br>PROCESS FLAG 1 : Rent reminder letters<br>PROCESS FLAG 2 : Turnover certificate reminder letters |
| TER | Territory | Used to restrict access to various codes and config by country or territory/jurisdiction/country. |

---

## Source Notes

* `-` means the workbook cell is blank and does not add a rule or default.
* Validation and derivation expressions are preserved verbatim so implementation-specific PLE functions and field names are not reinterpreted.
* Code descriptions in field rules identify the required lookup family; use the workbook's `Codes` / `LOVs` worksheets or the target PLE database to validate the current allowed values.
* References to related PLE entities require the corresponding table data or target database. If that data is unavailable, report `Warning / REQUIRES DATABASE VERIFICATION` rather than claiming the reference is valid or invalid.
