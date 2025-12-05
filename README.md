
# Magic Formula — Implementação em Python (Joel Greenblatt)

> **Descrição rápida:**
> Repositório com uma implementação da *Magic Formula* de Joel Greenblatt para ranquear ações com base em **Earnings Yield** e **Return on Capital**. Este README explica como o código funciona, como executar.

---

## Índice

- [Sobre](#sobre)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Como a fórmula funciona](#como-a-fórmula-funciona)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Exemplo de saída / tabelas (placeholder para imagens)](#exemplo-de-saída--tabelas-placeholder-para-imagens)
- [Boas práticas e limitações](#boas-práticas-e-limitações)
- [Contribuição](#contribuição)


---

## Sobre

Esta implementação utiliza dados financeiros (demonstrativos e preços) para calcular os dois indicadores centrais da *Magic Formula* de Joel Greenblatt:

1. **Earnings Yield** — uma medida de quanto lucro operacional a empresa gera em relação ao seu *Enterprise Value*.
2. **Return on Capital (ROIC)** — uma medida de quão eficientemente a empresa converte capital investido em lucro operacional.

O objetivo é gerar um ranking combinado que permita selecionar as ações "top N" segundo estes critérios.

---

## Pré-requisitos

- Python 3.8+
- Bibliotecas (exemplos): `pandas`, `numpy`

> Observação: adapte a lista de dependências ao que seu código efetivamente usa.

---

## Instalação

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/seu-repo.git
cd seu-repo
```

2. Crie e ative um ambiente virtual (opcional, recomendado):

```bash
python -m venv .venv
source .venv/bin/activate  # linux / mac
.\.venv\Scripts\activate  # windows
```

3. Baixe um dataset confiável:
Usado o do investsite.



---

## Como a fórmula funciona (explicação técnica)

### Passo a passo geral

1. **Coleta de dados**
   - Buscar demonstrações financeiras (mínimo: EBIT/operating income, ativos, passivos correntes, imobilizado, caixa, dívida) e preços de mercado (market cap ou preço * número de ações).

2. **Calcular Enterprise Value (EV)**
   - EV = Market Cap + Total Debt - Cash and Equivalents

3. **Calcular Earnings Yield (EY)**
   - EY = EBIT / EV
   - Nota: algumas variantes usam *Net income* ou *EBITDA* — aqui usamos **EBIT** (lucro operacional) por ser a fórmula clássica.

4. **Calcular Return on Capital (ROC)**
   - Uma implementação comum: ROC = EBIT / (Net Working Capital + Net Fixed Assets)
   - Onde *Net Working Capital* = Current Assets - Current Liabilities (ajuste conforme seu dataset) e *Net Fixed Assets* ≈ Property, Plant & Equipment (líquido).
   - Existem outras definições (ex.: Invested Capital, Total Assets - Current Liabilities). Escolha a que fizer sentido com os dados que você tem e documente no código.

5. **Rankings separadamente**
   - Rankear todas as empresas por `Earnings Yield` (maior EY recebe rank 1).
   - Rankear por `Return on Capital` (maior ROC recebe rank 1).

6. **Rank combinado**
   - Somar os ranks (Rank_EY + Rank_ROC) → `Combined Rank`.
   - Ordenar pelo `Combined Rank` crescente e escolher top N.

7. **Resultados**
   - Gerar tabela com colunas-chave.



## Exemplo de saída / tabelas (PLACEHOLDERS PARA IMAGENS)

> Coloque suas imagens na pasta `images/` do repositório e referencie aqui.

**Tabela Inicial:**

`![Tabela de rankings](images/tabela_rankings.png)`



**Tabela Após Transformação:**

`![Gráfico de backtest](images/chart_backtest.png)`



---

## Boas práticas e limitações

- **Não é recomendação de investimento.** Use como ferramenta de pesquisa e realize backtests robustos antes de considerar alocação real.
- **Viés de sobrevivência:** garanta que seu conjunto de dados trate empresas que saíram do mercado durante o período de análise.
- **Custos de transação / impostos:** inclua custos na simulação de performance real.
- **Risco de curto prazo:** a estratégia costuma funcionar no médio/longo prazo conforme a hipótese do autor, mas há períodos de baixo desempenho.

---

## Contribuição

Contribuições são bem-vindas!

1. Fork o projeto
2. Crie uma branch com sua feature (`git checkout -b feature/nome`)
3. Abra um Pull Request descrevendo a mudança

---


