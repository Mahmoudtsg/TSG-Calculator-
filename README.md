# TSG Salary & Cost Calculator

![TSG Logo](images/tsg-logo.png)

A comprehensive web-based salary and cost calculator for staffing professionals. Calculate payroll costs, taxes, business margins, and profitability across multiple countries and engagement types.

---

## 🚀 Overview

**Version:** 1.2.3  
**Release Date:** January 15, 2026  
**Developed for:** Technology Staffing Group (TSG)

This tool helps staffing professionals quickly and accurately calculate:
- Employee salaries (net ↔ gross conversions)
- Total company costs (including all social contributions)
- Tax and social security deductions
- Business margins and daily rates
- Multi-client allocation profitability
- Real-time currency conversions

### Key Differentiators
✅ **Three Engagement Types** - Employee payroll, B2B contractors, and multi-client allocations  
✅ **Multi-Country Support** - Switzerland, Romania, and Spain with country-specific tax rules  
✅ **Bi-directional Calculations** - Calculate from net salary, gross salary, or total company cost  
✅ **Live Currency Conversion** - Real-time EUR conversion with 24-hour cache  
✅ **Swiss Salary Benchmarking** - Compare salaries against market data (Switzerland only)  
✅ **Professional PDF Export** - Print-ready reports with TSG branding  

---

## 📊 Engagement Types

### 1. 👤 Employee Mode (TSG Payroll)
Calculate comprehensive payroll costs for employees on TSG's books.

**Features:**
- Net ↔ Gross ↔ Total cost conversions
- Social security contributions (country-specific)
- Tax withholdings and deductions
- Employer costs and contributions
- Business margin calculations
- **Swiss Salary Benchmark** (Switzerland only)

**Available for:** Switzerland, Romania, Spain

**Swiss Salary Benchmark:**
- Intelligent job title matching with fuzzy search
- Salary comparison against real market data
- Visual salary range indicators
- Position percentile display
- Handles abbreviations (e.g., "ML Engineer" → "Machine Learning Engineer")

---

### 2. 🤝 B2B Mode (Independent Contractor)
Business-to-business contractor cost modeling for independent consultants.

**Features:**
- Contractor cost input (daily or hourly rates)
- Three pricing modes:
  - **Target Margin %** - Calculate required client rate
  - **Client Daily Rate** - Calculate margin from known rate
  - **Client Budget** - Work backwards from budget
- Multi-currency support
- Profit margin and markup analysis

**Note:** No payroll taxes or social security—pure cost/revenue modeling.

---

### 3. 📊 Allocation Mode (Multi-Client Profitability)
Commercial profitability modeling when one employee is allocated to multiple clients simultaneously.

**Key Concept:** The employer pays one fixed daily cost (deducted once), and additional client allocations generate incremental profit.

**Features:**
- Base salary at 100% with engagement percentage
- Employer multiplier (e.g., 1.20)
- Dynamic client table (unlimited clients)
- Allocation percentage per client
- Automatic baseline client identification
- Incremental profit calculation
- Annual profit projections

**Calculation Logic:**
```
1. Engaged Salary = Salary × (Engagement% / 100)
2. Employer Cost = Engaged Salary × Multiplier
3. Base Daily Cost = Employer Cost / Working Days [PAID ONCE]

For each client:
4. Client Revenue/Day = Daily Rate × (Allocation% / 100)

5. Baseline Client = Highest revenue/day client
   - Baseline Profit = Revenue - Base Daily Cost

6. Other Clients = Incremental profit
   - Profit = Revenue (cost already covered)

7. Total Profit = Sum of all client profits
```

**Example:**
```
Inputs:
- Salary 100%: 160,000 CHF
- Engagement: 80%
- Multiplier: 1.20
- Working Days: 220
- Client A: 60% allocation, 1,250 CHF/day
- Client B: 20% allocation, 1,250 CHF/day

Results:
- Base Daily Cost: 698.18 CHF
- Client A Revenue: 750 CHF → Profit: 51.82 CHF (baseline)
- Client B Revenue: 250 CHF → Profit: 250 CHF (incremental)
- Total Daily Profit: 301.82 CHF
- Annual Profit: 66,400.40 CHF
```

---

## 🌍 Supported Countries

