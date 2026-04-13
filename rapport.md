# Rapport de Projet : Prédiction de la performance des chevaux en course hippique

## 1. Introduction et Objectifs

L’objectif de ce projet est de prédire la performance d’un cheval lors d’une course hippique à partir d’un ensemble de variables décrivant à la fois les caractéristiques du cheval, de la course, du jockey, de l’entraîneur ainsi que des informations issues du marché des paris.

La variable cible retenue n’est pas la position exacte à l’arrivée, mais une variable binaire pos3, indiquant si le cheval termine dans les trois premières positions.

Ce choix méthodologique se justifie par plusieurs éléments :

La position exacte est extrêmement bruitée et dépend de nombreux facteurs aléatoires
Les différences entre certaines positions (ex : 4e vs 5e) sont peu informatives
L’objectif d’être dans le top 3 correspond davantage à une logique métier (performance / pari)

Ainsi, le problème est formulé comme une classification binaire, visant à estimer la probabilité de performance élevée.

Le jeu de données utilisé contient un ensemble d’observations de courses hippiques, avec des variables numériques et catégorielles décrivant différents aspects de la compétition.

Afin de répondre à cette problématique, la démarche adoptée repose sur les étapes suivantes :

Analyse exploratoire des données
Traitement des valeurs manquantes
Transformation et création de variables
Construction d’un pipeline de modélisation
Comparaison de plusieurs modèles de machine learning
Analyse des performances et interprétation des résultats

---

## 2. Préparation des données et Analyse Exploratoire
### 2.1. Réduction préalable du volume de données

Avant la séparation entre échantillon d’apprentissage et échantillon de test, une réduction du volume de données a été effectuée. En effet, la taille initiale du jeu de données était trop importante pour permettre des temps de calcul raisonnables, en particulier lors des phases de modélisation et de comparaison de plusieurs algorithmes.

Plutôt que de procéder à un échantillonnage aléatoire global, nous avons choisi de conserver 20 % des observations pour chaque combinaison de la variable cible (`top3`) et de la variable temporelle (`date`). Cette stratégie permet de réduire la taille du dataset tout en préservant au mieux sa structure, notamment la répartition des classes au fil du temps.

Ainsi, cette étape vise à obtenir un sous-échantillon plus léger à manipuler, sans déformer excessivement la distribution de la variable cible ni la dimension temporelle des données.


### 2.2. Stratégie de séparation des données (Train/Test Split)

Contrairement à une approche classique aléatoire, j'ai choisi de réaliser un split temporel des données.

Les données les plus anciennes sont utilisées pour l’apprentissage, tandis que les plus récentes servent à l’évaluation.

Ce choix est fondamental pour plusieurs raisons :

Il permet de respecter la chronologie des événements
Il évite toute fuite d’information (data leakage)
Il reproduit une situation réelle de prédiction (prédire le futur à partir du passé)

Un split aléatoire aurait artificiellement amélioré les performances du modèle en mélangeant des observations passées et futures.

![Schéma du split temporel](images/split_temporel.png)

### 2.3. Analyse exploratoire des variables

Une analyse descriptive a été réalisée afin de comprendre la structure des données.

``Distribution des variables``

Certaines variables présentent une forte asymétrie, notamment :

jockey_freq
trainer_freq
sp_prob

Ces distributions sont caractérisées par :

une forte concentration de petites valeurs
quelques valeurs extrêmes élevées

![Histogrammes](images/histogrammes.png)

Ces caractéristiques peuvent poser problème pour certains modèles, notamment les modèles linéaires.

``Analyse des corrélations``

Une analyse des corrélations entre variables explicatives a été effectuée afin d’identifier :

des relations redondantes
des risques de multicolinéarité

![Table de corrélation](images/correlations_variables.png)

Les corrélations observées restent globalement modérées, ce qui suggère :

une faible redondance entre variables
une complémentarité de l’information

Cela justifie le maintien d’un grand nombre de variables dans la modélisation.

``Lien avec la variable cible``

Certaines variables apparaissent plus liées à la performance :

sp_prob (logique de marché)
or (niveau du cheval)
variables liées au jockey / entraîneur

Cependant, ces relations restent complexes et potentiellement non linéaires.

