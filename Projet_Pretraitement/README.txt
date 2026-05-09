# Projet de fin de module - Analyse des techniques de prétraitement

## Auteur

- **Nom :** Louraoui Ayoub
- **Encadrant :** M. Mestari Mohammed
- **Groupe :** 4IADM G1
- **Date :** 2 mai 2026

---

## Description

Ce projet analyse et compare l'impact de différentes techniques de prétraitement sur deux types de données :

1. **Données tabulaires (Titanic)** : Classification binaire pour prédire la survie des passagers du Titanic.
2. **Données textuelles (20 Newsgroups)** : Classification multiclasse de documents textuels.

L'étude utilise les outils suivants : Python, scikit-learn, pandas, numpy, matplotlib.

---

## Contenu du dossier

 Ayoub_Louraoui_Projet_Pretraitement/
├── code_projet.ipynb #  le code complet
├── README.md # Ce fichier
├── Rapport_Pretraitement.pdf # Rapport détaillé du projet
└── Sorties_experimentales
├── sorties_experimentales.json
└── figures/ # Dossier des graphiques
├── courbes_ROC.png
├── importance_variables.png
├── pdp_titanic.png
├── matrice_confusion_texte.png
├── mots_discriminants.png
└── effet_ngrammes.png





---

## Résultats principaux

### Partie I - Données tabulaires (Titanic)

#### 1. Validation croisée (5-fold)

| Méthode                    | Accuracy moyenne | Écart-type |
|----------------------------|-----------------|------------|
| Logistic Regression        | 79.64%          | ±3.2%      |
| Random Forest              | 79.23%          | ±2.8%      |
| Random Forest + KNNImputer | 82.34%          | ±2.5%      |

#### 2. Évaluation finale sur test

| Modèle                     | Accuracy | AUC-ROC |
|----------------------------|----------|---------|
| Logistic Regression        | 79.89%   | 0.8523  |
| Random Forest (optimisé)   | 82.68%   | 0.8765  |
| Random Forest + KNNImputer | 82.70%   | 0.8771  |

#### 3. Meilleurs hyperparamètres (Random Forest)

| Paramètre           | Valeur optimale |
|---------------------|-----------------|
| n_estimators        | 200             |
| max_depth           | 10              |
| min_samples_split   | 5               |

---

### Partie II - Données textuelles (20 Newsgroups)

#### 1. Validation croisée (3-fold)

| Méthode                              | Accuracy moyenne |
|--------------------------------------|-----------------|
| CountVectorizer + ComplementNB       | 90.60%          |
| TF-IDF + LogisticRegression          | 89.44%          |
| TF-IDF + bigrammes + LogisticRegression | 91.20%      |

#### 2. Évaluation finale sur test

| Méthode                              | Accuracy |
|--------------------------------------|----------|
| CountVectorizer + ComplementNB       | 88.32%   |
| TF-IDF + LogisticRegression          | 88.91%   |
| TF-IDF + bigrammes + LogisticRegression | **91.28%** |

#### 3. Effet des n-grammes

| Plage de n-grammes | Accuracy (CV 3-fold) |
|--------------------|----------------------|
| (1,1) unigrammes   | 89.87%               |
| (1,2) unigrammes+bigrammes | 89.18%        |
| (1,3) 1 à 3 grammes | 89.40%              |
| (2,2) bigrammes seuls | 69.18%            |

---

## Importance des variables (Titanic)

| Variable     | Importance |
|--------------|------------|
| sex          | 17.82%     |
| pclass       | 4.64%      |
| age          | 3.83%      |
| fare         | 3.21%      |
| embarked     | 1.42%      |
| sibsp        | 0.14%      |
| parch        | 0.00%      |
| alone        | -1.28%     |

---

## Mots discriminants par classe (20 Newsgroups)

| Classe                  | Top 5 mots                          |
|-------------------------|-------------------------------------|
| sci.med                 | doctor, disease, patients, medical, health |
| sci.space               | space, nasa, orbit, moon, launch    |
| rec.sport.baseball      | baseball, game, hit, braves, season |
| talk.politics.guns      | guns, firearm, rights, amendment, weapons |

---

## Recommandations

| Contexte                              | Méthode recommandée                    | Justification                              |
|---------------------------------------|----------------------------------------|--------------------------------------------|
| Données tabulaires (sans outliers)    | Logistic Regression + StandardScaler   | Performance 79.89%, simple et interprétable |
| Données tabulaires (meilleure perf)   | Random Forest + KNNImputer             | Meilleure accuracy (82.70%)                |
| Meilleur compromis                    | Random Forest optimisé                 | Accuracy 82.68%, plus rapide que KNNImputer |
| Données textuelles (simple)           | CountVectorizer + ComplementNB         | Rapide, accuracy 88.32%                    |
| Données textuelles (meilleure perf)   | TF-IDF + bigrammes + LogisticRegression | Meilleure accuracy (91.28%)               |
| Données creuses (sparse)              | MaxAbsScaler                           | Préserve la parcimonie                     |

---

## Diagnostics

| Situation                               | Observation                                      |
|-----------------------------------------|--------------------------------------------------|
| Performances optimales (textes)         | TF-IDF + bigrammes : 91.28%                     |
| Performances optimales (tabulaires)     | Random Forest + KNNImputer : 82.70%             |
| Impact des bigrammes                    | Gain de +2% par rapport aux unigrammes          |
| Variable la plus discriminante (Titanic)| sex (femmes 74% survie vs hommes 19%)           |
| Robustesse aux outliers                 | Random Forest peu affecté                       |

---

## Graphiques générés

| Fichier                          | Description                                      |
|----------------------------------|--------------------------------------------------|
| `matrice_confusion_titanic.png`  | Matrice de confusion du Random Forest optimisé  |
| `courbes_ROC.png`                | Courbes ROC comparées des modèles Titanic       |
| `importance_variables.png`       | Importance des variables par permutation        |
| `pdp_titanic.png`                | Partial Dependence Plots (effet des variables)  |
| `matrice_confusion_texte.png`    | Matrice de confusion du meilleur modèle texte   |
| `mots_discriminants.png`         | Top 15 mots discriminants par classe            |
| `effet_ngrammes.png`             | Impact des n-grammes sur la performance         |

---

## Technologies utilisées

- **Langage :** Python 3.10+
- **Bibliothèques :** 
  - numpy, pandas (manipulation des données)
  - scikit-learn (prétraitement, modélisation, évaluation)
  - matplotlib (visualisations)
  - seaborn (dataset Titanic)

---

## Conclusion

Ce projet démontre l'importance du choix des techniques de prétraitement selon la nature des données :

- **Pour les données tabulaires** : Random Forest avec imputation médiane offre le meilleur compromis performance/robustesse (Accuracy 82.7%).
- **Pour les données textuelles** : TF-IDF avec bigrammes associé à LogisticRegression atteint la meilleure performance (Accuracy 91.3%).
- **Aucune méthode n'est universellement optimale** : le choix doit être guidé par les caractéristiques des données.

---

*Projet réalisé dans le cadre du module "Prétraitement, représentation, modélisation et analyse des données avec scikit-learn" - EMSI 2025/2026*