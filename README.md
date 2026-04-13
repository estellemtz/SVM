# Projet de Machine Learning : Prédiction du Top 3 en courses hippiques

## Objectif du projet

Ce projet vise à prédire si un cheval termine dans le **top 3 d’une course hippique** à partir de données historiques.
Il s’agit d’un problème de **classification binaire**, où la variable cible indique si un cheval finit dans les trois premiers.

---

## Problématique

Dans quelle mesure les caractéristiques d’une course, d’un cheval et du contexte de pari permettent-elles de prédire la probabilité qu’un cheval termine dans le top 3 ?

---

## Dataset

Le dataset utilisé provient d’une base de données hippiques (`raceform.db`) contenant plusieurs milliers d’observations.

Pour des raisons de taille, il n’est pas directement versionné sur GitHub.

### Téléchargement

https://drive.google.com/file/d/1dNkYE4WfnNfQoGLvFmnWlKXSm8-scKE-/view?usp=sharing 

### Installation

Placer le fichier dans le dossier :

```
data/raceform.db
```

---

## Structure du projet

```
.
├── notebooks/
│   └── projet_ml_courses_hippiques_Estelle_MARTINEZ.ipynb
├── data/
│   └── README.md
├── images/
├── rapport_ecrit_Estelle_MARTINEZ.md
├── pyproject.toml
├── uv.lock
└── README.md
```

---

## Environnement

* Python 3.11.14
* Gestionnaire de dépendances : **uv**

### Installation des dépendances

```bash
uv sync
```

---

## Reproduction du projet
1. Cloner le repo
1. Télécharger le dataset à partir du lien : https://drive.google.com/file/d/1dNkYE4WfnNfQoGLvFmnWlKXSm8-scKE-/view?usp=sharing  
2. Le placer dans `data/`
3. Installer les dépendances :

   ```bash
   uv sync
   ```
4. Ouvrir le notebook :

   ```
   notebooks/projet_ml_courses_hippiques_Estelle_MARTINEZ.ipynb
   ```

---

## Modélisation

Plusieurs modèles de machine learning ont été comparés :

* Régression logistique
* SVM
* Random Forest
* XGBoost
* KNN
* MLP
* Bagging

Les performances ont été évaluées à l’aide de :

* Accuracy
* Precision
* Recall
* F1-score
* ROC-AUC

---

## Interprétabilité

L’analyse du modèle repose sur des méthodes d’interprétation globale et locale :

### Interprétation globale

* Feature importance
* Permutation importance
* SHAP global
* PDP / ICE

### Interprétation locale

* SHAP (explication individuelle)

---

## Résultats

Le projet met en évidence que certaines variables influencent fortement la probabilité d’un cheval de finir dans le top 3, notamment les performances passées, les cotes et les caractéristiques de la course.

---

## Information

Spécification des hyperparamètres du  meilleur modèle dans le fichier **BEST_MODEL**

## Limites

* Données potentiellement bruitées
* Déséquilibre de classes
* Variables contextuelles difficiles à mesurer

---

## Perspectives

* Optimisation des hyperparamètres
* Feature engineering avancé
* Ajout de données externes
* Modèles plus complexes (stacking, boosting avancé)

---

## Auteurs

Projet réalisé par :

* Estelle Martinez 
