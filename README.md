# Web Traffic Time Series Forecasting

🇫🇷 [Version française](#version-française) · 🇬🇧 [English version](#english-version)

---

## Version française

J'ai participé à cette compétition Kaggle pour m'entraîner sur les séries temporelles (elle a 9 ans quand j'écris ce readme) : https://www.kaggle.com/competitions/web-traffic-time-series-forecasting

L'objectif : prédire 64 jours de trafic sur ~145 000 pages Wikipédia. La métrique est le SMAPE (plus c'est bas, mieux c'est). Je voulais explorer plusieurs approches par curiosité et apprentissage.

### Résultats

| Approche | Fichier | Score SMAPE | État |
| --- | --- | --- | --- |
| LSTM | `le-traffic-web-lstm-w.ipynb` | **43.84** | Soumis |
| XGBoost | `le-traffic-web-xgboost.ipynb` | ~45.9 | Non soumis, évaluation locale sur 50 pages |
| LSTM (optimisation mémoire) | `le-traffic-web-lstm-dk.ipynb` | — | Ne fonctionne pas |

Pour situer : les meilleures solutions tournaient autour de 35-38, et une simple médiane par page se situe autour de 44-45. Mon 43.84 est donc au niveau d'une baseline. Je le laisse tel quel plutôt que d'annoncer un chiffre que je n'ai pas obtenu.

### 1. XGBoost

On m'avait conseillé ce modèle, réputé comme l'un des plus performants. Je n'ai pas soumis les prédictions sur Kaggle, donc il n'a pas de score officiel : je me suis évalué moi-même en entraînant chaque page sur son historique privé des 64 derniers jours, puis en comparant la prédiction de ces 64 jours aux valeurs réelles. **SMAPE moyen d'environ 45.9** sur 50 pages.

Deux réserves sur ce chiffre : c'est un simple holdout et non une validation croisée, et les 50 pages sont les premières lignes du fichier plutôt qu'un tirage aléatoire, donc il est indicatif. Il n'est pas non plus directement comparable au 43.84 du LSTM, qui vient du leaderboard Kaggle sur l'ensemble du jeu de test.

### 2. Réseau de neurones

Deux fichiers correspondent à cette approche :

- **`_w`** : version fonctionnelle, score de 43.84017 sur la compétition.
- **`_dk`** : tentative d'amélioration qui ne fonctionne pas. Deux problèmes non résolus à ce jour :
  - **Mémoire** : le code construit tout le jeu de données fenêtré en mémoire d'un coup, ce qui dépasse la RAM autorisée par Kaggle. J'ai tenté de réduire l'empreinte mémoire sans succès. Le vrai correctif est probablement de générer les batches à la volée plutôt que de tout charger.
  - **Dimensions** : une erreur de dimensions des tableaux empêche l'exécution. Je n'ai pas encore isolé la cause.

Je préfère documenter ces échecs plutôt que de supprimer le fichier.

---

## English version

I entered this Kaggle competition to practice time series forecasting (it was 9 years old when I wrote this readme): https://www.kaggle.com/competitions/web-traffic-time-series-forecasting

The goal: forecast 64 days of traffic for ~145,000 Wikipedia pages. The metric is SMAPE (lower is better). I wanted to explore several approaches out of curiosity and to learn.

### Results

| Approach | File | SMAPE score | Status |
| --- | --- | --- | --- |
| LSTM | `le-traffic-web-lstm-w.ipynb` | **43.84** | Submitted |
| XGBoost | `le-traffic-web-xgboost.ipynb` | ~45.9 | Not submitted, local evaluation on 50 pages |
| LSTM (memory optimisation) | `le-traffic-web-lstm-dk.ipynb` | — | Does not run |

For context: top solutions scored around 35-38, and a simple per-page median lands around 44-45. So my 43.84 is at baseline level. I am leaving it as measured rather than claiming a number I did not obtain.

### 1. XGBoost

This model was recommended to me as one of the strongest available. I never submitted the predictions to Kaggle, so it has no official score: I evaluated it myself by training each page on its history minus the last 64 days, then comparing the forecast for those 64 days against the actual values. **Mean SMAPE of roughly 45.9** across 50 pages.

Two caveats on that number: it is a plain holdout rather than cross-validation, and the 50 pages are the first rows of the file rather than a random draw, so it is indicative only. It is also not directly comparable to the LSTM's 43.84, which comes from the Kaggle leaderboard on the full test set.

### 2. Neural network

Two files correspond to this approach:

- **`_w`**: working version, scored 43.84017 on the competition.
- **`_dk`**: an improvement attempt that does not run. Two issues remain unresolved:
  - **Memory**: the code builds the entire windowed dataset in memory at once, which exceeds the RAM allowed by Kaggle. I tried to reduce the footprint without success. The real fix is likely to generate batches on the fly instead of loading everything.
  - **Dimensions**: an array shape error prevents execution. I have not isolated the cause yet.

I would rather document these failures than delete the file.

---

MIT License · [maaabz](https://github.com/maaabz)
