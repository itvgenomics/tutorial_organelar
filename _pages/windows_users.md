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
