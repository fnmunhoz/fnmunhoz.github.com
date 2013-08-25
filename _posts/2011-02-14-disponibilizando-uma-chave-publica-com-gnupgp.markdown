---
author: felipe
comments: true
date: 2011-02-14 00:33:58+00:00
layout: post
slug: disponibilizando-uma-chave-publica-com-gnupgp
title: Disponibilizando uma chave pública com GnuPGP
wordpress_id: 287
---

Para que outras pessoas enviem arquivos para você com segurança, elas podem encriptar os arquivos utilizando sua chave pública.

É necessário então que você disponibilize essa chave pública para ela. Isto pode ser feito de muitas formas, por exemplo, enviando sua chave pública por email, ou então disponibilizando a mesma em um servidor de chaves públicas, o que se mostra bem mais prático e ágil.

Primeiramente é necessário gerar um par de chaves pública e privada. Com o GnuPGP pode ser realizado da seguinte forma:

`gpg --gen-key`

Serão apresentadas opções de escolha de quais algoritmos de geração de chaves você deseja utilizar.

As opções de algoritmos variam entre as versões do gpg e do sistema operacional utilizado, no debian 5, por exemplo, são as seguintes:



	
  * (1) DSA and Elgamal (default)

	
  * (2) DSA (sign only)

	
  * (5) RSA (sign only)


No ubuntu 10.10 é disponibilizada, uma a opção a mais:

	
  * (1) RSA and RSA (default)

	
  * (2) DSA and Elgamal

	
  * (3) DSA (sign only)

	
  * (4) RSA (sign only)


Escolha a opção default nos dois casos, pois dessa forma serão geradas tanto a chave para assinatura (sing) quanto para encriptação, que é o que desejamos no momento.

Na sequência será questionado o tamanho em bits da chave e o tempo de expiração, podem ser escolhidas as opções default.

Será necessário também uma passphrase que será solicitada sempre que for utilizada esta chave para decriptar alguma informações, de maneira simplificada, funciona como uma senha.

O último passo é a geração do par de chaves, sendo que nesse ponto o wizard solicitará que você utilize o teclado, o mouse e o disco, para que a entropia do sistema seja maior, e facilite a geração de uma chave forte.

Com a chave gerada, a mesma pode ser lista com o seguinte comando:
`gpg --list-keys`

O próximo passo é enviar esta chave por email para a pessoa que deseja lhe enviar o arquivo confidencial ou então disponilizar esta chave em um servidor de chaves públicas, como comentado acima.
Para enviar para um servidor utilize o seguinte comando:

`gpg --send-keys 'User ID'`

Basta aguardar alguns minutos e a chave já estará disponível para que outras pessoas a utilizem.
