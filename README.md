# Guide de Référence - Calcul Symbolique avec SymPy

## Table des matières

1. [Manipulation d'expressions](#1-manipulation-dexpressions)
2. [Calcul différentiel](#2-calcul-différentiel)
3. [Calcul intégral](#3-calcul-intégral)
4. [Limites](#4-limites)
5. [Séries et développements](#5-séries-et-développements)
6. [Matrices et algèbre linéaire](#6-matrices-et-algèbre-linéaire)

---

## 1. Manipulation d'expressions

### Opérations principales

| Fonction | Description | Exemple |
|----------|-------------|---------|
| **`expand()`** | Développe les expressions (produits, puissances) | `expand((x+1)²)` → `x² + 2x + 1` |
| **`factor()`** | Factorise en produit de facteurs simples | `factor(x²+2x+1)` → `(x+1)²` |
| **`simplify()`** | Simplifie selon des règles heuristiques | `simplify((x²-1)/(x-1))` → `x+1` |
| **`collect()`** | Regroupe les termes similaires | `collect(x*y + x + 2*x², x)` |
| **`cancel()`** | Simplifie les fractions rationnelles | `cancel((x²+2x+1)/(x+1))` → `x+1` |
| **`apart()`** | Décomposition en éléments simples | Décompose les fractions rationnelles |
| **`together()`** | Met sur le même dénominateur | `together(1/x + 1/y)` → `(x+y)/(xy)` |

### Cas d'usage

- **expand()** : Développer des polynômes pour voir tous les termes
- **factor()** : Trouver les racines et simplifier les expressions
- **simplify()** : Nettoyer des expressions complexes
- **collect()** : Organiser les termes par puissance
- **cancel()** : Simplifier avant calcul de limites ou dérivées
- **apart()** : Intégration de fractions rationnelles
- **together()** : Additionner/soustraire des fractions

---

## 2. Calcul différentiel

### Opérations de dérivation

| Fonction | Description | Exemple |
|----------|-------------|---------|
| **`diff(f, x)`** | Dérivée de f par rapport à x | `diff(x³, x)` → `3x²` |
| **`diff(f, x, n)`** | Dérivée n-ième de f | `diff(x³, x, 2)` → `6x` |
| **`diff(f, x, y)`** | Dérivée partielle ∂²f/∂x∂y | Dérivées mixtes |
| **`Derivative()`** | Dérivée non évaluée (symbolique) | Représentation symbolique |
| **`gradient()`** | Gradient d'une fonction scalaire | Vecteur des dérivées partielles |
| **`hessian()`** | Matrice hessienne (dérivées secondes) | Matrice des ∂²f/∂xᵢ∂xⱼ |
| **`jacobian()`** | Matrice jacobienne (dérivées partielles) | Pour fonctions vectorielles |

### Cas d'usage

- **diff(f, x)** : Calcul de pentes, vitesses, taux de variation
- **diff(f, x, 2)** : Concavité, accélération, courbure
- **diff(f, x, y)** : Analyse de fonctions à plusieurs variables
- **Derivative()** : Écriture symbolique sans évaluation
- **gradient()** : Optimisation, direction de plus grande croissance
- **hessian()** : Classification des points critiques (min/max)
- **jacobian()** : Changements de variables, transformations

---

## 3. Calcul intégral

### Opérations d'intégration

| Fonction | Description | Exemple |
|----------|-------------|---------|
| **`integrate(f, x)`** | Intégrale indéfinie (primitive) | `integrate(x², x)` → `x³/3` |
| **`integrate(f, (x,a,b))`** | Intégrale définie de a à b | `integrate(x², (x,0,1))` → `1/3` |
| **`integrate(f, (x,a,b), (y,c,d))`** | Intégrale double/triple | Aires, volumes, masses |
| **`Integral()`** | Intégrale non évaluée (symbolique) | Représentation formelle |
| **`oo`** | Représente l'infini pour bornes | `integrate(e^(-x), (x,0,oo))` |
| **Piecewise** | Intégration par morceaux | Fonctions définies par morceaux |

### Cas d'usage

- **integrate(f, x)** : Trouver les primitives, résoudre équations différentielles
- **integrate(f, (x,a,b))** : Aires sous courbes, travail, distance
- **Intégrales doubles** : Aires de surfaces, volumes
- **Intégrales triples** : Masses, centres de gravité
- **Bornes infinies** : Probabilités (loi normale), transformées
- **Integral()** : Documentation, représentation sans calcul

---

## 4. Limites

### Opérations sur les limites

| Fonction | Description | Exemple |
|----------|-------------|---------|
| **`limit(f, x, a)`** | Limite de f quand x→a | `limit(sin(x)/x, x, 0)` → `1` |
| **`limit(f, x, a, '+')`** | Limite à droite (x→a⁺) | `limit(1/x, x, 0, '+')` → `∞` |
| **`limit(f, x, a, '-')`** | Limite à gauche (x→a⁻) | `limit(1/x, x, 0, '-')` → `-∞` |
| **`limit(f, x, oo)`** | Limite à l'infini (x→+∞) | Comportement asymptotique |
| **`limit(f, x, -oo)`** | Limite en -∞ (x→-∞) | Comportement à gauche |
| **Limite bilatérale** | Compare limites gauche/droite | Continuité en un point |
| **Formes indéterminées** | 0/0, ∞/∞, etc. (L'Hôpital) | SymPy applique automatiquement |

### Cas d'usage

- **limit(f, x, a)** : Continuité, définition de la dérivée
- **Limites latérales** : Détecter les discontinuités
- **limit(f, x, oo)** : Asymptotes horizontales, convergence
- **Formes indéterminées** : Résolution automatique avec règle de L'Hôpital
- **Analyse de fonctions** : Comprendre le comportement global

---

## 5. Séries et développements

### Opérations sur les séries

| Fonction | Description | Exemple |
|----------|-------------|---------|
| **`series(f, x, x0, n)`** | Développement de Taylor/Laurent autour de x₀ | Approximation polynomiale |
| **`summation(f, (i,a,b))`** | Somme de a à b (finie ou infinie) | `summation(1/n², (n,1,∞))` |
| **`Sum()`** | Somme non évaluée (symbolique) | Notation Σ |
| **`Product()`** | Produit symbolique | Notation Π |
| **`fps()`** | Série formelle de puissances | Série génératrice |
| **`O(xⁿ)`** | Terme de reste (ordre n) | Notation de Landau |
| **`rseries()`** | Série autour d'un point singulier | Développement de Laurent |

### Cas d'usage

- **series()** : Approximations locales, calculs numériques
- **Taylor** : Approximation de fonctions (sin, cos, exp, ln)
- **summation()** : Séries convergentes, calcul exact
- **Séries infinies** : π², e, constantes mathématiques
- **Sum()** : Écriture formelle sans calcul
- **Ordre O()** : Analyse d'erreur, complexité algorithmique
- **Approximations** : Simplifier des calculs complexes

### Séries classiques

- **eˣ** : 1 + x + x²/2! + x³/3! + ...
- **sin(x)** : x - x³/3! + x⁵/5! - x⁷/7! + ...
- **cos(x)** : 1 - x²/2! + x⁴/4! - x⁶/6! + ...
- **ln(1+x)** : x - x²/2 + x³/3 - x⁴/4 + ...
- **1/(1-x)** : 1 + x + x² + x³ + ... (série géométrique)

---

## 6. Matrices et algèbre linéaire

### Opérations matricielles

| Fonction | Description | Cas d'usage |
|----------|-------------|-------------|
| **`Matrix()`** | Création de matrice | Définir des systèmes linéaires |
| **`det()`** | Déterminant | Test d'inversibilité (det≠0) |
| **`inv()`** | Matrice inverse | Résolution de Ax=b (x=A⁻¹b) |
| **`transpose()`** | Transposée | Matrices symétriques, produit scalaire |
| **`eigenvals()`** | Valeurs propres | Stabilité, vibrations, dynamique |
| **`eigenvects()`** | Vecteurs propres | Directions propres, modes |
| **`diagonalize()`** | Diagonalisation | Puissances de matrices, systèmes différentiels |
| **`rank()`** | Rang de la matrice | Dimension de l'image |
| **`nullspace()`** | Noyau (espace nul) | Solutions de Ax=0 |
| **`columnspace()`** | Espace des colonnes | Image de la transformation |
| **`rref()`** | Forme échelonnée réduite | Résolution de systèmes |
| **`LUdecomposition()`** | Décomposition LU | Résolution efficace |
| **`QRdecomposition()`** | Décomposition QR | Orthogonalisation, moindres carrés |
| **`cholesky()`** | Décomposition de Cholesky | Matrices définies positives |

### Opérations avancées

- **`trace()`** : Somme des éléments diagonaux
- **`solve(b)`** : Résout Ax=b directement
- **`norm()`** : Norme matricielle
- **`is_symmetric()`** : Test de symétrie
- **`is_positive_definite()`** : Test de définie positive
- **Puissances** : `M**n` pour calculer Mⁿ

### Cas d'usage principaux

1. **Systèmes linéaires** : Résolution de Ax = b
2. **Transformations géométriques** : Rotations, projections
3. **Analyse de stabilité** : Valeurs propres de matrices jacobiennes
4. **Réduction dimensionnelle** : PCA (analyse en composantes principales)
5. **Équations différentielles** : Systèmes linéaires (diagonalisation)
6. **Optimisation** : Matrices hessiennes (min/max)
7. **Physique quantique** : Opérateurs, états propres
8. **Graphes** : Matrices d'adjacence, connectivité

---

## Ressources complémentaires

- **Documentation officielle** : [https://docs.sympy.org](https://docs.sympy.org)
- **Tutoriels** : [https://docs.sympy.org/latest/tutorial/](https://docs.sympy.org/latest/tutorial/)
- **Installation** : `pip install sympy`

## Recommandations

1. **Toujours simplifier** : Utilisez `simplify()` après vos calculs
2. **Vérifier numériquement** : `.evalf()` ou `float()` pour valeurs numériques
3. **Substitution** : `.subs(x, valeur)` pour remplacer des variables
4. **Affichage LaTeX** : `sp.init_printing()` pour un affichage élégant


## Exemples typiques

```python
# Dérivée d'une fonction composée
f = sin(x**2 + 1)
diff(f, x)  # → 2*x*cos(x² + 1)

# Intégrale définie
integrate(x*exp(-x), (x, 0, oo))  # → 1

# Limite classique
limit((1 + 1/n)**n, n, oo)  # → e

# Développement de Taylor
exp(x).series(x, 0, 5)  # → 1 + x + x²/2 + x³/6 + x⁴/24 + O(x⁵)

# Valeurs propres
M = Matrix([[1, 2], [2, 1]])
M.eigenvals()  # → {-1: 1, 3: 1}
```

---
