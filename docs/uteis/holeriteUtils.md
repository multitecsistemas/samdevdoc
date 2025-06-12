# HoleriteUtils

## Visão Geral

A classe `HoleriteUtils` é uma classe utilitária que fornece métodos especializados para operações relacionadas a holerites (folhas de pagamento) no sistema SAM. Ela encapsula consultas complexas de folha de pagamento, cálculos de valores, processamento de férias e rescisões, e geração de dados para relatórios.

!!! info "Localização"
    **Pacote:** `sam.server.samdev.utils`

## Métodos de Busca de Entidades

### 👤 Funcionários

#### findAbh80ByUniqueKey()
Busca um funcionário pelo código único com cargo e departamento carregados.
```java
public Abh80 findAbh80ByUniqueKey(String abh80codigo)
```

|Parâmetro        | Descrição                  |
|-----------------|----------------------------|
|**abh80codigo**  |Código único do funcionário |

**Exemplo:**
```java
Abh80 funcionario = holeriteUtils.findAbh80ByUniqueKey("001234");
```

### 📋 Eventos de Folha

#### findAbh21ByUniqueKey()
Busca um evento de folha de pagamento pelo código.
```java
public Abh21 findAbh21ByUniqueKey(String abh21codigo)
```

|Parâmetro        | Descrição           |
|-----------------|---------------------|
|**abh21codigo**  |Código do evento     |

## Métodos de Dados de Folha

### 🏢 Dados CAE (Cadastro de Atividade Econômica)

#### findDadosFba01011sCAEByRemessaHolerite()
Busca dados de folha para CAE específico com informações de CVR.
```java
public List<TableMap> findDadosFba01011sCAEByRemessaHolerite(
    Long idAbh80, 
    ClientCriterion critAbb11, 
    String codCAE, 
    LocalDate dataInicial, 
    LocalDate dataFinal, 
    Set<Integer> tiposFba0101
)
```

|Parâmetro         | Descrição                           |
|------------------|-------------------------------------|
|**idAbh80**       |ID do funcionário                    |
|**critAbb11**     |Critério de filtro por departamento  |
|**codCAE**        |Código do CAE                        |
|**dataInicial**   |Data inicial do período              |
|**dataFinal**     |Data final do período                |
|**tiposFba0101**  |Tipos de valores a buscar            |

**Retorna:** Lista com campos `fba01011valor` e `abh2101cvr`

#### findDadosFba01011sCAEByRemessaHoleriteTxt()
Versão específica para exportação em formato texto.
```java
public List<TableMap> findDadosFba01011sCAEByRemessaHoleriteTxt(
    Long idAbh80, 
    ClientCriterion critAbb11, 
    String codCAE, 
    LocalDate dataInicial, 
    LocalDate dataFinal, 
    Set<Integer> tiposFba0101
)
```

### 📊 Dados Agrupados por Evento

#### findDadosFba01011sByRemessaHolerite()
Busca dados agrupados por evento para geração de holerite.
```java
public List<TableMap> findDadosFba01011sByRemessaHolerite(
    Long idAbh80,
    ClientCriterion critAbb11,
    LocalDate dataInicial,
    LocalDate dataFinal,
    Set<Integer> tiposFba0101,
    int tipoAbh21,
    String eveFerNaoImpr
)
```

|Parâmetro          | Descrição                                      |
|-------------------|------------------------------------------------|
|**idAbh80**        |ID do funcionário                               |
|**critAbb11**      |Critério de filtro por departamento             |
|**dataInicial**    |Data inicial do período                         |
|**dataFinal**      |Data final do período                           |
|**tiposFba0101**   |Tipos de valores a buscar                       |
|**tipoAbh21**      |Tipo do evento                                  |
|**eveFerNaoImpr**  |Código do evento de férias não impresso (opcional) |

**Retorna:** Lista agrupada com campos `abh21codigo`, `abh21nome`, `ref` (referência), `valor`

#### findDadosFba01011sByExportarHoleriteParaTxt()
Versão para exportação em formato texto.
```java
public List<TableMap> findDadosFba01011sByExportarHoleriteParaTxt(
    Long idAbh80,
    ClientCriterion critAbb11,
    LocalDate dataInicial,
    LocalDate dataFinal,
    Set<Integer> tiposFba0101,
    int tipoAbh21,
    String eveFerNaoImpr
)
```

## Métodos de Contagem

### 👨‍👩‍👧‍👦 Dependentes

#### findAbh8002QtdeDependentesIR()
Conta dependentes para Imposto de Renda.
```java
public Integer findAbh8002QtdeDependentesIR(Long idAbh80)
```

