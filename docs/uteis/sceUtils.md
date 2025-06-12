# SCEUtils

## Visão Geral

A classe `SCEUtils` é uma classe utilitária que fornece métodos especializados para consultas e operações relacionadas ao Sistema de Controle de Estoque (SCE) no sistema SAM. Ela encapsula consultas complexas de saldo de estoque, lançamentos, preços médios e operações retroativas, servindo como uma camada de abstração entre os serviços de negócio e as operações de controle de estoque.

!!! info "Localização"
    **Pacote:** `sam.server.samdev.utils`

## Métodos de Saldo de Estoque

### 📊 Saldo Resumido

#### saldoEstoqueItemResumido()
Retorna o saldo de estoque do item de forma resumida (valor único).
```java
public BigDecimal saldoEstoqueItemResumido(Long abm01id, Integer aam04disp, Integer aam04posse)
```

|Parâmetro      | Descrição                    |
|---------------|------------------------------|
|**abm01id**    |ID do item                    |
|**aam04disp**  |Código de disponibilidade     |
|**aam04posse** |Código de posse               |

**Exemplo:**
```java
BigDecimal saldo = sceUtils.saldoEstoqueItemResumido(123L, 1, 1);
```

#### saldoEstoqueItemResumido() - Retroativo
Versão retroativa que consulta o saldo em uma data específica.
```java
public BigDecimal saldoEstoqueItemResumido(
    Long abm01id, 
    Integer aam04disp, 
    Integer aam04posse, 
    LocalDate dataDoSaldo
)
```

|Parâmetro        | Descrição                           |
|-----------------|-------------------------------------|
|**dataDoSaldo**  |Data para consulta retroativa        |

#### saldoEstoqueItemResumido() - Completo
Versão completa com filtros adicionais para consulta detalhada.
```java
public BigDecimal saldoEstoqueItemResumido(
    Long abm01id, 
    Integer aam04disp, 
    Integer aam04posse, 
    LocalDate dataDoSaldo, 
    List<Long> aam04ids, 
    List<Long> abm15ids0, 
    List<Long> abm15ids1, 
    List<Long> abm15ids2
)
```

|Parâmetro        | Descrição                           |
|-----------------|-------------------------------------|
|**aam04ids**     |Lista de IDs aam04 para filtro       |
|**abm15ids0**    |Lista de IDs abm15 (nível 0)         |
|**abm15ids1**    |Lista de IDs abm15 (nível 1)         |
|**abm15ids2**    |Lista de IDs abm15 (nível 2)         |

### 📈 Saldo Sintético

#### saldoEstoqueItemSintetico()
Retorna o saldo de estoque agrupado por categorias (visão sintética).
```java
public List<TableMap> saldoEstoqueItemSintetico(Long abm01id, Integer aam04disp, Integer aam04posse)
```

**Retorna:** Lista com dados agrupados do estoque

#### saldoEstoqueItemSintetico() - Retroativo
Versão retroativa para consulta sintética em data específica.
```java
public List<TableMap> saldoEstoqueItemSintetico(
    Long abm01id, 
    Integer aam04disp, 
    Integer aam04posse, 
    LocalDate dataDoSaldo
)
```

#### saldoEstoqueItemSintetico() - Completo
Versão completa com todos os filtros disponíveis.
```java
public List<TableMap> saldoEstoqueItemSintetico(
    Long abm01id, 
    Integer aam04disp, 
    Integer aam04posse, 
    LocalDate dataDoSaldo, 
    List<Long> aam04ids, 
    List<Long> abm15ids0, 
    List<Long> abm15ids1, 
    List<Long> abm15ids2
)
```

### 🔍 Saldo Analítico

#### saldoEstoqueItemAnalitico()
Retorna o saldo de estoque com máximo detalhamento (visão analítica).
```java
public List<TableMap> saldoEstoqueItemAnalitico(Long abm01id, Integer aam04disp, Integer aam04posse)
```

**Retorna:** Lista com dados detalhados do estoque

#### saldoEstoqueItemAnalitico() - Retroativo
Versão retroativa para consulta analítica em data específica.
```java
public List<TableMap> saldoEstoqueItemAnalitico(
    Long abm01id, 
    Integer aam04disp, 
    Integer aam04posse, 
    LocalDate dataDoSaldo
)
```

