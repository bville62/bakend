# 📋 FICHE DE RÉVISION : TRANSFORMATION DE LAPLACE

---

## 1️⃣ DÉFINITION ET NOTATION

**Transformée de Laplace :**
$$F(p) = L(f) = \int_0^{+\infty} e^{-pt}f(t)dt$$

**Condition d'existence :**
- \(f(t)\) continue par morceaux
- \(f(t)\) à croissance exponentielle : \(|f(t)| \le Me^{\alpha t}\)
- Transformée existe si \(\text{Re}(p) > \alpha\)

**Notation :** \(L(f) = F(p)\) ou \(f(t) \xrightarrow{L} F(p)\)

---

## 2️⃣ TABLE DES TRANSFORMÉES USUELLES

| Fonction \(f(t)\) | Transformée \(F(p)\) |
|---|---|
| \(\gamma(t)\) (échelon unité) | \(\frac{1}{p}\) |
| \(\delta(t)\) (impulsion Dirac) | \(1\) |
| \(t^n\gamma(t)\) (\(n \in \mathbb{N}\)) | \(\frac{n!}{p^{n+1}}\) |
| \(e^{at}\gamma(t)\) | \(\frac{1}{p-a}\) |
| \(\cos(\omega t)\gamma(t)\) | \(\frac{p}{p^2+\omega^2}\) |
| \(\sin(\omega t)\gamma(t)\) | \(\frac{\omega}{p^2+\omega^2}\) |

---

## 3️⃣ PROPRIÉTÉS FONDAMENTALES

### ✅ Linéarité
$$L(\alpha f + \beta g) = \alpha L(f) + \beta L(g)$$