**Critério:** `abh8002ir = 1`

#### findAbh8002QtdeDependentesSF()
Conta dependentes para Salário Família.
```java
public Integer findAbh8002QtdeDependentesSF(Long idAbh80)
```

**Critério:** `abh8002sf = 1 OR abh8002sf = 2`

#### findAbh8002QtdeDependentes()
Conta total de dependentes.
```java
public Integer findAbh8002QtdeDependentes(Long idAbh80)
```

## Métodos de Cálculo

### 💰 Cálculo de CAE

#### calcularCAE()
Calcula o valor total do CAE considerando CVR (Crédito/Débito).
```java
public BigDecimal calcularCAE(
    Long abh80id,
    ClientCriterion critAbb11,
    String codCAE,
    LocalDate dataInicial,
    LocalDate dataFinal,
    Set<Integer> tiposFba0101
)
```

**Lógica de Cálculo:**
- Se `abh2101cvr = 0`: **soma** o valor
- Se `abh2101cvr ≠ 0`: **subtrai** o valor

**Exemplo:**
```java
BigDecimal valorCAE = holeriteUtils.calcularCAE(
    funcionario.getAbh80id(),
    criterioDepto,
    "001",
    LocalDate.of(2024, 1, 1),
    LocalDate.of(2024, 1, 31),
    Set.of(1, 2, 3)
);
```

### 🏖️ Cálculo de Férias e Rescisões

#### calcularFeriasRescisaoPagas()
Calcula valores de férias e rescisões pagas para zeragem.
```java
public List<TableMap> calcularFeriasRescisaoPagas(
    ClientCriterion critAbb11,
    Long idAbh80,
    LocalDate dataInicial,
    LocalDate dataFinal,
    Set<Integer> tiposFba0101,
    String eveFeriasLiquida,
    String eveFeriasPagas,
    String eveAbonoLiquido,
    String eveAbonoPago,
    String eveAd13Liquido,
    String eveAd13Pago,
    String eveResLiquida,
    String eveResPaga
)
```

## Métodos Auxiliares

### 📅 Referências por Período

#### findFba01011RefByTrabAndEventoAndData()
Busca referência (dias) por funcionário, evento e período.
```java
public BigDecimal findFba01011RefByTrabAndEventoAndData(
    Long idTrab,
    String evento,
    LocalDate dtInicial,
    LocalDate dtFinal
)
```

**Filtros Aplicados:**
- `fba0101tpVlr = 0` (apenas tipo 0)
- Período entre `dtInicial` e `dtFinal`

### 💵 Valores para Zeragem

#### findFba01011ValorEventoParaZerarFeriasAndRescisaoTxt()
Busca valor específico para zeragem de férias/rescisão (versão texto).
```java
public BigDecimal findFba01011ValorEventoParaZerarFeriasAndRescisaoTxt(
    ClientCriterion critAbb11,
    Long idAbh80,
    LocalDate dataInicial,
    LocalDate dataFinal,
    int tipoFba0101,
    String codAbh21
)
```

#### findFba01011ValorEventoParaZerarFeriasAndRescisaoHolerite()
Busca valor e referência para zeragem de férias/rescisão (versão holerite).
```java
public TableMap findFba01011ValorEventoParaZerarFeriasAndRescisaoHolerite(
    ClientCriterion critAbb11,
    Long idAbh80,
    LocalDate dataInicial,
    LocalDate dataFinal,
    int tipoFba0101,
    String codAbh21,
    String eveFerNaoImpr
)
```

**Retorna:** `TableMap` com campos `ref` (referência) e `valor`

### 🏖️ Último Cálculo de Férias

#### findFbc0101UltimoCalculoByIdTrabalhadorAndTipoFerias()
Busca o último cálculo de férias do funcionário.
```java
public Fbc0101 findFbc0101UltimoCalculoByIdTrabalhadorAndTipoFerias(Long idAbh80)
```

## Considerações Técnicas

!!! tip "Boas Práticas"
    - Sempre verificar se entidades retornadas não são `null`
    - Considerar performance ao usar métodos que fazem múltiplas consultas
    - Aplicar critérios de departamento quando necessário para segurança

## Tratamento de Erros

A classe utiliza o tratamento de erros padrão do MultiORM. Principais exceções:

- **ValidacaoException**: Dados inválidos ou não encontrados
- **RuntimeException**: Erros de banco de dados ou sistema
- **NullPointerException**: Parâmetros obrigatórios não informados