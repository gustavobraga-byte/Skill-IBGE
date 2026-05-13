# 🇧🇷 IBGE BR — Claude Skill para APIs do IBGE

Skill para o Claude (Anthropic) que permite consultar **todas as APIs oficiais do IBGE** (Instituto Brasileiro de Geografia e Estatística) — dados agregados (SIDRA), localidades, malhas geográficas, CNAE, nomes, notícias, indicadores de países, pesquisas e calendário.

## APIs Cobertas

| API | Versão | Descrição |
|-----|--------|-----------|
| **Agregados (SIDRA)** | v3 | Dados de pesquisas e censos (PNAD, IPCA, PIB, Censo, etc.) |
| **SIDRA Direct** | — | Consulta direta a tabelas SIDRA |
| **Localidades** | v1 | Regiões, UFs, municípios, distritos, mesorregiões |
| **Malhas Geográficas** | v4 | Mapas em GeoJSON / TopoJSON / SVG |
| **CNAE** | v2 | Classificação Nacional de Atividades Econômicas |
| **Nomes** | v2 | Frequência de nomes (Censo 2010) |
| **Notícias** | v3 | Releases e notícias da Agência IBGE |
| **Países** | v1 | Indicadores socioeconômicos de 193 países |
| **Pesquisas** | v1 | Indicadores e resultados de pesquisas |
| **Calendário** | v3 | Cronograma de divulgações do IBGE |

Todas as APIs são **públicas e gratuitas** — sem necessidade de autenticação.

## Estrutura do Projeto

```
ibge-br/
├── README.md
├── INSTALL.md
├── CONTRIBUTING.md
├── LICENSE
├── SKILL.md              # Arquivo principal da skill
└── references/           # Referências detalhadas por API
    ├── agregados.md      # API de Agregados (SIDRA) v3
    ├── sidra-direct.md   # API Sidra Direct
    ├── localidades.md    # API de Localidades v1
    ├── malhas.md         # API de Malhas Geográficas v4
    ├── cnae.md           # API CNAE v2
    ├── nomes.md          # API Nomes v2
    ├── noticias.md       # API Notícias v3
    ├── paises.md         # API Países v1
    ├── pesquisas.md      # API de Pesquisas v1
    └── calendario.md     # API Calendário v3
```

## Exemplos Rápidos

```bash
# População de São Paulo (cidade) — Censo 2022
curl "https://apisidra.ibge.gov.br/values/t/9514/n6/3550308/p/2022/v/allxp/f/n/h/n"

# Produção de café em Araponga (MG) — 2024
curl "https://apisidra.ibge.gov.br/values/t/1613/n6/3103702/c82/2723/p/2024/v/214/f/n/h/n"

# Listar todos os estados
curl "https://servicodados.ibge.gov.br/api/v1/localidades/estados"

# Municípios de São Paulo
curl "https://servicodados.ibge.gov.br/api/v1/localidades/estados/SP/municipios"

# IPCA — últimos 12 meses
curl "https://apisidra.ibge.gov.br/values/t/1737/n1/all/p/last%2012/v/allxp/f/n/h/n"

# PIB per capita por estado — 2022
curl "https://apisidra.ibge.gov.br/values/t/5938/n3/all/p/2022/v/allxp/f/n/h/n"

# Frequência do nome "Maria"
curl "https://servicodados.ibge.gov.br/api/v2/censos/nomes/Maria"

# Mapa do Brasil com estados (SVG)
curl "https://servicodados.ibge.gov.br/api/v4/malhas/paises/BR?intrarregiao=UF"
```

## Tabelas SIDRA Comuns

| Código | Descrição |
|--------|-----------|
| 6579 | Estimativas populacionais |
| 9514 | Censo 2022 — População |
| 200 | Censo — População (série histórica 1970-2010) |
| 4714 | PNAD Contínua — Taxa de desemprego |
| 6381 | PNAD Contínua — Rendimento médio |
| 6706 | PIB a preços correntes |
| 5938 | PIB per capita |
| 1612 | Produção agrícola — lavouras temporárias |
| 1613 | Produção agrícola — lavouras permanentes |
| 1419 | IPCA — Índice Nacional de Preços |
| 1737 | IPCA — Variação mensal |
| 7060 | INPC |

## Códigos de Localidades

| Nível | Formato | Exemplo |
|-------|---------|---------|
| Brasil | `1` ou `BR` | |
| Região | 1 dígito ou sigla | `1` ou `N` (Norte), `3` ou `SE` (Sudeste) |
| UF | 2 dígitos ou sigla | `35` ou `SP`, `33` ou `RJ` |
| Município | 7 dígitos | `3550308` (São Paulo), `3103702` (Araponga) |
| Distrito | 9 dígitos | — |

## Links Úteis

- [Documentação oficial das APIs IBGE](https://servicodados.ibge.gov.br/api/docs)
- [API Sidra — Ajuda](https://apisidra.ibge.gov.br/home/ajuda)
- [SIDRA — Consulta Web](https://sidra.ibge.gov.br)
- [IBGE — Portal](https://www.ibge.gov.br)

## Licença

MIT
