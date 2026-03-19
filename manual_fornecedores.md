# Fornecedores — Fator Ásia

## Visão geral

A janela **Fornecedores - Fator Ásia** permite gerenciar quais distribuidores possuem o fator de importação asiático aplicado na planilha de vendas. Ao atualizar, a configuração é salva e a planilha é modificada via xlwings.

## Quando usar

Esta etapa pode ser realizada a **qualquer momento** após a criação da planilha de vendas (etapa BOM). Durante o orçamento, o processo pode ser repetido múltiplas vezes conforme novos fornecedores forem sendo considerados.

## Passo a passo

### 1. Buscar planilha de vendas

1. Clique em **Buscar**
2. Selecione a planilha de vendas (`.xls`, `.xlsx` ou `.xlsm`)

### 2. Selecionar distribuidores

A tabela lista todos os distribuidores disponíveis (carregados de `Data/fornecedores.ini`) com checkboxes na coluna **Fator Ásia**.

Marque os distribuidores que devem ter o fator de importação asiático aplicado nos cálculos da planilha.

### 3. Atualizar

Clique em **Atualizar** para:

1. Salvar a seleção na configuração do programa (`config.ini`)
2. Atualizar a planilha de vendas com as informações de fator Ásia (via xlwings)

**Nota:** Se nenhuma planilha foi selecionada, apenas a configuração será salva (sem atualizar o Excel).

### Editar distribuidores

Clique em **Editar** para abrir a janela de [edição de distribuidores](manual_configuracoes.md#editar-distribuidores), onde é possível adicionar ou remover nomes da lista.

## Efeito na planilha de vendas

- Apenas os fornecedores presentes nesta lista estarão disponíveis para seleção via **drop-down** na coluna **Fornecedor** da seção **OUTROS** de cada Mapa na planilha
- Ao atualizar, os **valores unitários** (última coluna de cada fornecedor nos Mapas) são ajustados automaticamente com base no Fator Ásia
- A seção **MELHORES PREÇOS** de cada mapa **não é atualizada automaticamente** — para atualizá-la, execute `CTRL+SHIFT+A` no mapa ou clique no botão correspondente na aba **Menu** da planilha de vendas

## Ajuste do percentual do Fator Ásia

O percentual do Fator Ásia é configurado diretamente na **aba Menu** da planilha de vendas (não no BudgetApp). Esse valor é aplicado no preço unitário de cada fornecedor habilitado, e o preço final considera a compensação do MOQ.

Ao ajustar o valor **FATOR ÁSIA** na aba Menu:

- Os preços unitários de todos os fornecedores habilitados são ajustados **automaticamente** nos mapas
- Para atualizar a seção **MELHORES PREÇOS**, use o botão disponível na aba Menu
