---
author: felipe
comments: true
date: 2011-04-04 03:34:50+00:00
layout: post
slug: criando-tuneis-seguros-com-ssh
title: Criando túneis seguros com SSH
wordpress_id: 425
---

Criar uma VPN com o OpenVPN, por exemplo, permite que clientes se conectem de forma transparente entre a filial e a matriz de uma empresa. Entretanto existem situações em que uma configuração de tunelamento mais simples pode ser utilizada, através do próprio SSH que normalmente já está instalado em grande parte dos servidores.

Digamos que você queira se conectar no serviço HTTP de um servidor de intranet da empresa que só está disponível dentro da rede da empresa.

Isso pode ser feito através do SSH da seguinte forma:

`
ssh -f -N -L{PORTA_LOCAL}:{IP_DO_SERVIDOR}:{PORTA_DO_SERVICO} {USUARIO}@{IP_DO_SERVIDOR}
`

Onde,

PORTA_LOCAL: será a porta que você irá utilizar para se conectar ao serviço remoto
IP_DO_SERVIDOR: será o endereço IP ou DNS do servidor que será realizada a conexão
PORTA_DO_SERVICO: será a porta do serviço que desejamos nos conectar
USUARIO: Usuário SSH válido do servidor 

Por exemplo, para acessar o serviço **HTTP** do servidor **intranet.lan**
utilizando a porta local 5000, o comando seria o seguinte:

`
ssh -f -N -L5000:intranet.lan:80 user@intranet.lan
`

A partir de agora a intranet remota estará disponível para acesso através do endereço http://localhost:5000/
da máquina que originou o tunelamento.

Outro exemplo poderia ser a criação do Túnel para a utilização de um proxy:

`
ssh -f -N -L3128:proxy.lan:3128 user@proxy.lan
`

Com esta configuração bastaria que o navegador fosse apontado para o proxy em localhost:3128 e todo tráfego do navegador seria redirecionado para o proxy através do tunelamento criado. 

