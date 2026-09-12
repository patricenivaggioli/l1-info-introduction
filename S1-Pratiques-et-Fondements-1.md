# S1 — Pratiques et fondements 1

**UE Pratiques et fondements** · Cours : Architecture des ordinateurs · Gestion d'identité en ligne · Pratique des machines

Cette UE relie la pratique (Linux, web) aux fondements (architecture matérielle). Elle donne le contexte dans lequel les programmes s'exécutent.

---

## 1. Architecture des ordinateurs

Comprendre les principes fondamentaux du fonctionnement d'un ordinateur et les relations entre matériel et logiciel.

### Représentation de l'information

#### Systèmes de numération

| Système | Base | Symboles | Exemple |
|---------|------|----------|---------|
| Binaire | 2 | 0, 1 | `1010` = 10 |
| Décimal | 10 | 0–9 | `42` |
| Hexadécimal | 16 | 0–9, A–F | `0xFF` = 255 |

#### Conversions essentielles

```
Binaire → Décimal : 1010 = 1×8 + 0×4 + 1×2 + 0×1 = 10
Décimal → Binaire : 42 ÷ 2 = 21 r0 → 21 ÷ 2 = 10 r1 → ... → 101010
Binaire → Hexa   : 1010 1111 → 1010=A, 1111=F → 0xAF
```

#### Codage des caractères

- **ASCII** : 128 caractères codés sur 7 bits (lettres, chiffres, ponctuation).
- **UTF-8** : encodage variable (1 à 4 octets), compatible ASCII, couvre Unicode.

### Organisation d'un processeur

| Composant | Rôle |
|-----------|------|
| **ALU** | Opérations arithmétiques et logiques (addition, ET, OU...) |
| **Registres** | Mémoire ultra-rapide dans le CPU (PC, IR, accumulateurs) |
| **Unité de contrôle** | Décode et séquence les instructions |
| **Bus** | Chemin de communication entre CPU, mémoire et I/O |
| **RAM** | Mémoire volatile, stocke programmes et données en exécution |
| **Cache** | Mémoire intermédiaire entre CPU et RAM (L1, L2, L3) |

### Cycle d'exécution (fetch-decode-execute)

1. **Fetch** — l'instruction est lue depuis la mémoire à l'adresse pointée par le PC.
2. **Decode** — l'unité de contrôle décode l'instruction.
3. **Execute** — l'ALU ou un autre composant exécute l'opération.
4. Le PC est incrémenté → retour à l'étape 1.

### Mémoire

| Type | Vitesse | Taille | Persistance |
|------|---------|--------|------------|
| Registres | Ultra-rapide | Octets | Volatile |
| Cache L1/L2 | Très rapide | Ko | Volatile |
| RAM | Rapide | Go | Volatile |
| Disque SSD | Lent | To | Persistante |
| Disque HDD | Très lent | To | Persistante |

### Assemblage de composants

Le cours illustre un principe central de la programmation : assembler des composants de base pour produire des composants spécifiques. Ici, les composants sont matériels (portes logiques → ALU → CPU), mais le même raisonnement s'applique au logiciel (fonctions → modules → programmes).

---

## 2. Gestion d'identité en ligne

Réfléchir à notre rapport aux géants du web (Big Tech) et adopter de bonnes pratiques pour son image en ligne.

### Concepts clés

| Concept | Pratique |
|---------|----------|
| **Empreinte numérique** | Tout ce qu'on publie laisse une trace ; penser avant de poster |
| **Big Tech** | Concentration des données chez Google, Meta, Amazon... |
| **Page web personnelle** | Créer et héberger un site simple pour valoriser ses projets |
| **Hébergement** | GitHub Pages, Netlify, ou serveur personnel |

### Réaliser une page web simple

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Ma page</title>
</head>
<body>
    <h1>Bonjour, je suis Patrice</h1>
    <p>Étudiant en licence informatique à Paris 8.</p>
    <ul>
        <li><a href="projets.html">Mes projets</a></li>
        <li><a href="contact.html">Contact</a></li>
    </ul>
</body>
</html>
```

### Bonnes pratiques

- Séparer contenu (HTML), style (CSS) et interactivité (JS).
- Garder sa page à jour avec ses projets académiques et personnels.
- Réfléchir aux données personnelles partagées sur les réseaux sociaux.

---

## 3. Pratique des machines

Se familiariser avec l'environnement **GNU/Linux** et la ligne de commande.

### Commandes essentielles

| Commande | Rôle |
|----------|------|
| `pwd` | Afficher le répertoire courant |
| `ls -la` | Lister les fichiers (avec détails) |
| `cd /chemin` | Changer de répertoire |
| `mkdir nom` | Créer un répertoire |
| `cp src dst` | Copier un fichier |
| `mv src dst` | Déplacer ou renommer |
| `rm -r nom` | Supprimer |
| `cat fichier` | Afficher le contenu |
| `chmod` | Modifier les permissions |
| `ssh user@serveur` | Se connecter à distance |

### Permissions (rappel)

```
rwxr-xr--  →  propriétaire: rwx | groupe: r-x | autres: r--
```

```bash
chmod +x script.sh    # rendre exécutable
chmod 755 script.sh  # rwxr-xr-x
```

---

## Conseils de révision

- Pour l'architecture : pratiquer les conversions de base (binaire, hexa, décimal) jusqu'à l'automatisme.
- Pour la pratique des machines : utiliser Linux au quotidien, ne pas attendre le cours pour taper des commandes.
- Pour la gestion d'identité : mettre en ligne sa page web personnelle dès le début du semestre.
