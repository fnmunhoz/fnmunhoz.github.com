---
author: felipe
comments: true
date: 2010-10-16 20:32:00+00:00
layout: post
slug: integrando-o-pam-ao-ldap
title: Integrando o PAM ao LDAP
wordpress_id: 112
---




Nos proximos passos estaremos configurando o PAM para autenticar usuarios que estao na base LDAP.










Entendendo o PAM




Plugglable Autentication Modules (Modulos de autenticaçao plugaveis) sao um conjunto de bibliotecas usadas para fazer autenticaçao, gerenciamento de contas, controle de recursos dos usuarios no sistema, em adiçao ao tradicional sistema de acesso baseado em usuarios/grupos.




Este recurso permite modificar a forma que um aplicativo autentica e define recursos para o usuario sem necessidade de recompilar o aplicativo principal.




Os recursos que desejamos controlar restriçoes via PAM sao especificados individualmente por serviços nos arquivos correspondentes em `/etc/pam.d` e entao os arquivos correspondentes em `/etc/security` sao usados para controlar tais restriçoes.




Para mais informaçoes sobre o PAM acesse o [Guia Foca GNU/Linux Capitulo 19 - Restriçoes de acesso, recursos e serviços](http://focalinux.cipsga.org.br/guia/avancado/ch-d-restr.htm)







Instalando o Suporte do PAM ao LDAP




# apt-get install libnss-ldap libpam-ldap nscd libpam-foreground




Durante a instalaçao sera apresentado um wizard para facilitar o processo de configuraçao. As informaçoes que serao necessarias serao:






  * URI: ldap://localhost/


  * DN: dc=dominiolocal,dc=loc


  * Conta admistrativa: cn=admin,dc=dominiolocal,dc=loc


  * Password da conta administrativa: (mesmo password definido na instalaçao do openldap).




[![](/images/integrando-o-pam-ao-ldap/pam_ldap-1.png.scaled500-300x192.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-1.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-2.png.scaled1000-300x190.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-2.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-5.png.scaled1000-300x191.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-5.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-6.png.scaled1000-300x191.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-6.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-7.png.scaled1000-300x190.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-7.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-3.png.scaled1000-300x192.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-3.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-4.png.scaled1000-300x190.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-4.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-8.png.scaled1000-300x189.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-8.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-9.png.scaled1000-300x191.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-9.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-10.png.scaled1000-300x193.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-10.png.scaled1000.png)
[![](/images/integrando-o-pam-ao-ldap/pam_ldap-11.png.scaled1000-300x190.png)](/images/integrando-o-pam-ao-ldap/pam_ldap-11.png.scaled1000.png)


[See and download the full gallery on posterous](http://blog.felipemunhoz.com/integrando-o-pam-ao-ldap)







Conforme informado durante o wizard sera necessario editar o arquivo /etc/nsswitch.conf para que o sistema procure as informaçoes de autenticaçao na base ldap. O arquivo deve ser editado conforme exemplo a seguir:




----------------------------




/etc/nsswitch.conf




----------------------------







passwd:  files ldap
group:  files ldap
shadow:  files ldap




hosts:  files dns
networks:  files ldap




protocols:  db files
services:  db files
ethers:  db files
rpc:  db files




netgroup:  nis







--------------------------------




Configurando o PAM para acessar a base LDAP




Para que o PAM acesse a base LDAP e necessario editar os seguintes arquivos conforme abaixo:




--------------------------------------




/etc/pam.d/common-account




--------------------------------------




account sufficient pam_ldap.so
account required pam_unix.so try_first_pass




--------------------------------------




/etc/pam.d/common-session




--------------------------------------




_ _




_ _




_


session required pam_mkhomedir.so skel=/etc/skel umask=0022 silent
___


session sufficient pam_unix.so


___


_




--------------------------------------




/etc/pam.d/common-auth




--------------------------------------




auth required pam_nologin.so
auth required pam_env.so
auth sufficient pam_ldap.so
auth required pam_unix.so nullok_secure try_first_pass




--------------------------------------







/etc/pam.d/common-password







--------------------------------------











password  sufficient  pam_ldap.so




password  required  pam_unix.so nullok obscure min=4 max=8 md5 try_first_pass







--------------------------------------




Apos estas configuraçoes a autenticaçao de usuarios ja pode ser realizada atraves dos usuarios cadastrados na base LDAP.




Para consultar quais usuarios estao disponiveis para autenticaçao execute o seguinte comando:




# getent passwd



