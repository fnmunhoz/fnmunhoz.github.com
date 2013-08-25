---
author: felipe
comments: true
date: 2010-06-14 01:16:31+00:00
layout: post
slug: ambiente-rubyonrails-matador-no-kubuntu-1
title: Ambiente RubyOnRails no Kubuntu [1]
wordpress_id: 75
categories:
- desenvolvimento
- rails
- tecnologia
tags:
- desenvolvimento
- rails
---

Apresento abaixo meu ambiente de desenvolvimento RubyOnRails para minha referência futura ou para quem se interessar :)

A configuração descrita será para o Kubuntu 10.4, mas não deve ser muito diferente para outras distribuições.

Depois de seguir alguns tutoriais sobre como configurar o ambiente RubyOnRails e ter o ambiente funcionando, vi que algo muito importante é poder trabalhar com diversas versões do ruby e do rails.

Entretanto, ao instalar mais de uma versão no mesmo ambiente em pouco tempo temos um ambiente confuso de se trabalhar e de descobrir qual versão de cada software está sendo utilizada ( ruby 1.8, ruby enterprise, jruby, etc). A situação piora quando quando começam a ser instaladas as GEMs para cada uma das versões. É fácil perceber que o ambiente se torna caótico facilmente.

Como a comunidade ruby não gosta de confusão existe uma solução muito elegante para se trabalhar com quantas versões do ruby, do rails e das gems forem necessárias.

O projeto chama-se [RVM](http://rvm.beginrescueend.com/) Ruby Version Manager, que trata-se de um script de linha de comando que permite a instalação e o gerenciamento de multiplas instalações do Ruby, cada uma com seu conjunto de gems isoladas umas das outras.

Para instalar o RVM siga os seguintes passos:

    
    sudo apt-get install curl libreadline-dev
    bash <


Adicione a linha abaixo no final do seu arquivo .bashrc

    
    [[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"


Agora basta fechar o terminal e abrir novamente e você terá uma interface para a instalação e o gerenciamento de quantas versões do ruby quiser! E o melhor funcionando independentes umas das outras, sem interferir inclusive em outras versões que já tiverem sido instaladas para o sistema. Além disso esse ambiente fica disponível apenas para o seu usuário, já que tudo é instalado dentro do seu diretório pessoal ( $HOME/.rvm/ ).

**O que pode ser instalado com o RVM**

Certo o RVM está instalado, mas agora que versão do ruby pode ser instalada? Para saber as principais execute:

    
    rvm list known


Esta lista apresenta apenas algumas das versões que podem ser instaladas, já que o RVM está preparado para baixar e compilar os rubies ( como são chamadas as versões pelo rvm ) diretamente do site ou dos repositórios oficiais. Teoricamente você pode instalar qualquer versão disponibilizada.

**Instalando alguns pacotes de dependência**

Esta etapa somente é necessária para utilizar a gem [heroku](http://heroku.com/)

    
    rvm package install readline



    
    rvm package install openssl


**Instalando o Ruby 1.9.2 e o Rails 3**

Vamos instalar o ruby 1.9.2 que é a versão do ruby que oferece suporte ao Rails 3:

Caso queira ter suporte ao readline e openssl instale da seguinte forma:

    
    rvm install 1.9.2-head -C --with-openssl-dir=$HOME/.rvm/usr,--with-readline-dir=$HOME/.rvm/usr



    
    Caso contrário apenas execute:



    
    rvm install 1.9.2-head


Agora crie um gemset específico para a instalação de gems para o Rails 3 da seguinte forma:

    
    rvm --create --default use 1.9.2-head@rails3


Em seguida instale a versão beta do rails 3

    
    gem install rails --pre


Pronto, para confirmar que versão do rails está sendo utilizada execute:

    
    rails --version


Se desejar instale o heroku

    
    gem install heroku


É isso última versão do rails instalado. Agora é escolher e configurar uma IDE e sair programando :)
