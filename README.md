# Singularity recipes for pangenome reconstruction software

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/2730)

[Singularity](https://www.sylabs.io/docs/) recipes for building pangenome software containers.

## Getting a pre-built container

If you would like a pre-built version of any of the containers you can pull it down from [Singularity Hub](https://www.singularity-hub.org/collections/2730/usage)
like so

```sh
tool="roary"
singularity pull --name "$tool".sif shub://iferres/Singularity_recipes:"$tool"
```

## Running containers

All software can be run by calling the images (`.sif`) directly from the command line (you will have to have Singularity installed), as they are executable:
```sh
./roary.sif -h

## Please cite Roary if you use any of the results it produces:
##     Andrew J. Page, Carla A. Cummins, Martin Hunt, Vanessa K. Wong, Sandra Reuter, Matthew T. G. Holden, Maria Fookes, Daniel Falush, Jacqueline A. Keane, Julian Parkhill,
## 	"Roary: Rapid large-scale prokaryote pan genome analysis", Bioinformatics, 2015 Nov 15;31(22):3691-3693
##     doi: http://doi.org/10.1093/bioinformatics/btv421
## 	Pubmed: 26198102
## 
## Usage:   roary [options] *.gff
## 
## Options: -p INT    number of threads [1]
##          -o STR    clusters output filename [clustered_proteins]
##          -f STR    output directory [.]
##          -e        create a multiFASTA alignment of core genes using PRANK
##          -n        fast core gene alignment with MAFFT, use with -e
##          -i        minimum percentage identity for blastp [95]
##          -cd FLOAT percentage of isolates a gene must be in to be core [99]
##          -qc       generate QC report with Kraken
##          -k STR    path to Kraken database for QC, use with -qc
##          -a        check dependancies and print versions
##          -b STR    blastp executable [blastp]
##          -c STR    mcl executable [mcl]
##          -d STR    mcxdeblast executable [mcxdeblast]
##          -g INT    maximum number of clusters [50000]
##          -m STR    makeblastdb executable [makeblastdb]
##          -r        create R plots, requires R and ggplot2
##          -s        dont split paralogs
##          -t INT    translation table [11]
##          -ap       allow paralogs in core alignment
##          -z        dont delete intermediate files
##          -v        verbose output to STDOUT
##          -w        print version and exit
##          -y        add gene inference information to spreadsheet, doesnt work with -e
##          -iv STR   Change the MCL inflation value [1.5]
##          -h        this help message
## 
## Example: Quickly generate a core gene alignment using 8 threads
##          roary -e --mafft -p 8 *.gff
## 
## For further info see: http://sanger-pathogens.github.io/Roary/
## 
```

In that way you will be running the main program, but bear in mind that some of the software also include helper scripts that you can also use, but you will have to use `shell` or `exec` singularity's sub commands in order to have access to them. 
```sh
singularity exec roary.sif roary-query_pan_genome -h

## Usage: query_pan_genome [options] *.gff
## Perform set operations on the pan genome to see the gene differences between groups of isolates.
## 
## Options: -g STR    groups filename [clustered_proteins]
##          -a STR    action (union/intersection/complement/gene_multifasta/difference) [union]
##          -c FLOAT  percentage of isolates a gene must be in to be core [99]
##          -o STR    output filename [pan_genome_results]
##          -n STR    comma separated list of gene names for use with gene_multifasta action
##          -i STR    comma separated list of filenames, comparison set one
##          -t STR    comma separated list of filenames, comparison set two
##          -v        verbose output to STDOUT
##          -h        this help message
##  
## Examples: 
## Union of genes found in isolates
##          query_pan_genome -a union *.gff
##          
## Intersection of genes found in isolates (core genes)
##          query_pan_genome -a intersection *.gff
##          
## Complement of genes found in isolates (accessory genes)
##          query_pan_genome -a complement *.gff
## 
## Extract the sequence of each gene listed and create multi-FASTA files
##          query_pan_genome -a gene_multifasta -n gryA,mecA,abc *.gff
## 
## Gene differences between sets of isolates
##          query_pan_genome -a difference --input_set_one 1.gff,2.gff --input_set_two 3.gff,4.gff,5.gff
## 
## For further info see: http://sanger-pathogens.github.io/Roary/
## 
```

Please, refer to [Singularity](https://www.sylabs.io/docs/) manual pages for more information.



