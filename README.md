## BSQ (Biggest Square)

**BSQ** est un projet de la piscine 42 dont l’objectif est de détecter et d’afficher le plus grand carré possible dans une carte composée de cases vides et d’obstacles.

---

## Table des matières

* [Description](#description)
* [Installation](#installation)
* [Compilation](#compilation)
* [Usage](#usage)
* [Format de la map](#format-de-la-map)
* [Exemples](#exemples)
* [Algorithme](#algorithme)
* [Tests](#tests)
* [Auteur](#auteur)

---

## Description

Le programme lit une ou plusieurs cartes depuis des fichiers texte ou l’entrée standard, chaque carte étant constituée de lignes de mêmes longueurs.
Chaque caractère représente :

* `.` : une case vide
* `o` : un obstacle

Le but est de repérer le plus grand carré constitué uniquement de cases vides et de l’afficher en remplaçant les `.` qui le composent par `x`.

---

## Installation

1. **Récupérer le dépôt**

   ```bash
   git clone https://github.com/s2adr/Big-Square.git
   cd Big-Square
   ```

2. **Prérequis**

   * Un compilateur C (gcc ou clang)
   * Make (optional, pour la facilité de compilation)

---

## Compilation

* **Avec Makefile**

  ```bash
  make
  ```

  Génère l’exécutable `bsq`.

* **Sans Makefile**

  ```bash
  gcc -Wall -Wextra -Werror -o bsq *.c
  ```

---

## Usage

```bash
# Lire depuis un fichier
./bsq maps/map01.txt

# Plusieurs fichiers
./bsq maps/map01.txt maps/map02.txt

# Lire depuis stdin
cat maps/map01.txt | ./bsq
```

* Si plusieurs fichiers sont passés en argument, le programme traite chaque carte séparément.
* En cas d’erreur (fichier non trouvé, format invalide), un message est affiché sur la sortie d’erreur et le programme continue avec le fichier suivant.

---

## Format de la map

Le fichier commence par une ligne d’en-tête indiquant :

```
<nombre_de_lignes><caractère_vide><caractère_obstacle><caractère_plein>
```

* `<nombre_de_lignes>` : nombre total de lignes de la carte (entier positif)
* `<caractère_vide>`   : caractère représentant une case vide (typiquement `.`)
* `<caractère_obstacle>` : caractère pour obstacle (typiquement `o`)
* `<caractère_plein>`    : caractère utilisé pour dessiner le plus grand carré (typiquement `x`)

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
....
.o..
....
....
```

**Sortie attendue :**

```
xxxx
xox.
xxxx
xxxx
```

---

## Algorithme

1. Lecture et validation de la carte
2. Conversion en matrice d’entiers
3. Application de la programmation dynamique :

   * Pour chaque cellule `(i, j)` vide, calcul de la taille du plus grand carré se terminant en `(i, j)`
   * `dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1`
4. Repérage de la plus grande valeur dans `dp`, et position du carré
5. Remplacement des `.` par le caractère plein dans la carte originale
6. Affichage de la carte modifiée

---

## Tests

* Fournis plusieurs fichiers de test dans le dossier `maps/`, couvrant :

  * Cartes entièrement vides
  * Cartes pleines d’obstacles
  * Cartes irrégulières (format invalide)
  * Cartes de grandes dimensions

* Tu peux automatiser les tests avec un script bash :

  ```bash
  #!/bin/bash
  for map in maps/*.txt; do
    echo "=== Test de $map ==="
    ./bsq "$map" || echo "Erreur sur $map"
  done
  ```

---

## Auteur

* **Saad** **Idrissi**

---
