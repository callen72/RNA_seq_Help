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







