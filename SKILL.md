---
name: ibge-br
description: Skill para consultar as APIs oficiais do IBGE (Instituto Brasileiro de Geografia e Estatística). Cobre dados agregados (SIDRA), localidades, malhas geográficas, CNAE, nomes, notícias, indicadores de países, pesquisas, e calendário. Use esta skill sempre que o usuário precisar de dados estatísticos, geográficos, econômicos, demográficos, ou sociais do Brasil.
metadata:
  skill-author: opencode
---

# IBGE - Instituto Brasileiro de Geografia e Estatística

Skill para consultar **todas as APIs oficiais do IBGE**. Abaixo estão as APIs disponíveis, endpoints principais e exemplos de uso.

---

## APIs Disponíveis

| API | Versão | Base URL | Descrição |
|-----|--------|----------|-----------|
| **Agregados (SIDRA)** | v3 | `https://servicodados.ibge.gov.br/api/v3/agregados` | Dados de pesquisas e censos (PNAD, IPCA, PIB, Censo, etc.) |
| **SIDRA Direct** | — | `https://apisidra.ibge.gov.br/values` | Consulta direta a tabelas SIDRA |
| **Localidades** | v1 | `https://servicodados.ibge.gov.br/api/v1/localidades` | Divisões administrativas (regiões, UFs, municípios, distritos) |
| **Malhas** | v4 | `https://servicodados.ibge.gov.br/api/v4/malhas` | Mapas em GeoJSON/TopoJSON/SVG |
| **CNAE** | v2 | `https://servicodados.ibge.gov.br/api/v2/cnae` | Classificação Nacional de Atividades Econômicas |
| **Nomes** | v2 | `https://servicodados.ibge.gov.br/api/v2/censos/nomes` | Frequência de nomes (Censo 2010) |
| **Notícias** | v3 | `https://servicodados.ibge.gov.br/api/v3/noticias` | Releases e notícias da Agência IBGE |
| **Países** | v1 | `https://servicodados.ibge.gov.br/api/v1/paises` | Indicadores socioeconômicos de 193 países |
| **Pesquisas** | v1 | `https://servicodados.ibge.gov.br/api/v1/pesquisas` | Indicadores e resultados de pesquisas |
| **Calendário** | v3 | `https://servicodados.ibge.gov.br/api/v3/calendario` | Cronograma de divulgações do IBGE |

---

## Fluxo de Trabalho

1. **Entender o que o usuário quer** — Dados estatísticos? Geografia? Nomes? Notícias? Classificação econômica?
2. **Consultar o arquivo de referência** da API relevante em `references/` para ver exemplos e parâmetros.
3. **Fazer a chamada HTTP** usando a ferramenta de fetch disponível.
4. **Retornar os resultados** formatados de forma legível, com a URL da consulta e os dados obtidos.

---

## APIs e Endpoints Principais

### 1. Agregados (SIDRA) — Dados Estatísticos

Base: `https://servicodados.ibge.gov.br/api/v3/agregados`

**Endpoint: Listar agregados**
```
GET /api/v3/agregados
```
Parâmetros: `periodo`, `assunto`, `classificacao`, `periodicidade`, `nivel`

**Endpoint: Metadados de um agregado**
```
GET /api/v3/agregados/{agregado}/metadados
```

**Endpoint: Localidades por agregado**
```
GET /api/v3/agregados/{agregado}/localidades/{nivel}
```

**Endpoint: Períodos por agregado**
```
GET /api/v3/agregados/{agregado}/periodos
```

**Endpoint: Dados (variáveis por agregado, períodos e localidades)**
```
GET /api/v3/agregados/{agregado}/periodos/{periodos}/variaveis/{variavel}?localidades={localidades}&classificacao={classificacao}&view={view}
```

**Endpoint: Dados (últimos 6 períodos)**
```
GET /api/v3/agregados/{agregado}/variaveis/{variavel}?localidades={localidades}&classificacao={classificacao}
```

### 2. SIDRA Direct — Consulta Direta a Tabelas

Base: `https://apisidra.ibge.gov.br/values`

