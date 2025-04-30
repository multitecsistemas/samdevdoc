# Fórmulas

## Introdução

Uma fórmula é um método prático de resolver um assunto, dar instruções ou expressar uma operação. Em algumas tarefas do SAM4 o processamento de dados pode ser feito de forma customizada, ou seja, cada empresa pode processar livremente. Essas customizações são feitas por meio das fórmulas. Por exemplo, cálculo de documentos, cálculo de folha de pagamento, manipulação de valores de itens no estoque.

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
Este método retorna uma coleção de métodos úteis para manipulação do banco de dados, descritos abaixo:

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

### `selecionarAlinhamento`
----

O alinhamento de valores permite fazer um alinhamento dos campos de registros contidos em um leiaute, uma fórmula, em listagens para alinhar campos livres do sistema (Json), possibilitando usar nas fórmulas um nome padronizado.
Este método seleciona qual alinhamento de valores será utilizado no script

**Argumentos:**

| Tipo   | Descrição                      |
|--------|--------------------------------|
| String | Código do alinhamento          |

=== "Exemplo"
	``` java
	selecionarAlinhamento("0001")
	```

### `getCampo`
----
Este método retorna o campo informado no alinhamento de valores pelo conteúdo do registro. Este método deve ser utilizado após a utilização do método `selecionarAlinhamento`

**Argumentos:**

| Tipo   | Descrição                      |
|--------|--------------------------------|
| String | Registro                       |
| String | Campo                          |

=== "Exemplo"
	``` java
	getCampo("C100", "ICMS")
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

### get()
----

Quando uma Listagem é executada, alguns dados podem ser enviados para o processo, estes dados são conteúdo dos filtros. O envio deste dado é feito através de um Mapa de chave e valor, para recuperar estes dados utilizamos o método `get()` e suas variações.

Exemplo: Em uma listagem existe um campo de data e foi atribuído o nome dataDeInicio.

``` html
<m-date label="Data de Inicio" v-model="filtros.dataDeInicio" />
```

Para recuperar o conteudo deste campo a partir do código groovy utilizamos o método `get()`.

``` groovy
def dataDeInicio = get("dataDeInicio")
```

Este método por si só retorna um objeto. Contamos com alguma variações deste método que nos trazem os dados já convertidos.

| Método              | Retorno           | Método              | Retorno           |
| ------------------- | ----------------- | ------------------- | ----------------- |
| getString()         | Texto             | getLocalDate()      | Data              |
| getBoolean()        | Booleano          | getLocalTime()      | Hora              |
| getInteger()        | Inteiro           | getIntervaloDatas() | Array de Datas    |
| getLong()           | Longo             | getListLong()       | Lista de Longos   |
| getBigDecimal()     | Decimal           | getListInteger()    | Lista de Inteiros |

