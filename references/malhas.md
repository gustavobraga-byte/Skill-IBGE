# API de Malhas Geográficas — v4

Base URL: `https://servicodados.ibge.gov.br/api/v4/malhas`

## Endpoints

### País
```
GET /api/v4/malhas/paises/{id}           # id = BR
GET /api/v4/malhas/paises/{id}/metadados
```

### Região
```
GET /api/v4/malhas/regioes/{id}          # 1,2,3,4,5 ou N,NE,SE,S,CO
GET /api/v4/malhas/regioes/{id}/metadados
```

### Estado (UF)
```
GET /api/v4/malhas/estados/{id}          # código (35) ou sigla (SP)
GET /api/v4/malhas/estados/{id}/metadados
```

### Município
```
GET /api/v4/malhas/municipios/{id}       # código de 7 dígitos
GET /api/v4/malhas/municipios/{id}/metadados
```

### Região Imediata
```
GET /api/v4/malhas/regioes-imediatas/{id}
GET /api/v4/malhas/regioes-imediatas/{id}/metadados
```

### Região Intermediária
```
GET /api/v4/malhas/regioes-intermediarias/{id}
GET /api/v4/malhas/regioes-intermediarias/{id}/metadados
```

## Parâmetros

| Parâmetro | Descrição | Valores |
|-----------|-----------|---------|
| `qualidade` | Qualidade do traçado | `1` (mínima) a `4` (máxima, padrão) |
| `formato` | Formato de saída | `svg` (padrão), `application/vnd.geo+json`, `application/json` |
| `intrarregiao` | Divisões internas | `BR` (Brasil), sigla de UF, código de região intermediária, imediata ou município |

O formato pode ser definido por:
- Parâmetro `formato` na query string
- Header `Accept`: `image/svg+xml`, `application/vnd.geo+json`, `application/json`

## Exemplos

### Mapa do Brasil com estados (SVG)
```bash
curl "https://servicodados.ibge.gov.br/api/v4/malhas/paises/BR?intrarregiao=UF"
```

### Mapa do estado de SP (GeoJSON)
```bash
curl -H "Accept: application/vnd.geo+json" "https://servicodados.ibge.gov.br/api/v4/malhas/estados/SP"
```

### Mapa do município de São Paulo (TopoJSON)
```bash
curl -H "Accept: application/json" "https://servicodados.ibge.gov.br/api/v4/malhas/municipios/3550308"
```

### Metadados da malha de SP
```bash
curl "https://servicodados.ibge.gov.br/api/v4/malhas/estados/SP/metadados"
```

## Notas
- Malhas são simplificadas (não as originais)
- Atualizadas anualmente conforme calendário do IBGE
- Formatos: SVG (imagem leve), GeoJSON (dados geoespaciais), TopoJSON (compacto)
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/malhas?versao=4
