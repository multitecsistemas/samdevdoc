# Scripts de Operação

## Introdução 

Dentre os Script do SAM o Script de Operações é o único que não é desenvolvido pela ferramenta SAMDEV, ele é construído dentro da própria tarefa. Com ele o desenvolvedor pode criar regras operacionais diferentes para cada tarefa, manipular campos da tela, fazer validações etc. Basicamente o desenvolvedor consegue manipular toda a tarefa. As telas do SAM são construídas em JAVA com SWING, Swing é um widget toolkit GUI para uso com o Java. Ele possui alguns componentes como, Campo texto, campo numérico, campo combo, etc. Cada um destes componentes possuem algumas propriedades que podem ser alteradas para configurar tamanho, largura, altura, cor, fonte, etc.

Um Script de Operação permite a manipulação dos componentes de tela do SAM, interferir em ações ou processos ou até mesmo criar componentes, ações ou processos customizados.

Os componentes de tela do SAM são construidos a partir de componentes `Swing`, sendo assim, os métodos aplicaveis aos componentes swing são aplicados aos componentes do SAM.

As tarefas do SAM são divididas em dois tipos:

1. Cadastros
2. Processos

!!! info "Saiba Mais"
	Para conhecer mais, veja alguns [exemplos](./exemplos/scripts.md). 

## Métodos

### `execute`
---
Disponível por padrão em todos os scripts, sendo executado antes da tarefa ser aberta, nele serão feitas as alterações em componentes visuais ou processos da tela.

=== "Exemplo"
    ``` java
    @Override 
    public void execute(MultitecRootPanel panel) {
    }
    ```

### `preSalvar`
---
Disponível por padrão nos scripts das tarefas de cadastro, sendo executado nos cadastros sempre que o usuário salvar (F9) um registro.

=== "Exemplo"
    ``` java
    @Override 
    public void preSalvar(boolean salvo) {
    }
    ```

### `posSalvar`
---
Disponível por padrão nos scripts das tarefas de cadastro, sendo executado nos cadastros após o usuário salvar (F9) um registro.

=== "Exemplo"
    ``` java
    @Override 
    public void posSalvar(Long id) {
    }
    ```

### `exibirInformacao`
----
Exibir em uma tela uma mensagem apenas informativa.

**Argumentos:**

| Tipo       | Descrição              |
|------------|------------------------|
| String     | Mensagem a ser exibida |

=== "Exemplo"
	``` java
	exibirInformacao("Olá Mundo!")
	```

### `exibirAtencao`
----
Exibir em uma tela uma mensagem de alerta/atenção porém sem interromper o processo.

**Argumentos:**

| Tipo       | Descrição              |
|------------|------------------------|
| String     | Mensagem a ser exibida |

=== "Exemplo"
	``` java
	exibirAtencao("O saldo da conta corrente está negativo.")
	```

### `exibirQuestao`
----
Exibir em uma tela uma questão com dois botões [SIM, NÃO] retornando [false] para [NÃO] e [true] para [SIM].

**Argumentos:**

| Tipo       | Descrição              |
|------------|------------------------|
| String     | Mensagem a ser exibida |

=== "Exemplo"
	``` java
	boolean resposta = exibirQuestao("Deseja continuar o processo?")
	```

### `interromper`
----
Este método lança uma exceção ao processo, interrompendo-o.

| Tipo   | Descrição                      |
|--------|--------------------------------|
| String | Mensagem a ser exibida         |

=== "Exemplo"
	``` java
	interromper("Você não tem permissão para continuar.")
	```


### `executarConsulta`
----

Executa a SQL informada no banco de dados, retornando uma lista de TableMap.

**Argumentos:**

| Tipo       | Descrição                             |
|------------|---------------------------------------|
| String     | SQL a ser executada no banco de dados |

=== "Exemplo"
	``` java
	List<TableMap> resultados = executarConsulta("SELECT * FROM Abh80 LIMIT 1")
	```

### `executarSalvarOuExcluir`
----

Executa uma SQL sem retorno, ou seja, apenas uma SQL para salvar (INSERT/UPDATE) ou excluir (DELETE) um registro no banco de dados.

**Argumentos:**

| Tipo       | Descrição                             |
|------------|---------------------------------------|
| String     | SQL a ser executada no banco de dados |

=== "Exemplo"
	``` java
	executarSalvarOuExcluir("UPDATE Abh80 SET abh80nome = 'José')
	```

### `ocultarColunas`
----
Oculta uma coluna de uma determinada Spread (Tabela) da tela.

**Argumentos:**

| Tipo       | Descrição                                                  |
|------------|------------------------------------------------------------|
| MSpread    | Spread que terá as colunas ocultas                         |
| int        | Índice das colunas que serão ocultas separadas por virgula |

=== "Exemplo"
	``` java
	MSpread spread = getComponente("nomeSpread")
    ocultarColunas(spread, 0, 3, 5, 10)
	```

### `criarMenu`
---
Cria um menu na parte superior da tarefa

**Argumentos:**

| Tipo             | Descrição                                      |
|------------------|------------------------------------------------|
| String           | Nome do Menu                                   |
| String           | Nome do Item do Menu                           |
| ActionListener   | Ffunção que será executada ao clicar no menu   |
| KeyStroke        | Atalho no teclado para chamar o menu           |

=== "Exemplo"
    ``` java
    criarMenu("Validações", "Validar Item", e -> validarItem(), null);
    ```

### `alterarTamanhoTela`
----
Altera a altura e a largura da tela somando os valores recebido como argumento ao tamanho original.

**Argumentos:**

| Tipo             | Descrição                      |
|---------------|-----------------------------------|
| int           | Largura que a tela será alterada  |
| int           | Altura que a tela será alterada   |


=== "Exemplo"
	``` java
	alterarTamanhoTela(10, 50)
	```

### `obterEmpresaAtiva`
----
Este método retorna um objeto do tipo Aac10 contendo os dados da empresa ativa.

=== "Exemplo"
    ``` java
    Aac10 aac10 = obterEmpresaAtiva()
    ```

### `obterUsuarioLogado`
----
Este método retorna um objeto do tipo Aab10 contendo os dados do usuário logado no sistema.

=== "Exemplo"
    ``` java
    Aab10 aab10 = obterUsuarioLogado()
    ```

### `obterWherePadrao`
----
Este método retorna um WHERE filtrando pelos [Campos Default](http://samdoc.info/manuald?id=57791) para ser utilizado em SQLs.

**Argumentos**

| Tipo   | Descrição                      |
|--------|--------------------------------|
| String | Nome da Classe                 |
| Object | Comparador Ex.: WHERE, AND, OR |

=== "Exemplo"
	``` java
	String sql = "SELECT * FROM Eaa01 WHERE eaa01id = 123 " + obterWherePadrao("Eaa01", "AND")
	```
=== "Retorno"
	``` java
	"SELECT * FROM Eaa01 WHERE eaa01id = 123 AND eaa01gc IN (1, 2, 3)"
	```