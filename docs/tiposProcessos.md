# Tipos de Processos

Abaixo você entenderá melhor sobre alguns processos que podem ser customizados no SAM.

## Extração de dados

----

O processo de Extração de dados consiste em se comunicar com bancos de dados para capturar os dados que serão disponibilizados para o sistema destino. Toda a extração de informações da base de dados são através de consultas, listagens, relatórios, resumos, estatísticas, demonstrações, análises, documentos fiscais e não fiscais etc.

### Listagens

----

As Listagens são documentos que disponibilizam informações claras e objetivas de setores da empresa, contando sempre com informações atualizadas e confiáveis, fornecendo dados que são utilizados como base para a tomada de decisão e planejamento de ações. É preciso apresentar esses dados em um formato que facilite a interpretação. São apresentados em forma de tabelas e comparativos, mas podem ser mais completos e estruturados.

### Cubo de Decisões

----

Esta ferramenta auxilia na tomada de decisão da empresa, portanto, é importante o desenvolvedor, conhecer este meio mais fácil para obter melhores resultados. O Cubo de Decisões possibilita visualizar as atividades da empresa de modo gráfico e simplificado, bem como, o seu desempenho, potenciais riscos ou desvios do planejado e a capacidade de obter indicadores de gestão.

### Gedgets

----

Gadgets são elementos que possuem uma função, adicionar conteúdo extra ao painel do SAMERP. Por exemplo, gadgets podem realizar consultas no banco de dados e exibir o conteúdo em forma de gráficos, listas, ícones e muito mais. Os gadgets são construídos a partir de um código HTML, podendo usar CSS e Javascript, e também em Groovy. Os gadgets podem ser colocados em qualquer lugar do painel, na realidade, tudo que você precisa fazer é arrastar e soltar o gadget até a área escolhida.

## Regras de Negócios

----

Regras de negócio são padrões que condicionam o funcionamento do negócio, sendo comumente aplicadas no contexto da arquitetura de softwares. Você pode escrever suas regras de negócio através de fórmulas, interceptadores ou scripts de operações, possibilitando produzir ou validar dados que venham dar respostas, mais adequadas à gestão de seus negócios.

### Fórmulas

----

Uma fórmula é um método prático de resolver um assunto, dar instruções ou expressar uma operação. Em algumas tarefas do SAM4 o processamento de dados pode ser feito de forma customizada, ou seja, cada empresa pode processar livremente. Essas customizações são feitas através das fórmulas. Por exemplo, cálculo de documentos, cálculo de folha de pagamento, manipulação de valores de itens no estoque.

### Interceptação

----

Interceptor, como o próprio nome sugere, nos permite de forma bem simples interceptar e configurar requisições antes delas serem disparadas para o banco de dados. Isso possibilita fazer uma imensidão de coisas, um exemplo seria validar se a requisição está de acordo com os padrões de cadastro de uma determinada empresa, ou de repente bloquear determinados usuário de realizar estas requisições, e até tratar objetos antes de terminar a requisição. As possibilidades são inúmeras.

### Scripts de Operações

----

<p style="text-align: justify">Dentre os Script do SAM o Script de Operações é o único que não é desenvolvido pela ferramenta SAMDEV, ele é construído dentro da própria tarefa. Com ele o desenvolvedor pode criar regras operacionais diferentes para cada tarefa, manipular campos da tela, fazer validações etc. Basicamente o desenvolvedor consegue manipular toda a tarefa. As telas do SAM são construídas em JAVA com SWING, Swing é um widget toolkit GUI para uso com o Java. Ele possui alguns componentes como, Campo texto, campo numérico, campo combo, etc. Cada um destes componentes possuem algumas propriedades que podem ser alteradas para configurar tamanho, largura, altura, cor, fonte, etc.</p>

## Integração com o SAM

----

A integração com o SAM pode ser realizada fazendo ou recebendo requisições de outros sistemas, APIs, serviços etc. Essa integração pode ser realizado através das SERVLETS.

### Servlets

----

Uma Servlet dá uma ideia de servidor pequeno cujo objetivo basicamente é receber requisições HTTP, processá-las e responder ao cliente, essa resposta pode ser um JSON, um HTML, uma imagem etc.