# RelatorioBase

## Visão Geral

`RelatorioBase` é uma classe abstrata que fornece a base para a criação de relatórios. Ela oferece funcionalidades completas para geração de relatórios em diferentes formatos (PDF, XLSX).

!!! info "Localização"
    **Pacote:** `sam.server.samdev.relatorio`

---

## Propriedades Protegidas

| Propriedade | Tipo | Descrição |
|-------------|------|-----------|
| `resourceLoader` | `ResourceLoader` | Carregador de recursos |
| `params` | `Map<String, Object>` | Mapa de parâmetros do relatório |

## Propriedades Privadas

| Propriedade | Tipo | Descrição |
|-------------|------|-----------|
| `parametroService` | `ParametroService` | Serviço de parâmetros |
| `alinhamento` | `Map<String, String>` | Mapa de alinhamentos |
| `springContext` | `ApplicationContext` | Contexto Spring |
| `senhaPDF` | `String` | Senha para proteger PDFs |

---

## Métodos Abstratos

### `criarValoresIniciais()`

```java
public abstract Map<String, Object> criarValoresIniciais();
```

Define os valores iniciais necessários para o relatório.

**Retorno:** Mapa contendo os valores iniciais

---

### `executar()`

```java
public abstract DadosParaDownload executar();
```

Executa a lógica principal do relatório e retorna os dados para download.

**Retorno:** Objeto `DadosParaDownload` com os dados do relatório processado

---

## Estrutura Base

Estrutura base para montar um Relatório.

``` java
import sam.server.samdev.relatorio.DadosParaDownload;
import sam.server.samdev.relatorio.RelatorioBase;

class Relatorio extends RelatorioBase{
    @Override
    String getNomeTarefa() {
        return null
    }

    @Override
    Map<String, Object> criarValoresIniciais() {
        return null
    }

    @Override
    DadosParaDownload executar() {
        return null
    }
}
```

---

## Métodos de Acesso

### `getSession()`
Retorna a sessão do banco de dados.

```java
public Session getSession()
```

---

### `getSamWhere()`
Retorna os critérios padrão SAM.

```java
public SAMWhere getSamWhere()
```

---

### `getVariaveis()`
Retorna as variáveis de sessão.

```java
public Variaveis getVariaveis()
```

---

### `getResourceLoader()`
Retorna o carregador de recursos.

```java
public ResourceLoader getResourceLoader()
```

---

### `ignorarTempoLimiteDoRelatorio()`
Define se o tempo limite do relatório deve ser ignorado, retorna `false` por padrão.

```java
public boolean ignorarTempoLimiteDoRelatorio()
```

---

## Métodos de Sessão

### `obterEmpresaAtiva()`
Obtém a empresa ativa na sessão.

```java
public Aac10 obterEmpresaAtiva()
```

---

### `obterUsuarioLogado()`
Obtém o usuário logado na sessão.

```java
public Aab10 obterUsuarioLogado()
```

---

### `obterWherePadrao()`
Obtém o critério padrão WHERE para uma classe, retorna uma `String` com o where.

```java
public String obterWherePadrao(String classe)
public String obterWherePadrao(String classe, String whereAndOr)
public String obterWherePadrao(String classe, String whereAndOr, String alias)
```

|  Parâmetros | Descrição                        |
|-------------|----------------------------------|
| `classe`    | Nome da Tabela                   |
| `whereAndOr`| Operador AND ou OR (padrão: AND) |
| `alias`     | Alias opcional para a classe     |

---

## Métodos de Acesso ao Banco de Dados

### `getAcessoAoBanco()`
Retorna um utilitário para acesso ao banco de dados, devolve um objeto da classe [BancoDadosUtils](../uteis/BancoDadosUtils.md).

```java
public BancoDadosUtils getAcessoAoBanco()
```

---

### `criarParametroSql()`
Cria um parâmetro SQL.

```java
public Parametro criarParametroSql(String chave, Object valor)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `chave`     | Chave do parâmetro |
| `valor`     | Valor do parâmetro |

---

## Métodos de Parâmetros

### `adicionarParametro()`
Adiciona um parâmetro ao mapa de parâmetros para ser enviado ao relatório.

```java
public void adicionarParametro(String key, Object value)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `key`       | Chave do parâmetro |
| `value`     | Valor do parâmetro |

---

### `closeParams()`
Fecha todos os parâmetros que implementam `Closeable` e limpa o mapa.

```java
public void closeParams()
```

---

## Métodos de Carregamento de Relatórios

### `carregarArquivoRelatorio()`
Carrega um arquivo `jasper` de relatório JasperReports, retornando um objeto `JasperReport` carregado.

```java
protected JasperReport carregarArquivoRelatorio()
protected JasperReport carregarArquivoRelatorio(String nome)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `nome`      | Nome opcional do arquivo (sem extensão) |

---

## Métodos de Processamento de Relatórios

### `processarRelatorio()`
Processa um relatório JasperReports com os dados fornecidos, retorna um Objeto `JasperPrint` processado.

```java
protected JasperPrint processarRelatorio(JasperReport report, List<TableMap> dados)
protected JasperPrint processarRelatorio(JasperReport report, TableMapDataSource dados)
```
|  Parâmetros | Descrição          |
|-------------|--------------------|
| `report`      | Relatório compilado |
| `dados` | Dados para preencher o relatório|

---

## Métodos de Geração de PDFs

### `gerarPDF()`
Gera um PDF do relatório, retorna um Objeto `DadosParaDownload` contendo o PDF gerado.

```java
protected DadosParaDownload gerarPDF(List<TableMap> dados)
protected DadosParaDownload gerarPDF(String nome, List<TableMap> dados)
protected DadosParaDownload gerarPDF(String nome, TableMapDataSource dados)
protected DadosParaDownload gerarPDF(String nome, TableMapDataSource dados, 
                                     String grupoRelatorio, boolean saltarPagina)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `nome`      | Nome do arquivo `jasper` do relatório (opcional) |
