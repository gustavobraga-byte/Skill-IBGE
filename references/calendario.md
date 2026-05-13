# API Calendário — v3

Base URL: `https://servicodados.ibge.gov.br/api/v3/calendario`

## Endpoint

```
GET /api/v3/calendario
```

## Parâmetros

| Parâmetro | Descrição | Exemplo |
|-----------|-----------|---------|
| `de` | Data inicial | `01-01-2024` |
| `ate` | Data final | `31-12-2024` |
| `produto` | Produto/pesquisa | `IPCA`, `PNAD`, `PIB`, `Censo` |
| `tipo` | Tipo de evento | `divulgacao` (publicação), `coleta` (pesquisa de campo), `todos` |
| `page` | Página | `1` (padrão) |
| `qtd` | Quantidade | `20` (padrão) |

## Exemplos

### Próximas divulgações
```bash
curl "https://servicodados.ibge.gov.br/api/v3/calendario"
```

### Divulgações do IPCA em 2024
```bash
curl "https://servicodados.ibge.gov.br/api/v3/calendario?produto=IPCA&de=01-01-2024&ate=31-12-2024"
```

### Coletas de campo do PNAD
```bash
curl "https://servicodados.ibge.gov.br/api/v3/calendario?tipo=coleta&produto=PNAD"
```

## Notas
- Consulta o cronograma oficial de divulgações do IBGE
- Inclui tanto divulgações de resultados quanto períodos de coleta
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/calendario?versao=3
