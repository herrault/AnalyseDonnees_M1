# Évaluation Finale : Analyse de données avec R (3 Heures)

**Consignes :**

* Vous avez accès à votre script de cours complet.
* Vous devez répondre aux questions en écrivant le code demandé dans un script intitulé **script_reponse.R**. Organisez votre script en indiquant les balises des questions (**##1.1...**). Lorsqu'une inteprétation vous est demandée, écrivez votre texte précédé d'un #. Déposez votre script sur Moodle. 

---

## 💻 Exercice 1 : Chaîne de Traitement des Données (`dplyr`) 

### Question 1.1 : Préparation et Ajout d'une Colonne Géographique (30 points)

Le jeu de données initial `arbres` (avant `clean_names()`) contient une colonne nommée **`geo_point_2d`** au format texte, par exemple `"48.8589, 2.3411"`.

Votre objectif est de créer un nouveau *dataframe* appelé **`arbres_prep_geo`** qui :

1.  Conserve **uniquement** les arbres dont la colonne **`remarquable` n'est pas manquante (`NA`)**.
2.  Ajoute **deux nouvelles colonnes numériques** : **`latitude`** et **`longitude`**, en séparant la colonne `geo_point_2d`.

### Question 1.2 : Réorganisation et Renommage 

En partant du *dataframe* **`arbres_prep_geo`** ou **`arbres`** :

1.  **Renommez** la colonne **`arrondissement`** en **`a_r_r`**.
2.  **Déplacez** la colonne **`genre`** pour qu'elle soit la **première** colonne du *dataframe*, suivie immédiatement par la colonne **`espece`**.

### Question 1.3 : Récapitulatif Statistique Avancé 

À partir du *dataframe* **`arbres_prep_geo`** ou ou **`arbres`**, générez un tableau de synthèse (`resume_stade`) qui, **pour chaque `stade_de_developpement`** (sans inclure les `NA`) :

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

En utilisant le *dataframe* **`arbres`**, écrivez le code `ggplot2` pour réaliser une **série de graphiques de densité** qui montrent la distribution de la **`hauteur_m`** pour chaque catégorie de **`remarquable`** ("OUI" ou "NON"), en séparant l'affichage **par arrondissement** (`arrondissement`).

Vous devez :
1.  Utiliser un graphique de densité (`geom_density`).
2.  Utiliser `facet_grid()` pour séparer les graphiques par arrondissement.
3.  Laisser les échelles de l'axe X des hauteurs **libres** entre les arrondissements.

### Question 2.2 : Interprétation d'un Graphique en Violon et Code 

1. Écrivez la séquence de code nécessaire pour générer un graphique en violon comparant la distribution de la `hauteur_m` par `domanialite`. Limitez les valeurs de hauteur à 50m. 
2. Décrivez et interprétez la forme des groupes d'arbres localisés dans les cimetières, les alignements ou les périphériques. 

## 💻 Exercice 3 : Logique de Web Scraping et Manipulation de Texte 

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

Le vecteur `prix` correspond à: `c("Prix : 1500 €", "Prix : 950 €", "Prix : 2000 €")`.

Votre objectif est de convertir ce vecteur en un **vecteur numérique** ne contenant que les valeurs `1500`, `950`, `2000`.

1. Complétez le script en utilisant la fonction `gsub()` et la conversion `as.numeric()`.
2. Ecrivez une ligne pour constuire un data.frame contenant les trois valeurs avec les colonnes contenant les 3 noms de parcelle. 


