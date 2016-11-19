# RNA_seq_Help
scripts and software used to help annotate RNA-Seq data

cd /lustre/projects/RNA_Seq_Data

mv RNA_seq_files/ /lustre/projects/RNA_Seq_Data/
>cd /lustre/projects/RNA_Seq_Data/
/lustre/projects/RNA_Seq_Data>ls
RNA_seq_files
/lustre/projects/RNA_Seq_Data>cd RNA_seq_files/
/lustre/projects/RNA_Seq_Data/RNA_seq_files>ls
WTair1_S1_R1_001.fastq  WTair3_S3_R1_001.fastq.gz  WTeth2_S7_R1_001.fastq.gz
WTair2_S2_R1_001.fastq  WTeth1_S4_R1_001.fastq.gz  WTeth3_S8_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>gunzip WTair3_S3_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>ls
WTair1_S1_R1_001.fastq  WTair3_S3_R1_001.fastq     WTeth2_S7_R1_001.fastq.gz
WTair2_S2_R1_001.fastq  WTeth1_S4_R1_001.fastq.gz  WTeth3_S8_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>gunzip WTeth1_S4_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>ls
WTair1_S1_R1_001.fastq  WTair3_S3_R1_001.fastq  WTeth2_S7_R1_001.fastq.gz
WTair2_S2_R1_001.fastq  WTeth1_S4_R1_001.fastq  WTeth3_S8_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>gunzip WTeth2_S7_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>gunzip WTeth3_S8_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>ls -l
total 25810876
-rw-r--r-- 1 callen72 users 4294934528 Sep 19 11:00 WTair1_S1_R1_001.fastq
-rw-r--r-- 1 callen72 users 4835516675 Sep 19 10:46 WTair2_S2_R1_001.fastq
-rw-r--r-- 1 callen72 users 4188371450 Sep 19 10:49 WTair3_S3_R1_001.fastq
-rw-r--r-- 1 callen72 users 4637692584 Sep 19 10:53 WTeth1_S4_R1_001.fastq
-rw-r--r-- 1 callen72 users 4147069520 Sep 19 10:56 WTeth2_S7_R1_001.fastq
-rw-r--r-- 1 callen72 users 4326615469 Sep 19 10:59 WTeth3_S8_R1_001.fastq

/lustre/projects/RNA_Seq_Data/RNA_seq_files>wget https://www.ncbi.nlm.nih.gov/genome/all/GCF_000009725.1_ASM972v1/GCF_000009725.1_ASM972v1_genomic.fna.gz” > 6803genome.fa.gz
/lustre/projects/RNA_Seq_Data/RNA_seq_files>ls
6803genome.fa.gz        WTair3_S3_R1_001.fastq  WTeth3_S8_R1_001.fastq
WTair1_S1_R1_001.fastq  WTeth1_S4_R1_001.fastq
WTair2_S2_R1_001.fastq  WTeth2_S7_R1_001.fastq

mkdir raw_data
cd raw_data
/lustre/projects/RNA_Seq_Data/raw_data>curl ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF_000009725.1_ASM972v1/GCF_000009725.1_ASM972v1_genomic.fna.gz > 6803genome.fa.gz
/lustre/projects/RNA_Seq_Data/raw_data>ls
6803genome.fa.gz

/lustre/projects/RNA_Seq_Data/raw_data>gunzip 6803genome.fa.gz
/lustre/projects/RNA_Seq_Data/raw_data>ls
6803genome.fa

/lustre/projects/RNA_Seq_Data/raw_data>curl ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF_000009725.1_ASM972v1/GCF_000009725.1_ASM972v1_genomic.gff.gz > geneannotation.gff3.fa.gz
/lustre/projects/RNA_Seq_Data/raw_data>ls
6803genome.fa  geneannotation.gff3.fa.gz

/lustre/projects/RNA_Seq_Data/raw_data>gunzip geneannotation.gff3.fa.gz
/lustre/projects/RNA_Seq_Data/raw_data>ls
6803genome.fa  geneannotation.gff3.fa

cd ../

RESTARTED EVERYTHING!!!!

