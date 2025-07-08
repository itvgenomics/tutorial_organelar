---
title: "Para usuários Windows"
layout: archive
permalink: /windows_users/
---  

### Windows

Se você é usuário de Windows, terá que ativar a função do Windows Subsystem Linux 2 (WSL2).

Para tal, siga as intruções do [tutorial](https://marcelo-albuquerque.medium.com/como-instalar-o-wsl-2-no-windows-10-3e26d99d7161)\
obs1: Escolha instalar o Ubuntu 24.04 LTS.

#### Passo 1 — Habilitar o Subsistema do Windows para Linux
Antes de instalar qualquer distribuição do Linux no Windows, precisamos primeiro habilitar o recurso opcional “Subsistema do Windows para Linux”.

Abra o PowerShell como administrador e execute:
```console
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

#### Passo 2 — Habilitar o recurso de Máquina Virtual
Antes de instalar o WSL 2, precisamos habilitar o recurso opcional Plataforma de Máquina Virtual. Nosso computador exigirá funcionalidades de virtualização para usar esse recurso.

No PowerShell como administrador execute:
```console
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Vamos reiniciar o computador para concluir a instalação do WSL e a atualização para o WSL 2.

#### Passo 3— Baixar o pacote de atualização do kernel do Linux
Clique neste [link](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) para fazer o download do pacote de atualização do kernel do Linux do WSL 2 para computadores x64. Execute o pacote de atualização baixado e finalize a instalação.

#### Passo 4 — Definir o WSL 2 como a sua versão padrão
Abra o PowerShell e execute este comando para definir o WSL 2 como a versão padrão ao instalar uma nova distribuição do Linux:
```console
wsl --set-default-version 2
```

#### Passo 5 — Instalar a distribuição do Linux de sua escolha
Abra a [Microsoft Store](https://aka.ms/wslstore) e escolha sua distribuição do Linux favorita (Sugiro a 24.04 LTS); realize a instalação e após finalizada, inicie sua distribuição pelo menu iniciar.

#### Passo 6 — Configurações padrão
Na primeira vez que você iniciar uma distribuição do Linux recém-instalada, uma janela de console será aberta e será solicitado que você aguarde um ou dois minutos para que os arquivos sejam descompactados e armazenados em seu PC. Todas as futuras inicializações deverão levar menos de um segundo.

Agora, você precisará criar uma conta de usuário e uma senha para sua nova distribuição do Linux.

Apenas siga os passos solicitados:
![]([/tutorial_metabarcoding/images/fastqc.png](https://miro.medium.com/v2/resize:fit:1100/format:webp/0*qHOWa2UoONeoyI0r.png))


Tudo finalizado!!!
