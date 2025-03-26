---
title: "Part 4 - Diversity metrics and plots with PIMBA_plot"
layout: archive
permalink: /handsOn_plot/
---

## Plot your diversity results

When you finish with PIMBA_run, you can generate basic plots for your results, such as PCoA, rarefaction curves, and alpha and beta diversity plots.
You will need only two files that PIMBA_run will generate and one metadata file you must provide.

Example of OTU table (otu_table.txt) generated with PIMBA_run:

![](https://github.com/reinator/pimba/blob/main/Figures/otutable_example.png?raw=true)

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
