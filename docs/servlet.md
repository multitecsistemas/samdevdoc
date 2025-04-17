# Servlet

## Introdução

Uma Servlet dá uma ideia de servidor pequeno cujo objetivo basicamente é receber requisições HTTP, processá-las e responder ao cliente, essa resposta pode ser um JSON, um HTML, uma imagem etc.

## Hearders

| Nome                | Valor               | Função                                       | Requerido |
|---------------------|---------------------|----------------------------------------------|-----------|
| api-user-header     | Chave da API do SAM | Autenticar a requisição                      | SIM       |
| ignore-body-decrypt | `true` ou `false`   | ignora a criptografia do corpo da requisição | NÃO       |

## Métodos

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

### `getAcessoAoBanco`
---
Este método retorna uma coleção de métodos uteis para manipulação do banco de dados descritos a baixo:

| Metodo                         | Descrição                                                                                                       |
| -------------------------------| ----------------------------------------------------------------------------------------------------------------|
| buscarListaDeTableMap          | Retorna uma lista de `TableMap` contendo os registros obtidos a partir da execução de uma SQL.                  |
| buscarUnicoTableMap            | Retorna um único `TableMap` contendo o registro obtido a partir da execução de uma SQL.                         |
| buscarListaDeRegistros         | Retorna uma lista de registros (entidades) obtidos a partir da execução de uma SQL.                             |
| buscarRegistroUnico            | Retorna um único registro (entidade) obtido a partir da execução de uma SQL.                                    |
| buscarMultiResultSet           | Retorna um objeto `MultiResultSet` contendo os registros obtidos a partir da execução de uma SQL.               |
| obterMapDeRegistros            | Retorna um `Map` contendo os registros obtidos a partir da execução de uma SQL, usando coluna como chave/valor. |
| obterListaDeBigDecimal         | Retorna uma lista de `BigDecimal` obtidos a partir da execução de uma SQL.                                      |
| obterBigDecimal                | Retorna um único `BigDecimal` obtido a partir da execução de uma SQL.                                           |
| obterListaDeInteger            | Retorna uma lista de `Integer` obtidos a partir da execução de uma SQL.                                         |
| obterInteger                   | Retorna um único `Integer` obtido a partir da execução de uma SQL.                                              |
| obterListaDeDate               | Retorna uma lista de objetos `LocalDate` obtidos a partir da execução de uma SQL.                               |
| obterDate                      | Retorna um único objeto `LocalDate` obtido a partir da execução de uma SQL.                                     |
| obterListaDeString             | Retorna uma lista de `String` obtidas a partir da execução de uma SQL.                                          |
| obterString                    | Retorna uma única `String` obtida a partir da execução de uma SQL.                                              |
| obterListaDeLong               | Retorna uma lista de `Long` obtidos a partir da execução de uma SQL.                                            |
| obterLong                      | Retorna um único `Long` obtido a partir da execução de uma SQL.                                                 |
| buscarRegistroUnicoById        | Retorna um registro de uma tabela pelo ID informado como argumento.                                             |
| buscarRegistroUnicoByCriterion | Retorna um registro de uma tabela filtrado por um `Criterion`.                                                  |

### `criarParametroSql`
----
Este método retorna um objeto do tipo [Parametro](/parametro) para ser utilizado nos métodos que realizam a manipulação do banco de dados que vimos acima.

**Argumentos**

| Tipo   | Descrição |
|--------|-----------|
| String | Chave     |
| Object | Valor     |


=== "Exemplo"
	``` java
	String sql = " SELECT * FROM Abm01 WHERE abm01codigo = :codigo AND abm01tipo = :tipo "
	
	Parametro paramCodigo = criarParametroSql("codigo", "0101001")
	Parametro paramTipo = criarParametroSql("tipo", 0)
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

### `getSession`
----
Este método retorna um objeto do tipo [Session](/session) para manipular o banco de dados.

=== "Exemplo"
	``` java
	Session session = getSession()
	session.persist(xpto)
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

### `converterCorpoRequisicaoParaString`
----
Este método converte o corpo da requisição enviado a um Servlet para String.

=== "Exemplo"
	``` java
	String body = converterCorpoRequisicaoParaString()
	```

### `converterCorpoRequisicaoParaObjeto`
----
Este método converte o corpo da requisição enviado a um Servlet para um objeto do tipo informado como argumento.

**Argumentos:**

| Tipo     | Descrição                          |
|----------|------------------------------------|
| Class<?> | Tipo do objeto que será convertido |

=== "Exemplo"
	``` java
	TableMap body = converterCorpoRequisicaoParaObjeto(TableMap.class)
	```

### `getParametroRequisicao`
----
Este método retorna o conteudo de um parêmetro enviado ao Servlet via URL.

**Argumentos:**

| Tipo   | Descrição          |
|--------|--------------------|
| String | Nome do parâmetro  |

=== "Exemplo"
	``` groovy
	// URL: https://endereco.sam/caminhoServlet?id_registro=12345
	def id_registro = getParametroRequisicao("id_registro")
	```
