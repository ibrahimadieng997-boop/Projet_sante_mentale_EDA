<div align="center">

# 🧠 Consommation de drogues chez les jeunes

### Analyse exploratoire des données d'un centre de santé mentale

*600 jeunes patients · 19 variables · 1 question : qu'est-ce qui est associé à la dépendance ?*

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?logoColor=white)
![Statut](https://img.shields.io/badge/Statut-EDA%20termin%C3%A9e-2EA44F)

</div>

---

## 📌 Résumé

La consommation de substances chez les adolescents et jeunes adultes est un enjeu majeur de santé publique. Ce projet analyse les données de **600 jeunes patients** suivis dans un centre de santé mentale afin de comprendre **qui sont ces patients, comment ils consomment, et quels facteurs sont associés à leur niveau de dépendance**.

Le travail suit la démarche complète d'une analyse exploratoire professionnelle : **inspection de la qualité des données, nettoyage, analyse univariée, analyse bivariée et tests statistiques**, avec une interprétation médicale et méthodologique de chaque résultat.

> 🎯 **Choix assumé :** il ne s'agit pas de prédire le type de drogue, mais de **poser des bases statistiques rigoureuses** avant toute modélisation.

## 🧭 Problématique

> **Quels profils, quels comportements et quels contextes sont associés à un score de dépendance (SDS) élevé chez les jeunes patients ?**

Le **score SDS** mesure la gravité de la dépendance d'une personne à une substance. Il est la variable centrale de l'étude (valeurs de 0 à 13).

## 🗃️ Les données

| Caractéristique | Valeur |
|---|---|
| Patients | **600** |
| Variables | **19** (9 catégorielles · 10 numériques) |
| Doublons | 0 |
| Valeurs manquantes | 80 cellules, uniquement sur `age_premiere_consommation` (13,3 %) |
| Fichier | `data/dataset_consommation_drogues_jeunes.csv` (séparateur `;`) |

| Thème | Variables |
|---|---|
| 👤 **Profil** | `age`, `sexe`, `niveau_scolaire`, `milieu_residence`, `situation_familiale` |
| 💊 **Consommation** | `type_drogue_principale`, `frequence_consommation`, `age_premiere_consommation`, `duree_consommation_mois`, `score_dependance_SDS` |
| 🧠 **Santé mentale** | `score_estime_soi`, `score_qualite_vie`, `score_anxiete_HAM_A` |
| 👨‍👩‍👧 **Environnement** | `soutien_familial`, `influence_pairs`, `antecedents_familiaux_addiction`, `revenu_familial_fcfa`, `heures_reseaux_sociaux_jour` |

## 🧹 Préparation des données

| Étape | Action |
|---|---|
| **Doublons** | Aucun détecté, aucune ligne supprimée |
| **Cohérence des modalités** | Casse harmonisée sur `sexe` (« FEMME » / « HOMME » → « Femme » / « Homme ») |
| **Valeurs aberrantes** | Méthode IQR avec winsorisation sur le revenu familial |
| **Valeurs manquantes** | Identifiées et conservées, à traiter avant modélisation |
| **Valeurs extrêmes médicales** | Durées de consommation très longues conservées : profils chroniques plausibles, non des erreurs |

---

## 🔍 Analyse univariée : que contient l'échantillon ?

### 🎯 Score de dépendance SDS

| Moyenne | Médiane | Écart-type | Min | Max | Asymétrie |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 2,51 | 2 | 2,41 | 0 | 13 | +1,41 |

**Lecture :** la distribution est concentrée à gauche avec une longue queue vers la droite. **La grande majorité des patients présente une dépendance faible** (scores entre 0 et 3) ; seule une minorité dépasse 6, et les cas au-delà de 8 sont des valeurs atypiques.

### 📈 Variables numériques

| Variable | Médiane | Constat |
|---|:---:|---|
| **Revenu familial** | ≈ 95 600 FCFA | Majorité de ménages modestes à modérés, minorité à hauts revenus |
| **Durée de consommation** | 12,4 mois | Deux pics (0 à 5 mois, 9 à 14 mois), consommateurs chroniques jusqu'à 68 mois |
| **Réseaux sociaux** | 4 h / jour | Distribution quasi symétrique, 3 à 5 h pour la majorité, usages extrêmes rares |
| **Qualité de vie** | ≈ 82 / 100 | Majorité satisfaite, petit groupe à très faible qualité de vie |
| **Âge de 1re consommation** | 19 ans | 50 % ont commencé entre 16 et 21 ans, certains dès **11 ans** |

### 🏷️ Variables catégorielles

**Type de drogue principale**

```
Alcool            ██████████████████████████████  30,3 %  (182)
Cannabis          ███████████████████████         23,2 %  (139)
Tabac             █████████████████████▌          21,8 %  (131)
Aucune            █████████████▎                  13,3 %  ( 80)
Solvants / colle  ███████▋                         7,7 %  ( 46)
Amphétamines      ███▋                             3,7 %  ( 22)
```

**Fréquence de consommation**

```
Jamais            ████████████████████████▋       24,7 %  (148)
Occasionnelle     ██████████████████████          22,0 %  (132)
Hebdomadaire      ███████████████████▌            19,5 %  (117)
Mensuelle         █████████████████▊              17,8 %  (107)
Quotidienne       ████████████████                16,0 %  ( 96)
```

**Contexte social**

| Variable | Répartition |
|---|---|
| **Soutien familial** | Oui 59,3 % · Non 40,7 % |
| **Milieu de résidence** | Urbain 67,2 % · Rural 32,8 % |
| **Niveau scolaire** | Lycée 29,2 % · Collège 23,5 % · Université 21,7 % · Déscolarisé 14,0 % · Formation pro. 11,7 % |

**À retenir :** l'alcool, le cannabis et le tabac couvrent plus de 75 % des cas ; 75,3 % des patients déclarent une consommation active ; plus de 40 % n'ont pas de soutien familial.

---

## 🔗 Analyse bivariée : quels facteurs sont liés à la dépendance ?

Les distributions n'étant pas normales et les variances hétérogènes, des **tests non paramétriques** ont été retenus plutôt que l'ANOVA ou le test de Pearson.

| Relation étudiée | Test | Résultat | Conclusion |
|---|---|---|---|
| Âge de 1re consommation × SDS | Spearman | ρ = 0,059 · p = 0,180 | ❌ **Pas de lien significatif** |
| Fréquence de consommation × SDS | Kruskal-Wallis | H = 102,25 · p = 3,26 × 10⁻²¹ | ✅ **Lien très significatif** |
| Type de drogue × SDS | Kruskal-Wallis | H = 183,16 · p = 1,13 × 10⁻³⁷ | ✅ **Lien très significatif** |

### Ce que révèlent les comparaisons

- **Fréquence :** les patients qui ne consomment « jamais » ont les scores les plus bas (médiane proche de 0) ; les autres fréquences ont une médiane proche de 2 avec une forte dispersion.
- **Type de drogue :** cannabis, tabac et alcool ont une médiane autour de 2 ; les **solvants/colle** se distinguent avec la médiane la plus élevée (≈ 3) et la plus grande dispersion ; les **amphétamines** montrent des scores plus faibles et moins dispersés.
- **Âge de première consommation :** malgré l'intuition courante, aucune relation monotone n'est détectée dans cet échantillon.

---

## 💡 Conclusions

1. 📉 **La dépendance est faible pour la majorité des patients**, avec un petit groupe à risque élevé qui mérite une attention particulière.
2. 🔗 **La fréquence et le type de substance** sont fortement associés au score de dépendance.
3. 🧒 **L'âge de première consommation** n'explique pas, à lui seul, le niveau de dépendance.
4. ⚠️ **Une initiation dès 11 ans** existe : un signal pour cibler la prévention dès l'adolescence.
5. 👨‍👩‍👧 Plus de **40 % des patients sans soutien familial** : un levier d'accompagnement à explorer.

## ⚠️ Limites

- Une EDA révèle des **associations, pas des causalités**.
- **Déséquilibre de classes** : amphétamines (3,7 %) et solvants/colle (7,7 %) sont peu représentés, d'où une prudence sur les conclusions les concernant.
- **13,3 % de valeurs manquantes** sur l'âge de première consommation.
- Échantillon issu d'**un seul centre** : généralisation à prouver.

## 🔮 Perspectives

- Imputer les valeurs manquantes
- Étudier les liens avec la **qualité de vie**, l'**anxiété (HAM-A)**, l'**estime de soi**, le **soutien familial** et l'**influence des pairs**
- Construire des **modèles explicatifs** (régression) puis **prédictifs**
- Développer un tableau de bord interactif (Streamlit)

## 🛠️ Compétences démontrées

| Domaine | Détail |
|---|---|
| **Data cleaning** | Doublons, incohérences, valeurs manquantes, winsorisation (IQR) |
| **Statistiques** | Analyse univariée et bivariée, tests de Spearman et Kruskal-Wallis |
| **Python** | Pandas, NumPy, SciPy, Matplotlib, Seaborn |
| **Esprit critique** | Choix de tests justifié, prudence causale, limites explicites |
| **Communication** | Rapport de 22 pages avec interprétation de chaque résultat |

## 🗂️ Structure du dépôt

```
├── README.md
├── data/
│   └── dataset_consommation_drogues_jeunes.csv
├── Rapport_Santé_mentale.pdf      # Rapport complet (22 pages)
└── notebook.ipynb                 # Code de l'analyse
```

## 🚀 Reproduire l'analyse

```bash
git clone https://github.com/ibrahimadieng997-boop/Projet_sante_mentale_EDA.git
cd Projet_sante_mentale_EDA
pip install pandas numpy scipy matplotlib seaborn jupyter
jupyter notebook notebook.ipynb
```

> 💡 Le CSV utilise le séparateur `;` : `pd.read_csv("data/dataset_consommation_drogues_jeunes.csv", sep=";", encoding="latin-1")`

## 👤 Auteur

**Ibrahima Dieng**
Junior en Data Science et Intelligence Artificielle

📍 Thiès, Médina Fall, Sénégal
💻 GitHub : [ibrahimadieng997boop](https://github.com/ibrahimadieng997boop)
✉️ [ibrahimadieng997@gmail.com](mailto:ibrahimadieng997@gmail.com)

---

<div align="center">

⭐ *Ce projet vous plaît ? Laissez une étoile, et n'hésitez pas à me contacter !*

</div>
