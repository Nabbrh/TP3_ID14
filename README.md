# TP3 : Deux cas : Small Data et Big Data

**Nabila Brahimi**, Polytech Marseille, 5A Informatique 

| Dossier | Dataset (Kaggle) | Traitement |
|---|---|---|
| [`Small/`](Small) | *International Bestselling Books — Market Trends* (mnkaggler) : 7 909 lignes | chaîne complète Data → EDA → Prétraitement → Transformation → ML → Évaluation → Déploiement, avec pandas et scikit-learn |
| [`Big/`](Big) | *setimage* (aymenhadjslimane) : 4 318 images de feuilles de pomme de terre, 2,9 Go, 6 classes | Hadoop HDFS et Spark (extraction distribuée, MLlib), de la Transformation au Déploiement |

## Résultats principaux
- **Small** : prédire si un livre deviendra un best-seller international (classé dans au moins 2 pays).
  Régression logistique : PR-AUC 0,49 (4 fois le hasard), ROC-AUC 0,85.
- **Big** : reconnaître 6 états de la feuille (5 maladies et « saine »). Forêt aléatoire MLlib : 57,2 %
  d'accuracy, contre 16,1 % pour la référence. Une fuite de données a été détectée dans le découpage fourni
  (51 % du test déjà vu à l'entraînement) et corrigée par un découpage par photo d'origine.

## Contenu
- `Small/` : notebook exécuté, dataset CSV, modèle déployé (`modele_bestsellers.joblib`).
- `Big/` : notebook exécuté, modèles exportés (`modele_pommes_de_terre.json` : régression logistique ;
  `modele_pommes_de_terre_foret.joblib` : forêt aléatoire), configuration du cluster Hadoop
  (`docker-compose.yaml`).

## Reproduire
- Environnement : Python 3.12, pandas, scikit-learn, PySpark 3.5, Java 8 (Windows).
- **Small** : ouvrir le notebook et tout exécuter (le CSV est dans le dossier).
- **Big** : les images ne sont pas dans le dépôt (2,9 Go). Il faut les télécharger depuis Kaggle (*setimage*)
  et placer les dossiers `train/` et `test/` à côté du notebook. Lancer le cluster avec
  `docker compose up -d` (section 2), puis exécuter le notebook.
