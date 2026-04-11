# Spécification des hyperparamètres du meilleur modèle

## Modèle retenu

Le modèle final retenu est **Random Forest** car c'est celui qui avait les meilleurs résultats. 

## Hyperparamètres 

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


```python
print(rf_random.best_params_)
```

puis recopier les hyperparamètres exacts ici.




