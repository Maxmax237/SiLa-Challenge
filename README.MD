# 🌸 Tableau de Bord Iris - Analyse Multi-Graphiques

## 📋 Description

Projet d'analyse de données complet du célèbre **dataset Iris** utilisant Python, matplotlib, seaborn, numpy et pandas. Ce projet génère un tableau de bord multi-graphiques avec des visualisations avancées et des statistiques descriptives complètes.

## 🎯 Objectifs du Projet

- ✅ Télécharger et charger le dataset Iris (150 observations, 3 espèces)
- ✅ Calculer les statistiques descriptives (moyenne, médiane, écart-type, quartiles)
- ✅ Créer un tableau de bord avec subplot 2x2 :
  - Histogramme des distributions
  - Scatter plot avec régression linéaire
  - Heatmap de corrélation
  - Box plots des distributions
- ✅ Générer un graphique animé (évolution des moyennes)
- ✅ Soigner la mise en forme (titres, légendes, annotations)

## 📦 Structure du Projet

```
iris_dashboard/
│
├── download_iris.py              # Téléchargement du dataset
├── statistiques.py               # Calculs statistiques descriptifs
├── dashboard.py                  # Génération des visualisations
├── main.py                       # Script principal
│
├── iris_dataset.csv              # Dataset Iris (généré)
├── rapport_statistiques_iris.txt # Rapport statistique détaillé
├── statistiques_resumees.csv     # Tableau récapitulatif CSV
│
├── dashboard_iris_principal.png       # Dashboard 2x2 subplots
├── dashboard_iris_supplementaire.png  # Graphiques supplémentaires
├── animation_iris.gif                 # Animation des moyennes
│
└── README.md                     # Cette documentation
```

## 🛠️ Bibliothèques Utilisées

- **pandas** : Manipulation et analyse de données
- **numpy** : Calculs numériques et statistiques
- **matplotlib** : Visualisations de base
- **seaborn** : Visualisations statistiques avancées
- **scipy** : Régression linéaire et statistiques
- **sklearn** : Chargement du dataset Iris

## 🚀 Installation et Exécution

### Prérequis

```bash
# Installer les dépendances (déjà installées dans l'environnement)
pip install pandas numpy matplotlib seaborn scipy scikit-learn
```

### Exécution Complète

```bash
cd /home/user/iris_dashboard
python3 main.py
```

### Exécution Modulaire

```bash
# Télécharger uniquement le dataset
python3 download_iris.py

# Calculer uniquement les statistiques
python3 statistiques.py

# Générer uniquement les visualisations
python3 dashboard.py
```

## 📊 Statistiques Calculées

### Mesures de Tendance Centrale
- **Moyenne** : Valeur moyenne de chaque variable
- **Médiane (Q2)** : Valeur centrale (50ᵉ percentile)

### Mesures de Dispersion
- **Écart-type** : Mesure de la dispersion autour de la moyenne
- **Variance** : Carré de l'écart-type
- **Étendue** : Différence entre max et min
- **IQR** : Écart interquartile (Q3 - Q1)

### Quartiles
- **Q1** : Premier quartile (25ᵉ percentile)
- **Q2** : Deuxième quartile (50ᵉ percentile - médiane)
- **Q3** : Troisième quartile (75ᵉ percentile)
- **Min/Max** : Valeurs minimale et maximale

## 📈 Visualisations Générées

### 1. Dashboard Principal (2x2 Subplots)

**Fichier** : `dashboard_iris_principal.png`

#### Subplot 1 : Histogramme
- Distribution des longueurs de pétales par espèce
- Ligne verticale pour la moyenne globale
- Couleurs distinctes par espèce
- Annotations statistiques

#### Subplot 2 : Scatter Plot avec Régression
- Relation longueur vs largeur des pétales
- Ligne de régression linéaire
- Équation de régression et R²
- Coloration par espèce

#### Subplot 3 : Heatmap de Corrélation
- Matrice de corrélation des 4 variables numériques
- Coefficients annotés
- Palette de couleurs divergente (coolwarm)
- Corrélations de -1 (négative) à +1 (positive)

#### Subplot 4 : Box Plots
- Distributions de toutes les variables
- Quartiles visibles (Q1, médiane, Q3)
- Valeurs aberrantes (outliers)
- Points individuels superposés

### 2. Graphiques Supplémentaires

**Fichier** : `dashboard_iris_supplementaire.png`

- **Violin Plot** : Distribution détaillée des longueurs de pétales
- **Scatter Plot Sépales** : Longueur vs largeur des sépales
- **KDE Plot** : Densité de probabilité des largeurs de pétales
- **Bar Plot** : Moyennes par espèce pour toutes les variables

### 3. Animation

**Fichier** : `animation_iris.gif`

