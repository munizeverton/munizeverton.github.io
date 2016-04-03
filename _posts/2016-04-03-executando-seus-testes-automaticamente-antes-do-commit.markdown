---
layout: post
title:  "Executando seus testes automaticamente antes do commit"
date:   2016-04-03 13:00:00
categories: Git TDD
---

Quando trabalhamos em projetos Git é comum a tarefa de rodar a suite de testes antes de fazer um git commit para ver se nada foi esquecido.
Essa tarefa pode ser automatizada através de um recurso do Git chamado Hook.

**O que é um hook do Git**
> Like many other Version Control Systems, Git has a way to fire off custom scripts when certain important actions occur

Os hooks são gatilhos disparados por algumas ações do git.
Para mais detalhes veja a [documentação oficial][documentacao-oficial]

Para a tarefa proposta aqui nós vamos usar o hook pre-commit.
Ele é chamado antes do commit ser executado.
Nosso objetivo é fazer como que o script, antes do commit, execute nossa suite de testes e caso ocorra alguma falha o commit seja rejeitado.

**Vamos ao código**

{% highlight bash linenos=table %}
	#!/bin/bash

	echo "Rodando os testes..."

	cd Test\

	phpunit

	rc=$?
	if [[ $rc != 0 ]] ; then
	    echo "Ocorreu alguma falha nos testes"
	    exit $rc
	fi 

	exit 0
{% endhighlight %}

Como você pode ver, é um script bem simples.

Primeiro nós entramos na pasta de teste, que no meu caso é Test\
Depois nós usamos o comando que executa a suite de testes. No meu caso é phpunit

Por ultimo, é só pegar o retorno do comando que foi executado. Se houver erro nos testes será retornado algo diferente de 0, o que vai fazer com que o commit seja rejeitado. Caso contrário retornamos 0 para o commit ocorrer normalmente

**Tornando o hook executável**

Para que o script que criamos se torne um hook, ele deve ser colocado no diretório de hooks do git, que no caso é seu_projeto/.git/hooks
No nosso caso o arquivo será salvo com o nome de pre-commit
Depois é só dar permissão de execução nesse arquivo (chmod +x pre-commit)

Pronto! Agora toda vez que você for fazer um commit os testes serão executados e o commit será rejeitado caso ocorra alguma falha

[documentacao-oficial]: https://git-scm.com/book/uz/v2/Customizing-Git-Git-Hooks
