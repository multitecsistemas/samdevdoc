
# Utils

Classe utilitária com métodos genéricos de apoio para manipulação de coleções, strings, mapas, criptografia, validações e outros recursos utilitários comuns.

## Pacote

`br.com.multitec.utils`

---

## Métodos

### 📌 Validações e Comparações

- `boolean in(Object value, Object ... in)`
- `boolean inIgnoreCase(String value, String ... in)`
- `boolean isEmpty(Collection<?> collection)`
- `boolean isEquals(Object obj1, Object obj2)`
- `boolean jsBoolean(Object value)`
- `boolean isAllNull(Object ... values)`
- `boolean isAllNotNull(Object ... values)`
- `boolean orAllisNullOrNotNull(Object ... values)`

### 🔐 Criptografia

- `String createMD5(String chave)`
- `String createMD5(String chave, int fases)`

### 🗺️ Mapas e Listas

- `Map<String, String> mapString(Object ... keyAndValues)`
- `Map<String, Object> mapByPattern(String keys, Object ... values)`
- `<K, V> Map<K, V> map(Object ... keyAndValues)`
- `<T> List<T> list(T ... ts)`
- `<T> List<T> joinLists(List<T> listA, List<T> listB)`

### 🔄 Transformações e Operadores

- `<T> int findIndex(List<T> list, Predicate<T> test)`
- `Runnable compoundRunnable(Runnable... runnables)`
- `<T> Supplier<T> compoundSupplier(Supplier<T>, Consumer<T>)`
- `<T, E> Function<T, E> compoundFunction(Function<T, E>, Consumer<E>)`

### 📏 Comparações

- `int compare(Comparable v1, Comparable v2)`

### 🔎 Reflexão e DicDados

- `void preencheCamposRequeridos(MultiEntity entity)`
- `<T> T campoEstaCarregado(Supplier<T> supplier)`
- `boolean campoEstaCarregado(MultiEntity entity, String nomeCampo)`
- `List<String> camposCarregados(MultiEntity entity)`

### 📄 String e URL

- `String urlEncode(String str)`

### 📦 Versão e Tipo de Item

- `String getVersao()`
- `String getTipoItem(Integer abm01tipo)`

### 🧮 Cálculos

- `int calculoDigitoVerificadorModulo11(String numero)`

### 📑 Bytes

- `byte[] removeAllNonUTF8Bytes(byte[] bytes)`

---

## Exemplo de uso

```java
boolean resultado = Utils.in("A", "A", "B", "C");
System.out.println(resultado); // true
```

