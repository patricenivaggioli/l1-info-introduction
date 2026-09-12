# S1 — Programmation pour le jeu vidéo 1

**UE Mineure — 6 ECTS** · Moteur : Godot

Cette UE introduit le fonctionnement des moteurs de jeux et les mathématiques utiles en informatique et en conception de jeux vidéo.

---

## 1. Introduction aux moteurs de jeux

**Moteur utilisé : Godot Engine**

Comprendre le rôle et les fonctionnalités d'un moteur de jeu, puis prendre en main Godot en pratique.

### Qu'est-ce qu'un moteur de jeu ?

Un **moteur de jeu** est un cadre logiciel qui fournit les outils et bibliothèques nécessaires pour créer un jeu, sans avoir à tout programmer de zéro.

| Fonctionnalité | Description |
|----------------|-------------|
| **Rendu** | Affichage 2D/3D à l'écran (sprites, modèles, lumières) |
| **Physique** | Détection de collisions, gravité, mouvement |
| **Audio** | Gestion des sons et musiques |
| **Entrées** | Clavier, souris, manette, écran tactile |
| **Scènes** | Organisation du jeu en niveaux, menus, etc. |
| **Scripting** | Logique du jeu via un langage de scripting |

### Pourquoi Godot ?

- **Libre et open-source** (licence MIT).
- **Léger** — un seul exécutable, pas d'installation lourde.
- **GDScript** — langage de scripting proche de Python.
- **2D et 3D** — moteur unifié pour les deux dimensions.
- **Nœuds et scènes** — architecture intuitive orientée objet.

### Architecture de Godot : nœuds et scènes

Tout dans Godot est un **nœud** (Node). Les nœuds s'organisent en arbre :

```
Scene (Node2D)
├── Sprite        → affiche une image
├── CollisionShape2D → définit une zone de collision
├── Camera2D      → suit le joueur
└── Label          → affiche du texte
```

- Une **scène** est un arbre de nœuds, réutilisable et instanciable.
- Le jeu est une collection de scènes (menu, niveau, game over...).

### GDScript — Bases

```gdscript
extends CharacterBody2D

var speed = 200.0

func _ready():
    # Appelé une fois au démarrage
    print("Joueur prêt")

func _process(delta):
    # Appelé à chaque frame
    var direction = Input.get_vector("left", "right", "up", "down")
    velocity = direction * speed
    move_and_slide()

func _on_area_entered(area):
    # Signal : collision détectée
    print("Collision avec", area.name)
```

### Concepts clés

| Concept | Description |
|---------|-------------|
| **`_ready()`** | Fonction appelée une fois quand le nœud entre dans la scène |
| **`_process(delta)`** | Fonction appelée à chaque frame (logique du jeu) |
| **`delta`** | Temps écoulé depuis la dernière frame (pour un mouvement fluide) |
| **Signaux** | Mécanisme d'événements : un nœud émet, un autre écoute |
| **`Input`** | Gestion des entrées clavier/souris/manette |
| **`move_and_slide()`** | Déplacement avec gestion automatique des collisions |

---

## 2. Mathématiques pour l'informatique et les jeux vidéo

Notions mathématiques de base utiles en algorithmique et en conception de jeux vidéo.

### Théorie des ensembles et probabilités discrètes

| Notion | En jeu vidéo |
|--------|-------------|
| **Ensembles** | Groupes d'objets (ennemis, items, joueurs) |
| **Union / Intersection** | Combiner des groupes, filtrer |
| **Probabilités** | Tirage aléatoire (loot, drops, critiques) |

```python
# Probabilité d'un drop
import random
def drop_item():
    if random.random() < 0.1:   # 10% de chance
        return "épée rare"
    return "potion"
```

### Géométrie euclidienne dans le plan

| Notion | En jeu vidéo |
|--------|-------------|
| **Vecteurs** | Direction et vitesse d'un personnage |
| **Distance** | Détecter si un ennemi est dans le rayon d'attaque |
| **Produit scalaire** | Vérifier l'alignement ou l'angle entre deux directions |
| **Rotation** | Orienter un sprite vers la souris ou un ennemi |

```python
import math

# Distance entre deux points
def distance(p1, p2):
    return math.sqrt((p2[0] - p1[0])**2 + (p2[1] - p1[1])**2)

# Vecteur normalisé (direction pure)
def normalize(vx, vy):
    norm = math.sqrt(vx**2 + vy**2)
    if norm == 0:
        return (0, 0)
    return (vx / norm, vy / norm)
```

### Arithmétique et cryptographie

| Notion | Application |
|--------|------------|
| **Modulo (`%`)** | Hashing, cycles, position toroïdale |
| **PGCD** | Base du RSA, simplification de fractions |
| **Nombres premiers** | Cryptographie (clés, chiffrement) |

```python
# Exponentiation modulaire (base de RSA)
def mod_pow(base, exp, mod):
    result = 1
    base = base % mod
    while exp > 0:
        if exp % 2 == 1:
            result = (result * base) % mod
        exp = exp // 2
        base = (base * base) % mod
    return result
```

### Matrices et systèmes linéaires

| Notion | En jeu vidéo |
|--------|-------------|
| **Matrices 2×2, 3×3** | Transformations (rotation, mise à l'échelle) |
| **Produit matriciel** | Combiner plusieurs transformations |
| **Systèmes linéaires** | Résoudre des équations, interpolation |

```python
# Matrice de rotation 2D (angle θ)
import math
def rotation_matrix(theta):
    c, s = math.cos(theta), math.sin(theta)
    return [[c, -s], [s, c]]

# Appliquer à un vecteur (x, y)
def apply(M, x, y):
    return (M[0][0]*x + M[0][1]*y, M[1][0]*x + M[1][1]*y)
```

---

## Conseils de révision

- Télécharger Godot et créer un petit projet (déplacer un sprite avec les flèches).
- Pratiquer les manipulations de vecteurs et matrices sur papier, puis en code.
- Réviser les conversions entre systèmes de numération pour les exercices d'arithmétique.
- Comprendre les signaux Godot : ils sont l'équivalent des événements/callbacks en programmation classique.
