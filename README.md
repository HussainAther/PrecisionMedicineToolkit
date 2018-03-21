# PrecisionMedicineToolkit

![FHIR-compliant output](https://i.imgur.com/tm9iZWM.png)

# Introduction

* EMR data must be easily accessible for experts from clinical informatics and bioinformatics to use.
* Existing software annotatte variants and identify SNPs associated with disease, but no software integrates findings from variant annotation in a FHIR-compliant format.
* A FHIR-compliant output would be useful for scientists for extraction of variant information, RESTful API, and administrative actions.
* This toolkit addresses the needs to make this information easily accessible by creating a FHIR-compliant output that would be easily accessible by different types of bioinformaticians.

# What is this
This toolkit creates a FHIR-compliant JSON file from an input EMR file after extracting relevant biological information from databases. It runs the contents of the EMR file through various databases and collects information from them. PrecisionMedicineToolkit uses various steps for extracting genomic information.

![Workflow](/images/pipeline.png)

The workflow shows the steps and databases used in creating a FHIR-compliant JSON format.

![ANNOVAR output](https://i.imgur.com/jliJAzN.png)

ANNOVAR can compare variants to existing variant databases and annotate the variant records with any database values it retrieves. For example, it can note where relative to a known gene a variant falls (eg. if it is exonic, intergenic, etc.) and which genes it affects. It can compare a variant's position to regional annotations such as conserved or DNAse hypersensitive regions. Furthermore, it can also check specific annotation or scoring databases to see if a variant is present, such as dbSNP, PolyPhen, or 1000 genomes. Although it's developed for use with the human genome (defaulting to build hg18, though newer builds can be specified), genomes and databases for other species or samples may be used as well. Annovar exists as a suite of Perl scripts and supplementary data files, and thus can in theory be run on any system with a working perl interpreter. ANNOVAR annotates genetic variants detected from diverse genomes (including human genome hg18, hg19, hg38, as well as mouse, worm, fly, yeast and many others).

GWAS is a technique for determining genetic loci associated with common disease or traits using large groups of various across genomes. PrecisionMedicineToolkit uses the NHGRI GWAS catalog to annotate the input variants.

![Sample variant copy identified](https://i.imgur.com/U0FlhJe.png)


# How to use it
`./precisionmed_wrapper.sh -i inputjsonfile.txt [-o outputDirectory]`

  **-i inputFile** JSON input file.

  **-o outDir**    Specify the directory for output - default is /home/ubuntu/PrecisionMedicineToolkit/output/json.

  This script runs a combination of bash and Python scripts to produce
  ResearchStudy JSON files for GWAS results in the output directory.

# Requirements
SnpEff (http://snpeff.sourceforge.net/index.html#)

ANNOVAR (http://annovar.openbioinformatics.org/en/latest/)

GWAS catalog, located in /data (https://www.ebi.ac.uk/gwas/docs/about)

# Future Directions
* Modifying to accept multiple JSON variant files
* Adding annotation JSON files with relevant information from SnpEff and Annovar
* Integrate the following tools:
  - SRA Toolkit (https://ncbi.github.io/sra-tools/install_config.html)
  - TOPMed (Bravo API https://bravo.sph.umich.edu/freeze5/hg38/help)
* Integrating with a major EHR software company (such as EPIC)
* Expose toolkit to a web interface
* Validata JSON before processing
* Create docker component of the pipeline

# Authors
Halé Kpetigo (hale.kpetigo@gmail.com)

Syed Hussain Ather (shussainather@gmail.com)

Blythe Hospelhorn (blythe.hospelhorn@gmail.com)

Luli Zou (luli.zou@gmail.com)
