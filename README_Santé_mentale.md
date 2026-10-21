<div align="center">

# 🧠 Consommation de drogues chez les jeunes
### Analyse exploratoire (EDA) d'un centre de santé mentale

*Que nous disent les données de 600 jeunes patients sur la dépendance, le mode de vie et le contexte social ?*

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![Statut](https://img.shields.io/badge/Statut-EDA%20termin%C3%A9e-2EA44F)

</div>

---

## 🎯 Le projet en 30 secondes

Un centre de santé mentale a collecté des données sur **600 jeunes patients** : profil, contexte familial, consommation de substances, scores psychologiques.

L'objectif n'est **pas de prédire** le type de drogue, mais de **poser des bases statistiques solides** : nettoyer les données, comprendre chaque variable (analyse **univariée**), puis étudier les liens entre variables (analyse **bivariée**), en lien avec le **score de dépendance SDS**.

> **SDS** : score mesurant la gravité de la dépendance d'une personne à une substance.

## 📊 Le jeu de données

| | |
|---|---|
| **Patients** | 600 |
| **Variables** | 19 (9 catégorielles, 10 numériques) |
| **Doublons** | 0 |
| **Valeurs manquantes** | 80 (uniquement `age_premiere_consommation`, soit 13,3 %) |
| **Variable étudiée** | `score_dependance_SDS` |

**Catégorielles :** sexe, niveau scolaire, milieu de résidence, situation familiale, type de drogue principale, fréquence de consommation, influence des pairs, antécédents familiaux d'addiction, soutien familial.
**Numériques :** âge, âge de première consommation, durée de consommation (mois), score SDS, estime de soi, qualité de vie, anxiété (HAM-A), heures sur les réseaux sociaux/jour, revenu familial (FCFA).

### Qualité des données

<p align="center"><img src="assets/valeurs_manquantes.png" width="45%" alt="Carte des valeurs manquantes"></p>

## 🧹 Nettoyage

- **Doublons :** aucun détecté
- **Incohérences de saisie :** harmonisation de la casse sur la variable sexe (« FEMME », « HOMME » → « Femme », « Homme »)
- **Valeurs aberrantes :** méthode IQR (winsorisation) sur le revenu familial
- **Valeurs manquantes :** conservées et signalées, à traiter avant toute modélisation

---

## 🔍 Analyse univariée

### Variable cible : score de dépendance SDS

Moyenne **2,51** · Médiane **2** · Min 0 · Max 13 · Asymétrie **+1,41**

<p align="center">
<img src="assets/sds_hist.png" width="48%" alt="Histogramme SDS">
<img src="assets/sds_box.png" width="48%" alt="Boxplot SDS">
</p>

💡 La grande majorité des patients a une **dépendance faible** (scores entre 0 et 3). Seule une minorité dépasse 6 : ce sont les valeurs atypiques du boxplot.

### Variables quantitatives

**Revenu familial (FCFA)** : médiane ≈ 95 600, distribution étalée vers la droite.

<p align="center">
<img src="assets/revenu_hist.png" width="48%" alt="Histogramme revenu">
<img src="assets/revenu_box.png" width="48%" alt="Boxplot revenu">
</p>

**Durée de consommation (mois)** : médiane 12,4 mois, avec des consommateurs chroniques jusqu'à 68 mois (valeurs plausibles, conservées).

<p align="center">
<img src="assets/duree_hist.png" width="48%" alt="Histogramme durée">
<img src="assets/duree_box.png" width="48%" alt="Boxplot durée">
</p>

**Heures sur les réseaux sociaux / jour** : distribution quasi symétrique centrée sur **4 h** ; la majorité des jeunes passe entre 3 et 5 h.

<p align="center">
<img src="assets/reseaux_hist.png" width="48%" alt="Histogramme réseaux sociaux">
<img src="assets/reseaux_box.png" width="48%" alt="Boxplot réseaux sociaux">
</p>

**Score de qualité de vie** : médiane ≈ 82 / 100, avec un sous-groupe minoritaire à qualité de vie nettement plus faible.

<p align="center">
<img src="assets/qualite_hist.png" width="48%" alt="Histogramme qualité de vie">
<img src="assets/qualite_box.png" width="48%" alt="Boxplot qualité de vie">
</p>

**Âge de première consommation** : médiane **19 ans**, 50 % des patients ont commencé entre 16 et 21 ans, certains dès **11 ans**, ce qui souligne l'enjeu de prévention dès l'adolescence.

<p align="center">
<img src="assets/age1ere_hist.png" width="48%" alt="Histogramme âge première consommation">
<img src="assets/age1ere_box.png" width="48%" alt="Boxplot âge première consommation">
</p>

### Variables qualitatives

**Type de drogue principale** : l'**alcool** domine (30,3 %), suivi du cannabis (23,2 %) et du tabac (21,8 %). Les amphétamines (3,7 %) et solvants/colle (7,7 %) sont rares.

<p align="center"><img src="assets/type_drogue.png" width="60%" alt="Type de drogue"></p>

**Fréquence de consommation** : répartition équilibrée ; 75,3 % des patients déclarent une consommation active.

<p align="center"><img src="assets/frequence.png" width="60%" alt="Fréquence de consommation"></p>

**Contexte social**

| Soutien familial | Milieu de résidence |
|:---:|:---:|
| <img src="assets/soutien_pie.png" width="100%" alt="Soutien familial"> | <img src="assets/milieu_pie.png" width="100%" alt="Milieu de résidence"> |
| 59,3 % ont un soutien familial | 67,2 % vivent en milieu urbain |

**Niveau scolaire** : lycée (29,2 %), collège (23,5 %), université (21,7 %), déscolarisés (14 %), formation professionnelle (11,7 %).

<p align="center"><img src="assets/scolaire_pie.png" width="45%" alt="Niveau scolaire"></p>

---

## 🔗 Analyse bivariée

### Âge de première consommation vs score SDS (numérique × numérique)

<p align="center"><img src="assets/bivar_age_sds.png" width="60%" alt="Âge première consommation vs SDS"></p>

Test de **Spearman** : ρ = 0,059 ; p = 0,180.
➡️ **Pas de corrélation significative** : l'âge de début n'explique pas à lui seul le niveau de dépendance.

### Fréquence de consommation vs score SDS (catégoriel × numérique)

<p align="center"><img src="assets/bivar_freq_sds.png" width="70%" alt="SDS selon la fréquence"></p>

Test de **Kruskal-Wallis** : H = 102,25 ; p = 3,26 × 10⁻²¹.
➡️ **Lien significatif.** Les patients qui ne consomment « jamais » ont les scores les plus bas (médiane proche de 0).

### Type de drogue vs score SDS (catégoriel × numérique)

<p align="center"><img src="assets/bivar_type_sds.png" width="70%" alt="SDS selon le type de drogue"></p>

Test de **Kruskal-Wallis** : H = 183,16 ; p = 1,13 × 10⁻³⁷.
➡️ **Lien significatif.** Les solvants/colle ont la médiane la plus élevée (≈ 3) et la plus grande dispersion ; les amphétamines montrent des scores plus faibles et moins dispersés.

> Le test non paramétrique de Kruskal-Wallis a été préféré à l'ANOVA car les distributions ne sont pas normales et les variances sont hétérogènes.

---

## ✅ Ce qu'il faut retenir

1. La dépendance (SDS) est **faible pour la majorité**, avec un petit groupe à risque élevé.
2. La **fréquence** et le **type** de substance sont significativement liés au score SDS.
3. L'**âge de première consommation** n'est pas corrélé au SDS dans cet échantillon.
4. Une consommation **précoce dès 11 ans** existe : cible de prévention.

## ⚠️ Limites

- L'EDA met en évidence des **associations, pas des causalités**.
- **Déséquilibre de classes** : amphétamines et solvants/colle sont peu représentés, d'où une prudence sur les conclusions les concernant.
- 13,3 % de valeurs manquantes sur l'âge de première consommation.

## 🔮 Suite du projet

- Traiter les valeurs manquantes (imputation)
- Étudier d'autres variables : qualité de vie, anxiété (HAM-A), estime de soi, soutien familial, influence des pairs
- Construire des modèles explicatifs ou prédictifs sur des bases solides

## 🛠️ Compétences démontrées

`Python` · `Pandas` · `Nettoyage de données` · `Analyse univariée et bivariée` · `Matplotlib / Seaborn` · `Tests statistiques non paramétriques (Spearman, Kruskal-Wallis)` · `Interprétation et communication des résultats`

## 🗂️ Structure du dépôt

```
├── README.md
├── assets/                     # Graphiques de l'analyse
├── data/
│   └── dataset_consommation_drogues_jeunes.csv
├── Rapport_Santé_mentale.pdf   # Rapport complet (22 pages)
└── notebook.ipynb              # Code de l'analyse
```

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
