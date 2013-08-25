---
author: felipe
comments: true
date: 2010-11-22 01:08:00+00:00
layout: post
slug: script-de-backup-simples-para-linux
title: Script de backup simples para linux
wordpress_id: 107
---


    

O script de backup abaixo, utiliza o aplicativo tar para criar uma copia compactada do diretorio /var/www dentro do diretorio /mnt/backup. Para diferenciar o arquivo de backup de outros backups desse mesmo diretorio e adicionada a data atual no nome do arquivo de backup.




#!/bin/bash  
DATA=`date +%Y-%m-%d-%H-%M`  
cd /mnt/backup  
tar -zcvf sites-"$DATA".tar.gz /var/www/


  
