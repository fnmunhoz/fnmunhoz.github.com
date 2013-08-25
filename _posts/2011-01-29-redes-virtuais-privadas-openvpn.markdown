---
author: felipe
comments: true
date: 2011-01-29 12:44:51+00:00
layout: post
slug: redes-virtuais-privadas-openvpn
title: 'Redes Virtuais Privadas: OpenVPN'
wordpress_id: 227
---

O OpenVPN é uma solução de VPN de código aberto, bastante simples de configurar comparado a outras soluções e também seguro.

Possui versões para Linux e Windows podendo conectar via VPN com clientes utilizando os dois sistemas operacionais. Outra característica interessante é que ele pode ser usado por clientes conectados através de NAT, já que apenas o servidor necessita de portas abertas.

Além disso, possui uma boa tolerância a falhas na conexão bem como conexões com IP dinâmico, já que a VPN pode ser configurada para ser automaticamente reestabelecida em caso de queda na conexão.

O OpenVPN pode ser configurado para utilizar chaves estáticas, que oferecem um nível mediano de segurança, no entanto a configuração é bem mais simples.

Para obter uma configuração mais segura podem ser utilizados certificados X509, apesar de desta forma a configuração ser mais complexa.

A decisão deve ser tomada levando em conta se é preferível maior praticidade ou maior segurança.
