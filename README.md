# Rapido Data Scientist Take-Home Assessment
## Captain Acquisition, Onboarding Funnel, Campaign Evaluation & Airport Supply

---

### Executive Overview

This repository contains the end-to-end data science assessment for Rapido's **Captain Acquisition & Supply Marketplace Analysis**. The analysis investigates captain onboarding efficiency, stage-by-stage volume loss, low-device quality leaks, marketing campaign causality (`CAMP_WA_002`), and airport marketplace demand-supply dynamics.

---

### Key Audited Findings Summary

1. **Cohort Maturity & Right-Censoring**:
   * Data extraction timestamp: `2026-06-30 23:59 IST`. Average onboarding duration is **6.42 days** (up to 14 days).
   * **1,297 captains** are marked `in_progress`, 100% of whom belong to the June 2026 cohort.
   * **Mature Baseline Cohort (Jan–May 2026, N = 20,207)**: Baseline A2O conversion rate is **17.48%** (3,532 approved / 20,207 signups). Raw overall conversion (16.82%) undercounts true conversion due to right-censoring.

2. **Onboarding Funnel & Leaks**:
   * **Largest Absolute Volume Loss**: **Registration Certificate (RC)** stage — **4,887 captains lost** (29.3% of total funnel loss).
   * **Largest Proportional Drop**: **Fitness Certificate / Insurance** stage — stage conversion is **62.80%** (2,303 lost out of 6,191 entering).
   * **Biggest Fixable Leak**: **Low-tier device photo capture & OCR failures** (5,568 photo/OCR failures, representing **62.86% of all 8,858 low-device verification failures** in the mature cohort).
   * **Planning Uplift Scenario**: Recovering 50% of the low-device conversion gap to mid-tier (19.50%) yields a base-case planning estimate of **+52 approved captains/month** (+258 over 5 mature months).

3. **Campaign Evaluation (`CAMP_WA_002`)**:
   * **Observed Association**: WhatsApp recipients converted at **28.98%** vs **11.21%** non-recipients (+17.78% pts raw difference).
   * **Diagnosis**: The lift is heavily confounded by **Selection Bias**. `CAMP_WA_002` was sent exclusively to downstream captains who had already cleared early stages (DL & RC).
   * **Within-Recipient Diagnostic**: Within recipients, clickers converted at **28.34%** vs non-clickers at **29.44%** (-1.09% pts difference), providing no positive incremental evidence from clicking.
   * **Decision**: **REJECT immediate 5x budget scaling**. Run a 14-day RCT with a proposed 15% holdout group first.

4. **Airport Demand & Supply Mismatch**:
   * Mismatch is **TIME-SPECIFIC (Night Peak: 21:00–03:00 IST)**, where fulfillment drops to **31.91%** (46,020 unfulfilled rides over May-June, representing 83.6% of all unfulfilled airport demand).
   * **Post-Airport Behavior**: 41.1% of airport trips drop in suburban zones. **83.5% of suburban drops do NOT get a return fare within 20 minutes**, driving a **21.0% captain cancellation rate**. The observed pattern is consistent with deadheading friction reducing the attractiveness of returning to the airport.
   * **Decision**: **NO to targeted airport acquisition push**. Target raising night fulfillment from 31.9% toward 60% (~+9,500 incremental rides/month goal) via dynamic return-fare guarantees and toll repositioning allowances.

---

### Repository Structure

```text
Rapido_Assessment/
│
├── Data/
│   ├── activation.csv
│   ├── airport_hourly.csv
│   ├── airport_trips.csv
│   ├── approvals.csv
│   ├── captains.csv
│   ├── doc_events.csv
│   └── nudges.csv
│
├── rapido_analysis.ipynb          # End-to-end reproducible Jupyter Notebook
├── Rapido_2_Page_Memo.docx        # Executive Memo for Head of Supply (Max 2 pages)
├── Rapido_Presentation_Deck.pptx  # Executive Presentation Deck (Max 6 slides)
├── Rapido_Presentation_Deck.docx  # Document format of presentation deck
├── README.md                      # Documentation & instructions
└── requirements.txt               # Python package dependencies
```

---

### Installation & Execution

1. **Clone Repository & Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Run Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```
   Open `rapido_analysis.ipynb` and click **Run All Cells**. All analysis, calculations, tables, and figures will execute end-to-end from the raw CSV data in `Data/`.

---

### Important Note
The data used in this assessment is synthetic assessment data provided for evaluation purposes. Financial numbers (e.g. ₹1.5L SDK, ₹0.50 WhatsApp OTP, ₹150 return guarantee) represent illustrative planning/pilot budget assumptions.
