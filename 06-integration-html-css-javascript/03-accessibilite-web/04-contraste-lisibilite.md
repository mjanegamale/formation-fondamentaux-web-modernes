🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.3.4 - Contraste et lisibilité

## Pourquoi le contraste et la lisibilité sont-ils cruciaux ?

Le **contraste** et la **lisibilité** sont des aspects fondamentaux de l'accessibilité web qui affectent **tous les utilisateurs**, pas seulement les personnes en situation de handicap.

### Qui est concerné ? 👥

- **Personnes malvoyantes** ou avec une vision réduite
- **Personnes daltoniennes** (environ 8% des hommes, 0,5% des femmes)
- **Personnes âgées** avec une baisse naturelle de la vision
- **Tout le monde** dans certaines situations :
  - Écran en plein soleil ☀️
  - Écran avec reflets
  - Fatigue oculaire après une longue journée
  - Utilisation sur un vieil écran ou smartphone

### Le principe fondamental

> **Votre contenu doit être lisible par tous, dans toutes les conditions.**

Un bon contraste et une bonne lisibilité ne sont pas des "bonus" — ce sont des **exigences légales** dans de nombreux pays et des **fondamentaux** du design web.

---

## Qu'est-ce que le contraste ?

Le **contraste** est la différence de luminosité entre deux couleurs, typiquement entre :
- Le texte (premier plan)
- Le fond (arrière-plan)

### Contraste faible vs contraste élevé

```
❌ Contraste faible (difficile à lire) :
   Texte gris clair #CCCCCC sur fond blanc #FFFFFF

✅ Contraste élevé (facile à lire) :
   Texte noir #000000 sur fond blanc #FFFFFF
```

**Plus le contraste est élevé, plus le texte est facile à lire.**

---

## Les normes WCAG : ratios de contraste

Les **WCAG (Web Content Accessibility Guidelines)** définissent des ratios de contraste minimums à respecter.

### Comprendre le ratio de contraste

Le ratio de contraste se mesure de **1:1** (aucun contraste) à **21:1** (contraste maximum, noir sur blanc).

```
Exemples de ratios :
- 1:1   = Blanc sur blanc (invisible)
- 3:1   = Seuil minimum pour certains éléments
- 4.5:1 = Seuil minimum pour le texte normal
- 7:1   = Seuil minimum pour le texte petit (AAA)
- 21:1  = Noir sur blanc (contraste maximum)
```

---

### Les seuils WCAG à respecter

#### **Niveau AA** (Minimum requis) 📋

C'est le niveau de conformité **standard** que vous devez viser.

| Type de contenu | Ratio minimum requis |
|-----------------|---------------------|
| **Texte normal** (18px+) | **4.5:1** |
| **Texte large** (24px+ ou 18.5px+ gras) | **3:1** |
| **Éléments d'interface** (boutons, icônes) | **3:1** |
| **Éléments graphiques** (graphiques, diagrammes) | **3:1** |

---

#### **Niveau AAA** (Amélioré) 🏆

C'est le niveau de conformité **renforcé** (recommandé pour les sites publics, santé, etc.).

| Type de contenu | Ratio minimum requis |
|-----------------|---------------------|
| **Texte normal** | **7:1** |
| **Texte large** | **4.5:1** |

---

### Exemples concrets de contraste

#### ❌ Mauvais contraste (ne respecte pas AA)

```css
/* Ratio : 2.3:1 - ÉCHEC */
.mauvais-contraste {
  color: #999999;         /* Gris moyen */
  background-color: #FFFFFF; /* Blanc */
}
```

**Problème** : Difficile à lire pour beaucoup de personnes.

---

#### ⚠️ Contraste limite (respecte AA pour texte large uniquement)

```css
/* Ratio : 3.2:1 - OK pour texte large seulement */
.contraste-limite {
  color: #767676;         /* Gris */
  background-color: #FFFFFF; /* Blanc */
  font-size: 24px;        /* Texte large */
}
```

**Note** : Acceptable pour les titres, mais pas pour le texte courant.

---

#### ✅ Bon contraste (respecte AA)

```css
/* Ratio : 4.6:1 - SUCCÈS AA */
.bon-contraste {
  color: #595959;         /* Gris foncé */
  background-color: #FFFFFF; /* Blanc */
}
```

**Résultat** : Lisible par la majorité des utilisateurs.

---

