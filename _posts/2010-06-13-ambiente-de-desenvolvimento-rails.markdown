---
author: felipe
comments: true
date: 2010-06-13 21:20:45+00:00
layout: post
slug: ambiente-de-desenvolvimento-rails
title: Ambiente de Desenvolvimento Rails
wordpress_id: 69
---

O mundo das aplicações caminha cada vez mais para a WEB, aplicações Desktop ainda são amplamente utilizadas, mas a tendência é que sejam migradas para a WEB em sua maioria. Neste sentido a minha escolha do ambiente de desenvolvimento tem foco na WEB, indepentende do tipo de dispositivo que irá acessar a aplicação ( PCs, notebooks, netbooks, smartphones, geladeiras?) ela deve estar preparada e atender de forma satisfatória.

De acordo com os [requisitos](http://blog.felipemunhoz.com/2010/06/13/requisitos-do-ambiente-de-programacao/) que defini como básicos nos meus estudos para um ambiente de desenvolvimento, o rails cumpre até agora todos eles de forma bastante interessante. Vamos a eles:



	
  * Open Source

	
  * Multiplaforma (Linux, Windows, MacOS, Android)

	
  * Bem documentado

	
  * Comunidade ativa

	
  * Ferramentas que agilizem o desenvolvimento de aplicações

	
  * Possua diversas opções de IDEs

	
  * Utilizar controle de versão


**Open Source**

Tanto a linguagem [Ruby](http://ruby-lang.org/) na qual o [RubyOnRails](http://rubyonrails.org/) foi criado quanto o próprio framework são softwares open source, portanto livres de qualquer tipo de licença que impeçam a sua utilização. Você pode utilizá-lo e distribuí-lo sem restrições. Veja a [licença da linguagem Ruby](http://www.ruby-lang.org/en/LICENSE.txt) e a [licença do framework RubyOnRails](http://www.opensource.org/licenses/mit-license.php)

**Multiplataforma**

O Ruby é altamente portável: é desenvolvido principalmente em ambiente GNU/Linux, mas trabalha em muitos tipos de ambientes UNIX, Mac OS X, Windows 95/98/Me/NT/2000/XP, DOS, BeOS, OS/2, etc.
E o framework RubyOnRails por consequência herda todas essas características de portabilidade.

**Bem documentado**

Uma das características mais marcantes de ruby e rails é a legibilidade de código. Parece que os programadores dessa linguagem tem alergia código ilegível. É notavel a qualidade da documentação produzida para o framework, seja através de textos, screencasts, podcasts, ou até mesmo palestras que os programadores da linguagem produzem. Parece ser o grande marketing do comunidade rails, demostrar as suas vantagens de forma clara e incentivadora para que outros programadores se convertam :).

**Comunidade ativa**

Como dito no tópico anterior a comunidade de ruby e de rails é que mantém e tem dado toda essa visibilidade a linguagem e ao framework. A comunidade é o ponto muito forte. Se há espaço para uma piada é que a explicação para tanta documentação de qualidade é porque programador RubyOnRails tem tempo para documentar já que a linguagem faz boa parte do trabalho pesado :P. Java algúem?

**Ferramentas que agilizem o desenvolvimento de aplicações**

Quando não estão documentando seus achados sobre RubyOnRails os programadores estão desenvolvendo ferramentas para diminuir a quantidade de tarefas necessárias durante o desenvolvimento. Essas ferramentas vão desde geradores de código automatizados até o desenvolvimento de plugins e bibliotecas ( chamados de gems ) reutilizaveis entre diversas aplicações. E o mais legal é que muitas dessas gems senão a maioria são open source :)

**Possua diversas opções de IDEs**

Essa provavelmente é a discussão mais polêmica, já que é questão de gosto, mas os programadores rails em sua maioria programam em MacOS X utilizando o [TextMate](http://macromates.com/) como IDE. Entretanto essa é só uma das opções, e a desvantagem que vejo nela é que só funciona no MacOS X e como (ainda) não tenho um procuro uma IDE multiplataforma de acordo com os requisitos que já citei acima. Nesta perspectiva de uma IDE multiplataforma e que suporte Rails o [Aptana](http://aptana.org/) tem me agradado bastante, principalmente por ser baseado no [Eclipse](http://www.eclipse.org) que já tenho familiaridade, podendo inclusive ser instalado como um plugin.

**Utilizar controle de versão**

Até hoje venho utilizando o [Subversion](http://subversion.tigris.org/) como software de controle de versão. Atende bem as minhas necessidades, mas estou bastante inclinado a utilizar um [sistema de controle de versão distribuído](http://en.wikipedia.org/wiki/Distributed_revision_control) como o [GIT](http://git-scm.com/).
