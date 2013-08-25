---
author: felipe
comments: true
date: 2010-10-16 16:47:00+00:00
layout: post
slug: instalando-e-configurando-o-openldap-no-debian-para-autenticacao-centralizada-de-usuarios
title: Instalando e configurando o Openldap no Debian para Autenticação Centralizada
  de Usuários
wordpress_id: 113
---


    

Este tutorial ira apresentar os passos para a instalaçao e configuraçao do Openldap em um sistema debian-based de modo que os usuarios do sistema fiquem armazenados na base do servidor LDAP.




Instalando o OpenLDAP




A instalaçao do servidor OpenLDAP no Debian pelo apt-get e feita pela instalaçao do pacote slapd e do pacote de utilitarios ldap-utils:




# apt-get install slapd ldap-utils




Durante a instalaçao e apresentado um wizard em que deve ser informada a senha administrativa do servidor openldap. Informe uma senha de sua preferencia.




Apos este passo o servidor LDAP esta instalado e escutando na porta 389 que e a porta padrao do serviço. Para confirmar que o servidor esta online verifique se a porta 389 do sistema realmente esta em 'LISTEN'. Para isso execute o netstat da seguinte forma:




# netstat -ant |grep 389




O resultado deve ser algo parecido com o seguinte:




servidor-ldap:/etc# netstat -ant |grep 389  
tcp  0  0 0.0.0.0:389  0.0.0.0:*  LISTEN    
tcp6  0  0 :::389  :::*  LISTEN 




Se o comando acima nao retornar nenhum resultado e porque o servidor nao esta funcionando corretamente.







Configurando o Servidor OpenLDAP




O pacote openldap do debian possui outro wizard que permite realizar as demais configuraçoes do servidor OpenLDAP. Para executar o wizard e necessario executar o dpgk-reconfigure da seguinte forma:




# dpkg-reconfigure slapd




A primeira pergunta e se voce deseja que o wizard termine sem oferecer as opçoes de configuraçao. Responda que Nao.




A segunda pergunta e sobre o dominio que sera utilizado para construir o DN do servidor LDAP. Neste exemplo foi definido o dominio 'dominiolocal.loc'.




A terceira pergunta e sobre o nome da organizaçao/empresa para ser usada no DN. Neste exemplo foi definido o nome 'minhaorganizacao'.




A quarta e quinta pergunta sao para definir novamente a senha de acesso ao servidor. Defina uma senha de sua preferencia.




A sexta pergunta e sobre o backend da base de dados para ser utilizada. Escolha o backend HDB que possui alguns vantagens em relaçao ao BDB.




A setima pergunta e para escolher se a base de dados sera removida quando o pacote slapd for removido complemente (purged). Escolha Nao




A oitava pergunta explica que existem arquivos de uma configuraçao antiga do openldap que nao permitiram que continue com a configuraçao. Responda Sim para que a base seja movida para outro local.




