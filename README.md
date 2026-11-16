# bcb-dashboard

Dashboard web de indicadores financeiros (Dólar, Selic, IPCA), com dados do
[pipeline automatizado](https://github.com/brendacaarmo/bcb-financial-pipeline),
atualizados todos os dias, lidos via API REST do Supabase. No topo da página,
um **resumo do dia escrito por IA**, com os números verificados pelo pipeline.

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
   diariamente via GitHub Actions, grava os dados no PostgreSQL do Supabase e
   gera o resumo do dia com IA (Gemini).
2. Este dashboard consulta as tabelas `indicadores` e `resumos_diarios` via API
   REST pública, protegidas por uma política de leitura (Row Level Security) que
   só permite `SELECT`.
3. Os dados são renderizados em cartões de KPI e gráficos interativos.

## Resumo do dia (IA)

O cartão no topo mostra o resumo mais recente da tabela `resumos_diarios`:

- O selo indica a origem do texto: **"Escrito por IA · números verificados"** ou
  **"Gerado por regras (sem IA)"**, quando o pipeline usou o plano B.
- Abaixo do texto aparecem a data de geração, a data mais recente dos dados e o
  modelo usado.
- O texto é inserido na página com `textContent`, então nunca é interpretado como
  HTML.
- Se a tabela estiver vazia ou a consulta falhar, o cartão simplesmente não
  aparece e o resto do dashboard continua funcionando.

Como o resumo é escrito e verificado é explicado no
[repositório do pipeline](https://github.com/brendacaarmo/bcb-financial-pipeline/blob/main/docs/llm_summary.md).

## Rodando localmente

```bash
git clone https://github.com/brendacaarmo/bcb-dashboard.git
cd bcb-dashboard
python3 -m http.server 8000
# abra http://localhost:8000
```

## Autora

Brenda Carmo — [LinkedIn](https://www.linkedin.com/in/brenda-carmo-151b12208/) · [Portfólio](https://brendacaarmo.github.io/)
