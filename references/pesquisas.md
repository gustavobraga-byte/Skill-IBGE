# API de Pesquisas — v1

Base URL: `https://servicodados.ibge.gov.br/api/v1/pesquisas`

## Endpoints

### Listar pesquisas
```
GET /api/v1/pesquisas?q={termo}
```

### Pesquisa por ID
```
GET /api/v1/pesquisas/{pesquisas}
```

### Períodos de uma pesquisa
```
GET /api/v1/pesquisas/{pesquisa}/periodos
```

### Indicadores por pesquisa (todos períodos)
```
GET /api/v1/pesquisas/{pesquisa}/indicadores/{posicao}
```
Parâmetros: `scope`, `localidade`

### Indicadores por pesquisa e períodos
```
GET /api/v1/pesquisas/{pesquisa}/periodos/{periodos}/indicadores/{posicao}
```
Parâmetros: `scope`, `localidade`

### Resultados por pesquisa
```
GET /api/v1/pesquisas/{pesquisa}/resultados/{localidades}
```
Parâmetros: `scope`, `groupBy`

### Resultados por pesquisa, indicadores
```
GET /api/v1/pesquisas/{pesquisa}/indicadores/{posicao}/resultados/{localidades}
```
Parâmetros: `scope`, `groupBy`

### Resultados por pesquisa, períodos, indicadores
```
GET /api/v1/pesquisas/{pesquisa}/periodos/{periodos}/indicadores/{posicao}/resultados/{localidades}
```
Parâmetros: `scope`, `groupBy`

### Resultados por indicador (qualquer pesquisa)
```
GET /api/v1/pesquisas/-/indicadores/{indicador}/resultados/{localidade}
```

### Ranking
```
GET /api/v1/pesquisas/{pesquisa}/indicadores/{indicador}/ranking
```
Parâmetros: `orderBy`, `contexto`, `natureza`, `offset`, `lower`, `upper`, `localidade`

```
GET /api/v1/pesquisas/{pesquisa}/periodos/{periodos}/indicadores/{indicador}/ranking
```

## Exemplos

### Listar todas pesquisas
```bash
curl "https://servicodados.ibge.gov.br/api/v1/pesquisas"
```

### Buscar pesquisa "PNAD"
```bash
curl "https://servicodados.ibge.gov.br/api/v1/pesquisas?q=PNAD"
```

### Períodos da pesquisa PNAD Contínua
```bash
curl "https://servicodados.ibge.gov.br/api/v1/pesquisas/{pesquisa_id}/periodos"
```

## Notas
- Subconjunto da API de Agregados
- Retorna indicadores enriquecidos de fontes internas e externas
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/pesquisas