**Formato da URL:**
```
GET /values/t/{tabela}/p/{periodos}/v/{variaveis}/n{nivel}/{localidades}/c{classificacao}/{categorias}/h/{h}/f/{f}/d/{d}
```

**Parâmetros:**
- `t` — Código da tabela SIDRA (obrigatório)
- `p` — Períodos: `all`, `last [n]`, `first [n]`, ou lista de códigos (ex: `2020,2021`)
- `v` — Variáveis: `all` (todas), `allxp` (exceto percentuais), ou lista de códigos
- `n1`, `n2`, `n3`, `n6` — Nível territorial: `all` ou lista de códigos IBGE
- `g` — Visão territorial pré-definida (alternativa a n)
- `c81`, `c2`, etc. — Classificações e categorias
- `h` — Cabeçalho: `y` (sim) ou `n` (não)
- `f` — Formato campos: `a` (código+nome), `c` (código), `n` (nome), `u` (unidade territorial)
- `d` — Decimais: `s` (padrão), `m` (máximo), `0`-`9`

**Exemplo:**
```
GET /values/t/1612/n1/1/c81/2702/p/2021/v/allxp/f/n/h/n
```
Retorna dados da tabela 1612 (produção agrícola), Brasil, feijão, 2021, todas variáveis.

### 3. Localidades — Divisões Administrativas

Base: `https://servicodados.ibge.gov.br/api/v1/localidades`

| Recurso | Endpoint | Exemplo |
|---------|----------|---------|
| Regiões | `GET /regioes` | Todas as regiões |
| Região por ID | `GET /regioes/{id}` | `regioes/1` (Norte) |
| UFs (Estados) | `GET /estados` | Todos os estados |
| UF por ID | `GET /estados/{UF}` | `estados/35` (SP) ou `estados/SP` |
| UFs por região | `GET /regioes/{id}/estados` | `regioes/3/estados` (Sudeste) |
| Municípios | `GET /municipios` | Todos os municípios |
| Municípios por UF | `GET /estados/{UF}/municipios` | `estados/SP/municipios` |
| Município por ID | `GET /municipios/{id}` | `municipios/3550308` (São Paulo) |
| Distritos | `GET /distritos` | Todos os distritos |
| Distritos por UF | `GET /estados/{UF}/distritos` | |
| Mesorregiões | `GET /mesorregioes` | |
| Microrregiões | `GET /microrregioes` | |
| Regiões Metropolitanas | `GET /regioes-metropolitanas` | |
| Regiões Imediatas | `GET /regioes-imediatas` | |
| Regiões Intermediárias | `GET /regioes-intermediarias` | |
| Países | `GET /paises` | |
| País por ID | `GET /paises/{pais}` | `paises/BR` |

Parâmetros comuns: `orderBy`, `view`

### 4. Malhas Geográficas — Mapas

Base: `https://servicodados.ibge.gov.br/api/v4/malhas`

| Recurso | Endpoint | Formatos |
|---------|----------|----------|
| País (Brasil) | `GET /paises/BR` | SVG, GeoJSON, TopoJSON |
| Região | `GET /regioes/{id}` | |
| Estado | `GET /estados/{id}` | |
| Município | `GET /municipios/{id}` | |
| Região Imediata | `GET /regioes-imediatas/{id}` | |
| Região Intermediária | `GET /regioes-intermediarias/{id}` | |

Parâmetros: `qualidade` (1-4), `formato` (svg, geoJSON, topoJSON), `intrarregiao`

Metadados: adicionar `/metadados` ao final do endpoint

### 5. CNAE — Classificação de Atividades

Base: `https://servicodados.ibge.gov.br/api/v2/cnae`

| Recurso | Endpoint |
|---------|----------|
| Seções | `GET /secoes` |
| Seção por ID | `GET /secoes/{secao}` (ex: `A`, `J`) |
| Divisões | `GET /divisoes` |
| Divisões por seção | `GET /secoes/{secao}/divisoes` |
| Grupos | `GET /grupos` |
| Grupos por divisão | `GET /divisoes/{divisao}/grupos` |
| Classes | `GET /classes` |
| Classe por ID | `GET /classes/{classe}` (ex: `6201-5/01`) |
| Subclasses | `GET /subclasses` |

