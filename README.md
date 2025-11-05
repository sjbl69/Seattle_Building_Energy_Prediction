#  Prédiction de la Consommation Énergétique des Bâtiments de Seattle

## 🏙️ Contexte du projet
La ville de **Seattle** s’est engagée à devenir **neutre en carbone d’ici 2050**.  
Pour atteindre cet objectif, la mairie souhaite **estimer la consommation d’énergie et les émissions de CO₂** des bâtiments **non résidentiels** à partir de leurs caractéristiques structurelles : taille, usage, localisation, année de construction, etc.

Les relevés réels étant coûteux à obtenir, le but est de construire un modèle prédictif capable d’estimer ces valeurs à partir des données déjà disponibles.

 **Objectif principal :**
Prédire la **consommation énergétique totale** et les **émissions de gaz à effet de serre** des bâtiments de Seattle.

---

## 📁 Structure du projet

projet_seattle/
│
├── 📂 data/
│ ├── 2016_Building_Energy_Benchmarking.csv → Données brutes téléchargées depuis la source
│ ├── data_cleaned.csv → Données nettoyées et filtrées (bâtiments non résidentiels)
│ ├── X_train.csv / X_test.csv → Variables explicatives (train / test)
│ ├── y_train.csv / y_test.csv → Cibles (train / test)
│
├── 📂 notebooks/
│ ├── 01_EDA.ipynb → Analyse exploratoire et nettoyage
│ ├── 02_Feature_Engineering.ipynb → Création et transformation des variables
│ ├── 03_Modelisation.ipynb → Entraînement et comparaison des modèles
│ └── 04_Optimisation_Interpretation.ipynb → Optimisation du modèle et interprétation des résultats
│
├── requirements.txt → Liste des dépendances Python nécessaires
├── README.md → Présentation et documentation complète du projet
└── .gitignore → Fichiers/dossiers exclus du suivi Git (.venv, fichiers lourds)

##  Étapes du projet

### 1️⃣ Analyse exploratoire (EDA)
📘 *Notebook : `01_EDA.ipynb`*

**Objectif :**
Explorer les données, comprendre leur structure et les nettoyer avant la modélisation.

**Actions réalisées :**
- Chargement du dataset brut (`2016_Building_Energy_Benchmarking.csv`)
- Filtrage des bâtiments **non résidentiels**
- Nettoyage des colonnes 
- Suppression des doublons
- Identification des cibles :
  - Consommation : `SiteEnergyUse(kBtu)`
  - Émission : `TotalGHGEmissions`
- Visualisations :
  - Histogrammes de distribution
  - Matrice de corrélation
- Sauvegarde du jeu nettoyé → `data/data_cleaned.csv`

---

### 2️⃣ Feature Engineering
📘 *Notebook : `02_Feature_Engineering.ipynb`*

**Objectif :** transformer les variables pour les rendre exploitables par un modèle ML.

**Étapes réalisées :**
- Séparation entre :
  - `X` → variables explicatives  
  - `y` → variable cible (`SiteEnergyUse(kBtu)`)
- Encodage des variables catégorielles (`OneHotEncoder`)
- Normalisation des variables numériques (`StandardScaler`)
- Séparation du dataset en **train/test** (80 % / 20 %)
- Sauvegarde :
  - `X_train.csv`, `X_test.csv`
  - `y_train.csv`, `y_test.csv`

---

### 3️⃣ Modélisation supervisée
📘 *Notebook : `03_Modelisation.ipynb`*

**Objectif :** tester plusieurs modèles pour prédire la consommation d’énergie.

**Modèles testés :**
- Régression Linéaire  
- Ridge Regression  
- Forêt Aléatoire  

**Évaluation via validation croisée (`cross_validate`)**

| Modèle | R² moyen | MAE moyen |
|--------|-----------|-----------|
| Régression Linéaire | 0.62 | 15.3 |
| Ridge Regression | 0.65 | 14.9 |
| 🌳 Forêt Aléatoire | **0.82** | **11.7** |

🟢 Le meilleur modèle est la **Forêt Aléatoire**.

---

### 4️⃣ Optimisation et interprétation
📘 *Notebook : `04_Optimisation_Interpretation.ipynb`*

**Objectif :**
Optimiser le modèle sélectionné et analyser les variables les plus importantes.

**Actions réalisées :**
- Optimisation des hyperparamètres via `GridSearchCV`
- Évaluation finale sur le jeu de test
- Calcul de la performance :
  - `R² = 0.84`
  - `MAE = 10.9`
- Visualisation des *feature importances* :  
  les variables les plus influentes sont la **surface totale**, **l’année de construction**, et le **type de propriété**.

---

## 📈 Synthèse des résultats
✅ Le modèle final (Random Forest optimisé) prédit la consommation énergétique avec une bonne précision.  
🏢 Les caractéristiques structurelles expliquent bien les variations de consommation entre bâtiments.

---

## 🧰 Technologies utilisées

| Domaine | Librairies |
|----------|------------|
| Manipulation de données | `pandas`, `numpy` |
| Visualisation | `matplotlib`, `seaborn` |
| Machine Learning | `scikit-learn`, `xgboost` |
| Environnement | `jupyter`, `ipykernel` |

---

## ⚙️ Installation rapide

###  Cloner le dépôt
```bash
git clone https://github.com/sjbl69/Seattle_Building_Energy_Prediction.git
cd Seattle_Building_Energy_Prediction
