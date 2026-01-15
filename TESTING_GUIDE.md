# TSG Salary Calculator - Comprehensive Testing Guide

**Version:** 1.2.3  
**Last Updated:** January 15, 2026  
**Purpose:** Complete manual testing checklist for all features and scenarios

---

## 📋 Table of Contents

1. [Pre-Testing Setup](#pre-testing-setup)
2. [Employee Mode Tests](#employee-mode-tests)
3. [B2B Mode Tests](#b2b-mode-tests)
4. [Allocation Mode Tests](#allocation-mode-tests)
5. [Currency Conversion Tests](#currency-conversion-tests)
6. [UI/UX Tests](#uiux-tests)
7. [Export & Print Tests](#export--print-tests)
8. [Edge Cases & Validation](#edge-cases--validation)
9. [Browser Compatibility Tests](#browser-compatibility-tests)
10. [Performance Tests](#performance-tests)

---

## Pre-Testing Setup

### ✅ Initial Checklist
- [ ] Open `index.html` in a web browser
- [ ] Verify the page loads without errors (check browser console - F12)
- [ ] Verify TSG logo appears at the top
- [ ] Verify all three engagement type buttons are visible
- [ ] Clear browser cache and localStorage (for fresh start)
- [ ] Check internet connection (required for FX rates and CDN libraries)

### Tools Needed
- Modern web browser (Chrome, Firefox, Safari, or Edge)
- Browser developer tools (F12)
- Calculator or spreadsheet for verification
- Printer or PDF viewer (for print tests)

---

## Employee Mode Tests

### Test 1: Switzerland - From Gross Salary (Monthly)

**Objective:** Verify Swiss payroll calculations with default settings

**Steps:**
1. Click **"Employee"** engagement type
2. Select **"Switzerland"** from country dropdown
3. Select **"From Gross Salary"** mode
4. Enter **8,000 CHF**
5. Select **"Monthly"** period
6. Keep occupation rate at **100%**
7. Click **"Calculate"**

**Expected Results:**
- ✅ Net salary displays (approximately 6,300-6,500 CHF)
- ✅ Total company cost displays (approximately 9,500-10,000 CHF)
- ✅ All contribution breakdowns appear:
  - AVS/AI/APG (employee + employer)
  - AC (unemployment)
  - LPP (pension)
  - LAA (accident insurance)
  - AF, CPE, LFP (employer only)
- ✅ No income tax line (Switzerland doesn't include cantonal tax)
- ✅ Daily cost rate shows (Total Cost ÷ 220 days)
- ✅ Results are in CHF
- ✅ EUR conversion option appears

**Validation:**
- [ ] Net salary is less than gross
- [ ] Total cost is greater than gross
- [ ] All percentages look correct (AVS ~4.35%, etc.)
- [ ] Numbers are rounded to 2 decimals

---

### Test 2: Switzerland - From Net Salary (Yearly)

**Objective:** Test reverse calculation (Net → Gross)

**Steps:**
1. Stay in Switzerland Employee mode
2. Click **"Clear All"** button
3. Select **"From Net Salary"** mode
4. Enter **75,000 CHF**
5. Select **"Yearly"** period
6. Click **"Calculate"**

**Expected Results:**
- ✅ Gross salary displays (approximately 95,000-100,000 CHF)
- ✅ Total company cost displays
- ✅ All contributions calculated correctly
- ✅ Calculation completes in < 2 seconds

**Validation:**
- [ ] When you switch to "From Gross" with the calculated gross, you get back ~75,000 net
- [ ] No error messages in console
- [ ] Yearly amounts are 12x monthly equivalents

---

### Test 3: Switzerland - Advanced Options

**Objective:** Test Swiss-specific advanced options

**Steps:**
1. Stay in Switzerland Employee mode
2. Click **"Advanced Options"**
3. Modify settings:
   - Monthly Other Benefits: **500 CHF**
   - LPP Rate: **12%** (instead of 7%)
   - LFP Rate: **0.08%** (instead of 0.03%)
   - LAA Non-Professional: **2%** (instead of 1.5%)
   - BVG Pension Plan: Select **"Super-obligatory"**
4. Enter From Gross: **12,000 CHF** monthly
5. Click **"Calculate"**

**Expected Results:**
- ✅ Total cost includes 500 CHF benefit
- ✅ LPP contribution uses 12% rate
- ✅ LFP uses 0.08%
- ✅ LAA non-prof uses 2%
- ✅ For high salaries, super-obligatory doesn't cap LPP base
- ✅ Advanced options remain visible after calculation

**Validation:**
- [ ] LPP amount = (Gross - LPP coordination) × 12% (employee part)
- [ ] Benefits appear in total cost
- [ ] Advanced options persist until cleared

---

### Test 4: Switzerland - Swiss Salary Benchmark

**Objective:** Test Swiss salary benchmarking feature

**Steps:**
1. Stay in Switzerland Employee mode
2. Enter From Gross: **120,000 CHF** yearly
3. In the **"Swiss Salary Benchmark"** field, enter: **"Software Engineer"**
4. Click **"Calculate"**

**Expected Results:**
- ✅ Benchmark section appears below results
- ✅ Shows salary range (Min - Median - Max)
- ✅ Visual bar with position indicator
- ✅ Percentile or position text (e.g., "Above Median")
- ✅ Salary comparison message

**Validation:**
- [ ] Try variations: "software engineer", "Software Developer", "SE"
- [ ] Try abbreviations: "ML Engineer" (should match Machine Learning Engineer)
- [ ] Try invalid titles - should show "No benchmark data" message
- [ ] Benchmark ONLY appears in Switzerland Employee mode

---

### Test 5: Romania - From Gross Salary

**Objective:** Test Romanian payroll with IT tax exemption

**Steps:**
1. Click **"Clear All"**
2. Select **"Romania"** country
3. Select **"From Gross Salary"**
4. Enter **10,000 RON** monthly
5. Click **"Advanced Options"**
6. Check **"Tax Exemption"** checkbox
7. Click **"Calculate"**

**Expected Results:**
- ✅ CAS: 25% employee deducted
- ✅ CASS: 10% employee deducted
- ✅ CAM: 2.25% employer added
- ✅ Income tax: **0 RON** (due to exemption)
- ✅ Net salary = Gross - CAS - CASS
- ✅ Total cost = Gross + CAM

**Validation:**
- [ ] With exemption: No income tax
- [ ] Without exemption: 10% income tax should appear
- [ ] CAS + CASS = 35% of gross

---

### Test 6: Romania - Monthly Meal Benefits

**Objective:** Test non-taxable benefits

**Steps:**
1. Stay in Romania Employee mode
2. Click **"Advanced Options"**
3. Uncheck **"Tax Exemption"**
4. Enter **"Monthly Meal Benefits"**: **500 RON**
5. Check **"Base Function"**
6. Enter **"Number of Dependents"**: **2**
7. Enter From Gross: **8,000 RON** monthly
8. Click **"Calculate"**

**Expected Results:**
- ✅ Meal benefits (500 RON) added to:
  - Total company cost
  - Net take-home pay
- ✅ Meal benefits NOT added to gross (not taxable)
- ✅ Personal deduction: 510 RON applied (base function checked)
- ✅ Dependent deduction: 220 RON (2 × 110) applied
- ✅ Taxable base = Gross - CAS - CASS - Personal - Dependent
- ✅ Income tax = Taxable base × 10%

**Validation:**
- [ ] Net = Gross - CAS - CASS - Income Tax + Meal Benefits
- [ ] Deductions reduce income tax
- [ ] Uncheck "Base Function" → Personal deduction disappears

---

### Test 7: Spain - From Total Company Cost

**Objective:** Test reverse calculation (Total → Gross) for Spain

**Steps:**
1. Click **"Clear All"**
2. Select **"Spain"** country
3. Select **"From Total Company Cost"**
4. Enter **4,000 EUR** monthly
5. Click **"Calculate"**

**Expected Results:**
- ✅ Gross salary calculated (approximately 2,900-3,100 EUR)
- ✅ Net salary calculated (approximately 2,400-2,600 EUR)
- ✅ Employee contributions shown (~6.35% SS)
- ✅ Employer contributions shown (~29.90% SS)
- ✅ IRPF (income tax) estimated with progressive bands
- ✅ Contribution base limits applied (min 1,323, max 4,720.50)

**Validation:**
- [ ] Total cost = Gross + Employer SS
- [ ] Net = Gross - Employee SS - IRPF
- [ ] Calculation completes in < 2 seconds

---

### Test 8: Spain - High Salary (Contribution Base Cap)

**Objective:** Test contribution base maximum limit

**Steps:**
1. Stay in Spain Employee mode
2. Select **"From Gross Salary"**
3. Enter **6,000 EUR** monthly (above max base)
4. Click **"Calculate"**

**Expected Results:**
- ✅ Social security contributions capped at base max (4,720.50 EUR)
- ✅ Employee SS = 4,720.50 × 6.35%
- ✅ Employer SS = 4,720.50 × 29.90%
- ✅ IRPF calculated on full gross (no cap)
- ✅ Warning or note about contribution base cap

**Validation:**
- [ ] SS contributions don't increase beyond max base
- [ ] IRPF still calculated on full 6,000 EUR

---

### Test 9: Occupation Rate (Part-Time)

**Objective:** Test part-time employment calculations

**Steps:**
1. Select any country (e.g., Romania)
2. Select **"From Gross Salary"**
3. Enter **10,000 RON** monthly
4. Set **Occupation Rate: 80%**
5. Click **"Calculate"**

**Expected Results:**
- ✅ Adjusted gross = 10,000 × 0.80 = 8,000 RON
- ✅ All calculations based on 8,000 RON
- ✅ Daily cost rate uses **220 working days** (NOT 176)
- ✅ Daily rate = (Total Cost × 12) ÷ 220

**Validation:**
- [ ] Occupation rate scales salary only
- [ ] Working days always 220
- [ ] Try 60%, 80%, 100% - verify scaling

---

### Test 10: Business Outputs (Daily Rates)

**Objective:** Test business metrics calculations

**Steps:**
1. Continue from previous test (or any Employee calculation)
2. Scroll to **"Business Outputs"** section
3. Enter **"Daily Revenue Rate"**: **400 EUR**
4. View calculated metrics

**Expected Results:**
- ✅ Daily cost rate displayed (Total Cost ÷ 220 ÷ 12)
- ✅ Daily gross margin = Revenue - Cost
- ✅ Gross margin % = (Margin ÷ Revenue) × 100
- ✅ All in EUR (if different currency, uses conversion)

**Validation:**
- [ ] Margin % is correct percentage
- [ ] If revenue < cost, margin is negative
- [ ] If revenue = cost, margin is 0%

---

## B2B Mode Tests

### Test 11: B2B - Target Margin %

**Objective:** Test B2B pricing with target profit margin

**Steps:**
1. Click **"B2B"** engagement type
2. Select **"Daily"** cost period
3. Select **"EUR"** contractor currency
4. Enter **Contractor Cost**: **500 EUR**
5. Select **"Target Margin %"** pricing mode
6. Enter **Target Margin**: **30%**
7. Click **"Calculate"**

**Expected Results:**
- ✅ Daily placement rate = 500 ÷ (1 - 0.30) = **714.29 EUR**
- ✅ Daily profit = 714.29 - 500 = **214.29 EUR**
- ✅ Displayed margin = (214.29 ÷ 714.29) × 100 = **30.00%**
- ✅ Monthly profit = 214.29 × 22 = **4,714.38 EUR**
- ✅ Monthly placement rate = 714.29 × 22 = **15,714.38 EUR**

**Validation:**
- [ ] Margin % displayed is EXACTLY 30% (not 23% or other)
- [ ] Formula uses true margin (not markup)
- [ ] Try different margins: 20%, 35%, 50%

---

### Test 12: B2B - Client Daily Rate

**Objective:** Calculate margin from known client rate

**Steps:**
1. Stay in B2B mode
2. Click **"Clear All"**
3. Enter **Contractor Cost**: **400 CHF** daily
4. Select **Contractor Currency**: **CHF**
5. Select **"Client Daily Rate"** pricing mode
6. Enter **Client Daily Rate**: **600 CHF**
7. Click **"Calculate"**

**Expected Results:**
- ✅ Daily profit = 600 - 400 = **200 CHF**
- ✅ Margin % = (200 ÷ 600) × 100 = **33.33%**
- ✅ Monthly profit = 200 × 22 = **4,400 CHF**
- ✅ Markup % = (200 ÷ 400) × 100 = **50%**

**Validation:**
- [ ] Margin % ≠ Markup % (different formulas)
- [ ] Margin % = Profit ÷ Revenue
- [ ] Markup % = Profit ÷ Cost

---

### Test 13: B2B - Client Budget

**Objective:** Work backwards from total budget

**Steps:**
1. Stay in B2B mode
2. Click **"Clear All"**
3. Enter **Contractor Cost**: **350 EUR** daily
4. Select **"Client Budget"** pricing mode
5. Enter **Total Budget**: **20,000 EUR**
6. Enter **Number of Days**: **50**
7. Click **"Calculate"**

**Expected Results:**
- ✅ Daily placement rate = 20,000 ÷ 50 = **400 EUR**
- ✅ Daily profit = 400 - 350 = **50 EUR**
- ✅ Total profit = 50 × 50 = **2,500 EUR**
- ✅ Margin % = (50 ÷ 400) × 100 = **12.5%**

**Validation:**
- [ ] Daily rate × Days = Total budget
- [ ] Profit calculation is correct
- [ ] Try different budget/days combinations

---

### Test 14: B2B - Multi-Currency

**Objective:** Test currency conversion in B2B mode

**Steps:**
1. Stay in B2B mode
2. Click **"Clear All"**
3. Enter **Contractor Cost**: **500 CHF** daily
4. Select **Contractor Currency**: **CHF**
5. Select **"Display Currency"**: **EUR**
6. Select **"Target Margin %"** pricing mode
7. Enter **Target Margin**: **25%**
8. Click **"Calculate"**

**Expected Results:**
- ✅ All amounts display in EUR (converted from CHF)
- ✅ Exchange rate shown
- ✅ Business Outputs section appears with both currencies
- ✅ Conversions use current FX rate
- ✅ Margin % remains 25% regardless of currency

**Validation:**
- [ ] Try different currency combinations (CHF→EUR, RON→CHF, etc.)
- [ ] Verify exchange rate is reasonable
- [ ] If currencies match, Business Outputs section hides

---

### Test 15: B2B - Hourly Rate

**Objective:** Test hourly-based calculations

**Steps:**
1. Stay in B2B mode
2. Click **"Clear All"**
3. Select **"Hourly"** cost period
4. Enter **Contractor Cost**: **50 EUR** hourly
5. Enter **Hours per Day**: **8**
6. Select **"Target Margin %"**: **30%**
7. Click **"Calculate"**

**Expected Results:**
- ✅ Daily cost = 50 × 8 = **400 EUR**
- ✅ Calculations based on 400 EUR daily
- ✅ Daily placement rate = 400 ÷ 0.70 = **571.43 EUR**
- ✅ Hourly placement rate = 571.43 ÷ 8 = **71.43 EUR**

**Validation:**
- [ ] Hourly × Hours/Day = Daily cost
- [ ] All other calculations match daily mode
- [ ] Try different hours/day: 4, 6, 8

---

### Test 16: B2B - Benchmark Isolation

**Objective:** Verify Swiss benchmark does NOT appear in B2B mode

**Steps:**
1. Stay in B2B mode (Switzerland not selected, no country in B2B)
2. Complete any B2B calculation
3. Scroll through all results

**Expected Results:**
- ✅ NO Swiss Salary Benchmark section appears
- ✅ Only B2B-specific outputs shown
- ✅ No country-specific fields visible

**Validation:**
- [ ] Benchmark field is completely hidden
- [ ] No Swiss-specific UI elements

---

## Allocation Mode Tests

### Test 17: Allocation - Basic Setup

**Objective:** Test basic allocation mode functionality

**Steps:**
1. Click **"Allocation"** engagement type
2. Enter **Salary at 100%**: **160,000 CHF** (yearly)
3. Enter **Engagement %**: **80%**
4. Enter **Employer Multiplier**: **1.20**
5. Keep **Working Days/Year**: **220**
6. Click **"Add Client"** (2 times to add 2 clients)
7. Fill Client 1:
   - Name: **Client A**
   - Allocation %: **60%**
   - Daily Rate: **1,250 CHF**
8. Fill Client 2:
   - Name: **Client B**
   - Allocation %: **20%**
   - Daily Rate: **1,250 CHF**
9. Click **"Calculate"**

**Expected Results:**
- ✅ Engaged Salary = 160,000 × 0.80 = **128,000 CHF**
- ✅ Employer Cost = 128,000 × 1.20 = **153,600 CHF**
- ✅ Base Daily Cost = 153,600 ÷ 220 = **698.18 CHF**
- ✅ Client A Revenue = 1,250 × 0.60 = **750 CHF/day**
- ✅ Client A Profit = 750 - 698.18 = **51.82 CHF** (baseline)
- ✅ Client B Revenue = 1,250 × 0.20 = **250 CHF/day**
- ✅ Client B Profit = **250 CHF** (incremental, cost covered)
- ✅ Total Daily Profit = 51.82 + 250 = **301.82 CHF**
- ✅ Annual Profit = 301.82 × 220 = **66,400.40 CHF**
- ✅ Client A marked as **"Baseline"**

**Validation:**
- [ ] Base daily cost paid only once
- [ ] Highest revenue client is baseline
- [ ] Other clients show full revenue as profit
- [ ] Total allocation = 60% + 20% = 80% = Engagement %

---

### Test 18: Allocation - Validation

**Objective:** Test allocation percentage validation

**Steps:**
1. Stay in Allocation mode
2. Change **Engagement %** to **50%**
3. Keep clients at 60% + 20% = 80%
4. Click **"Calculate"**

**Expected Results:**
- ✅ Error message: **"Total allocation % (80%) exceeds engagement % (50%)"**
- ✅ Calculation blocked
- ✅ Error message highlighted in red

**Validation:**
- [ ] Cannot calculate when allocation > engagement
- [ ] Error message is clear
- [ ] Fix by reducing allocations or increasing engagement

---

### Test 19: Allocation - Three Clients

**Objective:** Test multiple client allocations

**Steps:**
1. Stay in Allocation mode
2. Set **Engagement %**: **100%**
3. Click **"Add Client"** to add a third client
4. Fill clients:
   - Client 1: **40%**, **1,000 CHF/day**
   - Client 2: **30%**, **1,200 CHF/day**
   - Client 3: **30%**, **800 CHF/day**
5. Click **"Calculate"**

**Expected Results:**
- ✅ Client 1 Revenue = 1,000 × 0.40 = **400 CHF/day**
- ✅ Client 2 Revenue = 1,200 × 0.30 = **360 CHF/day**
- ✅ Client 3 Revenue = 800 × 0.30 = **240 CHF/day**
- ✅ Client 1 is baseline (highest revenue: 400)
- ✅ Client 1 Profit = 400 - 698.18 = **-298.18 CHF** (negative!)
- ✅ Client 2 Profit = **360 CHF** (incremental)
- ✅ Client 3 Profit = **240 CHF** (incremental)
- ✅ Total Profit = -298.18 + 360 + 240 = **301.82 CHF**

**Validation:**
- [ ] Baseline can have negative profit (cost not covered)
- [ ] Other clients always show full revenue as profit
- [ ] Total can be positive even if baseline is negative
- [ ] Can add up to 10+ clients

---

### Test 20: Allocation - Remove Client

**Objective:** Test removing clients from allocation

**Steps:**
1. Stay in Allocation mode
2. Click **"Remove"** button on Client 2
3. Verify only 2 clients remain
4. Click **"Calculate"**

**Expected Results:**
- ✅ Client 2 removed from table
- ✅ Calculations only include remaining clients
- ✅ Total allocation updates
- ✅ Baseline recalculated

**Validation:**
- [ ] Remove works correctly
- [ ] Cannot remove if only 1 client remains
- [ ] Can add back after removing

---

### Test 21: Allocation - Currency Display

**Objective:** Test allocation mode accepts only one currency

**Steps:**
1. Stay in Allocation mode
2. Observe currency selection
3. Complete calculation
4. Check if EUR conversion available

**Expected Results:**
- ✅ All rates and costs in one currency (CHF in this test)
- ✅ No multi-currency mixing within allocation
- ✅ Results display in selected currency only

**Validation:**
- [ ] Single currency enforced
- [ ] Clear currency labeling

---

## Currency Conversion Tests

### Test 22: Display in EUR Toggle

**Objective:** Test EUR conversion feature

**Steps:**
1. Go to **Employee** mode
2. Select **Romania**
3. Enter From Gross: **10,000 RON** monthly
4. Click **"Calculate"**
5. Toggle **"Display in EUR"** ON
6. Wait for conversion

**Expected Results:**
- ✅ Exchange rate appears (e.g., 1 EUR = 4.97 RON)
- ✅ Last update date/time shown
- ✅ All amounts converted to EUR
- ✅ Original currency still visible
- ✅ Dual display format (e.g., "2,000 EUR (10,000 RON)")

**Validation:**
- [ ] Conversion uses current FX rate
- [ ] Math is correct: RON amount ÷ rate = EUR amount
- [ ] Toggle OFF returns to original currency
- [ ] Exchange rate cached (check localStorage)

---

### Test 23: Exchange Rate Refresh

**Objective:** Test manual FX rate refresh

**Steps:**
1. Stay in EUR conversion mode
2. Note current exchange rate
3. Click **"Refresh Rates"** button (if available)
4. Wait for API call

**Expected Results:**
- ✅ Loading indicator appears
- ✅ New rates fetched from API
- ✅ Amounts recalculated with new rates
- ✅ Update timestamp refreshed
- ✅ 24-hour cache reset

**Validation:**
- [ ] Refresh works without errors
- [ ] Console shows successful API call
- [ ] New rate may be slightly different

---

### Test 24: Offline Exchange Rates

**Objective:** Test cached exchange rates

**Steps:**
1. Complete a calculation with EUR conversion
2. Disconnect internet (or block API in DevTools)
3. Refresh the page
4. Toggle EUR conversion ON

**Expected Results:**
- ✅ Uses cached rates (up to 24 hours old)
- ✅ Shows "Last updated: [timestamp]"
- ✅ Warning if rates are stale (optional)
- ✅ Calculations still work

**Validation:**
- [ ] Cache persists across page reloads
- [ ] Rates valid for 24 hours
- [ ] After 24h, requires internet connection

---

## UI/UX Tests

### Test 25: Mode Switching

**Objective:** Test switching between engagement types

**Steps:**
1. Complete an Employee calculation (with results visible)
2. Click **"B2B"** button
3. Observe UI changes
4. Click **"Allocation"** button
5. Return to **"Employee"**

**Expected Results:**
- ✅ Previous results clear when switching modes
- ✅ Input fields change per mode
- ✅ Mode-specific sections appear/disappear
- ✅ No JavaScript errors in console
- ✅ Active button highlighted
- ✅ Smooth transitions

**Validation:**
- [ ] No data leakage between modes
- [ ] Each mode fully isolated
- [ ] UI responds immediately
- [ ] No residual data from previous mode

---

### Test 26: Clear All Functionality

**Objective:** Test the Clear All button

**Steps:**
1. Complete any calculation with results
2. Enter Advanced Options
3. Toggle EUR conversion ON
4. Click **"Clear All"** button

**Expected Results:**
- ✅ All input fields reset to default
- ✅ All results hidden
- ✅ Advanced options collapsed
- ✅ EUR conversion OFF
- ✅ Country/mode selection remains
- ✅ Exchange rates remain cached

**Validation:**
- [ ] Complete reset except mode/country
- [ ] No errors in console
- [ ] Ready for new calculation

---

### Test 27: Help Icons (?)

**Objective:** Test formula transparency tooltips

**Steps:**
1. Complete any Employee calculation
2. Look for **"?"** help icons throughout results
3. Click or hover over each **"?"** icon

**Expected Results:**
- ✅ Tooltip or modal appears
- ✅ Shows formula or explanation
- ✅ Clear, readable text
- ✅ Can dismiss tooltip/modal
- ✅ Icons present for all major calculations

**Validation:**
- [ ] All "?" icons functional
- [ ] Formulas are accurate
- [ ] No broken tooltips

---

### Test 28: Responsive Design

**Objective:** Test mobile and tablet layouts

**Steps:**
1. Open browser DevTools (F12)
2. Enable device toolbar (responsive mode)
3. Test at different screen sizes:
   - Mobile: 375px width
   - Tablet: 768px width
   - Desktop: 1920px width
4. Complete calculations at each size

**Expected Results:**
- ✅ Layout adapts to screen size
- ✅ No horizontal scrolling
- ✅ Buttons remain clickable
- ✅ Text remains readable
- ✅ Tables scroll or stack vertically
- ✅ Logo scales appropriately

**Validation:**
- [ ] Test portrait and landscape orientations
- [ ] Touch targets are large enough (mobile)
- [ ] No overlapping elements

---

### Test 29: Input Validation

**Objective:** Test invalid input handling

**Steps:**
1. Try entering invalid values:
   - Negative numbers: **-1000**
   - Letters: **abc**
   - Special characters: **@#$**
   - Zero: **0**
   - Very large numbers: **999999999999**
2. Click Calculate for each

**Expected Results:**
- ✅ Validation errors appear
- ✅ Clear error messages
- ✅ Calculation blocked for invalid input
- ✅ Input fields highlighted in red
- ✅ Helpful error text

**Validation:**
- [ ] Cannot calculate with invalid input
- [ ] Error messages are user-friendly
- [ ] Can correct and retry

---

### Test 30: Advanced Options Persistence

**Objective:** Test advanced options state management

**Steps:**
1. Go to Employee mode
2. Click **"Advanced Options"**
3. Set multiple options:
   - Monthly benefits: 200
   - Dependents: 1
   - Tax exemption: ON
4. Click **"Calculate"**
5. Change country
6. Return to original country

**Expected Results:**
- ✅ Options remain after calculation
- ✅ Options collapse but retain values
- ✅ Options reset when changing countries (country-specific)
- ✅ Can clear options with "Clear All"

**Validation:**
- [ ] Country-specific options appear/disappear correctly
- [ ] Values don't persist across countries
- [ ] Options visible/hidden as appropriate

---

## Export & Print Tests

### Test 31: Print Preview (Employee Mode)

**Objective:** Test print output for Employee mode

**Steps:**
1. Complete an Employee calculation (any country)
2. Click browser **Print** button (Ctrl+P or Cmd+P)
3. Review print preview

**Expected Results:**
- ✅ TSG logo appears at top
- ✅ Engagement type shows: **"Employee"**
- ✅ Input summary section included
- ✅ Complete results breakdown
- ✅ All contributions listed
- ✅ Clean, professional layout
- ✅ No UI buttons in print
- ✅ No unnecessary whitespace
- ✅ Proper page breaks

**Validation:**
- [ ] Only Employee results shown (no B2B/Allocation)
- [ ] All numbers align correctly
- [ ] Print fits on standard pages
- [ ] Colors print well (or grayscale-friendly)

---

### Test 32: Print Preview (B2B Mode)

**Objective:** Test print output for B2B mode

**Steps:**
1. Complete a B2B calculation
2. Click browser **Print** button
3. Review print preview

**Expected Results:**
- ✅ TSG logo at top
- ✅ Engagement type shows: **"B2B"**
- ✅ Contractor cost details
- ✅ Client pricing details
- ✅ Profit margin analysis
- ✅ No Employee payroll information
- ✅ Clean B2B-specific layout

**Validation:**
- [ ] Only B2B results shown
- [ ] No cross-contamination from other modes
- [ ] Professional appearance

---

### Test 33: Print Preview (Allocation Mode)

**Objective:** Test print output for Allocation mode

**Steps:**
1. Complete an Allocation calculation with 2-3 clients
2. Click browser **Print** button
3. Review print preview

**Expected Results:**
- ✅ TSG logo at top
- ✅ Engagement type shows: **"Allocation"**
- ✅ Base parameters listed
- ✅ Client table with all clients
- ✅ Profit breakdown per client
- ✅ Baseline client indicated
- ✅ Total profit summary
- ✅ No Employee/B2B information

**Validation:**
- [ ] All clients appear in table
- [ ] Table formatting is clean
- [ ] Numbers align properly
- [ ] Baseline marking visible

---

### Test 34: PDF Export (if available)

**Objective:** Test PDF export functionality

**Steps:**
1. Complete any calculation
2. Look for **"Export to PDF"** button
3. Click button
4. Wait for PDF generation
5. Open generated PDF

**Expected Results:**
- ✅ PDF downloads automatically
- ✅ Filename includes date/time
- ✅ All content rendered correctly
- ✅ TSG logo visible
- ✅ Full color (if applicable)
- ✅ Professional layout
- ✅ Readable fonts

**Validation:**
- [ ] PDF opens without errors
- [ ] Content matches screen display
- [ ] Images render correctly
- [ ] Text is selectable (not image)

---

## Edge Cases & Validation

### Test 35: Very Low Salary

**Objective:** Test minimum salary thresholds

**Steps:**
1. Employee mode, Switzerland
2. Enter From Gross: **1,000 CHF** monthly
3. Click Calculate

**Expected Results:**
- ✅ Calculation completes
- ✅ LPP may not apply (below minimum salary 22,680/year)
- ✅ Warning message if below minimum (optional)
- ✅ Other contributions still calculated

**Validation:**
- [ ] No crashes or errors
- [ ] Contributions capped at minimums where applicable
- [ ] Results are logical

---

### Test 36: Very High Salary

**Objective:** Test maximum thresholds and caps

**Steps:**
1. Employee mode, Switzerland
2. Enter From Gross: **50,000 CHF** monthly
3. Click Calculate

**Expected Results:**
- ✅ AC capped at ceiling (12,350 CHF/month)
- ✅ LPP uses BVG cap if "Mandatory BVG" selected
- ✅ All other contributions calculated normally
- ✅ Warning about ceilings (optional)

**Validation:**
- [ ] AC = 12,350 × 1.1% (not 50,000 × 1.1%)
- [ ] LPP respects pension plan mode setting
- [ ] Total cost is reasonable

---

### Test 37: Zero Allocation Percentage

**Objective:** Test zero allocation in Allocation mode

**Steps:**
1. Allocation mode
2. Add a client with **0%** allocation
3. Try to calculate

**Expected Results:**
- ✅ Validation error OR
- ✅ Client ignored in calculations
- ✅ Clear handling of zero allocation

**Validation:**
- [ ] No division by zero errors
- [ ] Reasonable error message

---

### Test 38: Negative Profit Scenario

**Objective:** Test when costs exceed revenue

**Steps:**
1. B2B mode
2. Contractor cost: **600 EUR** daily
3. Client daily rate: **500 EUR**
4. Calculate

**Expected Results:**
- ✅ Negative profit shown: **-100 EUR**
- ✅ Negative margin %: **-20%**
- ✅ Results clearly indicate loss
- ✅ Red color for negative values (optional)

**Validation:**
- [ ] Negative numbers display correctly
- [ ] User understands this is a loss
- [ ] No calculation errors

---

### Test 39: Exactly 100% Allocation

**Objective:** Test boundary condition

**Steps:**
1. Allocation mode
2. Engagement: **100%**
3. Add clients totaling exactly **100%**:
   - Client 1: 60%
   - Client 2: 40%
4. Calculate

**Expected Results:**
- ✅ Calculation succeeds
- ✅ Total allocation = 100% = Engagement
- ✅ No validation errors
- ✅ All profits calculated correctly

**Validation:**
- [ ] 100% is valid (not error)
- [ ] Results are accurate

---

### Test 40: Rapid Input Changes

**Objective:** Test debouncing and rapid input

**Steps:**
1. Employee mode
2. Rapidly change input values multiple times
3. Quickly switch between modes
4. Calculate immediately

**Expected Results:**
- ✅ No errors or crashes
- ✅ Latest values used in calculation
- ✅ UI remains responsive
- ✅ No race conditions

**Validation:**
- [ ] Console shows no errors
- [ ] Calculations use correct final values
- [ ] Performance remains smooth

---

## Browser Compatibility Tests

### Test 41: Chrome

**Objective:** Full functionality test in Chrome

**Steps:**
1. Open in latest Chrome browser
2. Complete tests 1-10 (Employee mode)
3. Complete tests 11-16 (B2B mode)
4. Complete tests 17-21 (Allocation mode)
5. Test print and export

**Expected Results:**
- ✅ All features work perfectly
- ✅ No console errors
- ✅ Smooth performance
- ✅ Correct rendering

---

### Test 42: Firefox

**Objective:** Full functionality test in Firefox

**Steps:**
1. Open in latest Firefox browser
2. Complete key tests from each mode
3. Test print and export
4. Check for Firefox-specific issues

**Expected Results:**
- ✅ All features work correctly
- ✅ Layout consistent with Chrome
- ✅ No Firefox-specific bugs
- ✅ Print preview works

---

### Test 43: Safari

**Objective:** Full functionality test in Safari

**Steps:**
1. Open in latest Safari browser (macOS/iOS)
2. Complete key tests from each mode
3. Test on iPhone/iPad if available
4. Test print and export

**Expected Results:**
- ✅ All features work correctly
- ✅ Touch interactions work (mobile)
- ✅ No Safari-specific bugs
- ✅ Print preview works

---

### Test 44: Edge

**Objective:** Full functionality test in Edge

**Steps:**
1. Open in latest Edge browser
2. Complete key tests from each mode
3. Test print and export

**Expected Results:**
- ✅ All features work correctly
- ✅ Consistent with Chrome (Chromium base)
- ✅ No Edge-specific bugs

---

## Performance Tests

### Test 45: Initial Load Time

**Objective:** Measure page load performance

**Steps:**
1. Clear browser cache completely
2. Open browser DevTools → Network tab
3. Load `index.html`
4. Measure load time

**Expected Results:**
- ✅ Page loads in < 3 seconds on 3G
- ✅ All CDN resources load successfully
- ✅ No 404 errors
- ✅ Logo and styles load quickly

**Validation:**
- [ ] DOMContentLoaded < 1.5s
- [ ] Full page load < 3s
- [ ] Check Network tab for bottlenecks

---

### Test 46: Calculation Performance

**Objective:** Measure calculation speed

**Steps:**
1. Open browser console
2. Run calculation multiple times
3. Use `console.time()` to measure:
   ```javascript
   console.time('calc');
   // Click Calculate button
   console.timeEnd('calc');
   ```

**Expected Results:**
- ✅ Calculations complete in < 100ms
- ✅ UI updates immediately
- ✅ No lag or freeze

**Validation:**
- [ ] Forward calculations: < 50ms
- [ ] Reverse calculations: < 100ms
- [ ] UI remains responsive

---

### Test 47: Memory Usage

**Objective:** Check for memory leaks

**Steps:**
1. Open DevTools → Performance/Memory tab
2. Complete 50+ calculations (switch modes, change countries)
3. Take memory snapshots
4. Compare memory usage

**Expected Results:**
- ✅ Memory usage stable
- ✅ No significant memory growth
- ✅ Garbage collection works properly

**Validation:**
- [ ] Memory doesn't continuously increase
- [ ] No console warnings about memory

---

### Test 48: Large Dataset (Allocation)

**Objective:** Test many clients in Allocation mode

**Steps:**
1. Allocation mode
2. Add 10+ clients
3. Fill all fields
4. Calculate

**Expected Results:**
- ✅ Calculation completes successfully
- ✅ All clients rendered in results
- ✅ Performance remains acceptable
- ✅ UI doesn't break

**Validation:**
- [ ] Can add many clients without issues
- [ ] Table scrolls if needed
- [ ] Print output handles many clients

---

## Final Checklist

### ✅ All Tests Completed

After completing all tests, verify:

- [ ] **No JavaScript errors** in console (any browser)
- [ ] **All calculations mathematically correct**
- [ ] **Mode isolation** - no cross-contamination
- [ ] **Currency conversions accurate**
- [ ] **Print outputs professional** for all modes
- [ ] **Mobile responsive** design works
- [ ] **Input validation** prevents invalid data
- [ ] **Performance acceptable** (< 100ms calculations)
- [ ] **Browser compatibility** confirmed (4+ browsers)
- [ ] **No memory leaks** or performance degradation

---

## 🐛 Bug Reporting Template

If you find issues during testing, use this template:

```
**Bug Title:** [Short description]

**Severity:** Critical / High / Medium / Low

**Test Number:** Test X - [Test name]

**Steps to Reproduce:**
1. Step 1
2. Step 2
3. Step 3

**Expected Result:**
What should happen

**Actual Result:**
What actually happens

**Browser:** Chrome 120 / Firefox 121 / Safari 17 / Edge 120

**Screenshots:** [Attach if applicable]

**Console Errors:** [Copy any error messages]

**Additional Notes:** Any other relevant information
```

---

## 📊 Test Summary Template

After completing all tests:

```
**Test Date:** YYYY-MM-DD
**Tester Name:** [Your name]
**Browser(s):** [List all browsers tested]

**Tests Passed:** X / 48
**Tests Failed:** Y / 48
**Bugs Found:** Z

**Critical Issues:**
- [List any critical bugs]

**Recommendations:**
- [Any suggestions for improvements]

**Overall Assessment:** ✅ Pass / ⚠️ Pass with Issues / ❌ Fail
```

---

## 🎯 Testing Tips

1. **Test methodically** - Don't skip steps
2. **Check console frequently** - Catch JavaScript errors
3. **Test edge cases** - Where bugs usually hide
4. **Cross-browser testing is essential** - Different engines behave differently
5. **Document everything** - Screenshots help debugging
6. **Test mobile devices** - Not just emulators
7. **Use real data** - Test with realistic scenarios
8. **Performance matters** - Users notice slow apps
9. **Print/Export is critical** - Business users rely on this
10. **Have fun!** - Testing reveals how solid your app is

---

**Good luck with your comprehensive testing! 🚀**

If you find any issues, fix them and re-test before deployment.
