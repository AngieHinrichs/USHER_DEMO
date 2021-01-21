# **UShER DEMO**
This repository contains examples input files to demonstrate "real time" phylogenetics using the [web interface](https://genome-test.gi.ucsc.edu/cgi-bin/hgPhyloPlace) to [**U**ltrafast **S**ample placement on **E**xisting t**R**ees (UShER)](https://github.com/yatisht/usher) to place user uploaded sequences onto a global and nearly comprehensive phylogeny of the available full length, high coverage, SARS-COV-2 sequences. You can read about this approach in [our manuscript](https://www.biorxiv.org/content/10.1101/2020.09.26.314971v1). As demonstrated below (see examples), UShER can be used (1) to rapidly determine relationships among user samples and identify closely related samples already present in the globaly phylogeny, (2) and as a rapid sequence quality control tool to determine if user uploaded samples are high quality sequences. 

## **Approach**
UShER uses maximum parsimony to place new samples onto an existing global reference phylogeny. This is accomplished by searching every branch on a fixed reference phylogeny for the placement that requires the fewest added mutations. Note that SARS-CoV-2 is a relatively slowly evolving virus with few informative mutations imposing a degree of uncertainty in phylogenetic inference regardless of the underlying method. Sample placements should be interpreted cautiously. 

## **Input**
The web interface accepts either a fasta sequence or Variant Call Format (VCF) file. If submitting a VCF, please check that [NC_045512.2](https://www.ncbi.nlm.nih.gov/nuccore/NC_045512) is used as the reference against which variants are called. Please note that UShER is designed to work with reasonably complete sequences. If a sample is not nearly full length and high coverage, sample placements may be unreliable (see also below). Our tools will check this when a user uploads fasta sequences, but VCF files do not necessarily encode that information. To help UShER we recommend that users produce VCF's with genotype information output for all sites including noting when data is missing. We are currently in the process of thoroughly investigating the effects of missing data and ambiguous genotypes. 

## **Data Privacy** ## 
We do not store user uploaded sequences and your results will not be available to other users (unless you choose to share them).

## **Output**
The UShER suite of tools outputs the mutation path (on the tree) and additional mutations unique to the uploaded sample as well as the number of equally parsimonious placements on the tree. UShER also reports the most closely related sample in the global tree as well as the lineage for that samples based on [Pangolin](https://github.com/cov-lineages/pangolin). When user uploaded samples are each others' closest relatives, the program will construct subtrees specific to user uploaded sequences to enable visualization of relationships. UShER produces subtrees including the 50 most closely related sequences as json-formatted trees  (viewable in [Nextstrain](https://nextstrain.org/) or [auspice.us](https://auspice.us/)), which allows users to [annotate the tree using custom metadata](https://docs.nextstrain.org/projects/auspice/en/stable/advanced-functionality/drag-drop-csv-tsv.html). Additionally, UShER outputs these trees and their mutations as custom "tracks" in the [UCSC SARS-CoV-2 Genome Browser](https://genome.ucsc.edu/cgi-bin/hgTracks?db=wuhCor1&position=NC_045512v2) to enable co-visualization of phylogenetic relationships and genetic variation. Users can download the resulting global phylogeny after UShER places their samples. 

## **Example 1: A typical use case**
The first example file contains five samples in fasta format. After downloading [example_files.zip](example_files.zip?raw=true), unzip it and upload the file example1_typical_use_case.fasta to the UShER [web interface](https://genome-test.gi.ucsc.edu/cgi-bin/hgPhyloPlace) by selecting the file from the "Choose File" prompt and then pushing the "Upload" button. You should quickly get output as described above. Here, we see that there are two subtrees. The first contains three of the users' samples and the second contains two. Please select the "view in Nextstrain" button on the far right of results table to examine the first subtree. In this case, we see that the samples are each other's closest relatives, consistent with recent transmission among the sampled hosts. The same result is apparent when viewing the second subtree as well. However, since these sequences are quite genetically distant, a user could surmise that there are two independent transmission chains among the five sequences. 

## **Example 2: Sequence Quality Control**
UShER can also be a quality control tool. Download and unzip [example_files.zip](example_files.zip?raw=true) if you haven't already, and upload the file example2_problematic_sequences.fasta as in the example above, you'll see that the output table is colored red in many cells indicating that both sample placements may be unreliable. For the first sequence, the parsimony score cell is red and reads 13. This indicates the sequence has 32 private mutations---that's a lot!---and suggests that this is a low quality sequence that contains many errors. The second row of the table contains output for the second sample. In this case, we see that there are 40 equally parsimonious placements on the tree. This is probably due to the presence of 3 mixed (or ambiguous) nucleotide positions in the sample. Neither sample placement should be considered reliable and both are likely low quality sequences. 
