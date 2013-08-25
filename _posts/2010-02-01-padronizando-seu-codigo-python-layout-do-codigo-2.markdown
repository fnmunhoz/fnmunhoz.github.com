---
author: felipe
comments: true
date: 2010-02-01 01:16:38+00:00
layout: post
slug: padronizando-seu-codigo-python-layout-do-codigo-2
title: 'Padronizando seu código Python: layout do código [2]'
wordpress_id: 41
---

Neste post da série [Padronizando seu código Python](http://blog.felipemunhoz.com/?p=10) será apresentado os padrões para o layout do código como identação, tamanho máximo de cada linha, linhas em branco e utilização de codificações de caracteres.

**Identação**

Em Python a identação é importantíssima, pois além de facilitar a leitura e organização do código, ela tem significado sintático para o interpretador, já que é utilizada na definição de blocos de código como laços de repetição, estruturas condicionais, definição de classes e funções, entre outros. Veja o exemplo a seguir:


    
    
    def foo(bar):
        if bar == "somevalue":
            print bar
        else:
            print "othervalue"
    



A [PEP 8](http://www.python.org/dev/peps/pep-0008/) recomenda que sejam utilizados **4 espaços** por nível de identação, que é a forma mais popular. É possível também utilizar 1 tab por nível de identação. Mas lembre-se nunca misture espaços e tabs, esta prática é fortemente desanconselhável. 

Portanto utilize sempre espaços, a maioria dos editores e IDEs utilizam esta configuração por padrão e facilitam sua utlilização, substituindo o caracter TAB digitado pelos 4 espaços de forma transparente.

**Tamanho máximo de cada linha**

A recomendação é não ultrapassar **79 caracteres** em cada linha. Esta recomendação é devido a característica de alguns dispositivos que apresentam no máximo 80 caracteres por linha, mas esse limite facilita também a comparação de dois códigos lado a lado utilizando uma interface [Diff](http://en.wikipedia.org/wiki/Diff) por exemplo.

No caso de textos dentro do código (documentação inline e comentários) a recomendação é que não ultrapasse **72 caracteres** com o objetivo de facilitar a leitura.

É claro que em muitas situações esse limite será ultrapassado, sendo necessário separar o código em diversas linhas. A maneira recomendada de fazer isso é utilizando o caracter de barra invertida, como mostra o exemplo a seguir:


    
    
    class Rectangle(Blob):
        
        def __init__(self, width, height,
                     color='black', emphasis=None, highlight=0):
            if width == 0 and height == 0 and \
               color == 'red' and emphasis == 'strong' or \
               highlight > 100:
                raise ValueError("sorry, you lose")
            if width == 0 and height == 0 and (color == 'red' or
                                               emphasis is None):
                raise ValueError("I don't think so -- values are %s, %s" %
                                 (width, height))
            Blob.__init__(self, width, height,
                          color, emphasis, highlight)
    



**Linhas em branco**

Separe definição de funções e classes com duas linhas em branco, e funções dentro de classes com uma linha em branco, de acordo com o exemplo a seguir:


    
    
    def calc_size(object):
       return size_object(object)
    
    
    def foo(bar):
        if bar == "somevalue":
            print bar
        else:
            print "othervalue"
    
        try:
            if other_test(bar):
                print "another"
        except:
            raise ValueError("one error has occured")
    
    
    class Rectangle(Blob):
    
            def __init__(self, width, height,
                         color='black', emphasis=None, highlight=0):
                if width == 0 and height == 0 and \
                   color == 'red' and emphasis == 'strong' or \
                   highlight > 100:
                    raise ValueError("sorry, you lose")
    



No próximo post da série veremos as convenções utilizadas na importação de bibliotecas para o código.
