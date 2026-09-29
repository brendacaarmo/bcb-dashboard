# bcb-dashboard

Dashboard web de indicadores financeiros (Dólar, Selic, IPCA), consumindo
dados em tempo real do [pipeline automatizado](https://github.com/brendacaarmo/bcb-financial-pipeline)
via API REST do Supabase.

🔗 **Acesse:** [brendacaarmo.github.io/bcb-dashboard](https://brendacaarmo.github.io/bcb-dashboard)

## Sobre

Site estático de página única, sem build, sem framework. Consome a API REST
automática do Supabase (PostgREST) diretamente do navegador, usando a chave
pública `anon`, e desenha os gráficos com Chart.js.

## Stack

- HTML5, CSS3, JavaScript (vanilla)
- [Chart.js](https://www.chartjs.org/) via CDN
- API REST do Supabase (PostgREST)
- Hospedagem: GitHub Pages

## Como funciona

1. O [pipeline](https://github.com/brendacaarmo/bcb-financial-pipeline) roda
   diariamente via GitHub Actions e grava os dados no PostgreSQL do Supabase.
2. Este dashboard consulta a tabela `indicadores` via API REST pública,
   protegida por uma política de leitura (Row Level Security) que só permite
   `SELECT`.
3. Os dados são renderizados em cartões de KPI e gráficos interativos.

## Rodando localmente

```bash
git clone https://github.com/brendacaarmo/bcb-dashboard.git
cd bcb-dashboard
python3 -m http.server 8000
# abra http://localhost:8000
```

## Autora

Brenda Carmo — [LinkedIn](https://www.linkedin.com/in/brenda-carmo-151b12208/) · [Portfólio](https://brendacaarmo.github.io)