A nona pergunta define se a versao 2 do protocolo LDAP sera suportada. Responda Nao.[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-3.png.scaled1000-300x190.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-3.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-4.png.scaled1000-300x191.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-4.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-5.png.scaled1000-300x190.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-5.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-1.png.scaled1000-300x192.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-1.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-2.png.scaled1000-300x191.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-2.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-9.png.scaled1000-300x191.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-9.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-7.png.scaled1000-300x190.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-7.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-8.png.scaled1000-300x190.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-8.png.scaled1000.png)
[![](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-6.png.scaled1000-300x192.png)](http://blog.felipemunhoz.com/wp-content/uploads/2010/10/openldap-6.png.scaled1000.png)


[See and download the full gallery on posterous](http://blog.felipemunhoz.com/instalando-e-configurando-o-openldap-no-debia)




O que o wizard faz e gerar o arquivo de configuraçao do OpenLDAP que fica em /etc/ldap/slapd.conf. Acesse esse arquivo e verifique as configuraçoes geradas.




Configurando o Cliente OpenLDAP




As configuraçoes apresentadas acima sao para o servidor OpenLDAP. É preciso tambem configurar o cliente LDAP para que o mesmo acesse o servidor configurado.




O arquivo de configuraçao do cliente OpenLDAP e o /etc/ldap/ldap.conf




Edite este arquivo para que servidor possa ser acessado pelo cliente da seguinte forma:




/etc/ldap/ldap.conf




----------------------




host 127.0.0.1  
base dc=dominiolocal,dc=loc  
uri ldap://localhost/  
ldap_version 3  
rootbinddn cn=admin,dc=dominiolocal,dc=loc




----------------------




Migrando os usuarios do sistema para a base LDAP




Apos a instalaçao do servidor LDAP a base de dados esta apenas com as informaçoes basicas cadastradas.




Para ver todo o conteudo da base LDAP ate o momento pode ser utilizado o comando 'slapcat'.




# slapcat




O slapcat realiza um 'dump' na base no formato LDIF.




Para que seja possivel a autenticaçao dos usuarios via LDAP e necessario importar as contas de usuario do sistema para a base LDAP. Para isso sao necessarios os arquivos de importaçao LDIF.




Estes arquivos tem uma sintaxe bastante rigida e para facilitar este processo podemos utilizar os scripts de migraçao do pacote migrationtools. Para instalar basta executar o seguinte:




# apt-get install migrationtools




Apos a instalaçao e necessario informar a configuraçao do servidor LDAP. Para isso edite o arquivo:




# vim /usr/share/migrationtools/migrate_common.ph




E altere as seguinte opçoes:




$DEFAULT_MAIL_DOMAIN = "dominiolocal.loc";  
$DEFAULT_BASE = "dc=dominiolocal,dc=loc";




Agora e possivel exportar as informaçoes com os seguintes comandos:




_# cd /usr/share/migrationtools  
__# ./migrate_group.pl /etc/group /root/group.ldif  
__# ./migrate_passwd.pl /etc/passwd /root/passwd.ldif_




Executando os comandos acima serao gerados os arquivos LDIF com as informaçoes de todos os usuarios e grupos atuais do sistema. Entretanto na pratica nao devemos importar para a base LDAP as contas administrativas do sistema como por exemplo as contas 'bin' e 'nobody'. O mesmo vale para os grupos.




Considerando isso, edite os arquivos exportados mantendo apenas as informaçoes dos usuarios que necessitarem realmente a autenticaçao centralizada na base ldap.




Abaixo segue dois exemplos de arquivos LDIF para um grupo e usuario 'senacti'.




---------------------




/root/group.ldif




---------------------







dn: cn=senacti,ou=Group,dc=dominiolocal,dc=loc  
objectClass: posixGroup  
objectClass: top  
cn: senacti  
userPassword: {crypt}x  
gidNumber: 1001




---------------------







/root/passwd.ldif




---------------------







dn: uid=senacti,ou=People,dc=dominiolocal,dc=loc  
uid: senacti  
cn: senacti  
objectClass: account  
objectClass: posixAccount  
objectClass: top  
objectClass: shadowAccount  
userPassword: {crypt}$1$Kcpij9aY$oFb9KKzEPrZZ69UyyqcsZ1  
shadowLastChange: 14899  
shadowMax: 99999  
shadowWarning: 7  
loginShell: /bin/bash  
uidNumber: 1001  
gidNumber: 1001  
homeDirectory: /home/senacti  
gecos: ,,,







---------------------




É preciso tambem criar um arquivo LDIF com os "ramos" People e Group que armazenarao os usuarios e grupos, respectivamente, na arvore LDAP. Segue um exemplo abaixo:




---------------------




/root/people_group.ldif




-----------------------------




dn: ou=People, dc=dominiolocal, dc=loc  
ou: People  
objectclass: organizationalUnit




dn: ou=Group, dc=dominiolocal, dc=loc  
ou: Group  
objectclass: organizationalUnit




-----------------------------




Agora ja temos as informaçoes dos usuarios convertidas para o formato LDIF. Temos entao que importar as informaçoes para o servidor da seguinte forma:




# /etc/init.d/slapd stop  
# cd /root  
# slapadd -l people_group.ldif  
# slapadd -l group.ldif  
# slapadd -l passwd.ldif  
# /etc/init.d/slapd start




Execute novamente o aplicativo 'slapcat' para ver que agora a base esta com as informaçoes dos usuarios na base LDAP.




Com as configuraçoes realizadas acima a base LDAP esta configurada e pronta para que um serviço se conecte para realizar a autenticaçao.



  
