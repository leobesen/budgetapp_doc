# Definir Perdas

## Visão geral

A janela **Perdas** calcula as perdas de componentes eletrônicos com base no encapsulamento (package) e pitch de cada componente. O resultado é gravado na aba **Necessidade** da planilha de vendas.

## Passo a passo

### 1. Buscar planilha de vendas

1. Clique em **Buscar** (arquivo)
2. Selecione a planilha de vendas (`.xls`, `.xlsx` ou `.xlsm`) gerada na etapa BOM

### 2. Buscar diretório de encapsulamentos

1. Clique em **Buscar** (diretório)
2. Selecione a pasta que contém o banco de dados `encaps.db`

Ao selecionar o diretório, a tabela é preenchida com os dados do banco:

| Coluna             | Descrição                                       |
| ------------------ | ----------------------------------------------- |
| **Encapsulamento** | Tipo do encapsulamento (ex: 0201, 0805, SOT-23) |
| **Pitch (mm)**     | Valor do pitch em milímetros                    |

### 3. Processar

Clique em **Processar** para iniciar o cálculo de perdas.

O programa:

1. Lê a descrição de cada PN na planilha de vendas
2. Busca o encapsulamento correspondente no banco de dados
3. Calcula as perdas com base no pitch
4. Preenche a aba **Necessidade** na planilha de vendas

## Encapsulamentos novos

Se o programa encontrar encapsulamentos que **não existem** no banco de dados:

1. Um arquivo `Encapsulamentos novos.xlsx` é gerado na pasta do orçamento
2. O usuário deve preencher manualmente o valor do **pitch** nesse arquivo
3. Na próxima execução, o programa importará automaticamente esses dados para o banco `encaps.db`

## Integração com Nexar

Se a pesquisa na API Nexar foi realizada **antes** do processamento de perdas (etapas 3 e 4 do [fluxo recomendado](README.md#como-usar-o-software)), as informações extras de encapsulamento obtidas pela API serão aproveitadas no cálculo, melhorando a precisão.

## Etapa seguinte: definição das perdas na planilha (manual)

Após processar as perdas no BudgetApp, é necessário completar o processo **diretamente na planilha de vendas** (Excel):

1. Abrir a planilha de vendas
2. Acessar a aba **Necessidade**
3. Clicar no botão **Atualizar Fórmulas**
4. Preencher os dados faltantes na coluna **Encapsulamento / Painel extra**:
   - Preencher os encapsulamentos que estiverem faltando
   - Conferir os existentes
   - Para itens PCI: definir a quantidade de painéis extras
5. Na coluna **PCI's por painel**: definir a quantidade de PCI nos painéis para os itens que forem PCI
6. Para cada Mapa existente:
   - Selecionar o Mapa no **drop-down** do cabeçalho
   - Clicar em **Atualizar Quantidade**
   - Clicar em **Transferir Mapa**
7. Após transferir todos os Mapas, a porcentagem de perdas estará aplicada
8. Salvar e fechar a planilha

## Mensagens de erro

| Mensagem                                   | Causa                        |
| ------------------------------------------ | ---------------------------- |
| "Selecione o arquivo de vendas"            | Nenhuma planilha selecionada |
| "Selecione o diretório de encapsulamentos" | Nenhum diretório selecionado |
