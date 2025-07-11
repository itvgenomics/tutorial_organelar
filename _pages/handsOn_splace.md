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
2 - Alinhar cada arquivo FASTA separadamente com o MAFFT;\
3 - Concatenar os genes alinhados oriundos de um mesmo organismo;

![](/tutorial_organelar/images/splace.png)

❗ Tudo que estiver entre <> você deve trocar por seus valores ❗

Primeiro entre no ambiente que estamos utilizando para a aula:
```console
ssh <seu_usuario>@172.173.153.176
```
Após entrar no ambiente, vá para a sua pasta dentro do diretório alunos:
```console
cd /aula/alunos/<sua_pasta>
```

Crie uma pasta chamada "teste_splace":
```console
mkdir teste_splace
```

Entre na pasta criada:
```console
cd teste_splace
```

Agora vamos copiar os arquivos de exemplo que iremos utilizar na aula. Separamos os genes de cloroplasto de 10 espécies de plantas da família Araceae.
Rode o comando abaixo para copiar os arquivos para a sua pasta criada:
```console
cp -r /aula/splace_exemplos/gb .
```
❗ Não esqueça do ponto (.) no comando acima.

Copie também alguns arquivos .txt que estão presentes na pasta: 
```console
cp /aula/splace_exemplos/*.txt .
```
Agora você já tem todos os arquivos necessários para rodar o SPLACE. 
O comando e os parâmetros necessários para rodar o SPLACE podem ser vistos abaixo:

```shell
/aula/splace/splace_v3.sh -l <files directory> -t <num_threads> -o <output_name> -g <genes_list> -s <separator> -y <format_files> -f <feature>
```

-l <files directory> = Diretório com os arquivos FASTA ou GENBANK a serem incluídos na análise; 

-t <num_threads>	= Número de threads a serem usadas na etapa de alinhamento. Default é 1 thread;

-o <output_name>	Nome do arquivo a ser gerado contendo o resultado; 

-g <genes_list>	= Se você fornecer uma lista com o nome dos genes a serem incluídos na análise, qualquer organimo que não possuir certo gene terá a informação de gene faltante ('?') na supermatriz gerada. Se não for fornecida uma lista de genes, a análise é feita apenas com os genes compartilhados;  

-s <separator> = Símbolo do separador usado para distinguir o nome do gene e qualquer outra informação nos arquivos FASTA dos organismos. 

-y <format_files>	= Formato dos arquivos presente no diretório a ser analisada. Pode ser "fasta" ou "gb", sem aspas. 

-f	<feature> = Se estiver utilizando "-y gb", defina se quer incluir "CDS", "tRNA" ou "rRNA" (sem aspas). 

Um exemplo de comando de como seria rodar o SPLACE pode ser visto abaixo:

```shell
/aula/splace/splace_v3.sh -l gb/ -t 8 -o Araceae -g genes_list.txt -y gb -f CDS
```
