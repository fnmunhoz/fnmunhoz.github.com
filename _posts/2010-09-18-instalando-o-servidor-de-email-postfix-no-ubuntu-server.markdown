---
author: felipe
comments: true
date: 2010-09-18 11:11:00+00:00
layout: post
slug: instalando-o-servidor-de-email-postfix-no-ubuntu-server
title: Instalando o servidor de email Postfix no Ubuntu Server
wordpress_id: 124
---


    

O [Postfix](http://www.postfix.org/) e um servidor de email simples de configurar para os casos mais comuns, tem uma boa performance e um historico de segurança bastante aceitavel, alem de abranger diversas situaçoes de uso e configuraçoes. Alem disso existe muita documentaçao na internet sobre ele, ja que e um dos mais usados em servidores linux.




Instalando o Posfix




Instalar o Postfix no Ubuntu e muito facil atraves do gerenciador de pacotes apt-get. Execute o seguinte no terminal:




Atualizando a lista de pacotes dos repositorios




# sudo apt-get update




Instalando o pacote do postfix




# sudo apt-get install postfix




Durante a instalaçao sera executado um wizard para uma configuraçao basica do postfix, conforme a sequencia de imagens a seguir




[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/09/postfix-1.png.scaled500-300x260.png)](http://posterous.com/getfile/files.posterous.com/temp-2010-09-18/GarcnbkGrmprxbupnnxdrgswvolxtoBkAngvznpoAnqhjgsbctgxqgEhiuuB/postfix-1.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/09/postfix-2.png.scaled1000-300x246.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/09/postfix-2.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/09/postfix-3.png.scaled1000-300x246.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/09/postfix-3.png.scaled1000.png)


[See and download the full gallery on posterous](http://blog.felipemunhoz.com/instalando-o-servidor-de-email-postifix-no-ub)




Neste wizard sao feitas duas perguntas:






  * A primeira pergunta e sobre a funçao que tera este servidor, sendo que "Internet Site" e a opçao mais usada. Nesta configuraçao e instalado um servidor que envia e recebe emails diretamente. É possivel utilizar outras formas de configuraçao como "Internet with Smarthost" sendo que nesta configuraçao o servidor apenas recebe mensagens mas nao envia, sendo que a funçao de enviar os emails e delegada a outro servidor de emails.




  * A segunda pergunta, diz respeito ao dominio que sera utilizado nas mensagens enviadas pelo servidor. Caso possua um dominio registrado, este deve ser utilizado caso contrario defina um proprio.







Estas sao as configuraçoes basicas que permitem o servidor de email funcionar. Apos estas perguntas a instalaçao termina e o servidor esta funcionando.


  
