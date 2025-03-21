---
title: "Submetendo jobs na fila do cluster"
layout: archive
permalink: /submitting_jobs/
---

Para mantermos organizado o ambiente computacional compartilhado, é utilizado o sistema [SLURM](https://slurm.schedmd.com/documentation.html) 
Este sistema permite que todos os processos que precisam de recursos de processador e memória do servidor Biotec02 fiquem organizados em uma fila de processamento e de fácil monitoramento.

### Arquivo SLURM
Todo comando que precise de recursos de processamento e memória não pode ser rodado diretamente do terminal. O comando precisa estar primeiramente dentro de um arquivo `.slurm`, cuja estrutura você pode verificar abaixo:

```shell
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=8
#SBATCH --time=1:00:00
#SBATCH --mem=32gb
#SBATCH --job-name=multiqc
#SBATCH --output=multiqc.slurm.log
#SBATCH --error=multiqc.slurm.err

printf "Inicio: `date`\n";
TBEGIN=`echo "print time();" | perl`

printf "\n"
printf "> Executando job_code7\n";
printf "> Rodando em $SLURM_CPUS_PER_TASK nucleos, em $SLURM_NNODES nos\n"

##########INSIRA SEU COMANDO ABAIXO##########################
module load Bio/FastQC/0.12.1
fastqc -t 8 SRR*
#############################################################

TEND=`echo "print time();" | perl`

printf "\n"/
printf "Fim: `date`\n";
printf "Tempo decorrido (s): `expr $TEND - $TBEGIN`\n";
printf "Tempo decorrido (min): `expr $(( ($TEND - $TBEGIN)/60 ))`\n";
echo "TERMINADO"
```

No exemplo acima, as primeiras linhas indicam os recursos que serão necessários para rodar o comando que você deseja executar.
Por exemplo, o programa `fastqc` será executado usando `8` threads. Isso é definido na linha abaixo:
```shell
#SBATCH --cpus-per-task=8
```

Na linha abaixo é informado a quantidade de memória RAM que será reservada para rodar a ferramenta. É importante saber se a quantidade informada realmente é necessária.
```shell
#SBATCH --mem=32gb
```

Nas três linhas seguintes, são definidos o nome do job, onde deverá ser salvo o log do comando e onde deverá ser salvo os erros dados no comando:
```shell
#SBATCH --job-name=multiqc
#SBATCH --output=multiqc.slurm.log
#SBATCH --error=multiqc.slurm.err
```

Toda vez que você for rodar um comando, deverá alterar a linha abaixo (talvez você tenha percebido pela sutil descrição no arquivo):
```shell
module load Bio/FastQC/0.12.1
fastqc -t 8 SRR*
```

As outras linhas são apenas comandos de controle do job e não devem ser alteradas.


### Editando o arquivo SLURM

Para editar o arquivo `.slurm`, você pode usar o comando `vim`. Com esse comando, você consegue editar o conteúdo do arquivo. 
```shell
vim multiqc.slurm
```

Após executar o comando, você precisa apertar a tecla `i` (INSERT) pra poder editar o documento.
Ao terminar de fazer as edições necessárias, você precisa apertar a tecla `ESC`, para sair do modo de edição.
Em seguida, digite a tecla de dois pontos `:` e em seguida digite `wq!` para indicar que você deseja salvar o documento e sair da edição.

Toda vez que você for rodar um comando dos softwares apresentados neste tutorial, você vai precisar submeter o job do comando para a fila de jobs do cluster Biotec02 com as instruções mostradas anteriormente.

### Submetendo o arquivo SLURM para a fila de jobs

Após ter editado o arquivo `.slurm` com o comando que você deseja executar, você precisa submeter o job para uma fila de processamento.

Para submeter seu job, execute o comando `sbatch` abaixo:
```shell
sbatch <arquivo.slurm>
```
Por exemplo:
```shell
sbatch multiqc.slurm
```

### Consultando a fila de jobs submetidos

Caso você queira saber quais jobs estão sendo executados, quem está executando, quanto de recurso computacional está sendo utilizado e há quanto tempo o processo está sendoe executado, basta usar o comando `squeue`:
```shell
squeue
```

Ao executar o comando acima, você vai ser capaz de verificar a fila de jobs submetidos até o momento e que estão rodando ou em pausa, como demonnstrado abaixo:

```shell
           JOBID PARTIT NAME         USER     ST         TIME   TIME_LIMIT CPUS MIN_MEM NODELIST
          745726 bigmem orthofinder  sandrade R   14-00:21:17  29-04:00:00   50    250G n01
          745758 bigmem bash         hmontene R    6-22:42:59   7-12:00:00   32    330G n01
          745755 long   panEDTA2     dmpachon R    7-05:56:15  30-00:00:00   30    200G n01
          746059 long   EDTA-Tx      dmpachon R       5:55:43  30-00:00:00   30    200G n02

```

No resultado do comando `squeue`, podemos ter as seguintes informações: 

`JOBID`: Identificador do job submetido. Esse identificador é importante caso queira deletar um job da fila; \
`USER`: Usuário que submeteu o job para a fila. Se você submeteu algum job, seu ID deve aparecer associada ao job submetido; \
`NAME`: Nome do job que você configurou no arquivo `.slurm`; \
`CPUS`: Número de threads usadas no job submetido; \
`MIN_MEM`: Quantidade de memória mínima reservada para o job; \
`ST`: Status do job. Pode ser R (Running), E (error), H (hold) ou Q (queue); \
`TIME`: Há quanto tempo o job está sendo executado.

###  Deletando um job específico
A numeração presente na coluna `JOBID`pode ser usada para caso você deseje deletar um job da fila, com o comando `scancel`. Para tal, você pode rodar o seguinte comando:
```shell
scancel 746059
```

Neste caso, o job de nome "EDTA-Tx" presente na fila de jobs seria deletado. Você só pode deletar um job que tenha sido submetido por você.




