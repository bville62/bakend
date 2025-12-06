# FICHE DE RÉVISION ULTIME – CSI (LE2)

## Objectif
Maîtriser tout ce qui tombe au partiel de **Conception des Systèmes d'Information (CSI)** à partir du cours et des anciens sujets (2021–2022, 2022–2023, 2023–2024, 2024–2025).

---

## Plan de la fiche
1. [Système d'information et contexte du cours](#1-système-dinformation-et-contexte-du-cours)
2. [Hiérarchie d'abstraction (MCD / MLD / MPD)](#2-hiérarchie-dabstraction-très-fréquent)
3. [Modèle entité–association (MEA)](#3-modèle-entité--association-mea)
4. [Traduction MEA → Modèle relationnel](#4-traduction-mea--modèle-relationnel)
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
- Acteurs
- Processus
- Informations
- Données
- Bases de données
- Matériels
- Applications

**Le système informatique** =
- **Matériels + Bases de données + Applications**

**Donc :**
- **SI** = plus large (inclut organisation, processus, acteurs, etc.)
- **Système informatique** = partie technique du SI

### 1.3. Donnée vs information

| Terme | Définition | Exemple |
|-------|-----------|---------|
| **Donnée** | Valeur brute, non interprétée | 18, "LE2", "2025-12-06", "IG2I-SS05" |
| **Information** | Donnée interprétée dans un contexte, qui a du sens | "Température = 18 °C dans la salle IG2I-SS05 ce matin" |

À l'examen, on attend :
- Une phrase claire : **l'information est une donnée interprétée**
- Éventuellement un exemple (non obligatoire)

---

## 2. HIÉRARCHIE D'ABSTRACTION (TRÈS FRÉQUENT)

### 2.1. Les trois niveaux

| Niveau | Nom du modèle | Caractéristiques |
|--------|---------------|------------------|
| **Conceptuel** | **MCD** (Modèle Conceptuel de Données) = **MEA** (Modèle Entité–Association) | Représente les **informations et leurs liens**. Indépendant de la technologie. |
| **Logique** | **MLD** (Modèle Logique de Données) | **Modèle relationnel** dans ce cours (tables, colonnes, PK, FK…). Dépend du type de base de données. |
| **Physique** | **MPD** (Modèle Physique de Données) | Définition SQL, types concrets, index, contraintes physiques. Dépend du SGBD choisi. |

### 2.2. À retenir par cœur

✅ **Ordre du plus abstrait au plus concret :**
```
Conceptuel (MCD/MEA) → Logique (MLD/MR) → Physique (MPD/SQL)
```

✅ **Noms des modèles** à chaque niveau (MCD / MLD / MPD)

✅ **En CSI**, on travaille surtout sur : **MCD (MEA)** et traduction en **MLD (modèle relationnel)**

---

## 3. MODÈLE ENTITÉ–ASSOCIATION (MEA)

C'est le **cœur du partiel** :
- Gros exercice de modélisation à partir d'un énoncé (drones, vols, salles, NextCloud, etc.)
- Exercice de compréhension et de critique d'un modèle existant

### 3.1. Concepts de base

#### Entité
- **Ensemble d'objets de même nature** (concrets ou abstraits)
- **Exemples :** Client, Produit, Course, Saison, Équipe, Salle, Bâtiment, Vol, Aéroport
- **Notation :** rectangle, **nom au singulier, majuscule initiale**

#### Attribut
- **Donnée unitaire** propre à une entité ou une association
- **Exemples :** nom, prénom, date de naissance, code, durée, prix, langue, email
- **Nom :** plutôt en minuscules ; en Merise accents/espaces tolérés, mais style proche UML : éviter accents et espaces

#### Identifiant
- **Attribut** (ou groupe d'attributs) qui identifie **univoquement** une occurrence d'entité
- Souvent **souligné** dans le MEA

**Deux types :**
- **Clé métier :** a un sens dans le métier (ex : numéro de sécurité sociale, matricule, code salle)
- **Clé neutre :** créée uniquement pour la modélisation (id auto-incrémenté, numéro interne)

**Bonne pratique :**
- Utiliser une **clé neutre simple** comme identifiant (un seul attribut)
- Garder la clé métier comme simple attribut (ex : code, numéro officiel)

#### Association
- **Lien d'une certaine nature** entre entités
- **Exemples :**
  - "Appartient à" entre Élève et Promotion
  - "Passe commande à" entre Client et Fournisseur
  - "Est affecté à" entre Enseignant et Bureau
- **Peut avoir ses propres attributs** (ex : date, quantité, statut, note)

⚠️ **Important :** Une association relie des **entités**, PAS des **attributs**

#### Multiplicités (cardinalités)
Sur chaque arc entre une entité et une association : **(min, max)**

**Valeurs usuelles :**
- `0,1` : au plus un (zéro ou un)
- `1,1` ou `1` : exactement un
- `0,n` ou `0,*` : zéro, un ou plusieurs
- `1,n` : au moins un (un ou plusieurs)
- `X,Y` : entre X et Y inclus (rare)

**Lecture dans les deux sens (TRÈS IMPORTANT) :**

Exemple : Élève —(Appartient à)— Promotion, avec multiplicités `1,1` côté Élève et `0,n` côté Promotion
- **Côté Élève :** "Un élève appartient à **une et une seule** promotion"
- **Côté Promotion :** "Une promotion peut contenir **zéro, un ou plusieurs** élèves"

#### Instance (ou occurrence)
- **Instance d'entité :** un objet concret avec des valeurs d'attributs
  - Ex : `dupont : Élève (nom = "Dupont", prénom = "Martine", âge = 19, …)`
- **Instance d'association :** un lien concret entre instances d'entités
  - Ex : `(dupont, promo_LE1)` pour l'association "Appartient à"

---

### 3.2. Règles importantes et pièges classiques

#### Règle 1 – Pas de références à d'autres entités dans les attributs
- ❌ **Interdit :** un attribut "promotion de l'élève" dans l'entité Élève
- ✅ **Correct :** une **association** "Appartient à" entre Élève et Promotion

#### Règle 2 – Pas de collections (liste, tableau…) comme attribut
- ❌ **Interdit :** "liste des vidéos postées" dans l'entité Utilisateur
- ✅ **Correct :** **association** "Poste" entre Utilisateur et Vidéo
- ❌ **Interdit :** "liste des sponsors" dans Équipe → très suspect (souvent demandé aux examens)

#### Règle 3 – Unicité d'une instance d'association
Pour une association donnée, entre deux mêmes occurrences d'entités, il ne peut y avoir qu'une seule occurrence d'association.

**Si on a besoin de plusieurs liens différents :** on **réifie** l'association
- Exemple : au lieu de "Passe commande à" (Client, Fournisseur, date)
- Créer une entité **Commande** et des associations autour

#### Règle 4 – Attributs atomiques
Un attribut doit contenir **une seule information**.

**Exemples d'attributs NON atomiques :**
- "adresse complète" si on a besoin de séparer rue, code postal, ville
- "listeSponsors" (liste = problème)
- "coordonnées" si on doit distinguer latitude et longitude

**Correction :**
- Découper en plusieurs attributs, OU
- Créer une nouvelle entité si c'est une liste

#### Règle 5 – Éviter les redondances
**Exemple typique dans les sujets :**
- Attribut "total" d'une vente, alors qu'on peut le **recalculer** à partir des lignes de vente et prix unitaire

**À retenir :** Si la donnée peut être recalculée facilement à partir d'autres données stockées, il vaut mieux **ne pas la stocker** (sauf si l'énoncé demande explicitement de conserver ce résumé).

#### Règle 6 – Identifiants bien choisis
L'examen demande parfois : *"L'un des identifiants du modèle est mal choisi. Lequel ? Comment corriger ?"*

**À vérifier :**
- **Unicité réelle** (la valeur doit bien identifier un objet unique)
- **Stabilité** (éviter les valeurs qui changent souvent, ex : email)
- **Minimalité** (éviter un identifiant multi-attribut alors qu'une clé neutre simple serait mieux)

---

### 3.3. Associations particulières

#### Association réflexive
Association entre une entité et elle-même (mais pas la même occurrence)

**Exemples :**
- Élève "Est mentor de" Élève
- Personne "Est père de" Personne

⚠️ **On doit préciser des rôles :** mentor / mentoré, père / enfant, etc.

**Cas typique de question de cours :** *"Qu'est-ce qu'une association réflexive ?"*

#### Association n-aire (n > 2)
Lien entre plus de deux entités

**Exemple :** Cours–Salle–Promotion pour "A lieu dans"

**Deux modélisations possibles :**
1. Directement comme association n-aire
2. Transformée (réifiée) en entité avec des associations binaires

**Exercice classique :** une même situation modélisée avec une association n-aire ou avec une entité

#### Héritage (généralisation / spécialisation)
- Notion vue dans les diapos mais indiquée **"hors programme"** pour la traduction
- **Idée :**
  - Une entité mère (Personne)
  - Des entités filles (Élève, Enseignant)
  - Les filles héritent des attributs de la mère et de ses associations

À connaître au moins en vocabulaire, car cela peut apparaître dans les questions de cours ou dans un MEA à commenter.

---

### 3.4. Méthode pour construire un MEA à partir d'un énoncé

1. **Lire l'énoncé** au moins 2–3 fois

2. **Extraire les groupes nominaux** importants : candidats entités / attributs
   - Ce qui semble "liste d'objets" → candidat entité
   - Ce qui décrit une propriété d'un objet → candidat attribut

3. **Identifier les actions / relations** (groupes verbaux) : candidats associations

4. **Pour chaque entité candidate**, décider :
   - Attributs pertinents
   - Identifiant (clé neutre + éventuelle clé métier)

5. **Pour chaque association :**
   - Entités reliées
   - Sens de lecture
   - Multiplicités min/max en se posant les bonnes questions des deux côtés
   - Attributs d'association si nécessaires (quantité, date, statut…)

6. **Vérifier :**
   - Pas de références à d'autres entités dans les attributs
   - Pas de listes / collections en attribut
   - Pas de redondances évidentes
   - Les contraintes métier importantes de l'énoncé sont bien modélisées

**Entraînement :**
- Refaire les gros énoncés :
  - Courses de drones
  - Réservation de vols par agence de voyages
  - Gestion des salles et du matériel
  - Plateforme de partage de fichiers type NextCloud

---

## 4. TRADUCTION MEA → MODÈLE RELATIONNEL

### 4.1. Principes généraux

- Le modèle logique de données (MLD) prend la forme d'un **modèle relationnel**
- Une **relation** = une **table**
- On conserve les informations de structure : colonnes, types, **clés primaires (PK)** et **clés étrangères (FK)**

**Règles de base :**
- Chaque **entité** → une **table (relation)** avec au minimum ses attributs
- L'**identifiant** de l'entité → **clé primaire (PK)** de la table
- Les **associations** → donnent lieu à des **clés étrangères** ou à des **tables supplémentaires** selon les multiplicités

---

### 4.2. Traduction des entités

**Entité → relation** avec les mêmes attributs

**Choix de la clé primaire (PK) :**
- Souvent un attribut clé neutre (id)
- Ou une clé métier si l'énoncé le justifie (ex : code unique stable)

**Exemple simple :**

Entité MEA
```
Promotion
  code (clé neutre)
  anneeDiplomante
  etablissement
  apprentissage
```

Traduction en MR
```
PROMOTION(code PK, anneeDiplomante, etablissement, apprentissage)
```

---

### 4.3. Traduction des associations binaires

#### Cas 1 – (x,1) – (x,n)
*Où 0,1 ou 1,1 d'un côté ; 0,n ou 1,n de l'autre*

**Règle :** Placer une **clé étrangère (FK)** du côté **(n)** vers le côté **(1)**

- **Sans attributs d'association :** juste une FK dans la table côté (n)
- **Avec attributs d'association :** les attributs sont stockés dans la table côté (n) en même temps que la FK

**Exemple :** "Un élève appartient à une et une seule promotion" / "Une promotion peut contenir plusieurs élèves"
```
ELEVE(idEleve PK, …, promoId FK → PROMOTION)
PROMOTION(codePK, …)
```

#### Cas 2 – (x,1) – (x,1)
*Où 0,1 ou 1,1 des deux côtés*

**Deux possibilités :**
1. **Fusion :** fusionner les deux entités en une seule table (si logique)
2. **OU** placer une FK dans un sens ou dans l'autre

#### Cas 3 – (x,n) – (x,n)
*Où 0,n ou 1,n des deux côtés*

**Règle :** Créer une **nouvelle table** pour l'association

Cette table contient :
- Une **FK** vers la première entité
- Une **FK** vers la deuxième entité
- Éventuels **attributs** de l'association
- La **clé primaire** formée des deux FKs (PK composite) ou d'une clé neutre + ces FKs

**Exemple typique :**

Association "Participe à" entre Pilote et Course avec multiplicités (0,n) — (0,n)
```
PARTICIPATION(piloteId FK, courseId FK, …, PK(piloteId, courseId))
```

#### Cas 4 – Association n-aire (n > 2)

**Règle :** Créer une **nouvelle table** représentant l'association

Cette table contient :
- Une **FK** vers **chaque** entité participante
- Les **attributs** de l'association
- La **clé primaire** formée de la combinaison des FKs (ou clé neutre + FKs)

---

### 4.4. Points d'attention dans la traduction

- Bien garder cohérence entre cardinalités et structure :
  - Côté **(n)** → FK côté **(1)**
  - **(n,n)** → table d'association
- Ne pas oublier les **attributs d'association**
- Choisir des **PK simples** et **stables**
- Pour les associations complexes (avec contraintes métier fortes), bien réfléchir à l'**identifiant** de la table d'association

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
- "Une vente peut être effectuée à la fois par un standardiste et un commercial." V/F ?

**Méthode pour répondre :**
1. Ne se baser que sur le **modèle**, pas sur le bon sens
2. Regarder les **multiplicités min/max** sur chaque arc
3. Se rappeler :
   - `min = 0` : l'objet peut exister sans participer à l'association
   - `min = 1` : l'objet doit participer au moins une fois
   - `max = 1` : au plus une participation
   - `max = n` : plusieurs participations possibles

---

### 5.2. Problèmes typiques à repérer

#### 1) Attribut non atomique
- **Exemple :** "liste sponsors" dans Équipe
- **Correction :** créer une entité Sponsor et une association avec Équipe

#### 2) Identifiant mal choisi
- Identifiant qui change souvent (ex : email)
- Identifiant multi-attribut inutilement complexe
- Absence de clé neutre alors que l'énoncé introduit un numéro interne

#### 3) Redondance
- Attribut "total" d'une vente alors qu'on peut le recalculer à partir des lignes de vente
- Attribut "coordonnées (latitude, longitude)" alors qu'on stocke déjà latitude et longitude séparément

#### 4) Incohérence avec une contrainte de l'énoncé
**Exemple :** "Une vente est effectuée par une seule personne : standardiste OU commercial"
- Si le MEA permet qu'une vente soit reliée à la fois à un standardiste et à un commercial → problème
- Corriger en modifiant la structure (entité Personne, ou contrainte supplémentaire, etc.)

---

### 5.3. Proposer une correction minimale

Quand l'énoncé demande : *"Proposez une modification minimale du modèle pour…"*

✅ **À faire :**
- Ne pas tout refaire
- Ajouter juste ce qu'il faut :
  - une entité
  - une association
  - un attribut
  - un ajustement de multiplicités
- **Toujours :**
  - Expliquer ce que tu ajoutes ou modifies
  - Justifier en quoi cela répond à la demande et évite les redondances

---

### 5.4. Traduction en modèle relationnel à partir du MEA

- Reprendre les règles de la [section 4](#4-traduction-mea--modèle-relationnel)
- Les sujets demandent souvent :
  - Traduction du modèle tel quel (sans les modifications de la question précédente), OU
  - En intégrant les modifications

**Entraînement :**
- Prendre les modèles conceptuels des sujets et :
  - Répondre aux Vrai/Faux
  - Identifier attributs non atomiques, redondances
  - Proposer corrections
  - Traduire en modèle relationnel

---

## 6. UML – CE QU'IL FAUT SAVOIR POUR LE PARTIEL

Le cours UML est une introduction. L'examen s'en sert surtout pour les **questions de cours** :
- Définir UML
- Citer des types de diagrammes
- Comparer MEA (Merise) et diagramme de classes UML
- Quelques éléments de vocabulaire (classe, objet, association, multiplicité, rôle)

### 6.1. Modèle et diagramme

**Modèle**
Consensus sur une **abstraction** représentant de façon simplifiée un aspect d'un système réel pour un objectif donné.

**Diagramme**
Représentation graphique d'une **structure** ou d'une **séquence d'opérations**.
Permet de **visualiser** un modèle (ou une partie).

---

### 6.2. UML : définition et rôle

**UML : Unified Modeling Language**
- **Langage de modélisation standardisé** (par l'OMG) depuis 1997
- Initialement pour le développement logiciel orienté objet
- Mais utilisable **au-delà de l'informatique**

**Points importants :**
- UML est un **LANGAGE** (syntaxe, sémantique), **pas une méthode complète**
- Permet de modéliser :
  - **aspect statique** (structure : diagrammes de classes, objets, composants…)
  - **aspect fonctionnel** (cas d'utilisation)
  - **aspect dynamique** (séquences, activités, états-transitions, etc.)

---

### 6.3. Diagrammes UML à citer

#### Diagrammes de structure
- Diagramme de classes
- Diagramme d'objets
- Diagrammes de composants
- Diagrammes de déploiement
- Diagrammes de paquetages
- Diagrammes de structures composites
- Diagrammes de profils

#### Diagrammes de comportement
- Diagrammes d'activités
- Diagrammes de cas d'utilisation
- Diagrammes d'états-transitions

#### Diagrammes d'interaction
- Diagrammes de séquence
- Diagrammes de communication
- Diagrammes de chronométrage
- Diagrammes d'interaction d'ensemble

**À l'examen :** il suffit souvent de citer **3 types de diagrammes UML** différents.

---

### 6.4. Diagramme de classes vs MEA Merise

#### Ressemblances
- Les deux représentent la **structure des données**
- **Classes UML** ≈ **entités MEA**
- **Associations UML** ≈ **associations MEA**
- **Multiplicités UML** (0..1, 1..1, 0..*, 1..*) ≈ **cardinalités Merise** (0,1 / 1,1 / 0,n / 1,n)

#### Différences

| Aspect | Merise | UML |
|--------|--------|-----|
| **Type** | Méthode complète | Langage de modélisation |
| **Domaine** | Systèmes d'information | Large spectre (logiciel, systèmes, etc.) |
| **Modèle de données** | Entité–association (MCD) | Diagramme de classes |
| **Approche** | Données + Traitements (MCD, MLD, MPD) | Multiaspects (structure, comportement, interaction) |

---

### 6.5. Vocabulaire UML de base

**Classe**
- Type abstrait caractérisé par des attributs et des opérations
- Notation typique : rectangle avec 3 compartiments (nom, attributs, opérations)

**Objet (instance)**
- Exemple concret de classe
- Notation : `nomInstance : NomClasse`, avec éventuellement les valeurs des attributs

**Association UML**
- Lien entre deux classes (ou plus)
- Multiplicités comme en Merise : 0..1, 1, 0..*, 1..*…

**Rôle**
- Nom placé à l'extrémité d'une association
- **Obligatoire** pour les associations réflexives ou multiples entre mêmes classes

---

## 7. VOCABULAIRE, ACRONYMES ET QUESTIONS DE COURS CLASSIQUES

### 7.1. Correspondance de vocabulaire (fréquent)

Dans les sujets, on trouve souvent des **appariements** :

| Concept model. relationnel | Concept MEA |
|---------------------------|------------|
| Relation | **Entité** ou Association |
| Lien | **Association** |
| Propriété | **Attribut** |
| Instance | **Occurrence** |
| Spécialisation | **Héritage** |

**Exemple d'appariement :**
```
(A) Relation        ↔  (c) Table
(B) Lien            ↔  (a) Association
(C) Propriété       ↔  (b) Attribut
(D) Instance        ↔  (d) Occurrence
```

---

### 7.2. Acronymes à connaître

**SGBDR**
- **Système de Gestion de Bases de Données Relationnelles**

**CRUD**
- **Create, Read, Update, Delete**
- Opérations de base sur les données

**UML**
- **Unified Modeling Language**

---

### 7.3. Questions types de cours

**Exemples de questions récurrentes :**
1. Donner la définition de **"système d'information"**
2. Donner la différence entre **donnée et information**
3. Rappeler la **hiérarchie d'abstraction** (conceptuel/logique/physique) et le modèle associé à chaque niveau
4. Définir **SGBDR, CRUD, UML**
5. Expliquer ce qu'est une **association réflexive** dans le MEA
6. Expliquer ce qu'est l'**identifiant implicite** d'une association binaire
7. Donner une **différence** entre modèle entité–association Merise et diagramme de classes UML
8. Citer **trois types de diagrammes UML**
9. Rappeler les **6 composants d'un système d'information**
10. Parmi les 6 composants du SI, lesquels forment le **système informatique** ?

---

## 8. STRATÉGIE DE RÉVISION ET ENTRAÎNEMENTS RECOMMANDÉS

### 8.1. Ce qui tombe presque à tous les coups

#### 1) Gros exercice de modélisation (10–12 points)
**Énoncé long** (drones, vols, salles, NextCloud…)

À faire :
- ✅ Modèle entité–association **complet**
- ✅ **Identifiants, attributs, multiplicités**
- ✅ **Choix de conception** expliqués
- ✅ **Parfois :** diagramme d'instances

#### 2) Exercice de compréhension / modification d'un MEA (5–8 points)
- Vrai/Faux d'interprétation
- Corrections : attributs non atomiques, redondances, identifiants, cardinalités
- Traduction du MEA en modèle relationnel
- **Parfois bonus :** requêtes SQL simples

#### 3) Questions de cours (3–4 points)
- Définitions : SI, donnée vs information
- Hiérarchie d'abstraction (MCD/MLD/MPD)
- Acronymes SGBDR/CRUD/UML
- Vocabulaire (relation/lien/propriété/instance/spécialisation)
- Différence Merise/UML
- Exemples de diagrammes UML

---

### 8.2. Plan de travail conseillé (4 jours/semaines)

#### **Jour/Semaine 1 – MEA (conception)**

Refaire au moins **deux gros énoncés** de modélisation :
- Courses de drones
- Vols d'avion
- Salles de Centrale Lille
- NextCloud (plateforme de partage de fichiers)

Pour chacun :
- Listes des entités et attributs
- Identifiants
- Associations + multiplicités
- Explications des choix de conception

#### **Jour/Semaine 2 – Traduction et critique**

- Prendre un MEA que tu as construit :
  - Le traduire en **modèle relationnel** (avec PK/FK et tables d'association)
  - Vérifier la cohérence des cardinalités
- Refaires les exercices de compréhension de modèles :
  - Vrai/Faux
  - Détection d'attributs non atomiques
  - Redondances
  - Modifications minimales

#### **Jour/Semaine 3 – UML et vocabulaire**

Apprendre par cœur :
- Définition de SI
- Hiérarchie d'abstraction (MCD → MLD → MPD)
- Différence donnée/information
- Acronymes SGBDR/CRUD/UML
- Vocabulaires relation/lien/propriété/instance/spécialisation
- 3 types de diagrammes UML
- Différence **Merise vs UML**

#### **Jour/Semaine 4 – Entraînement complet sur sujets complets**

- Reprendre un sujet complet d'examen (2021–2025)
- Traiter tous les exercices dans l'ordre
- Chrono-tiser : 3-4 heures pour te rapprocher des conditions réelles

---

### 8.3. Conseils supplémentaires

**Avant le partiel :**
1. Bien dormir la veille
2. Apporter stylos + crayons (le modèle se fait à la main, sauf demande explicite)
3. Relire rapidement la fiche la veille

**Pendant le partiel :**
1. Lire **entièrement** les énoncés avant de commencer
2. Commencer par ce qui te semble le plus facile
3. Bien justifier tes choix de conception
4. Vérifier tes multiplicités en les lisant dans les deux sens

**Bon courage! 🎓**

---

## Ressources annexes

### Checklist avant le partiel

- [ ] Je sais définir un système d'information
- [ ] Je sais expliquer la hiérarchie d'abstraction (MCD/MLD/MPD)
- [ ] Je peux construire un MEA à partir d'un énoncé
- [ ] Je repère les attributs non atomiques
- [ ] Je détecte les redondances
- [ ] Je sais traduire un MEA en modèle relationnel
- [ ] Je connais les multiplicités et cardinalités
- [ ] Je sais lire une association réflexive
- [ ] Je peux interpréter un modèle (Vrai/Faux)
- [ ] Je connais au moins 3 types de diagrammes UML
- [ ] Je peux donner une différence Merise/UML
- [ ] Je connais les acronymes SGBDR/CRUD/UML

### Sujets d'entraînement

- **2024–2025 :** Plateforme de partage de fichiers (NextCloud)
- **2023–2024 :** Compétition (diagramme à analyser + modif)
- **2022–2023 :** Courses de drones
- **2021–2022 :** Gestion des salles + Rétro-Vidéo + Cluster de calcul
- **Réparation 2022 :** Réservation de vols + Enseignants/Élèves
