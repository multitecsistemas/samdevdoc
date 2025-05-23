# Exportação de dados

## Introdução

A exportação de dados pode ser feita principalmente nos formatos XML, TXT e CSV, permitindo também a exportação em outros formatos.

## Filtros

Assim como em uma listagem, a exportação de dados pode ter ou não filtros, utilizando os [componentes das listagens](/relatorios/#componentes)

## Métodos

| Nome         | Descrição        | 
| ------------ | -----------------|
| String nome  | Nome do arquivo  |

### gerarXml
``` java
DadosParaDownload gerarXml(String nome, ElementXml xml)
```

### gerarTxt
``` java
DadosParaDownload gerarTxt(String nome, String txt)
```

### gerarCsv
``` java
DadosParaDownload gerarCsv(String nome, String csv)
```

### gerarDados
| Nome           | Descrição         | 
| -------------- | ------------------|
| byte[] dados   | bytes do arquivo  |
| MediaType type | tipo do arquivo   |

``` java
DadosParaDownload gerarDados(String nome, byte[] dados, MediaType type)
```