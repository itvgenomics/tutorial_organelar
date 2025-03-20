---
title: "Acessando o servidor"
layout: archive
permalink: /access_server/
---  

Você pode acessar o servidor Biotec02 de uma máquina Windows, Linux ou Mac.

### Windows

Para acessar o servidor no sistema operacional Windows, digite "Power Shell" no seu Menu Iniciar e abra um terminal, conforme a imagem abaixo:
![](/tutorial_metabarcoding_v3/images/powershell_iniciar.png)

### Ubuntu e Mac OS

Para acessar o servidor no Ubuntu ou Mac OS, abra um terminal normalmente.

### Acesse o servidor via SSH

No terminal, digite o seguinte comando, substituindo <seu_usuário> pelo usuário que lhe foi designado.

```console
ssh -p 59020  <seu_usuário>@biotec02.esalq.usp.br
```

Digite a senha quando for pedido. Se for seu primeiro acesso, você deverá mudar a senha.
