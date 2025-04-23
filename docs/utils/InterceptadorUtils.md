# InterceptadorUtils

Classe utilitária com métodos auxiliares para acesso às variáveis de sessão, entidades padrão, construção de cláusulas WHERE e integração com o banco de dados no contexto do SAM.

## Pacote

`sam.server.samdev.utils`

---

## Instância Singleton

#### `static InterceptadorUtils INSTANCE`
Instância pública única da classe.

---

## Sessão SAM

#### `SAMWhere getSamWhere()`
Retorna uma nova instância de `SAMWhere` com base nas variáveis da sessão atual.

#### `Variaveis getVariaveis()`
Retorna a instância atual de `Variaveis`, contendo contexto da sessão (usuário, empresa, etc).

---

## Entidades

#### `Aac01 obterGC(Long aac01id, Session s)`
Obtém a entidade `Aac01` (provavelmente grupo de cálculo ou similar) pelo seu ID usando uma sessão ORM.

#### `Aab10 obterUsuarioLogado()`
Retorna o usuário logado atual (`Aab10`), obtido a partir das variáveis de sessão.

#### `Aac10 obterEmpresaAtiva()`
Retorna a empresa ativa (`Aac10`) associada à sessão atual.

---

## Where Padrão

#### `String obterWherePadrao(String classe)`
Gera a cláusula WHERE padrão para uma entidade pelo nome da classe, utilizando `AND` por padrão.

#### `String obterWherePadrao(String classe, String whereAndOr)`
Permite definir o operador lógico (`AND` ou `OR`) para construir a cláusula WHERE padrão com base na classe informada.

---

## Banco de Dados

#### `BancoDadosUtils getAcessoAoBanco(Session s)`
Instancia a classe `BancoDadosUtils` para acesso ao banco, já configurada com a sessão atual e `SAMWhere`.

#### `Parametro criarParametroSql(String chave, Object valor)`
Cria uma instância de `Parametro` para uso em queries parametrizadas.

---

## Controle de Fluxo

#### `void interromper(String mensagem)`
Lança uma `ValidacaoException` com a mensagem informada. Usado para parar fluxos com validação explícita.

---

## Exemplo de uso

```java
InterceptadorUtils utils = InterceptadorUtils.INSTANCE;

String wherePadrao = utils.obterWherePadrao("sam.model.entities.fb.Fba01");
BancoDadosUtils banco = utils.getAcessoAoBanco(session);

if (!usuarioValido) {
    utils.interromper("Usuário não autorizado.");
}
```