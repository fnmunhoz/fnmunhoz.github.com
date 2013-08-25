---
author: felipe
comments: true
date: 2011-06-10 01:37:48+00:00
layout: post
slug: deploy-de-aplicacoes-rubyonrails-criando-seus-proprios-pacotes
title: 'Deploy de aplicações RubyOnRails: criando seus próprios pacotes'
wordpress_id: 533
categories:
- devops
tags:
- dev
- devops
- rails
- ruby
---

Devido as necessidades do projeto que estamos trabalhando na [OnCast](http://www.oncast.com.br) começamos uma pesquisa por soluções de deploy para projetos em RubyOnRails.

Estamos usando Rails 3 com Ruby 1.9.2 e para o ambiente de desenvolvimento [RVM](http://rvm.beginrescueend.com) é a melhor solução, pois podemos facilmente alterar a versão do ruby que estamos utilizando.

Entretanto para o ambiente de produção as dificuldades são maiores, e as opções também vamos a elas.



### Pacotes nativos do sistema operacional


Esta seria a solução mais trivial, se nossa aplicação depende do ruby 1.9.2, poderiamos utlizar o apt-get e instalar esta versão através de um comando como esse:
`
$ sudo apt-get install ruby-1.9.2
`
No entanto na maioria das distribuições esta versão recente do ruby não está disponível, no ubuntu 10.10, por exemplo, a última versão disponível é o ruby-1.9.1. 

Além disso muitas outras incompatibilidades acabam aparecendo como versões desatualizadas de outros aplicativos, como o rubygems, por exemplo.

Portanto utilizar os pacotes do sistema operacional se tornou inviável para o nosso caso.



### RVM em produção



Uma alternativa seria então utilizar o RVM, pois desta forma teriamos o controle de qual versão do ruby estariamos utilizando. Para instalar a versão 1.9.2, seria necessário o seguinte comando:
`
# rvm install 1.9.2
`

Utilizar RVM em produção não seria uma péssima escolha, já que no final das contas, o que o RVM faz, é baixar, compilar e instalar o ruby em um ambiente isolado, alterando os paths, permitindo que tenhamos diversas versões do ruby no mesmo sistema e que possamos alternar entre estas versões facilmente.

Entretanto em nosso ambiente de deploy em momento algum precisamos destas capacidades que o RVM nos proporciona, pelo contrário, o RVM acaba trazendo uma certa complexidade ao ambiente.

Por mais que sua utilização seja simples para desenvolvedores ruby que já estão acostumados, pode se tornar um inconveniente para profissionais de outras áreas, como sysadmins, que não necessitam entender do ecossistema do ruby e do rails para instalar a aplicação.

Além disso, o mais comum é instalar o [RVM em modo single-user](http://rvm.beginrescueend.com/rvm/install/) e não para todo o sistema, o que embora possa ser contornado, é uma complexidade a mais a ser resolvida.



### Criando pacotes próprios



Então por que não unir o melhor dos dois mundos? Ter um pacote nativo do sistema operacional com a versão específica que precisamos.

Para atingir esta proposta o [projeto FPM no GitHub](https://github.com/jordansissel/fpm/) facilitando a criação de um pacote nativo para sistema operacional de destino.

Atualmente o FPM tem suporte para os formatos DEB e RPM, dos sistemas baseados em Debian e Red Hat respectivamente.

Existem diversas outras ferramentas que realizam este trabalho, entretanto o objetivo do FPM é tornar isto uma tarefa trivial do ponto de vista dos desenvolvedores ou [DevOps](http://en.wikipedia.org/wiki/DevOps) como está na moda :)

É importante ressaltar que o FPM não é a solução completa, ainda será necessário, no caso do ruby, baixar, e compilar a linguagem, para que depois ela possa ser empacotada com o FPM.

Felizmente estas tarefas podem ser resolvidas utilizando um Makefile como mostram alguns [exemplos no repositório do FPM](https://github.com/jordansissel/fpm/tree/master/examples).

Referências:

[1] [http://goo.gl/sWs3Z](http://goo.gl/sWs3Z)
[2] [https://github.com/jordansissel/fpm](https://github.com/jordansissel/fpm)
[3] [http://www.slideshare.net/fabiokung/ruby-and-rails-packaging-to-production](http://www.slideshare.net/fabiokung/ruby-and-rails-packaging-to-production)