### 6. Nomes — Frequência de Nomes

Base: `https://servicodados.ibge.gov.br/api/v2/censos/nomes`

**Frequência por nome:**
```
GET /api/v2/censos/nomes/{nome}?sexo={M|F}&groupBy={decada|localidade|uf}&localidade={codigo}
```

**Ranking de nomes:**
```
GET /api/v2/censos/nomes/ranking?decada={1930..2010}&localidade={codigo}&sexo={M|F}
```

### 7. Notícias

Base: `https://servicodados.ibge.gov.br/api/v3/noticias`

```
GET /api/v3/noticias?tipo={release|noticia}&qtd={10}&page={1}&busca={termo}&destaque={true|false}&de={data}&ate={data}
```

### 8. Países — Indicadores Internacionais

Base: `https://servicodados.ibge.gov.br/api/v1/paises`

**Listar países:**
```
GET /api/v1/paises/{paises}?lang={pt|en|es}
```

**Indicadores:**
```
GET /api/v1/paises/indicadores/{indicadores}
```

**Indicadores por país:**
```
GET /api/v1/paises/{paises}/indicadores/{indicadores}?periodo={periodo}
```

Códigos de indicadores comuns: `77849` (população), `77824` (PIB total), `77823` (PIB per capita), `77831` (IDH), `77830` (expectativa de vida)

### 9. Pesquisas

Base: `https://servicodados.ibge.gov.br/api/v1/pesquisas`

**Listar pesquisas:**
```
GET /api/v1/pesquisas?q={termo}
```

**Pesquisa por ID:**
```
GET /api/v1/pesquisas/{pesquisas}
```

**Indicadores por pesquisa:**
```
GET /api/v1/pesquisas/{pesquisa}/indicadores/{posicao}?localidade={codigo}
```

**Resultados:**
```
GET /api/v1/pesquisas/{pesquisa}/resultados/{localidades}
```

### 10. Calendário

Base: `https://servicodados.ibge.gov.br/api/v3/calendario`

```
GET /api/v3/calendario?de={data}&ate={data}&produto={IPCA|PNAD|PIB}&tipo={divulgacao|coleta}
```

---

## Códigos de Localidades IBGE

- **Brasil**: `1` (nível `n1`) ou código `BR`
- **Regiões**: `1` (Norte), `2` (Nordeste), `3` (Sudeste), `4` (Sul), `5` (Centro-Oeste) — siglas: `N, NE, SE, S, CO`
- **Estados (UFs)**: 2 dígitos — ex: `35` (SP), `33` (RJ), `31` (MG) — ou sigla: `SP, RJ, MG`
- **Municípios**: 7 dígitos — ex: `3550308` (São Paulo), `3304557` (Rio de Janeiro)
- **Distritos**: 9 dígitos

## Níveis Territoriais (SIDRA)

| Código | Nível |
|--------|-------|
| N1 | Brasil |
| N2 | Grande Região |
| N3 | Unidade da Federação (UF) |
| N6 | Município |
| N7 | Região Metropolitana |
| N8 | Mesorregião |
| N9 | Microrregião |
| N10 | Distrito |
| N13 | RM e RIDE |
| N14 | Região Integrada de Desenvolvimento |
| N17 | Região Geográfica Imediata |
| N18 | Região Geográfica Intermediária |

---

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
| 1612 | Produção agrícola municipal |
| 1705 | Exemplo da documentação |
| 1419 | IPCA — Índice Nacional de Preços |
| 1737 | IPCA — Variação mensal |
| 7060 | INPC |
| 1848 | Mortalidade infantil |
| 1613 | Produção pecuária municipal |

## Todo código precisa de recurso? (Sem API Key)

Todas as APIs do IBGE são **públicas e gratuitas**, sem necessidade de autenticação.

---

## Referências

- Documentação oficial: https://servicodados.ibge.gov.br/api/docs
- Documentação SIDRA: https://apisidra.ibge.gov.br/
- Query Builder SIDRA: https://apisidra.ibge.gov.br/home/ajuda
