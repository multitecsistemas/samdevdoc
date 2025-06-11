# BancoDadosUtils

## Visão Geral

A classe `BancoDadosUtils` é uma classe utilitária que fornece métodos simplificados para operações no banco de dados no sistema SAM. Ela encapsula funcionalidades do MultiORM e oferece uma interface mais amigável para execução de consultas SQL, operações CRUD e manipulação de dados.

!!! info "Localização"
    **Pacote:** `sam.server.samdev.utils`

## Métodos de Consulta

### 📋 TableMap - Mapas de Dados

#### buscarListaDeTableMap()
Executa consultas SQL retornando listas de `br.com.multitec.utils.collections.TableMap` (mapas chave-valor).
```java
public List<TableMap> buscarListaDeTableMap(String sql)
public List<TableMap> buscarListaDeTableMap(String sql, Parametro... parametros)
public List<TableMap> buscarListaDeTableMap(String sql, boolean isPagina, int pagina, Parametro... parametros)
public List<TableMap> buscarListaDeTableMap(String sql, boolean isPagina, int pagina, int tamanhoPagina, Parametro... parametros)
```

|Parametro         | descrição                                  |
|------------------|--------------------------------------------|
|**sql**           |Consulta SQL a ser executada                |
|**parametros**    |Parâmetros nomeados da consulta (opcional)  |
|**isPagina**      |Se deve aplicar paginação                   |
|**pagina**        |Número da página (baseado em zero)          |
|**tamanhoPagina** |Tamanho da página (padrão: 1000)            |


#### buscarUnicoTableMap()
Executa consulta SQL retornando um único `br.com.multitec.utils.collections.TableMap`.
```java
public TableMap buscarUnicoTableMap(String sql)
public TableMap buscarUnicoTableMap(String sql, Parametro... parametros)
```

!!! tip "Uso Recomendado"
    Use `TableMap` quando precisar de flexibilidade nos dados retornados ou quando trabalhar com consultas com JOINs complexos.

### 🗃️ Entidades - Registros Tipados

#### buscarListaDeRegistros()
Executa consultas SQL retornando listas de entidades tipadas.
```java
public <T extends MultiEntity> List<T> buscarListaDeRegistros(String sql)
public <T extends MultiEntity> List<T> buscarListaDeRegistros(String sql, Parametro... parametros)
public <T extends MultiEntity> List<T> buscarListaDeRegistros(String sql, boolean isPagina, int pagina, Parametro... parametros)
```

#### buscarRegistroUnico()
Executa consulta SQL retornando uma única entidade.
```java
public <T extends MultiEntity> T buscarRegistroUnico(String sql)
public <T extends MultiEntity> T buscarRegistroUnico(String sql, Parametro... parametros)
```


**Exemplo:**
```java
// Buscar entidades por Código
String sql = "SELECT * FROM abe01 WHERE abe01codigo = :codigo";
Abe01 funcionario = buscarRegistroUnico(sql, Parametro.criar("codigo", "12345678901"));
```

### 🔢 Tipos Primitivos

#### BigDecimal
```java
public BigDecimal obterBigDecimal(String sql)
public BigDecimal obterBigDecimal(String sql, Parametro... parametros)
public List<BigDecimal> obterListaDeBigDecimal(String sql)
public List<BigDecimal> obterListaDeBigDecimal(String sql, Parametro... parametros)
public List<BigDecimal> obterListaDeBigDecimal(String sql, boolean isPagina, int pagina, Parametro... parametros)
```

!!! note "Valor Padrão"
    O método `obterBigDecimal()` retorna `BigDecimal(0)` quando o resultado é `null`.

#### Integer
```java
public Integer obterInteger(String sql)
public Integer obterInteger(String sql, Parametro... parametros)
public List<Integer> obterListaDeInteger(String sql)
public List<Integer> obterListaDeInteger(String sql, Parametro... parametros)
public List<Integer> obterListaDeInteger(String sql, boolean isPagina, int pagina, Parametro... parametros)
```

!!! note "Valor Padrão"
    O método `obterInteger()` retorna `0` quando o resultado é `null`.

#### String
```java
public String obterString(String sql)
public String obterString(String sql, Parametro... parametros)
public List<String> obterListaDeString(String sql)
public List<String> obterListaDeString(String sql, Parametro... parametros)
public List<String> obterListaDeString(String sql, boolean isPagina, int pagina, Parametro... parametros)
```

#### Long
```java
public Long obterLong(String sql)
public Long obterLong(String sql, Parametro... parametros)
public List<Long> obterListaDeLong(String sql)
public List<Long> obterListaDeLong(String sql, Parametro... parametros)
public List<Long> obterListaDeLong(String sql, boolean isPagina, int pagina, Parametro... parametros)
```

#### LocalDate
```java
public LocalDate obterDate(String sql)
public LocalDate obterDate(String sql, Parametro... parametros)
public List<LocalDate> obterListaDeDate(String sql)
public List<LocalDate> obterListaDeDate(String sql, Parametro... parametros)
public List<LocalDate> obterListaDeDate(String sql, boolean isPagina, int pagina, Parametro... parametros)
```