/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>ls
WTair1_S1_R1_001.fastq     WTair3_S3_R1_001.fastq.gz  WTeth2_S7_R1_001.fastq.gz
WTair2_S2_R1_001.fastq.gz  WTeth1_S4_R1_001.fastq.gz  WTeth3_S8_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>curl ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF_000009725.1_ASM972v1/GCF_000009725.1_ASM972v1_genomic.fna.gz > 6803genome.fa.gz

/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>ls
6803genome.fa.gz           WTair3_S3_R1_001.fastq.gz  WTeth3_S8_R1_001.fastq.gz
WTair1_S1_R1_001.fastq     WTeth1_S4_R1_001.fastq.gz
WTair2_S2_R1_001.fastq.gz  WTeth2_S7_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>curl ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF_000009725.1_ASM972v1/GCF_000009725.1_ASM972v1_genomic.gff.gz > geneannotation.gff3.fa.gz

/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>ls
6803genome.fa.gz           WTair2_S2_R1_001.fastq.gz  WTeth2_S7_R1_001.fastq.gz
geneannotation.gff3.fa.gz  WTair3_S3_R1_001.fastq.gz  WTeth3_S8_R1_001.fastq.gz
WTair1_S1_R1_001.fastq     WTeth1_S4_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>gunzip 6803genome.fa.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>ls
6803genome.fa              WTair2_S2_R1_001.fastq.gz  WTeth2_S7_R1_001.fastq.gz
geneannotation.gff3.fa.gz  WTair3_S3_R1_001.fastq.gz  WTeth3_S8_R1_001.fastq.gz
WTair1_S1_R1_001.fastq     WTeth1_S4_R1_001.fastq.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>gunzip geneannotation.gff3.fa.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>ls
6803genome.fa           WTair2_S2_R1_001.fastq.gz  WTeth2_S7_R1_001.fastq.gz
geneannotation.gff3.fa  WTair3_S3_R1_001.fastq.gz  WTeth3_S8_R1_001.fastq.gz
WTair1_S1_R1_001.fastq  WTeth1_S4_R1_001.fastq.gz

Moved 6803genome.fa and geneannotation.gff3.fa.gz to raw_data directory
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data/raw_data>ls
6803genome.fa  geneannotation.gff3.fa.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data/raw_data>gunzip geneannotation.gff3.fa.gz
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data/raw_data>ls
6803genome.fa  geneannotation.gff3.fa

/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>fastqc -o . ./WTair2_Output/raw_data/WTair2_S2_R1_001.fastq.gz
-bash: fastqc: command not found
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>module load fastqc
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>fastqc -o . ./WTair2_Output/raw_data/WTair2_S2_R1_001.fastq.gz
Skipping './WTair2_Output/raw_data/WTair2_S2_R1_001.fastq.gz' which didn't exist, or couldn't be read
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>mkdir output
/lustre/projects/RNA_Seq_Data/RNA_Seq_Data>fastqc -o ./output ./WTair2_Output/raw_data/WTair2_S2_R1_001.fastq.gz
Skipping './WTair2_Output/raw_data/WTair2_S2_R1_001.fastq.gz' which didn't exist, or couldn't be read

RESTART AGAIN!!!!
will be following e_coli steps
/e_coli>ls
analysis  raw_data

1_fastqc       3_fastqc  5_samtools  7_abyss
2_trimmomatic  4_bwa     6_snpEff    8_quast


