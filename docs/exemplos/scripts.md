# Exemplos Script de Operação

## Ocultar coluna da spread

Ocultando algumas colunas da spread, o metodo ocultarColunas recebe a spread e os indices das colunas a serem ocultadas

!!! warning "Atenção"
    Este script somente OCULTA a coluna, sendo assim é necessário considerar a mesma na contagem do indice

``` java
    @Override
    public void execute(MultitecRootPanel tarefa) {
        MSpread sprEaa0103s = getComponente("sprEaa0103s");
        ocultarColunas(sprEaa0103s, 0, 1, 2, 3, 4, 5);
    }

```

## Ocultar campo livre da spread

Adiciona um evento ao perder o foco do campo de `tipo de documento`, pode ser alterado para outro campo
ou evento, para remover um campo livre da spread.

!!! warning "Atenção"
    Sempre passar o nome do campo no banco (Ex.: eaa01json) seguido de . (ponto) e o nome do campo livre

``` java
 @Override
    public void execute(MultitecRootPanel tarefa) {
        MNavigationController nvgAah01codigo = getComponente("nvgAah01codigo");
        nvgAah01codigo.addFocusListener(new FocusAdapter() {
            @Override
            public void focusLost(FocusEvent e) {
                MSpread sprEaa0103s = getComponente("sprEaa0103s");
                ocultarColunas(sprEaa0103s, "eaa0103json.vlr_total_docum", "", "");
            }
        });
    }
```

## Alterar tamanho da tela

Altera o tamanho da tela, largura e altura.

``` java
    @Override
    public void execute(MultitecRootPanel tarefa) {
        Window tela = tarefa.getWindow();
        tela.setBounds((int) tela.getBounds().x, (int) tela.getBounds().y, (int) tela.getBounds().width, (int) tela.getBounds().height + 50);
    }
```

## Sobreescrever metodo windowLoad

O metodo windowLoad é executado no momento que a tela está sendo carregada, algumas alterações 
em tela precisam ser feitas após esse metodo.

!!! warning "Atenção"
    Lembre-se de sempre executar o windowLoad original antes do seu codigo

``` java
public class Script extends sam.swing.ScriptBase{
    public Runnable  windowLoadOriginal;

    @Override
    public void execute(MultitecRootPanel tarefa) {
        this.windowLoadOriginal = tarefa.windowLoad ;
        tarefa.windowLoad = {novoWindowLoad()};
    }

    protected void novoWindowLoad(){
        this.windowLoadOriginal.run();
        // Execute seu codigo aqui, validação, alteração etc...
    }
}
```

## Sobreescrever metodo cancelar

Sobrescrever o metodo cancelar de uma tela. Podendo ser usado para validações ou processar dados.

!!! warning "Atenção"
    Lembre-se de sempre executar o cancelar original depois do seu codigo

``` java
public class Script extends sam.swing.ScriptBase{
    public Runnable  cancelarOriginal;

    @Override
    public void execute(MultitecRootPanel tarefa) {
        this.cancelarOriginal = tarefa.cancelar;
        tarefa.cancelar = {novoCancelar()};
    }

    protected void novoCancelar(){
        throw new ValidacaoException("Validação ao cancelar")
        this.cancelarOriginal.run()
    }
}
```

## Abrir uma outra tarefa 

Pode abrir uma nova tarefa ao disparar algum evento, clique em um botão ou alguma condição.

``` java
public class Script  extends sam.swing.ScriptBase{
    private MultitecRootPanel tarefa;

    @Override
    public void execute(MultitecRootPanel tarefa) {
        this.tarefa = tarefa;
    }

    private void abrirTarefaSCV2002() {
        try {
            SCV2002 scv2002 = new SCV2002();
            WindowUtils.createJDialog(scv2002.getWindow(), scv2002);
            scv2002.open.run();
        } catch (Exception err) {
            ErrorDialog.defaultCatch(this.tarefa.getWindow(), err);
        }
    }
}
```

## Alterar função F5 da spread

