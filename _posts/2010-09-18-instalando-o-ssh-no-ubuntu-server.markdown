---
author: felipe
comments: true
date: 2010-09-18 12:36:00+00:00
layout: post
slug: instalando-o-ssh-no-ubuntu-server
title: Instalando o SSH no Ubuntu Server
wordpress_id: 123
---


    

O [SSH](http://www.openssh.com/) e uma das ferramentas dos sistemas operacionais Unix mais uteis no dia-a-dia, permitindo administrar os servidores remotamente e com segurança.




Caso o sistema operacional esteja instalado em um servidor de maquinas virtuais como o VirtualBox, o SSH tambem sera muito util, pois nao sera mais preciso utilizar o console do VirtualBox para acessar o sistema operacional. Tudo podera ser feito via SSH.




A instalaçao do servidor SSH no Ubuntu Server e extremamente simples atraves do gerenciador de pacotes apt-get.




# sudo apt-get install ssh




Pronto atraves desta instalaçao padrao o SSH esta funcionando e escutando na porta 22. Nao esqueça de definir uma boa senha para os usuarios!


  