### 🇨🇭 Switzerland (CHF)
**Tax Year:** 2026

**Social Contributions:**
- **AVS** (Old-age insurance): 4.35% employee + 4.35% employer
- **AI** (Disability insurance): 0.70% employee + 0.70% employer
- **APG** (Income compensation): 0.25% employee + 0.25% employer
- **AC** (Unemployment): 1.10% each (capped at 12,350 CHF/month)
- **AF** (Family allowances): 2.25% employer only
- **AMat** (Maternity): 0.029% each (Geneva 2026)
- **CPE** (Training fund): 0.07% employer only
- **LFP** (Vocational training): 0.03-0.08% employer (configurable)
- **LPP** (Pension): Variable rate (default 7%, age-dependent) with mandatory cap
- **LAA** (Accident insurance): 1% employer (professional), configurable employee (non-professional, default 1.5%)

**2026 BVG/LPP Updates:**
- Minimum salary for LPP: 22,680 CHF/year
- Coordination deduction: 26,460 CHF/year
- BVG maximum insured salary: 90,720 CHF/year
- Pension plan mode toggle:
  - **Mandatory BVG** (default): Insured salary capped at 90,720 CHF/year
  - **Super-obligatory**: Uncapped insured salary for high earners

**Important Notes:**
- ❗ Income tax NOT included (varies by canton, commune, church)
- AC ceiling: Monthly gross capped at 12,350 CHF (annual ceiling 148,200 / 12)
- LAA non-professional rate varies by insurer

