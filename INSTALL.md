# Instalação — Skill IBGE

Instruções para instalar esta skill em qualquer assistente de IA (Claude Code, Cursor, Windsurf, Cline, Continue.dev, Copilot, etc.).

> ✅ Todas as APIs do IBGE são **públicas e gratuitas** — sem chave, sem token, sem cadastro.

---

## Índice

- [Visão Geral](#visão-geral)
- [Método 1: Claude Code / opencode](#método-1-claude-code--opencode)
- [Método 2: Cursor](#método-2-cursor)
- [Método 3: Windsurf](#método-3-windsurf)
- [Método 4: Cline (VS Code)](#método-4-cline-vs-code)
- [Método 5: Continue.dev](#método-5-continuedev)
- [Método 6: GitHub Copilot / Copilot Chat](#método-6-github-copilot--copilot-chat)
- [Método 7: Aider](#método-7-aider)
- [Método 8: RAG / Base de Conhecimento](#método-8-rag--base-de-conhecimento)
- [Método 9: Uso Manual (curl / Python / JS)](#método-9-uso-manual)
- [Verificação](#verificação)

---

## Visão Geral

Há **3 formas principais** de usar esta skill:

| Abordagem | Descrição |
|-----------|-----------|
| **Instalação como skill** | O agente carrega automaticamente o `SKILL.md` + arquivos de referência quando detecta consultas sobre IBGE |
| **Contexto RAG** | Adicione os arquivos `.md` como documentos em sistemas de RAG (bases vetoriais, knowledge bases) |
| **Referência manual** | Use os comandos `curl` nos arquivos de referência para consultar as APIs diretamente |

---

## Método 1: Claude Code / opencode

### Opção A — Clonar direto no diretório de skills

```bash
git clone https://github.com/gustavobraga-byte/Skill-IBGE.git ~/.agents/skills/ibge-br
```

### Opção B — Copiar manualmente

```bash
# Baixe o repositório
git clone https://github.com/gustavobraga-byte/Skill-IBGE.git /tmp/ibge-br
# Copie para o diretório de skills
cp -r /tmp/ibge-br ~/.agents/skills/ibge-br
```

A skill será carregada automaticamente quando o agente detectar consultas relacionadas ao IBGE.

---

## Método 2: Cursor

Copie para o diretório `.cursor/skills/` **na raiz do seu projeto**:

```bash
# Na raiz do seu projeto
git clone https://github.com/gustavobraga-byte/Skill-IBGE.git .cursor/skills/ibge-br
```

Ou manualmente:

```bash
mkdir -p .cursor/skills
cp -r /caminho/para/ibge-br .cursor/skills/ibge-br
```

O Cursor carrega skills de `.cursor/skills/` automaticamente.

---

## Método 3: Windsurf

Copie para o diretório `.windsurf/skills/` **na raiz do seu projeto**:

```bash
git clone https://github.com/gustavobraga-byte/Skill-IBGE.git .windsurf/skills/ibge-br
```

---

## Método 4: Cline (VS Code)

Cline aceita **regras customizadas** via arquivos de instruções.

### Opção A — Instruções globais do Cline

Adicione o conteúdo do `SKILL.md` (ou o caminho do arquivo) nas **Instruções Customizadas do Cline**:

1. Abra as configurações do Cline (ícone de engrenagem na extensão)
2. Em "Custom Instructions", adicione:

```
Você tem acesso à Skill IBGE. Consulte o arquivo SKILL.md e os arquivos em references/ para endpoints e exemplos.
```

### Opção B — Como contexto no prompt

Cole o conteúdo de `SKILL.md` no prompt ou use o Cline com `--file`:

```
@file /caminho/para/ibge-br/SKILL.md
```

---

## Método 5: Continue.dev

Adicione os arquivos `.md` como **documentos de contexto** no arquivo `config.json` do Continue:

```json
{
  "docs": [
    {
      "title": "IBGE Skill",
      "url": "https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/SKILL.md"
    }
  ]
}
```

Ou copie localmente e referencie como `@file`:

```
@file /caminho/para/ibge-br/references/agregados.md
```

---

## Método 6: GitHub Copilot / Copilot Chat

### Opção A — .github/copilot-instructions.md

Crie o arquivo `.github/copilot-instructions.md` no repositório:

```markdown
## IBGE Data API

Você pode consultar dados do IBGE (Instituto Brasileiro de Geografia e Estatística)
usando as APIs públicas listadas no repositório:
https://github.com/gustavobraga-byte/Skill-IBGE

Todas as APIs são gratuitas e sem autenticação.

Exemplos rápidos:
- População: `curl "https://apisidra.ibge.gov.br/values/t/9514/n6/3550308/p/2022/v/allxp/f/n/h/n"`
- Estados: `curl "https://servicodados.ibge.gov.br/api/v1/localidades/estados"`
- IPCA: `curl "https://apisidra.ibge.gov.br/values/t/1737/n1/all/p/last%2012/v/allxp/f/n/h/n"`
```

### Opção B — Contexto explícito no chat

No Copilot Chat, referencie o repositório:

```
Use the IBGE skill from github.com/gustavobraga-byte/Skill-IBGE to help me query Brazilian census data
```

---

## Método 7: Aider

Use com o `--read` para carregar os arquivos de referência:

```bash
aider --read /caminho/para/ibge-br/SKILL.md --read /caminho/para/ibge-br/references/agregados.md
```

Ou adicione ao seu arquivo `.aider.conf.yml`:

```yaml
read:
  - /caminho/para/ibge-br/SKILL.md
```

---

## Método 8: RAG / Base de Conhecimento

Adicione os arquivos `.md` como documentos no seu sistema RAG:

```bash
# Copiar toda a pasta para a base de conhecimento
cp -r ibge-br /caminho/para/sua-base/

# Ou referenciar as URLs raw do GitHub
```

**URLs raw para ingestão em bases vetoriais:**

| Arquivo | URL |
|---------|-----|
| SKILL.md | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/SKILL.md` |
| Agregados | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/agregados.md` |
| SIDRA Direct | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/sidra-direct.md` |
| Localidades | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/localidades.md` |
| Malhas | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/malhas.md` |
| CNAE | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/cnae.md` |
| Nomes | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/nomes.md` |
| Notícias | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/noticias.md` |
| Países | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/paises.md` |
| Pesquisas | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/pesquisas.md` |
| Calendário | `https://raw.githubusercontent.com/gustavobraga-byte/Skill-IBGE/main/references/calendario.md` |

---

## Método 9: Uso Manual

Mesmo sem um agente de IA, você pode usar as APIs diretamente com qualquer linguagem.

### curl

```bash
# Listar estados
curl -s "https://servicodados.ibge.gov.br/api/v1/localidades/estados" | jq '.[].nome'

# População de SP (Censo 2022)
curl -s "https://apisidra.ibge.gov.br/values/t/9514/n6/3550308/p/2022/v/allxp/f/n/h/n"

# IPCA últimos 12 meses (formatado)
curl -s "https://apisidra.ibge.gov.br/values/t/1737/n1/all/p/last%2012/v/allxp/f/n/h/n" | jq
```

### Python

```python
import requests
import json

# Listar estados
resp = requests.get("https://servicodados.ibge.gov.br/api/v1/localidades/estados")
estados = resp.json()
for e in estados:
    print(f"{e['sigla']} - {e['nome']}")

# População de um município
resp = requests.get(
    "https://apisidra.ibge.gov.br/values/t/9514/n6/3550308/p/2022/v/allxp/f/n/h/n"
)
print(json.dumps(resp.json(), indent=2, ensure_ascii=False))
```

### JavaScript (Node.js)

```javascript
const res = await fetch(
  "https://servicodados.ibge.gov.br/api/v1/localidades/estados/SP/municipios"
);
const data = await res.json();
console.log(data.map(m => m.nome).slice(0, 10));
```

---

## Verificação

Teste se a instalação funcionou:

```bash
# Teste 1: Listar estados brasileiros (deve funcionar sempre)
curl -s "https://servicodados.ibge.gov.br/api/v1/localidades/estados" | jq 'length'
# Deve retornar: 27

# Teste 2: População do Brasil (Censo 2022)
curl -s "https://apisidra.ibge.gov.br/values/t/9514/n1/all/p/2022/v/allxp/f/n/h/n" | jq '.[1].V'
# Deve retornar: 203080756 (ou valor similar)
```

Se os comandos acima retornarem dados, a skill está pronta para uso.

---

## Estrutura dos Arquivos

```
ibge-br/
├── README.md           # Visão geral do projeto
├── INSTALL.md          # Este arquivo
├── SKILL.md            # Arquivo principal da skill (carregado pelo agente)
├── CONTRIBUTING.md     # Guia de contribuição
├── LICENSE             # Licença MIT
└── references/         # Referências detalhadas por API
    ├── agregados.md    # API de Agregados (SIDRA) v3
    ├── sidra-direct.md # API Sidra Direct
    ├── localidades.md  # API de Localidades v1
    ├── malhas.md       # API de Malhas Geográficas v4
    ├── cnae.md         # API CNAE v2
    ├── nomes.md        # API Nomes v2
    ├── noticias.md     # API Notícias v3
    ├── paises.md       # API Países v1
    ├── pesquisas.md    # API de Pesquisas v1
    └── calendario.md   # API Calendário v3
```