### 2.4. Gestion des valeurs manquantes

Certaines variables présentent des valeurs manquantes.

Ces absences peuvent être :

accidentelles
structurelles (ex : absence de rating pour certains chevaux)

Afin de rendre les données exploitables par les modèles, une imputation par la médiane a été appliquée aux variables numériques.

Ce choix est motivé par :

sa robustesse face aux valeurs extrêmes
sa simplicité de mise en œuvre

Cependant, dans le cas de la variable or, l’absence d’information est elle-même informative. Une variable indicatrice or_missing a donc été créée afin de conserver cette information.

--- 

## 3. Prétraitement et transformation des variables
### 3.1. Feature Engineering

Plusieurs transformations ont été réalisées.

Variable binaire : has_rating_min

La variable rating_min a été transformée en variable binaire afin de distinguer :

les courses avec seuil minimal
les courses sans contrainte

Cette variable permet de capter des différences structurelles entre types de courses.

### 3.2. Transformation logarithmique

Les variables suivantes ont été transformées :

jockey_freq
trainer_freq
sp_prob

via une transformation log1p.

Objectifs :

réduire l’asymétrie
limiter l’impact des valeurs extrêmes
améliorer la stabilité des modèles

(image : avant/après log)

### 3.3. Préparation pour la modélisation

Les différentes transformations ont été intégrées dans un pipeline afin de garantir :

la reproductibilité
l’absence de fuite d’information
une application cohérente sur train et test
## 4. Modélisation et comparaison des modèles

Afin de répondre à l’objectif de prédiction, plusieurs modèles ont été testés.

### 4.1. Régression logistique

Modèle de référence permettant :

une interprétation directe
une première approximation des relations

Limite : incapacité à capturer des relations complexes.

### 4.2. Random Forest

Modèle basé sur des arbres :

capture les non-linéarités
robuste aux outliers
limite le surapprentissage
4.3. XGBoost

Modèle de boosting performant :

capture des interactions complexes
optimise les performances prédictives
intègre de la régularisation
4.4. Optimisation des modèles

Les hyperparamètres ont été ajustés afin d’améliorer les performances, notamment :

profondeur des arbres
nombre d’estimateurs
learning rate

---

## 5. Évaluation des performances

Les modèles ont été évalués à l’aide de :

Accuracy
ROC-AUC
Precision / Recall

![ROC_CURVE](images/ROC_CURVE.png)

Résultats
XGBoost est le modèle le plus performant
Random Forest offre un bon compromis
La régression logistique reste utile pour l’interprétation

--- 

## 6. Analyse et interprétation des résultats
### 6.1. Variables importantes

Les variables les plus influentes sont :

sp_prob : très forte capacité prédictive
or : niveau du cheval
variables liées au jockey et à l’entraîneur

Cela suggère que :

le marché intègre déjà une grande partie de l’information
l’expérience des acteurs joue un rôle clé

### 6.2. Analyse des résidus

(image : résidus)

Les résidus sont globalement centrés autour de 0, ce qui indique :

absence de biais majeur
bonne calibration globale du modèle

Cependant, certaines erreurs persistent, liées à :

l’aléa des courses
des variables non observées

---

## 8. Discussion des choix méthodologiques
Choix de la variable cible

Le passage à pos3 permet de stabiliser le problème et d’améliorer la prédictibilité.

Transformations

Les transformations log jouent un rôle clé dans la qualité du modèle.

Imputation

L’imputation médiane est un compromis entre robustesse et simplicité.

Split temporel

Choix essentiel pour garantir une évaluation réaliste.

---

## 7. Explicabilité et interprétabilité du modèle

Les modèles de machine learning utilisés, en particulier les modèles ensemblistes comme XGBoost, présentent des performances élevées mais sont souvent considérés comme des "boîtes noires". Il est donc essentiel de comprendre les mécanismes sous-jacents à leurs prédictions.

Dans cette optique, nous avons mobilisé des méthodes d’explicabilité globale et locale, permettant d’interpréter à la fois le comportement général du modèle et ses décisions individuelles.

---

### 7.1. Explicabilité globale : importance des variables (SHAP)

Afin d’identifier les variables les plus influentes dans les prédictions du modèle, nous avons utilisé la méthode SHAP (SHapley Additive exPlanations).

