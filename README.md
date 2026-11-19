## Introduction to Mass Spectrometry Data Analysis and Multi-Omics Integration Workshop 2026

### Instructors

Paul Stewart, PhD (paul.stewart@hci.utah.edu)

Augustine Takyi, MS (augustine.takyi@hci.utah.edu)

Filipa Blasco Lopes, PhD (u6071085@utah.edu)

### Slido Link

https://app.sli.do/event/9J3yDJiS4gkgT6tDJXgFBF

### Link to this Repository:

https://github.com/pstew/mass_spec_multi-omics_2026/

### Workshop schedule

#### Day 1 — Thursday, November 19

| Time | Activity |
|:--|:--|
| 09:00-10:15 | Get started with a short R and RStudio tutorial, then take a first look at the omics data in the spreadsheet |
| 10:15-10:30 | Break |
| 10:30-12:00 | Read in the proteomics data, make QC plots, and explore the samples with PCA and heatmaps |
| 12:00-13:00 | Lunch |
| 13:00-14:15 | Match UniProt accessions to mouse gene symbols and test for differences in protein abundance |
| 14:15-14:30 | Break |
| 14:30-16:00 | Make volcano plots, run KEGG pathway enrichment, and save the results |

#### Day 2 — Friday, November 20

| Time | Activity |
|:--|:--|
| 09:00-10:30 | Questions from yesterday and getting started with today's data/metadata |
| 10:30-10:45 | Break |
| 10:45-12:00 | Review PCA, work through the practice questions, and start WGCNA |
| 12:00-13:00 | Lunch |
| 13:00-14:15 | Relate gene modules to fatty acids, then use SNF to combine the gene and lipid similarity networks |
| 14:15-14:30 | Break |
| 14:30-16:00 | Group the mice using the combined network, then use genotype, diet, and omics measurements to interpret the groups |

### R/RStudio download

- https://cran.r-project.org
- https://posit.co/download/rstudio-desktop/

### Materials

#### Day 1
- Intro
- GitHub
  - What it is
  - Getting files for today
- Getting started with R: https://monashbioinformaticsplatform.github.io/r-intro/start.html
- Set up project in a folder + new RStudio project
	- Importance of staying organized
	- Project folder structure
		- source files
		- data
		- scripts
		- work (or results)
	- More reading: https://pmc.ncbi.nlm.nih.gov/articles/PMC2709440/
- Let's look at DIA_LFQ_ProteinAbundanceForRscriptAnalysis.xlsx
	- For 100% reproducibility, we want to minimize data handling in Excel because Excel is prone to errors.
	- File names are important (and also contain important data)
		- Where it came from/what it is/what it is for
	- Questions to ask: what am I looking at? Are there the right number of samples? How many features (e.g. proteins)? Has the data been manipulated in any way? What annotations are there? Experimental groups? Do column names need a mapping table (e.g.  sample_01, sample_02, sample_03) and do not tell us what group they belong to?
		- Has both column annotation and row annotation. This is important “metadata” (aka meta data).
		- There are twenty samples across four conditions: KO_TP, KO_baseline, WT_TP, WT_baseline.
	- "Group Labels" are protein annotations. These look like Uniprot annotations (https://www.uniprot.org), which is pretty standard protein database for proteomics experiments. 
		- When in doubt about annotations, just check.
			- https://www.uniprot.org and https://www.uniprot.org/id-mapping
			- https://www.genecards.org
		- Cannot tell what the identity is just by looking at them. Eventually need to be mapped to gene symbols.
		- Be careful with Uniprot "Entry Name", which look like gene symbols but are not. Will cause issues when doing downstream analyses and looking them up in the literature.
		- Have ...-1, ...-2, which indicates isoforms.
			- Isoforms not always included in reference library
	- 7409 features (e.g. proteins).
		- A good number for shotgun proteomics.
		- Fewer features than expected can indicate sample or sample prep issues.
		- Very few features means it is likely a targeted proteomics experiment (and I might not be on the same page as to what kind of experiment was performed).
	- The filename identifies these as protein-level LFQ abundance values.
		- LFQ is label free quantification, which normalizes intensity values across runs to reduce technical variation. It uses pairwise peptide ratio comparisons to estimate protein-level abundance.
		- Not standarized! LFQ is a general concept, not a single method. MaxQuant LFQ (MaxLFQ) is different than MSFragger (via IonQuant).
		- Missing values are blank and have not been imputed (missing values replaced with some value or different values).
			- Good for analyses in R. R will treat blanks as NA, which is a special value representing missing (or undefined) data. 
			- We expect some missingness in mass spec data. 
				- Mass spec data that does not have missingness indicates it was imputed or possibly run with TMT (which tends to have very little missingness).
  		- Fix typo in H3.
	- Let's separate our column annotations to make separate meta data. 
		- Do not need to do it now, but we could also do this for row annotations since we generally have a lot of information associated with each protein/peptide in proteomics experiments.
		- A text editor like https://www.sublimetext.com can really help speed up basic text manipulation. This could mostly be done in RStudio as well.
		- Critically important for understanding what data we have and staying organized in our analysis.
			- Avoids "hard coding" of samples.
			- Easy to add additional data later as it becomes available.
		- We need unique column names. R will see duplicated column names and handle them implicitly, but this is can be prone to errors and lead to confusion for beginners. 
			- Better to define them explicitly.
		- Save with descriptive-name_date in data folder as a tab delimited text file. 
			- Why tab delimited files are generally a good idea.
			- Use yyyy-mm-dd date format for sorting. 
	- Delete the extra column headers in the experimental data since this information is saved in the meta data file. 
		- In R we will define the first row as the column header so we can refer to specific samples/conditions.
		- Save with descriptive-name_date in data folder as a tab delimited text file. 
	- Switch back to RStudio (see [Day 1 R Markdown](scripts/Day01_proteomics.Rmd)).

#### Day 2

Open [Day 2 R Markdown](scripts/Day02_SNF.Rmd).

