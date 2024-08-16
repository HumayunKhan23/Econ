# SSA State-Level Disability Claims Data Cleaning and Replication

This repository contains Stata code for cleaning and analyzing state-level disability claims data from the Social Security Administration's State Agencies Monthly Workload (MOWL) dataset. The dataset covers the years 2002–2017 for all 50 states and the District of Columbia.

Data excludes claims processed in Guam, Puerto Rico, federal disability processing centers, and certain extended services teams.

## Repository Structure

- **data/raw/**: Contains the raw MOWL dataset.
- **data/final/**: Contains the cleaned and processed dataset (`ssa_state.dta`).
- **output/figures/replication/**: Contains the generated figures for the replication exercise.

## Files

- **`ssa_state_cleaning.do`**: Stata code for cleaning the SSA state-level dataset.
- **`ssa_state_replication.do`**: Stata code for replicating the results from Engelhardt's paper.

## Data Cleaning (`ssa_state_cleaning.do`)

This script performs the following tasks:

1. **Import Raw Data**: Imports the raw data from the Excel file `SSA-SA-MOWL.xls`. This can be found at this link https://www.ssa.gov/disability/data/SSA-SA-MOWL.xls

2. **Variable Renaming**: Renames the original variables by adding an underscore prefix to avoid conflicts with Stata's reserved keywords.

3. **Variable Generation**:
   - Generates state FIPS codes.FIPS codes are government issued numerical identifiers that are used to uniquely identify states. FIPS codes are more commonly used 
     in these types of datasets over state name or state abbreviation.
   - Excludes specific records as in the Engelhart paper. (federal disability processing components, Guam, Puerto Rico, and certain extended services teams).
   - Extracts and formats date information. The SSI dataset we has the dates formatted as year-month. The "-" makes the variable a string. However we needed to 
     merge the SSI and minimum wage datasets and the minimum wage dataset contained the dates as a numerical variable in ym format so we converted the SSI date 
     variable to ym as well to allow merging.
   - Creates variables for different types of claims, including SSDI-only, SSI-only, and concurrent claims. 
   - Calculates allowance rates for each claim type.
   - Generates variables for reconsiderations and continuing disability reviews (CDRs).
   - Combines SSDI-only and concurrent SSDI & SSI claims into a single set of variables. 

4. **Save Cleaned Data**: The final cleaned dataset is saved as `ssa_state.dta` in the `data/final/` directory.

## Replication (`ssa_state_replication.do`)

This script replicates the results from Gary V. Engelhardt's paper, "The minimum wage and DI claims":

1. **Figure 1**:

   - Figure one is from 2001-2017. One line represents the unemployment rate and the other being claims.
   - Code generates indices for SSDI-only, SSDI+SSI, and SSDI-only + concurrent claims.
  
2. **Separate Analysis**

   - Create local variables for SSDSI + SSI, SSDI-only, SSI-only, SSI DC, and SSDI-only + Concur.
