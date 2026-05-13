# API Sidra (Direct) — Consulta Direta a Tabelas

Base URL: `https://apisidra.ibge.gov.br/values`

## Formato da URL

```
GET /values/t/{tabela}/p/{periodos}/v/{variaveis}/n{nivel}/{localidades}/c{classificacao}/{categorias}/h/{h}/f/{f}/d/{d}
```

## Parâmetros

### Tabela (obrigatório)
`/t/{codigo}` — Código numérico da tabela SIDRA

### Períodos (P)
`/p/all` — Todos os períodos
`/p/last` — Último período
`/p/last {n}` — Últimos n períodos
`/p/first {n}` — Primeiros n períodos
`/p/{cod1},{cod2}` — Lista de códigos
`/p/{cod1}-{cod2}` — Faixa de códigos

### Variáveis (V)
`/v/all` — Todas as variáveis (incluindo percentuais)
`/v/allxp` — Todas exceto percentuais
`/v/{cod1},{cod2}` — Lista de códigos

### Territórios (N ou G)
`/n1/all` — Brasil
`/n2/all` — Todas as Grandes Regiões
`/n3/all` — Todas as UFs
`/n3/{cod1},{cod2}` — UFs específicas
`/n6/all` — Todos os municípios
`/n6/{cod1},{cod2}` — Municípios específicos
`/n6/In%20n3%20{uf}` — Municípios dentro de UFs
`/g/{codigo}` — Visão territorial pré-definida (alternativa a N)

### Classificações (C)
`/c{id}/all` — Todas as categorias
`/c{id}/allxt` — Todas exceto o total
`/c{id}/{cat1},{cat2}` — Categorias específicas
`/c{id}/{cat1}%20{cat2}` — Soma de categorias

### Formatação
`/h/y` — Com cabeçalho (padrão)
`/h/n` — Sem cabeçalho
`/f/a` — Código e nome (padrão)
`/f/c` — Apenas código
`/f/n` — Apenas nome
`/f/u` — Código/nome da unidade territorial + nomes
`/d/s` — Decimais padrão (padrão)
`/d/m` — Máximo de decimais
`/d/0` a `/d/9` — Número fixo de decimais

### Formato de saída (query string)
`?formato=json` (padrão) ou `?formato=xml`

## Exemplos

### Produção de feijão, Brasil, 2021
```
GET /values/t/1612/n1/1/c81/2702/p/2021/v/allxp/f/n/h/n
```

### IPCA mensal, últimos 12 meses, Brasil
```
GET /values/t/1737/n1/all/c315/all/p/last%2012/v/allxp/f/n/h/n
```

### PIB por estado, 2022
```
GET /values/t/5938/n3/all/p/2022/v/allxp/f/n/h/n
```

### População por município de SP, 2023
```
GET /values/t/6579/n6/In%20n3%2035/p/2023/v/allxp/f/n/h/n
```

### Desemprego por região, série histórica
```
GET /values/t/4714/n2/all/p/all/v/allxp/f/n/h/n
```

## Caracteres Especiais nos Resultados

| Símbolo | Significado |
|---------|-------------|
| `-` | Zero absoluto (não arredondado) |
| `0` | Zero arredondado |
| `X` | Valor inibido (proteção de informante) |
| `..` | Não se aplica |
| `...` | Não disponível |
| `A-Z` | Faixa de valores |

## Notas
- Máximo de 100.000 valores por consulta
- Sem autenticação
- Documentação completa: https://apisidra.ibge.gov.br/home/ajuda
