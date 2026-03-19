# Consolidar BOM

## Visão geral

A janela **BOM** consolida arquivos de BOM (Bill of Materials) individuais das placas em uma planilha de vendas unificada com mapas de orçamento. Também permite selecionar quais distribuidores terão colunas na planilha.

## Pré-requisito

As BOMs das placas devem estar geradas e salvas no formato `.xlsx` dentro da pasta `1 - BOM/Bom das Placas/` do diretório do orçamento.

## Passo a passo

### 1. Buscar diretório do orçamento

1. Clique em **Buscar**
2. Selecione a pasta do orçamento

A pasta deve conter a seguinte estrutura obrigatória:

```
NOME_PASTA/
├── 1 - BOM/
│   └── Bom das Placas/     ← arquivos .xlsx das BOMs
└── 4 - MATERIAL/            ← destino da planilha de vendas
```

O programa lista automaticamente todos os arquivos `.xlsx` encontrados na pasta `Bom das Placas`.

### 2. Configurar BOM (aba BOM)

A tabela exibe os arquivos BOM encontrados com as colunas:

| Coluna      | Descrição                                     |
| ----------- | --------------------------------------------- |
| **Arquivo** | Nome do arquivo BOM (somente leitura)         |
| **Lote**    | Quantidade do lote (editável individualmente) |
| **PCI**     | Checkbox para incluir o PN da placa no mapa   |

**Controles globais:**

- **spinBox QTD** (máx. 9999): Altera o lote de todas as BOMs simultaneamente
- **checkBox "Todos"**: Marca/desmarca o checkbox PCI de todas as BOMs
- **Novo Mapa**: Gera um novo mapa na planilha de vendas
- **LCD**: Exibe o número de mapas gerados
- **Salvar**: Consolida e salva a planilha de vendas final

### 3. Configurar distribuidores (aba Distribuidores)

A tabela lista todos os distribuidores disponíveis (carregados de `Data/fornecedores.ini`) com checkboxes para seleção.

- **Salvar**: Salva a seleção atual de distribuidores na configuração
- **Editar**: Abre a janela de [edição de distribuidores](manual_configuracoes.md#editar-distribuidores)

Os distribuidores selecionados ganharão colunas nos mapas da planilha de vendas.

### 4. Gerar mapas e salvar

1. Configure os lotes e checkboxes PCI desejados
2. Clique em **Novo Mapa** para gerar o primeiro mapa
3. Repita para mapas adicionais (com lotes diferentes, se necessário)
4. Clique em **Salvar** para consolidar a planilha de vendas (gerada em `4 - MATERIAL`)
5. Feche a seção BOM antes de prosseguir para as próximas etapas

## Limites

- **Máximo de 20 arquivos BOM** por orçamento
- **Máximo de 6 mapas** por planilha de vendas

## Exclusão de PN

No **Mapa 1** da planilha gerada, insira **'x' ou 'X' na coluna NR** de um PN para excluí-lo das pesquisas posteriores (Nexar, Externo).

## Mensagens de erro

| Mensagem                               | Causa                                                   |
| -------------------------------------- | ------------------------------------------------------- |
| "Limite máximo de arquivos BOM's (20)" | Mais de 20 arquivos `.xlsx` na pasta de BOMs            |
| "Erro ao procurar por arquivos"        | Estrutura de diretório inválida ou pasta não encontrada |
| "Diretório inválido"                   | Nenhum diretório selecionado ao tentar criar mapa       |
| "Nenhum arquivo (.xlsx) encontrado"    | Pasta vazia ao tentar criar mapa                        |
| "Limite máximo de mapas (6)"           | Tentativa de criar mais de 6 mapas                      |
| "Nenhum mapa gerado."                  | Tentativa de salvar sem ter gerado mapas                |
