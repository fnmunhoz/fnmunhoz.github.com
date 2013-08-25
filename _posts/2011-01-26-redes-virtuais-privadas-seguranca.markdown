---
author: felipe
comments: true
date: 2011-01-26 22:38:17+00:00
layout: post
slug: redes-virtuais-privadas-seguranca
title: 'Redes Virtuais Privadas: Segurança'
wordpress_id: 213
---

Uma característica importante e **fundamental** destas redes virtuais é que os dados que trafegam através dela são **encriptados**, o que reduz o problema dos dados estarem trafegando pela internet. Mesmo que alguém mal intencionado capture estes dados não conseguirá distinguir do que se trata.

É claro que não eliminamos as chances de um invasor tirar proveito da situação. Pode acontecer que por uma falha de segurança em um dos servidores da VPN o invasor consiga acesso ao mesmo, e consequentemente as chaves de encriptação da VPN, conseguindo desta forma decodificar as informações. Mas se o administrador se precaver e ter uma VPN com servidores bem configurados, as chances de isso acontecer são realmente baixas.

Existe uma probabilidade bem maior que através de [engenharia social](http://www.slideshare.net/fnmunhoz/engenharia-social-3590818) o invasor consiga acesso a rede através de um funcionário da empresa ingênuo que envie informações para fora da empresa, do que um invasor que consiga acesso diretamente.
