# 📊 Carte de Risque IA - Analyse Avancée de Risque Financier

## 📋 Contexte du Projet

Ce projet a été réalisé dans le cadre d'une **deuxième mission de stage en analyse de données avec Python**. Il s'agit d'une solution complète d'analyse de risque financier d'entreprises, combinant des approches traditionnelles de scoring métier avec des techniques avancées de Machine Learning et de détection d'anomalies.

### 🎯 Objectif Principal

Développer une **Carte de Risque IA** permettant d'évaluer et de classifier le niveau de risque financier d'entreprises en se basant sur leurs indicateurs financiers clés. La solution combine :
- 📊 **Analyse métier** : Scoring basé sur des règles métier et ratios financiers
- 🤖 **Intelligence Artificielle** : Modèles de Machine Learning pour prédiction de risque
- 🔍 **Détection d'anomalies** : Identification automatique de comportements financiers atypiques
- 📈 **Visualisation interactive** : Dashboard Streamlit pour exploration des données

---

## 🚀 Méthodologie & Pipeline d'Analyse

Le projet suit une approche structurée en **4 étapes principales** :

### **Étape 1 : Prétraitement & Feature Engineering** 🧹

#### 1.1 Chargement et Exploration des Données
- Importation des données depuis `Data_09092025.xlsx`
- Analyse exploratoire (shape, types, distributions)
- Identification des valeurs manquantes

#### 1.2 Nettoyage des Données
- Détection des valeurs aberrantes (méthode IQR + Isolation Forest)
- Traitement des outliers par secteur d'activité
- Gestion des valeurs manquantes

#### 1.3 Normalisation par Secteur/Année
- Standardisation des indicateurs (Z-score) par secteur
- Normalisation temporelle pour comparaisons inter-annuelles
- Création d'indicateurs relatifs

#### 1.4 Création de Nouveaux Indicateurs
- **DSO-DPO** : Besoin en Fonds de Roulement (Délai clients - Délai fournisseurs)
- Ratios de rentabilité, liquidité et structure
- Indicateurs standardisés (Z-scores)

#### 1.5 Feature Store
Organisation des features par catégories :
- **Identifiants** : Nom, Activité, Année
- **Indicateurs Bruts** : Liquidité, Marge nette, IS/CA, RN/ACTIF, etc.
- **Indicateurs Standardisés** : Z-scores sectoriels
- **Indicateurs Dérivés** : DSO-DPO, ratios composites

#### 1.6 Export & Sauvegarde
- Sauvegarde du Feature Store : `Feature_Store_Carte_Risque_v1.csv`
- Création de métadonnées (version, date, statistiques)

---

### **Étape 2 : Scoring Avancé** 🎯

#### 2.1 Scoring Métier Pondéré
Application de pondérations basées sur l'importance métier :
- **Liquidité** : 25%
- **Rentabilité** : 25% (Marge nette, RN/ACTIF)
- **BFR** : 20% (DSO-DPO)
- **Fiscalité** : 15% (IS/CA)
- **Structure** : 15% (Ratio immobilisations)

#### 2.2 Machine Learning Supervisé
- **Création de labels** : Classification binaire (Risque Haut vs Bas) basée sur le score métier
- **Modèles utilisés** :
  - Random Forest Classifier (haute performance)
  - Régression Logistique (interprétabilité)
- **Validation** : Cross-validation, métriques de performance

#### 2.3 Score Hybride Final
- Combinaison : **60% Score Métier + 40% Score ML**
- Classification en 4 catégories :
  - 🟢 **Risque Faible**
  - 🟡 **Risque Modéré**
  - 🟠 **Risque Élevé**
  - 🔴 **Risque Critique**

---

### **Étape 3 : Détection d'Anomalies** 🔍

Application de **3 algorithmes complémentaires** :

#### 3.1 Isolation Forest
- Détection d'anomalies globales
- Basé sur l'isolation des points atypiques

#### 3.2 Local Outlier Factor (LOF)
- Détection d'anomalies locales
- Analyse de la densité locale des points

#### 3.3 DBSCAN
- Clustering spatial
- Identification des points hors clusters

#### 3.4 Indice d'Anomalie Consolidé
- Agrégation des 3 méthodes
- Score consolidé d'anomalie (0-1)
- Classification binaire : Normal vs Anomalie

---

### **Étape 4 : Visualisation & Dashboard Streamlit** 📈

#### Fonctionnalités du Dashboard
- **Vue d'ensemble** : Statistiques globales et distributions
- **Analyse par secteur** : Comparaisons inter-secteurs
- **Exploration individuelle** : Fiches entreprises détaillées
- **Visualisations interactives** :
  - Scatter plots (Score vs Anomalie)
  - Heatmaps de corrélation
  - Distributions de scores
  - Matrices de confusion

---

## 🛠️ Technologies & Librairies Utilisées

### Data Science & Machine Learning
- **pandas** : Manipulation et analyse de données
- **numpy** : Calculs numériques
- **scikit-learn** : Algorithmes de ML et preprocessing
  - `RandomForestClassifier`, `LogisticRegression`
  - `IsolationForest`, `LocalOutlierFactor`, `DBSCAN`
  - `StandardScaler`, `LabelEncoder`

### Visualisation
- **matplotlib** : Visualisations statiques
- **seaborn** : Visualisations statistiques avancées
- **plotly** : Graphiques interactifs
- **streamlit** : Dashboard web interactif

