# Email PCI

## Visão geral

A janela **PCI** permite montar e enviar e-mails de cotação para fornecedores de Placas de Circuito Impresso (PCI). O e-mail inclui especificações técnicas das placas, quantidades por lote e informações de painel.

O envio é feito via **Microsoft Outlook** (automação COM).

## Interface

A janela é dividida em duas abas: **OM** (destinatários) e **SPEC** (especificações da PCI).

---

### Aba OM

Configura o número da OM e os destinatários do e-mail.

| Campo                | Descrição                                                                      |
| -------------------- | ------------------------------------------------------------------------------ |
| **spinBox OM**       | Número da Ordem de Material (OM)                                               |
| **comboBox Destino** | Empresa do destinatário (carregado de `Data/Email/email_pci_fornecedores.ini`) |

**Tabela de destinatários:**

| Coluna       | Descrição                            |
| ------------ | ------------------------------------ |
| Destinatário | Endereço de e-mail (somente leitura) |
| Para         | Checkbox — destinatário principal    |
| Cc           | Checkbox — cópia                     |

**Botões:**

- **Atualizar**: Recarrega a lista de destinatários do arquivo INI
- **Editar**: Abre a janela de [edição de endereços de e-mail](manual_configuracoes.md#editar-endereços-de-e-mail)

---

### Aba SPEC

Configura as especificações técnicas de cada PCI a ser cotada.

| Campo                         | Descrição                 |
| ----------------------------- | ------------------------- |
| **Nome da PCI**               | PN da placa de circuito   |
| **Nome do arquivo do painel** | Nome do arquivo de painel |
| **PCI por painel**            | Número de PCIs por painel |

**Slider Lotes** (1 a 5): Define a quantidade de lotes. A tabela de lotes exibe duas linhas:

- **Lotes**: Quantidade de PCIs por lote
- **Extra**: Painéis extras por lote

O programa calcula automaticamente o número de painéis necessários com base na quantidade do lote, PCIs por painel e painéis extras.

**Tabela de especificações** (7 linhas):

| Especificação                    | Valor padrão                                             |
| -------------------------------- | -------------------------------------------------------- |
| Matéria Prima (FR4,...)          | FR4                                                      |
| Acabamento (HASL, ENIG, OSP,...) | HASL                                                     |
| TG (Temperatura do Vidro)        | 120                                                      |
| Espessura do Cobre (Oz)          | 0,5                                                      |
| Espessura da Placa (mm)          | 1,6                                                      |
| Cor da Máscara de Solda          | comboBox (Verde, Branco, Preto, Vermelho, Azul, Amarelo) |
| Cor da Serigrafia                | comboBox (Verde, Branco, Preto, Vermelho, Azul, Amarelo) |

Os 5 primeiros campos são editáveis com texto livre. Os 2 últimos utilizam comboBox com cores pré-definidas.

**Botões:**

- **Adicionar PCI**: Adiciona a PCI configurada ao e-mail (o LCD exibe a contagem)
- **Remover PCI**: Remove a última PCI adicionada

**Template:**

- **comboBox Template**: Seleciona o modelo de e-mail (carregado de `Data/Templates/PCI/`)
- **Editar**: Abre a janela de [edição de templates](manual_configuracoes.md#editar-templates-de-e-mail)

---

### Enviar

Clique em **Enviar** para gerar e enviar o e-mail.

O assunto do e-mail segue o formato: `OM<número>/<ano> - <destinatário>`

Exemplo: `OM001/26 - CIRCUIBRAS`

## Templates

Os templates de e-mail ficam em `Data/Templates/PCI/` e consistem em 4 arquivos por modelo:

- `<nome>_salutation.txt` — Saudação/vocativo
- `<nome>_body.txt` — Corpo da mensagem (deve conter a tag `<<TABLE>>` para posicionar a tabela de especificações)
- `<nome>_closing.txt` — Despedida
- `<nome>_table.txt` — Idioma da tabela (`ENG` ou `PORT`)

## Mensagens de erro

| Mensagem                                   | Causa                                  |
| ------------------------------------------ | -------------------------------------- |
| "Nome da PCI não dicionado!"               | Campo nome da PCI vazio                |
| "Nome do arquivo de painel não dicionado!" | Campo nome do arquivo vazio            |
| "Nenhum destinatário selecionado!"         | Nenhum checkbox "Para" marcado         |
| "Nenhuma PCI adicionada!"                  | Tentativa de enviar sem adicionar PCIs |
