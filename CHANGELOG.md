# Changelog

Updates to the Michigan Hospital Price Transparency Project, newest first.

## 2026-11-27

### Rates posted without a dollar amount
- **Classified all 29.8 million rates that have no dollar figure:**
  - **Packaged (87%):** the service is paid as part of a stay or visit, such as "bundled into the DRG payment" or "not separately reimbursed."
  - **Tied to an external fee schedule:** a Medicare, Medicaid or payer fee schedule that the file doesn't include.
  - **A percentage of a fee schedule:** for example, 100–135% of Medicare.
  - **A percentage of charges with no charge posted:** mostly inpatient stays, where the total charge isn't known in advance.
- **Estimated dollar amounts** for about 527,000 rates at 10 hospitals where the file allows it: the percentage of charges × the item's posted gross charge. That is the same calculation hospitals use on the 93 million rates where they post both. One hospital had put dollar amounts in the percentage field, and those were recovered as dollars.
- **Estimates are kept separate** from posted rates and labeled. They run 2–5 times what other insurers pay for the same items, because percent-of-charges contracts usually belong to small insurers, auto and workers' compensation plans, and out-of-network arrangements.
- **Excluded:** placeholder gross charges of $0.01.

## 2026-11-26

### Access to emergency care
- **New measure:** straight-line distance from each Michigan ZIP code area to the nearest hospital and the nearest emergency department. Results are summarized by county using Census population.
- **Sources:**
  - Emergency departments come from the Michigan College of Emergency Physicians' 2026 list and the MDHHS freestanding ED directory, instead of the CMS hospital list.
  - Hospitals in Wisconsin, Indiana and Ohio are included for border residents.
  - Distances never cross Lake Michigan, though trips across the Mackinac Bridge are allowed.
- **Finding:** 13 counties (about 216,000 people) have no hospital. Freestanding EDs cut the number of residents more than 30 miles from emergency care from about 17,000 to about 11,300.
- **Corrections to public data:**
  - five hospitals that CMS lists as having no emergency services do have EDs
  - one hospital is assigned to the wrong county in the CMS file
  - a freestanding ED is missing from the state directory

### Hospitals linked to counties
- Every hospital is linked to its county and ZIP code, with Census population, land area and density for all 83 counties.

### Population and demographics
- Added Census American Community Survey 2024 5-year data for every county and ZIP code area: population and age, education, household income, and health insurance coverage. United States figures are included as a benchmark.

### Drug pricing units
- Rebuilt the test that determines whether each hospital's injectable drug prices are per billing unit or per vial.
- 97 of 123 hospitals now have a determined convention, up from 38 of 99. New methods cover hospitals that post no NDC on drug lines and hospitals that post only negotiated rates.
- Rebuilt the insulin unit check on current files.

### Refreshed hospital files
- Loaded new files for six hospitals whose posted files were more than a year old or incomplete. Every Michigan hospital in the dataset now has a current file.

### Insurance premiums and employer plans
- Added 2027 Marketplace premiums by rating area, the 2027 Medicare Advantage plan landscape, MEPS-IC 2025 employer premiums for Michigan and the United States, and 2025 Form 5500 filings for Michigan employer health plans.
- **Finding:** Form 5500 cannot name the administrator of most large self-insured employer plans, because those plans pay benefits from the employer's general assets and file no service-provider schedule. Several large employers' programs appear by name in the hospital price files instead.

## 2026-11-23 to 2026-11-25

### Drug code repair
- Repaired NDCs damaged by spreadsheet formatting: lost leading zeros, added suffixes, and package quantities appended to the code. Every change is logged with its original value.
- The share of NDCs that match a federal reference (FDA, NADAC or CMS ASP) rose from 34% to 82%.

### Retired drug billing codes
- Flagged 7,786 drug lines where the hospital's billing code disagrees with CMS's code for that NDC.
- Mapped retired codes to their replacements only where the CMS HCPCS quarterly update and ASP crosswalk both confirm the change: 3,622 lines.

### Payer names
- Applied a reviewed set of payer-name rules, covering spelling variants and product-line corrections such as Medicare Advantage plans posted under commercial names. Different companies are never merged.

## 2026-11-22

### All Michigan hospitals loaded
- Loaded price files for all 162 Michigan hospitals with posted files: about 190 million payer rates after duplicate plan names were combined.
- Cross-checked the hospital list against CMS and Patient Rights Advocate.

### Medicare benchmarks
- Built hospital-specific Medicare benchmarks for inpatient stays (IPPS and LTCH, FY2027), outpatient services (OPPS), lab tests (CLFS) and Part B drugs (ASP).
- **Validation:** hospitals' own posted Medicare rates match the benchmark at 96–100%.

### Data-quality flags
- Flagged placeholder, duplicate and boilerplate rates (for example, identical small amounts repeated across thousands of services). Flagged rows are kept and labeled, not deleted.

### First results
- Commercial inpatient rates were a median of about 1.8 times Medicare. Outpatient imaging showed the widest gaps.
