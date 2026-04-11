# Projet de machine learning :  Classification du top 3 en courses hippiques

Ce dépôt contient un projet de **classification supervisée** visant à prédire si un cheval termine dans le **top 3** d'une course.

## Contenu du dépôt

- `notebooks/projet_ml_courses_hippiques.ipynb` : notebook principal du projet
- `data/` : dossier pour le **dataset brut**
- `pyproject.toml` : dépendances du projet gérées avec **UV**
- `uv.lock` : verrouillage exact de l'environnement
- `BEST_MODEL.md` : spécification des hyperparamètres du modèle retenu
- `.python-version` : version de Python utilisée

## Version de Python

Le notebook a été exécuté avec **Python 3.11.14**.

## Reproductibilité

### 1. Installer UV

Suivre la documentation officielle de UV.

### 2. Cloner le dépôt

```bash
git clone https://github.com/estellemtz/SVM.git
cd SVM
```

### 3. Ajouter le dataset brut

Déposer le fichier brut dans :

```text
data/raceform.db
```

### 4. Synchroniser l'environnement

```bash
uv sync
```

### 5. Lancer le notebook

```bash
uv run jupyter notebook
```

## Modélisation

Les modèles comparés dans le notebook incluent notamment :

- Régression logistique
- SVM linéaire calibré
- Random Forest
- XGBoost
- Bagging Classifier
- KNN
- MLP Classifier

## Explicabilité / interprétabilité

Méthodes utilisées dans le notebook :

- Feature importance
- Permutation importance
- SHAP global
- SHAP local
- PDP
- ALE
- ICE



