# Genotype-Privacy-PRS-Benchmark
We ran polygenic risk score (PRS) calculations using 1000 Genome Project's Omni Microarray genotype data on a population of 2318 individuals and show the ancestry and PRS results here.
The calculation and related data preprocessing are done by the Michigan Imputation Server.

# Data Sources

1. [1000 Genome Genotype Data](https://www.internationalgenome.org/category/omni/)
    1. To download, run
       ```{bash}
       curl -O ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/supporting/hd_genotype_chip/ALL.chip.omni_broad_sanger_combined.20140818.snps.genotypes.vcf.gz
       ```
2. [1000 Genome Phase 3 v5 Reference Panel](https://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/) for running imputation & PRS calculations

# Data Preparation

After downloading the Omni genotype data hosted by 1000 Genome, run the following to dissect the whole genome VCF file into ones arranged by chromosomes:

```{bash}
for chr in {1..22}; do
    bcftools view -r ${chr} -Oz -o chr${chr}.vcf.gz \
    ALL.chip.omni_broad_sanger_combined.20140818.snps.genotypes.vcf.gz
done
```

# Running PRS Calculation

Upload the prepared per-chromosome `vcf.gz` files to the Michigan Imputation Server and select configurations accordingly (see below).

- Genotype data is prepared according to genome build **GRCh37/hg19**.
- Use **1000G Phase 3 v5** as reference panel for the job.
- Feel free to adjust **rsq** filter and **trait** category for polygenic scoring.
  - For the benchmark results shown in this repo, trait category is **Cancer**.

<img width="870" height="938" alt="Screenshot 2025-11-08 at 7 00 04 PM" src="https://github.com/user-attachments/assets/9d02674a-0ce9-4b15-8613-fc79b97c065c" />
