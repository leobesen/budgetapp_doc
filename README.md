# Manual do Usuário — BudgetApp v17

## Sobre o BudgetApp

O BudgetApp é uma aplicação desktop para gerenciamento de orçamentos de componentes eletrônicos. Ele permite consolidar BOMs (Bill of Materials), consultar preços via API Nexar/Octopart, importar cotações de distribuidores externos, calcular perdas de componentes e gerar e-mails para fornecedores de PCIs e componentes.

## Como usar o software

Esta seção descreve o fluxo de trabalho completo, desde a consolidação da BOM até a importação final dos resultados. Siga as etapas na ordem indicada para obter os melhores resultados.

### Pré-requisito

As BOMs das placas devem estar geradas e salvas na pasta do orçamento, dentro do subdiretório `1 - BOM/Bom das Placas/`, no formato `.xlsx`.

### Etapa 1 — Consolidação da planilha de orçamento

> Seção: [**BOM**](manual_bom.md)

1. Abrir o BudgetApp
2. Acessar a seção **BOM**
3. Buscar pelo diretório do orçamento
4. Na **aba Distribuidores**: selecionar os distribuidores/fornecedores que estarão inclusos neste orçamento (nas colunas dos Mapas)
5. Na **aba BOM**:
   - Definir a quantidade do lote para o Mapa
   - Definir se a PCI já está inclusa na BOM (checkbox PCI)
   - Clicar em **Novo Mapa**
   - Repetir o processo para a quantidade de mapas (lotes) necessários
   - Clicar em **Salvar** para consolidar (criar) a planilha de vendas na pasta `4 - MATERIAL`
6. Fechar a seção BOM

### Etapa 2 — Seleção dos fornecedores para Fator Ásia

> Seção: [**Fornecedores - Fator Ásia**](manual_fornecedores.md)

Esta etapa pode ser realizada a qualquer momento após a criação da planilha de vendas.

1. Acessar a seção **FORNECEDORES - FATOR ÁSIA**
2. Buscar a planilha de vendas
3. Selecionar os fornecedores que devem ter o fator Ásia aplicado
4. Clicar em **Atualizar**

**Observações:**

- Os fornecedores presentes nesta lista são os que estarão disponíveis para seleção via drop-down na coluna **Fornecedor** da seção **OUTROS** de cada Mapa na planilha
- Durante o orçamento, este processo pode ser repetido sempre que novos fornecedores forem considerados — basta acessar a seção, editar a lista e atualizar a planilha
- Ao adicionar ou retirar o Fator Ásia de um fornecedor, os valores unitários (última coluna de cada fornecedor nos Mapas) são ajustados automaticamente. Porém, para atualizar a seção **MELHORES PREÇOS** do mapa, é necessário executar manualmente via `CTRL+SHIFT+A` no mapa ou pelo botão na aba Menu da planilha

### Etapa 3 — Pré-busca de especificações dos PNs (Nexar)

> Seção: [**Nexar**](manual_nexar.md)

1. Acessar a seção **NEXAR**
2. Buscar pela planilha de vendas
3. Selecionar os distribuidores para busca na API (de preferência os mesmos já considerados na planilha)
4. Clicar em **Solicitar** — ao concluir, um arquivo `data.json` será criado na pasta `4 - MATERIAL` (este arquivo serve de cache para futura importação)
5. Clicar em **Necessidade** para importar as especificações dos PNs para a aba Necessidade da planilha
6. Fechar a tela Nexar

### Etapa 4 — Importação de encapsulamentos do banco de dados

> Seção: [**Perdas**](manual_perdas.md)

1. Acessar a seção **PERDAS**
2. Buscar pela planilha de vendas
3. Buscar pelo diretório de encapsulamentos (que contém `encaps.db`)
4. Clicar em **Processar**
5. Fechar a tela Perdas

### Etapa 5 — Definição das perdas na planilha (manual)

> Realizada diretamente na **planilha de vendas** (Excel)