#### saldoEstoqueItemAnalitico() - Completo
Versão completa com parâmetros adicionais para máximo controle.
```java
public List<TableMap> saldoEstoqueItemAnalitico(
    Long abm01id, 
    Integer aam04disp, 
    Integer aam04posse, 
    LocalDate dataDoSaldo, 
    List<TableMap> tmBcd01s, 
    List<Long> aam04ids, 
    List<Long> abm15ids0, 
    List<Long> abm15ids1, 
    List<Long> abm15ids2
)
```

|Parâmetro        | Descrição                           |
|-----------------|-------------------------------------|
|**tmBcd01s**     |Lista de TableMaps BCD01 específicos |

## Métodos de Consulta de Lançamentos

### 📋 Lançamentos por Data

#### buscarLancamentosEstoqueItemData()
Busca lançamentos de estoque com opção de consulta retroativa ou por período.
```java
public List<TableMap> buscarLancamentosEstoqueItemData(
    Long abm01id, 
    boolean isRetroativo, 
    LocalDate dataRetroativa, 
    Criterion critWherePeriodo, 
    List<Long> aam04ids, 
    List<Long> abm15ids0, 
    List<Long> abm15ids1, 
    List<Long> abm15ids2
)
```

|Parâmetro              | Descrição                                    |
|-----------------------|----------------------------------------------|
|**isRetroativo**       |Se é consulta retroativa                      |
|**dataRetroativa**     |Data para consulta retroativa (null se não retroativo) |
|**critWherePeriodo**   |Critério de filtro por período               |

!!! tip "Uso por Período"
    Para consulta por período específico:
    - `isRetroativo = false`
    - `dataRetroativa = null`
    - `critWherePeriodo` deve conter o filtro desejado

**Exemplo:**
```java
List<TableMap> lancamentos = sceUtils.buscarLancamentosEstoqueItemData(
    123L,           // ID do item
    false,          // Não retroativo
    null,           // Data retroativa null
    criterioPeriodo, // Critério de período
    Arrays.asList(1L, 2L), // IDs AAM04
    null, null, null       // IDs ABM15
);
```

## Métodos de Preço Médio

### 💰 Preço Médio Atual

#### precoMedioUnitarioAtual()
Retorna o preço médio unitário atual do item.
```java
public BigDecimal precoMedioUnitarioAtual(Long abm01id, Long aac10id)
```

|Parâmetro      | Descrição                    |
|---------------|------------------------------|
|**abm01id**    |ID do item                    |
|**aac10id**    |ID do AAC10                   |

### 📊 Preço Médio Retroativo

#### buscarPMRetroativo()
Obtém o preço médio do lançamento imediatamente anterior ao processado.
```java
public BigDecimal buscarPMRetroativo(Long abm01id, LocalDate bcc01data, Long bcc01id)
```

|Parâmetro      | Descrição                    |
|---------------|------------------------------|
|**bcc01data**  |Data do lançamento BCC01      |
|**bcc01id**    |ID do lançamento BCC01        |

**Retorna:** Preço médio (bcc01pmu) do lançamento anterior

## Métodos de Cálculo

### 📈 Saldo Decrescente

#### saldoEstoque()
Calcula o saldo de estoque de forma decrescente.
```java
public BigDecimal saldoEstoque(Long abm01id, LocalDate bcc01data, Long bcc01id)
```

**Lógica de Cálculo:**
- Obtém saldo atual (soma de bcc02)
- Subtrai lançamentos (bcc01) posteriores
- Subtrai lançamento igual ao que está sendo processado

**Exemplo:**
```java
BigDecimal saldoCalculado = sceUtils.saldoEstoque(
    123L,                    // ID do item
    LocalDate.of(2024, 1, 15), // Data do lançamento
    456L                     // ID do lançamento
);
```

## Considerações Técnicas

!!! tip "Boas Práticas"
    - Use `BigDecimal` para cálculos monetários e de precisão
    - Sempre validar parâmetros antes de chamar os métodos
    - Considerar performance ao usar métodos analíticos com grandes volumes
    - Aplicar filtros apropriados para reduzir volume de dados

## Tratamento de Erros

A classe utiliza o tratamento de erros padrão do SCEService. Principais exceções:

- **ValidacaoException**: Parâmetros inválidos ou dados não encontrados
- **RuntimeException**: Erros de banco de dados ou sistema
- **NullPointerException**: Parâmetros obrigatórios não informados