#### ✅ Excellent contraste (respecte AAA)

```css
/* Ratio : 7.3:1 - SUCCÈS AAA */
.excellent-contraste {
  color: #404040;         /* Gris très foncé */
  background-color: #FFFFFF; /* Blanc */
}

/* Ou le classique noir sur blanc */
.maximum-contraste {
  color: #000000;         /* Noir */
  background-color: #FFFFFF; /* Blanc */
  /* Ratio : 21:1 - Maximum */
}
```

**Résultat** : Excellent pour tous les utilisateurs.

---

## Outils pour vérifier le contraste

### 1. **Contrast Checker en ligne** 🔍

#### WebAIM Contrast Checker
- URL : https://webaim.org/resources/contrastchecker/
- **Comment l'utiliser** :
  1. Entrez la couleur du texte (foreground)
  2. Entrez la couleur du fond (background)
  3. L'outil calcule le ratio et indique si ça passe AA/AAA

**Exemple d'utilisation :**
```
Foreground: #595959
Background: #FFFFFF
→ Ratio: 4.6:1
→ AA Normal Text: ✅ Pass
→ AAA Normal Text: ❌ Fail
→ AA Large Text: ✅ Pass
```

---

#### Coolors Contrast Checker
- URL : https://coolors.co/contrast-checker
- Interface visuelle et intuitive
- Suggestions de couleurs alternatives

---

### 2. **Extensions de navigateur** 🔧

#### WAVE (Web Accessibility Evaluation Tool)
- Disponible pour Chrome et Firefox
- Analyse votre page et identifie les problèmes de contraste
- Gratuit

**Comment l'utiliser :**
1. Installez l'extension WAVE
2. Ouvrez votre site web
3. Cliquez sur l'icône WAVE
4. Les erreurs de contraste sont signalées en rouge

---

#### axe DevTools
- Extension officielle de Deque
- Audit complet d'accessibilité
- Identifie les problèmes de contraste

---

### 3. **DevTools du navigateur** 🛠️

Les navigateurs modernes ont des outils intégrés pour vérifier le contraste.

#### Chrome DevTools

```
1. Clic droit sur un élément → Inspecter
2. Dans l'onglet "Styles", cliquez sur un carré de couleur
3. Le sélecteur de couleur s'ouvre
4. En bas : ratio de contraste avec un indicateur ✅ ou ❌
5. Chrome suggère même des couleurs conformes !
```

**Fonctionnalités utiles :**
- Ligne de contraste AA (montre les couleurs qui passent)
- Ligne de contraste AAA
- Calcul automatique du ratio

---

#### Firefox DevTools

```
1. Outils → Inspecteur
2. Sélectionnez un élément avec du texte
3. Onglet "Accessibilité"
4. Section "Contraste" : ratio calculé automatiquement
```

---

### 4. **Plugins Figma/Adobe XD** 🎨

Pour les designers qui créent des maquettes :

- **Stark** : Plugin pour vérifier le contraste dans Figma
- **Contrast** : Plugin Adobe XD
- **A11y - Color Contrast Checker** : Plugin Figma gratuit

**Vérifiez le contraste dès la phase de design, pas après le développement !**

---

## Au-delà du contraste : la lisibilité

Le contraste seul ne suffit pas. La **lisibilité** dépend de plusieurs facteurs.

### 1. **Taille de police** 📏

#### Tailles minimales recommandées

```css
/* ❌ Trop petit : difficile à lire */
body {
  font-size: 12px; /* À éviter */
}

/* ✅ Taille confortable */
body {
  font-size: 16px; /* Minimum recommandé */
}

/* ✅ Encore mieux */
body {
  font-size: 18px; /* Idéal pour le corps de texte */
}
```

**Règle générale :**
- **Minimum 16px** pour le texte courant
- **18-20px** recommandé pour une meilleure lisibilité
- **24px+** pour les titres secondaires

---

#### Unités relatives pour l'accessibilité

```css
/* ✅ Utilisez rem pour respecter les préférences utilisateur */
body {
  font-size: 1rem;      /* = 16px par défaut, mais adaptable */
}

h1 {
  font-size: 2.5rem;    /* = 40px par défaut */
}

p {
  font-size: 1.125rem;  /* = 18px par défaut */
}
```

**Pourquoi `rem` ?**
- Les utilisateurs peuvent agrandir la police dans les paramètres du navigateur
- Votre site s'adapte automatiquement
- Meilleur pour l'accessibilité que `px` fixes

