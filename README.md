# Michigan Hospital Price Transparency Project

An independent research project that collects the prices Michigan hospitals are required to publish, cleans them into one comparable dataset, and measures how what hospitals charge compares with what Medicare pays.

**Status:** data collection and validation are in progress (November 2026). The database and code will be released once validation is complete. This repository holds project documentation and a log of updates for now.

## Why this project

Since 2021, federal rules (45 CFR Part 180) have required U.S. hospitals to post machine-readable files listing their standard charges, including the rates they have negotiated with each insurer. In practice the files are hard to use:

- each one is large, often millions of rows
- formats vary by hospital
- the same insurer can appear under dozens of names
- drug prices are posted in different units

This project turns those files into a dataset where a price at one hospital can be fairly compared with a price at another, and with Medicare.

## What the dataset covers

- **Hospitals:** 162 Michigan hospitals with current price files: acute care, critical access, children's, long-term acute care and rehabilitation hospitals. This covers every hospital on the CMS list that has a file. Not included: 4 state psychiatric hospitals (by choice), 4 VA medical centers (federal facilities are exempt) and one behavioral health hospital that posts no file.
- **Prices:** about 190 million posted payer rates, plus gross charges and cash prices.
- **Benchmarks:** Medicare payment rates for inpatient stays (IPPS and LTCH PPS, FY2027), outpatient services (OPPS, October 2026), lab tests (Clinical Laboratory Fee Schedule) and Part B drugs (ASP, October 2026).
- **Context:** population, income, education and insurance coverage by county and ZIP code (Census ACS 2024 5-year), employer premiums (MEPS-IC 2025), Marketplace and Medicare Advantage plans for 2027, and distance to emergency care.

## How the data is built

1. **Ingest:** read each hospital's file (CSV or JSON, CMS template versions 2 and 3) and check it against the CMS data dictionary. Every number keeps a link to its source file and row.
2. **Identify and normalize payers:** map thousands of payer and plan names to insurers and product lines (commercial, Medicare Advantage, Medicaid managed care, and others). Different companies are never merged, and every rule change is reviewed.
3. **Normalize drug codes and units:** repair National Drug Codes (NDCs) damaged by spreadsheet formatting. Map retired drug billing codes to their replacements only when an official CMS crosswalk confirms the mapping. Determine, hospital by hospital, whether a drug price covers one billing unit or a whole vial.
4. **Flag data-quality issues:** flag rates that are placeholders, duplicates, boilerplate amounts or likely unit errors. Flagged rows are kept and labeled, never deleted.
5. **Build the Medicare benchmark:** compute what Medicare would pay each hospital for the same service, using that hospital's own wage index and payment adjustments.
6. **Validate:** confirm the benchmark against the hospitals' own posted Medicare rates. Posted Medicare and Medicare Advantage rates come out at 96–100% of the computed Medicare price.

## Early findings (preliminary)

These figures come from November 2026 data and will be updated as validation finishes.

- **Commercial insurance pays far more than Medicare.** The median commercial rate for an inpatient stay is about 181% of what Medicare pays for the same stay, with the middle half of rates between 146% and 233%. Medicare Advantage rates sit close to Medicare, at 96%.
- **The same procedure varies widely in price.** For a hip or knee replacement without complications (MS-DRG 470), Medicare pays about $17,700. Commercial rates across Michigan range from $7,650 to $71,699.
- **The gap is widest for imaging.** For CT scans, the typical commercial rate is about 8 times the Medicare rate.
- **Some communities are far from emergency care.** 13 Michigan counties, home to about 216,000 people, have no hospital. In the most remote, such as Ontonagon, Alcona and Montmorency, residents live 20–35 miles in a straight line from the nearest emergency department. Statewide, about 2.9% of residents live more than 15 miles from one.

## Data-quality findings

Building the dataset has surfaced problems in public data sources themselves:

- **CMS lists hospitals as having no emergency services when they do.** The CMS Hospital General Information file marks five Michigan general hospitals as having no emergency department. All five operate 24/7 EDs, confirmed by the hospitals and by the Michigan College of Emergency Physicians.
- **CMS lists one address per hospital certification number.** Several ED campuses (for example, Corewell Blodgett and Lakeland Niles) have no separate address in the CMS file.
- **The state's freestanding ED directory is incomplete.** The MDHHS directory (September 2024) leaves out at least one operating 24/7 freestanding ED, in Cheboygan County.
- **Some hospital files are hard to reach.** For example, one vendor's hosting site served an invalid security certificate.
- **Spreadsheet damage:** drug codes in some price files have lost their leading zeros.
- **Prices without dollar amounts:** some small hospitals post most negotiated rates only as a percentage of charges.

## Data sources

All source data is public:

- Hospital machine-readable price files, published by each hospital
- Centers for Medicare & Medicaid Services (CMS):
  - Hospital General Information
  - IPPS, LTCH, OPPS and CLFS payment files
  - ASP drug pricing files and NDC–HCPCS crosswalks
  - HCPCS quarterly updates
  - Marketplace public use files
  - Medicare Advantage landscape file
  - NADAC drug acquisition costs
- U.S. Food and Drug Administration: National Drug Code Directory
- U.S. Census Bureau: American Community Survey 2024 5-year estimates, Gazetteer files, ZCTA-to-county relationship file
- Agency for Healthcare Research and Quality: MEPS Insurance Component 2025
- U.S. Department of Labor: Form 5500 filings
- Michigan College of Emergency Physicians: Michigan Emergency Departments 2026
- Michigan Department of Health and Human Services: Free Standing ED Directory (September 2024)
- Patient Rights Advocate (hospitalpricingfiles.org), used to cross-check hospital file lists

## Limitations

- Posted prices are not paid claims. A file shows the contracted rate, not what a patient was billed or paid.
- A hospital's file covers its facility charges. Separate physician bills are not included.
- Some rates are posted only as a percentage of charges or as a formula, without a dollar amount.
- Distances are straight-line, not driving distances.
- Some hospital files are more than six months old. Each hospital's file date is tracked.

## Contact

Isabel Pereira de Almeida, MPH
isabelalmeidamph@proton.me

## Licence-Documents

License: Documentation and data in this repository are licensed under Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0). Please credit “Isabel Pereira de Almeida, MPH, Michigan Hospital Price Transparency Project.” For commercial use, contact isabelalmeidamph@proton.me.

See [CHANGELOG.md](CHANGELOG.md) for a dated log of updates.
