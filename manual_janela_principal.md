# Janela Principal — Menu

## Visão geral

A janela principal do BudgetApp v17 é o ponto de entrada do programa. Ela apresenta botões para acessar cada funcionalidade do sistema.

## Como executar

```bash
python mainwindow.py
```

Ao iniciar, o programa carrega automaticamente as configurações do arquivo `Data/config.ini` (criptografado).

## Botões disponíveis

| Botão                         | Janela         | Descrição                                                     |
| ----------------------------- | -------------- | ------------------------------------------------------------- |
| **BOM**                       | Consolidar BOM | Consolida arquivos BOM e gera a planilha de vendas            |
| **PERDAS**                    | Perdas         | Calcula perdas de componentes por encapsulamento              |
| **NEXAR**                     | Nexar          | Consulta a API Nexar (Octopart) para preços e disponibilidade |
| **EXTERNO**                   | Externo        | Gera BOMs e importa resultados de LCSC, DigiKey e Octopart    |
| **PCI**                       | Email PCI      | Gera e envia e-mails de cotação de PCIs                       |
| **PN**                        | Email PN       | Gera e envia e-mails de cotação de componentes                |
| **FORNECEDORES - FATOR ÁSIA** | Fornecedores   | Gerencia distribuidores com fator Ásia na planilha            |
| **Info** (ícone)              | Info           | Exibe o fluxo de uso recomendado e informações de contato     |

## Janela Info

A janela **Info** contém duas abas:

- **MANUAL**: Exibe o fluxo de uso recomendado do programa (mesma sequência descrita no [README](README.md))
- **INFO**: Informações de contato do desenvolvedor e versão do programa