---

### 2. **Choix de la police** ✍️

#### Polices lisibles vs polices décoratives

```css
/* ✅ Polices sans-serif : excellentes pour le web */
body {
  font-family: Arial, Helvetica, sans-serif;
}

/* ✅ Polices serif : bonnes pour le texte long */
body {
  font-family: Georgia, 'Times New Roman', serif;
}

/* ⚠️ Polices décoratives : uniquement pour les titres */
h1 {
  font-family: 'Fancy Font', cursive;
}

/* ❌ Polices trop stylisées : à éviter pour le texte courant */
p {
  font-family: 'Ultra Decorative', fantasy; /* NON ! */
}
```

**Bonnes pratiques :**
- Privilégiez les polices **simples et claires**
- Évitez les polices trop fines (font-weight < 400)
- N'utilisez pas trop de polices différentes (2-3 maximum)

---

### 3. **Interligne (line-height)** 📐

Un bon espacement entre les lignes améliore considérablement la lisibilité.

```css
/* ❌ Trop serré : difficile à lire */
p {
  line-height: 1.0; /* Les lignes se touchent */
}

/* ⚠️ Par défaut du navigateur : acceptable mais pas optimal */
p {
  line-height: normal; /* ≈ 1.2 */
}

/* ✅ Recommandé : 1.5 minimum */
p {
  line-height: 1.5; /* WCAG recommande 1.5 minimum */
}

/* ✅ Idéal : 1.6-1.8 pour le texte long */
article p {
  line-height: 1.7;
}
```

**Règle WCAG** : L'interligne doit être au moins **1.5 fois** la taille de la police.

---

### 4. **Longueur de ligne** 📏

Des lignes trop longues ou trop courtes fatiguent les yeux.

```css
/* ❌ Trop large : fatiguant */
.article {
  max-width: 100%; /* Lignes de 150+ caractères */
}

/* ✅ Largeur optimale : 60-80 caractères par ligne */
.article {
  max-width: 65ch; /* ch = largeur d'un caractère */
}

/* Ou en pixels/rem */
.article {
  max-width: 700px;
}
```

**Recommandation** :
- **60-80 caractères** par ligne pour le texte courant
- **45-75 caractères** pour un confort optimal

---

### 5. **Espacement des paragraphes** 📄

```css
/* ✅ Espacement entre paragraphes */
p {
  margin-bottom: 1.5em; /* Espace visuel entre les paragraphes */
}

/* ✅ Espacement des lettres (letter-spacing) */
p {
  letter-spacing: 0.02em; /* Légèrement espacé pour améliorer la lisibilité */
}

/* ✅ Espacement des mots (word-spacing) */
p {
  word-spacing: 0.05em;
}
```

**Règle WCAG** : L'espacement entre paragraphes doit être au moins **2 fois** la taille de la police.

---

### 6. **Alignement du texte** 📐

```css
/* ✅ Texte aligné à gauche : le plus lisible */
p {
  text-align: left;
}

/* ⚠️ Texte justifié : peut créer des espacements irréguliers */
p {
  text-align: justify; /* À éviter ou utiliser avec hyphens */
  hyphens: auto; /* Césure automatique pour compenser */
}

/* ⚠️ Centré : uniquement pour titres ou texte court */
h1 {
  text-align: center;
}

/* ❌ Aligné à droite : difficile à lire (sauf langues RTL) */
p {
  text-align: right; /* À éviter pour le texte long */
}
```

---

## Cas particuliers de contraste

### 1. **Texte sur image** 🖼️

Le texte sur image est **difficile à rendre accessible** car le contraste varie selon l'image.

#### ❌ Mauvaise approche

```html
<div style="background-image: url('photo.jpg');">
  <h1>Titre sur l'image</h1>
</div>
```

**Problème** : Si l'image est claire, le texte blanc est invisible. Si l'image est sombre, le texte noir est invisible.

---

#### ✅ Solutions recommandées

**Solution 1 : Overlay (calque semi-transparent)**

```css
.hero {
  position: relative;
  background-image: url('photo.jpg');
  background-size: cover;
}

/* Calque sombre semi-transparent */
.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6); /* Noir à 60% d'opacité */
  z-index: 1;
}

.hero h1 {
  position: relative;
  z-index: 2;
  color: white;
}
```

---

