# MDFeUtils

Classe utilitária com métodos para geração de chave de acesso MDF-e, formatação de datas e horas no padrão UTC, criação de XML e formatação de valores utilizados no contexto de documentos fiscais eletrônicos.

## Pacote

`sam.server.samdev.utils`

---

## Constantes

- `DateTimeFormatter yyMM`: Formato `yyMM` (ano e mês).
- `DateTimeFormatter UTC`: Formato ISO `yyyy-MM-dd'T'HH:mm:ss`.

---

## Geração de Chave de Acesso

#### `static String gerarChaveDeAcesso(String codigoIbge, LocalDate emissao, String serie, Integer numero, Long eaa10id, String aac10ni, String modelo, int formaEmissao)`
Gera uma chave de acesso para MDF-e (modelo 58) a partir das informações do emitente, modelo, número, série e forma de emissão. A chave possui 44 dígitos com cálculo de dígito verificador.

---

## XML

#### `static ElementXml criarElementXmlNFe(String namespace)`
Cria o elemento raiz do XML com o nome padrão `"MDFe"`.

#### `static ElementXml criarElementXmlNFe(String namespace, String name)`
Permite definir o nome da raiz ao criar o elemento XML.

#### `static String gerarXML(ElementXml nfe)`
Converte o `ElementXml` para `String` no formato XML, com codificação UTF-8.

---

## Datas no Formato UTC

#### `static String dataFormatoUTC(LocalDateTime data)`
Converte um `LocalDateTime` para o formato UTC ISO 8601 com offset fixo `-03:00`.

#### `static String dataFormatoUTC(LocalDate data, LocalTime hora)`
Converte uma data e hora para o formato UTC. Se `hora` for `null`, usa o horário atual (`MDate.time()`).

---

## Formatação de Valores

#### `static String formatarDecimal(BigDecimal value, int casasDecimais, boolean vlrZeroRetornaNull)`
Formata um valor decimal com o número de casas decimais especificado. Retorna `"0"` ou `null` se o valor for zero, dependendo do parâmetro `vlrZeroRetornaNull`.

---

## Inscrição Estadual

#### `static String formatarIE(String ie)`
Formata a inscrição estadual. Se o valor for `"ISENTO"` ou `"ISENTA"`, retorna `"ISENTO"`. Caso contrário, retorna apenas os números da string. Se for `null`, assume `"ISENTO"`.

---

## Exemplo de uso

```java
String chave = MDFeUtils.gerarChaveDeAcesso("35", LocalDate.now(), "1", 123456, 456789L, "12345678000195", "58", 1);
String xml = MDFeUtils.gerarXML(MDFeUtils.criarElementXmlNFe("http://www.portalfiscal.inf.br/mdfe"));
String dataUTC = MDFeUtils.dataFormatoUTC(LocalDateTime.now());
String valorFormatado = MDFeUtils.formatarDecimal(new BigDecimal("154.457"), 2, false);
```