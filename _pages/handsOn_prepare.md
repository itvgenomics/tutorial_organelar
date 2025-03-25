---
title: "Hands On"
layout: archive
permalink: /handsOn_prepare/
---  

Before running PIMBA, let's examine whether the base quality of the dataset you have chosen is good or bad.
Go to the folder `~/cursos/MetabarcodingITV2025/<your_dataset>/` and replace `<your_dataset>` with your chosen dataset.
If you use the `ls` command, you can list and view all the FASTQ files in the dataset.

```console  
cd ~/cursos/MetabarcodingITV2025/<your_dataset>/
ls
```
To run FastQC in the biotec02 server, you need to load the software module with the following command:
```console  
module load Bio/FastQC/0.12.1
```

Once you have loaded the FastQC module correctly, just type the command below and wait for FastQC to analyze your dataset.
```console  
fastqc *.fastq
```
FastQC generated the HTML files that will allow you to see the base quality of your data.
You can combine all quality reports into a single file with MultiQC.
### WARNING ❗ :exclamation:
As explained, you can't run this command directly from the terminal. Therefore, copy the file `multiqc.slurm` that is in the directory `/home/program2/src/PIMBA_smk/scripts/multiqc.slurm` to the folder where you are going to run fastqc.

Open the `multiqc.slurm` file, check if everything is correct, and submit the job to the processing queue, as explained [here](https://itvgenomics.github.io/tutorial_metabarcoding_v3/submitting_jobs/)

Now let's PIMBA!

The first step in running PIMBA is to prepare your data. PIMBA can be used with paired-end or single-end reads (the latter being single-index or dual-index). The output will be a Fasta file that can be used in the next step. In this tutorial, we will use only paired-end reads, but you can check how to prepare single-end reads with dual and single-indexes [here](https://github.com/itvgenomics/pimba_smk/blob/main/README.md#a-configure-the-configyaml-file).

### A) Configure the config.yaml File

The config.yaml file (~/cursos/MetabarcodingITV2025/pimba_smk/config/config.yaml) is the general configuration file. It should contain parameters such as the maximum number of processors, adapter sequences, input file paths, etc. Open the file in a text editor and make the following modifications. **Note: Use full paths; partial paths will not work in this version.**

You can edit the config file with the following command:
```console  
vim ~/cursos/MetabarcodingITV2025/pimba_smk/config/config.yaml
```
#### General options for all modes

| Parameter | Description |
| ----------- | ----------- |
| num_threads | The num_threads option indicates the maximum number of processors to be used for tasks that allow parallelization. |

#### General options for the Prepare Mode
If the user wishes to run the "prepare" mode to prepare the reads for the "run" mode, edit the following options:

| Parameter | Description |
| ----------- | ----------- |
| minlength | The minimum length of a read after quality filtering. |
| minphred | The minimum PHRED score for quality filtering. |
| outputprepare | The name of the output file to be created in FASTA format. The ".fasta" extension is included automatically |

#### Inputs to run paired-end reads
If the user wishes to run PIMBA for paired-end reads, it is necessary to configure:

| Parameter | Description |
| ----------- | ----------- |
| rawdatadir | The path to the directory where the reads are located |
| adapters | The path to the adapter file within the resources directory |

Once you have finished editing the `config.yaml` file with the file paths, you can now run the prepare module with the following command:
```console  
bash pimba_smk_main.sh -p paired_end -r no -g no -t 8 -c config/config.yaml
```
The "pimba_smk_main.sh" file is the main bash script that runs all the pipeline steps in Snakemake. This file takes the following parameters as input:

- "-p": PIMBA preparation mode; choose between "paired_end", "single_index", "dual_index", or "no";
- "-r": PIMBA execution mode; specify the name of the marker gene (and consequently the database) to be used, choosing from 16S-SILVA, 16S-GREENGENES, 16S-RDP, 16S-NCBI, ITS-FUNGI-NCBI, ITS-FUNGI-UNITE, ITS-PLANTS-NCBI, or COI-NCBI. For a custom database, include the path to the directory where the database is stored instead of the marker gene. To skip, indicate "no";
- "-g": PIMBA plotting mode; choose between "yes" or "no";
- "-t": number of processors;
- "-c": the path to the config file.

### WARNING ❗ :exclamation:
Remember that you cannot run the command above directly in the terminal. For that, we will use a slurm file located in `/home/program2/src/PIMBA_smk/scripts/pimba_prepare.slurm`.
Copy the `pimba_prepare.slurm` file to the folder you have created `~/cursos/MetabarcodingITV2025/pimba_smk/`.
```console  
cp /home/scripts/pimba_prepare.slurm ~/cursos/MetabarcodingITV2025/pimba_smk/
```

Edit the slurm file and check if the command is correct
```console  
vim ~/cursos/MetabarcodingITV2025/pimba_smk/pimba_prepare.slurm
```

Once everything is correct, you can now submit your job to be processed:
```console  
sbatch ~/cursos/MetabarcodingITV2025/pimba_smk/pimba_prepare.slurm
```

When pimba_prepare finishes, it will create a FASTA file with the name of the parameter `outputprepare` you have chosen. Let's assume it is called `AllSamples`.\
This FASTA file gatherers all reads from all samples in a unique file (hence the name `AllSamples`).
If you wish to know how many reads remained after quality treatment in this file, you can use the command below:

```console  
  grep -c ">" AllSamples.fasta
```

Another created FASTA file ends with `withSingleton`. ' This file contains the same reads as the other FASTA file but also has good-quality reads that were not paired.