- Évolution progressive des moyennes par espèce
- Affichage variable par variable
- Animation à 2 FPS pour meilleure lisibilité
- Légende et titre dynamiques

## 📋 Résultats Statistiques Clés

### Dataset Iris
- **Observations** : 150
- **Variables numériques** : 4
- **Espèces** : 3 (Setosa, Versicolor, Virginica)

### Statistiques Principales

#### Sepal Length (cm)
- Moyenne : 5.843 cm
- Médiane : 5.800 cm
- Écart-type : 0.828 cm
- Q1 : 5.100 cm | Q3 : 6.400 cm

#### Sepal Width (cm)
- Moyenne : 3.057 cm
- Médiane : 3.000 cm
- Écart-type : 0.436 cm
- Q1 : 2.800 cm | Q3 : 3.300 cm

#### Petal Length (cm)
- Moyenne : 3.758 cm
- Médiane : 4.350 cm
- Écart-type : 1.765 cm
- Q1 : 1.600 cm | Q3 : 5.100 cm

#### Petal Width (cm)
- Moyenne : 1.199 cm
- Médiane : 1.300 cm
- Écart-type : 0.762 cm
- Q1 : 0.300 cm | Q3 : 1.800 cm

## 🎨 Caractéristiques de Mise en Forme

### Couleurs
- **Setosa** : Rouge (#FF6B6B)
- **Versicolor** : Turquoise (#4ECDC4)
- **Virginica** : Bleu (#45B7D1)

### Typographie
- **Titres** : Police en gras, taille 14-20pt
- **Labels** : Police en gras, taille 11-12pt
- **Légendes** : Taille 9-11pt, fond semi-transparent

### Annotations
- Équations de régression avec R²
- Statistiques clés (moyenne, quartiles)
- Nombre d'observations
- Informations contextuelles

### Grilles
- Grilles légères (alpha=0.3)
- Style pointillé pour meilleure lisibilité
- Présentes sur tous les graphiques

## 📁 Fichiers Générés

| Fichier | Description | Taille |
|---------|-------------|--------|
| `iris_dataset.csv` | Dataset Iris au format CSV | 4.1 Ko |
| `rapport_statistiques_iris.txt` | Rapport statistique détaillé | 2.1 Ko |
| `statistiques_resumees.csv` | Tableau récapitulatif | 558 octets |
| `dashboard_iris_principal.png` | Dashboard 2x2 subplots | 830 Ko |
| `dashboard_iris_supplementaire.png` | Graphiques supplémentaires | 663 Ko |
| `animation_iris.gif` | Animation moyennes | 107 Ko |

## 🔍 Insights et Observations

### Corrélations Fortes
- **Petal Length ↔ Petal Width** : R² ≈ 0.96 (très forte corrélation positive)
- **Sepal Length ↔ Petal Length** : Corrélation positive significative
- **Sepal Width** : Corrélation plus faible avec les autres variables

### Différenciation des Espèces
- **Setosa** : Pétales nettement plus courts et étroits
- **Virginica** : Dimensions généralement les plus grandes
- **Versicolor** : Dimensions intermédiaires

### Distributions
- **Petal Length** : Distribution bimodale (deux pics)
- **Sepal Width** : Distribution quasi-normale
- **Séparation claire** entre Setosa et les deux autres espèces

## 🎓 Concepts Statistiques Appliqués

- **Statistiques descriptives** : Moyenne, médiane, écart-type, quartiles
- **Régression linéaire** : Relation entre variables continues
- **Corrélation** : Mesure de la relation entre variables
- **Visualisation** : Histogrammes, scatter plots, heatmaps, box plots
- **Distribution** : Analyse de la forme et de la dispersion des données

## 📚 Ressources

- **Dataset Iris** : [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/iris)
- **Kaggle** : [Iris Dataset](https://www.kaggle.com/datasets/uciml/iris)
- **Seaborn** : [Documentation officielle](https://seaborn.pydata.org/)
- **Matplotlib** : [Documentation officielle](https://matplotlib.org/)

## 🏆 Points Forts du Projet

✓ **Code modulaire** : Séparation claire des responsabilités
✓ **Visualisations professionnelles** : Mise en forme soignée
✓ **Statistiques complètes** : Toutes les mesures importantes
✓ **Documentation exhaustive** : README et rapports détaillés
✓ **Reproductible** : Scripts autonomes et bien structurés
✓ **Pédagogique** : Commentaires et explications détaillées

## 📝 Auteur

Projet d'analyse de données - Dataset Iris
Bibliothèques : matplotlib, seaborn, numpy, pandas

---

**Version** : 1.0  
**Date** : Février 2024  
**Licence** : Éducatif - Libre d'utilisation pour l'apprentissage
