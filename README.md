# openfold3-training-data-RODA
Documentation for the openfold3 training dataset hosted on AWS Registry of Open Data
//TODO: add total sizes for datasets

# Introduction

This repositroy contains documentation on the open-access data used to train Openfold3, open source biomolecular structure prediction model. This dataset represents the culmination of millions of cpu and gpu hours, and is the largest open source databse of paired multiple sequence alignment and 3D structures. There N keys datasets that we descibe below. For each dataset, we provided a detailed description of how the data was generated and preprocessed in [methods.md]() file in this repo.

# Datasets

The RODA bucket contains a separate prefix for each subdataset. 
```
<bucket-name>/
  - README.md
  - PDB
  - PDB-disorderd
  - long-monomer-distillation-set
  - short-monomer-distillation-set
```

Each dataset is available in at least 2 forms, a "raw" version, containing compressed MSA/ structure files, and a "preprocessed" version, which contains npz arrays that are suitable for training Openfold3.

## PDB

This folder contains MSAs and structures from the protein data bank(PDB). For each unique sequence in the PDB, we generate MSAs following the [OF3 MSA protocol]() available at `pdb/raw/msas/{pdb_chain_id}`. As the same unique sequence may be used across many PDB structures, we provide a mapping between all PDB chains and the representatives that have alignmetns at `pdb/raw/msas/representative_mapping.csv`

We provide the snapshot of pdb structures in CIF format at `pdb/raw/structures/{pdb_id}/{pdb_id}.cif` 



We provide preprocessed data suitable for training with the following directory structure:
```
pdb/preprocessed/
  - structures/{pdb_id}/{pdb_id}.npz
  - msas/{pdb_id}/{pdb_id}.npz
  - template_alignments/{pdb_id}/{pdb_id}.npz
  - template_structures/{pdb_id}/{pdb_id}.npz
```

Please see the Openfold3 [documentation]() for how to integrate this into training.

Finally, JSON metadata files corresponding to training, validation, and evaluation sets are available at `pdb/{train/val/eval}.json`

## PDB-disorderd

The PDB-disorderd dataset is an auxiliary trainind dataset for Openfold3. It contains XXX PDB structures predicted by Alphafold Multimer. Raw CIF files can be found at `pdb-disordered/raw/structure/{pdb_id}/{pdb_id}.cif` and preprocessed npz files at `pdb-disordered/preprocessed/{pdb_id}/{pdb_id}.npz`

## Long monomer distilation set

This dataset contains MSAs and predicted structure for 13 million long (sequence length  >= 200 amino acids) from the MGNIFY database.
