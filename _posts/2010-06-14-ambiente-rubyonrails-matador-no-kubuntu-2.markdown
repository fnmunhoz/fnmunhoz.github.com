---
author: felipe
comments: true
date: 2010-06-14 02:47:30+00:00
layout: post
slug: ambiente-rubyonrails-matador-no-kubuntu-2
title: Ambiente RubyOnRails no Kubuntu [2]
wordpress_id: 86
categories:
- desenvolvimento
- rails
- tecnologia
tags:
- desenvolvimento
- rails
---

No [post anterior](http://blog.felipemunhoz.com/2010/06/14/ambiente-rubyonrails-matador-no-kubuntu-1/) foi configurado o ambiente para o rails 3. Neste post vamos para a instalação da IDE.

Seguindo os princípios definidos nos [requisitos do ambiente de desenvolvimento](http://blog.felipemunhoz.com/2010/06/13/requisitos-do-ambiente-de-programacao/) optei pela IDE desenvolvida pela [Aptana](http://aptana.org/).

A versão estável é a radrails 2, entretanto optei pela versão beta Aptana Studio 3 que será a versão da IDE com suporte para o Rails 3  (que no momento que escrevo este post também encontra-se em estágio beta).

Para realizar o download vá [nesta página](http://aptana.org/products/studio3/download) e escolha a versão desejada. Ou baixe diretamente a versão para linux 32 bits [neste link](http://download.aptana.com/studio3/standalone/3.0.0/linux/Aptana_Studio_3_Setup_Linux_x86_3.0.0.zip).

Vá até a pasta de download e descompacte os arquivos no diretório criado abaixo.

    
    cd ~
    mkdir -p dev/ides/studio3
    mkdir -p dev/workspaces/studio3
    cd Downloads
    unzip Aptana_Studio_3_Setup_Linux_x86_3.0.0.zip
    mv Aptana\ Studio\ 3/* ~/dev/ides/studio3/


Se desejar crie um atalho no menu do KDE para o Studio 3.

Abra o Studio 3 e altere o workspace para a pasta ~/dev/workspaces/studio3

Pronto IDE instalada!