**Resources:**
- LPP Reference: [www.ciepp.ch](http://www.ciepp.ch)

---

### 🇷🇴 Romania (RON)

**Social Contributions:**
- **CAS** (Social security): 25% employee
- **CASS** (Health insurance): 10% employee
- **CAM** (Work insurance): 2.25% employer
- **Income tax**: 10% on taxable base
- **Personal deduction**: 510 RON/month (base function only)
- **Dependent deduction**: 110 RON/month per dependent

**Advanced Options:**
- Tax exemptions for IT workers
- Tax exemptions for disabled persons
- Monthly meal benefits (non-taxable)
- Base function toggle affects personal deductions

---

### 🇪🇸 Spain (EUR)

**Social Contributions:**
- **Common Contingencies**: 4.70% employee + 23.60% employer
- **Unemployment**: 1.55% employee + 5.50% employer
- **Professional Training**: 0.10% employee + 0.60% employer
- **FOGASA**: 0.20% employer only
- **Contribution base**: Min 1,323 EUR, Max 4,720.50 EUR/month
- **IRPF** (Income tax): Progressive bands (19%-47%)

**Important Notes:**
- ⚠️ IRPF is an **estimate** based on simplified progressive bands
- Actual withholding depends on personal circumstances and autonomous community
- Contribution base limits applied to social security (not IRPF)

---

## ✨ Key Features

### Core Functionality
- ✅ **Bi-directional Calculations** - Start from net, gross, or total cost
- ✅ **Three Calculation Modes** per country
- ✅ **Salary Period Toggle** - Monthly or yearly input
- ✅ **Reverse Calculations** - Advanced iterative algorithms
- ✅ **Live Currency Conversion** - All amounts shown in local currency + EUR
- ✅ **Editable Exchange Rates** - Manual override with auto-refresh
- ✅ **Occupation Rate** - Configure part-time employment (60%, 80%, 100%)
- ✅ **Advanced Options** - Meal benefits, dependents, tax exemptions, pension rates
- ✅ **Business Metrics** - Daily/monthly rates, profit margins, markup
- ✅ **Formula Transparency** - View calculation steps with "?" help icons
- ✅ **Employee Information** - Capture name, date of birth, role
- ✅ **PDF Export** - Professional reports with TSG branding
- ✅ **Responsive Design** - Works on desktop, tablet, mobile

### Technical Features
- 🏗️ **Modular Architecture** - Separate rule engines per country
- 🔄 **Real-time Calculations** - Instant results with debounced inputs
- 💾 **Client-side Caching** - Exchange rates cached for 24 hours
- 🎨 **TSG Branding** - Professional design with brand colors
- ♿ **Accessibility** - WCAG-compliant design
- 📱 **Mobile-First** - Responsive grid system
- 🔐 **Privacy-First** - All calculations client-side, no data transmission

---

## 📂 Project Structure

```
tsg-salary-calculator/
├── index.html                  # Main application file
├── css/
│   ├── style.css              # Main styles with TSG branding
│   ├── print.css              # Print-specific styles
│   └── salaryBenchmark.css    # Swiss benchmark styles
├── js/
│   ├── main.js                # Application entry point
│   ├── calculator.js          # Employee payroll calculation engine
│   ├── allocation.js          # Allocation mode calculation engine
│   ├── ui.js                  # UI management and display
│   ├── fxService.js           # Currency exchange service
│   ├── salaryBenchmark.js     # Swiss salary benchmark feature
│   ├── swissSalaryData.js     # Swiss market salary data
│   └── rules/
│       ├── romania.js         # Romania tax and contribution rules
│       ├── switzerland.js     # Switzerland tax and contribution rules
│       └── spain.js           # Spain tax and contribution rules
├── images/
│   └── tsg-logo.png           # TSG company logo
├── data/
│   └── IT_Salaries_Switzerland_2025.xlsx    # Swiss salary benchmark data
└── README.md                  # This file
```

---

## 🚦 Getting Started

### Prerequisites
- Modern web browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- Internet connection (for exchange rates and CDN libraries)

### Installation

**Option 1: Direct Access (Simplest)**
1. Download or clone the project
2. Open `index.html` in your web browser
3. Start calculating!

**Option 2: Local Server (Recommended for Development)**

Using Python:
```bash
python -m http.server 8000
```

Using Node.js:
```bash
npx serve
```

Using PHP:
```bash
php -S localhost:8000
```

Then navigate to `http://localhost:8000`

### No Build Process Required
This is a static website with no dependencies to install. All libraries are loaded via CDN:
- Font Awesome (icons)
- Google Fonts (Inter font family)
- jsPDF (PDF export)
- html2canvas (PDF rendering)

---

## 📖 How to Use

### Step 1: Select Engagement Type

Choose from three engagement types:
1. **👤 Employee** - TSG payroll calculations
2. **🤝 B2B** - Independent contractor modeling
3. **📊 Allocation** - Multi-client profitability

---

### Employee Mode

1. **Select Country**: Switzerland, Romania, or Spain
2. **Select Calculation Mode**:
   - **From Net Salary** - Calculate gross and total cost
   - **From Gross Salary** - Calculate net and total cost
   - **From Total Company Cost** - Calculate gross and net
3. **Enter Amount**: Input the salary or cost
4. **Choose Period**: Monthly or yearly
5. **Click Calculate**: View detailed breakdown

**Advanced Options:**
- Monthly meal benefits (non-taxable in Romania)
- Base function toggle (Romania)
- Number of dependents (for tax deductions)
- Tax exemption status
- LPP pension rate (Switzerland)
- LFP vocational training rate (Switzerland)
- LAA non-professional rate (Switzerland)
- BVG pension plan mode (Switzerland)

**Swiss Salary Benchmark:**
- Available only for Switzerland Employee mode
- Enter job title in the benchmark field
- View salary comparison with market data
- See where the salary falls in the market range

---

### B2B Mode

1. **Enter Contractor Cost**:
   - Daily or hourly rate
   - Select currency (EUR, CHF, RON)
   - Input cost per unit

2. **Choose Pricing Mode**:
   - **Target Margin %** - Set desired profit margin, calculate required client rate
   - **Client Daily Rate** - Enter client rate, calculate actual margin
   - **Client Budget** - Enter total budget and days, work backwards

3. **Select Display Currency**: View results in any supported currency

4. **Click Calculate**: View profitability analysis

---

### Allocation Mode

1. **Enter Base Parameters**:
   - **Salary at 100%**: Annual base salary
   - **Engagement %**: Percentage engaged (0-100%)
   - **Employer Multiplier**: Cost multiplier (e.g., 1.20)
   - **Working Days/Year**: Default 220

2. **Add Clients**:
   - Click **"Add Client"** to add rows
   - Enter client name, allocation %, and daily rate
   - Total allocation % must not exceed engagement %

3. **Click Calculate**:
   - View base daily cost (paid once)
   - See revenue and profit per client
   - Identify baseline client
   - Review total daily and annual profit

---

## 💱 Currency Conversion

### Display in EUR
Toggle **"Display in EUR"** to convert all amounts to EUR using live exchange rates.

**Features:**
- Shows current exchange rate
- Displays last update date
- Rates cached for 24 hours
- Manual refresh available

**Exchange Rate Formula:**
All conversions go through RON as base currency:
1. Input → RON: `valueRON = valueInput × RON_per_input`
2. RON → Target: `valueTarget = valueRON / RON_per_target`

**Exchange Rate Provider:** exchangerate-api.com

---

## 🧮 Calculation Methods

### Forward Calculation (Gross → Net)
1. Apply employee social security contributions
2. Calculate taxable base (after deductions)
3. Apply income tax (progressive or flat rate)
4. Subtract from gross to get net salary
5. Add employer contributions to get total company cost

### Reverse Calculation (Net → Gross)
**Method:** Newton-Raphson iteration
- Initial estimate: Net × 1.5
- Iterate until convergence (tolerance: 0.01)
- Maximum 50 iterations
- Adjusts based on effective tax rate

### Reverse Calculation (Total → Gross)
**Method:** Binary search
- Search range: 0 to Total Cost
- Iterate until convergence (tolerance: 0.01)
- Maximum 50 iterations
- More stable than Newton-Raphson for this case

### Rounding Rules
- All monetary values rounded to 2 decimal places
- Rounding method: `Math.round(value * 100) / 100`
- Applied consistently across all calculations

---

## 📄 Export & Print

### PDF Export
Generate professional PDF reports with:
- TSG logo and branding
- Engagement type indicator
- Complete input summary
- Detailed calculation breakdown
- All contributions and deductions
- Business metrics (if applicable)

### Print-Friendly Output
Optimized print layout with:
- Clean, professional formatting
- TSG brand colors
- Page break optimization
- Logo at the top
- Essential information only
- Mode-specific results (no cross-contamination)

---

## 🔧 Configuration & Maintenance

### Updating Tax Rates (Annual)

Tax rates change annually. Update files in `js/rules/`:

**Romania (`js/rules/romania.js`):**
```javascript
rates: {
    CAS: 0.25,              // Update if changed
    CASS: 0.10,             // Update if changed
    INCOME_TAX: 0.10,       // Update if changed
    CAM: 0.0225,            // Update if changed
    PERSONAL_DEDUCTION: 510, // Update annually
    DEPENDENT_DEDUCTION: 110 // Update annually
}
```

**Switzerland (`js/rules/switzerland.js`):**
```javascript
rates: {
    AVS_EMPLOYEE: 0.0435,    // Update if changed
    AC_CEILING: 148200,      // Update annually
    LPP_MIN_SALARY: 22680,   // Update annually (2026 value)
    LPP_COORDINATION: 26460, // Update annually (2026 value)
    BVG_MAX_INSURED: 90720,  // Update annually (2026 value)
    // ... other rates
}
```

**Spain (`js/rules/spain.js`):**
```javascript
rates: {
    SS_BASE_MIN: 1323.00,    // Update annually
    SS_BASE_MAX: 4720.50,    // Update annually
    IRPF_BANDS: [            // Update if changed
        { limit: 12450, rate: 0.19 },
        { limit: 20200, rate: 0.24 },
        // ...
    ]
}
```

### Updating Working Days

Change in `js/calculator.js`:
```javascript
WORKING_DAYS_PER_YEAR: 220,  // Update if needed
```

### Updating Swiss Salary Benchmark Data

Replace `data/IT_Salaries_Switzerland_2025.xlsx` with updated data.  
Update `js/swissSalaryData.js` with new salary ranges.

### Customizing Brand Colors

Update in `css/style.css`:
```css
:root {
    --tsg-red: #ED1C24;      /* Primary brand color */
    --tsg-black: #231F20;    /* Primary text color */
    --digital-blue: #005DFF; /* Accent color */
}
```

---

## 🐛 Known Limitations

### Switzerland
- ❗ **Income tax NOT included** - varies by canton, commune, church tax
- ⚠️ LPP rates are configurable but age-dependent in reality
- ⚠️ LAA rates are estimates (vary by industry/company)
- ℹ️ AC additional rate (0.5%) above ceiling applies automatically

### Romania
- ⚠️ Meal vouchers not automatically calculated (can be added in benefits)
- ℹ️ Tax exemptions are binary (on/off) - no partial exemptions
- ℹ️ Personal deductions only apply if "base function" is checked

### Spain
- ❗ **IRPF is an estimate** - actual withholding varies significantly
- ⚠️ Simplified progressive bands used
- ⚠️ Does not account for:
  - Autonomous community variations
  - Personal circumstances (disability, family)
  - Annual adjustments (14 payments vs 12)

### General
- 💱 Exchange rates updated daily (cached 24h)
- 📅 Calculations assume standard employment contracts
- 🔢 Reverse calculations have ±0.01 to ±1.00 tolerance
- 🌐 Requires internet connection for FX rates and CDN libraries

---

## 🔐 Privacy & Security

- ✅ **All calculations performed client-side** (no data sent to servers)
- ✅ **No personal data stored** (except localStorage for FX cache)
- ✅ **No cookies used**
- ✅ **GDPR compliant**
- ✅ **No tracking or analytics**
- ⚠️ PDF exports contain entered data (handle appropriately)

---

## 🌐 Browser Compatibility

| Browser | Minimum Version | Status |
|---------|----------------|--------|
| Chrome | 90+ | ✅ Fully Supported |
| Firefox | 88+ | ✅ Fully Supported |
| Safari | 14+ | ✅ Fully Supported |
| Edge | 90+ | ✅ Fully Supported |
| Opera | 76+ | ✅ Fully Supported |
| IE 11 | - | ❌ Not Supported |

**Required Browser Features:**
- ES6+ JavaScript
- CSS Grid & Flexbox
- Fetch API
- LocalStorage
- CSS Custom Properties

---

## 📊 Performance

- **Initial Load**: < 2s on 3G connection
- **Calculation Speed**: < 100ms per calculation
- **FX Rate Cache**: 24-hour client-side cache reduces API calls
- **No Build Process**: CDN libraries loaded on-demand

---

## 🚧 Future Enhancements

### Planned Features
- [ ] Additional countries (France, Germany, UK)
- [ ] Export to Excel format
- [ ] Save/load calculation scenarios
- [ ] Comparison mode (side-by-side countries)
- [ ] Annual tax declaration preview
- [ ] Multi-language support (English, French, German)
- [ ] Dark mode theme

### Technical Improvements
- [ ] Add automated unit tests
- [ ] Implement service worker for offline use
- [ ] Add progressive web app (PWA) capabilities
- [ ] Optimize for very slow connections
- [ ] Add automated tax rate update notifications

---

## 📞 Support

**Developed by:** TSG Internal Development Team  
**For support:** Contact your HR or Finance department  
**Version:** 1.2.3  
**Last Updated:** January 15, 2026

---

## 📄 License

**© 2026 Technology Staffing Group. All rights reserved.**

This tool is for internal use only. Unauthorized distribution is prohibited.

---

## 🙏 Acknowledgments

- **Exchange Rates:** exchangerate-api.com
- **Icons:** Font Awesome
- **Fonts:** Google Fonts (Inter)
- **PDF Export:** jsPDF library
- **PDF Rendering:** html2canvas library
- **Swiss Salary Data:** Based on Swiss IT market research 2025

---

## ⚠️ Disclaimer

This calculator provides **estimates** based on current tax rules and rates. Results should be used for planning purposes only.

**For accurate payroll processing:**
- Consult with certified tax professionals
- Verify with official government sources
- Consider individual circumstances
- Account for local variations and exceptions

**Tax laws change frequently.** This tool should be reviewed and updated annually to ensure compliance with current regulations.

---

## 📝 Quick Reference

### Romania Quick Rates
- CAS: 25% (employee)
- CASS: 10% (employee)
- CAM: 2.25% (employer)
- Income Tax: 10%

### Switzerland Quick Rates  
- AVS/AI/APG: 5.3% (employee + employer each)
- AC: 1.1% each (up to ceiling)
- LPP: ~7-18% (age-dependent)
- AF: 2.25% (employer only)

### Spain Quick Rates
- Employee SS: ~6.35%
- Employer SS: ~29.90%
- IRPF: 19-47% (progressive)
- Base: 1,323 - 4,720.50 EUR

---

**🎯 Ready to calculate? Open `index.html` and start exploring!**
