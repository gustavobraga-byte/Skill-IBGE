# API de Localidades — v1

Base URL: `https://servicodados.ibge.gov.br/api/v1/localidades`

## Endpoints

### Regiões do Brasil
```
GET /api/v1/localidades/regioes
GET /api/v1/localidades/regioes/{id}       # 1=Norte, 2=NE, 3=SE, 4=Sul, 5=CO
```

### Unidades da Federação (Estados)
```
GET /api/v1/localidades/estados
GET /api/v1/localidades/estados/{UF}        # código (35) ou sigla (SP)
GET /api/v1/localidades/regioes/{id}/estados
```

### Municípios
```
GET /api/v1/localidades/municipios
GET /api/v1/localidades/municipios/{id}     # código de 7 dígitos
GET /api/v1/localidades/estados/{UF}/municipios
GET /api/v1/localidades/mesorregioes/{id}/municipios
GET /api/v1/localidades/microrregioes/{id}/municipios
GET /api/v1/localidades/regioes/{id}/municipios
GET /api/v1/localidades/regioes-imediatas/{id}/municipios
GET /api/v1/localidades/regioes-intermediarias/{id}/municipios
```

### Distritos
```
GET /api/v1/localidades/distritos
GET /api/v1/localidades/distritos/{id}
GET /api/v1/localidades/estados/{UF}/distritos
GET /api/v1/localidades/municipios/{id}/distritos
```

### Mesorregiões e Microrregiões
```
GET /api/v1/localidades/mesorregioes
GET /api/v1/localidades/mesorregioes/{id}
GET /api/v1/localidades/estados/{UF}/mesorregioes
GET /api/v1/localidades/microrregioes
GET /api/v1/localidades/microrregioes/{id}
GET /api/v1/localidades/estados/{UF}/microrregioes
GET /api/v1/localidades/mesorregioes/{id}/microrregioes
```

### Regiões Geográficas (Imediatas e Intermediárias)
```
GET /api/v1/localidades/regioes-imediatas
GET /api/v1/localidades/regioes-imediatas/{id}
GET /api/v1/localidades/estados/{UF}/regioes-imediatas
GET /api/v1/localidades/regioes-intermediarias
GET /api/v1/localidades/regioes-intermediarias/{id}
GET /api/v1/localidades/estados/{UF}/regioes-intermediarias
GET /api/v1/localidades/regioes-intermediarias/{id}/regioes-imediatas
```

### Regiões Metropolitanas
```
GET /api/v1/localidades/regioes-metropolitanas
GET /api/v1/localidades/regioes-metropolitanas/{id}
GET /api/v1/localidades/estados/{UF}/regioes-metropolitanas
```

### Regiões Integradas de Desenvolvimento (RIDE)
```
GET /api/v1/localidades/regioes-integradas-de-desenvolvimento
GET /api/v1/localidades/regioes-integradas-de-desenvolvimento/{id}
```

### Subdistritos
```
GET /api/v1/localidades/subdistritos
GET /api/v1/localidades/subdistritos/{id}
GET /api/v1/localidades/estados/{UF}/subdistritos
GET /api/v1/localidades/municipios/{id}/subdistritos
```

### Aglomerações Urbanas
```
GET /api/v1/localidades/aglomeracoes-urbanas
GET /api/v1/localidades/aglomeracoes-urbanas/{id}
```

### Países
```
GET /api/v1/localidades/paises
GET /api/v1/localidades/paises/{pais}       # código ISO ALPHA-2 (BR, US, etc.)
```

## Parâmetros Comuns
- `orderBy` — campo para ordenação (ex: `nome`)
- `view` — nível de detalhamento
- `lang` — idioma (apenas para países: `pt`, `en`, `es`)

## Exemplos

### Listar todos os estados
```bash
curl "https://servicodados.ibge.gov.br/api/v1/localidades/estados"
```

### Municípios de São Paulo
```bash
curl "https://servicodados.ibge.gov.br/api/v1/localidades/estados/SP/municipios"
```

### Detalhes do município de São Paulo
```bash
curl "https://servicodados.ibge.gov.br/api/v1/localidades/municipios/3550308"
```

### Regiões imediatas de MG
```bash
curl "https://servicodados.ibge.gov.br/api/v1/localidades/estados/MG/regioes-imediatas"
```

### Países da América do Sul (usando M49)
```bash
curl "https://servicodados.ibge.gov.br/api/v1/localidades/paises?lang=pt"
```

## Notas
- Códigos IBGE: Região=1 dígito, UF=2 dígitos, Município=7 dígitos, Distrito=9 dígitos
- Siglas de UF podem ser usadas em vez de códigos numéricos
- As regiões imediatas/intermediárias substituem microrregiões/mesorregiões desde 2023
- Países seguem metodologia M49 da ONU
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/localidades
