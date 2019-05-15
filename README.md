# BGCs_in_rare_metagenomic_DNA

## Distance_v1.0.ipynb
#### Compares domain networks to references and to other networks. 
---
For each soil sample, sequenced amplicons forming networks of 3 or more domains are translated into protein sequences and compared to the protein sequence of BGCs in databases (MIBiG and AntismashDB) or to predicted domain networks from other soil samples using blastp. If at least 50% of the domains in a network matched independent positions on proteins from a BGC in a database or independent domains in another domain network, a similarity score is calculated for the pair. The similarity score is defined as the median pairwise identity between domains and reference BGC proteins, taking into account non-matching domains and the best combination of matching domains. 
This script was used to calculate similarity scores used in Fig. 2a, Fig. 3a, and Supplementary Table 4.
Fig. 3a was generated using chord2.js, a d3.js plugin developed by G. Gherdovich (https://bitbucket.org/gghh/chord2/). 




## HIseq abundance-v1.0.ipynb
#### Estimates the abundance of metagenomic inserts of interest by calculating the associated depth of coverage obtained with a shallow untargetted sequencing run of the whole library.
---
Duplicate reads are removed using BBtools’s clumpify.sh and reads originating from pWEB_TNC vector or residual E. coli chromosomal DNA are detected and filtered out by aligning them using bbmap.sh. The remaining short reads are aligned on all contigs of interest (recovered library clones encoding BGCs or random metagenomic inserts obtained from long reads assembly) using bbmap.sh. For each contig of interest, aligned reads are extracted with SAMtools, and coverage for each base pair is obtained using bedtools’ genomeCoverageBed in order to calculate a mean coverage per base pair (depth of coverage). Based on the depth of coverage obtained by sequencing 15.5 Gbp, the abundance of the genomes of origin of each contig is extrapolated and expressed as the sequencing output required to obtain a depth of coverage of 20 (required output = 15.5/Obtained coverage * 20). 
This script was used to generate the abundance histogram depicted in Fig. 2d.




## PacBio_processing_v1.0.ipynb
#### Performs de-novo assembly of metagenomic inserts from PacBio reads.
---
Reads are aligned on 2000bp of pWEB_TNC vector sequence and the E. coli chromosome using minimap2 with default parameters. Non-aligned reads are kept in full while aligned reads are processed with Jvarkit’s SamExtractClip to recover only their non-aligned regions (i.e. metagenomic inserts regions clipped by minimap2). Following vector and residual E. coli DNA filtering, the reads are assembled using Flye. Resulting contigs longer than 25kb harboring vector edges (end to end inserts) are used in downstream analysis (predicted domain detection in Fig. 2c, Supplementary Table 4 and abundance estimation in Fig. 2d)

