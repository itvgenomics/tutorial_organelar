---
title: "Phylogenomics with SPLACE"
layout: archive
permalink: /handsOn_splace/
---

Após a anotação e curadoria, os genes anotados podem ser utilizados em análises filogenômicas. 
Para isso, utilizamos uma ferramenta chamada SPLACE (https://www.frontiersin.org/journals/bioinformatics/articles/10.3389/fbinf.2022.1074802/full)

O código do SPLACE está disponível na página do Github (https://github.com/reinator/splace)

O SPLACE irá automatizar três principais etapas:

1 - Separar os mesmos genes de diferentes organismos em diferentes arquivos FASTA;\
2 - Alinhar cada arquivo FASTA separadamente;\
3 - Concatenar os genes alinhados oriundos de um mesmo organismo;

![](https://github.com/reinator/splace/blob/main/workflow2.png)

Example of OTU Tax assignment (tax_assignment.txt):

![](https://github.com/reinator/pimba/blob/main/Figures/taxresult_example.png?raw=true)

Example of Metadata file (metadata.csv):

![](https://github.com/reinator/pimba/blob/main/Figures/metadata_example.png?raw=true)
  
 The first column must always be "SampleID" and the second column must always be "SampleName"

 To run PIMBA plot, you will need to configure the following variables in the `pimba_smk/config/config.yaml` file:

| Parameter | Description |
| ----------- | ----------- |
| metadata | The path to the metadata file |
| group_by | Set "group_by" with the metadata parameter to group the samples (use "False" for not grouping the samples) |

Then, you can run the following command:
```console
./pimba_smk_main.sh -p no -r no -g yes -t 8 -c config/config.yaml
```

But remember❗ You cannot run the commands above directly in the terminal. Copy the file `/home/program2/src/PIMBA_smk/scripts/pimba_plot.slurm` to your folder. Open the file after you have pasted it to your work directory to see if everything is correctly set. Then, submit the job to the processing queue:

```console
sbatch pimba_plot.slurm
```
 
The list of plots that pimba_plot.sh will generate:

alpha_diversity_dotplot.svg\
rarefaction_curve2.svg\
cluster_dendogram.svg\
phylum_barplots.svg\
class_barplots.svg\
order_barplots.svg\
family_barplots.svg\
genus_barplots.svg\