**Solution 2 : Ombre portée (text-shadow)**

```css
.hero h1 {
  color: white;
  text-shadow:
    2px 2px 4px rgba(0, 0, 0, 0.8),
    -1px -1px 2px rgba(0, 0, 0, 0.8);
}
```

---

**Solution 3 : Fond derrière le texte**

```css
.hero h1 {
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 1rem;
  display: inline-block;
}
```

---

### 2. **Texte désactivé (disabled)** 🔒

Les éléments désactivés doivent rester lisibles, même s'ils ne sont pas interactifs.

```css
/* ❌ Mauvais : contraste trop faible */
button:disabled {
  color: #CCCCCC;
  background: #F5F5F5;
  /* Ratio ≈ 1.4:1 - ÉCHEC */
}

/* ✅ Bon : contraste suffisant */
button:disabled {
  color: #757575; /* Plus foncé */
  background: #F0F0F0;
  opacity: 0.7; /* Indication visuelle de l'état */
  cursor: not-allowed;
  /* Ratio ≈ 4.6:1 - SUCCÈS AA */
}
```

---

### 3. **Liens dans le texte** 🔗

Les liens doivent être **facilement identifiables**, pas seulement par la couleur.

#### ❌ Mauvaise approche (couleur uniquement)

```css
/* Problème : les personnes daltoniennes peuvent ne pas voir la différence */
a {
  color: #0066CC; /* Bleu */
  text-decoration: none;
}
```

---

#### ✅ Bonne approche (couleur + autre indicateur)

```css
/* ✅ Soulignement par défaut */
a {
  color: #0066CC;
  text-decoration: underline;
}

/* ✅ Ou soulignement au survol */
a {
  color: #0066CC;
  text-decoration: none;
  border-bottom: 2px solid #0066CC;
}

a:hover,
a:focus {
  text-decoration: underline;
  background-color: #E6F2FF;
}
```

**Règle WCAG** : La couleur seule ne doit **jamais** être le seul moyen de distinguer un lien.

---

### 4. **Placeholders de formulaire** 📝

Les placeholders sont souvent trop clairs et ne respectent pas les normes de contraste.

```css
/* ❌ Placeholder par défaut : souvent trop clair */
input::placeholder {
  color: #999999; /* Ratio ≈ 2.8:1 - ÉCHEC */
}

/* ✅ Placeholder avec bon contraste */
input::placeholder {
  color: #757575; /* Ratio ≈ 4.6:1 - SUCCÈS AA */
}
```

**Attention** : Ne comptez pas uniquement sur les placeholders pour les instructions. Utilisez des `<label>` visibles !

---

## Le daltonisme et l'utilisation de la couleur

Environ **8% des hommes** et **0.5% des femmes** sont daltoniens. Votre site doit être utilisable sans dépendre uniquement de la couleur.

### Types de daltonisme courants

1. **Deutéranopie** : difficulté à distinguer rouge et vert (le plus courant)
2. **Protanopie** : difficulté avec le rouge
3. **Tritanopie** : difficulté avec le bleu et le jaune
4. **Achromatopsie** : vision en noir et blanc (rare)

---

### ❌ Ne pas faire : information uniquement par la couleur

```html
<!-- ❌ Mauvais : seule la couleur indique l'erreur -->
<p style="color: red;">Champ obligatoire</p>

<!-- ❌ Mauvais : seule la couleur différencie les états -->
<button style="background: green;">Actif</button>
<button style="background: red;">Inactif</button>
```

---

### ✅ À faire : couleur + autre indicateur

```html
<!-- ✅ Bon : couleur + icône + texte -->
<p style="color: #C00;">
  <span aria-hidden="true">⚠️</span>
  <strong>Erreur :</strong> Champ obligatoire
</p>

<!-- ✅ Bon : couleur + texte clair -->
<button style="background: green;">
  ✓ Actif
</button>
<button style="background: red;">
  ✕ Inactif
</button>

<!-- ✅ Bon : utiliser des motifs différents dans les graphiques -->
<canvas>
  <!-- Graphique avec couleurs ET motifs/textures -->
</canvas>
```

**Règle WCAG 1.4.1** : La couleur ne doit **jamais** être le seul moyen de transmettre une information.

---

## Mode sombre (Dark mode) et contraste 🌙

Le mode sombre est populaire, mais il faut aussi respecter le contraste.

### Contraste en mode sombre

