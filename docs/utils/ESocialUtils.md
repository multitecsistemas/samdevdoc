# ESocialUtils

Classe utilitária para manipulações específicas de datas, horas, XML e formatos numéricos utilizados no contexto do **eSocial**.

## Pacote

`sam.server.samdev.utils`

---

## Constantes

- `PATTERN_DDMMYYYY`: `"ddMMyyyy"`
- `PATTERN_YYYYMMDD`: `"yyyyMMdd"`
- `PATTERN_YYYY_MM_DD`: `"yyyy-MM-dd"`
- `PATTERN_MMYYYY`: `"MMyyyy"`
- `PATTERN_YYYY_MM`: `"yyyy-MM"`
- `PATTERN_YYYY`: `"yyyy"`
- `PATTERN_HHMMSS`: `"HHmmss"`
- `PATTERN_HHMM`: `"HHmm"`
- `VERSAO`: `"v02_04_01"`

---

## Geração de ID

#### `static String comporIdDoEvento(int ti, String ni)`
Gera o ID de um evento eSocial com base no tipo de evento (`ti`), no número identificador (`ni`), na data e hora atual, e um número sequencial interno.

---

## Formatação de Datas e Horas

#### `static String formatarData(LocalDate value)`
Formata a data no padrão `ddMMyyyy`.

#### `static String formatarData(LocalDate value, String pattern)`
Formata a data utilizando o padrão fornecido.

#### `static String formatarHora(LocalTime value)`
Formata a hora no padrão `HHmm`.

#### `static String formatarHora(LocalTime value, String pattern)`
Formata a hora com o padrão personalizado.

#### `static String formatarHora(LocalDate value, String pattern)`
Formata uma data como se fosse uma hora (uso específico com `LocalDate`, cuidado ao usar).

---

## XML

#### `static String gerarXML(ElementXml eSocial)`
Converte um objeto `ElementXml` em uma `String` XML utilizando `Transformer`.

#### `static ElementXml criarElementXmlESocial(String namespace)`
Cria a tag raiz `eSocial` com o namespace fornecido, usando `XMLConverter`.

---

## Formatação de Decimais

#### `static String formatarDecimal(BigDecimal value, int casasDecimais, boolean vlrZeroRetornaNull)`
Formata um `BigDecimal` com o número especificado de casas decimais. Se `value` for zero e `vlrZeroRetornaNull` for `true`, retorna `null`.

---

## Exemplo de uso

```java
String idEvento = ESocialUtils.comporIdDoEvento(1, "12345678901");
String dataFormatada = ESocialUtils.formatarData(LocalDate.now());
String hora = ESocialUtils.formatarHora(LocalTime.now());

ElementXml eSocial = ESocialUtils.criarElementXmlESocial("http://www.esocial.gov.br/schema");
String xml = ESocialUtils.gerarXML(eSocial);

BigDecimal valor = new BigDecimal("123.456");
String valorFormatado = ESocialUtils.formatarDecimal(valor, 2, false);
```