### Autres
- **jupyter** : Environnement de développement
- **openpyxl** : Lecture de fichiers Excel

---

## 📂 Structure du Projet

```
Mission_2_Carte_de_Risque_IA/
│
├── Mission_2_Carte_de_Risque_IA_Niveau_Avancé_Mohamadou_Hayatou.ipynb
│   └── Notebook principal contenant toute l'analyse (4 étapes)
│
├── Data_09092025.xlsx
│   └── Données source (indicateurs financiers des entreprises)
│
├── Feature_Store_Carte_Risque_v1.csv
│   └── Feature Store généré (étape 1)
│
├── Carte_Risque_IA_Finale.csv
│   └── Résultats finaux avec scores et classifications
│
├── dashboard.py
│   └── Application Streamlit pour visualisation interactive
│
├── requirements.txt
│   └── Liste des dépendances Python
│
└── README.md
    └── Documentation du projet (ce fichier)
```

---

## 🔧 Installation & Utilisation

### Prérequis
- Python 3.8+
- pip (gestionnaire de packages Python)

### Installation des dépendances

```bash
# Cloner le repository
git clone https://github.com/mohamadouhayatouabbassi-glitch/Mission_2_Carte_de_Risque_IA.ipynb.git
cd Mission_2_Carte_de_Risque_IA.ipynb

# Installer les dépendances
pip install -r requirements.txt
```

### Exécution du Notebook

```bash
# Lancer Jupyter Notebook
jupyter notebook

# Ouvrir le fichier :
# Mission_2_Carte_de_Risque_IA_Niveau_Avancé_Mohamadou_Hayatou.ipynb
```

### Lancement du Dashboard Streamlit

```bash
# Exécuter le dashboard
streamlit run dashboard.py

# Le dashboard s'ouvrira automatiquement dans votre navigateur
# Par défaut : http://localhost:8501
```

---

## 📊 Résultats & Insights Clés

### Indicateurs de Performance

#### Scoring Métier
- Distribution des scores : [0-100]
- Catégorisation en 4 niveaux de risque
- Pondération alignée avec les pratiques métier

#### Machine Learning
- **Accuracy** : Haute précision dans la classification de risque
- **Cross-validation** : Validation robuste du modèle
- **Feature Importance** : Identification des indicateurs les plus prédictifs

#### Détection d'Anomalies
- Taux d'anomalies détectées : ~10-15% des observations
- Consensus entre les 3 algorithmes pour les cas critiques
- Identification de patterns financiers atypiques

### Insights Business

1. **Liquidité & Rentabilité** : Indicateurs les plus discriminants pour le risque
2. **BFR (DSO-DPO)** : Fort impact sur la santé financière
3. **Variabilité sectorielle** : Importance de la normalisation par secteur
4. **Anomalies** : Détection précoce de situations financières critiques

---

## 🎓 Compétences Développées

Ce projet de stage a permis de développer et mettre en œuvre :

### Compétences Techniques
- ✅ Manipulation avancée de données avec **pandas**
- ✅ Feature engineering et preprocessing
- ✅ Implémentation d'algorithmes de Machine Learning supervisé
- ✅ Techniques de détection d'anomalies (unsupervised learning)
- ✅ Visualisation de données (matplotlib, seaborn, plotly)
- ✅ Développement de dashboards interactifs avec **Streamlit**

### Compétences Méthodologiques
- ✅ Approche structurée de résolution de problèmes
- ✅ Pipeline complet de Data Science (de l'exploration à la production)
- ✅ Validation et interprétation de modèles
- ✅ Combinaison d'approches métier et IA (score hybride)

### Compétences Business
- ✅ Compréhension des indicateurs financiers
- ✅ Analyse de risque d'entreprise
- ✅ Communication de résultats techniques à des non-experts
- ✅ Création de solutions orientées utilisateur final

---

## 🔮 Perspectives d'Amélioration

### Court terme
- [ ] Intégration de données temporelles (séries chronologiques)
- [ ] Ajout de features externes (secteur économique, région)
- [ ] Optimisation des hyperparamètres des modèles ML

### Moyen terme
- [ ] Déploiement du dashboard en production
- [ ] API REST pour intégration avec d'autres systèmes
- [ ] Système d'alertes automatiques pour anomalies critiques

### Long terme
- [ ] Modèles de Deep Learning (LSTM pour séries temporelles)
- [ ] Prédiction de défaillance d'entreprise (failure prediction)
- [ ] Analyse de sentiment sur données textuelles (rapports financiers)

---

## 👤 Auteur

**Mohamadou Hayatou Abbassi**

- Stagiaire en Analyse de Données avec Python
- Mission : Développement d'une Carte de Risque IA

---

## 📄 Licence

Ce projet a été développé dans le cadre d'un stage académique.

---

## 🙏 Remerciements

- Équipe encadrante pour les spécifications métier
- Communauté open-source pour les librairies utilisées
- Ressources pédagogiques en Data Science et Machine Learning

---

## 📞 Contact & Support

Pour toute question ou suggestion concernant ce projet :

- **GitHub Issues** : [Ouvrir une issue](https://github.com/mohamadouhayatouabbassi-glitch/Mission_2_Carte_de_Risque_IA.ipynb/issues)
- **Email** : [Contact via GitHub]

---

**Note** : Ce projet représente une première mission de stage et constitue une base solide pour des développements futurs dans le domaine de l'analyse de risque financier assistée par IA.
