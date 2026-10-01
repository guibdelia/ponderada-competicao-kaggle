# Brasileirão: probabilidades de resultado (A / D / H)

Projeto acadêmico de modelagem probabilística (LogLoss multiclasse) para o Campeonato Brasileiro Série A.

## Conteúdo

- `notebook_submissoes.ipynb`: notebook único, executável do início ao fim, que gera todas as submissões e o `experimentos.csv`.
- `submissions/`: CSVs enviados ao Kaggle (`Id,A,D,H`).
- `experimentos.csv`: registro de cada versão (features, modelo, parâmetros, LogLoss por fold, decisão, CSV).
- `data/`: `train.csv`, `test.csv`, `sample_submission.csv` (não alterados).

## Submissões

| Versão | Arquivo | Modelo | LogLoss (validação temporal) |
|---|---|---|---|
| v01 | `submission_28_09.csv` | Logística, 17 variáveis, C=1 | 1.0337 |
| v02 | `submission_29_09.csv` | Logística, 17 variáveis, C=0.003 | 1.0273 |
| v03 | `submission2_29_09.csv` | Logística, `elo_diff`, C=0.1 | 1.0228 |
| v04 | `submission3_29_09.csv` | + `venue_form_diff`, `form_pts_away`, C=0.03 | 1.0222 |
| v05 | `submission_30_09.csv` | + `Home`/`Away` one-hot, C=0.01 | 1.0218 |
| final | `submission2_30_09.csv` | Blend 0,5·v04 + 0,5·v05 | 1.0218 |

Validação *walk-forward* por temporada (folds 2016–2021), média ponderada.

## Como reproduzir

Requer Python com `numpy`, `pandas`, `scikit-learn`, `matplotlib` e `jupyter`. Na raiz do repositório:

```bash
jupyter nbconvert --to notebook --execute --inplace notebook_submissoes.ipynb
```

A execução regenera os CSVs de `submissions/` com conteúdo idêntico aos versionados.

## Regras

Sem dados externos, sem odds no pipeline (existem só no treino), sem uso de outras linhas do teste; imputação, escala e codificação ajustadas apenas no treino de cada fold.
