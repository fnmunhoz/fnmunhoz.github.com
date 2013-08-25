---
author: felipe
comments: true
date: 2011-04-10 21:23:12+00:00
layout: post
slug: protegendo-se-de-ataques-por-forca-bruta-no-ssh
title: Protegendo-se de ataques por força bruta no SSH
wordpress_id: 451
---

O SSH é um serviço bastante visado por atacantes na internet, principalmente pelo fato de ao conseguir acesso por SSH, o atacante tem a chance de utilizar o sistema sem restrições, ter acesso a rede interna, entre outros.

Como mostrado no post sobre [Configurações do Servidor SSH](/configurando-o-servidor-ssh/) é possível realizar um tunning para melhorar a segurança do serviço. Entretanto essas configurações não impedem um ataque por força bruta, por exemplo.

Um ataque de força bruta consiste basicamente de um robô realizando tentativas de acesso ao sistema uma após a outra com pouco intervalo de tempo entre as tentativas, utilizando muitas combinações de usuários e senhas. Estas combinações utilizam listas de usuários e senhas comumente encontradas nos sistemas.

Existem diversas formas de se defender destes tipos de ataques. Veremos a seguir uma lista delas baseado [neste artigo](http://www.la-samhna.de/library/brutessh.html).


## **Senhas fortes**


Senhas fortes ajudam a proteger o acesso por SSH. Sem dúvida senhas como 'p@ssword' ou 'senha123' serão facilmente descobertas em um ataque por força bruta baseado em dicionários de palavras.

**Vantagem**: Simples de implantar

**Desvantagem**: Necessita checar as senhas no momento da criação para verificar se é uma senha realmente forte. Além disso não reduz a sobrecarga tanto na rede quando no serviço SSH.


## **Autenticação por chaves**


A autenticação por chaves permite uma camada de proteção superior a autenticação por senha, já que para obter acesso ao sistema é preciso possuir a chave criptográfica privada, que em teoria somente o dono deve ter acesso.

Veja neste post como [configurar o serviço SSH para utilizar autenticação por chaves](/configurando-o-servidor-ssh-para-utilizar-chaves-de-autenticacao/)

Considere também configurar o SSH para não permitir a autenticação por senha através da opção _PasswordAuthentication_.

**Vantagem:** Muito seguro, quando são tomados os cuidados necessários.

**Desvantagem:** Pessoas não técnicas podem ter dificuldade de configurar o serviço. Também é preciso proteger muito bem a chave privada, já que a mesma dá acesso ao sistema. Além disso, é possível que os usuários deixem a frase secreta em branco, diminuindo consideravelmente a segurança.


## **Bloqueando os ataques através do iptables**


É possível bloquear o acesso ao serviço SSH através do firewall iptables. As regras abaixo bloqueiam as conexões após três tentativas no mesmo minuto.

`# iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH -j ACCEPT
# iptables -A INPUT -p tcp --dport 22 -m recent --update --seconds 60 --hitcount 4 --rttl --name SSH -j LOG --log-prefix "SSH_brute_force "
# iptables -A INPUT -p tcp --dport 22 -m recent --update --seconds 60 --hitcount 4 --rttl --name SSH -j DROP
`

**Vantagem:** É transparente para os usuários.

**Desvantagem:** A regra é aplicada também para três tentativas com sucesso, já que as regras não distinguem conexões bem sucedidas.



## **Bloqueando conexões através do log sshd**



Outra forma bastante eficaz de se proteger de ataques por força bruta é bloquear os invasores através do monitoramento do arquivo de log do próprio sshd que fica em /var/log/auth.log

É possível utilizar um conjunto de comandos nativos do bash para realizar a tarefa como por exemplo uma combinação de 'grep', 'awk', 'uniq' entre outros.

Existem também diversos softwares que realizam esta tarefa. Um deles é o fail2ban.

Para instalar basta um:
`apt-get install fail2ban`

A configuração do fail2ban é realizada através do arquivo /etc/fail2ban/jail.conf

É possível especificar o tempo que o atacante ficará bloqueado e também o número de tentativas frustadas que resultará em bloqueio.

**Vantagem:** É transparente para os usuários e distingue tentativas mal-sucedidadas das bem-sucedidas

**Desvantagem:**Necessita de outro daemon além do sshd para funcionar.
