# S1 — Programmation 1

**UE Informatique — 18 ECTS** · Langages : Python, C, Racket

Cette UE est le cœur du semestre 1. Elle introduit deux paradigmes complémentaires : l'impératif (Python, C) et le fonctionnel (Racket), pour donner de bonnes habitudes de programmation dès le départ.

---

## 1. Méthodologie de la programmation

**Langages : Python & C**

L'objectif n'est pas d'apprendre un langage, mais d'apprendre à *apprendre à programmer* : concevoir, implémenter, compiler, exécuter et tester des programmes de manière autonome.

### Concepts clés

| Concept | Détail |
|---------|--------|
| **Conception** | Décomposer un problème en sous-problèmes, écrire un algorithme avant de coder |
| **Implémentation** | Traduire l'algorithme en code Python ou C |
| **Compilation** | Chaîne de compilation en C (`gcc`), interprétation en Python |
| **Exécution** | Comprendre ce qui se passe en mémoire à l'exécution |
| **Test** | Écrire des jeux de tests, vérifier les cas limites |

### Python — Points essentiels

```python
# Variables et types
x = 42              # int
name = "Alice"       # str
prices = [10, 20]    # list

# Structure conditionnelle
if x > 10:
    print("grand")
else:
    print("petit")

# Boucle
for i in range(10):
    print(i)

# Fonction
def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

### C — Points essentiels

```c
#include <stdio.h>

int factorial(int n) {
    int result = 1;
    for (int i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}

int main() {
    printf("%d\n", factorial(5));
    return 0;
}
```

### Différences clés Python ↔ C

| Aspect | Python | C |
|--------|--------|---|
| Typage | Dynamique | Statique |
| Mémoire | Gérée automatiquement (GC) | Manuelle (`malloc`/`free`) |
| Exécution | Interprété | Compilé (`gcc`) |
| Tableaux | `list` dynamique | `int[]` taille fixe |
| Chaînes | `str` natif | `char[]` ou `char*` |

### Méthodologie de travail

1. **Lire** l'énoncé en entier et identifier les entrées/sorties.
2. **Décomposer** le problème en étapes simples.
3. **Écrire** un pseudo-algorithme ou un schéma.
4. **Coder** progressivement, tester au fur et à mesure.
5. **Tester** avec des cas limites (vide, négatif, grand).

---

## 2. Programmation fonctionnelle 1

**Langage : Racket** (dialecte de Scheme/Lisp)

Le paradigme fonctionnel fait réfléchir au **quoi** (l'objectif) plutôt qu'au **comment** (les étapes). Pas de boucles `for` ni de variables mutables : on utilise des fonctions, de la récursivité et des listes.

### Concepts clés

| Concept | Détail |
|---------|--------|
| **Fonctions** | Des valeurs comme les autres ; peuvent être passées en argument |
| **Récursivité** | Remplace les boucles ; un cas de base + un cas récursif |
| **Listes** | Structure de données fondamentale (cons, car, cdr) |
| **Immutabilité** | Pas d'effets de bord ; on produit de nouvelles valeurs |
| **Fonctions d'ordre supérieur** | `map`, `filter`, `foldl`/`foldr` |

### Syntaxe Racket — Bases

```racket
;; Définir une fonction
(define (square x)
  (* x x))

;; Conditionnelle
(define (abs-val x)
  (if (< x 0) (- x) x))

;; Récursivité : factorielle
(define (factorial n)
  (if (= n 0)
      1
      (* n (factorial (- n 1)))))

;; Listes
(define lst (list 1 2 3 4 5))
(first lst)         ; → 1
(rest lst)          ; → (2 3 4 5)
(cons 0 lst)        ; → (0 1 2 3 4 5)

;; Fonctions d'ordre supérieur
(map square lst)            ; → (1 4 9 16 25)
(filter even? lst)          ; → (2 4)
(foldl + 0 lst)             ; → 15
```

### Schéma récursif standard

```racket
;; Modèle : cas de base + cas récursif
(define (my-func lst)
  (cond
    [(null? lst) ...]              ; cas de base : liste vide
    [else (... (first lst)         ; traiter le premier élément
               (my-func (rest lst)))]))  ; récursion sur le reste
```

### Impératif vs. Fonctionnel

| Aspect | Impératif (Python/C) | Fonctionnel (Racket) |
|--------|---------------------|---------------------|
| Boucle | `for`, `while` | Récursivité |
| Variables | Mutables (`x = x + 1`) | Immuables (pas d'affectation) |
| État | Modifié en place | Pas d'effet de bord |
| Pensée | "Comment faire étape par étape" | "Quelle transformation appliquer" |

---

## Conseils de révision

- Pratiquer régulièrement : la programmation s'apprend en codant, pas en lisant.
- Faire les exercices au fur et à mesure — les corrections progressives sont essentielles en S1.
- Comparer les deux paradigmes : réécrire un même algorithme en Python et en Racket.
- Tester systématiquement les cas limites (liste vide, valeur 0, entrée négative).
