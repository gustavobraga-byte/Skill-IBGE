# Instalação

## Como Skill para Agentes de IA

### Claude Code / opencode

Copie a pasta para o diretório de skills:

```bash
cp -r ibge-br ~/.agents/skills/ibge-br
# Ou clone direto do GitHub
git clone https://github.com/SEU-USUARIO/ibge-br.git ~/.agents/skills/ibge-br
```

A skill será carregada automaticamente quando o agente detectar consultas relacionadas ao IBGE.

### Cursor

Copie para o diretório `.cursor/skills/` do seu projeto:

```bash
cp -r ibge-br .cursor/skills/ibge-br
```

### Windsurf

Copie para o diretório `.windsurf/skills/` do seu projeto:

```bash
cp -r ibge-br .windsurf/skills/ibge-br
```

### Outros Agentes (Copilot, Codeium, Continue.dev, etc.)

Use o repositório como contexto — clone e referencie os arquivos `.md` como documentação nos prompts:

```bash
git clone https://github.com/SEU-USUARIO/ibge-br.git
```

Os arquivos em `references/` contêm exemplos de `curl` prontos para uso que funcionam em qualquer ferramenta.

## Como Base de Conhecimento (RAG / Contexto)

Adicione os arquivos `.md` como documentos de contexto no seu sistema RAG:

```bash
# Exemplo: copiar para uma base de conhecimento
cp -r ibge-br /caminho/para/sua/base/
```

Cada arquivo em `references/` cobre uma API específica com endpoints, parâmetros e exemplos.

## Como Referência (Uso Manual com curl)

Qualquer pessoa pode consultar as APIs do IBGE com `curl`:

```bash
# Testar — listar estados brasileiros
curl -s "https://servicodados.ibge.gov.br/api/v1/localidades/estados" | head -c 200
```

```python
# Ou com Python
import requests
resp = requests.get("https://servicodados.ibge.gov.br/api/v1/localidades/estados/SP/municipios")
print(resp.json())
```

```javascript
// Ou com JavaScript (Node.js)
const res = await fetch("https://servicodados.ibge.gov.br/api/v1/localidades/estados");
const data = await res.json();
console.log(data);
```

## Requisitos

- Nenhum. As APIs do IBGE são **públicas e gratuitas** — sem chave, sem token, sem cadastro.
- Para uso manual: apenas `curl` ou qualquer cliente HTTP.