1. Abrir a planilha de vendas
2. Acessar a aba **Necessidade**
3. Clicar no botão **Atualizar Fórmulas**
4. Preencher os encapsulamentos faltantes na coluna **Encapsulamento / Painel extra**:
   - Preencher os encapsulamentos que estiverem faltando
   - Conferir os existentes
   - Para itens que forem PCI: definir a quantidade de painéis extras
5. Na primeira coluna (**PCI's por painel**): definir a quantidade de PCI nos painéis para os itens PCI
6. Para cada Mapa:
   - Selecionar o Mapa desejado no drop-down do cabeçalho
   - Clicar em **Atualizar Quantidade**
   - Clicar em **Transferir Mapa**
7. Após transferir todos os Mapas, a porcentagem de perdas estará aplicada a cada mapa do orçamento
8. Salvar e fechar a planilha

### Etapa 6 — Importação das cotações Nexar

> Seção: [**Nexar**](manual_nexar.md)

1. Acessar a seção **NEXAR**
2. Buscar pela planilha de vendas
3. Clicar em **Importar** — a solicitação já foi realizada na etapa 3 e está salva no `data.json`

**Nota:** Se o arquivo `data.json` estiver muito antigo (preços desatualizados), pode-se realizar uma nova busca clicando em **Solicitar** antes de importar.

Após a importação, as cotações encontradas para cada fornecedor são atualizadas nos Mapas.

### Etapa 7 — Fator Ásia (ajuste na planilha)

> Realizada na **aba Menu** da planilha de vendas

1. Na aba **Menu** da planilha, ajustar a porcentagem do **FATOR ÁSIA**
2. Esse valor será aplicado automaticamente no preço unitário (última coluna) de cada fornecedor habilitado para Fator Ásia — o preço final considera a compensação do MOQ
3. Para atualizar a seção **MELHORES PREÇOS** de todos os mapas, utilizar o botão disponível na aba Menu

### Etapa 8 — Importação de resultados externos (opcional)

> Seção: [**Externo**](manual_externo.md)

1. Acessar a seção **EXTERNO**
2. Buscar pela planilha de vendas
3. Clicar em **Gerar BOM** para gerar arquivos de upload
4. Enviar os arquivos para LCSC, DigiKey ou Octopart
5. Salvar e renomear os resultados conforme o padrão esperado
6. Clicar em **Importar** para gravar os dados na planilha

Consulte o [manual Externo](manual_externo.md) para detalhes de cada distribuidor.

### Etapa 9 — Envio de e-mails (quando necessário)

> Seções: [**Email PCI**](manual_email_pci.md) e [**Email PN**](manual_email_pn.md)

- Use a seção **PCI** para enviar cotações de placas de circuito impresso
- Use a seção **PN** para enviar cotações de componentes eletrônicos

---

## Índice

| Seção                                                   | Descrição                                   |
| ------------------------------------------------------- | ------------------------------------------- |
| [Janela Principal](manual_janela_principal.md)          | Menu principal e navegação                  |
| [BOM](manual_bom.md)                                    | Consolidar BOM e gerar mapas                |
| [Perdas](manual_perdas.md)                              | Definir perdas de componentes               |
| [Nexar](manual_nexar.md)                                | Consulta à API Nexar                        |
| [Externo](manual_externo.md)                            | Importação de LCSC, DigiKey e Octopart      |
| [Email PCI](manual_email_pci.md)                        | Envio de e-mail para fornecedores de PCI    |
| [Email PN](manual_email_pn.md)                          | Envio de e-mail para cotação de componentes |
| [Fornecedores - Fator Ásia](manual_fornecedores.md)     | Gerenciamento de fornecedores asiáticos     |
| [Configurações Compartilhadas](manual_configuracoes.md) | Editar distribuidores, e-mails e templates  |

## Observação importante

A **planilha de vendas deve estar fechada** durante todas as operações do BudgetApp. Se o programa acusar erro de leitura, feche o BudgetApp, abra a planilha no Excel, salve-a, feche-a e tente novamente.
