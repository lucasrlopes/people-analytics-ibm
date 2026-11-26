# People Analytics: o que explica o turnover

Análise em Python dos 1.470 funcionários da base IBM HR Analytics, para entender quem sai da empresa e por quê. A base é fictícia, criada por cientistas de dados da IBM, e é muito usada em estudos de RH.

## Resumo

- **Hora extra é o sinal mais forte:** quem faz hora extra sai quase 3 vezes mais (30,5% contra 10,4%).
- **Salário baixo + hora extra é a combinação crítica:** nesse grupo, 58,5% saíram, mais de 3,5 vezes a média da empresa (16,1%).
- **O risco está no começo:** 34,9% de turnover no primeiro ano de casa, contra 8,1% depois de 10 anos.
- **Os padrões são reais, não acaso:** os testes estatísticos confirmam salário, hora extra, tempo de casa e idade (p < 0,001). Gênero não faz diferença.

## Perguntas de negócio

1. Qual é o turnover geral e onde ele se concentra (área, cargo)?
2. Quem sai ganha menos? Faz mais hora extra?
3. Em que momento da carreira na empresa o risco é maior?
4. As diferenças encontradas são estatisticamente significativas ou podem ser obra do acaso?

## Principais achados

**Definição:** turnover = % de funcionários com `Attrition = Yes`. São 237 saídas em 1.470 funcionários (16,1%).

- **Cargo pesa mais que área:** por área, o turnover vai de 13,8% (Pesquisa e Desenvolvimento) a 20,6% (Vendas). Por cargo, a distância é muito maior: 39,8% entre os representantes de vendas (Sales Representative) e 2,5% entre os diretores de pesquisa (Research Director). Técnicos de laboratório (23,9%) e RH (23,1%) também ficam bem acima da média.
- **Salário:** quem saiu tinha salário mensal mediano de 3.202, contra 5.204 de quem ficou. O quarto da empresa que ganha menos (até 2.911 por mês) tem 29,3% de turnover; os outros três quartos ficam entre 10% e 14%.
- **Hora extra:** 28% dos funcionários fazem hora extra, e o turnover deles é de 30,5%, contra 10,4% de quem não faz.
- **A combinação:** cruzando as duas coisas, quem faz hora extra e está no quarto de menor salário tem 58,5% de turnover (106 pessoas). Sem hora extra, o mesmo quarto salarial tem 17,5%. Com hora extra, mesmo o quarto de maior salário chega a 18,1%, acima da média.
- **Tempo de casa:** 34,9% de turnover até 1 ano de empresa, caindo para 8,1% depois de 10 anos. Quem saiu tinha mediana de 3 anos de casa (contra 6) e 32 anos de idade (contra 36).
- **Testes estatísticos:** para variáveis numéricas, como salário e tempo de casa, usei o teste de Mann-Whitney, que não exige que os dados sigam uma curva normal (o salário é bem assimétrico). Para categorias, como hora extra e cargo, usei o qui-quadrado, e o V de Cramér para medir a força da relação (de 0 a 1).

| Fator | Teste | Resultado | Força (V de Cramér) |
| --- | --- | --- | --- |
| Hora extra | Qui-quadrado | p < 0,001 | 0,24 |
| Cargo | Qui-quadrado | p < 0,001 | 0,24 |
| Estado civil | Qui-quadrado | p < 0,001 | 0,18 |
| Viagens a trabalho | Qui-quadrado | p < 0,001 | 0,13 |
| Área | Qui-quadrado | p = 0,005 | 0,09 |
| Gênero | Qui-quadrado | p = 0,291 (não significativo) | 0,03 |
| Salário mensal | Mann-Whitney | p < 0,001 | |
| Anos de casa | Mann-Whitney | p < 0,001 | |
| Idade | Mann-Whitney | p < 0,001 | |
| Distância de casa | Mann-Whitney | p = 0,002 | |

## O que eu recomendaria ao RH

1. **Olhar a hora extra recorrente como alerta de saída**, principalmente nos cargos de menor salário. É o grupo com 58,5% de turnover.
2. **Revisar a remuneração dos cargos com mais saídas** (representantes de vendas e técnicos de laboratório), comparando com o mercado.
3. **Reforçar o acompanhamento no primeiro ano** (onboarding, conversas de 30, 60 e 90 dias), quando o risco é 4 vezes maior que o de quem tem mais de 10 anos de casa.

Esses achados mostram associação, não causa: a hora extra pode levar à saída, mas também pode ser sinal de uma área sobrecarregada que já perde gente. O próximo passo é um modelo de previsão de turnover, que estima o risco de cada funcionário combinando todos os fatores.

## Notebooks

1. `01_exploracao.ipynb`: primeira leitura da base (1.470 linhas e 35 colunas, sem vazios nem duplicados) e remoção de 3 colunas constantes (`EmployeeCount`, `Over18` e `StandardHours`).
2. `02_eda.ipynb`: turnover por área, cargo, faixa salarial, hora extra e tempo de casa, com gráficos e o cruzamento de hora extra com salário.
3. `03_testes_estatisticos.ipynb`: testes de Mann-Whitney e qui-quadrado, V de Cramér e a tabela-resumo de todos os fatores.

## Dados

[IBM HR Analytics Employee Attrition & Performance](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) (Kaggle). O arquivo não fica neste repositório. Para reproduzir:

1. Baixe o CSV no link acima e coloque em `data/WA_Fn-UseC_-HR-Employee-Attrition.csv`.
2. Abra os notebooks na ordem numérica e rode todas as células (Python com pandas, matplotlib e scipy; o Anaconda já traz os três).

## Estrutura

```
people-analytics-ibm/
├── data/                          # CSV da base (fora do Git)
├── 01_exploracao.ipynb
├── 02_eda.ipynb
├── 03_testes_estatisticos.ipynb
└── README.md
```

## Ferramentas

Python (pandas, matplotlib, scipy) · Jupyter (VS Code) · Git/GitHub