| `dados` | Dados para preencher o relatório|
| `grupoRelatorio` | Nome do grupo de relatório (opcional)|
| `saltarPagina` | Se deve iniciar nova página ao trocar de grupo|

---

### `convertPrintToPDF()`
Converte um `JasperPrint` em bytes PDF.

```java
protected byte[] convertPrintToPDF(JasperPrint print)
```

**Nota:** Se `senhaPDF` estiver definida, o PDF será encriptado com as permissões de cópia e impressão.

---

### `converterPDFParaImpressoraTermica()`
Converte um PDF para formato de imagem otimizado para impressoras térmicas, retorna um Objeto `DadosParaDownload` contendo a imagem JPG.

```java
protected DadosParaDownload converterPDFParaImpressoraTermica(DadosParaDownload dadosPdf, 
                                                              int dpiDaImpressora, 
                                                              int larguraDaImpressaoEmMilimetros)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `dadosPdf`      | PDF a ser convertido|
| `dpiDaImpressora` |Resolução em DPI|
| `larguraDaImpressaoEmMilimetros` |Largura da impressão em mm|


---

## Métodos de Geração de XLSX

### `gerarXLSX()`
Gera uma planilha XLSX do relatório, retorna um Objeto `DadosParaDownload` contendo o XLSX gerado.

```java
protected DadosParaDownload gerarXLSX(List<TableMap> dados)
protected DadosParaDownload gerarXLSX(String nome, List<TableMap> dados)
protected DadosParaDownload gerarXLSX(String nome, TableMapDataSource dados)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `nome`      | Nome do arquivo de relatório (opcional)|
| `dados` |Dados para o relatório|

---

## Métodos de Alinhamento de Valores

### `selecionarAlinhamento()`
Seleciona o alinhamento de valores baseado em um código.

```java
public void selecionarAlinhamento(String codigo)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `codigo`      |Código do alinhamento|

---

### `getCampo()`
Obtém o valor de um campo do alinhado selecionado, retorna o Valor alinhado ou `null` se não encontrado.

```java
public String getCampo(String registro, String campo)
public String getCampo(String codAlinhamento, String registro, String campo)
```

|  Parâmetros | Descrição          |
|-------------|--------------------|
| `codAlinhamento`      |Código do alinhamento (opcional)|
| `registro`      |Nome do registro|
| `campo`      |Nome do campo|

---

## Métodos Auxiliares

### `getResourcePath()`
Obtém o caminho de um recurso baseado no pacote da classe.

```java
protected String getResourcePath(String nome)
protected String getJasperResourcePath(String nome)
```

---

### `getArquivo()`
Obtém um arquivo de recurso como InputStream.

```java
protected InputStream getArquivo(String nome)
```

---

### `criarFiltros()`
Cria um mapa de filtros a partir de argumentos variáveis.

```java
public Map<String, Object> criarFiltros(Object ... filtros)
```

---

### `instanciarService()`
Obtém uma instancia de um service do SAM4.

```java
public <T> T instanciarService(Class<? extends T> serviceClass)
```

!!! warning "Atenção"
    Os Services do SAM não podem ser instanciados com `new`.

---

### `interromper()`
Interrompe a execução lançando uma `ValidacaoException`.

```java
public void interromper(String mensagem)
```

---

### `getEstoqueUtils()`
Retorna um utilitário para operações de estoque, devolve um objeto da classe [SCEUtils](../uteis/SCEUtils.md).

```java
public SCEUtils getEstoqueUtils()
```

---

## Métodos de Senha PDF
Obtém ou define a senha para proteger o PDF gerado.

### `getSenhaPDF()` e `setSenhaPDF()`

```java
public String getSenhaPDF()
public void setSenhaPDF(String senhaPDF)
```


!!! info "Proteção de PDFs"
    A senha do PDF deve ser configurada através de `setSenhaPDF()` antes de chamar `gerarPDF()` para que a proteção seja aplicada.
    
---

## Exemplo de Uso

```java
public class RelatorioVendas extends RelatorioBase {
    
    @Override
    public Map<String, Object> criarValoresIniciais() {
        Map<String, Object> valores = new HashMap<>();
        valores.put("dataInicio", LocalDate.now());
        valores.put("dataFim", LocalDate.now());
        return valores;
    }
    
    @Override
    public DadosParaDownload executar() {
        // Adicionar parâmetros
        adicionarParametro("empresa", obterEmpresaAtiva().getAac10nome());
        
        // Buscar dados
        BancoDadosUtils banco = getAcessoAoBanco();
        List<TableMap> dados = banco.buscarListaDeTableMap("SELECT * FROM eaa01");
        
        // Gerar PDF
        return gerarPDF("RelatorioVendas", dados);
    }
}
```