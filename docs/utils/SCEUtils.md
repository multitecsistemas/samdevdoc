# SCEUtils

Classe utilitária para acesso a saldos de estoque (resumido, sintético e analítico), lançamentos e cálculos de preço médio de itens no módulo SCE (Sistema de Controle de Estoque).

## Pacote

`sam.server.samdev.utils`

---

## Construtores

#### `SCEUtils(Session session, SAMWhere samWhere, SCEService sceService)`
Inicializa com sessão, regras padrão de filtro e serviço SCE.

#### `SCEUtils(Session session, SAMWhere samWhere)`
Inicializa apenas com sessão e regras padrão (sem serviço).

#### `SCEUtils(SCEService sceService)`
Inicializa apenas com o serviço SCE.

---

## Saldo de Estoque - Resumido

#### `BigDecimal saldoEstoqueItemResumido(Long abm01id, Integer aam04disp, Integer aam04posse)`
Retorna o saldo resumido do item.

#### `BigDecimal saldoEstoqueItemResumido(..., LocalDate dataDoSaldo)`
Versão retroativa do saldo resumido.

#### `BigDecimal saldoEstoqueItemResumido(..., dataDoSaldo, aam04ids, abm15ids0, abm15ids1, abm15ids2)`
Versão completa com filtros adicionais.

---

## Saldo de Estoque - Sintético

#### `List<TableMap> saldoEstoqueItemSintetico(...)`
Versão atual.

#### `List<TableMap> saldoEstoqueItemSintetico(..., LocalDate dataDoSaldo)`
Versão retroativa.

#### `List<TableMap> saldoEstoqueItemSintetico(..., dataDoSaldo, aam04ids, abm15ids0, abm15ids1, abm15ids2)`
Versão completa com filtros adicionais.

---

## Saldo de Estoque - Analítico

#### `List<TableMap> saldoEstoqueItemAnalitico(...)`
Versão atual.

#### `List<TableMap> saldoEstoqueItemAnalitico(..., LocalDate dataDoSaldo)`
Versão retroativa (sem detalhamento de movimento).

#### `List<TableMap> saldoEstoqueItemAnalitico(..., dataDoSaldo, tmBcd01s, aam04ids, abm15ids0, abm15ids1, abm15ids2)`
Versão completa com detalhamento de movimentos e filtros adicionais.

---

## Lançamentos

#### `List<TableMap> buscarLancamentosEstoqueItemData(...)`
Retorna lançamentos do item no estoque, podendo ser retroativos ou por período.

---

## Preço Médio

#### `BigDecimal precoMedioUnitarioAtual(Long abm01id, Long aac10id)`
Retorna o preço médio atual do item.

---

## Saldo de Estoque com Cálculo Reverso

#### `BigDecimal saldoEstoque(Long abm01id, LocalDate bcc01data, Long bcc01id)`
Retorna o saldo considerando lançamentos posteriores ao lançamento informado (modo reverso).

---

## Preço Médio Retroativo

#### `@Deprecated BigDecimal buscarPMRetroativo(Long abm01id, LocalDate bcc01data, Long bcc01id, BigDecimal pmAtual)`
Versão obsoleta para buscar o PM retroativo.

#### `BigDecimal buscarPMRetroativo(Long abm01id, LocalDate bcc01data, Long bcc01id)`
Versão atual para buscar o preço médio do lançamento anterior.