SHAP repose sur une approche issue de la théorie des jeux, attribuant à chaque variable une contribution marginale à la prédiction.

#### Importance globale des variables

![shap_sum](images/shap_sum.png)

L’analyse du graphique SHAP met en évidence plusieurs résultats importants :

- La variable `sp_prob` apparaît comme la plus influente. Cela est cohérent puisque cette variable est issue du marché des paris, qui agrège déjà une grande quantité d’informations.
- Les variables liées au niveau du cheval (`or`) jouent également un rôle déterminant.
- Les variables associées au jockey et à l’entraîneur (`jockey_freq`, `trainer_freq`) contribuent significativement à la prédiction.

Les couleurs du graphique indiquent la valeur de la variable :

- En rouge : valeurs élevées
- En bleu : valeurs faibles

On observe que des valeurs élevées de `sp_prob` augmentent fortement la probabilité d’être dans le top 3, ce qui confirme la pertinence de cette variable.

#### Interprétation globale

Globalement, le modèle s’appuie sur trois grandes dimensions :

- **L’information de marché** (sp_prob)
- **Le niveau intrinsèque du cheval** (rating)
- **L’expérience des acteurs** (jockey / entraîneur)

Ces résultats sont cohérents avec l’intuition métier.

---

### 7.2. Explicabilité locale : analyse individuelle (SHAP)

Afin de comprendre comment le modèle prend une décision pour un individu donné, nous avons analysé les contributions locales à l’aide de SHAP.

![shap_water](images/shap_water.png)

Le graphique waterfall permet de décomposer une prédiction individuelle :

- On part d’une valeur moyenne (baseline)
- Chaque variable vient augmenter ou diminuer la prédiction

On observe que :

- Certaines variables ont un effet fortement positif (ex : probabilité élevée, bon rating)
- D’autres variables peuvent réduire la probabilité (ex : faible expérience du jockey)

Cela permet de comprendre précisément pourquoi un cheval est prédit comme performant ou non.

---

### 7.3. Explicabilité locale : LIME

En complément de SHAP, nous avons utilisé la méthode LIME (Local Interpretable Model-agnostic Explanations).

LIME consiste à approximer localement le modèle complexe par un modèle simple et interprétable (souvent linéaire) autour d’une observation donnée.

(image : LIME output)

Pour un individu spécifique, LIME permet d’identifier :

- Les variables qui poussent la prédiction vers le haut
- Les variables qui la tirent vers le bas

Contrairement à SHAP, LIME peut parfois produire des résultats plus instables, car il repose sur un échantillonnage local. Néanmoins, il offre une lecture intuitive des décisions du modèle.

---

### 7.4. Discussion sur l’explicabilité

Les méthodes SHAP et LIME offrent des perspectives complémentaires :

- SHAP fournit une interprétation cohérente et théoriquement fondée
- LIME permet une lecture locale intuitive

Les résultats obtenus confirment que le modèle s’appuie principalement sur des variables pertinentes du point de vue métier.

Cependant, ces méthodes mettent également en évidence la complexité du modèle :

- certaines interactions entre variables sont difficiles à interpréter
- des effets locaux peuvent diverger des tendances globales

Cela souligne l’importance de combiner performance prédictive et interprétabilité dans un contexte appliqué.

---

### 7.5. Limites de l’interprétation

Malgré leur intérêt, ces méthodes présentent certaines limites :

- Elles reposent sur des approximations du modèle
- Elles peuvent être sensibles aux données utilisées
- Elles n’expliquent pas les causalités, mais uniquement les contributions statistiques

Ainsi, les résultats doivent être interprétés avec prudence.

---

## 9. Limites
Données bruitées
Variables manquantes non observées
Difficulté intrinsèque du problème

---

## 10. Conclusion

Ce projet met en évidence l’importance :

du prétraitement des données
du choix de la variable cible
de la comparaison de modèles

Les modèles de machine learning permettent d’obtenir des performances satisfaisantes, mais restent limités par la nature aléatoire du phénomène étudié.

Des améliorations pourraient inclure :

l’ajout de nouvelles variables
des modèles plus avancés
une meilleure prise en compte du contexte des courses