# DecimalUtils

Utilitário para operações com valores decimais (`BigDecimal`) com métodos encadeáveis, além de suporte para parsing, formatação, arredondamento, comparação e divisão em parcelas.

## Pacote

`br.com.multitec.utils`

---

## Instanciação

#### `static DecimalUtils create(Object value)`
Cria uma nova instância de `DecimalUtils` a partir de um valor (`Number`, `String`, `BigDecimal`, etc). **Não aceita `Double`.**

---

## Operações Matemáticas

#### `DecimalUtils sum(Object... values)`
Soma os valores fornecidos à instância atual.

#### `DecimalUtils subtract(Object... values)`
Subtrai os valores fornecidos da instância atual.

#### `DecimalUtils multiply(Object... values)`
Multiplica os valores fornecidos com o valor atual.

#### `DecimalUtils divide(Object... values)`
Divide o valor atual pelos valores fornecidos utilizando a escala atual.

#### `DecimalUtils round(int casasDecimais)`
Arredonda o valor para o número de casas decimais usando `RoundingMode.HALF_EVEN`.

#### `DecimalUtils trunc(int casasDecimais)`
Trunca o valor para o número de casas decimais usando `RoundingMode.FLOOR`.

#### `DecimalUtils negateIfPositive()`
Inverte o sinal do valor se ele for positivo.

#### `DecimalUtils setScale(MathContext scale)`
Define a escala e modo de arredondamento para futuras operações.

---

## Obtenção de Resultado

#### `BigDecimal get()`
Retorna o valor atual como `BigDecimal`.

---

## Parcelamento

#### `List<BigDecimal> part(int numeroDeParcelas)`
Divide o valor atual em parcelas iguais, corrigindo arredondamentos na última.

#### `List<BigDecimal> part(int numeroDeParcelas, int parcToAddRest)`
Divide o valor e aplica o ajuste de arredondamento na parcela especificada por `parcToAddRest`.

---

## Comparação

#### `int compareTo(Object value)`
Compara o valor atual com outro valor numérico.

---

## Máximo e Mínimo

#### `static BigDecimal max(BigDecimal... values)`
Retorna o maior valor da lista.

#### `static BigDecimal min(BigDecimal... values)`
Retorna o menor valor da lista.

---

## Parsing e Formatação

#### `static DecimalUtils parse(String value)`
Converte uma `String` formatada (ex: `"1.234,56"`) para `DecimalUtils`.

#### `String format()`
Formata o valor com 2 casas decimais (`min` e `max`) para o padrão `pt-BR`.

#### `String format(int maxFractionDigits, int minFractionDigits)`
Formata o valor com controle das casas decimais para o padrão `pt-BR`.

#### `String toString()`
Sobrescreve `toString()` usando o método `format()`.

---

## Exemplo de uso

```java
DecimalUtils valor = DecimalUtils.create("1000");
List<BigDecimal> parcelas = valor.part(3, 2);

System.out.println("Parcelas: " + parcelas);
System.out.println("Total formatado: " + valor.format());
```