### ✅ Dérivation Temporelle (CRUCIAL)
$$L(f') = pL(f) - f(0^+)$$
$$L(f'') = p^2L(f) - pf(0^+) - f'(0^+)$$

**Cas particulier :** Si conditions initiales nulles → \(L(f^{(n)}) = p^nL(f)\)

### ✅ Théorème du Retard (Shifting)
$$L(f(t-a)\gamma(t-a)) = e^{-ap}F(p)$$

**Utilité :** Gérer les signaux décalés ou les créneaux retardés

### ✅ Translation de Pôle (Damping)
$$L(e^{-at}f(t)) = F(p+a)$$

**Utilité :** Ajouter une exponentielle décroissante \(e^{-at}\)

### ✅ Intégration
$$L\left(\int_0^t f(x)dx\right) = \frac{L(f)}{p}$$

### ✅ Produit de Convolution
$$L(f*g) = L(f) \cdot L(g)$$
où \((f*g)(t) = \int_0^t f(\tau)g(t-\tau)d\tau\)

### ✅ Signaux Périodiques
Pour signal de période \(T\) avec motif \(x_0(t)\) :
$$X(p) = \frac{X_0(p)}{1-e^{-pT}}$$

### ✅ Théorèmes des Valeurs Initiale et Finale
$$\lim_{p \to +\infty} pL(f) = f(0^+)$$
$$\lim_{p \to 0} pL(f) = f(+\infty)$$

---

## 4️⃣ TRANSFORMÉE INVERSE - MÉTHODE GÉNÉRALE

### 🎯 Stratégie pour fraction rationnelle \(F(p) = \frac{N(p)}{D(p)}\)

**Étape 1 :** Décomposer en éléments simples
$$F(p) = \sum \frac{A_i}{(p-p_i)^{k_i}}$$

**Étape 2 :** Utiliser les termes de base :
- \(L^{-1}\left(\frac{1}{p-a}\right) = e^{at}\gamma(t)\)
- \(L^{-1}\left(\frac{1}{(p-a)^n}\right) = \frac{t^{n-1}}{(n-1)!}e^{at}\gamma(t)\)

**Étape 3 :** Appliquer linéarité

---

## 5️⃣ CAS PARTICULIERS IMPORTANTS

### 📌 Trinôme Irréductible
**Identifier :** \(p^2 + bp + c\) avec \(\Delta < 0\)

**Compléter le carré :**
$$p^2 + bp + c = \left(p + \frac{b}{2}\right)^2 + \omega^2$$

**Puis utiliser translation de pôle :** \(q = p + \frac{b}{2}\)
$$L^{-1}\left(\frac{1}{(p+a)^2+\omega^2}\right) = \frac{1}{\omega}e^{-at}\sin(\omega t)\gamma(t)$$

### 📌 Racines Multiples
Pour \(\frac{1}{(p-a)^n}\), utiliser :
$$L^{-1}\left(\frac{1}{(p-a)^n}\right) = \frac{t^{n-1}}{(n-1)!}e^{at}\gamma(t)$$

### 📌 Exponentielle Amortie
Pour \(e^{-at}g(t)\), remplacer \(p\) par \(p+a\) dans \(G(p)\)

### 📌 Signal Créneau
$$\text{Créneau}(0,T) : f(t) = \gamma(t) - \gamma(t-T) \quad \Rightarrow \quad F(p) = \frac{1-e^{-pT}}{p}$$

---

## 6️⃣ RÉSOLUTION D'ÉQUATION DIFFÉRENTIELLE

### 🔧 Méthode en 4 étapes

**Étape 1 :** Appliquer \(L\) aux deux membres
$$L(ay'' + by' + cy) = L(f(t))$$

**Étape 2 :** Utiliser formules de dérivation
$$a[p^2Y(p) - py(0) - y'(0)] + b[pY(p) - y(0)] + cY(p) = F(p)$$

**Étape 3 :** Isoler \(Y(p)\)
$$Y(p) = \frac{F(p) + \text{termes initiaux}}{ap^2 + bp + c}$$

**Étape 4 :** Décomposer et appliquer \(L^{-1}\)

---

## 7️⃣ ASTUCES ET PIÈGES COURANTS

### ⚠️ Pièges
1. **Oublier la fonction \(\gamma(t)\)** → \(\sin(t) \neq\) \(\sin(t)\gamma(t)\)
2. **Conditions initiales** → Ne pas appliquer \(L(f') = pL(f)\) si \(f(0) \neq 0\)
3. **Factoriser le dénominateur** → Impossible de décomposer si pas factorisé
4. **Racines multiples** → Attention à la décomposition avec puissances

### ✨ Astuces
- **Linéariser les expressions** : \(\sin^2(x) = \frac{1-\cos(2x)}{2}\)
- **Développer les polynômes** : \((t^2-1)^2 = t^4 - 2t^2 + 1\)
- **Utiliser identités remarquables** : \(1 - e^{-pT} = (1-e^{-pT/2})(1+e^{-pT/2})\)
- **Vérifier avec théorèmes V.I. et V.F.** quand possible

---

## 8️⃣ FORMULAIRE COMPLET DES PROPRIÉTÉS

| Propriété | Domaine temporel | Domaine Laplace |
|---|---|---|
| **Linéarité** | \(\alpha f + \beta g\) | \(\alpha F + \beta G\) |
| **Retard** | \(f(t-a)\gamma(t-a)\) | \(e^{-ap}F(p)\) |
| **Amortissement** | \(e^{-at}f(t)\) | \(F(p+a)\) |
| **Dérivée** | \(f'(t)\) | \(pF(p) - f(0^+)\) |
| **Intégrale** | \(\int_0^t f(x)dx\) | \(\frac{F(p)}{p}\) |
| **Convolution** | \((f*g)(t)\) | \(F(p) \cdot G(p)\) |
| **Périodique T** | Motif répété | \(\frac{F_0(p)}{1-e^{-pT}}\) |
| **Multiplication t** | \(tf(t)\) | \(-F'(p)\) |

---

## 9️⃣ EXERCICES-TYPE À MAÎTRISER

### Type 1 : Calcul direct
$$f(t) = (3t^2 - e^{-2t})\gamma(t)$$
→ Appliquer linéarité + table

### Type 2 : Amortissement
$$f(t) = e^{-3t}\cos(4t)\gamma(t)$$
→ Identifier base + translation pôle

### Type 3 : Signal par morceaux
$$f(t) = \begin{cases} 2 & 0 \le t < 3 \\ 0 & t \ge 3 \end{cases}$$
→ Échelons retardés + théorème du retard

### Type 4 : Équation différentielle
$$y'' + 3y' + 2y = e^{-t}, \quad y(0)=1, \quad y'(0)=0$$
→ Transformation complète + décomposition

### Type 5 : Signal périodique
Motif sur \([0,T]\) → Utiliser \(\frac{X_0(p)}{1-e^{-pT}}\)

### Type 6 : Transformée inverse
$$F(p) = \frac{5}{p(p+2)^2}$$
→ Décomposition + table

---

## 🔟 CHECKLIST AVANT L'INTERRO

- [ ] Je connais la table des 6 transformées usuelles
- [ ] Je maîtrise les 7 propriétés fondamentales
- [ ] Je sais décomposer en éléments simples (racines simples et multiples)
- [ ] Je comprends la translation de pôle pour les exponentielles amortis
- [ ] Je sais résoudre une ED en 4 étapes
- [ ] Je peux gérer les signaux périodiques
- [ ] Je maîtrise le théorème du retard
- [ ] Je sais compléter un carré pour trinômes irréductibles
- [ ] Je peux vérifier mes réponses avec V.I. et V.F.
- [ ] Je n'oublie jamais la fonction \(\gamma(t)\)

---

## 📝 DERNIERS CONSEILS

✅ **À faire :**
- Énonce TOUJOURS la propriété utilisée
- Factorise systématiquement les polynômes
- Complète les carrés pour les trinômes
- Vérifie tes décompositions en éléments simples
- Applique les théorèmes V.I./V.F. pour vérifier

❌ **À éviter :**
- Oublier les conditions initiales
- Négliger le \(\gamma(t)\)
- Mélanger \(e^{-at}\) et \(e^{at}\)
- Faire des erreurs de signe
- Sauter les étapes de simplification

---

**Bon courage ! 🎓 Tu as les clés, à toi de jouer ! 💪**
