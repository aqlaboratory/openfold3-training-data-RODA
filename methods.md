
# Core PDB dataset

All sequences for chains in the pdb on XXX and deduplicated. For each unique protein sequence in this set, we generated 4 sets of MSAs: 
alignments to uniprot, uniref90, and mgnify with jackhmmer, and alignments to the ColabFold database with hhblits.
For RNA chains we generated MSAs with nhmmer, searching against rnacentral, rfam, and NCBI nucleotide collection
Next, we performed a template search using the unire90 MSA against structures in the PDB using the `hmmsearch`, and then selecting hits that meet AF3 template criteria outlined in the AF3 SI


# Disordered PDB dataset 

Utilizing the MSAs from the previous step, we predicted structures using the AF2.3-Multimer for all multi-protein complexes in the PDB. Each prediction was made with 5 seeds and with templates, with the best structure selected as the final prediction used for training

# long and short monomer datasets

The mgnify database was downloaded an clustered to XXX similarity, yielding 41M representative sequences, 13M long monomer( sequence length >= 200) and 28M short monomer. 
For each sequence, we generate initial alignments searching uniref100 with jackhmmer, and ColabFoldDB with hhblits. These alignmetns are then concatenated and then 
diversity filtered following the procedure outlined in [Miridita et al](). This filtered MSA was used for template search using hhblits with a max date cutoff of 2021-09-30. 
Next, we predicted structures using openfold with deepmind weights. We predicted one structure with templates, and one strucure without and select the predicted structure with the highest average pLDDT to 
use for training. Notably, we do not impose any global pLDDT filter. 
