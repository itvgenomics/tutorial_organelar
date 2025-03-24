---
title: "Hands On"
layout: archive
permalink: /handsOn_pimba/
---  

# PIMBA 3.0 - A PIpeline for MetaBarcoding Analysis
PIMBA allows the use of customized databases, as well as other reference databases.

## How to cite?
The peer-reviewed version of the paper can be found at https://doi.org/10.1007/978-3-030-91814-9_10

```console  
OLIVEIRA, R. R. M. et al. PIMBA: A PIpeline for MetaBarcoding Analysis. Advances in Bioinformatics and Computational Biology. 1ed. Switzerland: Springer, 2021, v. 13063, p. 106–116, 2021.
```

```console  
OLIVEIRA, RENATO RENISON MOREIRA; SILVA, R. L. ; NUNES, GISELE LOPES ; OLIVEIRA, GUILHERME .PIMBA: a PIpeline for MetaBarcoding Analysis. In: Stadler P.F., Walter M.E.M.T., Hernandez-Rosales M., Brigido M.M.. (Org.).Advances in Bioinformatics and Computational Biology. 1ed. Switzerland: Springer, 2021, v. 13063, p. 106-116
```

## How to install?
After you have logged in to the Biotec02 server, you will need to create the environment to run PIMBA. Type the following commands in a terminal console:

```console  
export MAMBA_ROOT_PREFIX=$HOME/pkgmngrs/Micromamba/
eval "$(/home/program2/bin/Micromamba/2.0.5-0/bin/micromamba shell hook -s posix)"
micromamba create -n snakemake_env -c bioconda -c conda-forge singularity=3.8.6 snakemake=7.32.4
```

Once you have created the environment, you will need to activate it:

```console  
micromamba activate snakemake_env
```

We recommend to create a folder where you will save your data and run the analysis during the course:
```console  
mkdir -p ~/cursos/MetabarcodingITV2025/
```

Now we will enter the folder you have created:
```console  
cd ~/cursos/MetabarcodingITV2025/
```

Then you just need to download the software PIMBA into the folder:
```console  
git clone https://github.com/itvgenomics/pimba_smk.git
```

You can enter the downloaded folder:
```console  
cd pimba_smk/
```

To see the files in the folder you have downloaded, type the following command:
```console  
ls
```

### Reccomendation ❗
You can create sessions to "save" the status of your work across the different days of this course. For that, just type the following command in your terminal:
```console
screen -S <name_your_session>
```

e.g.: 
```console
screen -S curso_metabar
```

Once you do that, and run the PIMBA commands in this session, you can detach this session, without ending it, just holding the following keys:
CTRL+A+D

Once you close your terminal, you can return (attach) to the session with the command:
```console
screen -r curso_metabar
```

To end a session permanently, just hold the following keys:
CTRL+D

You can create different sessions. To list all of them, just type:
```console
screen -ls
```



And that's all! Now you can run PIMBA on your data!

