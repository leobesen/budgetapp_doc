# Externo (LCSC / DigiKey / Octopart)

## Visão geral

A janela **Externo** permite gerar arquivos BOM compatíveis com os sites de distribuidores externos (LCSC, DigiKey e Octopart), e depois importar os resultados de volta para a planilha de vendas.

## Interface

A tela possui quatro ações principais:

- **Buscar**: Seleciona a planilha de vendas
- **Gerar BOM**: Gera os arquivos de mapa para upload nos sites
- **Link**: Abre o site do distribuidor selecionado no navegador
- **Importar**: Lê o arquivo exportado pelo distribuidor e grava os dados na planilha

O **comboBox** permite selecionar o distribuidor: `LCSC`, `DigiKey` ou `Octopart`.

## Arquivo de entrada

Ao clicar em **Buscar**, o programa aceita arquivos Excel nos formatos `.xls`, `.xlsx` ou `.xlsm`.

A planilha precisa seguir a estrutura esperada pelo sistema:

- Aba `Menu`
- Abas `Mapa 1`, `Mapa 2`, `Mapa 3`... quando existirem
- Senha da planilha compatível com a configuração interna
- Token da API presente na aba `Menu`

## Fluxo recomendado

### 1. Selecionar a planilha

1. Clique em **Buscar**
2. Selecione a planilha de vendas/orçamento
3. Confirme que o nome apareceu no campo da tela

### 2. Gerar os arquivos BOM

1. Clique em **Gerar BOM**
2. Localize os arquivos `BOM_Mapa_...` na mesma pasta da planilha

### 3. Enviar o BOM ao distribuidor

1. Selecione o distribuidor no comboBox (`LCSC`, `DigiKey` ou `Octopart`)
2. Clique em **Link** para abrir o site correspondente
3. Faça o upload do arquivo `BOM_Mapa_...xlsx` no portal do distribuidor

### 4. Exportar o resultado do site

Depois que o site processar o BOM, exporte o resultado e salve o arquivo na **mesma pasta da planilha original**.

### 5. Renomear o arquivo exportado

O arquivo exportado precisa seguir exatamente o padrão de nome esperado pelo BudgetApp (ver seção abaixo por distribuidor).

### 6. Importar no BudgetApp

1. Selecione o distribuidor no comboBox
2. Clique em **Importar**

---

## Como a exportação funciona

### Dados usados

O arquivo é montado a partir das colunas do mapa:

- `PN` na coluna 3
- `SOMA` na coluna 6

As linhas começam na linha 8 da planilha. Linhas marcadas com os seguintes códigos na coluna `NR` são **ignoradas**: `x`, `X`, `e`, `E`, `E1`, `E2`, `E3`, `E4`.

### Arquivos gerados

Os arquivos são gravados na **mesma pasta da planilha selecionada**.

Padrão de nome:

```
BOM_Mapa_<numero_do_mapa>_Arquivo_<numero_do_arquivo>.xlsx
```

Exemplos:

```
BOM_Mapa_1_Arquivo_1.xlsx
BOM_Mapa_1_Arquivo_2.xlsx
```

### Limite por arquivo

O sistema divide automaticamente os itens em blocos de até **199 PNs por arquivo**. Se um mapa tiver mais de 199 itens válidos, serão criados múltiplos arquivos (`Arquivo_1`, `Arquivo_2`, etc.).

### Estrutura do arquivo gerado

Cada arquivo `.xlsx` contém uma planilha chamada `Mapa X` com duas colunas:

- `PN`
- `QTD`

---

## Fluxo por distribuidor

### LCSC

**Link:** `https://www.lcsc.com/bom`

**Upload:**

1. Acesse o site e envie o arquivo `BOM_Mapa_...xlsx`
2. Configure: "Data start row" = 2, "Manufacturer Part Number" = PN1, "Quantity" = QTD
3. Exporte o resultado em `.xls`

**Renomear arquivo exportado:**

```
LCSC_Mapa_<numero_do_mapa>_Arquivo_<numero_do_arquivo>.xls
```

