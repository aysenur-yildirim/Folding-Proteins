# Fold-Switching Proteins
This repo contains a batch preparation pipeline to fetch sequences/structures for PDB IDs listed in FSR.xlsx, generate DSSP, align FASTA to DSSP numbering, and prepare inputs for PSIPRED and JPred.

# Workflow

PDB FASTA download

Source list: FSR.xlsx (PDB IDs + chains when applicable).

Sequences were downloaded from the RCSB Protein Data Bank at chain level and stored as:

rcsb_pdb_all_fasta_files.gz → archive of per‑entry FASTA files

rcsb_pdb_allpdbidswithchain.fasta → merged multi‑FASTA of all sequences

CIF & DSSP generation

With CIF_DSSP_Download.ipynb, CIF structures were fetched and DSSP was run for each PDB (and chain if needed).

Produced DSSP files are archived in all_dssp.zip.

FASTA ↔ DSSP alignment & H/E/C extraction

fastadsspalignment.ipynb aligns each FASTA sequence to the author residue numbering in CIF/DSSP and extracts DSSP H/E/C labels aligned to the sequence.

Resulting CSVs live in fastadsspalign_csv.zip.

PSIPRED predictions

PSIPRED results for uploaded FASTAs are aggregated in PSIPRED_ss2_zips.zip (standard .ss2 format and related files).

JPred FASTA cleanup & batch prep

FASTA headers were sanitized to satisfy JPred’s rules (A–Z/a–z/0–9/_ only).

MSE (Selenomethionine) residues were converted to M; any non‑standard characters were removed.

Sequences longer than 800 aa were automatically split into chunks (_1, _2, ...).

A batch‑ready compact‑ID multi‑FASTA was produced: jpred_batch_MSEclean_compact.fasta.

Per‑sequence FASTAs are in jpred_batch_MSEclean_compact_fastas.zip; the ID ↔ original name mapping is jpred_batch_MSEclean_name_mapping.csv.

Note: JPred results will be added to the repo as they become available.

Context / references
Inaccurate secondary structure predictions often indicate protein fold switching  (pnas.1800168115.sapp.pdf)

# Files & What They Are

FSR.xlsx → List of PDB identifiers (and chains) to be processed. Source: supplementary material of Inaccurate secondary structure predictions often indicate protein fold switching (pnas.1800168115.sapp.pdf).

rcsb_pdb_all_fasta_files.gz → Gzipped archive of per‑PDB FASTA files downloaded from RCSB.

rcsb_pdb_allpdbidswithchain.fasta → Combined multi‑FASTA of all sequences.

CIF_DSSP_Download.ipynb → Notebook to download CIFs and compute DSSP.

all_dssp.zip → Archive of all produced .dssp files.

fastadsspalignment.ipynb → Aligns FASTA to CIF/DSSP numbering and emits H/E/C per residue.

fastadsspalign_csv.zip → CSV outputs of the alignment step.

PSIPRED_ss2_zips.zip → Aggregated PSIPRED outputs (.ss2, etc.).

jpred_batch_MSEclean_compact.fasta → JPred batch‑ready multi‑FASTA with compact IDs.

jpred_batch_MSEclean_compact_fastas.zip → Per‑sequence FASTAs for JPred batch upload.

jpred_batch_MSEclean_name_mapping.csv → Compact ID ↔ original header mapping.

README.md → This documentation.
