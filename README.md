# pa-salmon
## pa-salmon

Using salmon to processes *P. aeruginosa* RNA-seq data

## Overview

1. Create transcriptome index
    These are reference genome specific and can be made in decoy-unaware or
    decoy-aware modes
    examples: salmon_ti.script, salmon_ti_decoy.script

2. Load fastq files to directories accessible on discovery
    * keep all fastq files that correspond to a sample (eg paired) in sub-directories
    * dartfs storage is accessible by discovery but larger than user home dirs
    but is usually specific to a lab
    * global scratch can also be used (files last 30 days)
    * examples: /dartfs-hpc/rc/lab/H/HoganD or /dartfs-hpc/scratch/

3. Map samples to t-index
    * Use the salmon quant command for fast mapping
    parameters used in this project were chosen for *P. aeruginosa*
    and may be bacteria-specific.
    * Run samples in parallel via job arrays.
    * examples: salmon_metals_spu.scipt, salmon_metals_spu_decoy.script

4. Collect salmon output (quant.fs files) into count table
    * Since the salmon calls save all outputs to files named quant.fs in different
    directories, and
    * salmon also uses cDNA gene identifiers,
    * collect them all as columns
    in a table with column names as sample names and rownames as gene names
    * example: spu_collect.script
