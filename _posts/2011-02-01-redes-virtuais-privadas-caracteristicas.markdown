---
author: felipe
comments: true
date: 2011-02-01 22:24:15+00:00
layout: post
slug: redes-virtuais-privadas-caracteristicas
title: 'Redes Virtuais Privadas: características'
wordpress_id: 243
---

Existe um conjunto básico de requisitos que qualquer solução de VPN deve estar preparada para atender, a seguir vamos ver cada um deles:

**Autenticação de Usuários**

Restringir o acesso por usuários e grupos é um dos requisitos de uma solução de VPN. É importante também que qualquer acesso ou tentativa de acesso à VPN, seja registrado de forma que futuramente seja possível emitir um relatório com as conexões de cada usuário.

**Criptografia de Dados**

Como citado em posts anteriores o tráfego de dados pela VPN deve ser encriptado, já que as informações passam pela internet, que é uma rede pública, e caso esses dados sejam interceptados, o interceptador não conseguirá decifrar.

**Gerenciamento de chaves**

A utilização de chaves criptográficas garantem a segurança da criptografia dos dados que trafegam pela VPN, pois são elas que armazenam o segredo da comunicação.

**Gerenciamento de endereço**

O endereço do cliente também deve ser privado, isto é, não deve ser possível se comunicar diretamente com ele de fora da VPN.
