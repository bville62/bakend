[Uploading fiche-revision-csi-complete.md…]()
# FICHE DE RÉVISION ULTIME – CSI (LE2)
## Version enrichie avec schémas et diagrammes

## Objectif
Maîtriser tout ce qui tombe au partiel de **Conception des Systèmes d'Information (CSI)** à partir du cours et des anciens sujets (2021–2022, 2022–2023, 2023–2024, 2024–2025).

---

## Plan de la fiche
1. [Système d'information et contexte du cours](#1-système-dinformation-et-contexte-du-cours)
2. [Hiérarchie d'abstraction (MCD / MLD / MPD)](#2-hiérarchie-dabstraction-très-fréquent)
3. [Modèle entité–association (MEA)](#3-modèle-entité--association-mea)
4. [Traduction MEA → Modèle relationnel](#4-traduction-mea--modèle-relationnel) ⭐ **AVEC SCHÉMAS**
5. [Lecture, critique et correction d'un MEA](#5-lecture-critique-et-correction-dun-mea)
6. [UML (introduction)](#6-uml--ce-quil-faut-savoir-pour-le-partiel)
7. [Vocabulaire et acronymes](#7-vocabulaire-acronymes-et-questions-de-cours-classiques)
8. [Stratégie de révision](#8-stratégie-de-révision-et-entraînements-recommandés)

---

## 1. SYSTÈME D'INFORMATION ET CONTEXTE DU COURS

### 1.1. Définition de système d'information

Un **système d'information (SI)** est un ensemble structuré de :
- **informations**
- **acteurs**
- **processus**
- **ressources techniques** (en partie)

qui permet de **collecter, stocker, traiter et mettre à disposition de l'information** pour atteindre un objectif (gérer une entreprise, diffuser de l'info, suivre des élèves, etc.).

**Points clés à retenir :**
- Le SI sert les **acteurs** : il ne doit pas être conçu sans eux
- Le SI **évolue** avec les besoins (objectifs qui peuvent changer)
- L'**informatique** est un **sous-ensemble** du SI, pas le SI complet

### 1.2. Système d'information vs système informatique

**Composants typiques d'un SI (à connaître) :**
```
┌─────────────────────────────────────┐
│      SYSTÈME D'INFORMATION          │
├─────────────────────────────────────┤
│  • Acteurs                          │
│  • Processus                        │
│  • Informations & Données           │
│  ┌─────────────────────────────┐    │
│  │ SYSTÈME INFORMATIQUE        │    │
│  ├─────────────────────────────┤    │
│  │ • Matériels                 │    │
│  │ • Bases de données          │    │
│  │ • Applications              │    │
│  └─────────────────────────────┘    │
│  • Organisation, Méthodes           │
└─────────────────────────────────────┘
```

**Donc :**
- **SI** = plus large (inclut organisation, processus, acteurs, etc.)
- **Système informatique** = partie technique du SI

### 1.3. Donnée vs information

| Terme | Définition | Exemple |
|-------|-----------|---------|
| **Donnée** | Valeur brute, non interprétée | 18, "LE2", "2025-12-06", "IG2I-SS05" |
| **Information** | Donnée interprétée dans un contexte, qui a du sens | "Température = 18 °C dans la salle IG2I-SS05 ce matin" |

```
DONNÉES BRUTES  →  [INTERPRÉTATION CONTEXTUELLE]  →  INFORMATION
   "18"                 (température, salle IG2I)      "18°C dans IG2I"
   "2025-12-06"        (date d'aujourd'hui)           "Partiel CSI ce jour"
   "LE2"               (promotion IG2I)                "Je suis en LE2 à IG2I"
```

---

## 2. HIÉRARCHIE D'ABSTRACTION (TRÈS FRÉQUENT)

### 2.1. Les trois niveaux

| Niveau | Nom du modèle | Caractéristiques |
|--------|---------------|------------------|
| **Conceptuel** | **MCD** (Modèle Conceptuel de Données) = **MEA** (Modèle Entité–Association) | Représente les **informations et leurs liens**. Indépendant de la technologie. |
| **Logique** | **MLD** (Modèle Logique de Données) | **Modèle relationnel** dans ce cours (tables, colonnes, PK, FK…). Dépend du type de base de données. |
| **Physique** | **MPD** (Modèle Physique de Données) | Définition SQL, types concrets, index, contraintes physiques. Dépend du SGBD choisi. |

### 2.2. Schéma de la hiérarchie d'abstraction

```
NIVEAU CONCEPTUEL (MCD/MEA)
┌────────────────────────────────────┐
│  Élève       Promotion              │
│  -------     ----------             │
│  • numéro    • code                 │
│  • nom       • année                │
│  • prénom    • établissement        │
│              • apprentissage        │
│       ↓ Appartient à (1,1 — 0,n)    │
└────────────────────────────────────┘
         ↓ TRADUCTION
         
NIVEAU LOGIQUE (MLD/MODÈLE RELATIONNEL)
┌────────────────────────────────────┐
│  ELEVE(numPK, nom, prénom, promoId FK)        │
│  PROMOTION(codePK, année, établissement, apprentissage) │
└────────────────────────────────────┘
         ↓ IMPLÉMENTATION
         
NIVEAU PHYSIQUE (MPD/SQL)
┌────────────────────────────────────┐
│  CREATE TABLE ELEVE(               │
│    num INT PRIMARY KEY,            │
│    nom VARCHAR(255) NOT NULL,      │
│    prénom VARCHAR(255),            │
│    promoId VARCHAR(10) FOREIGN KEY │
│  );                                │
│  CREATE TABLE PROMOTION(           │
│    code VARCHAR(10) PRIMARY KEY,   │
│    année INT,                      │
│    établissement VARCHAR(255),     │
│    apprentissage BOOLEAN           │
│  );                                │
└────────────────────────────────────┘
```

### 2.3. À retenir par cœur

✅ **Ordre du plus abstrait au plus concret :**
```
CONCEPTUEL (MCD/MEA) → LOGIQUE (MLD/MR) → PHYSIQUE (MPD/SQL)
```

✅ **Noms des modèles** à chaque niveau (MCD / MLD / MPD)

✅ **En CSI**, on travaille surtout sur : **MCD (MEA)** et traduction en **MLD (modèle relationnel)**

---

## 3. MODÈLE ENTITÉ–ASSOCIATION (MEA)

C'est le **cœur du partiel** :
- Gros exercice de modélisation à partir d'un énoncé (drones, vols, salles, NextCloud, etc.)
- Exercice de compréhension et de critique d'un modèle existant

### 3.1. Concepts de base avec schémas

#### Entité
```
┌──────────────────┐
│     ÉLÈVE        │  ← Nom de l'entité (singulier, majuscule)
├──────────────────┤
│ Attributs:       │
│ • numéro (PK)    │  ← Identifiant (souligné)
│ • nom            │
│ • prénom         │
│ • dateNaissance  │
│ • email          │
└──────────────────┘
```

#### Attribut
```
Attributs atomiques (simples)      Attributs NON atomiques (composés)
────────────────────────────       ──────────────────────────────────
• nom ✅                           • adresseCOMPLETE (rue + CP + ville) ❌
• prénom ✅                        • listeSponsors (liste) ❌
• email ✅                         • coordonnées (lat + long) ❌
• dateNaissance ✅                 • dateHeureArrivée (date + heure) ❌
```

#### Identifiant (clé)
```
CAS 1 – Clé neutre simple (RECOMMANDÉ)
┌─────────────────────┐
│  PROMOTION          │
├─────────────────────┤
│ • idPromo (PK) ← Clé neutre │
│ • code (métier)     │
│ • année             │
│ • établissement     │
└─────────────────────┘

CAS 2 – Clé métier simple
┌─────────────────────┐
│  PROMOTION          │
├─────────────────────┤
│ • code (PK) ← Clé métier unique │
│ • année             │
│ • établissement     │
└─────────────────────┘

CAS 3 – Clé composée (multi-attribut) ⚠️
┌─────────────────────────────────────┐
│  RESULTAT (examen)                  │
├─────────────────────────────────────┤
│ • idElève (PK1)     │
│ • idCours (PK1)     │ ← Clé composée (2 attributs)
│ • note              │
│ • date              │
└─────────────────────────────────────┘
```

#### Association avec multiplicités

```
EXEMPLE 1 – Association (1,1) — (0,n)
┌──────────────┐ 1,1      0,n ┌────────────────┐
│  ÉLÈVE       │◄──────────────│   PROMOTION    │
└──────────────┘ Appartient à  └────────────────┘

Lecture côté Élève:    Un élève appartient à UNE ET UNE SEULE promotion
Lecture côté Promotion: Une promotion peut contenir AUCUN, UN OU PLUSIEURS élèves


EXEMPLE 2 – Association (0,1) — (0,n)
┌──────────────┐ 0,1      0,n ┌────────────────┐
│  ENSEIGNANT  │◄──────────────│   BUREAU       │
└──────────────┘ Est affecté à └────────────────┘

Lecture côté Enseignant: Un enseignant peut être affecté à AU PLUS UN bureau
Lecture côté Bureau:     Un bureau peut contenir AUCUN OU PLUSIEURS enseignants


EXEMPLE 3 – Association (0,n) — (0,n)
┌──────────────┐ 0,n      0,n ┌────────────────┐
│  CLIENT      │◄──────────────│   PRODUIT      │
└──────────────┘ Achète        └────────────────┘

Lecture côté Client:  Un client peut acheter AUCUN, UN OU PLUSIEURS produits
Lecture côté Produit: Un produit peut être acheté par AUCUN, UN OU PLUSIEURS clients
```

#### Instance (occurrence)

```
ENTITÉ Élève
┌──────────────────┐
│     ÉLÈVE        │
├──────────────────┤
│ • numéro
│ • nom
│ • prénom
│ • dateNaissance
│ • email
└──────────────────┘

        ↓ INSTANCIATION

INSTANCES d'Élève
┌──────────────────────────────────────┐
│ dupont : ÉLÈVE                       │
├──────────────────────────────────────┤
│ • numéro = 12345                     │
│ • nom = "Dupont"                     │
│ • prénom = "Martine"                 │
│ • dateNaissance = "1995-05-15"       │
│ • email = "m.dupont@centrale.fr"     │
└──────────────────────────────────────┘

┌──────────────────────────────────────┐
│ martin : ÉLÈVE                       │
├──────────────────────────────────────┤
│ • numéro = 12346                     │
│ • nom = "Martin"                     │
│ • prénom = "Jean"                    │
│ • dateNaissance = "1995-08-22"       │
│ • email = "j.martin@centrale.fr"     │
└──────────────────────────────────────┘
```

### 3.2. Règles importantes et pièges classiques

#### Règle 1 – Pas de références à d'autres entités dans les attributs

```
❌ MAUVAIS (anti-pattern)
┌──────────────────┐
│     ÉLÈVE        │
├──────────────────┤
│ • numéro (PK)    │
│ • nom            │
│ • prénom         │
│ • promotion ← RÉFÉRENCE À UNE AUTRE ENTITÉ ! │
└──────────────────┘

✅ CORRECT (avec association)
┌──────────────────┐       1,1        0,n ┌────────────────┐
│     ÉLÈVE        │◄──────────────────────│  PROMOTION     │
├──────────────────┤ Appartient à      ├────────────────┤
│ • numéro (PK)    │                       │ • code (PK)    │
│ • nom            │                       │ • année        │
│ • prénom         │                       │ • établissement│
└──────────────────┘                       └────────────────┘
```

#### Règle 2 – Pas de collections comme attribut

```
❌ MAUVAIS
┌──────────────┐
│  ÉQUIPE      │
├──────────────┤
│ • id (PK)    │
│ • couleur    │
│ • sponsors ← LISTE/COLLECTION ! │
└──────────────┘

✅ CORRECT (avec entité Sponsor)
┌──────────────┐        0,n      1,n ┌──────────────┐
│  ÉQUIPE      │◄────────────────────│  SPONSOR     │
├──────────────┤ Sponsorisée par ├──────────────┤
│ • id (PK)    │                      │ • id (PK)    │
│ • couleur    │                      │ • nom        │
│ • budget     │                      │ • secteur    │
└──────────────┘                      └──────────────┘
```

#### Règle 3 – Unicité d'une instance d'association

```
⚠️ PROBLÈME : Multiplicités n,n sans attributs d'association
┌──────────────┐ 0,n        0,n ┌──────────────┐
│  CLIENT      │◄────────────────│ FOURNISSEUR  │
├──────────────┤ Passe commande ├──────────────┤
│ • id (PK)    │                 │ • id (PK)    │
│ • nom        │                 │ • code       │
└──────────────┘                 └──────────────┘

PROBLÈME: Un même client peut commander plusieurs fois
au même fournisseur, mais on veut garder trace de chaque commande
avec une date !

✅ SOLUTION : Réification (créer une entité COMMANDE)
┌──────────────┐ 1,n        1,1 ┌──────────────┐
│  CLIENT      │───────────────►│  COMMANDE    │
├──────────────┤ Passe      ├──────────────┤
│ • id (PK)    │            │ • id (PK)    │
│ • nom        │            │ • date       │
└──────────────┘ 1,1        1,n └──────────────┘
                  ◄───────────────│
                 Reçue par        │
                        ┌──────────────┐
                        │ FOURNISSEUR  │
                        ├──────────────┤
                        │ • id (PK)    │
                        │ • code       │
                        └──────────────┘
```

#### Règle 4 – Attributs atomiques

```
NON ATOMIQUES                          CORRIGES EN ATTRIBUTS ATOMIQUES
────────────────────────────────       ────────────────────────────────
adresseComplète                        → rue, codePostal, ville, pays
                                       → ou entité ADRESSE séparée

coordonnées (lat/long)                 → latitude, longitude

dateHeureArrivée (date ET heure)       → dateArrivée, heureArrivée

listeSponsors (collection)             → entité SPONSOR
                                       + association SPONSORISE

nomPrenomSociete (3 infos)             → nom, prenom, nomSociete
```

#### Règle 5 – Éviter les redondances

```
❌ MAUVAIS (redondance)
┌──────────────────┐            ┌──────────────────┐
│  VENTE           │            │  LIGNE_VENTE     │
├──────────────────┤ 1,1    0,n ├──────────────────┤
│ • id (PK)        │◄───────────│ • id (PK)        │
│ • dateVente      │ Concerne   │ • idVente (FK)   │
│ • total ← PEUT SE│            │ • idProduit (FK) │
│   RECALCULER !   │            │ • quantité       │
│ • montantTVA     │            │ • prixUnitaire   │
└──────────────────┘            │ • montantLigne   │
                                └──────────────────┘

✅ CORRECT (pas de redondance)
Total = somme de tous les montantLigne
MontantTVA = total * taux (si besoin, le calculer)

Si VRAIMENT on veut garder 'total' pour performance:
→ L'énoncé DOIT le demander explicitement
→ Et il faut justifier qu'on le met à jour après chaque vente
```

#### Règle 6 – Identifiants bien choisis

```
MAUVAIS IDENTIFIANT             BON IDENTIFIANT
─────────────────────           ───────────────
email (change !)                idUtilisateur (PK)
telephone (change !)            email (attribut simple)
(nom, prenom) multi-attrib      Et garder (nom, prenom) comme clé métier
numéro auto-incr instable       code métier stable
```

### 3.3. Associations particulières

#### Association réflexive

```
EXEMPLE : Élève mentor d'un autre Élève

┌──────────────────┐
│    ÉLÈVE         │
├──────────────────┤
│ • numéro (PK)    │
│ • nom            │
│ • prénom         │
└──────────────────┘
        ▲  ↓
        │  │
        └──┘
       0,1 (menteur) ← rôles obligatoires !
       0,n (mentoré)

Est mentor de

Lecture :
- Un élève peut mentorer AUCUN OU PLUSIEURS autres élèves
- Un élève peut être mentoré par AU PLUS UN élève
```

#### Association n-aire (n > 2)

```
EXEMPLE : Cours a lieu dans une Salle pour une Promotion

┌──────────────┐     ┌──────────────┐
│  COURS       │     │  SALLE       │
├──────────────┤     ├──────────────┤
│ • id (PK)    │     │ • id (PK)    │
│ • nom        │     │ • numéro     │
│ • durée      │     │ • capacité   │
└──────────────┘     └──────────────┘
         ▲                    ▲
         │                    │
         └────────┬───────────┘
                  │
              A lieu dans
           (association n-aire)
                  │
         ┌────────┴───────────┐
         │                    ▼
    ┌──────────────┐
    │ PROMOTION    │
    ├──────────────┤
    │ • code (PK)  │
    │ • année      │
    └──────────────┘

Contraintes :
- Un cours a lieu dans EXACTEMENT UNE salle et UNE promotion
- Une salle peut accueillir PLUSIEURS cours
- Une promotion peut avoir PLUSIEURS cours
```

---

## 4. TRADUCTION MEA → MODÈLE RELATIONNEL

⭐ **C'EST LA PARTIE LA PLUS IMPORTANTE ET LA PLUS TESTÉE AU PARTIEL**

### 4.1. Principes généraux

```
NIVEAU CONCEPTUEL (MEA)
    ↓
    └─ Chaque ENTITÉ → TABLE
    └─ Chaque ASSOCIATION → dépend des multiplicités
       ├─ (1,1)—(1,n) → FK dans table côté n
       ├─ (1,1)—(1,1) → fusion OU FK
       └─ (n,n) → NOUVELLE TABLE

NIVEAU LOGIQUE (MODÈLE RELATIONNEL)
```

### 4.2. Traduction des entités - Schémas détaillés

#### Schéma basique

```
MEA - ENTITÉ
┌────────────────────┐
│   PROMOTION        │
├────────────────────┤
│ • code (PK)        │← Identifiant
│ • anneeDiplomante  │
│ • etablissement    │
│ • apprentissage    │
└────────────────────┘

        ↓ TRADUCTION

MR - RELATION (TABLE)
┌─────────────────────────────────────────────────┐
│  PROMOTION                                      │
├─────────────────────────────────────────────────┤
│  code (PK)        VARCHAR(10)                   │
│  anneeDiplomante  INT                          │
│  etablissement    VARCHAR(255)                 │
│  apprentissage    BOOLEAN                      │
└─────────────────────────────────────────────────┘
```

### 4.3. Traduction des associations binaires - CAS PAR CAS

#### CAS 1 – Association (x,1) — (x,n) ⭐ LE PLUS COURANT

```
MEA
┌──────────────┐ 1,1      0,n ┌────────────────┐
│  ÉLÈVE       │◄──────────────│  PROMOTION     │
├──────────────┤ Appartient à ├────────────────┤
│ • numéro(PK) │                │ • code (PK)    │
│ • nom        │                │ • année        │
│ • prénom     │                │ • établissement│
└──────────────┘                └────────────────┘

RÈGLE : FK du côté (n) pointant vers (1)

        ↓ TRADUCTION

MR - RELATIONS
┌──────────────────────────────────────┐
│  ÉLÈVE                               │
├──────────────────────────────────────┤
│  numéro (PK)         INT             │
│  nom                 VARCHAR(255)    │
│  prénom              VARCHAR(255)    │
│  promoCode (FK→PROM) VARCHAR(10)     │← FK du côté (n)
└──────────────────────────────────────┘

┌────────────────────────────────────┐
│  PROMOTION                         │
├────────────────────────────────────┤
│  code (PK)           VARCHAR(10)    │
│  année               INT            │
│  établissement       VARCHAR(255)   │
└────────────────────────────────────┘

INTERPRÉTATION:
- Chaque élève DOIT avoir une promotion (1,1)
- Chaque promotion peut avoir plusieurs élèves (0,n)
- La FK "promoCode" dans ÉLÈVE force cette contrainte
```

#### CAS 1b – Avec attributs d'association

```
MEA (association WITH attributes)
┌──────────────┐ 1,1      0,n ┌────────────────┐
│  ÉLÈVE       │◄──────────────│  COURS         │
├──────────────┤ S'inscrit à├────────────────┤
│ • numéro(PK) │ • date        │ • id (PK)      │
│ • nom        │ • note        │ • titre        │
│ • prénom     │                │ • duree        │
└──────────────┘                └────────────────┘

RÈGLE : Les attributs de l'association vont côté (n)

        ↓ TRADUCTION

MR
┌──────────────────────────────────────┐
│  ÉLÈVE                               │
├──────────────────────────────────────┤
│  numéro (PK)         INT             │
│  nom                 VARCHAR(255)    │
│  prénom              VARCHAR(255)    │
└──────────────────────────────────────┘

┌────────────────────────────────────────┐
│  COURS                                 │
├────────────────────────────────────────┤
│  id (PK)             INT               │
│  titre               VARCHAR(255)      │
│  duree               INT               │
└────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  INSCRIPTION                           │← NOUVELLE TABLE  │
├────────────────────────────────────────┤
│  eleveNum (FK→ELEVE)  INT              │
│  coursId (FK→COURS)   INT              │
│  date                 DATE             │← Attributs assoc
│  note                 FLOAT            │← dans cette table
└────────────────────────────────────────┘

OÙ:
PK(INSCRIPTION) = (eleveNum, coursId)
```

#### CAS 2 – Association (x,1) — (x,1)

```
MEA - OPTION 1 : FUSION
┌──────────────────┐ 1,1      1,1 ┌────────────────┐
│  PERSONNE        │◄──────────────│  PERMIS        │
├──────────────────┤ Possède    ├────────────────┤
│ • id (PK)        │                │ • numéro (PK)  │
│ • nom            │                │ • dateExpire   │
│ • prénom         │                │ • categorie    │
│ • dateNaissance  │                └────────────────┘
└──────────────────┘

        ↓ TRADUCTION

MR - FUSION EN UNE SEULE TABLE
┌────────────────────────────────────────┐
│  PERSONNE                              │
├────────────────────────────────────────┤
│  id (PK)              INT              │
│  nom                  VARCHAR(255)     │
│  prénom               VARCHAR(255)     │
│  dateNaissance        DATE             │
│  permisNum            VARCHAR(20)      │
│  permisDateExpire     DATE             │
│  permisCategorie      VARCHAR(10)      │
└────────────────────────────────────────┘

AVANTAGES: Une seule table, plus simple
INCONVÉNIENTS: Redondance si une personne n'a pas de permis


────────────────────────────────────────────────────────

MEA - OPTION 2 : CLÉS ÉTRANGÈRES
        ↓ TRADUCTION

MR - DEUX TABLES + FK
┌────────────────────────────────────────┐
│  PERSONNE                              │
├────────────────────────────────────────┤
│  id (PK)              INT              │
│  nom                  VARCHAR(255)     │
│  prénom               VARCHAR(255)     │
│  dateNaissance        DATE             │
│  permisNum (FK)       VARCHAR(20)      │
└────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  PERMIS                                │
├────────────────────────────────────────┤
│  numéro (PK)          VARCHAR(20)      │
│  dateExpire           DATE             │
│  categorie            VARCHAR(10)      │
└────────────────────────────────────────┘

AVANTAGES: Plus de flexibilité, pas de redondance
INCONVÉNIENTS: Deux tables à gérer
```

#### CAS 3 – Association (x,n) — (x,n) ⭐ TRÈS IMPORTANT

```
MEA - ASSOCIATION (n,n)
┌──────────────┐ 0,n      0,n ┌────────────────┐
│  CLIENT      │◄──────────────│  PRODUIT       │
├──────────────┤ Achète    ├────────────────┤
│ • id (PK)    │                │ • id (PK)      │
│ • nom        │                │ • nom          │
│ • email      │                │ • prix         │
└──────────────┘                └────────────────┘

RÈGLE : NOUVELLE TABLE d'association avec FKs des deux côtés

        ↓ TRADUCTION

MR - TROIS TABLES
┌────────────────────────────────────────┐
│  CLIENT                                │
├────────────────────────────────────────┤
│  id (PK)              INT              │
│  nom                  VARCHAR(255)     │
│  email                VARCHAR(255)     │
└────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  PRODUIT                               │
├────────────────────────────────────────┤
│  id (PK)              INT              │
│  nom                  VARCHAR(255)     │
│  prix                 FLOAT            │
└────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  ACHAT ← TABLE D'ASSOCIATION           │
├────────────────────────────────────────┤
│  clientId (FK→CLIENT)  INT             │
│  produitId (FK→PRODUIT) INT            │
│  quantité              INT             │
│  dateAchat             DATE            │
├────────────────────────────────────────┤
│  PK(ACHAT) = (clientId, produitId)    │
│  OU ajouter une clé neutre idAchat    │
└────────────────────────────────────────┘

INTERPRÉTATION:
- Un CLIENT peut ACHETER plusieurs PRODUITS
- Un PRODUIT peut être ACHETÉ par plusieurs CLIENTS
- Table ACHAT représente chaque occurrence d'association
```

#### CAS 3b – Association (n,n) avec attributs

```
MEA
┌──────────────┐ 0,n      0,n ┌────────────────┐
│  ÉTUDIANT    │◄──────────────│  COURS         │
├──────────────┤ S'inscrit   ├────────────────┤
│ • id (PK)    │ • date        │ • id (PK)      │
│ • nom        │ • note finale │ • nom          │
│              │                │ • credits      │
└──────────────┘                └────────────────┘

        ↓ TRADUCTION

MR
┌────────────────────────────────────────┐
│  ÉTUDIANT                              │
├────────────────────────────────────────┤
│  id (PK)              INT              │
│  nom                  VARCHAR(255)     │
└────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  COURS                                 │
├────────────────────────────────────────┤
│  id (PK)              INT              │
│  nom                  VARCHAR(255)     │
│  credits              INT              │
└────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  INSCRIPTION ← ATTRIBUTS ICI            │
├────────────────────────────────────────┤
│  etudiantId (FK→ETUDIANT)  INT         │
│  coursId (FK→COURS)        INT         │
│  date                      DATE        │
│  noteFinale                FLOAT       │
├────────────────────────────────────────┤
│  PK(INSCRIPTION) = (etudiantId, coursId) │
└────────────────────────────────────────┘
```

#### CAS 4 – Association n-aire (n > 2)

```
MEA - ASSOCIATION 3-AIRE
┌──────────────┐      ┌────────────────┐
│  COURS       │      │  SALLE         │
├──────────────┤      ├────────────────┤
│ • id (PK)    │      │ • id (PK)      │
│ • titre      │      │ • numéro       │
│ • duree      │      │ • capacité     │
└──────────────┘      └────────────────┘
         ▲                      ▲
         │                      │
         └──────────┬───────────┘
                    │
               A lieu dans
             (heure départ)
                    │
         ┌──────────┴──────────┐
         │                     ▼
         │            ┌────────────────┐
         │            │  PROMOTION     │
         │            ├────────────────┤
         │            │ • code (PK)    │
         │            │ • année        │
         │            └────────────────┘
         │
         └─ Association à 3 entités

        ↓ TRADUCTION

MR - NOUVELLE TABLE AVEC 3 FKs
┌───────────────────────────────────────────┐
│  COURS                                    │
├───────────────────────────────────────────┤
│  id (PK)              INT                 │
│  titre                VARCHAR(255)        │
│  duree                INT                 │
└───────────────────────────────────────────┘

┌───────────────────────────────────────────┐
│  SALLE                                    │
├───────────────────────────────────────────┤
│  id (PK)              INT                 │
│  numéro               VARCHAR(20)         │
│  capacité             INT                 │
└───────────────────────────────────────────┘

┌───────────────────────────────────────────┐
│  PROMOTION                                │
├───────────────────────────────────────────┤
│  code (PK)            VARCHAR(10)         │
│  année                INT                 │
└───────────────────────────────────────────┘

┌───────────────────────────────────────────┐
│  SESSION ← TABLE POUR ASSOCIATION 3-AIRE  │
├───────────────────────────────────────────┤
│  coursId (FK→COURS)       INT             │
│  salleId (FK→SALLE)       INT             │
│  promoCode (FK→PROMOTION) VARCHAR(10)     │
│  heureDepart              TIME            │
├───────────────────────────────────────────┤
│  PK(SESSION) = (coursId, salleId, promoCode) │
└───────────────────────────────────────────┘
```

### 4.4. TABLEAU RÉCAPITULATIF DES RÈGLES DE TRADUCTION

```
┌─────────────────────────────────────┬──────────────────────────────────┐
│  MEA - MULTIPLICITÉS                │  MR - STRUCTURE RÉSULTANTE       │
├─────────────────────────────────────┼──────────────────────────────────┤
│                                     │                                  │
│  ENTITÉ A                           │  Table A: attributs A + clé PK   │
│                                     │                                  │
├─────────────────────────────────────┼──────────────────────────────────┤
│                                     │                                  │
│  (x,1)—(x,n)                        │  FK côté (n) → pointant (1)      │
│  Assoc: attributs optionnels        │  Attrib. assoc. côté (n)         │
│                                     │                                  │
├─────────────────────────────────────┼──────────────────────────────────┤
│                                     │                                  │
│  (x,1)—(x,1)                        │  OU Fusion (1 table)             │
│                                     │  OU FK dans un sens              │
│                                     │                                  │
├─────────────────────────────────────┼──────────────────────────────────┤
│                                     │                                  │
│  (x,n)—(x,n)                        │  Nouvelle table d'association    │
│  Assoc: attributs (date, note...)  │  avec FKs des 2 côtés            │
│                                     │  + attributs de l'assoc.         │
│                                     │  PK = (FK1, FK2) ou clé neutre  │
│                                     │                                  │
├─────────────────────────────────────┼──────────────────────────────────┤
│                                     │                                  │
│  n-aire (n > 2)                     │  Nouvelle table avec FK vers     │
│                                     │  CHAQUE entité participante      │
│                                     │  PK = (FK1, FK2, ..., FKn)      │
│                                     │                                  │
└─────────────────────────────────────┴──────────────────────────────────┘
```

### 4.5. Exemple complet : De MEA à MR

```
MEA COMPLET - GESTION DE COMMANDES

┌─────────────────┐ 1,1    0,n ┌─────────────────┐
│   CLIENT        │◄───────────│   COMMANDE      │
├─────────────────┤ Passe  ├─────────────────┤
│ • id (PK)       │            │ • id (PK)       │
│ • nom           │            │ • dateCommande  │
│ • email         │            │ • dateExpedition│
│ • adresse       │            └─────────────────┘
└─────────────────┘                    │
                                       │ 1,1  0,n
                           ┌───────────┘
                           │
                    Contient
                           │
                    ┌──────▼──────┐
                    │  LIGNE_CMD  │
                    ├─────────────┤
                    │ • id (PK)   │
                    │ • quantité  │
                    │ • prix      │
                    └──────▲──────┘
                           │ 0,n  1,1
                    ┌──────┴──────┐
                    │             │
              Concerne
                    │
            ┌──────▼───────┐
            │   PRODUIT    │
            ├──────────────┤
            │ • id (PK)    │
            │ • nom        │
            │ • stock      │
            │ • prixUnit   │
            └──────────────┘

        ↓ TRADUCTION EN MR

TABLES:

CLIENT(id PK, nom, email, adresse)

COMMANDE(id PK, clientId FK→CLIENT, dateCommande, dateExpedition)

LIGNE_COMMANDE(
  id PK,
  commandeId FK→COMMANDE,
  produitId FK→PRODUIT,
  quantité,
  prix
)

PRODUIT(id PK, nom, stock, prixUnit)

CONTRAINTES:
- clientId dans COMMANDE : NOT NULL (1,1)
- commandeId dans LIGNE_COMMANDE : NOT NULL
- produitId dans LIGNE_COMMANDE : NOT NULL
```

---

## 5. LECTURE, CRITIQUE ET CORRECTION D'UN MEA

Très présent dans les annales :
- QCM / Vrai–Faux d'interprétation à partir d'un MEA donné
- Détection de problèmes (multiplicités, identifiants, attributs non atomiques, redondance)
- Propositions de corrections minimales

### 5.1. Interprétation (Vrai/Faux)

**Types de questions :**
- "On peut créer une équipe sans participant." V/F ?
- "Un participant peut ne pas rejoindre d'équipe." V/F ?
- "Une matière n'existe que si au moins un élève y est inscrit." V/F ?

**Méthode pour répondre :**

```
ÉTAPE 1: Repérer les multiplicités min/max dans le modèle

ÉTAPE 2: Se poser les bonnes questions:
- min = 0 côté entité X ? → X peut exister sans association
- min = 1 côté entité X ? → X DOIT participer à association
- max = 1 côté entité X ? → X participe au plus 1 fois
- max = n côté entité X ? → X peut participer plusieurs fois

ÉTAPE 3: Répondre V ou F basé UNIQUEMENT sur le modèle

EXEMPLE:
MEA: Élève —(Appartient à)— Promotion
     1,1                         0,n

Q1: "On peut créer une promotion sans élève." V/F
A1: V (multiplicité 0,n côté Élève: min=0, donc Promotion peut exister sans Élève)

Q2: "Un élève peut ne pas appartenir à une promotion." V/F
A2: F (multiplicité 1,1 côté Élève: min=1, donc Élève DOIT appartenir à Promotion)

Q3: "Une promotion peut contenir plusieurs élèves." V/F
A3: V (multiplicité 0,n côté Promotion: max=n, donc plusieurs Élèves)
```

### 5.2. Problèmes typiques à repérer

```
CHECKLIST DES PROBLÈMES COURANTS:

☐ Attribut non atomique
  - "adresseComplète" au lieu de (rue, CP, ville)
  - "listeSponsors" (collection)
  - "coordonnées" au lieu de (latitude, longitude)
  → Solution: découper ou créer entité

☐ Redondance
  - "total" d'une vente recalculable
  - même info en deux endroits différents
  → Solution: enlever l'attribut redondant

☐ Identifiant mal choisi
  - email (peut changer)
  - numéro métier instable
  - multi-attribut inutile (mieux: clé neutre)
  → Solution: remplacer par clé neutre

☐ Référence à autre entité dans attribut
  - "promotionDeLEleve" dans Élève
  - "autorDuLivre" dans Livre (si c'est une FK)
  → Solution: utiliser association

☐ Contrainte métier non modélisée
  - Ex: "Une vente = standardiste OU commercial (pas les deux)"
  → Solution: ajuster structure ou ajouter constraint

☐ Association missing ou mal placée
  - Besoin de représenter relation absente
  → Solution: ajouter association
```

---

## 6. UML – CE QU'IL FAUT SAVOIR POUR LE PARTIEL

### 6.1. UML vs MEA - Schéma comparatif

```
MERISE (MEA)                           UML (Diagramme de classes)

Entité                                 ≈ Classe
┌──────────────┐                       ┌──────────────┐
│   ÉLÈVE      │                       │    Élève     │
├──────────────┤                       ├──────────────┤
│ • numéro     │                       │ - numéro     │
│ • nom        │                       │ - nom        │
│ • prénom     │                       │ - prénom     │
└──────────────┘                       │              │
                                       │ + methodes() │
Identifiant (souligné)                 └──────────────┘
                                       
Association                            ≈ Association
┌──────────┐ 1,1    0,n ┌────────┐    ┌──────────┐ 1    0..* ┌────────┐
│  Élève   │◄───────────│ Promotion  Élève     |──────── Promotion
└──────────┘ Appartient└────────┘    └──────────┘        └────────┘

Multiplicité Merise:                   Multiplicité UML:
(min, max)                             min..max
- (0,1) = au plus un                   - 0..1 = au plus un
- (1,1) = exactement un                - 1 = exactement un
- (0,n) = zéro à plusieurs             - 0..* = zéro à plusieurs
- (1,n) = au moins un                  - 1..* = au moins un

Instance d'entité                      ≈ Objet
dupont : Élève                         e1 : Élève
(nom = "Dupont", ...)                  (numéro = 12345, ...)
```

### 6.2. Types de diagrammes UML (à citer)

```
DIAGRAMMES UML
│
├─ DIAGRAMMES DE STRUCTURE
│  ├─ Diagramme de CLASSES ✅ (le plus courant pour les données)
│  ├─ Diagramme d'OBJETS (instances)
│  ├─ Diagramme de COMPOSANTS
│  ├─ Diagramme de DÉPLOIEMENT
│  ├─ Diagramme de PAQUETAGES
│  └─ ...
│
└─ DIAGRAMMES DE COMPORTEMENT
   ├─ Diagramme d'ACTIVITÉS
   ├─ Diagramme de CAS D'UTILISATION
   ├─ Diagramme d'ÉTATS-TRANSITIONS
   │
   └─ Diagrammes d'INTERACTION
      ├─ Diagramme de SÉQUENCE ✅
      ├─ Diagramme de COMMUNICATION
      └─ ...

À l'examen: citer 3 types (classe, séquence, cas d'utilisation suffisent)
```

---

## 7. VOCABULAIRE, ACRONYMES ET QUESTIONS DE COURS CLASSIQUES

### 7.1. Correspondance de vocabulaire

```
Modèle relationnel           MEA
────────────────────       ──────
Relation                   Entité
Table                      (même entité)
Lien                       Association
Propriété / Colonne        Attribut
Instance / Tuple           Occurrence
Clé primaire               Identifiant
Clé étrangère              (résultat d'association)
Spécialisation / Héritage  Héritage (généralisation)
```

### 7.2. Acronymes à connaître

```
SGBDR
System de Gestion de Bases de Données Relationnelles
= logiciel qui gère les BD (MySQL, PostgreSQL, Oracle...)

CRUD
Create, Read, Update, Delete
= 4 opérations de base sur les données

UML
Unified Modeling Language
= langage de modélisation standardisé

MCD
Modèle Conceptuel de Données = MEA

MLD
Modèle Logique de Données = Modèle relationnel

MPD
Modèle Physique de Données = SQL implémenté

PK
Primary Key = Clé primaire

FK
Foreign Key = Clé étrangère

SI
Système d'Information
```

### 7.3. Questions types de cours

```
Q1: Définir "système d'information"
A1: Ensemble structuré d'informations, acteurs et processus
    permettant de collecter, stocker et mettre à disposition l'info.

Q2: Différence donnée / information
A2: Donnée = valeur brute (18)
    Information = donnée interprétée (18°C dans salle IG2I)

Q3: Hiérarchie d'abstraction + noms des modèles
A3: Conceptuel (MCD/MEA) → Logique (MLD/MR) → Physique (MPD/SQL)

Q4: Association réflexive
A4: Lien entre une entité et elle-même, avec rôles obligatoires
    Ex: Élève mentor de Élève (mentor / mentoré)

Q5: Identifiant implicite d'une association binaire
A5: = combinaison de l'identifiant des deux entités participantes

Q6: Différence Merise vs UML
A6: Merise = méthode complète (MCD/MLD/MPD, traitements)
    UML = langage de modélisation standardisé (diagrammes multiples)

Q7: Citer 3 diagrammes UML
A7: - Diagramme de classes
    - Diagramme de séquence
    - Diagramme de cas d'utilisation

Q8: Composants du SI
A8: Acteurs, Processus, Informations, Données, BDD, Matériels, Applications
    Système informatique = Matériels + BDD + Applications
```

---

## 8. STRATÉGIE DE RÉVISION ET ENTRAÎNEMENTS RECOMMANDÉS

### 8.1. Ce qui tombe presque à tous les coups

#### 1) Gros exercice de modélisation (10–12 points)

**Énoncés types :**
- Plateforme de partage de fichiers (NextCloud)
- Courses de drones
- Réservation de vols par agence de voyages
- Gestion des salles et du matériel
- Système de location de films

**À faire :**
- ✅ Modèle entité–association **complet**
- ✅ **Identifiants, attributs, multiplicités clairs**
- ✅ **Justifier chaque choix de conception**
- ✅ **Parfois :** diagramme d'instances

#### 2) Exercice de compréhension / modification (5–8 points)

- Vrai/Faux d'interprétation du MEA
- Corrections : attributs non atomiques, redondances
- Traduction en modèle relationnel
- **Bonus :** petites requêtes SQL

#### 3) Questions de cours (3–4 points)

- Définitions : SI, donnée vs information
- Hiérarchie d'abstraction
- Acronymes SGBDR/CRUD/UML
- Vocabulaire et correspondances
- Différence Merise/UML

### 8.2. Calendrier de révision (4 semaines)

```
SEMAINE 1 – FONDAMENTAUX
┌─────────────────────────────────────────┐
│ Jour 1-2: Lire les diapos CSI-01/02    │
│ Jour 3-4: Refaire 2 MEA à partir zéro │
│           (énoncé + MEA + schémas)     │
│ Jour 5-6: Questions de cours (définit) │
│ Jour 7: Bilan + ajuster zones faibles  │
└─────────────────────────────────────────┘

SEMAINE 2 – TRADUCTION & CAS D'ÉTUDE
┌─────────────────────────────────────────┐
│ Jour 1-2: Relire CSI-03 (traduction)   │
│ Jour 3-4: Traduire 2 MEA en MR complet│
│           (avec les 4 cas: 1,n / 1,1...) │
│ Jour 5-6: Exercices Vrai/Faux (sujets) │
│ Jour 7: Corrections + ajustements      │
└─────────────────────────────────────────┘

SEMAINE 3 – CRITIQUE & UML
┌─────────────────────────────────────────┐
│ Jour 1-2: Identifier problèmes MEA     │
│           (attributs, redondance...)    │
│ Jour 3-4: Proposer corrections min.    │
│ Jour 5-6: Vocabulaire + UML (CSI-04)   │
│ Jour 7: Mock test 1h30 (complet)       │
└─────────────────────────────────────────┘

SEMAINE 4 – ENTRAÎNEMENT INTENSIF
┌─────────────────────────────────────────┐
│ Jour 1-2: Sujet complet 2024-2025      │
│           (conditions examen: 3h30)     │
│ Jour 3-4: Sujet complet 2022-2023      │
│ Jour 5-6: Sujet complet 2021-2022      │
│ Jour 7: Révision fiche + repos         │
└─────────────────────────────────────────┘
```

### 8.3. Checklist avant le partiel

```
JE SAIS:
☐ Définir système d'information
☐ Expliquer hiérarchie d'abstraction (MCD → MLD → MPD)
☐ Construire un MEA à partir d'un énoncé
☐ Identifier attributs non atomiques et les corriger
☐ Détecter redondances et les justifier
☐ Lire multiplicités dans les 2 sens
☐ Repérer associations réflexives et n-aires
☐ Traduire MEA en MR (tous les cas)
☐ Interpréter un modèle (Vrai/Faux)
☐ Proposer corrections minimales
☐ Citer 3+ diagrammes UML
☐ Donner différence Merise/UML
☐ Définir SGBDR, CRUD, UML
☐ Distinguer donnée vs information
```

### 8.4. Conseils pratiques le jour du partiel

```
AVANT (30 min avant start)
├─ Bien dormir la veille
├─ Petit-déjeuner normal
├─ Apporter stylos + crayons
├─ Laisser téléphone dehors
└─ Mindset: "Je vais faire de mon mieux"

PENDANT (examen)
├─ Lire ENTIÈREMENT l'énoncé (5 min)
├─ Commencer par ce que tu maîtrises
├─ Pour MEA:
│  ├─ Identifier entités (groupes nominaux)
│  ├─ Identifier associations (groupes verbaux)
│  ├─ Placer multiplicités (2 sens obligatoire)
│  ├─ Vérifier: pas de FK en attribut, pas de listes
│  └─ Justifier choix de conception
├─ Pour traduction MR:
│  ├─ Rappel des 4 cas
│  ├─ Placer FKs du côté (n)
│  ├─ Créer tables d'assoc. si (n,n)
│  └─ Bien former clés primaires
├─ Pour questions cours:
│  ├─ Définitions précises (1-2 phrases)
│  └─ Pas besoin de développer trop
└─ Vérifier: présentation lisible, pas d'erreur évidente

APRÈS
└─ Pas de stress, tu as donné ton max!
```

---

## RÉSUMÉ ULTRA-RAPIDE

```
🎯 OBJECTIF FINAL

Savoir faire en 3h30:
1. Lire un énoncé complexe (5 min)
2. Construire un MEA correct (60 min)
3. Critiquer un modèle fourni (30 min)
4. Traduire en modèle relationnel (45 min)
5. Répondre à questions cours (30 min)

PIÈGES À ÉVITER:
❌ Référence à entité dans attribut
❌ Listes/collections en attribut
❌ Oublier attributs d'association
❌ Mal placer les FKs (doivent côté n)
❌ Oublier table d'assoc. pour (n,n)
❌ Multiplicités pas lues 2 sens
❌ Redondances évidentes pas éliminées

FORCE-TOI À:
✅ Justifier CHAQUE choix
✅ Lire multiplicités 2 fois
✅ Vérifier atomicité attributs
✅ Tracer un diagramme d'instances (mental)
✅ Traduire cas par cas (1,n puis n,n)
✅ Répondre Vrai/Faux avec logique pure
```

---

## Ressources et contacts

**Sujets d'entraînement recommandés:**
- 2024–2025 : Plateforme NextCloud (partage fichiers)
- 2023–2024 : Compétition sportive
- 2022–2023 : Courses de drones
- 2021–2022 : Gestion salles + Rétro-Vidéo + Cluster calcul
- 2022 (réparation) : Vols d'avion + Enseignants/Élèves

**Diapos officielles à relire:**
- CSI-01 : Présentation + SI
- CSI-02 : MEA en détail
- CSI-03 : Traduction MR
- CSI-04 : UML intro

---

**BON COURAGE POUR TON PARTIEL ! 🎓**

_Fait avec ❤️ et basé sur les vrais sujets CSI (LE2) 2021–2025_
