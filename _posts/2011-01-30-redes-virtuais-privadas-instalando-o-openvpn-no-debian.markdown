---
author: felipe
comments: true
date: 2011-01-30 00:16:26+00:00
layout: post
slug: redes-virtuais-privadas-instalando-o-openvpn-no-debian
title: 'Redes Virtuais Privadas: Instalando o OpenVPN no Debian'
wordpress_id: 236
---

O [OpenVPN](http://www.openvpn.net/) é uma solução de VPN open source sob a licença [GNU GPL](http://pt.wikipedia.org/wiki/GNU_General_Public_License) e multiplataforma podendo ser utilizado nos seguintes sistemas operacionais: Solaris, Linux, OpenBSD,FreeBSD, NetBSD, Mac OS X, e Windows 2000/XP/Vista.

A instalação no debian via apt-get é bastante simples:

`# apt-get install openvpn`

Após a instalação já pode ser criado um túnel simples, não encriptado, usando os comandos abaixo em um dos lados da VPN:

`# openvpn --remote 192.168.0.1 --dev tun0 --ifconfig 10.0.0.1 10.0.0.2`

O mesmo deve ser feito no outro lado da conexão invertendo o endereço IP ao final:

`# openvpn --remote 192.168.0.200 --dev tun0 --ifconfig 10.0.0.2 10.0.0.1`

Neste momento a conexão pela VPN já está estabelecida, execute o comando ifconfig e verifique se foi criada a conexão tun0 indicada nos comandos acima.

Execute um ping para os endereços IP da VPN criada para verificar se responde normalmente.

Na verdade a conexão acima não pode ser considerada uma VPN pois está utilizando um canal de comunicação aberto, sem criptografia. Veremos como configurar o OpenVPN para utilizar canais criptografados em um próximo post.
