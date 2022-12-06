# MIP 280A4 Final Project 2022
This report is catorgerizingand identifiying a virus sequence from a female Aedes aegypti originially from Guerrero, Mexico. This one was taken from the colony at the center for vector-borne infectious diseases (CVID)
it is written in [markdown formaty](https://www.markdownguide.org/basic-syntax/).
## step 1: copying the file to a new directory
https://github.com/twolbers/2022_MIP_280A4_final_project.git
## step 2: Quality check of seqeunce using [fastqc]
bio_tools) twolbers@thoth01:~/final_project$ fastqc Aedes_Guerrero_R1.fastq
## step 3: Trim addaptors and low quality reads using [cutadapt]
(bio_tools) twolbers@thoth01:~/final_project$ cutadapt -a AGATCGGAAGAGC -g GCTCTTCCGATCT -a AGATGTGTATAAGAGACAG -g CTGTCTCTTATACACATCT -q 30,30 --minimum-length 80 -o Aedes_Guerrero_trimmed1 \                                                > Aedes_Guerrero_R1.fastq \                                                                                             > | tee cutadapt.log
## step 4: Check quality of trimmed reads using [fastqc]
(bio_tools) twolbers@thoth01:~/final_project$ fastqc Aedes_Guerrero_trimmed1
## step 5: find and download host genome in fasta format
Began by looking at the taxonomy page on the NCBI website, found Aedes aegypti, copied the URL. Using the command below I added it to my /final_project directory.
(base) twolbers@thoth01:/home/data_for_classes/2022_MIP_280A4/final_project_datasets$ cd                                (base) twolbers@thoth01:~$ cd final_project                                                                             (base) twolbers@thoth01:~/final_project$ curl -OL https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/002/204/515/GCF_002204515.2_AaegL5.0/GCF_002204515.2_AaegL5.0_genomic.fna.gz
## step 6: Create an index for our Aedes aegypti seqeunce from NCBI using [bowtie2]
(base) twolbers@thoth01:~/final_project$ conda activate bio_tools                                                       (bio_tools) twolbers@thoth01:~/final_project$ nohup bowtie2-build GCF_002204515.2_AaegL5.0_genomic.fna.gz index

