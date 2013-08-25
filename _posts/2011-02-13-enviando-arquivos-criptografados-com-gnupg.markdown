---
author: felipe
comments: true
date: 2011-02-13 20:41:03+00:00
layout: post
slug: enviando-arquivos-criptografados-com-gnupg
title: Enviando arquivos criptografados com GnuPG
wordpress_id: 274
---

Para encriptar um arquivo utilizando a chave pública de uma pessoa, você deve primeiramente conseguir a chave pública da pessoa.

Isso pode ser feito de duas formas, solicitando que a pessoa envie a chave pública por email ou até mesmo pessoalmente, ou caso a pessoa disponibilize a chave pública dela em um servidor você pode fazer download da mesma.

Disponibilizar chaves públicas em um servidor na internet facilita bastante o processo, pois quem deseja enviar os arquivos encriptados não precisa entrar em contato solicitando o envio da chave.

Para listar as chaves que já estão disponíveis no gpg, utilize o seguinte comando:

`$ gpg --list-keys`

Caso não retorne nenhum resultado é porque ainda não existe nenhuma chave armazenada no sistema.

É bom lembrar que por se tratar de uma chave pública, não há problema algum de segurança em disponibilizá-la em um servidor. Veja mais sobre chaves públicas e privadas no post sobre [criptografia](/criptografia/).

Para importar a chave pública de uma pessoa com o gpg pode ser utilizado o comando de busca, da seguinte forma:

`$ gpg --search-keys 'NomeOuEmailDaPessoa'`

Serão listados todas as chaves armazenadas que correspondem a busca, para importar a chave basta digitar o número do resultado.

A partir de agora para encriptar um arquivo com a chave importada pode ser utilizado o seguinte comando do gpg:

`$ gpg --encrypt --recipient 'User ID' secret.txt`

Será gerado um arquivo encriptado secret.txt.gpg que pode ser enviado com segurança para o destinatário.