Exemplo: `LCSC_Mapa_1_Arquivo_1.xls`

**Regras de importação:**

- O sistema abre a primeira aba do arquivo
- Dados lidos a partir da linha 6
- Apenas itens com `Match type = Exact Matches` são considerados
- Colunas lidas: col. 3 (PN), col. 14 (Unit price), col. 19 (MOQ), col. 21 (Estoque), col. 25 (Match type)

### DigiKey

**Link:** `https://www.digikey.com.br/pt/mylists/`

**Upload:**

1. Faça login e acesse "myList" → "Upload a list"
2. Faça o upload, mapeando "Referência do cliente" para PN1 e "Quantity 1" para QTD
3. Nos filtros, selecione "Matched Parts"
4. Faça o download em CSV, incluindo: "Número de peça do fabricante", "Disponibilidade", "Quantity, Attrition, Price, Packaging...", e "Referência do cliente"

**Renomear arquivo exportado:**

```
Digikey_Mapa_<numero_do_mapa>_Arquivo_<numero_do_arquivo>.csv
```

Exemplo: `Digikey_Mapa_1_Arquivo_1.csv`

**Regras de importação:**

- Arquivo CSV separado por vírgula
- Primeira linha = cabeçalho (ignorada)
- Colunas lidas: col. 1 (MPN), col. 2 (Estoque), col. 9 (Price), col. 11 (MOQ)

### Octopart

**Link:** `https://octopart.com/my/bom-tool`

**Upload:**

1. Acesse o site logado
2. Configure suas preferências de distribuidores em `https://octopart.com/my/preferences` (Arrow, Digi-Key, Future, Mouser, Verical, etc.)
3. Envie o arquivo BOM na ferramenta de BOM
4. Faça o download do CSV dos resultados

**Renomear arquivo exportado:**

```
Octo_Mapa_<numero_do_mapa>_Arquivo_<numero_do_arquivo>.csv
```

Exemplo: `Octo_Mapa_1_Arquivo_1.csv`

---

## Como a importação grava os dados na planilha

O sistema faz o cruzamento pelo `PN` do mapa e preenche, na coluna do distribuidor correspondente:

- Preço
- MOQ
- Estoque

**Regras do cruzamento:**

- O `PN` é comparado após normalização de espaços
- Linhas marcadas como `x`, `X`, `e`, `E`, `E1`, `E2`, `E3`, `E4` continuam sendo ignoradas
- Apenas o distribuidor existente no cabeçalho do mapa é atualizado

## Convenções de nome resumidas

| Origem                | Padrão de nome                 |
| --------------------- | ------------------------------ |
| BudgetApp (gerado)    | `BOM_Mapa_1_Arquivo_1.xlsx`    |
| LCSC (importação)     | `LCSC_Mapa_1_Arquivo_1.xls`    |
| DigiKey (importação)  | `Digikey_Mapa_1_Arquivo_1.csv` |
| Octopart (importação) | `Octo_Mapa_1_Arquivo_1.csv`    |

**Observações:**

- O nome precisa respeitar maiúsculas/minúsculas
- O arquivo precisa estar na mesma pasta da planilha
- A numeração `_Arquivo_1`, `_Arquivo_2` deve seguir a mesma ordem da exportação original

## Erros comuns

| Erro                                       | Causas possíveis                                                        |
| ------------------------------------------ | ----------------------------------------------------------------------- |
| Erro ao abrir o arquivo de entrada         | Planilha não selecionada, arquivo bloqueado, formato inválido           |
| Planilha inválida ou mapas não encontrados | Ausência da aba `Menu` ou `Mapa X`, senha incorreta, token ausente      |
| Erro ao ler arquivos de entrada            | Arquivo fora da pasta, nome incorreto, extensão errada, layout alterado |

## Observação

Se o site do distribuidor alterar o layout do arquivo exportado, o BudgetApp pode deixar de importar corretamente até que o código seja ajustado para o novo formato.
