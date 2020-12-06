# BpPan
BP pangenome
## Quality control

### Genome selection

The ~5k sequencing runs on the SRA were initialy filtered before being assembled. Runs which did not have at least 100x coverage of the genome (approximately 400Mb raw sequence data) were excluded. In a small number of cases (<20), runs were excluded that had more than 1000x coverage in order for speedy proccessing.

Fastqc was used to filter sequence samples. Samples which failed the read quality step wer excluded.


### Assembly

Samples were assembled with shovil. SAmples over 100x coverage were downsampled to 100x to speed up assembly.

Assemblies were checked for DNA from other organisms which would indicate the sample was contaminated. Contamination of this sort would create spurious variation in the pangenome. Assemblies were analysed with Kraken 2 using the 8gb abbreviated refseq database. Isolates which were able to be identified down to the species level using this abbreviated database were discarded if >5% of the K-mers came form species other than BP. If an assembly could only be identfied down to the genus level, assemblies were discarded if >5% of the K-mers came from a genus other than Bordetella.

In this way a rigorous quality control method was applied.

## Pangenome stats

### How many in core and accessory genome?

This cna be read directly from the summary stats file

### How many genes have been disrupted vs deleted?

Using the script 'Blast script denovo assemblies.R' it can be determined which genes from the pangenome have been deleted (no AA or DNA homology) or disrupted (high DNA and low AA). This requires some pre processing as each gene is blasted against each genome.

We need to generate a single fasta file containing all the assemblies and their contigs, with each seq having a unique name. This is done using the rename_and_merge_fastas.R file and the mergeing all these new files together. This is then made into a blastdb.

The Blast R script can then be used ,after some tweaking.