#$ -N trim
#$ -q medium*
#$ -cwd
/data/apps/trimmomatic/0.36/trimmomatic-0.36.jar \
SE \
-threads 8 \
-trimlog WTair2_S2_R1_001.log \
-phred33 \
../../raw_data/WTair2_S2_R1_001.fastq \
WTair2_S2_R1_001.fastq.trimmed.fq \
ILLUMINACLIP:/data/apps/trimmomatic/0.36/adapters/TruSeq3-PE.fa:2:30:10\
SLIDINGWINDOW:4:15 MINLEN:75
>& trim.output


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data>ls -lh
total 25G
-rw-r--r-- 1 callen72 users 3.9M Nov 10 09:41 6803genome.fa
-rw-r--r-- 1 callen72 users 1.4M Nov 10 09:41 geneannotation.gff3.fa
-rw-r--r-- 1 callen72 users 4.0G Sep 19 11:00 WTair1_S1_R1_001.fastq
-rw-r--r-- 1 callen72 users 4.6G Sep 19 10:46 WTair2_S2_R1_001.fastq
-rw-r--r-- 1 callen72 users 4.0G Sep 19 10:49 WTair3_S3_R1_001.fastq
-rw-r--r-- 1 callen72 users 4.4G Sep 19 10:53 WTeth1_S4_R1_001.fastq
-rw-r--r-- 1 callen72 users 3.9G Sep 19 10:56 WTeth2_S7_R1_001.fastq
-rw-r--r-- 1 callen72 users 4.1G Sep 19 10:59 WTeth3_S8_R1_001.fastq
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data>chmod 775 *.fastq
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data>ls -lh
total 25G
-rw-r--r-- 1 callen72 users 3.9M Nov 10 09:41 6803genome.fa
-rw-r--r-- 1 callen72 users 1.4M Nov 10 09:41 geneannotation.gff3.fa
-rwxrwxr-x 1 callen72 users 4.0G Sep 19 11:00 WTair1_S1_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.6G Sep 19 10:46 WTair2_S2_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.0G Sep 19 10:49 WTair3_S3_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.4G Sep 19 10:53 WTeth1_S4_R1_001.fastq
-rwxrwxr-x 1 callen72 users 3.9G Sep 19 10:56 WTeth2_S7_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.1G Sep 19 10:59 WTeth3_S8_R1_001.fastq
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data>chmod 775 *.fa
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data>ls -lh
total 25G
-rwxrwxr-x 1 callen72 users 3.9M Nov 10 09:41 6803genome.fa
-rwxrwxr-x 1 callen72 users 1.4M Nov 10 09:41 geneannotation.gff3.fa
-rwxrwxr-x 1 callen72 users 4.0G Sep 19 11:00 WTair1_S1_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.6G Sep 19 10:46 WTair2_S2_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.0G Sep 19 10:49 WTair3_S3_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.4G Sep 19 10:53 WTeth1_S4_R1_001.fastq
-rwxrwxr-x 1 callen72 users 3.9G Sep 19 10:56 WTeth2_S7_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4.1G Sep 19 10:59 WTeth3_S8_R1_001.fastq


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data>ls -l
total 25816116
-rwxrwxr-x 1 callen72 users    3996723 Nov 10 09:41 6803genome.fa
-rwxrwxr-x 1 callen72 users    1385252 Nov 10 09:41 geneannotation.gff3.fa
-rwxrwxr-x 1 callen72 users 4294934528 Sep 19 11:00 WTair1_S1_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4835516675 Sep 19 10:46 WTair2_S2_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4188371450 Sep 19 10:49 WTair3_S3_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4637692584 Sep 19 10:53 WTeth1_S4_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4147069520 Sep 19 10:56 WTeth2_S7_R1_001.fastq
-rwxrwxr-x 1 callen72 users 4326615469 Sep 19 10:59 WTeth3_S8_R1_001.fastq

Trimming scritp in trim.qsh (run script for each WT...fastq file)
#$ -N trim
#$ -cwd
#$ -S /bin/bash
#$ -q medium*
#$ -l mem=10G,h_vmem=10G
#$ -pe threads 8
java -jar /data/apps/trimmomatic/0.33/trimmomatic-0.33.jar \
SE \
-threads 8 \
-phred33 \
-trimlog WTair2.logFile \
../../raw_data/WTair2_S2_R1_001.fastq \
WTair2_S2_R1_001.fastq.trimmed.fq \
ILLUMINACLIP:/data/apps/trimmomatic/0.36/adapters/TruSeq3-SE.fa:2:30:10 \
SLIDINGWINDOW:4:15 MINLEN:75

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic>ls
Log_Files  trims                              WTair3_S3_R1_001.fastq.trimmed.fq  WTeth2_S7_R1_001.fastq.trimmed.fq
trim.qsh   WTair2_S2_R1_001.fastq.trimmed.fq  WTeth1_S4_R1_001.fastq.trimmed.fq  WTeth3_S8_R1_001.fastq.trimmed.fq


