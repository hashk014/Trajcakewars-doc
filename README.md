# TrajCakeWars — Guide de Setup Rapide
## by TrajStudio

---

## Étape 1 : Installation

1. Place `TrajCakeWars.jar` dans le dossier `plugins/` de ton serveur.
2. Démarre le serveur une première fois pour générer les fichiers de config.
3. Arrête le serveur.

---

## Étape 2 : Préparer ta map CakeWars

Tu as besoin d'une map CakeWars construite avec :
- 2 îles (une par joueur) avec un bloc cake sur chacune
- Des ponts ou un espace entre les îles
- Un centre (optionnel, pour les générateurs diamant)
- Des emplacements pour les PNJ shops sur chaque île

### Option A : Ta map est dans un monde séparé
```
cp -r ton_monde_cakewars cw_templates/desert
```

### Option B : Ta map est dans le monde principal (world)
```
cp -r world cw_templates/desert
```

### Option C : En jeu
Rends-toi dans le monde contenant ta map et tape :
```
/cw savetemplate desert
```

Le dossier `cw_templates/` doit être à la racine du serveur,
au même niveau que `world/`, `plugins/`, etc.

---

## Étape 3 : Placer les PNJ Shops

Dans ta map CakeWars (avant de sauvegarder le template), place des
PNJ sur chaque île avec un plugin de ton choix :

### Avec Citizens :
```
/npc create §e§lItems Shop
/npc type VILLAGER
```
```
/npc create §a§lBlocks Shop
/npc type VILLAGER
```

### Avec un villageois vanilla :
Renomme-le avec un name tag contenant "Items" ou "Blocs".

### Mots-clés reconnus :
- Items Shop → nom contient : Items, Item, Combat, Armes
- Blocks Shop → nom contient : Blocks, Blocs, Build, Construction
- (Configurable dans config.yml)

Fais 2 PNJ par île (Items + Blocs) = 4 PNJ total.
Si tu as sauvegardé le template APRÈS avoir placé les PNJ,
ils seront clonés automatiquement à chaque partie.

---

## Étape 4 : Configurer l'arène

Démarre le serveur et connecte-toi en jeu.

### Créer l'arène :
```
/cw create desert
```

### Te téléporter dans le template pour configurer :
```
/cw tp desert
```

### Définir les 7 points obligatoires :
Va à chaque emplacement et tape la commande correspondante.

```
/cw set desert spawn1       → Spawn du joueur 1
/cw set desert spawn2       → Spawn du joueur 2
/cw set desert cake1        → Sur le bloc cake du joueur 1
/cw set desert cake2        → Sur le bloc cake du joueur 2
/cw set desert gen1         → Générateur de fer, île 1
/cw set desert gen2         → Générateur de fer, île 2
/cw set desert lobby        → Point d'attente/spectateur
```

### Ajouter des générateurs diamant (optionnel) :
```
/cw set desert diamond      → Répéter à chaque emplacement
```

### Personnaliser :
```
/cw setname desert §6§lDésert Brûlant
/cw seticon desert SAND
/cw settemplate desert desert
```

### Vérifier que tout est configuré :
```
/cw info desert             → Tout doit être vert ✓
```

### Revenir au lobby :
```
/cw back
```

---

## Étape 5 : Définir le point de retour lobby

Place-toi exactement là où les joueurs doivent être téléportés
après chaque partie (dans ton lobby principal) et tape :

```
/cw setlobby
```

---

## Étape 6 : Activer et sauvegarder

```
/cw enable desert
/cw save
```

---

## Étape 7 : PNJ lobby (optionnel)

Pour que les joueurs accèdent au CakeWars depuis le lobby
en cliquant sur un PNJ :

### Avec Citizens :
```
/npc create §d§lCakeWars 1v1
/npc type VILLAGER
/npc command add -p cw
```

Les joueurs cliquent → le menu /cw s'ouvre.

---

## Étape 8 : Tester

Connecte-toi avec 2 comptes (ou un ami).

1. Les 2 joueurs cliquent sur le PNJ lobby ou tapent `/cw`
2. Cliquer sur "Jouer" dans le menu
3. Le matchmaking trouve les 2 joueurs
4. Un monde temporaire est cloné
5. Les joueurs sont TP, freeze 5s, puis GO !
6. La partie se joue
7. Le vainqueur reçoit ses récompenses
8. Les 2 joueurs sont TP au lobby
9. Le monde temporaire est supprimé

---

## Ajouter une deuxième map

1. Construis une nouvelle map dans un monde dédié
2. Place les PNJ shops dedans
3. Sauvegarde : `/cw savetemplate jungle`
4. Crée l'arène : `/cw create jungle`
5. Configure : `/cw tp jungle` puis `/cw set jungle spawn1` etc.
6. Active : `/cw back` → `/cw enable jungle` → `/cw save`

Les 2 maps seront disponibles dans le matchmaking.

---

## Commandes essentielles (aide-mémoire)

### Joueur :
  /cw                → Menu principal
  /cw join           → Matchmaking rapide
  /cw join <code>    → Rejoindre session privée
  /cw private <map>  → Créer session privée
  /cw leave          → Quitter

### Admin :
  /cw create <id>              → Nouvelle arène
  /cw delete <id>              → Supprimer (x2 pour confirmer)
  /cw tp <arène>               → TP dans le template
  /cw back                     → Retour lobby
  /cw set <arène> <point>      → Définir un point
  /cw setname <arène> <nom>    → Nom d'affichage
  /cw seticon <arène> <mat>    → Icône GUI
  /cw settemplate <arène> <t>  → Lier au template
  /cw savetemplate <nom>       → Sauvegarder monde comme template
  /cw setlobby                 → Point de retour lobby
  /cw enable <arène>           → Activer
  /cw save                     → Sauvegarder
  /cw info <arène>             → Voir les points configurés
  /cw list                     → Lister les arènes
  /cw admin                    → Panel admin GUI

---

## Dépannage

### Le shop est vide
Supprime `plugins/TrajCakeWars/config.yml` et redémarre.
L'ancien config n'a pas les sections shop.

### Les arènes sont DISABLED / ready=false
Il manque des points. Tape `/cw info <arène>` pour voir
lesquels sont manquants (✗).

### Les joueurs tombent dans le vide après la game
Tape `/cw setlobby` à la bonne position dans le lobby.

### Le monde temporaire ne se crée pas
Vérifie que `cw_templates/<nom>` existe bien à la racine
du serveur et que le template est lié : `/cw settemplate <arène> <nom>`

### Le matchmaking ne trouve pas d'arène
L'arène doit être `ready=true` ET `state=WAITING`.
Tape `/cw enable <arène>` puis `/cw save`.

---

TrajCakeWars v2.1.5 — by hash
