# NFeUtils

Classe utilitária para geração de chave de acesso da NFe, formatação de datas e valores, criação de elementos XML e manipulação de informações específicas do contexto fiscal eletrônico.

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
- `PATTERN_UTC`: `"yyyy-MM-dd'T'HH:mm:ss"`
- `PATTERN_PT_BR`: `"dd/MM/yyyy HH:mm:ss"`
- `PATTERN_HHMMSS`: `"HHmmss"`
- `PATTERN_HHMM`: `"HHmm"`

---

## Datas e Horas

#### `String formatarData(LocalDate value)`
Formata a data no padrão `"yyyyMMdd"`.

#### `String formatarData(LocalDate value, String pattern)`
Formata a data com padrão customizado.

#### `String formatarHora(LocalTime value)`
Formata a hora no padrão `"HHmm"`.

#### `String formatarHora(LocalTime value, String pattern)`
Formata a hora com padrão customizado.

#### `String formatarDataHora(LocalDateTime value, String pattern)`
Formata um `LocalDateTime` com o padrão especificado.

#### `String dataFormatoUTC(LocalDateTime data, Integer fusoHorario)`
Formata a data e hora no padrão UTC, com fuso configurável (`-02:00`, `-03:00`, `-04:00`, `-05:00`).

#### `String dataFormatoUTC(LocalDate data, LocalTime hora, Integer fusoHorario)`
Mesma formatação UTC acima, com `LocalDate` e `LocalTime`.

---

## XML

#### `ElementXml criarElementXmlNFe(String namespace)`
Cria um elemento XML com nome `"NFe"`.

#### `ElementXml criarElementXmlNFe(String namespace, String name)`
Cria um elemento XML com nome customizado.

#### `String gerarXML(ElementXml nfe)`
Converte o `ElementXml` para `String` formatada em XML.

---

## Decimal

#### `String formatarDecimal(BigDecimal value, int casasDecimais, boolean vlrZeroRetornaNull)`
Formata um valor decimal para `String`, com opção de retornar `"0"` ou `null` quando for zero.

---

## Inscrição Estadual

#### `String formatarIE(String ie)`
Retorna `"ISENTO"` para inscrições isentas. Caso contrário, retorna apenas os números da string.

---

## Código Numérico

#### `Long gerarCodigoNumerico(Integer abb01num, Long eaa01id)`
Gera um código numérico para composição de chave de acesso, evitando padrões inválidos ou repetidos.

---

## Chave de Acesso NFe

#### `String gerarChaveDeAcesso(Eaa01 eaa01, Aac10 empresa, Integer formaEmissao, Long cNF)`
Gera a chave de acesso da NFe (modelo 55), com 44 dígitos, usando os dados do emitente, modelo, número, forma de emissão e código numérico (`cNF`).

---

## Série da Nota

#### `String tratarSerie(String numSerie)`
Trata a série da nota fiscal, garantindo que tenha no máximo 3 dígitos numéricos. Retorna `"000"` se inválida.

---

## Telefone

#### `String ajustarFone(String ddd, String fone)`
Concatena DDD e número, remove caracteres não numéricos, e retorna telefone limpo ou `null`.

---

## Exemplo de uso

```java
String data = NFeUtils.dataFormatoUTC(LocalDateTime.now(), 0);
String chave = NFeUtils.gerarChaveDeAcesso(eaa01, empresa, 1, 12345678L);
String telefone = NFeUtils.ajustarFone("11", "91234-5678");
```