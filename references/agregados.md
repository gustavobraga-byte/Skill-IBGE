# API de Agregados (SIDRA) — v3

Base URL: `https://servicodados.ibge.gov.br/api/v3/agregados`

## Endpoints

### Listar agregados
```
GET /api/v3/agregados
```
Parâmetros opcionais: `periodo`, `assunto`, `classificacao`, `periodicidade`, `nivel`

### Metadados de um agregado
```
GET /api/v3/agregados/{agregado}/metadados
```

### Localidades por agregado
```
GET /api/v3/agregados/{agregado}/localidades/{nivel}
```

### Períodos por agregado
```
GET /api/v3/agregados/{agregado}/periodos
```

### Dados (com períodos específicos)
```
GET /api/v3/agregados/{agregado}/periodos/{periodos}/variaveis/{variavel}
```
Parâmetros: `localidades` (obrigatório), `classificacao`, `view`

### Dados (últimos 6 períodos)
```
GET /api/v3/agregados/{agregado}/variaveis/{variavel}
```
Parâmetros: `localidades` (obrigatório), `classificacao`, `view`

## Exemplos

### Listar todos agregados
```bash
curl "https://servicodados.ibge.gov.br/api/v3/agregados"
```

### Metadados da tabela 6579 (estimativas populacionais)
```bash
curl "https://servicodados.ibge.gov.br/api/v3/agregados/6579/metadados"
```

### Dados: População por UF em 2023 (tabela 6579)
```bash
curl "https://servicodados.ibge.gov.br/api/v3/agregados/6579/periodos/2023/variaveis/9324?localidades=N3[all]"
```

### Dados: PIB por estado (últimos 6 períodos, tabela 5938)
```bash
curl "https://servicodados.ibge.gov.br/api/v3/agregados/5938/variaveis/XXXX?localidades=N3[all]"
```

### Dados com classificação (ex: sexo, tabela censitária)
```bash
curl "https://servicodados.ibge.gov.br/api/v3/agregados/{agregado}/periodos/{periodos}/variaveis/{variavel}?localidades=N3[all]&classificacao=2[6794]"
```

### View flat (tabela plana)
```bash
curl "https://servicodados.ibge.gov.br/api/v3/agregados/{agregado}/periodos/{periodos}/variaveis/{variavel}?localidades=N3[all]&view=flat"
```

## Parâmetro view
- Omitido (padrão): hierárquico agrupado
- `flat`: tabela plana
- `olap`: formato OLAP

## Notas
- `{agregado}` = código numérico da tabela SIDRA (ex: 6579)
- `{periodos}` = `all` ou lista separada por `|` (ex: `2020|2021|2022`)
- `{variavel}` = `all` ou lista separada por `|` (ex: `63|69`)
- `localidades` = formato `N{nivel}[lista]` (ex: `N3[all]`, `N3[35,33]`, `N6[3550308]`)
- `classificacao` = formato `{id_class}[{id_cat}]` (ex: `2[6794]`)
- Sem autenticação necessária
- Documentação oficial: https://servicodados.ibge.gov.br/api/docs/agregados?versao=3
