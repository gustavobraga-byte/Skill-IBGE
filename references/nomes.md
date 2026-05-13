# API Nomes — v2

Base URL: `https://servicodados.ibge.gov.br/api/v2/censos/nomes`

## Endpoints

### Frequência por nome
```
GET /api/v2/censos/nomes/{nome}
```

Parâmetros:
- `sexo` — `M` (masculino) ou `F` (feminino)
- `groupBy` — agrupamento: `decada` (padrão), `localidade`, `uf`
- `localidade` — código IBGE da localidade (UF=2 dígitos, munic=7 dígitos, `BR`=Brasil)

### Ranking
```
GET /api/v2/censos/nomes/ranking
```

Parâmetros:
- `decada` — década: `1930`, `1940`, ..., `2010`
- `localidade` — código IBGE
- `sexo` — `M` ou `F`

## Exemplos

### Frequência do nome "Maria" no Brasil
```bash
curl "https://servicodados.ibge.gov.br/api/v2/censos/nomes/Maria"
```

### Frequência de "João" em SP por década
```bash
curl "https://servicodados.ibge.gov.br/api/v2/censos/nomes/João?localidade=35"
```

### Frequência de "Ana" por UF
```bash
curl "https://servicodados.ibge.gov.br/api/v2/censos/nomes/Ana?groupBy=uf"
```

### Ranking dos nomes masculinos mais comuns no Brasil (2010)
```bash
curl "https://servicodados.ibge.gov.br/api/v2/censos/nomes/ranking?sexo=M&decada=2010"
```

### Ranking dos nomes femininos no Rio de Janeiro (1990)
```bash
curl "https://servicodados.ibge.gov.br/api/v2/censos/nomes/ranking?sexo=F&decada=1990&localidade=33"
```

## Notas
- Dados coletados no Censo 2010
- Para Brasil, use localidade=`BR`
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/nomes?versao=2
