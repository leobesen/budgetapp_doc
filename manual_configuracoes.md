# Configurações Compartilhadas

Este documento descreve as janelas auxiliares de configuração que são acessadas a partir de diversas telas do BudgetApp.

---

## Editar Distribuidores

**Acessível de:** BOM (aba Distribuidores), Nexar, Fornecedores - Fator Ásia

Permite adicionar, remover ou renomear distribuidores na lista compartilhada do sistema.

### Como usar

1. Clique em **Editar** na janela de origem
2. A janela exibe um editor de texto com os nomes dos distribuidores (um por linha)
3. Edite a lista conforme necessário:
   - Para adicionar: insira o nome em uma nova linha
   - Para remover: apague a linha correspondente
   - Para renomear: altere o texto da linha
4. Clique em **Salvar**

### Comportamento ao salvar

- Os nomes são **normalizados** (espaços extras removidos)
- Nomes **duplicados** são automaticamente removidos
- A lista atualizada é gravada em `Data/fornecedores.ini`
- O editor é recarregado com a lista normalizada

### Mensagens de erro

| Mensagem         | Causa                               |
| ---------------- | ----------------------------------- |
| "Caixa vazia..." | Tentativa de salvar sem nenhum nome |

---

## Editar Endereços de E-mail

**Acessível de:** Email PCI (aba OM), Email PN

Permite editar os endereços de e-mail dos destinatários de cada fornecedor.

### Como usar

1. Clique em **Editar** (destinatários) na janela de e-mail
2. A janela exibe o conteúdo do arquivo INI correspondente em um editor de texto
3. Edite os endereços seguindo o formato INI:

```ini
[NOME_FORNECEDOR]
0 = email1@exemplo.com
1 = email2@exemplo.com

[OUTRO_FORNECEDOR]
0 = email3@exemplo.com
```

4. Clique em **Salvar**

### Arquivos editados

| Origem    | Arquivo                                 |
| --------- | --------------------------------------- |
| Email PCI | `Data/Email/email_pci_fornecedores.ini` |
| Email PN  | `Data/Email/email_pn_fornecedores.ini`  |

### Mensagens de erro

| Mensagem         | Causa                                  |
| ---------------- | -------------------------------------- |
| "Caixa vazia..." | Tentativa de salvar com o editor vazio |

---

## Editar Templates de E-mail

**Acessível de:** Email PCI (aba SPEC), Email PN

Permite criar, editar e excluir modelos (templates) de e-mail usados nas cotações de PCI e PN.

### Interface

| Campo                            | Descrição                                                                            |
| -------------------------------- | ------------------------------------------------------------------------------------ |
| **comboBox Modelo**              | Seleciona o template existente para edição                                           |
| **Saudação**                     | Texto de saudação/vocativo (ex: "Dear,")                                             |
| **Corpo**                        | Conteúdo da mensagem. Deve conter a tag `<<TABLE>>` para indicar a posição da tabela |
| **Despedida**                    | Texto de encerramento (ex: "Best Regards,")                                          |
| **radioButton Inglês/Português** | Define o idioma da tabela no e-mail                                                  |
| **lineEdit Nome**                | Nome para um novo template                                                           |

### Ações

- **Salvar**: Salva as alterações no template selecionado
- **Novo**: Cria um novo template com o nome informado no campo "Nome"
- **Excluir**: Remove o template selecionado (apaga os 4 arquivos correspondentes)

### Arquivos de template

Cada template consiste em 4 arquivos no diretório `Data/Templates/PCI/` ou `Data/Templates/PN/`:

| Arquivo                 | Conteúdo                            |
| ----------------------- | ----------------------------------- |
| `<nome>_salutation.txt` | Saudação                            |
| `<nome>_body.txt`       | Corpo da mensagem (com `<<TABLE>>`) |
| `<nome>_closing.txt`    | Despedida                           |
| `<nome>_table.txt`      | Idioma da tabela: `ENG` ou `PORT`   |

### A tag `<<TABLE>>`

No corpo do e-mail, a tag `<<TABLE>>` é **obrigatória**. Ela indica onde a tabela de especificações (PCI) ou a tabela de PNs (PN) será inserida no corpo da mensagem. O texto antes da tag será o parágrafo superior, e o texto após será o parágrafo inferior.

### Mensagens de erro

| Mensagem                                     | Causa                                              |
| -------------------------------------------- | -------------------------------------------------- |
| "Caixa vazia..."                             | Tentativa de salvar com campos de texto vazios     |
| "As caixas de texto não devem estar vazias." | Tentativa de criar novo template com campos vazios |
| "Insira um nome para o novo template."       | Campo "Nome" vazio ao criar novo template          |
| "Lista de templates vazia."                  | Tentativa de excluir sem templates disponíveis     |
