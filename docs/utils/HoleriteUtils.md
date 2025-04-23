# HoleriteUtils

Classe utilitária voltada para consultas relacionadas a **cálculos de holerites**, **eventos**, **férias**, **rescisões**, e informações financeiras de trabalhadores em sistemas baseados no SAM.

## Pacote

`sam.server.samdev.utils`

---

## Construtor

#### `HoleriteUtils(Session session, SAMWhere samWhere)`
Inicializa a classe com uma sessão ativa do MultiORM e as regras padrão de filtragem do sistema (`SAMWhere`).

---

## Consultas de Entidades

#### `Abh80 findAbh80ByUniqueKey(String abh80codigo)`
Busca um trabalhador (`Abh80`) pelo código, com joins de cargo e departamento.

#### `Abh21 findAbh21ByUniqueKey(String abh21codigo)`
Busca um evento de folha (`Abh21`) pelo código.

---

## Consultas de Eventos FBA01011

#### `List<TableMap> findDadosFba01011sCAEByRemessaHoleriteTxt(...)`
Retorna dados de eventos de CAE para um trabalhador em um período específico, para uso em geração de arquivo texto de holerite.

#### `List<TableMap> findDadosFba01011sCAEByRemessaHolerite(...)`
Mesmo que o anterior, sem foco no TXT.

#### `List<TableMap> findDadosFba01011sByExportarHoleriteParaTxt(...)`
Consulta eventos agrupados para exportação de holerite, ignorando eventos específicos se necessário.

#### `List<TableMap> findDadosFba01011sByRemessaHolerite(...)`
Versão alternativa para exportação de dados sem o filtro para eventos de férias.

---

## Dependentes

#### `Integer findAbh8002QtdeDependentesIR(Long idAbh80)`
Retorna a quantidade de dependentes considerados para IR.

#### `Integer findAbh8002QtdeDependentesSF(Long idAbh80)`
Retorna dependentes considerados para salário-família.

#### `Integer findAbh8002QtdeDependentes(Long idAbh80)`
Retorna a quantidade total de dependentes.

---

## Consultas e Cálculos Diversos

#### `Fbc0101 findFbc0101UltimoCalculoByIdTrabalhadorAndTipoFerias(Long idAbh80)`
Busca o último cálculo de férias de um trabalhador.

#### `BigDecimal findFba01011RefByTrabAndEventoAndData(...)`
Soma os dias de referência de um evento para um trabalhador em um período.

#### `List<TableMap> calcularFeriasRescisaoPagas(...)`
Calcula eventos que devem compensar (zerar) valores líquidos de férias e rescisões, como abonos e adiantamentos.

#### `BigDecimal findFba01011ValorEventoParaZerarFeriasAndRescisaoTxt(...)`
Soma os valores de um evento para zerar férias/rescisão em exportações para texto.

#### `TableMap findFba01011ValorEventoParaZerarFeriasAndRescisaoHolerite(...)`
Similar ao anterior, mas retorna também os dias de referência como `TableMap`.

#### `BigDecimal calcularCAE(...)`
Soma e subtrai valores de eventos de CAE, considerando seu fator de compensação (`abh2101cvr`).

---

## Exemplo de uso

```java
HoleriteUtils util = new HoleriteUtils(session, samWhere);

Abh80 trabalhador = util.findAbh80ByUniqueKey("000123");
Integer qtdeDependentes = util.findAbh8002QtdeDependentes(trabalhador.getId());
BigDecimal refDias = util.findFba01011RefByTrabAndEventoAndData(trabalhador.getId(), "0021", LocalDate.now().minusMonths(1), LocalDate.now());
```