# Spécification des hyperparamètres du meilleur modèle

## Modèle retenu

Le modèle final retenu est un **Random Forest**.
Il a été sélectionné car il offre le meilleur compromis entre performance prédictive et robustesse par rapport aux autres modèles testés.

---

## Hyperparamètres du modèle

Les hyperparamètres utilisés pour le modèle final sont les suivants :

```python
RandomForestClassifier(
    n_estimators=200,
    max_depth=12,
    min_samples_leaf=20,
    n_jobs=-1,
    class_weight="balanced_subsample",
    random_state=42
)
```

---

## Justification

Ce paramétrage permet :

* de limiter le surapprentissage grâce à une profondeur contrôlée (`max_depth`)
* de stabiliser les prédictions via un nombre suffisant d’arbres (`n_estimators`)
* de prendre en compte le déséquilibre des classes (`class_weight`)
* d’assurer la reproductibilité des résultats (`random_state`)

---

## Remarque

Ces hyperparamètres ont été déterminés après plusieurs tests et ajustements empiriques afin d’optimiser les performances du modèle.



