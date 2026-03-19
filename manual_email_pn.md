# Email PN

## Visão geral

A janela **PN** permite montar e enviar e-mails de cotação de componentes eletrônicos (Part Numbers) para fornecedores. Os PNs são carregados diretamente da planilha de vendas, filtrando os itens marcados para cotação.

O envio é feito via **Microsoft Outlook** (automação COM).

## Passo a passo

### 1. Buscar planilha de vendas

1. Clique em **Buscar**
2. Selecione a planilha de vendas (`.xls`, `.xlsx` ou `.xlsm`)

### 2. Configurar OM e etapa

| Campo              | Descrição                                  |
| ------------------ | ------------------------------------------ |
| **spinBox OM**     | Número da Ordem de Material                |
| **comboBox Etapa** | Etapa de cotação: `E1`, `E2`, `E3` ou `E4` |

### 3. Carregar PNs

Clique em **Carregar PNs** para ler os componentes da planilha de vendas.

O programa carrega os PNs marcados com **'e' ou 'E'** (ou a etapa correspondente: `E1`, `E2`, `E3`, `E4`) na coluna **NR do Mapa 1**.

**Tabela de PNs:**

| Coluna            | Descrição                                           |
| ----------------- | --------------------------------------------------- |
| PN                | Part Number do componente (somente leitura)         |
| (checkbox)        | Selecionar/deselecionar PN para o e-mail            |
| FABRICANTE        | Nome do fabricante (somente leitura)                |
| QTD 1, QTD 2, ... | Quantidade por mapa (uma coluna por mapa existente) |

Todos os PNs vêm selecionados por padrão. Desmarque os que não deseja incluir no e-mail.

### 4. Configurar destinatários

| Campo                 | Descrição                                                                     |
| --------------------- | ----------------------------------------------------------------------------- |
| **comboBox Destino**  | Empresa do destinatário (carregado de `Data/Email/email_pn_fornecedores.ini`) |
| **comboBox Template** | Modelo de e-mail (carregado de `Data/Templates/PN/`)                          |

**Tabela de destinatários:**

| Coluna       | Descrição                            |
| ------------ | ------------------------------------ |
| Destinatário | Endereço de e-mail (somente leitura) |
| Para         | Checkbox — destinatário principal    |
| Cc           | Checkbox — cópia                     |

**Botões:**

- **Atualizar**: Recarrega a lista de destinatários
- **Editar** (destinatários): Abre a janela de [edição de endereços de e-mail](manual_configuracoes.md#editar-endereços-de-e-mail)
- **Editar** (template): Abre a janela de [edição de templates](manual_configuracoes.md#editar-templates-de-e-mail)

### 5. Enviar

Clique em **Enviar** para gerar e enviar o e-mail com os PNs selecionados e suas quantidades.

O assunto do e-mail segue o formato: `OM<número>/<ano> - <destinatário>`

## Templates

Os templates de e-mail ficam em `Data/Templates/PN/` e seguem a mesma estrutura dos templates PCI:

- `<nome>_salutation.txt` — Saudação
- `<nome>_body.txt` — Corpo (com tag `<<TABLE>>`)
- `<nome>_closing.txt` — Despedida
- `<nome>_table.txt` — Idioma da tabela (`ENG` ou `PORT`)

## Mensagens de erro

| Mensagem                                            | Causa                                |
| --------------------------------------------------- | ------------------------------------ |
| "Selecione o arquivo de vendas"                     | Nenhuma planilha selecionada         |
| "Dados referentes aos PNs não foram encontrados!"   | Tentativa de enviar sem carregar PNs |
| "Não foram selecionados PNs na planilha de vendas!" | Nenhum PN encontrado na planilha     |
| "Nenhum destinatário selecionado!"                  | Nenhum checkbox "Para" marcado       |
