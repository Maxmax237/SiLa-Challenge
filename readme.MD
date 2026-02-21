# 🚀 Pipeline ETL Complet - Python Data Processing

Un site web statique interactif et pédagogique présentant en détail l'implémentation complète d'un pipeline Extract-Transform-Load (ETL) en Python avec pandas, numpy, seaborn et matplotlib.

## 📋 Sommaire

- [Vue d'ensemble](#vue-densemble)
- [Fonctionnalités](#fonctionnalités)
- [Structure du projet](#structure-du-projet)
- [Installation et utilisation](#installation-et-utilisation)
- [Documentation détaillée](#documentation-détaillée)
- [Visualisations](#visualisations)
- [Technologies utilisées](#technologies-utilisées)
- [Contribution](#contribution)

## 🎯 Vue d'ensemble

Ce projet est une implémentation complète et détaillée d'un pipeline ETL en Python, présentée sous forme d'un site web interactif et éducatif. Il couvre tous les aspects du traitement des données : extraction, transformation, nettoyage, analyse et export.

### Objectifs pédagogiques
- Comprendre les concepts fondamentaux du pipeline ETL
- Maîtriser les techniques avancées de manipulation de données avec pandas
- Apprendre à détecter et traiter les valeurs aberrantes
- Créer des features dérivées pour l'analyse de données
- Exporter des données vers différents formats avec mise en forme

## ✨ Fonctionnalités

### 1. Extraction des données
- **Lecture multi-fichiers CSV** : Gestion de fichiers avec différents encodages et formats
- **Détection automatique** : Détection intelligente de l'encodage et des séparateurs
- **Gestion des erreurs** : Système robuste de gestion des erreurs de lecture

### 2. Transformation des données
- **Fusion des datasets** : Utilisation de `pd.concat()` et `pd.merge()`
- **Standardisation** : Uniformisation des colonnes et des types de données
- **Nettoyage avancé** : Gestion des valeurs manquantes avec différentes stratégies

### 3. Détection des outliers
- **Méthode IQR** : Détection basée sur l'intervalle interquartile
- **Stratégies de traitement** : Capping, suppression ou transformation
- **Analyse statistique** : Rapport détaillé sur les outliers détectés

### 4. Features dérivées
- **Statistiques par groupe** : Moyenne, médiane, écart-type par catégorie
- **Ratios et proportions** : Création de variables ratio
- **Features polynomiales** : Utilisation de PolynomialFeatures de sklearn
- **Composantes principales** : PCA pour la réduction de dimensionnalité

### 5. Export des données
- **CSV** : Export avec compression et gestion des gros fichiers
- **Excel** : Export avec mise en forme professionnelle
- **Formatage conditionnel** : Color scales, data bars et icon sets

### 6. Visualisations interactives
- **Chart.js** : Graphiques animés et interactifs
- **Distribution des données** : Histogrammes et diagrammes en barres
- **Corrélation** : Matrices de corrélation et graphiques en ligne
- **Outliers** : Diagrammes en secteur pour la répartition

## 📁 Structure du projet

```
pipeline-etl-website/
├── index.html              # Page principale avec toutes les sections
├── css/
│   └── style.css          # Styles modernes et responsive
├── js/
│   └── main.js            # JavaScript interactif et animations
└── README.md              # Documentation complète
```

## 🚀 Installation et utilisation

### Prérequis
- Un navigateur web moderne (Chrome, Firefox, Safari, Edge)
- Connexion internet (pour les CDN)

### Installation
1. Clonez le dépôt ou téléchargez les fichiers
2. Ouvrez `index.html` dans votre navigateur
3. Explorez les différentes sections du pipeline ETL

### Utilisation
- **Navigation** : Utilisez la barre de navigation fixe pour accéder aux différentes sections
- **Code Python** : Copiez le code directement depuis les blocs de code
- **Visualisations** : Interagissez avec les graphiques Chart.js
- **Mode sombre** : Activez le mode sombre avec le bouton en haut à droite

## 📚 Documentation détaillée

### Les 4 datasets utilisés

#### 1. Titanic Dataset
- **Taille** : ~891 lignes × 12 colonnes
- **Colonnes** : PassengerId, Survived, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked
- **Utilisation** : Classification binaire (survie/passage)
- **Source** : Kaggle Titanic competition

#### 2. Iris Dataset
- **Taille** : 150 lignes × 5 colonnes
- **Colonnes** : sepal_length, sepal_width, petal_length, petal_width, species
- **Utilisation** : Classification multiclasse (3 espèces d'iris)
- **Source** : Fisher's Iris dataset

#### 3. Amazon Bestsellers Books
- **Taille** : ~2000+ lignes × 7 colonnes
- **Colonnes** : Name, Author, User Rating, Reviews, Price, Year, Genre
- **Utilisation** : Analyse de tendances et recommandation
- **Source** : Kaggle Amazon bestsellers

#### 4. Weather Data 2018-2022
- **Taille** : ~1800+ lignes × 6 colonnes
- **Colonnes** : date, temperature, humidity, precipitation, windspeed, location
- **Utilisation** : Séries temporelles et prévisions météo
- **Source** : Données météorologiques historiques

### Extraction des données

```python
def extraire_donnees(self, chemins_fichiers):
    """
    Extrait les données de plusieurs fichiers CSV
    """
    for nom, chemin in chemins_fichiers.items():
        try:
            # Détection automatique de l'encodage
            df = self._lire_csv_avec_encodage(chemin)
            self.data[nom] = df
            print(f"✅ {nom}: {df.shape[0]} lignes, {df.shape[1]} colonnes")
        except Exception as e:
            print(f"❌ Erreur extraction {nom}: {e}")
            raise
```

### Nettoyage des valeurs manquantes

```python
def nettoyer_valeurs_manquantes(self, df, strategy='median'):
    """
    Nettoie les valeurs manquantes en utilisant la stratégie spécifiée
    """
    df_clean = df.copy()
    missing_cols = df_clean.columns[df_clean.isnull().any()].tolist()
    
    for col in missing_cols:
        if df_clean[col].dtype in ['int64', 'float64']:
            if strategy == 'median':
                median_value = df_clean[col].median()
                df_clean[col].fillna(median_value, inplace=True)
                print(f"✅ {col}: Valeurs manquantes remplacées par la médiane ({median_value:.2f})")
    
    return df_clean
```

### Détection des outliers (IQR)

```python
def detecter_outliers_iqr(self, df, columns=None, multiplier=1.5):
    """
    Détecte les outliers en utilisant la méthode IQR
    """
    outliers_info = {}
    numeric_cols = columns or df.select_dtypes(include=[np.number]).columns
    
    for col in numeric_cols:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        
        # Limites de détection
        lower_bound = Q1 - multiplier * IQR
        upper_bound = Q3 + multiplier * IQR
        
        # Identification des outliers
        outliers = df[(df[col] < lower_bound) | (df[col] > upper_bound)]
        
        outliers_info[col] = {
            'Q1': Q1, 'Q3': Q3, 'IQR': IQR,
            'lower_bound': lower_bound,
            'upper_bound': upper_bound,
            'outliers_count': len(outliers)
        }
    
    return outliers_info
```

### Export Excel avec mise en forme

```python
def exporter_excel_formate(self, df, chemin_sortie, nom_feuille='Données'):
    """
    Exporte vers Excel avec mise en forme professionnelle
    """
    with pd.ExcelWriter(chemin_sortie, engine='xlsxwriter') as writer:
        # Écrire les données
        df.to_excel(writer, sheet_name=nom_feuille, index=False)
        
        # Formater l'en-tête
        workbook = writer.book
        worksheet = writer.sheets[nom_feuille]
        
        header_format = workbook.add_format({
            'bold': True,
            'text_wrap': True,
            'valign': 'top',
            'fg_color': '#D7E4BC',
            'border': 1
        })
        
        # Appliquer le format d'en-tête
        for col_num, value in enumerate(df.columns.values):
            worksheet.write(0, col_num, value, header_format)
        
        # Ajustement automatique de la largeur des colonnes
        for i, col in enumerate(df.columns):
            max_length = max(df[col].astype(str).map(len).max(), len(col)) + 2
            worksheet.set_column(i, i, min(max_length, 50))
```

## 📊 Visualisations

### Graphiques inclus
1. **Distribution des datasets** : Diagramme en barres montrant la taille de chaque dataset
2. **Performance du pipeline** : Graphique en ligne montrant le temps d'exécution de chaque étape
3. **Répartition des outliers** : Diagramme en secteur montrant le pourcentage d'outliers détectés

### Interactivité
- **Animations** : Tous les graphiques sont animés avec des transitions fluides
- **Responsive** : Les graphiques s'adaptent à la taille de l'écran
- **Tooltips** : Informations détaillées au survol des points de données
- **Légendes** : Légendes interactives pour filtrer les séries

## 🛠 Technologies utilisées

### Frontend
- **HTML5** : Structure sémantique moderne
- **CSS3** : Styles avancés avec variables CSS et animations
- **JavaScript ES6+** : Interactivité et animations
- **Bootstrap 5** : Framework CSS responsive
- **Chart.js** : Visualisations de données interactives
- **Prism.js** : Coloration syntaxique du code Python

### Bibliothèques Python (dans le code)
- **pandas** : Manipulation et analyse de données
- **numpy** : Calculs numériques
- **seaborn** : Visualisations statistiques
- **matplotlib** : Graphiques et visualisations
- **scikit-learn** : Features engineering et preprocessing

### Outils de développement
- **Git** : Contrôle de version
- **VS Code** : Éditeur de code
- **Chrome DevTools** : Débogage et optimisation

## 🤝 Contribution

Les contributions sont les bienvenues ! Voici comment contribuer :

### Rapport de bugs
1. Créez une issue décrivant le bug
2. Incluez les étapes pour reproduire le problème
3. Ajoutez des captures d'écran si pertinent

### Propositions d'amélioration
1. Fork le projet
2. Créez une branche pour votre fonctionnalité
3. Commitez vos changements
4. Push vers la branche
5. Ouvrez une Pull Request

### Améliorations suggérées
- [ ] Ajouter plus de datasets (Bitcoin, COVID-19, etc.)
- [ ] Implémenter des algorithmes de machine learning
- [ ] Ajouter des tests unitaires pour le code Python
- [ ] Créer une version interactive avec Jupyter Notebook
- [ ] Ajouter des exemples de dashboard avec Plotly
- [ ] Implémenter le streaming de données en temps réel

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier LICENSE pour plus de détails.

## 🙏 Remerciements

- **Kaggle** pour les datasets
- **Chart.js** pour les visualisations interactives
- **Bootstrap** pour le framework CSS
- **Prism.js** pour la coloration syntaxique
- **La communauté open source** pour les bibliothèques Python

## 📞 Contact

Pour toute question ou suggestion, n'hésitez pas à ouvrir une issue ou à contribuer au projet.

---

**⭐ Si ce projet vous est utile, n'hésitez pas à lui donner une étoile !** ⭐
