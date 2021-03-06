+++
title = "Matrices"

date = 2018-09-09T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = true

[git]
  icon = "github"
  repo = "https://github.com/Bertbk/course_4m053"
  issue = "https://github.com/Bertbk/course_4m053/issues"
  prose = "https://prose.io/#Bertbk/course_4m053/edit/master/"

# Add menu entry to sidebar.
[menu.4m053]
  parent = "dense"
  identifier = "matrices_denses"
  name = "Matrices"
  weight = 15

+++

## Objectifs

1. Implémenter une classe `Matrice` pour manipuler des matrices carrées
2. Implémenter des opérations entre les classe `Matrice` et `Vecteur`

## Fichiers

Tout comme les vecteurs, il est largement préférable de créer un fichier header et un fichier source pour les matrices. 

## Stockage

La classe `Matrice` représente des matrices **carrées** (uniquement) et les stocke sous forme **dense**. Cette classe permettra d'effectuer des opérations matricielles (multiplication, ...). Elle contient comme données privées (au moins, libre à vous d'en ajouter):
 
- `int N_` : Le nombre de colonnes (= de lignes)
- `std::vector<double> coef_` : Les coefficients, stockés dans un tableau à une dimension de la bibliothèque standard

Les coefficients sont stockés de la façon suivante. Le coefficient positionné en $(i,j)$ dans la matrice sera à la position `i+j*N_` dans le vecteur de coefficients, où `N_` est le nombre de colonnes ou de lignes.

Comme pour la classe `Vecteur`, la classe `Matrice` comporte des constructeurs :
```c++
Matrice (); // constructeur vide
Matrice (int N); // constructeur créant une matrice nulle de taille N
Matrice (const Matrice & M); // constructeur par recopie
```
et un destructeur 
```c++
~Matrice() = default;
```

Le fichier header pour les matrices ressemble à

```cpp
// Fichier include/matrice.hpp
#pragma once
#include<vector> // pour les std::vector

class Matrice{
private:
  int N_;
  std::vector<double> coef_;
public: 
  Matrice (); // constructeur vide
  Matrice (int N); // constructeur créant une matrice nulle de taille N
  Matrice (const Matrice & M); // constructeur par recopie
  ~Matrice() = default;
};
```

## Quelques méthodes

- Méthode (constante) qui renvoie la taille de la matrice
- Méthode (constante) qui affiche la matrice dans le terminal
- Accesseurs :

```c++
double & operator() (int i, int j);     // Accès à la référence
double operator() (int i, int j) const; // Accès à la valeur (recopie)
```
Le premier permet d'accéder au coefficient de la matrice par référence (permettant une modification ultérieure) tandis que le second ne fait que renvoyer (une copie de) la valeur du coefficient.

{{% alert tips %}}
À partir de maintenant, vous ne devriez plus jamais accéder aux coefficients via `coef_` mais uniquement via les accesseurs ! Par exemple `A(i,j) = ...`.
{{% /alert %}}

## Opérations élémentaires

En mathématique, une matrice n'est pas qu'un tableau de coefficients et des opérations comme la multiplication ou l'addition sont possibles : Ne nous privons pas de les implémenter !

{{% alert exercise %}}
Améliorer votre classe `Matrice` avec les fonctionnalités suivantes :

1. L'addition et la soustraction entre deux matrices en surchargeant les opérateur `+` et `-`
2. La multiplication par une autre `Matrice`
3. La multiplication par un scalaire

Pour ces deux dernières opérations, vous pouvez soit construire un `operator` dans la classe (avec ou sans `friend`) ou à l'extérieure de celle-ci (comme pour les `Vecteur`).
{{% /alert %}}

## Produit Matrice-Vecteur

Implémentez le produit matrice vecteur sous forme d'un `operator` :
```c++
Vecteur operator*(const Matrice&, const Vecteur&);
```

{{% alert note %}}
N'oubliez pas, alors, d'inclure le fichier header des vecteurs.
{{% /alert %}}

{{% alert note %}}
Quelques astuces générales :

- Pensez à utiliser des références en argument pour éviter les copies inutiles d'objets qui peuvent être lourdes en mémoire, ce qui est le cas pour les matrices
- Dans le cas des références passées en argument, pensez à les déclarer constantes dans les cas pertinents
- De même, pensez à déclarer les méthodes de vos classes comme constantes dans les cas qui conviennent
{{% /alert %}}


