# SSA State-Level Disability Claims Data Cleaning and Replication

This repository contains Stata code for cleaning and analyzing state-level disability claims data from the Social Security Administration's State Agencies Monthly Workload (MOWL) dataset. The dataset covers the years 2002–2017 for all 50 states and the District of Columbia.

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

3. **Technical Variable Generation**:
   - Generates state FIPS codes.
   - Excludes specific records (federal disability processing components, Guam, Puerto Rico, and certain extended services teams).
   - Extracts and formats date information.

4. **Disability Claims Variables**:
   - Creates variables for different types of claims, including SSDI-only, SSI-only, and concurrent claims.
   - Calculates allowance rates for each claim type.
   - Generates variables for reconsiderations and continuing disability reviews (CDRs).

5. **Calculated DI Variables**:
   - Combines SSDI-only and concurrent SSDI & SSI claims into a single set of variables.

6. **Save Cleaned Data**: The final cleaned dataset is saved as `ssa_state.dta` in the `data/final/` directory.

## Replication (`ssa_state_replication.do`)

This script replicates the results from Gary V. Engelhardt's paper, "The minimum wage and DI claims":

1. **Figure 1**: 
   - Generates indices for SSDI-only, SSDI+SSI, and SSDI-only + concurrent claims, normalized to 2001 values.
   - Creates line graphs for each claim type over the years 2001-2017.

2. **Data Handling**:
   - Uses the cleaned dataset `ssa_state.dta`.
   - Excludes SSI Disabled Child claims for certain calculations.

## Sample Notes

The dataset used is a state-year panel of DI claims for 2002–2017. It includes claims processed in the 50 states and the District of Columbia but excludes claims processed in Guam, Puerto Rico, federal disability processing centers, and certain extended services teams.

## How to Run

1. Clone this repository:
   ```sh
   git clone https://github.com/yourusername/ssa-state-cleaning.git
