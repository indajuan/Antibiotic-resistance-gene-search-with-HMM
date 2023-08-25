# Antibiotic resistance gene search with HMM
## Implementation of fARGene and fARGene's HMM

[fARGene](https://github.com/fannyhb/fargene/tree/master) has several hidden Markov models (HMM) to identify fragments of antibiotic resistance genes (ARG) from metagenomes (short-fragment HMM), to do spades assembly on these fragments, and to evaluate if any contig has potential to have an ARG (full-sized HMM).

In this repo, we implement the search for ARGs using fARGEne and Snakemake for the workflow. There is also the option to do the assembly and run on an external list of reads to do the assembly with and run the full-sized HMM on them. Notice that the options for fARGene are fixed and it would require modifications in the rules to change them.

### Preparation
- Install both conda environments with the configuration files `main_run.yml` and `fargene.yml`

### Running fARGene
- Write in the configuration file `config_fargene.yaml` the information necessary:
..* `working_folder` the specification for the working working directory, example `/home/user/run_fargene/`
..* `fastq_folder` the directory where the paired-end fastq files are located, example `/home/user/run_fargene/FASTQ/`. The files should be stored in this format `/home/user/run_fargene/FASTQ/ACCESSION_NUMBER/ACCESSION_NUMBER_1_QC.fastq`
..* the output directory, example `/home/user/run_fargene/output/`
..* the directory where the pre-trained HMM from fARGene are saved in the conda environment, example `/home/user/fargene/fargene_analysis/models/`
..* the number of threads used
- Start the `main_run` environment, `conda activate main_run`
- Run the analysis, `snakemake -s Snake_fargene -r -p -j <number of cores> --use-conda`
- The output is 4 folders inside the output directory:
..* `translated` contains the translated reads to the six frames
..* `reads`are the short fragment reads detected as potential ARG that are used by fARGene for the assembly of contigs
...* `genes`are the putative ARG found by fARGene
..* `analysis` is fARGene's own output


### Extracting fastq sequences from a file containig a list of reads, run the assembly, and run fARGene full-sized HMM models on the contigs
- Write in the configuration file `config_hmm_all.yaml` the information necessary:
..* working_folder, example `/storage/user/`
..* reads_folder: the folder where the files containing the list of reads is located, example `/storage/user/metagenome_short/data/independent_reads/`. The files should have the following format `/storage/user/metagenome_short/data/independent_reads/ACCESSION_NUMBER.txt`
..* output_folder: `/storage/user/independent_reads_output/`
..* model_folder: the directory where the pre-trained HMM from fARGene are saved in the conda environment, example `/home/user/fargene/fargene_analysis/models/`
..* spades_folder, spades is saved in fargene's conda environtment, example `/home/user/.conda/envs/fargene/bin/spades.py`
- Start the `main_run` conda environment, `conda activate main_run`
- Run the analysis, `snakemake -s Snake_hmm_all -r -p -j <number of cores> --use-conda`
- The output is 
