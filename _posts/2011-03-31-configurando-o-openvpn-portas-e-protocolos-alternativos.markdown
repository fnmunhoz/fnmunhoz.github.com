---
author: felipe
comments: true
date: 2011-03-31 21:47:32+00:00
layout: post
slug: configurando-o-openvpn-portas-e-protocolos-alternativos
title: 'Configurando o OpenVPN: portas e protocolos alternativos'
wordpress_id: 413
---

Por padrão o OpenVPN escuta na porta 1194 utilizando o protocolo TCP. É possível alterar tanto a porta de escuta quanto o protocolo utilizado.

As configurações devem ser realizadas nos arquivos de configuração (.conf) de cada VPN criada, tanto nos clientes quanto no servidor.

Para especificar em qual porta o OpenVPN escutará a opção é a seguinte:

**port 12333**

Para alterar para o protocolo UDP a configuração é a seguinte:

**proto udp**

A vantagem em utilizar o protocolo UDP em vez do TCP é devido à sobrecarga desnecessária que o TCP implica. Como o protocolo TCP controla o tratamento de erros na transmissão de pacotes, ele acaba realizando uma verificação extra nos pacotes, já que os protocolos que serão utilizados através da VPN já fazem isso, como por exemplo o HTTP.