### 🔍 Métodos Especializados

#### buscarMultiResultSet()
Executa consulta retornando um `MultiResultSet` para processamento de múltiplos conjuntos de resultados.
```java
public MultiResultSet buscarMultiResultSet(String sql)
public MultiResultSet buscarMultiResultSet(String sql, Parametro... parametros)
```


#### obterMapDeRegistros()
Cria um mapa a partir dos resultados da consulta.
```java
public Map<String, String> obterMapDeRegistros(String sql, String colunaKey, String colunaValue)
```

|Parametro        | descrição                        |
|-----------------|----------------------------------|
|**sql**          |Consulta SQL                      |
|**colunaKey**    |Nome da coluna para chave do mapa |
|**colunaValue**  |Nome da coluna para valor do mapa |

#### obterCount()
Executa consulta de contagem retornando um `Integer`.
```java
public Integer obterCount(String sql, Parametro... parametros)
```


## Métodos de Busca por Critérios

### buscarRegistroUnicoById()
Busca um registro pelo ID com todos os JOINs configurados no dicionário de dados.
```java
public <T extends MultiEntity> T buscarRegistroUnicoById(String clazz, Long id)
```


### buscarRegistroUnicoByCriterion()
Busca um registro usando critérios personalizados.
```java
public <T extends MultiEntity> T buscarRegistroUnicoByCriterion(String clazz, Criterion... criterion)
```

**Exemplo:**
```java
// Buscar entidade por código
Funcionario funcionario = db.buscarRegistroUnicoByCriterion("abe01", Criterions.eq("abe01codigo", "123456"));
```

## Métodos de Sistema

### 🏢 Dados da Empresa

#### obterEmpresa()
Retorna dados completos de uma empresa.
```java
public Aac10 obterEmpresa(Long aac10id)
```

#### buscarIEEmpresaPorEstado()
Busca a Inscrição Estadual de uma empresa em um estado específico.
```java
public String buscarIEEmpresaPorEstado(Long aac10id, Long aag02id)
```

### ⚙️ Parâmetros do Sistema

#### buscarParametro()
Busca o valor de um parâmetro do sistema.
```java
public <T> T buscarParametro(String param, String aplic)
```

|Parametro  | descrição         |
|-----------|-------------------|
|**param**  |Nome do parâmetro  |
|**aplic**  |Nome da aplicação  |


### 📄 Repositório JSON

#### buscarRepositorioJson()
Busca dados do repositório JSON com código e cláusula WHERE específicos.
```java
public Aba2001 buscarRepositorioJson(String aba20codigo, String where)
```

## Métodos de Exclusão

### deletarRegistro()
Exclui um registro específico.
```java
public void deletarRegistro(MultiEntity obj)
public void deletarRegistro(String clazz, Long id)
```

### deletarRegistros()
Exclui múltiplos registros de uma vez.
```java
public void deletarRegistros(String clazz, List<Long> ids)
```

### deletarRegistrosBySQL()
Executa exclusão via SQL personalizado.
```java
public void deletarRegistrosBySQL(String sql, Parametro... parametros)
```
**Exemplo:**
```java
deletarRegistrosBySQL("DELETE FROM abe01 WHERE abe01id < :abe01id",Parametro.criar("abe01id", 123456));
```

## Paginação

Todos os métodos de lista suportam paginação opcional:

| Parâmetro       | Tipo      | Descrição                           |
|-----------------|-----------|-------------------------------------|
| `isPagina`      | `boolean` | Ativa/desativa paginação            |
| `pagina`        | `int`     | Número da página (baseado em zero)  |
| `tamanhoPagina` | `int`     | Registros por página (padrão: 1000) |

**Exemplo:**
```java
// Buscar segunda página com 50 registros por página
List<TableMap> resultados = buscarListaDeTableMap(
    "SELECT * FROM abe01",
    true, // isPagina
    1,    // página (segunda página)
    50   // tamanhoPagina
);
```

## Tratamento de Parâmetros

A classe trata automaticamente parâmetros `null`, ignorando-os durante a execução da consulta. Isso permite flexibilidade na passagem de parâmetros condicionais.

```java
// Parâmetros podem ser null
Parametro[] params = {
    condicao1 ? Parametro.criar("param1", valor1) : null,
    condicao2 ? Parametro.criar("param2", valor2) : null
};

List<TableMap> resultados = buscarListaDeTableMap(sql, params);
```

## Tratamento de Erros

!!! warning "Exceções Comuns"
    - `ValidacaoException`: Lançada quando parâmetros obrigatórios não são fornecidos
    - `RuntimeException`: Encapsula erros de banco de dados e outras exceções técnicas

## Notas Importantes

!!! tip "Performance"
    - Use paginação para consultas que podem retornar muitos registros
    - Prefira `buscarRegistroUnico()` quando souber que haverá apenas um resultado
    - Use `TableMap` para consultas com JOINs complexos que não mapeiam diretamente para entidades

!!! info "Tipos de Retorno"
    - Métodos `obter*()` retornam valores padrão quando o resultado é `null`
    - Métodos `buscar*()` podem retornar `null`
    - Listas nunca são `null`, mas podem estar vazias