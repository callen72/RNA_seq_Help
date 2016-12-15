RNA-Seq 
cd /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/mkdir analysis raw_data
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data>ls
analysis  raw_data 
I used WinSCP to load the RNA-Seq data into the raw_data file
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


For the first fastqc run: 
fastqc -o . /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/WTair1_S1_R1_001.fastq

Failed to process file WTair1_S1_R1_001.fastq
uk.ac.babraham.FastQC.Sequence.SequenceFormatException: Ran out of data in the middle of a fastq entry.  Your file is probably truncated
        at uk.ac.babraham.FastQC.Sequence.FastQFile.readNext(FastQFile.java:179)
        at uk.ac.babraham.FastQC.Sequence.FastQFile.next(FastQFile.java:125)
        at uk.ac.babraham.FastQC.Analysis.AnalysisRunner.run(AnalysisRunner.java:76)
        at java.lang.Thread.run(Thread.java:745)

qrsh -pe threads 8 -l mem=10G
mkdir 2_trimmomatic
cd 2_trimmomatic
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
(Will take a while to trim wait til trim.e file says completed successfully)

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic>ls
Log_Files       WTair1.logFile
trim.e8944554   WTair1_S1_R1_001.fastq.trimmed.fq
trim.o8944554   WTair2_S2_R1_001.fastq.trimmed.fq
trim.pe8944554  WTair3_S3_R1_001.fastq.trimmed.fq
trim.po8944554  WTeth1_S4_R1_001.fastq.trimmed.fq
trim.qsh        WTeth2_S7_R1_001.fastq.trimmed.fq
trims           WTeth3_S8_R1_001.fastq.trimmed.fq

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis>nano trim.e8944554
TrimmomaticSE: Started with arguments: -threads 8 -phred33 -trimlog WTair1.logF$
Using Long Clipping Sequence: 'AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTA'
Using Long Clipping Sequence: 'AGATCGGAAGAGCACACGTCTGAACTCCAGTCAC'
ILLUMINACLIP: Using 0 prefix pairs, 2 forward/reverse sequences, 0 forward only$
Exception in thread "Thread-0" java.lang.NullPointerException
        at org.usadellab.trimmomatic.fastq.FastqParser.parseOne(FastqParser.jav$
        at org.usadellab.trimmomatic.fastq.FastqParser.next(FastqParser.java:17$
        at org.usadellab.trimmomatic.threading.ParserWorker.run(ParserWorker.ja$
        at java.lang.Thread.run(Thread.java:745)
Input Reads: 20530000 Surviving: 18847109 (91.80%) Dropped: 1682891 (8.20%)
TrimmomaticSE: Completed successfully


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/trims>nano trim.e8854189
TrimmomaticSE: Started with arguments: -threads 8 -phred33 -trimlog WTair2.logF$
Using Long Clipping Sequence: 'AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTA'
Using Long Clipping Sequence: 'AGATCGGAAGAGCACACGTCTGAACTCCAGTCAC'
ILLUMINACLIP: Using 0 prefix pairs, 2 forward/reverse sequences, 0 forward only$
Input Reads: 23114903 Surviving: 21247792 (91.92%) Dropped: 1867111 (8.08%)
TrimmomaticSE: Completed successfully


mkdir 3_fastqc (run command for each WT...fq file)
fastqc -o . ../2_trimmomatic/WTair1_S1_R1_001.fastq.trimmed.fq
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/3_fastqc>ls
WTair1_S1_R1_001.fastq.trimmed_fastqc.html  WTeth1_S4_R1_001.fastq.trimmed_fastqc.html
WTair1_S1_R1_001.fastq.trimmed_fastqc.zip   WTeth1_S4_R1_001.fastq.trimmed_fastqc.zip
WTair2_S2_R1_001.fastq.trimmed_fastqc.html  WTeth2_S7_R1_001.fastq.trimmed_fastqc.html
WTair2_S2_R1_001.fastq.trimmed_fastqc.zip   WTeth2_S7_R1_001.fastq.trimmed_fastqc.zip
WTair3_S3_R1_001.fastq.trimmed_fastqc.html  WTeth3_S8_R1_001.fastq.trimmed_fastqc.html
WTair3_S3_R1_001.fastq.trimmed_fastqc.zip   WTeth3_S8_R1_001.fastq.trimmed_fastqc.zip

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
cd 4_bowtie
ln -s /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTair2_S2_R1_001.fastq.trimmed.fq . (Run for each WT..trimmed)
ln -s /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotation.gff3.fa 
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>cp /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/6803genome.fa .
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls
6803_genome.1.bt2       map4.qsh                           WTeth1_Folder
6803_genome.2.bt2       map5.qsh                           WTeth1_Results
6803_genome.3.bt2       map6.qsh                           WTeth1_S4_R1_001.fastq.trimmed.fq
6803_genome.4.bt2       map.qsh                            WTeth2_Folder
6803_genome.fa          WTair1_S1_R1_001.fastq.trimmed.fq  WTeth2_Results
6803_genome.rev.1.bt2   WTair2_Folder                      WTeth2_S7_R1_001.fastq.trimmed.fq
6803_genome.rev.2.bt2   WTair2_Results                     WTeth3_Folder
geneannotation.gff3.fa  WTair2_S2_R1_001.fastq.trimmed.fq  WTeth3_Results
gene_index              WTair3_Folder                      WTeth3_S8_R1_001.fastq.trimmed.fq
map2.qsh                WTair3_Results
map3.qsh                WTair3_S3_R1_001.fastq.trimmed.fq


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

Had to rename the 6803genome.fa
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls
6803_genome.1.bt2      geneannotation.gff3.fa
6803_genome.2.bt2      map.qsh
6803_genome.3.bt2      WTair2_S2_R1_001.fastq.trimmed.fq
6803_genome.4.bt2      WTair3_S3_R1_001.fastq.trimmed.fq
6803_genome.fa         WTeth1_S4_R1_001.fastq.trimmed.fq
6803_genome.rev.1.bt2  WTeth2_S7_R1_001.fastq.trimmed.fq
6803_genome.rev.2.bt2  WTeth3_S8_R1_001.fastq.trimmed.fq

MAPPING script map.qsh (made a script for each sample ex:map2.qsh , map3.qsh, ect)
#$ -N Mapping
#$ -cwd
#$ -q medium*
#$ -pe threads 8
module load tophat
module load bowtie2
tophat -o WTair2_Folder -p1 -G ./gene.gff \
        --transcriptome-index ./gene_index/gene \
        6803_genome \
WTair2_S2_R1_001.fastq.trimmed.fq \
>& WTair2_Results

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls -lh
total 18M (This was the beginning of the scripts)
-rw-r--r-- 1 callen72 users 5.3M Nov 16 19:08 6803_genome.1.bt2
-rw-r--r-- 1 callen72 users 964K Nov 16 19:08 6803_genome.2.bt2
-rw-r--r-- 1 callen72 users   53 Nov 16 19:08 6803_genome.3.bt2
-rw-r--r-- 1 callen72 users 964K Nov 16 19:08 6803_genome.4.bt2
-rwxr-xr-x 1 callen72 users 3.9M Nov 16 19:07 6803_genome.fa
-rw-r--r-- 1 callen72 users 5.3M Nov 16 19:08 6803_genome.rev.1.bt2
-rw-r--r-- 1 callen72 users 964K Nov 16 19:08 6803_genome.rev.2.bt2
lrwxrwxrwx 1 callen72 users   77 Nov 19 06:08 geneannotation.gff3.fa -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotation.gff3.fa
drwxr-xr-x 2 callen72 users 4.0K Nov 21 11:23 gene_index
-rw-r--r-- 1 callen72 users  276 Nov 21 11:33 map2.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:38 map3.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:49 map4.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:51 map5.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:19 map.qsh
drwxr-xr-x 4 callen72 users 4.0K Nov 21 11:46 WTair2_Folder
-rw-r--r-- 1 callen72 users 1.8K Nov 21 11:46 WTair2_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTair2_S2_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTair2_S2_R1_001.fastq.trimmed.fq
drwxr-xr-x 4 callen72 users 4.0K Nov 21 11:34 WTair3_Folder
-rw-r--r-- 1 callen72 users  960 Nov 21 11:49 WTair3_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTair3_S3_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTair3_S3_R1_001.fastq.trimmed.fq
drwxr-xr-x 4 callen72 users 4.0K Nov 21 11:38 WTeth1_Folder
-rw-r--r-- 1 callen72 users  804 Nov 21 11:41 WTeth1_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTeth1_S4_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTeth1_S4_R1_001.fastq.trimmed.fq
drwxr-xr-x 4 callen72 users 4.0K Nov 21 11:49 WTeth2_Folder
-rw-r--r-- 1 callen72 users  579 Nov 21 11:49 WTeth2_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTeth2_S7_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTeth2_S7_R1_001.fastq.trimmed.fq
drwxr-xr-x 4 callen72 users 4.0K Nov 21 11:51 WTeth3_Folder
-rw-r--r-- 1 callen72 users  579 Nov 21 11:51 WTeth3_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTeth3_S8_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTeth3_S8_R1_001.fastq.trimmed.fq


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls -lh
total 18M (This was the end results i deleted the Mapping.e,o.pe., & po files because they were empty)
-rw-r--r-- 1 callen72 users 5.3M Nov 16 19:08 6803_genome.1.bt2
-rw-r--r-- 1 callen72 users 964K Nov 16 19:08 6803_genome.2.bt2
-rw-r--r-- 1 callen72 users   53 Nov 16 19:08 6803_genome.3.bt2
-rw-r--r-- 1 callen72 users 964K Nov 16 19:08 6803_genome.4.bt2
-rwxr-xr-x 1 callen72 users 3.9M Nov 16 19:07 6803_genome.fa
-rw-r--r-- 1 callen72 users 5.3M Nov 16 19:08 6803_genome.rev.1.bt2
-rw-r--r-- 1 callen72 users 964K Nov 16 19:08 6803_genome.rev.2.bt2
lrwxrwxrwx 1 callen72 users   77 Nov 19 06:08 geneannotation.gff3.fa -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotation.gff3.fa
drwxr-xr-x 2 callen72 users 4.0K Nov 21 11:23 gene_index
-rw-r--r-- 1 callen72 users  276 Nov 21 11:33 map2.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:38 map3.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:49 map4.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:51 map5.qsh
-rw-r--r-- 1 callen72 users  276 Nov 21 11:19 map.qsh
drwxr-xr-x 3 callen72 users 4.0K Nov 21 12:00 WTair2_Folder
-rw-r--r-- 1 callen72 users 2.0K Nov 21 12:00 WTair2_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTair2_S2_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTair2_S2_R1_001.fastq.trimmed.fq
drwxr-xr-x 3 callen72 users 4.0K Nov 21 12:09 WTair3_Folder
-rw-r--r-- 1 callen72 users 2.0K Nov 21 12:09 WTair3_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTair3_S3_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTair3_S3_R1_001.fastq.trimmed.fq
drwxr-xr-x 3 callen72 users 4.0K Nov 21 12:18 WTeth1_Folder
-rw-r--r-- 1 callen72 users 2.0K Nov 21 12:18 WTeth1_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTeth1_S4_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTeth1_S4_R1_001.fastq.trimmed.fq
drwxr-xr-x 3 callen72 users 4.0K Nov 21 12:25 WTeth2_Folder
-rw-r--r-- 1 callen72 users 2.0K Nov 21 12:25 WTeth2_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTeth2_S7_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTeth2_S7_R1_001.fastq.trimmed.fq
drwxr-xr-x 3 callen72 users 4.0K Nov 21 12:33 WTeth3_Folder
-rw-r--r-- 1 callen72 users 2.0K Nov 21 12:33 WTeth3_Results
lrwxrwxrwx 1 callen72 users  102 Nov 21 11:16 WTeth3_S8_R1_001.fastq.trimmed.fq -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/2_trimmomatic/WTeth3_S8_R1_001.fastq.trimmed.fq

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>cd WTair2_Folder/
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie/WTair2_Folder>ls
accepted_hits.bam  deletions.bed   junctions.bed  prep_reads.info
align_summary.txt  insertions.bed  logs           unmapped.bam

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie/WTair2_Folder/logs>ls
bowtie_build.log                        long_spanning_reads.segs.log
bowtie.left_kept_reads.log              m2g_left_kept_reads.err
bowtie.left_kept_reads.m2g_um.log       m2g_left_kept_reads.out
bowtie.left_kept_reads.m2g_um_seg1.log  prep_reads.log
bowtie.left_kept_reads.m2g_um_seg2.log  reports.log
bowtie.left_kept_reads.m2g_um_seg3.log  reports.samtools_sort.log0
g2f.err                                 run.log
g2f.out                                 segment_juncs.log
gtf_juncs.log                           tophat.log
juncs_db.log


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>nano WTair2_Results
[2016-11-21 11:19:28] Beginning TopHat run (v2.1.1)
-----------------------------------------------
[2016-11-21 11:19:28] Checking for Bowtie
                  Bowtie version:        2.2.8.0
[2016-11-21 11:19:28] Checking for Bowtie index files (genome)..
[2016-11-21 11:19:28] Checking for reference FASTA file
[2016-11-21 11:19:28] Generating SAM header for 6803_genome
[2016-11-21 11:19:29] Reading known junctions from GTF file
        Warning: TopHat did not find any junctions in GTF file
[2016-11-21 11:19:29] Preparing reads
         left reads: min. length=75, max. length=75, 21175267 kept reads (72525 discarded)
[2016-11-21 11:23:01] Building transcriptome data files ./gene_index/gene
[2016-11-21 11:23:03] Building Bowtie index from gene.fa
[2016-11-21 11:23:05] Mapping left_kept_reads to transcriptome gene with Bowtie2
[2016-11-21 11:37:36] Resuming TopHat pipeline with unmapped reads
[2016-11-21 11:37:36] Mapping left_kept_reads.m2g_um to genome 6803_genome with Bowtie2
[2016-11-21 11:43:42] Mapping left_kept_reads.m2g_um_seg1 to genome 6803_genome with Bowtie2$
[2016-11-21 11:43:52] Mapping left_kept_reads.m2g_um_seg2 to genome 6803_genome with Bowtie2$
[2016-11-21 11:44:03] Mapping left_kept_reads.m2g_um_seg3 to genome 6803_genome with Bowtie2$
[2016-11-21 11:44:14] Searching for junctions via segment mapping
[2016-11-21 11:45:50] Retrieving sequences for splices
[2016-11-21 11:45:50] Indexing splices
Building a SMALL index
[2016-11-21 11:45:51] Mapping left_kept_reads.m2g_um_seg1 to genome segment_juncs with Bowti$
[2016-11-21 11:45:55] Mapping left_kept_reads.m2g_um_seg2 to genome segment_juncs with Bowti$
[2016-11-21 11:45:59] Mapping left_kept_reads.m2g_um_seg3 to genome segment_juncs with Bowti$
[2016-11-21 11:46:03] Joining segment hits
[2016-11-21 11:46:19] Reporting output tracks
-----------------------------------------------
[2016-11-21 12:00:46] A summary of the alignment counts can be found in WTair2_Folder/align_$
[2016-11-21 12:00:46] Run complete: 00:41:18 elapsed


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4_bowtie>ls
6803_genome.1.bt2       WTair2_Results
6803_genome.2.bt2       WTair2_S2_R1_001.fastq.trimmed.fq
6803_genome.3.bt2       WTair3_Folder
6803_genome.4.bt2       WTair3_Results
6803_genome.fa          WTair3_S3_R1_001.fastq.trimmed.fq
6803_genome.rev.1.bt2   WTeth1_Folder
6803_genome.rev.2.bt2   WTeth1_Results
geneannotation.gff3.fa  WTeth1_S4_R1_001.fastq.trimmed.fq
gene_index              WTeth2_Folder
map2.qsh                WTeth2_Results
map3.qsh                WTeth2_S7_R1_001.fastq.trimmed.fq
map4.qsh                WTeth3_Folder
map5.qsh                WTeth3_Results
map.qsh                 WTeth3_S8_R1_001.fastq.trimmed.fq
WTair2_Folder

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis>mkdir 5_htseq
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis>cd 5_htseq/

cp ../4_bowtie/WTair2_Folder/accepted_hits.bam New_WTair2_accepted_hits.bam 
(made for each Output_Folder)
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>ls
New_WTair2_accepted_hits.bam  New_WTeth1_accepted_hits.bam  New_WTeth3_accepted_hits.bam
New_WTair3_accepted_hits.bam  New_WTeth2_accepted_hits.bam

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>ln -s /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotation.gff3.fa
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>ls
geneannotation.gff3.fa        New_WTair3_accepted_hits.bam  New_WTeth2_accepted_hits.bam
New_WTair2_accepted_hits.bam  New_WTeth1_accepted_hits.bam  New_WTeth3_accepted_hits.bam

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>module load samtools
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>samtools sort -n -o New_WTair2_sorted_byName.bam New_WTair2_accepted_hits.bam
[bam_sort_core] merging from 9 files...

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>samtools sort -n -o New_WTair1_sorted_byName.bam New_WTair1_accepted_hits.bam
[W::sam_read1] parse error at line 1
[bam_sort_core] truncated file. Aborting.


/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>ls -lh
total 13G
lrwxrwxrwx 1 callen72 users   77 Nov 21 19:50 geneannotation.gff3.fa -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotation.gff3.fa
-rw-r--r-- 1 callen72 users 474M Nov 21 20:54 New_WTair2_accepted_hits.bam
-rw-r--r-- 1 callen72 users  46K Nov 21 21:25 New_WTair2_counts.txt
-rw-r--r-- 1 callen72 users 915M Nov 21 21:06 New_WTair2_sorted_byName.bam
-rw-r--r-- 1 callen72 users 6.0G Nov 21 21:10 New_WTair2_sorted_byName.sam
-rw-r--r-- 1 callen72 users 404M Nov 21 20:24 New_WTair3_accepted_hits.bam
-rw-r--r-- 1 callen72 users 740M Nov 21 22:12 New_WTair3_sorted_byName.bam
-rw-r--r-- 1 callen72 users 447M Nov 21 20:25 New_WTeth1_accepted_hits.bam
-rw-r--r-- 1 callen72 users 826M Nov 21 22:20 New_WTeth1_sorted_byName.bam
-rw-r--r-- 1 callen72 users 414M Nov 21 20:25 New_WTeth2_accepted_hits.bam
-rw-r--r-- 1 callen72 users 780M Nov 21 22:28 New_WTeth2_sorted_byName.bam
-rw-r--r-- 1 callen72 users 428M Nov 21 20:26 New_WTeth3_accepted_hits.bam
-rw-r--r-- 1 callen72 users 809M Nov 21 22:34 New_WTeth3_sorted_byName.bam

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>samtools view -o New_WTair2_sorted_byName.sam New_WTair2_sorted_byName.bam (convert all bam files to sam files)
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>ls -lh
total 34G
lrwxrwxrwx 1 callen72 users   77 Nov 21 19:50 geneannotation.gff3.fa -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotation.gff3.fa
-rw-r--r-- 1 callen72 users 474M Nov 21 20:54 New_WTair2_accepted_hits.bam
-rw-r--r-- 1 callen72 users  46K Nov 21 21:25 New_WTair2_counts.txt
-rw-r--r-- 1 callen72 users 915M Nov 21 21:06 New_WTair2_sorted_byName.bam
-rw-r--r-- 1 callen72 users 6.0G Nov 21 21:10 New_WTair2_sorted_byName.sam
-rw-r--r-- 1 callen72 users 404M Nov 21 20:24 New_WTair3_accepted_hits.bam
-rw-r--r-- 1 callen72 users 740M Nov 21 22:12 New_WTair3_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.2G Nov 21 22:38 New_WTair3_sorted_byName.sam
-rw-r--r-- 1 callen72 users 447M Nov 21 20:25 New_WTeth1_accepted_hits.bam
-rw-r--r-- 1 callen72 users 826M Nov 21 22:20 New_WTeth1_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.9G Nov 21 22:40 New_WTeth1_sorted_byName.sam
-rw-r--r-- 1 callen72 users 414M Nov 21 20:25 New_WTeth2_accepted_hits.bam
-rw-r--r-- 1 callen72 users 780M Nov 21 22:28 New_WTeth2_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.2G Nov 21 22:41 New_WTeth2_sorted_byName.sam
-rw-r--r-- 1 callen72 users 428M Nov 21 20:26 New_WTeth3_accepted_hits.bam
-rw-r--r-- 1 callen72 users 809M Nov 21 22:34 New_WTeth3_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.5G Nov 21 22:42 New_WTeth3_sorted_byName.sam


htseq-count -s no -t ID name -i Name New_WTair2_sorted_byName.sam geneannotation.gff3.fa > New_WTair2_counts2.txt 
(run script for each .sam file)
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/5_htseq>ls -lh
total 34G
lrwxrwxrwx 1 callen72 users   77 Nov 21 19:50 geneannotation.gff3.fa -> /lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/raw_data/geneannotation.gff3.fa
-rw-r--r-- 1 callen72 users 474M Nov 21 20:54 New_WTair2_accepted_hits.bam
-rw-r--r-- 1 callen72 users  46K Nov 21 21:25 New_WTair2_counts.txt
-rw-r--r-- 1 callen72 users 915M Nov 21 21:06 New_WTair2_sorted_byName.bam
-rw-r--r-- 1 callen72 users 6.0G Nov 21 21:10 New_WTair2_sorted_byName.sam
-rw-r--r-- 1 callen72 users 404M Nov 21 20:24 New_WTair3_accepted_hits.bam
-rw-r--r-- 1 callen72 users  46K Nov 21 22:54 New_WTair3_counts.txt
-rw-r--r-- 1 callen72 users 740M Nov 21 22:12 New_WTair3_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.2G Nov 21 22:38 New_WTair3_sorted_byName.sam
-rw-r--r-- 1 callen72 users 447M Nov 21 20:25 New_WTeth1_accepted_hits.bam
-rw-r--r-- 1 callen72 users  46K Nov 21 23:07 New_WTeth1_counts.txt
-rw-r--r-- 1 callen72 users 826M Nov 21 22:20 New_WTeth1_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.9G Nov 21 22:40 New_WTeth1_sorted_byName.sam
-rw-r--r-- 1 callen72 users 414M Nov 21 20:25 New_WTeth2_accepted_hits.bam
-rw-r--r-- 1 callen72 users  46K Nov 22 20:30 New_WTeth2_counts.txt
-rw-r--r-- 1 callen72 users 780M Nov 21 22:28 New_WTeth2_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.2G Nov 21 22:41 New_WTeth2_sorted_byName.sam
-rw-r--r-- 1 callen72 users 428M Nov 21 20:26 New_WTeth3_accepted_hits.bam
-rw-r--r-- 1 callen72 users  46K Nov 22 21:17 New_WTeth3_counts.txt
-rw-r--r-- 1 callen72 users 809M Nov 21 22:34 New_WTeth3_sorted_byName.bam
-rw-r--r-- 1 callen72 users 5.5G Nov 21 22:42 New_WTeth3_sorted_byName.sam

The New_Filename_counts.txt files were then transferred from Newton into a folder on the
desktop and loaded onto R,
set the working directory with:
setwd("~/RNA_Seq")

A DESeqDataSet object was then created using the DESeqDataSetFromHTSeqCount command:
sampleFiles <- grep("counts2.txt",list.files("."),value=TRUE)
sampleCondition <- sub("(.*)\\d.*","\\1",sampleFiles)
my_sampleTable <- data.frame(sampleName = WTAirFiles, fileName = WTAirFiles, condition = WTAir)
my_data <- DESeqDataSetFromHTSeqCount(sampleTable = my_sampleTable, directory = ".",design = design, ignoreRank = FALSE)

DESeqDataSetFromHTSeqCount(sampleTable, directory = ".", design, ignoreRank = FALSE, ...)
  countData <- matrix(1:100,ncol=4)
condition <- factor(c("A","A","B","B"))

the main DESeq function was performed on the DESeqDataSet object:
deseq_results = DESeq(my_data)

To compare specific conditions such as WT air vs WT ethylene the following command was written:
resultsNames(deseq_results)
[1] "Intercept"          "conditionNew_WTair" "conditionNew_WTeth"
condition1_condition2_results_table = results(deseq_results, contrast = c("condition","WTair", "WTeth"))

This data set was then exported as excel spreadsheet with the command:
write.csv(as.data.frame(condition1_condition2_results_table),file=("condition1_condition2_results.csv"))

To produce an MA plot from the specified condition comparison:
plotMA(condtion1_condition2_results_table, main="DESeq2", ylim=c(-10,10))

To produce a PCA plot the read counts were first transformed by:
rld <- rlog(my_data, blind=FALSE)

The PCA plot was produced by:
plotPCA(rld)

-REDID MY HTSEQ COUNT TO SHOW THE NAME INSTEAD OF THE GENE ID.

/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis>ls
0_raw_data  1_fastqc  2_trimmomatic  3_fastqc  4_bowtie  5_htseq  6_CountReads
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis>mkdir 4b_bwa
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis>cd 4b_bwa/
/lustre/projects/RNA_Seq_Data/SynRNA_Seq_Data/analysis/4b_bwa>module load bwa

Index refernce genome.
bwa index ../4_bowtie/6803_genome.fa .

