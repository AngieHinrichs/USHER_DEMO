# **UShER DEMO**
This repository contains examples input files to demonstrate "real time" phylogenetics using the UCSC SARS-COV-2 genome browser. This function is available within the [genome browser](www.xxx.com). Specifically, we developed and integrated a program, **U**ltrafast **S**ample placement on **E**xisting t**R**ees (UShER, available from [Yatish Turakhia's strain phylogenetics package](https://github.com/yatisht/strain_phylogenetics)) to place user uploaded sequences onto a global phylogeny of more than 40,000 full length, high coverage, SARS-COV-2 sequences. This approach will be thouroughly validated and described in more detail in a forthcoming manuscript. 

## **Approach**
UShER uses maximum parsimony to place new samples onto a fixed global reference phylogeny. This is accmoplished by searching every branch on a fixed reference phylogeny for the maximum likelihood placement of each sample. Please note that UShER has been optimized for speed (each sample is placed in 10ths of a second), but methods such as maximum likelihood might improve phylogenetic inference in some cases. Additionally, SARS-CoV-2 is a relatively slowly evolving virus with few  informative mutations imposing a degree of uncertainty in phylogenetic inference regardless of the underlying method. Sample placements should be interpreted cautiously. 

## **Input**
The UCSC Genome Browser portal accepts either a fasta sequence or VCF. If submitting a vcf, please check that NC_045512v2 is used as the reference against which variants are called. Please note that UShER is designed to work with reasonably complete sequences. If a sample is not nearly full length and high coverage, sample placements may be unreliable. Our tools will check this when a user uploads fasta sequences, but vcf files do not necessarily encode that information. To help UShER we recommend that users produce vcf's with genotype information output for all sites. We are currently in the process of thouroughly investigating the effects of missing data and ambiguous genotypes. 

Please note that we do not store user uploaded samples and your results will not be available to other users (unless you choose to share them). 

## **Output**
The UShER suite of tools outputs the mutation path (on the tree) and additional mutations unique to the uploaded sample as well as the number of equally parsimonious placements on the tree. UShER also reports the most closely related sample in the global tree as well as the lineage for that samples based on [Pangolin](https://github.com/cov-lineages/pangolin). Typically the user sample would be of the same lineage, but we do not confirm this by separately running Pangolin. Furthemore, when user uploaded samples are each others' closest relatives, the program will construct subtrees specific to user uploaded sequences to enable visualization of relationships. UShER finally produces Subtrees including the 50 most closely related sequences as custom Genome Brower "Tracks" to enable co-visualization of phylogenetic relationships and genetic variation. All samples that are not distinguished by a mutation are collapsed into a single node to facilitate compact viewing. 

Users can download the resulting global phylogeny after UShER places their samples. However, we cannot distribute the [GISAID](https://www.gisaid.org/) database (either sequences or bulk metadata). To obtain those data, please set up a user account with [GISAID](https://www.gisaid.org/). 

## **Example 1: Two unrelated samples**
The first example file contains two samples in vcf format. After downloading this file, upload it to the UShER suite of tools within the [UCSC SARS-COV-2 Genome Browser](www.XXX.com) by selecting the file from the "Choose File" prompt and then pushing the "Upload" button. You should quickly get output as described above. Note that here, because these two samples are reasonably distantly related, their placements generate two separate tracks for viewing subtrees. 

## **Example 2: A set of related samples**
In some cases a user may upload samples from a single "transmission chain". UShER has been designed to infer the relationships and display the resulting subtree for these cases. Please upload the second example vcf file as for example 1, above. You will see simlar output as above. Here, the ten related sequences are grouped, and for each we see the mutation path from the root to each sample. If you select the "view tree in genome browser" button at the bottom of the page, it will display these 10 samples and the 40 most closely related samples that are already in the database. 

## **Example 3: One low-quality sequence** 
UShER can also be a quality control tool. If you upload example3.vcf as in the two example above, you'll see that the output indicates the sample has many mutations unique to its terminal branch on the tree. In particular, positions 3327-3332 have a large excess of mutations unique to this sample compared to its closest relatives. While this cannot definitively identify this a low quality sequence, it certainly bears careful inspection. In fact, it is possible to upload a bam file for each sample to enable visual inspection of the raw read data as well. For an example of how to do this, please see XXX. 