```css
/* ✅ Mode clair */
body {
  background: #FFFFFF;
  color: #1A1A1A;
  /* Ratio : 18:1 - Excellent */
}

/* ✅ Mode sombre - contraste inversé */
@media (prefers-color-scheme: dark) {
  body {
    background: #1A1A1A;
    color: #E0E0E0;
    /* Ratio : ≈ 13:1 - Excellent */
  }

  /* ⚠️ Attention : ne pas utiliser blanc pur sur noir pur */
  /* Trop de contraste peut fatiguer les yeux en mode sombre */

  /* ✅ Préférez légèrement grisé */
  body {
    background: #121212; /* Pas complètement noir */
    color: #E0E0E0;      /* Pas complètement blanc */
  }
}
```

**Astuce** : En mode sombre, un contraste légèrement réduit (13:1 vs 21:1) est souvent plus confortable.

---

## Checklist : Contraste et lisibilité ✅

### Contraste des couleurs

- [ ] Texte normal : ratio ≥ 4.5:1 (AA) ou ≥ 7:1 (AAA)
- [ ] Texte large : ratio ≥ 3:1 (AA) ou ≥ 4.5:1 (AAA)
- [ ] Éléments d'interface : ratio ≥ 3:1
- [ ] Texte sur image : toujours lisible (overlay ou ombre)
- [ ] Liens identifiables sans couleur seule
- [ ] Placeholders de formulaire : ratio ≥ 4.5:1
- [ ] Mode sombre : contraste adapté

---

### Typographie et lisibilité

- [ ] Taille de police ≥ 16px pour le texte courant
- [ ] Interligne (line-height) ≥ 1.5
- [ ] Longueur de ligne : 60-80 caractères
- [ ] Police lisible (éviter les polices trop décoratives)
- [ ] Espacement entre paragraphes ≥ 2x la taille de police
- [ ] Texte aligné à gauche (pas justifié sans césure)
- [ ] Unités relatives (rem) pour respecter les préférences utilisateur

---

### Information et couleur

- [ ] Aucune information transmise uniquement par la couleur
- [ ] Liens différenciés par autre chose que la couleur
- [ ] Messages d'erreur avec icônes ou texte explicite
- [ ] Graphiques avec motifs en plus des couleurs
- [ ] États des boutons clarifiés par texte/icône

---

## Tester votre site pour le contraste et la lisibilité

### Test manuel en 5 minutes 🧪

1. **Test de contraste basique**
   - Passez votre site en noir et blanc (extension de navigateur)
   - Tout est-il encore lisible ?
   - Les informations importantes sont-elles visibles ?

2. **Test de zoom**
   - Zoomez à 200% (Ctrl/Cmd + +)
   - Le texte reste-t-il lisible ?
   - La mise en page reste-t-elle utilisable ?

3. **Test de simulation de daltonisme**
   - Utilisez une extension comme "Colorblind Web Page Filter"
   - Simulez différents types de daltonisme
   - L'information est-elle toujours accessible ?

4. **Test de lecture**
   - Lisez un paragraphe de votre site
   - Est-ce confortable ?
   - Vos yeux fatiguent-ils ?

---

### Outils automatiques 🤖

1. **Lighthouse** (intégré à Chrome DevTools)
   - Audit automatique du contraste
   - Suggestions d'amélioration

2. **WAVE**
   - Identifie tous les problèmes de contraste
   - Affiche visuellement les erreurs

3. **axe DevTools**
   - Analyse complète de l'accessibilité
   - Rapports détaillés

4. **Contrast Checker** (WebAIM)
   - Vérification manuelle couleur par couleur
   - Suggestions de couleurs alternatives

---

## Palettes de couleurs accessibles

### Outils pour créer des palettes accessibles 🎨

1. **Accessible Colors** (usecontrast.com)
   - Génère des couleurs avec bon contraste
   - Ajuste automatiquement vos couleurs

2. **Colorable** (colorable.jxnblk.com)
   - Teste des combinaisons de couleurs
   - Affiche les ratios de contraste

3. **Adobe Color** (color.adobe.com)
   - Mode "accessible" intégré
   - Vérifie le contraste de vos palettes

4. **Coolors** (coolors.co)
   - Générateur de palettes
   - Vérification de contraste intégrée

---

### Exemple de palette accessible

