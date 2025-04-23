# DateUtils

Utilitário para manipulação e formatação de datas e horas em Java. Fornece métodos para cálculo de diferença entre datas, parsing, formatação e validações.

## Pacote

`br.com.multitec.utils`

---

## Métodos

### Cálculo de Diferença

#### `long dateDiff(LocalTime ini, LocalTime fim, ChronoUnit unit)`
Calcula a diferença entre dois horários no mesmo dia.

#### `long dateDiff(LocalDate ini, LocalDate fim, ChronoUnit unit)`
Calcula a diferença entre duas datas usando uma hora padrão (01:00:00).

#### `long dateDiff(LocalDateTime ini, LocalDateTime fim, ChronoUnit unit)`
Calcula a diferença entre dois `LocalDateTime`, considerando a precisão do `ChronoUnit` fornecido.

#### `long dateDiffWorkMinutes(LocalDateTime ini, LocalDateTime fim)`
Retorna a diferença em minutos entre dois `LocalDateTime`, adicionando +1 minuto.

#### `long dateDiffWorkMinutes(LocalTime ini, LocalTime fim)`
Mesmo comportamento do método anterior, porém com `LocalTime`.

---

### Obtenção de Intervalos

#### `LocalDate[] getStartAndEndMonth(LocalDate base)`
Retorna o primeiro e o último dia do mês de uma data base.

---

### Validação de Intervalo

#### `boolean isDateWithinRange(LocalDate data, LocalDate ini, LocalDate fim)`
Verifica se uma data está dentro de um intervalo (inclusive).

---

### Parsing de Datas

#### `LocalDate parseDate(String value)`
Converte uma `String` no formato `dd/MM/yyyy` para `LocalDate`.

#### `LocalDate parseDate(String value, String pattern)`
Converte uma `String` para `LocalDate` usando um padrão específico.

#### `LocalDateTime parseDateTime(String value)`
Converte uma `String` no formato `dd/MM/yyyy HH:mm` para `LocalDateTime`.

#### `LocalDateTime parseDateTime(String value, String pattern)`
Converte uma `String` para `LocalDateTime` usando um padrão específico.

#### `LocalTime parseTime(String value)`
Converte uma `String` no formato `HH:mm` para `LocalTime`.

#### `LocalTime parseTime(String value, String pattern)`
Converte uma `String` para `LocalTime` usando um padrão específico.

---

### Formatação de Datas

#### `String formatDate(LocalDate value)`
Formata uma data no padrão `dd/MM/yyyy`.

#### `String formatDate(LocalDate value, String pattern)`
Formata uma data em um padrão customizado.

#### `String formatDateTime(LocalDateTime value)`
Formata um `LocalDateTime` no padrão `dd/MM/yyyy HH:mm`.

#### `String formatDateTime(LocalDateTime value, String pattern)`
Formata um `LocalDateTime` com padrão customizado.

#### `String formatTime(LocalTime value)`
Formata um `LocalTime` no padrão `HH:mm`.

#### `String formatTime(LocalTime value, String pattern)`
Formata um `LocalTime` com padrão customizado.

---

### Outros

#### `Integer numMeses(Integer mes, Integer ano)`
Converte um par de ano e mês no total de meses desde o ano zero.

#### `long dateTimeToUTC(LocalDateTime time)`
Converte um `LocalDateTime` para timestamp em milissegundos UTC.

---

## Exemplo de uso

```java
LocalDate inicio = LocalDate.of(2024, 1, 1);
LocalDate fim = LocalDate.of(2024, 4, 1);
long dias = DateUtils.dateDiff(inicio, fim, ChronoUnit.DAYS);
System.out.println("Diferença em dias: " + dias);
```