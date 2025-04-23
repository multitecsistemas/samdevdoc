
# SFPUtils

Utilitário para operações relacionadas a cálculos trabalhistas e folha de pagamento no contexto do sistema SAM/SFP. Fornece métodos para consulta e processamento de eventos de folha, médias de valores, descontos, adicionais por tempo de serviço, e informações trabalhistas vinculadas a funcionários.

## Pacote

`sam.server.samdev.utils`

---

## Dependências

- `DateUtils`
- `DecimalUtils`
- `Scale`
- `SFPService`
- `SAMWhere`
- `Variaveis`
- `SFPVarDto`
- `Session` e `Query` (multiorm)

---

## Construtor

```java
public SFPUtils(Session session, SAMWhere samWhere, SFPService sfpService, Variaveis variaveis, SFPVarDto sfpVarDto)
```

Inicializa a utilitária com as dependências necessárias para manipulação de dados de folha.

---

## Métodos

### 🔍 Consulta de Valores de Eventos

- `BigDecimal buscarValor(String abh21codigo)`
- `BigDecimal buscarRefHoras(String abh21codigo)`
- `BigDecimal buscarRefDias(String abh21codigo)`
- `BigDecimal buscarRefUnid(String abh21codigo)`

Consulta valores, referências em horas, dias e unidades de um evento específico na folha.

### 📊 Cálculo de Situação e Período

- `int buscarSituacaoDoTrabalhador()`
- `int buscarSituacaoDoTrabalhador(LocalDate data)`
- `boolean trabalhadorEstaEmFerias(LocalDate data)`
- `boolean trabalhadorEstaAfastado(LocalDate data)`

Consulta situação, afastamentos e férias de um trabalhador em determinada data.

### 💸 Aplicação de Tabelas e Cálculos Previdenciários

- `BigDecimal aplicarTabelaDeINSS(String aaj51codigo, BigDecimal valor)`
- `BigDecimal aplicarTabelaDeIR(String aaj50codigo, BigDecimal valor, Integer qtdDepIR)`
- `BigDecimal buscarSalarioFamilia(String aaj51codigo, BigDecimal valor, Integer qtdDepSF)`

Aplica tabelas previdenciárias (INSS, IR, salário-família) para cálculo de deduções e adicionais.

### 📆 Cálculo de Afastamentos

- `BigDecimal buscarDiasAfastados(String abh21codigo, LocalDate dataBase)`
- `Integer buscarMesesAfastados(String abh21codigo, LocalDate dataBase)`

Consulta afastamentos em dias e meses, considerando períodos com afastamento superior a 15 dias.

### 📈 Consultas de Ocorrências e Cálculos na Folha

- `BigDecimal buscarValorDaOcorrencia(...)`
- `BigDecimal buscarValorNoCalculo(...)`
- `BigDecimal buscarValorNoUltimoCalculo(...)`
- `BigDecimal buscarValorNoUltimoCalculo13Salario(...)`

Consulta valores lançados na folha de pagamento com filtros por data, mês, empresa, tipo de valor.

### 📊 Cálculo de Médias

- `BigDecimal buscarMediaDeValores(...)`
- `BigDecimal buscarMediaDeRefHoras(...)`
- `BigDecimal buscarMediaDeRefDias(...)`
- `BigDecimal buscarMediaDeRefUnid(...)`

Calcula médias de valores e referências de eventos por período.

### 🏆 Adicionais e Percentuais

- `BigDecimal buscarPercentualPorTempoDeServico(LocalDate dataBase)`
- `BigDecimal buscarAdicionalPorTempoDeServico(...)`

Calcula percentual e adicional por tempo de serviço.

### 📅 Datas Auxiliares

- `LocalDate buscarDataInicialMaiorRem(LocalDate dataBase, int meses)`
- `LocalDate buscarUltimoDiaMesAnterior(LocalDate dataBase)`

Consulta datas de referência.

### 📄 Consultas de Salários e Dependentes

- `BigDecimal buscarSalarioDoMes()`
- `BigDecimal buscarSalarioDoMesAnterior(LocalDate dataBase)`
- `BigDecimal buscarValorDoSalarioHora(Long abh80id)`
- `BigDecimal buscarValorDoSalarioMes(Long abh80id)`
- `Integer buscarQtdeDependentesIR(Long abh80id)`
- `Integer buscarQtdeDependentesSF(Long abh80id)`

### 📌 Outras Consultas

- `BigDecimal buscarTetoDoInss(String aaj51codigo)`
- `Integer buscarTaxaRAT()`
- `BigDecimal buscarIndiceFAP()`

### 📊 Eventos Relacionados

- `BigDecimal buscarValorEventosRelacionados()`
- `BigDecimal buscarRefDiasEventosRelacionados()`
- `BigDecimal buscarRefHorasEventosRelacionados()`
- `BigDecimal buscarRefUnidEventosRelacionados()`

### 🔢 Operações Matemáticas

- `BigDecimal somarValores(BigDecimal ... valores)`
- `BigDecimal subtrairValores(BigDecimal ... valores)`
- `BigDecimal dividirValores(BigDecimal ... valores)`
- `BigDecimal multipicarValores(BigDecimal ... valores)`

### 📌 Consulta de Períodos e Dependências

- `Fbc01 buscarUltimoPeriodoAquisitivo(Long abh80id)`

---

## Exemplo de uso

```java
BigDecimal valorINSS = sfpUtils.aplicarTabelaDeINSS("INSS2024", new BigDecimal("3500.00"));
System.out.println("Desconto de INSS: " + valorINSS);
```
