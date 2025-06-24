## BSQ (Biggest Square)

[![GitHub repo](https://img.shields.io/badge/GitHub-Big--Square-blue?logo=github)](https://github.com/s2adr/Big-Square)

**BSQ** est un projet de la piscine 42 dont l’objectif est de détecter et d’afficher le plus grand carré possible dans une carte composée de cases vides et d’obstacles.

---

## Table des matières

- [Description](#description)
- [Installation](#installation)
- [Compilation](#compilation)
- [Usage](#usage)
- [Format de la map](#format-de-la-map)
- [Exemples](#exemples)
- [Algorithme](#algorithme)
- [Auteur](#auteur)

---

## Description

Le programme lit une ou plusieurs cartes depuis des fichiers texte ou l’entrée standard, chaque carte étant constituée de lignes de mêmes longueurs.\
Chaque caractère représente :

- `.` : une case vide  
- `o` : un obstacle

Le but est de repérer le plus grand carré constitué uniquement de cases vides et de l’afficher en remplaçant les `.` qui le composent par `x`.

---

## Installation

1. **Récupérer le dépôt**

   ```bash
   git clone https://github.com/s2adr/Big-Square.git
   cd Big-Square
   ```

2. **Prérequis**

   - Un compilateur C (gcc ou clang)
   - Make

---

## Compilation

- **Avec Makefile**

  ```bash
  make
  ```

---

## Usage

Pour générer une map, il faut utiliser le script Perl `gen_map.pl`, de la façon suivante :

```bash
./gen_map.pl x y z > fichier_contenant_la_map
```

x => correspond au nombre de lignes.\
y => correspond au nombre de colonnes.\
z => correspond à la densité des obstacles sur la map.

```bash
# Lire depuis un fichier
./bsq map

# Plusieurs fichiers
./bsq map map2

# Lire depuis stdin
gen_map.pl 10 12 3 | ./bsq
```

- Si plusieurs fichiers sont passés en argument, le programme traite chaque carte séparément.
- En cas d’erreur (fichier non trouvé, format invalide), un message est affiché sur la sortie d’erreur.

---

## Format de la map

Le fichier commence par une ligne d’en-tête indiquant :

```
<nombre_de_lignes><caractère_vide><caractère_obstacle><caractère_plein>
```

- `<nombre_de_lignes>` : nombre total de lignes de la carte (entier positif)
- `<caractère_vide>`   : caractère représentant une case vide (typiquement `.`)
- `<caractère_obstacle>` : caractère pour obstacle (typiquement `o`)
- `<caractère_plein>`    : caractère utilisé pour dessiner le plus grand carré (typiquement `x`)

Exemple :

```
9.ox
..............................
...o................o.........
...............o..............
..............................
...............o..............
..............................
......o.......................
...............o..............
..............................
```

---

## Exemples

**Carte d’entrée :**

```
4.ox
.........
.o.......
.........
.........
```

**Sortie attendue :**

```
.........
.o....xxx
......xxx
......xxx
```

Même si ça ne ressemble pas vraiment à un carré, ça en est un, tant qu'il y a le même nombre de caracteres en lignes et en colonnes, le carré est défini. (Sur l'exemple ci-dessous on voit un carré 3x3)

---

## Algorithme

1. Lecture et validation de la carte
2. Conversion en matrice d’entiers
3. Application de la programmation dynamique
4. Recherche de la plus grande valeur
5. Remplacement des `.` par `x`
6. Affichage final

---

## Auteur

**Saad Idrissi**  
Projet réalisé pendant la piscine 42.
