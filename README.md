# Tutorial Prático: Montagem de Genoma Organelar com OrganPipe

## Introdução ao Terminal e ao Ambiente Unix

O **terminal** é uma interface de linha de comando usada para interagir com o sistema operacional. Nele, você pode criar pastas, mover arquivos, instalar programas e rodar ferramentas bioinformáticas.

### Comandos básicos:

| Comando         | Função                                      |
| --------------- | ------------------------------------------- |
| `ls`            | Lista arquivos e diretórios                 |
| `cd <dir>`      | Entra em um diretório                       |
| `mkdir <dir>`   | Cria um novo diretório                      |
| `cp`            | Copia arquivos ou diretórios                |
| `pwd`           | Printa no terminal o ambiente de trabalho atual |
| `cat <arquivo>` | Mostra o conteúdo de um arquivo no terminal |
| `vim <arquivo>` | Abre um editor de texto no terminal         |

### O que é o terminal?

O **terminal** é uma interface de linha de comando usada para interagir com o sistema operacional via texto. Ele permite executar programas, navegar entre diretórios, manipular arquivos e muito mais.

### O prompt

Ao abrir o terminal, você verá uma linha parecida com:

```bash
<usuario>@azusdsgenvm003 ~:~$ 
```

Essa linha é chamada de **prompt**, e indica que o terminal está pronto para receber comandos.

### Executando comandos

Um comando geralmente tem esta estrutura:

```bash
comando [opções] [argumentos]
```

* **Comando:** o que você quer fazer (ex: `ls` para listar arquivos)
* **Opções:** modificam o comportamento do comando (ex: `-l` para exibir detalhes)
* **Argumentos:** informações que o comando vai usar (ex: caminho de um diretório)

Exemplo:

```bash
ls -lh /aula
```

Esse comando lista o conteúdo do diretório `/aula`, com informações detalhadas e tamanhos em formato legível.

### Onde estou? (pwd)

Use o comando `pwd` para ver o diretório atual:

```bash
pwd
```

### Criando diretórios (mkdir)

Você pode criar um novo diretório com:

```bash
mkdir novo_diretorio
```

Ou criar um subdiretório dentro de outro:

```bash
mkdir pasta1/subpasta
```

### Listando arquivos (ls)

Para ver o conteúdo de um diretório:

```bash
ls
```

Use opções como `-l` (detalhes) e `-h` (formato legível):

```bash
ls -lh pasta
```

### Navegando com cd

O comando `cd` permite trocar de diretório:

```bash
cd nome_da_pasta
```

Você pode usar **caminhos relativos** (baseados no diretório atual) ou **caminhos absolutos** (começam com `/`).

Exemplo de caminho relativo:

```bash
cd linux_tutorial
```

Exemplo de caminho absoluto:

```bash
cd /home/username/linux_tutorial
```

### Dica: Tab para autocompletar

Você pode usar a tecla **Tab** para completar automaticamente nomes de arquivos ou diretórios enquanto digita no terminal. Isso economiza tempo e evita erros.

---

## Acessando o Servidor na Nuvem (Azure)

Abra o terminal no seu computador e conecte-se ao servidor usando SSH:

```bash
ssh <usuario>@<ip>
```

Você será solicitado a digitar sua senha.

---

## Organização do servidor

A pasta com qual vamos trabalhar está localizada no /aula do sistema. Esta pasta possui o seguinte conteúdo:

| Nome                 | Tipo      | Descrição                                                                 |
|----------------------|-----------|---------------------------------------------------------------------------|
| `adaptadores.txt`    | Arquivo   | Arquivo de texto contendo sequências de adaptadores para filtragem.      |
| `alunos`             | Pasta     | Diretório principal para os trabalhos individuais dos alunos.            |
| `exemplo_output`     | Pasta     | Exemplo de saída gerada por uma execução completa do OrganPipe.          |
| `metadados.csv`      | Arquivo   | Arquivo CSV com metadados das amostras ou experimentos.                  |
| `organpipe`          | Pasta     | Contém os arquivos necessários para rodar o OrganPipe.         |
| `rawreads`           | Pasta     | Raw Reads utilizadas para serem utilizadas como exemplo.      |
| `seeds`              | Pasta     | Seeds de referência para as montagem.       |
| `sifdir`             | Pasta     | Diretório com os containers `.sif` usados pelo Singularity.              |
| `splace`             | Pasta     | Contém os arquivos necessários para rodar o Splace.   |
| `splace_exemplos`    | Pasta     | Exemplos de uso do Splace.                      |
| `splace_teste`       | Pasta     | Diretório para testes do Splace.                         |

---

## Preparando o Ambiente de Trabalho

Após logar:

```bash
cd /aula/alunos # Modifica o seu ambiente de trabalho atual para a pasta de trabalho
```
```bash
mkdir brunoms       # Cria uma pasta com seu nome de usuário
```
```bash
cd brunoms          # Entra na sua pasta de trabalho
```

---

## Ativando o Ambiente Conda

O **Conda** é um gerenciador de ambientes que facilita o uso de ferramentas bioinformáticas.

Ative o ambiente necessário para usar o OrganPipe:

```bash
source /opt/anaconda3/etc/profile.d/conda.sh
```
```bash
conda activate /home/c0363_ds_usr/.conda/envs/organpipe
```

---

## Baixando os Dados de Sequenciamento

Utilizaremos o `fasterq-dump` para baixar os dados do NCBI a partir de um ID SRA. Substitua `<ID>` pelo identificador desejado.

```bash
fasterq-dump <ID> -p --split-files -O sra_output && gzip sra_output/*
```

> Exemplo:
> `fasterq-dump SRR12345678 -p --split-files -O sra_output && gzip sra_output/*`

Esse comando irá:

* Baixar os arquivos `.fastq`;
* Dividir em pares de leitura (se for paired-end);
* Compactar os arquivos com gzip.

---

## Análise de Qualidade com FastQC

Execute o FastQC em todos os arquivos `.fastq.gz`:

```bash
fastqc sra_output/*.fastq.gz -o fastqc_output
```

> Isso irá criar um diretório `fastqc_output` com relatórios `.html` e `.zip` de qualidade.

Faça o download dos arquivos .html para o seu computador para poder visualizar os resultados.

---

## Editando o Arquivo de Configuração

O OrganPipe requer um arquivo `config.yaml` para definir as opções do pipeline.

### Para editar:

```bash
vim config.yaml
```

No **vim**:

* Pressione `i` ou `insert` para começar a editar (veja "INSERT" no canto inferior);
* Edite o conteúdo;
* Para salvar e sair: pressione `ESC`, digite `:wq` e pressione `ENTER`.

---

## Copiando os Arquivos do OrganPipe

Copie os arquivos de configuração e scripts necessários para seu diretório:

```bash
cp -r /aula/organpipe/* .
```

> **O ponto final (`.`) significa "copiar para o diretório atual" — não esqueça dele!**

---

## Rodando o Pipeline OrganPipe

Execute o pipeline com o seguinte comando:

```bash
bash OrganPipe.sh -d . -c config.yaml -t 4 -sifdir /aula/sifdir -np
```

