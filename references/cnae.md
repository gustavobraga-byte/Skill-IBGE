# API CNAE — Classificação Nacional de Atividades Econômicas — v2

Base URL: `https://servicodados.ibge.gov.br/api/v2/cnae`

## Hierarquia (5 níveis)

1. **Seção** (letra A-U): 21 categorias
2. **Divisão** (2 dígitos): 87
3. **Grupo** (3 dígitos): 285
4. **Classe** (4-5 dígitos): 673
5. **Subclasse** (7 dígitos): ~1300 (uso administrativo)

Exemplo:
```
Seção J → Divisão 62 → Grupo 62.0 → Classe 6201-5 → Subclasse 6201-5/01
```

## Endpoints

### Seções
```
GET /api/v2/cnae/secoes
GET /api/v2/cnae/secoes/{secao}              # ex: A, B, C... J...
```

### Divisões
```
GET /api/v2/cnae/divisoes
GET /api/v2/cnae/divisoes/{divisao}          # ex: 01, 62, 85
GET /api/v2/cnae/secoes/{secao}/divisoes
```

### Grupos
```
GET /api/v2/cnae/grupos
GET /api/v2/cnae/grupos/{grupo}              # ex: 01.1, 62.0
GET /api/v2/cnae/divisoes/{divisao}/grupos
GET /api/v2/cnae/secoes/{secao}/grupos
```

### Classes
```
GET /api/v2/cnae/classes
GET /api/v2/cnae/classes/{classe}            # ex: 0111-3, 6201-5
GET /api/v2/cnae/divisoes/{divisao}/classes
GET /api/v2/cnae/grupos/{grupo}/classes
GET /api/v2/cnae/secoes/{secao}/classes
```

### Subclasses
```
GET /api/v2/cnae/subclasses
GET /api/v2/cnae/subclasses/{subclasse}       # ex: 0111-3/01, 6201-5/01
GET /api/v2/cnae/classes/{classe}/subclasses
GET /api/v2/cnae/divisoes/{divisao}/subclasses
GET /api/v2/cnae/grupos/{grupo}/subclasses
GET /api/v2/cnae/secoes/{secao}/subclasses
```

## Exemplos

### Listar seções (A-U)
```bash
curl "https://servicodados.ibge.gov.br/api/v2/cnae/secoes"
```

### Seção J (Informação e Comunicação)
```bash
curl "https://servicodados.ibge.gov.br/api/v2/cnae/secoes/J"
```

### Divisões da seção J
```bash
curl "https://servicodados.ibge.gov.br/api/v2/cnae/secoes/J/divisoes"
```

### Classe de desenvolvimento de software
```bash
curl "https://servicodados.ibge.gov.br/api/v2/cnae/classes/6201-5"
```

### Subclasses de desenvolvimento de software
```bash
curl "https://servicodados.ibge.gov.br/api/v2/cnae/classes/6201-5/subclasses"
```

## Notas
- Subclasses: versão 2.2 (descontinuada desde 01/01/2019, migrada para 2.3)
- Demais níveis: versão 2.0 (revisão 2007)
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/CNAE?versao=2
