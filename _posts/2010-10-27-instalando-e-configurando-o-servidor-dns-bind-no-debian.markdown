---
author: felipe
comments: true
date: 2010-10-27 23:29:00+00:00
layout: post
slug: instalando-e-configurando-o-servidor-dns-bind-no-debian
title: Instalando e configurando o servidor DNS Bind no Debian
wordpress_id: 111
---


    

A instalaçao do servidor de DNS bind no debian e feita pelo apt-get:




# apt-get install bind9




Apos instalado o bind e inicializado e responde por padrao como um servidor DNS de cache, encaminhando as requisiçoes para os root servers sem responder diretamente.




Configuraçao do cliente DNS




Neste momento ja e possivel configurar os clientes da rede para utilizarem o seu servidor de DNS de cache.




O arquivo de configuraçao do cliente DNS no linux e o /etc/resolv.conf, segue um exemplo:




/etc/resolv.conf




------------------------




nameserver 208.67.222.222  
nameserver 208.67.220.220




------------------------




Nesse arquivo devem ser informados pelo menos os servidores DNS primario e secundario. Como exercicio configure nesse arquivo o endereço IP do servidor DNS que voce acabou de instalar e tente navegar na internet.







Configuraçao do servidor DNS




O arquvo de configuraçao principal do bind e o /etc/bind/named.conf. Aproveite e de uma olhada nesse arquivo. Voce vai ver alguns apontamentos para outros arquivos. Estes arquivos sao onde ficam configuradas as zonas DNS no bind. Repare tambem que na ultima linha linha desse arquivo e incluido o arquivo /etc/bind/named.conf.local.




Esse arquivo que e incluido e onde voce deve colocar suas zonas DNS, de forma que o arquivo principal (/etc/bind/named.conf) nao seja alterado.







/etc/bind/named.conf




---------------------------







// This is the primary configuration file for the BIND DNS server named.




//




// Please read /usr/share/doc/bind9/README.Debian.gz for information on the




// structure of BIND configuration files in Debian, *BEFORE* you customize




// this configuration file.




//




// If you are just adding zones, please do that in /etc/bind/named.conf.local




include "/etc/bind/named.conf.options";




// prime the server with knowledge of the root servers




zone "." {




type hint;




file "/etc/bind/db.root";




};




// be authoritative for the localhost forward and reverse zones, and for




// broadcast zones as per RFC 1912




zone "localhost" {




type master;




file "/etc/bind/db.local";




};




zone "127.in-addr.arpa" {




type master;




file "/etc/bind/db.127";




};




zone "0.in-addr.arpa" {




type master;




file "/etc/bind/db.0";




};




zone "255.in-addr.arpa" {




type master;




file "/etc/bind/db.255";




};




include "/etc/bind/named.conf.local";




--------------------------







Habilitando o log de consultas do servidor DNS




Para entender melhor o que o servidor bind esta fazendo podemos habilitar o log de mensagens. Para isso adicione as seguintes linhas no /etc/bind/named.conf.local:







/etc/bind/named.conf.local




-----------------------------------------







logging {




channel query.log {




file "/var/log/query.log";




// Set the severity to dynamic to see all the debug messages.




severity debug 3;




};




category queries { query.log; };




};







-----------------------------------------




Sera necessario ainda criar o arquivo de log mencionado e alterar o dono para o usuario 'bind'.




Feita a configuraçao fique analisando o arquivo de log e tente resolver alguns dominios para ver o que acontece.





  
