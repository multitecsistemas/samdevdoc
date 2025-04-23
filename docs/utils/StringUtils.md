
# StringUtils

Classe utilitária para operações de manipulação, formatação e transformação de `String` em Java.

## Pacote

`br.com.multitec.utils`

---

## Métodos

### 📏 Contagem e Capitalização

- `int count(String texto, String character)`
- `String capitalize(String value)`
- `String capitalize(String value, boolean lowerRest)`
- `String decapitalize(String value)`
- `String toTitleCase(String phrase)`

### 📑 Extração de Substrings

- `String extractNumbers(String texto)`
- `String extractLetters(String texto)`
- `String extractBetweenText(String templateStart, String templateEnd, String message)`
- `String substringAfterLast(String texto, String character)`
- `String substringAfterFirst(String texto, String str)`
- `String substringBeforeFirst(String texto, String character)`
- `String substringBeforeLast(String texto, String character)`
- `String substringBetween(String texto, String strStart, String strEnd)`

### 📝 Concatenação e Streams

- `String concat(Object ... values)`
- `Stream<String> stream(Object ... values)`

### 🛑 Validações

- `boolean isNullOrEmpty(String val)`
- `boolean isEquals(String string, String value)`

### 📄 StackTrace

- `String getStackTrace(Throwable t)`

### 🎭 Máscaras e Formatação

- `String toNumberMask(String mask, String value)`
- `String formatByClass(Object value)`
- `String formatByClass(Object value, boolean emptyOnNull)`

### ✂️ Ajuste e Limitação de Strings

- `String crop(String value, int maxLength)`
- `String crop(String value, int maxLength, String textOverflow)`
- `String wrap(String text, int lineSize)`
- `String wrap(String text, int lineSize, String lineWrap)`
- `String ajustString(Object value, int tamanho)`
- `String ajustString(Object value, int length, String character, boolean leftConcat)`
- `String ajustString(Object value, int length, char character, boolean leftConcat)`

### 📛 Normalização de Nomes e Texto

- `String string2ValidJavaName(String name)`
- `String unaccented(String text)`

### 📝 Templates e Mensagens

- `String message(String pattern, Object ... params)`
- `String messageByNames(String pattern, Object ... params)`
- `String messageByNames(String pattern, Map<String, Object> map)`

### 📜 Query e Espaços

- `String createSelectWithAlias(String className, String fields)`
- `String space(int tamanho)`

### 🔒 Criptografia Simples

- `String criptografaSimples(String senha)`
- `String descriptografaSimples(String senhaCriptografada)`

### 🔐 Base64

- `String base64Encode(String src)`
- `String base64Decode(String src)`

---

## Exemplo de uso

```java
String capitalizado = StringUtils.capitalize("exemplo");
System.out.println(capitalizado); // Exemplo
```

