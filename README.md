# Antibiotic resistance gene search with HMM
## Implementation of fARGene and fARGene's HMM

[fARGene](https://github.com/fannyhb/fargene/tree/master) has several hidden Markov models (HMM) to identify fragments of antibiotic resistance genes (ARG) from metagenomes (short-fragment HMM), to do spades assembly on these fragments, and to evaluate if any contig has potential to have an ARG (full-sized HMM).

In this repo, we implement the search for ARGs using fARGEne and Snakemake for the workflow. There is also the option to do the assembly and run on an external list of reads to do the assembly with and run the full-sized HMM on them. Notice that the options for fARGene are fixed and it would require modifications in the rules to change them.

 
