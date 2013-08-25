---
author: felipe
comments: true
date: 2010-09-18 12:58:00+00:00
layout: post
slug: configurando-o-arquivo-etchosts-para-facilitar-a-comunicacao-entre-os-servidores
title: Configurando o arquivo /etc/hosts para facilitar a comunicação entre os servidores
wordpress_id: 122
---


    

O arquivo `/etc/hosts` faz o relacionamento entre um nome de computador e endereço IP local. Recomendado para IPs constantemente acessados e para colocaçao de endereços de virtual hosts (quando deseja referir pelo nome ao inves de IP). A inclusao de um computador neste arquivo dispensa a consulta de um servidor de nomes para obter um endereço IP, sendo muito util para maquinas que sao acessadas frequentemente. 




No caso de um ambiente de testes com maquinas virtuais pode ser configurado este arquivo para facilitar o acesso entre os servidores, nao necessitando digitar o endereço IP e sim o proprio nome do servidor.




  
A configuraçao deste arquivo e bem simples, sendo que cada linha representa um mapeamento IP => nome, desta forma basta inserir os IPs de cada servidor e o seu nome correspondente separados por espaço, como no exemplo abaixo:




-------------------------------------------------------  
127.0.0.1  localhost  
192.168.0.101  ubuntu-server-vm1  
192.168.0.102  ubuntu-server-vm2  
-------------------------------------------------------




A partir de agora voce pode acessar qualquer um destes servidores da seguinte forma:




# ssh uservm1@ubuntu-server-vm1




em vez de:




# ssh [uservm1@192.168.0.101](mailto:uservm1@192.168.0.101)




Referencia: [http://focalinux.cipsga.org.br/guia/avancado/ch-rede.htm](http://focalinux.cipsga.org.br/guia/avancado/ch-rede.htm)





  
