---
author: felipe
comments: true
date: 2010-11-14 17:14:00+00:00
layout: post
slug: copiando-arquivos-via-ssh
title: Copiando arquivos via SSH
wordpress_id: 108
---


    

O serviço SSH alem de permitir a execuçao de comandos remotamente, possibilita tambem a copia de arquivos de forma bastante simples e poderosa.




A sintaxe basica e a seguinte:




# scp teste.txt login@servidor:/tmp




Este comando ira realizar a copia de um arquivo local 'teste.txt' para o diretorio '/tmp' do servidor remoto.




É possivel tambem o contrario, isto e, copiar arquivos do servidor remoto para o diretorio atual:




# scp login@servidor:/tmp/teste2.txt $HOME





  
