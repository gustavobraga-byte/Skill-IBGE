# API Notícias — v3

Base URL: `https://servicodados.ibge.gov.br/api/v3/noticias`

## Endpoint Único

```
GET /api/v3/noticias
```

## Parâmetros

| Parâmetro | Descrição | Exemplo |
|-----------|-----------|---------|
| `tipo` | Tipo de publicação | `release` ou `noticia` |
| `qtd` | Quantidade por página | `10` (padrão), `50`, `100` |
| `page` | Número da página | `1` (padrão) |
| `de` | Data inicial | `01-01-2024` |
| `ate` | Data final | `31-12-2024` |
| `introsize` | Tamanho da introdução | `200` (caracteres) |
| `destaque` | Apenas destaques | `true` ou `false` |
| `busca` | Termo de busca | `censo`, `ipca`, `inflação` |
| `idproduto` | ID do produto associado | |

## Exemplos

### Últimas 10 notícias
```bash
curl "https://servicodados.ibge.gov.br/api/v3/noticias/"
```

### Últimas notícias sobre o Censo
```bash
curl "https://servicodados.ibge.gov.br/api/v3/noticias/?busca=censo"
```

### Releases de 2024
```bash
curl "https://servicodados.ibge.gov.br/api/v3/noticias/?tipo=release&de=01-01-2024&ate=31-12-2024"
```

### Notícias em destaque sobre IPCA
```bash
curl "https://servicodados.ibge.gov.br/api/v3/noticias/?busca=IPCA&destaque=true&qtd=5"
```

## Notas
- Retorna objeto com paginação (`items`, `count`, `page`, `totalPages`, `nextPage`, `previousPage`)
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/noticias?versao=3
