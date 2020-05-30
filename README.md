A Multidimensional Precision Medicine Approach for Autism Subtype Identification
--------------------------------------------------------------------------------

The promise of precision medicine lies in data diversity. More than the sheer size of biomedical data, it is the layering of multiple data modalities, offering complementary perspectives, that is thought to enable the identification of coherent patient subgroups with shared pathophysiology. Here we use autism spectrum disorder (ASD) to test this notion. By combining healthcare claims, electronic health records, familial whole-exome sequences, and neurodevelopmental gene expression patterns, we identified a subgroup of patients with dyslipidemia-associated ASD.

For more details, see the accompanying paper (link available soon).

Installation
------------

First, clone this repository and enter the directory by running:

    git clone https://github.com/yuanluo/autism_precision_medicine
    cd autism_precision_medicine
    
The repository is implemented in R 3.x and Python 2.7.x, and depends on the following packages:
  - reshape2
  - ggplot2
  - scales
  - igraph
  - GenomicRanges
  - VariantAnnotation
  - grid
  - pheatmap
  - hash
  - genefilter
  - rtracklayer
  - MASS
  - foreach
  - doMC
    
Usage
-----
### Setting Paths

Paths can be set in the configuration file giConfig.R. In that file, the major paths are: `dn.ndar` that contains intermediate files for NDAR (https://ndar.nih.gov), e.g., variant annotations, compiled genotypes etc; `dn.base` that contains base data, e.g., from BrainSpan (http://developinghumanbrain.org). We are not authorized to share those datasets, but they are directly available from the above links.

### Running Code

Much of our code is designed to run a High Performance Computing (HPC) cluster, due to the highly parallel nature of the major processing steps. Following are examples of such steps. We have included examples for popular parallel job scheduling systems including LSF and Slurm.

#### Parallel Computation of Correlation among Exon Pairs from BrainSpan RNA-Seq data

Run the script `pcor.sh`, this script submit jobs to LSF scheduling system. This code is generated by the Python script `import pscripts as ps` function `ps.expr_cor_parallel_script()` that utilizes `pcor_tmp.lsf` and `pcor_tmp.sh`.

#### Printing Exon Clusters

To print the exons contained in the exon clusters

    source('printAllECs.R')
    source('printl2AllECs.R')

#### Cross Tabulating the Variant Annotation Files

Run the script `pCrossTabVA.sh`, this script submit jobs to LSF scheduling system.

#### Reading Genotype Out of Cross Tabulated Variant Annotations

Run the script `read_genotype_discordant.sh`, this script submit jobs to Slurm scheduling system. This code is generated by the Python script `import pscripts as ps` function `ps.read_genotype_discordant_slm_parallel_script()` that utilizes `read_genotype_discordant_tmp.lsf` and `read_genotype_discordant_tmp.sh`.

#### Generating the Lookup Table for SSC Family:

    source('sscFamLookupTabBatch.R')

#### Generating the Lookup table for Multiplex Family:

    source('ndarMultiplexSubjLookupTabBatch.R')

#### Generating Deleterious Variants Table

These tables contain deleterious variants (defined in `delMuts.R`) from subjects of different cohorts. To obtain them, run

    source('discordantDelvar.R')
    source('multiplexDelvar.R')
    source('discordantl2Delvar.R')
    source('multiplexl2Delvar.R')

#### Plotting the Exon Progression:

There are 3 modes of plotting: 1. line plotting with error bars; 2. LOWESS smoothed plotting; 3. Developmentally phased plotting. To obtain them, run 

    source('ecTempProgressLOWESS.R')
    source('ecTempProgressPhase.R')
    source('ecTempProgress.R')
    source('ecl2TempProgressLOWESS.R')
    source('ecl2TempProgressPhase.R')
    source('ecl2TempProgress.R')



    
    
