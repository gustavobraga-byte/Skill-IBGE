# Instalação

## Como Agente (Claude Code / opencode)

Copie a pasta para o diretório de skills do seu agente:

```bash
# Se o diretório de skills existir
cp -r ibge-br ~/.agents/skills/ibge-br

# Ou clone direto do GitHub
git clone https://github.com/SEU-USUARIO/ibge-br.git ~/.agents/skills/ibge-br
```

A skill será carregada automaticamente quando o agente detectar consultas relacionadas ao IBGE.

## Como Referência (Uso Manual)

Você pode consultar as APIs do IBGE diretamente com `curl` ou qualquer cliente HTTP:

```bash
# Testar instalação — listar estados brasileiros
curl -s "https://servicodados.ibge.gov.br/api/v1/localidades/estados" | head -c 200
```

Todos os endpoints estão documentados nos arquivos em `references/`.

## Requisitos

- Nenhum. As APIs do IBGE são públicas e não exigem autenticação.
- Apenas um cliente HTTP (curl, wget, fetch, etc.) para consultas manuais.
