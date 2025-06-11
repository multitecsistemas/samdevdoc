# FormulaBase

## Visão Geral

A classe `FormulaBase` é uma classe abstrata que serve como base para implementação de fórmulas no sistema SAM. Ela fornece uma estrutura comum para execução de fórmulas com acesso ao banco de dados, variáveis de sessão, mensageria e diversos utilitários.

!!! info "Localização"
    **Pacote:** `sam.server.samdev.formula`

## Métodos Abstratos

### executar()
```java
public abstract void executar();
```
Método principal que deve ser implementado pelas classes filhas para definir a lógica específica da fórmula.

### obterTipoFormula()
```java
public abstract FormulaTipo obterTipoFormula();
```
Retorna o tipo da fórmula sendo executada.

## Estrutura Base

Estrutura base para montar uma formula.

``` java
import sam.dicdados.FormulaTipo;
import sam.server.samdev.formula.FormulaBase;

class Formula extends FormulaBase{
    @Override
    void executar() {}

    @Override
    FormulaTipo obterTipoFormula() {
        return null
    }
}

```

## Funcionalidades Principais

### 📊 Acesso ao Banco de Dados

#### getAcessoAoBanco()
Retorna uma instância de [BancoDadosUtils](../uteis/bancoDadosUtils.md) para operações no banco de dados.
```java
public BancoDadosUtils getAcessoAoBanco()
```

#### criarParametroSql()
Cria um parâmetro SQL com chave e valor especificados.
```java
public Parametro criarParametroSql(String chave, Object valor)
```

### 👤 Variáveis da Sessão

#### obterEmpresaAtiva()
Retorna a empresa ativa na sessão atual.
```java
public Aac10 obterEmpresaAtiva()
```

#### obterUsuarioLogado()
Retorna o usuário logado na sessão atual.
```java
public Aab10 obterUsuarioLogado()
```

#### obterWherePadrao()
Gera cláusulas WHERE padrão para consultas:
```java
public String obterWherePadrao(String classe)
public String obterWherePadrao(String classe, String whereAndOr)
public String obterWherePadrao(String classe, String whereAndOr, String alias)
```

|Parametro      | descrição                      |
|---------------|--------------------------------|
|**classe**     |Nome da classe da entidade      |
|**whereAndOr** |Operador lógico (padrão: "AND") |
|**alias**      |Alias da tabela (opcional)      |

### 📨 Mensageria

!!! warning "Atenção"
    Os Metodos de Mensageria funcionam apenas se a tela que chamou a formula suportar.


#### verificarProcessoCancelado()
Verifica se o processo foi cancelado e lança `ThreadCanceladaException` se necessário.
```java
public void verificarProcessoCancelado()
```

#### enviarStatusProcesso()
Envia mensagem de status do processo. Automaticamente envolve a mensagem em tags HTML se necessário.
```java
public void enviarStatusProcesso(String mensagem)
```

### 🔧 Alinhamento de Valores

#### selecionarAlinhamento()
Carrega configurações de alinhamento baseadas no código fornecido.
```java
public void selecionarAlinhamento(String codigo)
```
!!! warning "Cuidado"
    Alinhamentos são carregados sob demanda e mantidos em memória

#### getCampo()
Obtém o nome do campo baseado no alinhamento configurado.
```java
public String getCampo(String registro, String campo)
public String getCampo(String codAlinhamento, String registro, String campo)
```

|Parametro          | descrição                        |
|-------------------|----------------------------------|
|**codAlinhamento** |Código do alinhamento (opcional)  |
|**registro**       |Nome do registro                  |
|**campo**          | Nome do campo                    |

### 🛠️ Utilitários

#### getHoleriteUtils()
Retorna utilitários para manipulação de holerites, devolve um objeto da classe [HoleriteUtils]()
```java
public HoleriteUtils getHoleriteUtils()
```

#### getEstoqueUtils()
Retorna utilitários para manipulação de estoque, devolve um objeto da classe [SCEUtils]()
```java
public SCEUtils getEstoqueUtils()
```

#### instanciarService()
Instancia um serviço do Spring usando o contexto da aplicação, usado para instanciar Services do SAM.
```java
public <T> T instanciarService(Class<? extends T> serviceClass)
```

!!! warning "Atenção"
    Os Services do SAM não podem ser instanciados com `new`.

#### interromper()
Interrompe a execução da fórmula com uma mensagem de erro.
```java
public void interromper(String mensagem)
```

### 🌐 Execução de Servlets

#### executarServletGet()
Executa uma servlet via HTTP GET.
```java
public byte[] executarServletGet(String server, String servlet, Map<String, String> headers, Map<String, Object> params)
```

|Parametro    | descrição                            |
|-------------|--------------------------------------|
|**server**   | URL do servidor                      |
|**servlet**  |Nome da servlet                       |
|**headers**  | Cabeçalhos HTTP (opcional)           |
|**params**   | Parâmetros da requisição (opcional)  |

#### executarServletPost()
Executa uma servlet via HTTP POST.
```java
public byte[] executarServletPost(String server, String servlet, Map<String, String> headers, Object body)
```

|Parametro    | descrição                            |
|-------------|--------------------------------------|
|**server**   | URL do servidor                      |
|**servlet**  |Nome da servlet                       |
|**headers**  | Cabeçalhos HTTP (opcional)           |
|**body**     | Corpo da requisição (opcional)       |

## Exemplo de Uso

```java
public class MinhaFormula extends FormulaBase {
    
    @Override
    public void executar() {
        // Verificar se o processo foi cancelado
        verificarProcessoCancelado();
        
        // Enviar status
        enviarStatusProcesso("Iniciando processamento da fórmula");
        
        // Obter dados da sessão
        Aac10 empresa = obterEmpresaAtiva();
        Aab10 usuario = obterUsuarioLogado();
        
        // Executar lógica específica
        BancoDadosUtils db = getAcessoAoBanco();
        // ... operações no banco
        
        enviarStatusProcesso("Fórmula executada com sucesso");
    }
    
    @Override
    public FormulaTipo obterTipoFormula() {
        return FormulaTipo.CAS_IMPORTAR_DADOS;
    }
}
```

## Notas Importantes

!!! tip "Boas Práticas"
    - Sempre verificar cancelamento em loops longos usando `verificarProcessoCancelado()`
    - Enviar mensagens de status regulares para informar o progresso
    - Usar `interromper()` para parar a execução com mensagens claras