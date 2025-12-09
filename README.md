# Évaluation Finale : Logique d'Analyse et d'Automatisation (3 Heures)

**Objectif :** Évaluer la capacité à construire des étapes logiques d'analyse de données (`dplyr`, `ggplot2`) et à appliquer les fonctions de Web Scraping (`rvest`) et de manipulation de chaînes de caractères (`gsub`, `paste0`, `strsplit`). L'accent est mis sur la logique d'enchaînement des opérations et la compréhension des fonctions.

**Consignes :**

* Vous avez accès à votre script de cours complet.
* Vous devez répondre aux questions en écrivant le **code logique** ou en **décrivant clairement** la séquence d'opérations nécessaires, en utilisant les noms de fonctions (ex : `filter()`, `mutate()`).
* **Données utilisées :** `arbres_clean` (pour les Exercices 1 & 2) et un script incomplet pour l'Exercice 3.

---

## 💻 Exercice 1 : Chaîne de Traitement des Données (`dplyr`) 

Cet exercice teste votre capacité à manipuler et transformer le *dataframe* `arbres_clean` en utilisant les verbes `dplyr`.

### Question 1.1 : Préparation et Ajout d'une Colonne Géographique (30 points)

Le jeu de données initial `arbres` (avant `clean_names()`) contient une colonne nommée **`geo_point_2d`** au format texte, par exemple `"48.8589, 2.3411"`.

Votre objectif est de créer un nouveau *dataframe* appelé **`arbres_prep_geo`** qui :

1.  Conserve **uniquement** les arbres dont la colonne **`remarquable` n'est pas manquante (`NA`)**.
2.  Ajoute **deux nouvelles colonnes numériques** : **`latitude`** et **`longitude`**, en séparant la colonne `geo_point_2d`.
3. 

### Question 1.2 : Réorganisation et Renommage 

En partant du *dataframe* **`arbres_prep_geo`** :

1.  **Renommez** la colonne **`arrondissement`** en **`a_r_r`**.
2.  **Déplacez** la colonne **`genre`** pour qu'elle soit la **première** colonne du *dataframe*, suivie immédiatement par la colonne **`espece`**.

### Question 1.3 : Récapitulatif Statistique Avancé 

À partir du *dataframe* **`arbres_prep_geo`**, générez un tableau de synthèse (`resume_stade`) qui, **pour chaque `stade_de_developpement`** (sans inclure les `NA`) :

1.  Compte le **nombre total** d'arbres (`n_arbres`).
2.  Calcule la **circonférence moyenne** (`moy_circ`).
3.  Calcule la **proportion** d'arbres **remarquables** (`prop_remarquable = n_remarquables / n_arbres`).

Enfin, triez ce tableau par `prop_remarquable` **décroissante**.

### Question 1.4 : Filtrage Spécifique et Compte 

Vous voulez identifier le **genre** le plus fréquent (celui qui apparaît le plus souvent) **uniquement** parmi les arbres qui remplissent **toutes** ces conditions :

* Sont considérés comme **Remarquables** (`remarquable == "OUI"`).
* Ont une **hauteur** (`hauteur_m`) strictement **supérieure à $20$ mètres**.
* Sont situés dans la **`domanialite`** "Jardin".

## 💻 Exercice 2 : Logique de visualisation avec ggplot2

### Question 2.1 : Structure de Visualisation par Facette 

En utilisant le *dataframe* **`arbres_prep_geo`**, écrivez le code `ggplot2` pour réaliser une **série de graphiques de densité** qui montrent la distribution de la **`hauteur_m`** pour chaque catégorie de **`remarquable`** ("OUI" ou "NON"), en séparant l'affichage **par arrondissement** (`arrondissement`).

Vous devez :
1.  Utiliser un graphique de densité (`geom_density`).
2.  Utiliser `facet_grid()` pour séparer les graphiques par arrondissement.
3.  Laisser les échelles de l'axe X des hauteurs **libres** entre les arrondissements.

### Question 2.2 : Interprétation d'un Graphique en Violon et Code (40 points)

Considérez le graphique en violon (Violin Plot) ci-dessous, qui compare la distribution de la **`hauteur_m`** (en Y) selon le **`domanialite`** (en X).

1.  **Code `ggplot2` pour obtenir ce graphique :** Écrivez la séquence de code nécessaire pour générer un graphique en violon comparant la distribution de la `hauteur_m` par `domanialite`. (Vous pouvez ignorer les thèmes et les limites d'axes.)
2.  **Interprétation :** En observant la forme du violon, décrivez la différence entre une catégorie où le violon est **très large et évasé aux extrémités** et une catégorie où il est **étroit au centre mais avec deux "bosses" distinctes (bimodal)**.

3.  # Exercice 3 : Logique de Web Scraping et Manipulation de Texte (1h15)

Cet exercice évalue votre compréhension et votre capacité à compléter un script d'automatisation. On utilise des données fictives de prix et de tailles de parcelles d'arbres sur une seule page.

---

### Question 3.1 : Ciblage HTML (rvest) (30 points)

Nous cherchons à extraire les titres des parcelles et leurs prix de la page. Ecrivez le code pour réaliser cette tâche

Le HTML de la page est structuré comme suit :

```html
<div class="parcel">
  <h2 class="title">Parcelle A - Chêne</h2>
  <span class="size">12 m²</span>
  <span class="price">Prix : 1500 €</span>
</div>
<div class="parcel">
  <h2 class="title">Parcelle B - Érable</h2>
  <span class="size">8 m²</span>
  <span class="price">Prix : 950 €</span>
</div>
```

---

### Question 3.2 : Nettoyage de Texte avec Expressions Régulières (45 points)

Le vecteur `prix` obtenu est : `c("Prix : 1500 €", "Prix : 950 €", "Prix : 2000 €")`.

Votre objectif est de convertir ce vecteur en un **vecteur numérique** ne contenant que les valeurs `1500`, `950`, `2000`.

Complétez le script en utilisant la fonction `gsub()` et la conversion `as.numeric()`.

```r
# Étape 1 : Supprimer tout ce qui n'est pas un nombre
prix_nettoye <- gsub(
    # Pattern : Matcher "Prix : " au début ET " €" à la fin
    "Prix : | €", 
    # Remplacement : Remplacer par rien (chaine vide)
    "", 
    prix)

# Étape 2 : Conversion
prix_numerique <- as.numeric(prix_nettoye)

