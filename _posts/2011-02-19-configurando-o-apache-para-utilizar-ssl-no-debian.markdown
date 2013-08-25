---
author: felipe
comments: true
date: 2011-02-19 21:49:13+00:00
layout: post
slug: configurando-o-apache-para-utilizar-ssl-no-debian
title: Configurando o apache para utilizar SSL no Debian
wordpress_id: 315
---

O SSL (Secure Socket Layer) é o protocolo usado para criar páginas seguras, encriptando toda a transmissão entre o cliente e o servidor. É bastante utilizado por sites de comércio eletrônico e por instituições financeiras.

Para instalar e configurar o apache com suporte a SSL no debian o primeiro passo é instalar os dois pacotes, o do apache e o do openssl:

`# apt-get install apache2 openssl`

Em seguida ativamos o módulo de SSL da seguinte forma:

`# a2enmod ssl`

Para que as alterações entrem em vigor é preciso reiniciar o servidor apache:

`# /etc/init.d/apache2 restart`

É necessário também ativar a configuração do virtual host com suporte a SSL, isto pode ser feito da seguinte forma:

`# a2ensite default-ssl`

Em seguida é necessário recarregar as configurações do apache para que o site em SSL seja ativado.

`# /etc/init.d/apache2 reload`

A partir desse momento já é possível acessar o servidor por HTTPS, por exemplo, https://localhost
No entanto, se você analisar o certificado que está sendo utilizado, verá que foi criado um certificado padrão.

É interessante que esse certificado, mesmo que não seja um certificado gerado por uma autoridade certificadora conhecida, possua as informações da empresa ou organização dona do site.

Para isso é necessário utilizar o OpenSSL para gerar uma chave criptográfica e o seu respectivo certificado. Os comandos a seguir realizam essa tarefa:

Gerando a chave criptográfica:

`# openssl genrsa -des3 -out certificado.key 1024`

Gerando o certificado com as informações personalizadas:

`# openssl req -new -key certificado.key -out certificado.csr`

Gerando um novo certificado que não solicite a passprhase ao reiniciar o apache:

`# openssl rsa -in certificado.key -out certificado.key.insecure`

Realizando uma cópia de segurança do certificado original

`# mv certificado.key certificado.backup`

Renomeando o certificado sem senha para o nome padrão.

`# mv certificado.key.insecure certificado.key`

Gerando o certificado final que possui a extensão '.crt' com o prazo para expiração e a chave criada anteriormente que possui a extensão '.key' ambos serão utilizados na configuração do servidor apache, como veremos em seguida:

`# openssl x509 -req -days 365 -in certificado.csr -signkey certificado.key -out certificado.crt`

Copiando os arquivos do certificado e da chave para o local definitivo.

`# cp certificado.crt /etc/ssl/certs/`

`# cp certificado.key /etc/ssl/private/`

Agora é necessário editar o arquivo /etc/apacha2/sites-enabled/default-ssl para apontar para o certificado e a chave criada, as configurações que devem ser alteradas são:

SSLCertificateFile    /etc/ssl/certs/certificado.crt
SSLCertificateKeyFile /etc/ssl/private/certificado.key

Por último é necessário reiniciar novamente o servidor apache e verificar se o novo certificado funcionou como esperado.

`/etc/init.d/apache2 restart`

Caso ocorra algum problema após reiniciar o servidor, verifique os arquivo de log do apache que ficam em /var/log/apache2
