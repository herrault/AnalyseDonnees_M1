# 🌳 Évaluation Finale : Logique d'Analyse et d'Automatisation (3 Heures)

**Objectif :** Évaluer la capacité à construire des étapes logiques d'analyse de données (`dplyr`, `ggplot2`) et à appliquer les fonctions de Web Scraping (`rvest`) et de manipulation de chaînes de caractères (`gsub`, `paste0`, `strsplit`). L'accent est mis sur la logique d'enchaînement des opérations et la compréhension des fonctions.

**Consignes :**

* Vous avez accès à votre script de cours complet.
* Vous devez répondre aux questions en écrivant le **code logique** ou en **décrivant clairement** la séquence d'opérations nécessaires, en utilisant les noms de fonctions (ex : `filter()`, `mutate()`).
* **Données utilisées :** `arbres_clean` (pour les Exercices 1 & 2) et un script incomplet pour l'Exercice 3.

---

## 💻 Exercice 1 : Chaîne de Traitement des Données (`dplyr`) (1h15)

Cet exercice teste votre capacité à manipuler et transformer le *dataframe* `arbres_clean` en utilisant les verbes `dplyr`.

### Question 1.1 : Préparation et Ajout d'une Colonne Géographique (30 points)

Le jeu de données initial `arbres` (avant `clean_names()`) contient une colonne nommée **`geo_point_2d`** au format texte, par exemple `"48.8589, 2.3411"`.

Votre objectif est de créer un nouveau *dataframe* appelé **`arbres_prep_geo`** qui :

1.  Conserve **uniquement** les arbres dont la colonne **`remarquable` n'est pas manquante (`NA`)**.
2.  Ajoute **deux nouvelles colonnes numériques** : **`latitude`** et **`longitude`**, en séparant la colonne `geo_point_2d`.

**Code logique (`dplyr` et fonctions de base) :**

```r
arbres_clean %>%
  # 1. Conserver uniquement les lignes non manquantes
  filter(!is.na(remarquable)) %>%
  # 2. Créer la latitude et la longitude à partir de geo_point_2d
  mutate(
    # Séparer la chaîne de caractères par la virgule (,)
    coords = strsplit(geo_point_2d, split = ","),
    # Extraire la première partie (Latitude) et la convertir en numérique
    latitude = as.numeric(sapply(coords, "[", 1)),
    # Extraire la deuxième partie (Longitude) et la convertir en numérique
    longitude = as.numeric(sapply(coords, "[", 2))
  ) %>%
  select(-coords) # Optionnel : Retirer la colonne temporaire 'coords'
