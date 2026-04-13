Projet de Machine Learning – Prédiction du top 3 en courses hippiques
1. Objectif
Ce projet vise à prédire si un cheval termine dans le top 3 d'une course à partir de données historiques hippiques.

Il répond aux consignes du projet :

dataset de plus de 4000 observations
problème de classification
comparaison de plusieurs modèles
interprétation globale et locale du meilleur modèle
2. Problématique
Dans quelle mesure les caractéristiques d’une course, d’un cheval et du contexte de pari permettent-elles de prédire la probabilité qu’un cheval termine dans les trois premiers ?

3. Dataset
Le dataset brut est une base SQLite nommée raceform.db.

Pour des raisons de taille, il n’est pas versionné directement sur GitHub. Téléchargement : https://drive.google.com/file/d/1dNkYE4WfnNfQoGLvFmnWlKXSm8-scKE-/view?usp=sharing

Placer le fichier ici : data/raceform.db

Voir aussi : data/README.md

4. Structure du dépôt
.
├── images/
├── notebooks/
│   └── projet_ml_courses_hippiques.ipynb
├── data/
│   └── README.md
├── README.md
├── rapport.md
├── pyproject.toml
├── uv.lock
└── best_model.md