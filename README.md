RNA-Seq Data Analysis Pipeline
- Designed for:
  + Stranded Zymo-Seq Total RNA-Seq
  + Non-Stranded Smart-seq2 Nextera XT RNA-Seq
- Developed by ZB Lab (SBS, NTU)
- This pipeline is for performing a series of tasks, including file extraction, trimming, alignment, assembly, expression analysis, and transcript classification. 
- Any quetion or bugs, please contact me at tienquanghuy.duong@ntu.edu.sg.

Table of Contents
    - Installation
    - Requirements
    - Usage
    - Directory Structure
    - Troubleshooting
    - License

1. Installation
- Clone the repository to your local machine:
	git clone <repository-url>
- Make the script executable
	chmod +x ZRNA_seq
- Move it to the directory in your $PATH (optional)

2. Requirements
- Ensure Python and pip are installed
	python3 --version
	pip3 --version
- Install the necessary dependencies (e.g., pandas):
	pip install pandas
- Ensure that all the required tools are available in your system path:
	trim_galore --help
	hisat2 --help
	stringtie --help
	samtools --help
	bedtools --help

3. Usage
- To run the pipeline, run the script.py:
	ZRNA_seq -lib {stranded,non_stranded} -q query -r reference 
	[-h help] [-@ thread] [-a adapter] [-st step] [-rc raw_count] [-c classification] 
	[-m min_overlap] [-o output] [-rq ref_fasta] [-rg ref_gff] [-v version] [-V verbose]
- The pipeline consists of several steps that can be executed in sequence, depending on the chosen options. The available steps are:
    	+ Extraction: Extract files from raw data.
	+ Trimming: Trim adapters and low-quality bases.
	+ Mapping: Align reads to a reference genome.
	+ Assembly: Perform transcript assembly using StringTie.
    	+ Expression Analysis: Calculate gene and transcript expression (TPM/FPKM).
    	+ Read Count Calculation: Calculate the read count for each gene.
    	+ Transcript Classification: Classify novel transcripts based on overlap and exon count.
- The adapter file must follow the format shown below. 
	+ A header is required
	+ The sample names should match those in the input folder containing the FASTQ files.
	+ Format:
	Sample,i7_index,i5_index
	Sample1,TGATTATACG,GTCGATTACA
	Sample2,CAGCCGCGTA,ACTAGCCGTG
	.............................

4. Directory Structure
- After running the pipeline, the following directory structure will be generated in final directory:
	+ 0_raw_reads: Directory where the extracted raw reads are stored.
	+ 1_trim: Directory for the trimmed reads.
	+ 2_map: Directory for mapping results (BAM files).
	+ 3_assembly: Directory for the transcript assembly and expression data.
	+ 4_count: Directory for read count results.
	+ 5_classification: Directory for transcript classification results.
- Final directory (specified with -- output): where all results are moved after processing.

5. Troubleshooting
- Missing dependencies: Make sure that all tools are installed correctly. If any dependencies are missing, you may need to install them manually or use a containerized solution like Docker.
- Errors in output: Ensure that the input files are formatted correctly and match the expected formats for each tool (e.g., GFF for genome annotation, FASTA for the reference genome).
- Memory/CPU issues: The pipeline uses parallel processing for certain steps. Ensure that you have enough computational resources available for running the pipeline efficiently.

6. License
- This project is licensed under the MIT License - see the LICENSE file for details.
