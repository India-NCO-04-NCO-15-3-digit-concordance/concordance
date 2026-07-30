# Concordance at 3-digit between NCO 2004 and NCO 2015

This repository contains the concordance between the NCO 2004 and the NCO 2015 at the 3-digit level. The documentation in the repository explains the methods used in constructing the concordance and instructions to use the concordance are laid out in this READ_ME as well as in the excel file. Kindly use the citation for the dataset whenever used in any work.

## Instructions to use the concordance:

1. In **'step_1'**, NCO 2004 codes are provided in column A and the corresponding NCO 2015 code assigned to it are found in column B. Column C lists the NCO 2015 codes for the newly created categories and its mapping to NCO 2004 code. For example, 5_n3 maps back to 911 from NCO 2004 (column A). In **'step_2'**, column A lists all the NCO 2015 codes and column B shows which codes coalesced together into newly created categories.	
2. In order to harmonize occupational codes at the 3-digit level across the NCO 2004 and the NCO 2015 classifications in the PLFS microdata, start with 'step_1'. Merge on column A into the master dataset for all waves uptill 2020-2021. It is recommended to loop over the waves individually instead of appending them together. Retain both "nco15" and "nco15_col" at this point.	
3. The 'nco15' column needs to be adjusted to account for new categories that replaced the codes coalesced together. Use the data in 'step_2' for this. A short STATA code is provided below to help with this.	
	
	`merge m:1 nco15 using "step_2.dta", update` // *update option generates merge outcomes differently*

	`keep if inlist(_merge, 1, 3, 4)` // *this retains the unmatched and not updated codes from master (original codes), as well as those that were missing and got updated*

	`drop _merge`

	`tostring nco15, gen(nco15_str)` // *identifers should be in string values*

	`gen nco15_rev = ""` // *for a clean final mapping*

	`replace nco15_rev = nco15_col` // *add in the mapping to newly created categories*
  
	`replace nco15_rev = nco15_str if missing( nco15_rev)` // *add in the mapping to NCO 2015 codes*
	
5. For all the waves post 2020-2021, only the codes coalesced together need to be replaced with the new categories. For this, merge using 'step_2' on column A and carry out the replacements as shown in the code above. 	
6. Textual descriptions of the new groups that the authors used are provided below. It can be extracted to a separate file and then merged into the master dataset. Alternatively, other unique titles can be assigned based on user discretion.	
	
<img width="1013" height="532" alt="image" src="https://github.com/user-attachments/assets/99f4302a-8950-4535-8d93-e9932b93e7ae" />


