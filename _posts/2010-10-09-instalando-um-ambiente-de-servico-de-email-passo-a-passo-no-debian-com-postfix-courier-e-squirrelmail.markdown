---
author: felipe
comments: true
date: 2010-10-09 13:15:00+00:00
layout: post
slug: instalando-um-ambiente-de-servico-de-email-passo-a-passo-no-debian-com-postfix-courier-e-squirrelmail
title: Instalando um Ambiente de Serviço de Email Passo a Passo no Debian com Postfix,
  Courier e Squirrelmail
wordpress_id: 114
---


    

Este tutorial ira demonstrar os passos necessarios para a instalaçao e configuraçao de um ambiente de serviço de email em sistemas Debian-based, utilizando os softwares Postfix como servidor SMTP, Courier como servidores POP3 e IMAP e Squirrelmail como webmail.




Instalando o Servidor SMTP Postfix




A instalaçao do servidor SMTP postfix e simples atraves do apt-get:




# apt-get install posfix




Durante a instalaçao sera apresentado um wizard para a definiçao das configuraçoes principais.




Na primeira delas deve ser informado o perfil do servidor que esta sendo instalado. Neste tutorial sera utilizada a opçao _"Internet site" _que permite ao servidor enviar e receber emails diretamente.




A segunda pergunta refere-se a configuraçao "mail name" que sera o dominio inserido nas mensagens enviadas, para os testes pode ser um dominio qualquer, por exemplo dominiolocal.lan




Apos estes dois passo o servidor esta configurado e funcionando para as situaçoes mais basicas.




Configurando o Postfix




O arquivo de configuraçao principal do postfix e o main.cf e no debian fica localizado no diretorio /etc/postfix.




Edite este arquivo de forma que ele tenha pelo menos as opçoes abaixo, de acordo com as configuraçoes de dominio do sistema operacional instalado.




myhostname = debian1.dominiolocal.lan  
alias_maps = hash:/etc/aliases  
alias_database = hash:/etc/aliases  
myorigin = /etc/mailname  
mydestination = dominiolocal.lan, debian1.dominiolocal.lan, localhost.dominiolocal.lan, localhost  
relayhost =   
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128  
mailbox_command = procmail -a "$EXTENSION"  
mailbox_size_limit = 0  
recipient_delimiter = +  
inet_interfaces = all  
home_mailbox = Maildir/




Fique atento para a configuraçao 'home_mailbox' que define o diretorio onde serao armazenadas as mensagens de cada usuario. Neste exemplo esse diretorio seria $HOME/Maildir/




Instalando o Servidor POP3 e IMAP Courier




As instalaçoes dos servidores POP3 e IMAP com suporte SSL Courier tambem podem ser feitas atraves do apt-get:




# apt-get install courier-pop courier-pop-ssl courier-imap courier-imap-ssl




Durante a instalaçao tambem e mostrado um wizard que pergunta se deseja que sejam criados os diretorios para administraçao via web. Responda que nao. Logo em seguida serao gerados os certificados SSL, basta prosseguir com a instalaçao. É possivel personalizar as informaçoes dos certificados, mas nao sera necessario neste momento.




Os arquivos de configuraçao do courier ficam armazenados no debian no diretorio /etc/courier. O arquivo de configuraçao do servidor POP3 e o /etc/courier/pop3d e o equivalente para o servidor IMAP e o /etc/courier/imapd.




Fique atento para a configuraçao 'MAILDIRPATH' destes dois arquivos de configuraçao que definem o diretorio onde serao armazenadas as mensagens de cada usuario. Este diretorio deve ser o mesmo que foi configurado na opçao 'home_mailbox' do postfix.




Apos este passo o servidor Courier esta instalado e funcionando para os casos mais basicos.




Criando o diretorio Maildir




O diretorio que armazena os emails Maildir e um diretorio como outro qualquer, mas necessita que existam outros 3 diretorios dentro dele, onde serao armazenados os emails. Para facilitar esta tarefa o courirer disponibiliza o utilitario 'maildirmake' que cria esta estrutura de diretorios




A utilizaçao e bastante simples, basta estar no diretorio Home do usuario logado e executar:




# cd $HOME  
# maildirmake Maildir




Deve-se tomar cuidado ao criar estes diretorios para que as permissoes fiquem corretas, para isto e necessario que o usuario dono e o grupo do diretorio Maildir sejam os mesmos do diretorio Home.




Instalando o Webmail Squirrelmail




A instalaçao do Squirrelmail tambem e feita atraves do apt-get:




# apt-get install squirrelmail




O squirrelmail utiliza o apache como Servidor Web, de modo que o apache e instalado como dependencia caso ainda nao esteja instalado.




Para configurar o squirrelmail no apache copie o arquivo de configuraçao que o proprio squrirrelmail disponibiliza para a o diretorio de configuraçao do apache:




# cp /etc/squirrelmail/apache.conf /etc/apache2/conf.d/squirrelmail.conf




Apos e necessario reiniciar o apache:




# /etc/init.d/apache2 restart




Acessando o Webmail e testando




Apos estes passos esta tudo instalado e configurado




Para acessar o webmail acesse o seguinte endereço no navegador (considerando que a instalaçao foi realizada em localhost):




[http://localhost/squirrelmail/](http://192.168.0.100/squirrelmail/)




Para testar realize a autenticaçao com um usuario valido do sistema e envie um email para o seu email pessoal do yahoo, gmail ou hotmail por exemplo. Como o servidor nao possui um dominio valido, provavelmente a mensagem sera enviada para a pasta de SPAM ou lixo eletronico.






  
