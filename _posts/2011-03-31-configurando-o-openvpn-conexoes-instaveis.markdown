---
author: felipe
comments: true
date: 2011-03-31 22:01:14+00:00
layout: post
slug: configurando-o-openvpn-conexoes-instaveis
title: 'Configurando o OpenVPN: conexões instáveis'
wordpress_id: 419
---

Um problema muito comum na utilização de VPNs é a utilização de conexões muito instáveis, como por exemplo, ADSLs ou 3G. Qualquer interrupção que ocorra na transmissão a VPN ficara off-line, sendo necessária uma intervenção de um administrador.

Para tratar este tipo de situação o OpenVPN possui uma série de configurações que permitem o reestabelecimento da conexão. A seguir uma descrição de cada um deles.

**keepalive 10 60**

A configuração keepalive permite que a conexão seja reiniciada caso não ocorra resposta dentro de um determinado período.

O primeiro número especifíca o intervalo, em segundos, de pings e o segundo o timeout. Após o timeout a VPN é automaticamente reiniciada. Caso a conexão não seja reestabelecida na primeira tentativa o OpenVPN tenta reconectar até tenha sucesso.

**inactive 3600**

A configuração inactive serve para especificar um tempo em segundos para que as tentativas de conexão sejam mantidas. No exemplo acima após 1 hora sem sucesso na conexão, o OpenVPN pára com as tentativas.

**comp-lzo**

A opção comp-lzo faz com que o OpenVPN passe a compactar os dados transmitidos através da VPN. O algoritmo utilizado é bastante leve, e portanto não será um grande empecilho com relação ao desempenho do processamento do servidor ou do cliente. 

**persist-key**
**persist-tun**

As opções de configuração persist-key e persist-tun fazem com que o OpenVPN mantenha tanto a interface de tunelamento quanto as chaves carregadas em memória, tornando o reestabelecimento da conexão mais rápido nos casos de queda. 

**float**

A opção float é bastante útil quando se utiliza conexões com IP dinâmico. Desta forma ao trocar o IP a conexão é reestabelecida da mesma forma. Essa situação é muito comum quando se utiliza serviços de DNS dinâmico como NoIP por exemplo. 



