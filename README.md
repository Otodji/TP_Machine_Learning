# Apprentissage supervisé (M2)

Travaux pratiques du cours d'**apprentissage supervisé** du Master 2 Data Science, en Python avec
scikit-learn. Le notebook principal parcourt tout le programme du cours, de la règle de Bayes aux
méthodes d'ensemble, en passant par l'équité algorithmique, et l'applique à deux jeux de données réels.

## Contenu du dépôt

| Fichier | Description |
|---|---|
| [`TP_complet.ipynb`](TP_complet.ipynb) | **Notebook principal** : le TP complet, organisé par séance (11 parties, 48 figures) |
| [`TP2.ipynb`](TP2.ipynb) | TP 2 (en cours) : préparation de l'environnement de travail |
| [`utils.py`](utils.py) | Module de fonctions communes au cours et aux TP : chargement des données, figures `plot_*` |
| [`utils.ipynb`](utils.ipynb) | Version notebook de `utils.py`, pour lire le code section par section |
| [`data/`](data/) | Jeux de données utilisés dans les TP |
| [`requirements.txt`](requirements.txt) | Bibliothèques Python nécessaires |

## Programme du TP complet

| # | Partie | Notions abordées |
|---|---|---|
| 0 | Données | Exploration de SAheart et Adult : dimensions, statistiques descriptives, valeurs manquantes |
| 1 | Règle de Bayes et coûts asymétriques | Classifieur de Bayes, seuil de décision quand les erreurs n'ont pas le même coût |
| 2 | Sur-apprentissage et compromis biais-variance | Courbe en U de l'erreur, décomposition biais-variance |
| 3 | Découpage des données, validation croisée | Apprentissage / validation / test, k-fold, fléau de la dimension, Bayes naïf |
| 4 | Frontières de décision | Comparaison Bayes naïf, LDA et QDA sur SAheart (âge, tabac) |
| 5 | Loi normale multivariée, LDA, QDA | Covariance, distance de Mahalanobis, nombre de paramètres de LDA et de QDA |
| 6 | Méthodes locales | Fenêtres de Parzen, k plus proches voisins, standardisation, choix de k par validation croisée, effet des variables de bruit |
| 7 | Arbres de décision (CART) | Impuretés (Gini, entropie), partition récursive, élagage et choix de α, instabilité des arbres |
| 8 | Méthodes d'ensemble | Bagging, erreur out-of-bag, forêts aléatoires (choix de `mtry`), boosting |
| 9 | Équité algorithmique | Métriques par groupe (taux de sélection, TPR, FPR, VPP) sur Adult selon le sexe, théorème d'impossibilité |
| 10 | Validation temporelle | Découpage des données qui respecte l'ordre du temps |
| 11 | Évaluation | Matrice de confusion, métriques selon le seuil, courbes ROC et précision-rappel |

### Quelques résultats

- **k-PPV sur SAheart** (k = 15, validation croisée stratifiée à 5 plis, *balanced accuracy*) :
  0,599 sans standardisation, contre **0,633** après standardisation des variables.
- **Forêt aléatoire sur Adult** : le taux de sélection est de 6,8 % pour les femmes et de 22,8 %
  pour les hommes, alors que les taux de base sont de 10,6 % et 30,8 %. Le modèle reproduit,
  et même accentue, l'écart présent dans les données.

## Jeux de données

| Fichier | Taille | Variable cible | Description |
|---|---|---|---|
| `data/SAheart.csv` | 462 × 10 | `chd` (maladie coronarienne) | Hommes d'une région à haut risque cardiaque du Cap-Occidental (Afrique du Sud). Détails dans [`SAheart-info.txt`](data/SAheart-info.txt) |
| `data/adult.csv` | 10 000 × 13 | `income` (revenu > 50 000 $) | Extrait du recensement américain de 1994 (UCI *Census Income*) |

Ces données sont chargées par `utils.load_saheart()` / `utils.saheart_xy()` et
`utils.load_adult()` / `utils.adult_xy()`.

## Installation et utilisation

Il faut Python 3.10 ou une version plus récente.

```bash
git clone https://github.com/Otodji/apprentissage-supervise-m2.git
cd apprentissage-supervise-m2

python -m venv .venv
# Windows :
.venv\Scripts\activate
# macOS / Linux :
source .venv/bin/activate

pip install -r requirements.txt
jupyter notebook TP_complet.ipynb
```

Lance le notebook **depuis la racine du dépôt** : il importe `utils.py` et lit les fichiers du
dossier `data/` à partir de ce dossier. La graine aléatoire est fixée (`GRAINE = 42`), donc les
résultats sont reproductibles.

## Références

- Hastie, Tibshirani & Friedman, *The Elements of Statistical Learning*, Springer, 2009
- James, Witten, Hastie, Tibshirani & Taylor, *An Introduction to Statistical Learning*, Springer, 2023
- Bishop, *Pattern Recognition and Machine Learning*, Springer, 2006
- Murphy, *Probabilistic Machine Learning: An Introduction*, MIT Press, 2022

## Crédits

Le module `utils.py` (figures et fonctions utilitaires) est fourni dans le cadre du cours
d'apprentissage supervisé du M2. Les notebooks de TP ont été réalisés par
[OTODJI Théophile](https://github.com/Otodji).
