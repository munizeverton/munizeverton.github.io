---
layout: post
title:  "Integrando seu projeto no Github com Travis CI"
date:   2016-04-05 15:00:00
categories: CI Travis Github
---

Integração contínua ou CI (Continuous Integration) é um tópico muito importante e atual.

> "Integração Contínua é uma pratica de desenvolvimento de software onde os membros de um time integram seu trabalho frequentemente, geralmente cada pessoa integra pelo menos diariamente – podendo haver multiplas integrações por dia. Cada integração é verificada por um build automatizado (incluindo testes) para detectar erros de integração o mais rápido possível. Muitos times acham que essa abordagem leva a uma significante redução nos problemas de integração e permite que um time desenvolva software coeso mais rapidamente."   
> -- <cite>Martin Fowler</cite>

Trata-se de uma técnica usada por times de desenvolvimento, em que o trabalho de todos é integrado de maneira constante (geralmente algumas vezes por dia).     
Dessa forma a integração de código é realizada a medida que as funcionalidades são desenvolvidas.

**Travis CI**

Existem diversas ferramentas que facilitam o processo de CI.  
Nesse post vamos falar sobre o Travis CI. Uma ferramenta de integração contínua na nuvem.  
Com ela você pode integrar seu código direto do github. O Travis CI é grátis para repositórios públicos.

Vamos ver como rodar os builds a cada novo push para o repositório.  
Vou usar como exemplo o repositório [Infanatica/InfanaticaCepModule][infanatica]

A primeira coisa a fazer e se logar ou criar uma conta no [Travis][travis] pela sua conta no Github.
Depois disso é só ir até a página do seu perfil e habilitar o build para o projeto que você quer integrar.

**Arquivo .travis.yml**  

A raiz do seu projeto precisa ter um arquivo chamado `.travis.yml`. Esse arquivo contem as configurações do travis. Abaixo o arquivo que foi usado no repositório da Infanatica:

{% highlight yml linenos=table %}
# see http://about.travis-ci.org/docs/user/languages/php/ for more hints
language: php

php:
    - 5.6
    - 7.0
    - hhvm
before_script:
    - composer install
script: phpunit

notifications:
    email:
        - munizeverton@gmail.com
        - diogomascarenha@gmail.com
{% endhighlight %}

Vamos entender o arquivo. 

* Primeiro nós setamos a linguagem como PHP
* Depois nós dizemos em quais versões do PHP o build será realizado. No caso foram as versões 5.6, 7.0 e HHVM
* Em before_script fica qualquer coisa que precise ser executada antes do script de build. Nesse caso será executado um composer install para instalar as dependências do projeto
* Finalmente em script fica o script de build. No nosso caso os testes serão executados pelo comando phpunit
* Em notifications nós setamos os emails que receberam notificação após os builds

Pronto! Depois de adicionado esse arquivo, a cada push realizado para o repositório no github o Travis vai fazer o build e te notificar por email se os testes passaram ou não.  
Você também pode acompanhar as saídas do console durante o processo de build pela página do Travis

[infanatica]: https://github.com/Infanatica/InfanaticaCepModule
[travis]: https://travis-ci.org/






