[README.md](https://github.com/user-attachments/files/25384610/README.md)
# Système Bancaire Orienté Objet (POO) en Python

## 📋 Description

Système bancaire complet implémenté en Python utilisant les concepts de Programmation Orientée Objet (POO). Le système gère différents types de comptes bancaires avec historique des transactions, gestion des exceptions et persistance des données en JSON.

## 🎯 Fonctionnalités

### Classes Principales

1. **Compte (Classe Abstraite)**
   - Classe de base pour tous les types de comptes
   - Gestion du solde, numéro de compte, titulaire
   - Méthodes : `deposer()`, `retirer()`, `virement()`
   - Historique complet des transactions avec horodatage

2. **CompteEpargne**
   - Hérite de Compte
   - Taux d'intérêt annuel configurable
   - Plafond de retrait mensuel (3000€)
   - Méthode `calculer_interets()`
   - Réinitialisation mensuelle du plafond

3. **ComptePro**
   - Hérite de Compte
   - Découvert autorisé configurable
   - Frais de gestion mensuels
   - Méthode `appliquer_frais_gestion()`
   - Gestion du solde négatif

### Gestion des Exceptions

- **SoldeInsuffisantError** : Levée quand le solde est insuffisant
- **PlafondDepasseError** : Levée quand un plafond est dépassé
- **MontantInvalideError** : Levée pour un montant négatif ou nul

### Transactions et Historique

- Chaque opération génère une transaction horodatée
- Stockage de : type, montant, solde avant/après, description, date
- Affichage de l'historique complet ou des N dernières transactions

### Persistance JSON

- Sauvegarde automatique de tous les comptes
- Chargement des données au démarrage
- Export de rapports détaillés en format texte
- Sérialisation/Désérialisation complète

## 🏗️ Architecture

```
banking_system/
│
├── exceptions.py          # Exceptions personnalisées
├── transaction.py         # Classe Transaction avec horodatage
├── compte.py             # Classe de base Compte (abstraite)
├── comptes_derives.py    # CompteEpargne et ComptePro
├── gestionnaire.py       # GestionnaireBancaire (persistance)
├── main.py               # Programme principal avec démonstrations
└── README.md             # Cette documentation
```

## 🚀 Utilisation

### Exécution des démonstrations

```bash
cd /home/user/banking_system
python3 main.py
```

### Exemple d'utilisation programmatique

```python
from comptes_derives import CompteEpargne, ComptePro
from gestionnaire import GestionnaireBancaire
from exceptions import SoldeInsuffisantError

# Créer des comptes
compte_epargne = CompteEpargne("Alice Martin", 5000.0, taux_interet=0.03)
compte_pro = ComptePro("Mon Entreprise", 10000.0, decouvert_autorise=2000.0)

# Opérations
compte_epargne.deposer(1000.0, "Salaire")
compte_epargne.retirer(500.0, "Courses")
compte_pro.virement(compte_epargne, 2000.0, "Dividendes")

# Calcul des intérêts
compte_epargne.calculer_interets()

# Frais de gestion
compte_pro.appliquer_frais_gestion()

# Historique
compte_epargne.afficher_historique()

# Gestion des exceptions
try:
    compte_epargne.retirer(10000.0)
except SoldeInsuffisantError as e:
    print(f"Erreur : {e}")

# Persistance
gestionnaire = GestionnaireBancaire("mes_comptes.json")
gestionnaire.ajouter_compte(compte_epargne)
gestionnaire.ajouter_compte(compte_pro)
gestionnaire.sauvegarder()
gestionnaire.exporter_rapport("rapport.txt")
```

## 📊 Démonstrations Incluses

1. **Opérations de base** : Dépôts, retraits, virements
2. **Gestion des exceptions** : Tests de tous les cas d'erreur
3. **Fonctionnalités avancées** : Intérêts, frais, découvert
4. **Historique et persistance** : Sauvegarde/chargement JSON

## 🔧 Concepts POO Utilisés

- ✅ **Héritage** : CompteEpargne et ComptePro héritent de Compte
- ✅ **Encapsulation** : Attributs privés (_solde) avec propriétés
- ✅ **Abstraction** : Classe abstraite Compte avec méthode abstraite
- ✅ **Polymorphisme** : Redéfinition des méthodes (retirer, to_dict)
- ✅ **Composition** : Compte contient des objets Transaction
- ✅ **Exceptions personnalisées** : Gestion d'erreurs spécifiques

## 📦 Dépendances

- Python 3.6+
- Modules standard uniquement (json, datetime, pathlib, typing, abc)

## 📝 Format JSON

```json
{
  "comptes": [
    {
      "type": "CompteEpargne",
      "numero_compte": "FR0000000001",
      "titulaire": "Alice Martin",
      "solde": 5125.0,
      "taux_interet": 0.03,
      "retraits_mois_actuel": 500.0,
      "historique": [
        {
          "type": "DEPOT",
          "montant": 1000.0,
          "solde_avant": 5000.0,
          "solde_apres": 6000.0,
          "description": "Salaire",
          "date": "2024-02-18T10:30:00"
        }
      ]
    }
  ]
}
```

## 🎓 Concepts Pédagogiques

Ce projet illustre :
- Design patterns (Factory, Repository)
- SOLID principles
- Clean Code practices
- Error handling best practices
- Data persistence patterns
- Unit testing readiness

## 📄 Licence

Projet éducatif - Libre d'utilisation pour l'apprentissage