mkdir 3_fastqc (run command for each WT...fq file)
fastqc -o . ../2_trimmomatic/WTair2_S2_R1_001.fastq.trimmed.fq
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/3_fastqc>ls
WTair2_S2_R1_001.fastq.trimmed_fastqc.html  WTeth1_S4_R1_001.fastq.trimmed_fastqc.zip
WTair2_S2_R1_001.fastq.trimmed_fastqc.zip   WTeth2_S7_R1_001.fastq.trimmed_fastqc.html
WTair3_S3_R1_001.fastq.trimmed_fastqc.html  WTeth2_S7_R1_001.fastq.trimmed_fastqc.zip
WTair3_S3_R1_001.fastq.trimmed_fastqc.zip   WTeth3_S8_R1_001.fastq.trimmed_fastqc.html
WTeth1_S4_R1_001.fastq.trimmed_fastqc.html  WTeth3_S8_R1_001.fastq.trimmed_fastqc.zip


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data>ls
6803genome.fa           WTair1_S1_R1_001.fastq  WTair3_S3_R1_001.fastq  WTeth2_S7_R1_001.fastq
geneannotation.gff3.fa  WTair2_S2_R1_001.fastq  WTeth1_S4_R1_001.fastq  WTeth3_S8_R1_001.fastq

Index genome using bwa - Burrows-Wheeler Alignment Tool
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bwa>bwa index /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/6803genome.fa
[bwa_index] Pack FASTA... 0.04 sec
[bwa_index] Construct BWT for the packed sequence...
[bwa_index] 0.95 seconds elapse.
[bwa_index] Update BWT... 0.04 sec
[bwa_index] Pack forward-only FASTA... 0.02 sec
[bwa_index] Construct SA from BWT and Occ... 0.41 sec
[main] Version: 0.7.15-r1140
[main] CMD: bwa index /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/6803genome.fa
[main] Real time: 1.689 sec; CPU: 1.476 sec

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bwa>ls /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data
6803genome.fa      6803genome.fa.pac       WTair2_S2_R1_001.fastq  WTeth3_S8_R1_001.fastq
6803genome.fa.amb  6803genome.fa.sa        WTair3_S3_R1_001.fastq
6803genome.fa.ann  geneannotation.gff3.fa  WTeth1_S4_R1_001.fastq
6803genome.fa.bwt  WTair1_S1_R1_001.fastq  WTeth2_S7_R1_001.fastq

rmdir 4_bwa
mkdir 4_bowtie
ln -s /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTair2_S2_R1_001.fastq.trimmed.fastq . (Run for each WT..trimmed)
ln -s /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotations.gff3 .

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls
geneannotations.gff3                  WTeth1_S4_R1_001.fastq.trimmed.fastq
WTair2_S2_R1_001.fastq.trimmed.fastq  WTeth2_S7_R1_001.fastq.trimmed.fastq
WTair3_S3_R1_001.fastq.trimmed.fastq  WTeth3_S8_R1_001.fastq.trimmed.fastq

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>cp /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/6803genome.fa .
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls
6803genome.fa                         WTeth1_S4_R1_001.fastq.trimmed.fastq
geneannotations.gff3                  WTeth2_S7_R1_001.fastq.trimmed.fastq
WTair2_S2_R1_001.fastq.trimmed.fastq  WTeth3_S8_R1_001.fastq.trimmed.fastq
WTair3_S3_R1_001.fastq.trimmed.fastq

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>module load bowtie2
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>bowtie2-build 6803genome.fa 6803_genome
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls
6803_genome.1.bt2      geneannotations.gff3
6803_genome.2.bt2      WTair2_S2_R1_001.fastq.trimmed.fastq
6803_genome.3.bt2      WTair3_S3_R1_001.fastq.trimmed.fastq
6803_genome.4.bt2      WTeth1_S4_R1_001.fastq.trimmed.fastq
6803genome.fa          WTeth2_S7_R1_001.fastq.trimmed.fastq
6803_genome.rev.1.bt2  WTeth3_S8_R1_001.fastq.trimmed.fastq
6803_genome.rev.2.bt2

MAPPING script map.qsh
#$ -N Mapping
#$ -cwd
#$ -q medium*
#$ -pe threads 8
module load tophat
module load bowtie2
tophat -p 1 -o WTair2_Folder -G geneannotations.gff3 \
--transcriptome-index ./gene_index/gene \
6803_genome \
WTair2_S2_R1_001.fastq.trimmed.fq \
>& WTair2_Results










