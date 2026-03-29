# FGItools

WGS analysis for Forensic

## Overview

FGItools is a samtools-like STR analysis tool for forensic genomics, providing unified interfaces for STR and SNP variant calling.

## Features

- **STR variant calling** via STRsensor wrapper
- **SNP variant calling** via bcftools or GATK HaplotypeCaller
- Automatic CODIS format conversion from STRsensor VCF output

## Installation

Download the Linux binary and make it executable:

```bash
chmod +x fgitools
```

## Usage

### STR Calling

```bash
fgitools callstr <bam_list> <output> -r <region> -f <fasta> [options]
```

**Required arguments:**
- `bam_list` - File containing list of BAM file paths (one per line)
- `output` - Output directory path
- `-r, --region` - Region file (BED format)
- `-f, --fasta` - Reference genome FASTA file

**Optional arguments:**
- `-t, --threads` - Number of threads (default: 1)

**Example:**
```bash
fgitools callstr bam_list.txt ./output -r regions.txt -f reference.fa -t 8
```

### SNP Calling

```bash
fgitools callsnp <bam_list> <output> -R <ref> [options]
```

**Required arguments:**
- `bam_list` - File containing list of BAM file paths
- `output` - Output VCF file path
- `-R, --ref` - Reference FASTA for bcftools mpileup

**Optional arguments:**
- `-q, --quality` - Quality threshold (default: 20)
- `-d, --depth` - Minimum depth (default: 10)
- `-T, --tool` - Tool to use: `bcftools` or `gatk` (default: bcftools)

**Example:**
```bash
fgitools callsnp bam_list.txt output.vcf -R reference.fa -T bcftools
```

## Output

### STR Calling (`callstr`)

- `output/all.vcf` - Combined STR variant calls in VCF format
- `output/all.txt` - CODIS-formatted results (automatically generated from all.vcf)

### SNP Calling (`callsnp`)

- `output.vcf` - Filtered SNP variant calls
