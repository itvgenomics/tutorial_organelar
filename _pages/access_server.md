---
title: "Para usuários Windows"
layout: archive
permalink: /windows_users/
---  

### Windows

Se você é usuário de Windows, terá que ativar a função do Windows Subsystem Linux 2 (WSL2).

Para tal, siga as intruções do [tutorial](https://marcelo-albuquerque.medium.com/como-instalar-o-wsl-2-no-windows-10-3e26d99d7161)\
obs1: Escolha instalar o Ubuntu 22.04 LTS.

Abra o terminal Ubuntu como o da imagem abaixo e digite o seguinte comando
![](/tutorial_metabarcoding/images/ubuntu.png)


```console
sudo apt-get install bc
```

Após a devida configuração do WSL2 e instalação do Ubuntu, agora você precisa instalar o software Docker Desktop.
Baixe o instalador [aqui](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe?utm_source=docker&utm_medium=webreferral&utm_campaign=dd-smartbutton&utm_location=module&_gl=1*6n2oph*_ga*MzM5NjI4NTIxLjE3MTIyNjcxNDI.*_ga_XJWPQMJYHQ*MTcxNjY5NzMzOS4xMS4wLjE3MTY2OTczMzkuNjAuMC4w)

Após a instalação do Docker Desktop, também é necessário instalar um módulo do docker no terminal WSL2.
Abra o terminal do Ubuntu e digite o seguinte comando:

```console
sudo apt-get install docker.io
```

Após tudo configurado, baixe os scripts da ferramenta PIMBA para seu computador. Os scripts podem ser baixados nense [link](https://github.com/reinator/pimba/tree/main)

Salve o arquivo baixado em uma pasta no seu computador. Minha sugestão é que você crie uma pasta chamada `disciplina_metabarcoding` e guarde os arquivos baixados nela. 

Após descompactar o arquivo baixado do PIMBA, descompacte-a (clicando com o botão direito e selecionando a opção de desompactar).Você vai precisar dar permissão de execução para os arquivos dessa pasta. Para isso, faça o seguinte:

Entre no diretório onde está a pasta:
```console
cd disciplina_metabarcoding/
```

Liste se a pasta baixada e descompactada está realmente presente:
```console
ls
```

Vendo que tudo está certo, dê o seguinte comando para habilitar o modo de execução dos arquivos do PIMBA:

```console
chmod -R +x pimba_main
```
