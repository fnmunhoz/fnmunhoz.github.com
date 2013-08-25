---
author: felipe
comments: true
date: 2010-11-14 17:07:00+00:00
layout: post
slug: configurando-o-servidor-ssh-para-utilizar-chaves-de-autenticacao
title: Configurando o servidor SSH para utilizar chaves de autenticação
wordpress_id: 109
---




O serviço SSH utiliza por padrao a autenticaçao por senha, entretanto sempre existe uma pequena possibilidade de que um atacante descobrir esta senha de alguma forma, utilizando [engenharia social](http://www.slideshare.net/fnmunhoz/engenharia-social-3590818) por exemplo.




Para resolver este problema o SSH oferece uma soluçao, atraves do uso de chaves de autenticaçao, utilizando uma chave publica e uma chave privada.




A chave publica e instalada nos servidores que serao acessados e a chave privada permanece somente no cliente com permissao para acessar os servidores, conforme imagem a seguir:![](/images/configurando-o-servidor-ssh-para-utilizar-chaves-de-autenticacao/ssh_rsa_identity.gif.scaled500-278x300.gif)





Caso o servidor SSH nao esteja instalado, veja [Instalando o SSH no Ubuntu Server](http://blog.felipemunhoz.com/instalando-o-ssh-no-ubuntu-server).







Para gerar esse par de chaves, execute no cliente o seguinte comando:




# ssh-keygen -t rsa




Este comando deve ser executado usando o login de usuario que sera utilizado para acessar o servidor SSH, caso contrario a autenticaçao nao vai funcionar.




Escolha as opçoes padrao para geraçao da chave, basta teclar 'enter'. Desta forma sera gerada a chave no diretorio $HOME/.ssh/ com o nome padrao 'id_rsa' (chave privada) e 'id_rsa.pub' (chave publica) e utilizando uma passphrase em branco.




É muito importante proteger o arquivo da chave privada (id_rsa) pois qualquer um que tiver acesso a este arquivo podera utilizar sua chave para se autenticar em um servidor de forma indevida.




Mantenha as permissoes desse arquivo com "600".




# chmod 600 $HOME/.ssh/id_rsa




Em seguida deve ser feita a copia da chave publica para o servidor permitindo que ela seja utilizada para autenticaçao




# ssh-copy-id -i ~/.ssh/id_rsa.pub usuario@servidor




Desta forma voce ja pode se autenticar no servidor SSH remoto sem necessitar de senha, basta o seguinte:




# ssh suario@servidor






