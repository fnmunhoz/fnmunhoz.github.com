---
author: felipe
comments: true
date: 2011-04-09 21:10:12+00:00
layout: post
slug: configurando-o-servidor-ssh
title: Configurando o servidor SSH
wordpress_id: 435
---

O arquivo de configuração do servidor SSH no debian fica localizado no seguinte path:

`/etc/ssh/sshd_config`

É importante não confundir com o arquivo de configuração do cliente SSH que é bastante parecido:

`/etc/ssh/ssh_config`

A diferença é somente que o arquivo do servidor tem uma letra 'd' a mais, salientando que é o arquivo de configuração do servidor (daemon).

**Port**

A porta padrão de acesso ao SSH é a 22, entretanto esta porta pode ser alterada para outra sua preferência, por exemplo a 2222.

Uma das principais razões de alterar a porta default do SSH é para os casos onde o servidor SSH está exposto para a internet, e devido a porta padrão ser a 22 ela é muita visada por tentativas de invasão. Alterar a porta padrão para uma porta menos visada, já diminuirá bastante as tentativas.

`Port 14344`

**ListenAdrress**

É possível especificar em quais endereços IP o servidor SSH escutará por conexões. Um caso típico são os servidores com mais de uma placa de rede, uma externa e outra conectada somente a rede local. Utilizando esta opção é possível bloquear o acesso externo mesmo sem a utilização de um firewall.

Por exemplo, digamos que a placa eth0 está ligada a internet com o IP 200.132.10.10 e a placa eth1 está ligada a rede interna 192.168.0.20, para limitar o acesso SSH somente a rede interna a configuração seria:

`ListenAddress 192.168.0.20`

**Protocol**

É possível escolher quais versões do protocolo SSH serão suportadas pelo servidor, atualmente a versão amplamente utilizada é a versão 2, já que a versão 1 possui diversos problemas de segurança conhecidos.

`Protocol 2`


**PermitRootLogin**

Esta opção é muito importante, já que ela define se o login por SSH através do usuário root será permitido ou não. É uma boa prática de segurança desabilitar o login do usuário root, já que além do usuário root ser conhecido previamente, pois todo linux possui um, se o invasor conseguir acesso através do root terá acesso completo ao sistema, inclusive poderes administrativos.

É mais interessante desabilitar esta configuração e realizar o login utilzando outro usuário do sistema e depois sim autenticando-se como root através do 'su' ou 'sudo'.

`PermitRootLogin no`

**AllowUsers**

Por padrão o SSH é configurado para permitir o login de qualquer usuário válido do sistema, através da configuração AllowUsers é possível restringir o login somente para alguns usuários. Por exemplo, para somente permitir o acesso aos usuários paulo e renato, a configuração é a seguinte:

`AllowUsers paulo renato`

**DenyUsers**

Para inverter a lógica e em vez de liberar o acesso somente para alguns usuários, pode ser utilizada a opção DenyUsers para negar o login somente para alguns usuários.

`DenyUsers marcus`

**PermitEmptyPasswords**

A opção PermitEmptyPasswords quando configurada para 'no' faz que qualquer conta do sistema sem senha seja automaticamente desabilitada. Isso evita que usuários desavisados ao criarem ou alterarem suas contas criem uma brecha de segurança no sistema.

`PermitEmptyPasswords no`

**Banner**

É possível apresentar uma mensagem ao usuário antes de liberar o acesso do usuário ao sistema, por exemplo, para informar que a conexão está sendo monitorada. Isto pode ser feito especificando um arquivo onde a mensagem será armazenada através da opção Banner:

`Banner = /etc/ssh/banner.txt`

**X11Forwarding**

É possível permitir que os clientes executem aplicações gráficas através do SSH, configurando esta opção para 'yes'.

`X11Forwarding yes`
