---
author: felipe
comments: true
date: 2011-03-28 00:55:33+00:00
layout: post
slug: configurando-o-openvpn-utilizando-chaves-estaticas
title: Configurando o OpenVPN utilizando chaves estáticas
wordpress_id: 396
---

Com o OpenVPN instalado, acesse o diretório de configurações:

`cd /etc/openvpn`

Em seguida deve ser gerada a chave de encriptação que será utilizada para a configuração, da seguinte forma:

`openvpn --genkey --secret static.key`

Foi criado o arquivo /etc/openvpn/static.key, esse arquivo deve estar presente tanto no cliente quanto no servidor, portanto copie o arquivo para a outra máquina, na qual será realizada a configuração. A cópia pode ser feita por SSH, por exemplo, mas lembre-se que esta é a chave que garante a segurança da VPN, sendo que em uma situação real esta chave deve ser transmitida de forma segura.

Com a chave presente nos dois equipamentos (cliente e servidor) devem ser criados os arquivos para a configuração e inicialização da VPN.

No servidor crie um arquivo chamado server.conf em /etc/openvpn com o seguinte conteúdo:

`
dev tun
ifconfig 10.0.0.1 10.0.0.2
secret static.key
`

No cliente crie um arquivo chamado client.conf em /etc/openvpn com o seguinte conteúdo:

`
remote 192.168.0.106
dev tun
ifconfig 10.0.0.2 10.0.0.1
secret static.key
`

Lembre-se de substituir no cliente a configuração "remote" pelo endereço IP do seu servidor.

Agora para que as configurações entrem em vigor, é necessário que o serviço seja reinicializado tanto no servidor quanto no cliente. Isto pode ser feito da seguinte forma:

`/etc/init.d/openvpn restart`

Para verificar se a configuração foi realizada com sucesso, pode ser executado o comando ipconfig, confirmando que as interfaces 'tun' da VPN foram realmente criadas.