```css
/* ✅ Palette accessible pour un site web */
:root {
  /* Couleurs principales */
  --primary: #0066CC;      /* Bleu */
  --primary-dark: #004C99; /* Bleu foncé */
  --secondary: #00AA66;    /* Vert */

  /* Couleurs de texte */
  --text-dark: #1A1A1A;    /* Presque noir */
  --text-medium: #595959;  /* Gris foncé */
  --text-light: #767676;   /* Gris moyen (texte large uniquement) */

  /* Couleurs de fond */
  --bg-white: #FFFFFF;
  --bg-light: #F5F5F5;
  --bg-medium: #E0E0E0;

  /* États */
  --success: #2D8659;      /* Vert foncé */
  --warning: #CC6600;      /* Orange foncé */
  --error: #C00000;        /* Rouge foncé */
  --info: #0066CC;         /* Bleu */
}

/* Tous ces contrastes respectent AA (4.5:1 minimum) */
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Gris trop clair

```css
/* ❌ Gris #999 sur blanc : ratio 2.8:1 - ÉCHEC */
p {
  color: #999999;
}
```

**Solution** : Utilisez au moins #595959 (ratio 7:1).

---

### ❌ Erreur 2 : Texte blanc sur fond coloré clair

```css
/* ❌ Blanc sur bleu clair : ratio 2.4:1 - ÉCHEC */
.button {
  background: #66B2FF;
  color: #FFFFFF;
}
```

**Solution** : Assombrissez le fond (#0066CC) ou foncez le texte.

---

### ❌ Erreur 3 : Liens non distinguables

```css
/* ❌ Lien bleu sur noir sans autre indicateur */
a {
  color: #0066FF;
  text-decoration: none;
}
```

**Solution** : Ajoutez un soulignement ou un autre indicateur visuel.

---

### ❌ Erreur 4 : Police trop petite

```css
/* ❌ Police à 12px : trop petite */
body {
  font-size: 12px;
}
```

**Solution** : Minimum 16px (1rem).

---

### ❌ Erreur 5 : Interligne insuffisant

```css
/* ❌ Line-height 1.2 : trop serré */
p {
  line-height: 1.2;
}
```

**Solution** : Minimum 1.5, idéalement 1.6-1.8.

---

## Résumé des bonnes pratiques

### ✅ Contraste

1. Respectez les ratios WCAG (4.5:1 minimum pour texte normal)
2. Testez avec des outils automatiques ET manuellement
3. Attention au texte sur image (utilisez des overlays)
4. N'utilisez jamais la couleur seule pour transmettre une information
5. Vérifiez le contraste en mode sombre aussi

### ✅ Typographie

1. Taille minimum 16px (1rem) pour le texte courant
2. Interligne minimum 1.5 (idéal : 1.6-1.8)
3. Longueur de ligne : 60-80 caractères
4. Polices simples et lisibles
5. Unités relatives (rem, em) pour l'adaptabilité

### ✅ Accessibilité visuelle

1. Identifiez les liens par plus que la couleur
2. Fournissez des indicateurs visuels multiples (icônes, texte)
3. Testez avec simulation de daltonisme
4. Permettez le zoom à 200% sans perte de fonctionnalité
5. Utilisez des palettes de couleurs accessibles

---

## Conclusion

Le contraste et la lisibilité sont des **fondamentaux non négociables** de l'accessibilité web. Un bon contraste et une bonne typographie :

- ✅ Rendent votre contenu **accessible à tous**
- ✅ Améliorent l'**expérience utilisateur** pour tout le monde
- ✅ Respectent les **normes et la loi**
- ✅ Donnent une image **professionnelle**
- ✅ Réduisent la **fatigue visuelle**

**La bonne nouvelle** : créer un site avec un bon contraste et une bonne lisibilité est simple si vous suivez les bonnes pratiques dès le début !

**Avec ces 4 sections sur l'accessibilité (importance, ARIA, navigation clavier, contraste), vous avez maintenant les fondamentaux pour créer des sites web accessibles à tous. 🌍**

---

## Ressources complémentaires

- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [WCAG 2.1 - Contrast Guidelines](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [MDN - Accessible colors](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Understanding_WCAG/Perceivable/Color_contrast)
- [A11y Color Contrast Checker](https://color.a11y.com/)
- [Colorblind Web Page Filter](https://www.toptal.com/designers/colorfilter)

⏭️ [Performance et optimisation](/06-integration-html-css-javascript/04-performance-optimisation/README.md)
