# Machine Learning Project – Prédiction de performance en courses hippiques

## Objectif

L'objectif de ce projet est de prédire si un cheval termine dans le top 3 d'une course à partir de données historiques.

Ce projet respecte les contraintes suivantes :

* Dataset supérieur à 4000 observations
* Problème de classification
* Comparaison de plusieurs modèles
* Interprétation globale et locale

---

## Dataset

Le dataset est trop volumineux pour être stocké sur GitHub.

Téléchargement :
https://drive.google.com/file/d/1dNkYE4WfnNfQoGLvFmnWlKXSm8-scKE-/view?usp=sharing 

### Instructions

1. Télécharger le fichier
2. Le placer dans le dossier `data/`
3. Nom attendu : `raceform.db`

---

## Installation

### Prérequis

* Python 3.11.14
* UV package manager

### Installation des dépendances

```
uv sync
```

---

## Exécution

Lancer le notebook :

```
notebooks/projet_ml_courses_hippiques.ipynb
```

Le dataset doit être placé dans :

```
data/raceform.db
```

---

## Modélisation

Les modèles suivants ont été testés :

* Régression logistique
* SVM
* Random Forest
* XGBoost
* KNN
* MLP
* Bagging

---

## Modèle retenu

Random Forest

Justification :

* Bon équilibre biais/variance
* Performance stable
* Interprétabilité

---

## Évaluation

Les modèles sont comparés avec :

* Accuracy
* Precision
* Recall
* F1-score
* ROC-AUC

---

## Interprétabilité

### Globale

* Feature importance
* Permutation importance
* SHAP
* PDP
* ALE

### Locale

* SHAP (explication individuelle)

---

## Structure du projet

```
.
├── notebooks/
│   └── projet_ml_courses_hippiques.ipynb
├── data/
│   └── README.md
├── pyproject.toml
├── uv.lock
├── BEST_MODEL.md
├── README.md
```

---

## Reproductibilité

Le projet est reproductible grâce à :

* pyproject.toml
* uv.lock
* dataset accessible via lien externe

---

## Auteur

Projet réalisé dans le cadre d’un cours de machine learning.
