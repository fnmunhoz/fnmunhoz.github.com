---
author: felipe
comments: true
date: 2010-09-12 15:16:00+00:00
layout: post
slug: instalando-o-gerenciador-de-maquinas-virtuais-virtualbox
title: Instalando o gerenciador de máquinas virtuais VirtualBox
wordpress_id: 126
---

Neste tutorial vamos mostrar como instalar o gerenciador de máquinas virtuais [VirtualBox](http://www.virtualbox.org/) no [Ubuntu](http://www.ubuntu.com) 10.04 32 bits.

Baixando o VirtualBox

Vá até a [página de downloads do VirtualBox para Linux](http://www.virtualbox.org/wiki/Linux_Downloads) e baixe a versão correspondente ao Ubuntu 10.04 i386.

Instalando o VirtualBox

Abra o terminal e vá até o diretório onde foi salvo o pacote .deb e instale o mesmo utilizando o comando dpkg com sudo.

$ sudo dpkg -i virtualbox-3.2_3.2.8-64453~Ubuntu~lucid_i386.deb

$ apt-get -f install

Aguarde alguns minutos para que a instalação termine.

Iniciando o VirtuaBox

Ainda no terminal execute o comando "VirtualBox" para inicializar.

$ ./VirtualBox

Será apresentada uma tela com a licença de uso, arraste a barra de rolagem até o final e aceite a licença para prosseguir.

[![](/images/instalando-o-gerenciador-de-maquinas-virtuais-virtualbox/virtualbox-1.png.scaled500-300x225.png)](/images/instalando-o-gerenciador-de-maquinas-virtuais-virtualbox/virtualbox-1.png.scaled500.png)

Em seguida aparecerá a tela inicial do VirtualBox, conforme imagem a seguir.

[![](/images/instalando-o-gerenciador-de-maquinas-virtuais-virtualbox/virtualbox-2.png.scaled1000-300x214.png)](/images/instalando-o-gerenciador-de-maquinas-virtuais-virtualbox/virtualbox-2.png.scaled1000.png)


Pronto o VirtualBox está instalado, o próximo passo é configurar uma máquina virtual, o que será mostrado no próximo tutorial.
