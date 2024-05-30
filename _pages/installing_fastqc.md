---
title: "Instalando o FastQC"
layout: archive
permalink: /installing_fastqc/
---  

### Instalando o FastQC

O [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) é um software que permite visualizar a qualidade das bases de uma amostra sequenciada. 
Além disso, também permite verificar algumas outras métricas de qualidade do sequenciamento, como presença de contaminantes, sequências artefatos, frequência de nucleotídeos, etc.

Se você utiliza Ubuntu ou o WSL2 no Windows, abra um terminal e digite o seguinte comando:

```console
sudo apt-get install fastqc
```

Se você utiliza Mac, abra um terminal e digite o seguinte comando:

```console
brew install fastqc
```

Após instalado, para rodar o FastQC em um arquivo Fastq, rode o seguinte comando:

```console
fastqc [arquivo.fastq]
```
Substituta o termo `arquivo.fastq` pelo caminho até o arquivo que você deseja analisar.
