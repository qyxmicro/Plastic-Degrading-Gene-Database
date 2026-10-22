# Plastic-Degrading Gene Database (PDG Database)

A curated reference database of plastic-degrading genes (PDGs) for the identification and characterization of potential plastic-degradation functions in environmental metagenomes.

## Overview

This repository provides a collection of reference protein sequences associated with plastic degradation, together with gene classification annotations.

The reference database was compiled from three publicly available resources:

- **PlasticDB** — a database of microorganisms and proteins associated with plastic biodegradation.
- **PAZy** — the Plastics-Active Enzymes Database.
- **PDG_DB** — a database of plastic-degrading genes for environmental multi-omics analysis.

A total of 956 reference protein sequences were collected from these resources (228 from PlasticDB, 414 from PAZy, and 314 from PDG_DB). After sequence clustering at 95% amino acid identity, 527 non-redundant representative protein sequences were retained.

The database is intended for homology-based screening of putative PDGs in microbial genomes and environmental metagenomes.

## Database Files

| File | Description |
|---|---|
| `PDG_reference_proteins_527.faa` | FASTA file containing 527 non-redundant reference protein sequences. |
| `PDG_gene_annotations_286.xlsx` | Annotation table containing 286 gene records with plastic substrate and functional classification information. |

The annotation table includes three columns:

- **ID_raw:** Original gene or protein identifier.
- **Plastic_sub:** Associated plastic substrate type(s).
- **Big_class:** Broad functional classification of the plastic-associated gene.

The `Big_class` field contains four categories: `Synthetic_Heterochain`, `Synthetic_Homochain`, `Natural_PHA`, and `Unannotated_or_Other`.

The annotation table and reference FASTA have different identifier coverage and should not be assumed to have a one-to-one correspondence.

## Database Construction

Reference protein sequences were collected from PlasticDB, PAZy, and PDG_DB and integrated into a combined sequence collection.

Redundant sequences were clustered using a 95% amino acid sequence identity threshold, resulting in 527 representative sequences.

These sequences constitute the reference dataset provided in this repository.

## Usage

The reference protein sequences can be used to construct a searchable database with [DIAMOND](https://github.com/bbuchfink/diamond).

### 1. Build the DIAMOND database

```bash
diamond makedb \
  --in PDG_reference_proteins_527.faa \
  --db PDG_reference
```

### 2. Search query proteins against the database

```bash
diamond blastp \
  --query query_proteins.faa \
  --db PDG_reference.dmnd \
  --out PDG_hits.tsv \
  --outfmt 6 \
  --evalue 1e-5 \
  --id 50 \
  --query-cover 70 \
  --threads 8
```

The example applies the following screening thresholds:

| Parameter | Threshold |
|---|---|
| E-value | ≤ 1e-5 |
| Amino acid sequence identity | ≥ 50% |
| Query coverage | ≥ 70% |

These thresholds are intended for identifying candidate homologs of reference PDGs. Sequence similarity alone does not demonstrate experimentally verified plastic-degrading activity.

## Applications

The database can support:

- Identification of putative plastic-degrading genes in metagenomic datasets.
- Comparative analysis of PDG diversity across microbial communities and environmental habitats.
- Investigation of potential plastic-degradation functions in microbial genomes and metagenome-assembled genomes (MAGs).

## References

The reference collection was compiled using information from the following databases. Users should acknowledge the relevant original resources when using these sequences.

1. Gambarini, V., et al. (2022). PlasticDB: a database of microorganisms and proteins linked to plastic biodegradation. *Database*, 2022, baac008. https://doi.org/10.1093/database/baac008

2. Buchholz, P. C. F., et al. (2022). Plastics degradation by hydrolytic enzymes: The plastics-active enzymes database—PAZy. *Proteins: Structure, Function, and Bioinformatics*, 90, 1443–1456. https://doi.org/10.1002/prot.26325

3. Zhang, J., et al. (2026). PDG_DB: A comprehensive database unveils environmental distribution patterns of plastic-degrading genes via large-scale multi-omic data analysis. *Water Research*, 296, 125619. https://doi.org/10.1016/j.watres.2026.125619

## Contact

For questions, suggestions, or issues related to this database, please open an issue in this GitHub repository.

**Repository:** https://github.com/qyxmicro/Plastic-Degrading-Gene-Database