É possível executar uma função após o F5 em uma spread, servindo para validar ou preencher algum campo de forma automatica.

``` java
class Script  extends sam.swing.ScriptBase{
    @Override
    public void execute(MultitecRootPanel tarefa) {
        MSpread sprAbe0101s = getComponente("sprAbe0101s");
        sprAbe0101s.f5Consumer = sprAbe0101s.f5Consumer.andThen({f5Consumer()});
    }

    public Consumer<Integer> f5Consumer() {
        MSpread sprAbe0101s = getComponente("sprAbe0101s");
        MTextFieldString txtAbe01ni = getComponente("txtAbe01ni");
        MTextFieldString txtAbe01ie = getComponente("txtAbe01ie");

        sprAbe0101s.setValueAt(txtAbe01ni.getValue(), 0, "abe0101ni");
        sprAbe0101s.setValueAt(txtAbe01ie.getValue(), 0, "abe0101ie");
    }
}
```

## Desabilitar campo de navegação

Desabilitando campo de navegação

``` java
private void desabilitarTipo(Eaa01 eaa01){
    MNavigation nvgAah01codigo = getComponente("nvgAah01codigo");
    nvgAah01codigo.setEnabled(false);
    nvgAah01codigo.setEditable(false);
}
```

## Adicionar função no menu cancelar

Adiciona uma nova função na opção cancelar alem da função default.

``` java
class Script extends sam.swing.ScriptBase{
    @Override
    public void execute(MultitecRootPanel tarefa) {
        tarefa.getWindow().getJMenuBar().getMnuArquivo().getMniCancelar().addActionListener(mnu -> this.mniCancelarActionListener(mnu));
    }

    protected void mniCancelarActionListener(ActionEvent evt) {
        if(!exibirQuestao("Deseja realmente sair sem SALVAR?")) interromper("Por favor salvar antes de SAIR.");
    }
}
```

## Sobreescrever KeyListener de componentes

É possível sobreescrever o KeyListener de um determinado componente.

!!! warning "Atenção"
    Lembre-se de sempre executar o KeyListener original antes ou depois do seu codigo.

``` java
class Script extends sam.swing.ScriptBase{
    private KeyListener[] keyListenersOriginais

    @Override
    public void execute(MultitecRootPanel tarefa) {
        MTextFieldString txtColetar = getComponente("txtColetar");
        this.keyListenersOriginais = txtColetar.getKeyListeners();
        if(this.keyListenersOriginais != null && this.keyListenersOriginais.size() > 0){
            for(KeyListener listener in this.keyListenersOriginais){
                txtColetar.removeKeyListener(listener)
            }
        }
        txtColetar.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                if(e.getKeyCode() == KeyEvent.VK_ENTER) {
                    keyListenerCustom(e);
                }
            }
        });

    }

    public void keyListenerCustom(KeyEvent event){
        //Realize sua logica aqui antes do KeyListener original
        if(this.keyListenersOriginais != null && this.keyListenersOriginais.size() > 0){
            for(KeyListener listener in this.keyListenersOriginais){
                listener.keyPressed(event)
            }
        }
        //Realize sua logica aqui depois do KeyListener original
    }
}
```

## Desabilita campo livre

``` java 
class DesabilitarCampoLivre extends sam.swing.ScriptBase{
    def exibirRegistroPadrao;

    public void execute(MultitecRootPanel tarefa) {
        this.exibirRegistroPadrao = tarefa.exibirRegistro
        tarefa.exibirRegistro = {exibir(tarefa)}
    }

    private void exibir(MultitecRootPanel tarefa){
        this.exibirRegistroPadrao.accept(tarefa.registro)

        def pnlCamposLivresJSON = getComponente("pnlCamposLivresJSON");
        def jsonPanels = pnlCamposLivresJSON.getJsonComponentPanels();

        for (jsonPanel in jsonPanels) {
            def nomeCampo = jsonPanel.getComponent().getName(); 
            if(nomeCampo == "texto") {
                jsonPanel.getComponent().getComponent().setEnabled(false);
            }
        }
    }
}
```