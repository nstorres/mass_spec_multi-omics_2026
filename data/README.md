# Input provenance

The following files were copied without modification from the user-provided UPAG project:

- `dia_lfq_protein_updated_headers_2026-07-16.txt`
- `sample_meta_2026-07-16.txt`
- `idmapping_2026_07_16.tsv`

The UniProt export supplies mouse gene annotations; the workshop preserves original accessions and complete exported gene-name fields. A first-symbol rule is an explicit teaching simplification.

`kegg_higher_WT_TP_2026-07-16.txt` is the saved Enrichr result from the original UPAG workshop, copied from its `work/` folder. It uses `KEGG_2019_Mouse` and the original WT_TP hit list. The revised lesson generates a gene list using the updated UniProt mapping. Students can submit that list in the live exercise. [Enrichr](https://maayanlab.cloud/Enrichr/) and [KEGG](https://www.kegg.jp/).

Day 2 loads `nutrimouse` directly from the installed mixOmics R package. No additional Day 2 input file is needed. Source documentation: https://github.com/mixOmicsTeam/mixOmics/blob/master/man/nutrimouse.Rd

The source dataset is credited to Pascal Martin and colleagues (2007). Day 2 builds the metadata from the package's sample rows and uses labels such as `Mouse_1` for the paired gene and lipid profiles. In the sample-matching exercise, students reverse the lipid columns in a practice copy and use the metadata to restore the order. SNF uses all 40 mice with both measurements. [Original study](https://doi.org/10.1002/hep.21510)

The lipid table contains percentages of 21 fatty acids measured in mouse liver. Day 2 reads these percentages as supplied, including the reported zeros. The optional MetaboAnalyst demonstration uses the web tool's built-in human protein and compound example.
