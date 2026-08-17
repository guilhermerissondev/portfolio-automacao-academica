# Portfolio — Automação de Processos Acadêmicos

Conjunto de notebooks Python extraídos de um projeto real de automação de auditoria
acadêmica (conferência de matrículas, carga horária, planejado x executado e geração
de relatórios executivos), reescritos aqui em versão **anonimizada** para fins de
portfolio.

## ⚠️ Sobre os dados

Os notebooks originais rodavam sobre planilhas reais de uma instituição de ensino
(matrículas, professores, cronogramas). Para esta publicação:

- **Nomes de instituições, sistemas e pessoas** foram substituídos por termos genéricos.
- **Todos os outputs de execução** (tabelas, gráficos, prints) foram removidos, pois
  continham dados reais de alunos e professores.
- Um payload de ~590 KB com uma base de alunos embutida em base64/gzip foi **removido
  por completo** de um dos notebooks.
- A lógica de negócio, estrutura do código e comentários foram preservados como
  estavam em produção — é o que se pretende demonstrar aqui.

Nenhum dado real de aluno, professor ou instituição está presente neste repositório.
Para rodar os notebooks é necessário fornecer suas próprias planilhas de entrada
(veja os parâmetros no início de cada um) ou usar o notebook `06_simulador_base_alunos`
para gerar uma base sintética de teste.

## O que cada notebook faz

| # | Notebook | Descrição |
|---|----------|-----------|
| 1 | [`01_consolidacao_base_matriculas.ipynb`](notebooks/01_consolidacao_base_matriculas.ipynb) | Consolida planilhas de fluxo, mapa pedagógico e registro de professores em uma base única calibrada, com auditoria de duplicatas e diagnóstico de qualidade. |
| 2 | [`02_auditoria_praticas_profissionais.ipynb`](notebooks/02_auditoria_praticas_profissionais.ipynb) | Reescrita em Python/pandas de um modelo originalmente feito em Power Query, para auditar carga horária x alunos em bases com milhões de linhas. |
| 3 | [`03_inteligencia_estatistica_academica.ipynb`](notebooks/03_inteligencia_estatistica_academica.ipynb) | Gera indicadores estatísticos e um dashboard executivo em PDF a partir da base consolidada de auditoria pedagógica. |
| 4 | [`04_auditoria_pedagogica_principal.ipynb`](notebooks/04_auditoria_pedagogica_principal.ipynb) | Cruza o planejado (mapa pedagógico) com o executado (registro de professores), aponta divergências e gera relatório executivo. |
| 5 | [`05_rateio_sinergia_alunos.ipynb`](notebooks/05_rateio_sinergia_alunos.ipynb) | Notebook complementar: rateia carga horária e alunos entre cursos que compartilham a mesma turma/aula (sinergia). |
| 6 | [`06_simulador_base_alunos.ipynb`](notebooks/06_simulador_base_alunos.ipynb) | Gera uma base de alunos sintética para testar e demonstrar os notebooks acima sem depender de dados reais. |

Os notebooks 1, 4 e 5 formam um pipeline (consolidação → auditoria principal →
rateio de sinergia); o 2 e o 3 são análises complementares/independentes; o 6 é um
gerador de dados sintéticos para quem quiser experimentar sem planilhas próprias.

## Stack técnica

- **Dados:** pandas, numpy, duckdb, pandera (validação de schema)
- **Excel/Relatórios:** openpyxl, xlsxwriter, reportlab
- **Visualização:** matplotlib, seaborn, plotly
- **Modelagem (notebook de inteligência estatística):** scikit-learn, lightgbm, optuna, mlflow

## Como usar

```bash
python -m venv .venv
.venv\Scripts\activate   # Windows
pip install -r requirements.txt
jupyter lab
```

Cada notebook documenta, em suas primeiras células, quais arquivos de entrada espera
e quais parâmetros podem ser ajustados. Não há dependência de serviços externos ou
credenciais — tudo roda localmente sobre arquivos `.xlsx`/`.csv`.

## Licença

Código disponibilizado sob a licença MIT (veja [LICENSE](LICENSE)). Os dados de
entrada/saída **não** fazem parte deste repositório.
