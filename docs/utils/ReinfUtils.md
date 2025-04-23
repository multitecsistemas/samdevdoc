# ReinfUtils

Classe utilitária para geração de identificadores e XMLs do Reinf, além de métodos auxiliares para formatação de datas, horas e valores decimais conforme exigências legais.

## Pacote

`sam.server.samdev.utils`

---

## Padrões de Formatação

- `PATTERN_DDMMYYYY`: `"ddMMyyyy"`
- `PATTERN_YYYYMMDD`: `"yyyyMMdd"`
- `PATTERN_YYYY_MM_DD`: `"yyyy-MM-dd"`
- `PATTERN_MMYYYY`: `"MMyyyy"`
- `PATTERN_YYYY_MM`: `"yyyy-MM"`
- `PATTERN_YYYY`: `"yyyy"`
- `PATTERN_HHMMSS`: `"HHmmss"`
- `PATTERN_HHMM`: `"HHmm"`

---

## Geração de Identificador Reinf

#### `static String gerarID(int ti, String ni)`
Gera o ID de um evento Reinf com base em tipo, número identificador, data, hora atual e número sequencial interno.

---

## Criação de XML

#### `static ElementXml configurarXML(String nameSpace)`
Cria a tag raiz do XML com o nome `"Reinf"` e o namespace especificado.

#### `static String gerarXML(ElementXml reinf)`
Converte um `ElementXml` em `String` XML com codificação UTF-8.

---

## Datas e Horas

#### `String formatarData(LocalDate value)`
Formata data no padrão `"ddMMyyyy"`.

#### `String formatarData(LocalDate value, String pattern)`
Formata uma `LocalDate` usando padrão customizado.

#### `String formatarHora(LocalTime value)`
Formata uma `LocalTime` no padrão `"HHmm"`.

#### `String formatarHora(LocalTime value, String pattern)`
Formata uma `LocalTime` com padrão customizado.

#### `String formatarHora(LocalDate value, String pattern)`
Formata uma `LocalDate` como hora. (Uso específico, atenção ao contexto).

---

## Verificação de Inclusão

#### `boolean isInclusao(LocalDate dataCadastro, LocalDate periodo)`
Verifica se a operação corresponde a uma inclusão com base no mês/ano da data de cadastro e do período informado.

---

## Formatação de Decimais

#### `String formatarDecimal(BigDecimal value, int casasDecimais, boolean vlrZeroRetornaNull)`
Formata valores `BigDecimal` no padrão brasileiro com vírgula como separador decimal. Pode retornar `"0,00"` ou `null` se o valor for zero.

---

## Exemplo de uso

```java
String idEvento = ReinfUtils.gerarID(1, "12345678901");
String dataFormatada = ReinfUtils.formatarData(LocalDate.now());
String valorFormatado = ReinfUtils.formatarDecimal(new BigDecimal("100.256"), 2, false);
ElementXml xml = ReinfUtils.configurarXML("http://www.reinf.gov.br/schema");
String conteudoXml = ReinfUtils.gerarXML(xml);
```