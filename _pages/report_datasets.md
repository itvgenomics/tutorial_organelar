---
title: "Datasets para o relatório"
layout: archive
permalink: /report_datasets/
---

Com base no sorteio realizado, baixe o dataset abaixo que você ficou responsável:

# COI de guano

[Dataset1](https://1drv.ms/f/s!Aq5Vg7CO1tohhbwJGGr5H8Lc1Aazhw?e=dtetey)\
[Dataset2](https://1drv.ms/u/s!Aq5Vg7CO1tohhb0eJd7m2YWFRiKL8g?e=MKGS7k)\
[Dataset3](https://1drv.ms/f/s!Aq5Vg7CO1tohhbwJGGr5H8Lc1Aazhw?e=OmHKsY)\
[Dataset4](https://1drv.ms/u/s!Aq5Vg7CO1tohhb0ZZte9lDS3D21f8Q?e=sapWhP)
([Metadados](https://1drv.ms/f/s!Aq5Vg7CO1tohhbwJGGr5H8Lc1Aazhw?e=vFWS7g))

# ITS de solo

[Dataset1](https://1drv.ms/u/s!Aq5Vg7CO1tohhb0SEFveYVDFeXzqmg?e=8e25yS)\
[Dataset2](https://1drv.ms/u/s!Aq5Vg7CO1tohhb0W-wRpGuTEa7XoDg?e=rOMaOF)\
[Dataset3](https://1drv.ms/u/s!Aq5Vg7CO1tohhb0N9HHUk5YkRvmvHw?e=1FRgOW)\
([Metadados](https://1drv.ms/u/s!Aq5Vg7CO1tohhb0f0pHAzR80VjC3NQ?e=2nOZwC))

# Questões para o relatório:

## Rode o pimba_prepare, coloque o comando usado e responda as perguntas abaixo com relação ao tratamento de dados dos dados:

1) Escolha duas amostras do seu dataset e responda:
   
   a) Rode o FastQC e compare o gráfico de qualidade das reads antes do tratamento de dados e depois. Quais as principais diferenças? Qual valor PHRED foi escolhido para rodar o pimba_prepare? (30pts)

   b) Quantas reads (sequências) existiam nas amostras antes e depois do tratamento de qualidades? (30pts)

   c) rode o pimba_prepare novamente escolhendo um valor mais alto ou mais baixo de qualidade PHRED. Quais diferenças você percebe com o antes e depois, e com relação ao valor anterior PHRED? (30pts)

   d) Quantas sequências ficaram no resultado final (AllSamples.fasta) do pimba_prepare? (10pts)


## Rode o pimba_run, coloque o comando usado e responda as perguntas abaixo com relação à clusterização e obtenção das OTUS:

1) Quantas OTUS foram obtidas? (20pts)

2) Dessas OTUS, quantas tiveram alguma classificação taxonômica com base no banco de dados que você utilizou? (20pts)

3) Altere o parâmetro `-l length` pra um valor diferente e responda as questões 1 e 2 considerando esses novos resultados. (30pts)

4) Altere o parâmetro de similaridade `-s ` e responda as questões 1 e 2 considerando esses novos resultados. (30pts)


