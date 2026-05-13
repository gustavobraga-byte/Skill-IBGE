# API Países — v1

Base URL: `https://servicodados.ibge.gov.br/api/v1/paises`

## Endpoints

### Listar países
```
GET /api/v1/paises/{paises}
```
Parâmetros: `lang` (`pt`, `en`, `es`)

### Indicadores disponíveis
```
GET /api/v1/paises/indicadores/{indicadores}
```

### Indicadores por país
```
GET /api/v1/paises/{paises}/indicadores/{indicadores}
```
Parâmetros: `periodo`

## Identificadores
- **Países**: ISO 3166-1 ALPHA-2 (2 letras) — ex: `BR`, `US`, `AR`, `PT`
- **Múltiplos países**: separar por `|` — ex: `BR|AR|US`

## Códigos de Indicadores

### Economia
| Código | Indicador |
|--------|-----------|
| 77818 | Chegada de turistas |
| 77819 | Gastos públicos com educação |
| 77820 | Gastos públicos com saúde |
| 77821 | Investimentos em P&D |
| 77822 | Mulheres economicamente ativas (15+) |
| 77823 | PIB per capita |
| 77824 | População economicamente ativa (15+) |
| 77825 | Total de exportações |
| 77826 | Total de importações |
| 77827 | Total do PIB |

### Indicadores Sociais
| Código | Indicador |
|--------|-----------|
| 77830 | Expectativa de vida ao nascer |
| 77831 | Índice de Desenvolvimento Humano (IDH) |
| 77832 | População com acesso à água potável |
| 77833 | População com acesso à rede sanitária |
| 77835 | Taxa bruta de matrículas |
| 77836 | Taxa de alfabetização (15+) |

### Meio Ambiente
| Código | Indicador |
|--------|-----------|
| 77838 | Áreas cultivadas |
| 77839 | Áreas de pastagens permanentes |
| 77840 | Áreas protegidas |
| 77841 | Produção de gás natural |
| 77842 | Produção de petróleo |

### População
| Código | Indicador |
|--------|-----------|
| 77844 | Densidade demográfica |
| 77845 | Homens |
| 77846 | Mulheres |
| 77847 | População rural |
| 77848 | População urbana |
| 77849 | População total |
| 77850 | Taxa bruta de mortalidade |
| 77851 | Taxa bruta de natalidade |
| 77852 | Taxa média de crescimento populacional |

### Redes
| Código | Indicador |
|--------|-----------|
| 77854 | Assinaturas de telefonia celular |
| 77855 | Assinaturas de telefonia fixa |
| 77857 | Indivíduos com acesso à internet |

### Saúde
| Código | Indicador |
|--------|-----------|
| 77829 | Consumo calórico |
| 77834 | Incidência de subnutrição |

## Exemplos

### Perfil do Brasil
```bash
curl "https://servicodados.ibge.gov.br/api/v1/paises/BR"
```

### Perfil do Brasil em inglês
```bash
curl "https://servicodados.ibge.gov.br/api/v1/paises/BR?lang=en"
```

### IDH e PIB per capita do Brasil
```bash
curl "https://servicodados.ibge.gov.br/api/v1/paises/BR/indicadores/77831|77823"
```

### Comparar população de Brasil, Argentina e EUA
```bash
curl "https://servicodados.ibge.gov.br/api/v1/paises/BR|AR|US/indicadores/77849"
```

### Listar todos indicadores disponíveis
```bash
curl "https://servicodados.ibge.gov.br/api/v1/paises/indicadores/77849|77823|77831"
```

## Notas
- Países organizados conforme metodologia M49 da ONU
- Sem autenticação
- Documentação: https://servicodados.ibge.gov.br/api/docs/paises
