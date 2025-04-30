# Bem-vindo

Bem vindo à documentação para desenvolvedores do ERP SAM.

!!! info "Saiba Mais"
	Para conhecer mais, visite o site oficial do [SAM](https://multitecsistemas.com.br). 

## Introdução

----

Este documento tem como finalidade apresentar as diferentes formas de customização de processos e integração com os recursos e funcionalidades do ERP SAM. Por exemplo, ao inserir um registro no sistema, há a possibilidade de intervir neste processo realizando críticas ou restrições. O SAM é um sistema totalmente adaptável e pode se enquadrar perfeitamente às regras do seu negócio, além de se integrar sem dificuldades a outros sistemas disponíveis no mercado. Aqui, veremos como realizar essas customizações e integrações.

## Recomendações

----

O SAM utiliza como parte de seus componentes algumas bibliotecas e frameworks, antes de começar recomendamos que você leia e entenda um pouco mais sobre elas.

- [VUE.js](https://br.vuejs.org/v2/guide/index.html)
- [ApexCharts](https://apexcharts.com)
- [Swing](https://docs.oracle.com/javase/tutorial/uiswing/start/about.html)

## Linguagens Utilizadas

----

As customizações e integrações com o SAM são construídas a partir da linguagem Groovy. O Groovy é uma linguagem de programação orientada a objetos desenvolvida para a plataforma Java como alternativa à linguagem de programação Java. Ele possui características de Python, Ruby e Smalltalk. Utiliza uma sintaxe similar à de Java, é compilada dinamicamente para bytecode Java e integra-se transparentemente com outros códigos e bibliotecas Java.

!!! summary "Visite a documentação do [Groovy](https://groovy-lang.org/documentation.html)."

Os componentes gráficos renderizados na web são construidos com HTML, CSS e JavaScript, podendo ou não utilizar os componentes dos frameworks que vimos acima. Já os componentes gráficos renderizados em desktop são construidos com Swing.

## Como funciona

----

Todas as customizações e integrações podem ser construidas a partir do próprio SAM, nele você encontrará uma ferramenta já integrada e pronta para uso chamada SAMDEV, porém, também podemos criá-las a partir de qualquer outro editor de textos, editor de códigos ou IDE de sua preferência.

*[IDE]: Integrated development environment (Ambiente de desenvolvimento integrado)


Além do SAMDEV, disponibilizamos um projeto base para ser usado em alguma IDE

- [projeto base](https://s3-sa-east-1.amazonaws.com/files.tasks.samdoc.info/uploads/div/303/formulas_base.zip) 

## Requisitos

----

Para instalar o SAM e utilizar do SAMDEV ou outros Editores/IDEs, devemos instalar os seguintes requisitos:

- [Java 21](https://www.oracle.com/java/technologies/javase/jdk21-archive-downloads.html)
- [PostgreSQL](https://www.postgresql.org/download/)

!!! note "Nota"
	Visite nosso repositório para visualizar alguns exemplos que iremos explorar por aqui. 
	[https://github.com/multitecsistemas/sam4](https://github.com/multitecsistemas/sam4)