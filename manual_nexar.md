# Nexar (API)

## Visão geral

A janela **Nexar** realiza consultas à API Nexar (antigo Octopart) para buscar preços, disponibilidade e informações de encapsulamento dos componentes presentes na planilha de vendas.

## Passo a passo

### 1. Buscar planilha de vendas

1. Clique em **Buscar**
2. Selecione a planilha de vendas (`.xls`, `.xlsx` ou `.xlsm`)

### 2. Solicitar

Clique em **Solicitar** para consultar a API Nexar.

O programa:

1. Lê os PNs da planilha de vendas (ignorando os marcados com 'x'/'X' na coluna NR do Mapa 1)
2. Monta as queries GraphQL em lotes de até **100 PNs por requisição** (`OCTO_PN_LIMIT`)
3. Envia as consultas à API Nexar
4. Salva os resultados no arquivo local `data.json` na pasta `4 - MATERIAL`

O arquivo `data.json` funciona como **cache**: a importação dos dados (etapa Importar) pode ser feita posteriormente sem precisar consultar a API novamente. Se os preços estiverem muito desatualizados, basta clicar em **Solicitar** novamente para atualizar o cache.

De preferência, selecione os mesmos distribuidores já considerados na planilha de vendas (configurados na etapa BOM).

### 3. Necessidade

Clique em **Necessidade** para importar dados de encapsulamento da pesquisa Nexar para a aba **Necessidade** da planilha de vendas.

Essa etapa é recomendada **antes** de processar as perdas, pois fornece informações adicionais de encapsulamento que melhoram o cálculo.

### 4. Importar

Clique em **Importar** para transferir os resultados do `data.json` para a planilha de vendas.

**Importante:** Este passo deve ser executado **somente após**:

- Definir as perdas (janela Perdas)
- Completar a aba Necessidade na planilha (Atualizar Fórmulas → Atualizar Quantidade → Transferir Mapa)
- Atualizar as quantidades (QTDE) nos mapas da planilha

Os dados importados incluem preços, MOQ e estoque dos distribuidores consultados. Após a importação, as cotações de cada fornecedor são atualizadas diretamente nos Mapas da planilha.

## Seleção de distribuidores

A tabela na parte inferior lista os distribuidores disponíveis com checkboxes. Esses são os distribuidores que serão consultados na API Nexar.

- **Salvar**: Salva a seleção de distribuidores para pesquisa na API
- **Editar**: Abre a janela de [edição de distribuidores](manual_configuracoes.md#editar-distribuidores)

**Nota:** Os distribuidores selecionados aqui são independentes dos selecionados na janela BOM (que definem as colunas da planilha).

## Mensagens de erro

| Mensagem                        | Causa                        |
| ------------------------------- | ---------------------------- |
| "Selecione o arquivo de vendas" | Nenhuma planilha selecionada |
