🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.3.3 - Navigation au clavier

## Pourquoi la navigation au clavier est-elle essentielle ?

La navigation au clavier est l'un des **aspects les plus importants** de l'accessibilité web. De nombreux utilisateurs dépendent exclusivement du clavier pour naviguer sur le web :

### Qui utilise la navigation au clavier ? ⌨️

- **Personnes aveugles ou malvoyantes** utilisant des lecteurs d'écran
- **Personnes avec des limitations motrices** qui ne peuvent pas utiliser une souris
- **Personnes atteintes de tremblements** (maladie de Parkinson, etc.)
- **Utilisateurs avancés** qui préfèrent le clavier pour sa rapidité
- **Personnes avec une blessure temporaire** (bras cassé, entorse au poignet)

### Le principe fondamental

> **Tout ce qui peut être fait avec une souris DOIT pouvoir être fait avec un clavier.**

Si un utilisateur ne peut pas accéder à une fonctionnalité ou un contenu avec le clavier seul, votre site **n'est pas accessible**.

---

## Les touches de navigation essentielles

Voici les touches que les utilisateurs utilisent pour naviguer au clavier :

### 1. **Tab** ➡️

**La touche la plus importante** pour l'accessibilité.

- Navigue vers l'**élément interactif suivant**
- Les éléments interactifs incluent : liens, boutons, champs de formulaire, etc.
- Suit l'ordre du DOM (de haut en bas, de gauche à droite)

```html
<button>Bouton 1</button>  <!-- Focus en premier -->
<button>Bouton 2</button>  <!-- Tab : focus en deuxième -->
<button>Bouton 3</button>  <!-- Tab : focus en troisième -->
```

---

### 2. **Shift + Tab** ⬅️

- Navigue vers l'**élément interactif précédent**
- Permet de revenir en arrière dans la navigation

---

### 3. **Enter (Entrée)** ↩️

- **Active** un lien ou un bouton
- **Soumet** un formulaire (si le focus est sur un bouton de soumission)

```html
<a href="/page">Lien</a>  <!-- Enter : suit le lien -->
<button onclick="...">Cliquer</button>  <!-- Enter : exécute l'action -->
```

---

### 4. **Espace (Space)** ␣

- **Active** un bouton
- **Coche/décoche** une case à cocher
- **Fait défiler** la page vers le bas (quand aucun élément n'a le focus)

```html
<button>Bouton</button>  <!-- Espace : active le bouton -->
<input type="checkbox">  <!-- Espace : coche/décoche -->
```

---

### 5. **Flèches directionnelles** ↑ ↓ ← →

- Naviguent dans des **groupes d'éléments** :
  - Boutons radio
  - Menus
  - Onglets
  - Listes déroulantes (select)
- **Font défiler** la page (↑ ↓)

```html
<!-- Dans un groupe de boutons radio, utilisez les flèches -->
<input type="radio" name="choix" value="1"> Option 1
<input type="radio" name="choix" value="2"> Option 2
<input type="radio" name="choix" value="3"> Option 3
```

---

### 6. **Escape (Échap)** ⎋

- **Ferme** une fenêtre modale
- **Annule** une action en cours
- **Quitte** un menu déroulant

```javascript
// Exemple : fermer une modale avec Escape
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    fermerModale();
  }
});
```

---

### 7. **Home / End** 🏠 🔚

- **Home** : va au début (premier élément, haut de page)
- **End** : va à la fin (dernier élément, bas de page)

---

### Tableau récapitulatif

| Touche | Action principale |
|--------|------------------|
| **Tab** | Élément suivant |
| **Shift + Tab** | Élément précédent |
| **Enter** | Activer lien/bouton, soumettre |
| **Espace** | Activer bouton, cocher case |
| **Flèches** | Naviguer dans un groupe |
| **Escape** | Fermer, annuler |
| **Home / End** | Début / Fin |

---

## Les éléments interactifs natifs

Certains éléments HTML sont **automatiquement accessibles au clavier** :

### ✅ Éléments naturellement focusables

Ces éléments peuvent recevoir le focus avec Tab **sans configuration supplémentaire** :

```html
<!-- Liens -->
<a href="/page">Lien</a>

<!-- Boutons -->
<button>Bouton</button>

<!-- Champs de formulaire -->
<input type="text">
<textarea></textarea>
<select>
  <option>Option 1</option>
</select>

<!-- Autres -->
<details>
  <summary>Cliquez pour déplier</summary>
</details>
```

**Ces éléments sont prêts à l'emploi !** Utilisez-les autant que possible.

---

### ❌ Éléments NON focusables par défaut

Ces éléments **ne peuvent pas recevoir le focus** avec Tab :

```html
<div>Texte</div>
<span>Texte</span>
<p>Paragraphe</p>
<h1>Titre</h1>
<img src="...">
```

**Si vous devez rendre ces éléments interactifs, utilisez `tabindex`** (voir section suivante).

---

## L'attribut `tabindex`

`tabindex` contrôle si un élément peut recevoir le focus et dans quel ordre.

### `tabindex="-1"` : Focusable par JavaScript uniquement

L'élément **ne peut pas** recevoir le focus avec Tab, mais peut être focusé avec JavaScript.

```html
<div id="message" tabindex="-1">
  Message important
</div>
```

```javascript
// Mettre le focus sur l'élément
document.getElementById('message').focus();
```

**Cas d'usage** :
- Messages d'erreur
- Zones vers lesquelles vous voulez diriger l'attention
- Contenu qui apparaît dynamiquement

---

### `tabindex="0"` : Focusable dans l'ordre naturel

L'élément devient **focusable avec Tab**, dans l'ordre naturel du DOM.

```html
<div tabindex="0" role="button" onclick="fairQuelqueChose()">
  Cliquer ici
</div>
```

⚠️ **Important** : Si vous utilisez `tabindex="0"` sur une div pour en faire un bouton, vous devez également :
- Ajouter `role="button"`
- Gérer les événements clavier (Enter et Espace)

**Préférez toujours un vrai `<button>` !**

---

### `tabindex="1+"` : Ordre personnalisé (⚠️ À ÉVITER)

Un nombre positif définit un **ordre de tabulation personnalisé**.

```html
<!-- ❌ Mauvais : ordre personnalisé -->
<button tabindex="3">Troisième</button>
<button tabindex="1">Premier</button>
<button tabindex="2">Deuxième</button>
```

**Pourquoi l'éviter ?**
- Casse l'ordre naturel et logique
- Difficile à maintenir
- Crée une expérience déroutante
- Peut créer des pièges à clavier

**Solution** : Réorganisez votre HTML pour avoir l'ordre correct.

---

### Résumé des valeurs de tabindex

| Valeur | Comportement | Usage recommandé |
|--------|-------------|------------------|
| `tabindex="-1"` | Pas dans Tab, focusable par JS | ✅ Oui, pour focus programmatique |
| `tabindex="0"` | Dans Tab, ordre naturel | ✅ Oui, si pas d'élément natif |
| `tabindex="1+"` | Ordre personnalisé | ❌ Non, à éviter absolument |

---

## L'indicateur de focus (`:focus`)

Quand un élément a le focus au clavier, il **doit être visuellement identifiable**.

### Le focus par défaut du navigateur

Par défaut, les navigateurs ajoutent un **contour** (outline) autour de l'élément focusé :

```css
/* Style par défaut du navigateur */
button:focus {
  outline: 2px solid blue; /* Varie selon le navigateur */
}
```

### ❌ L'erreur à ne JAMAIS faire

```css
/* ❌ DANGER : Ne supprimez JAMAIS le outline sans alternative ! */
* {
  outline: none; /* NE FAITES PAS ÇA */
}

button:focus {
  outline: none; /* NE FAITES PAS ÇA */
}
```

**Conséquence** : Les utilisateurs au clavier ne peuvent plus savoir où ils sont sur la page. **C'est une catastrophe pour l'accessibilité.**

---

### ✅ Personnaliser le focus correctement

Si vous n'aimez pas le style par défaut, vous **devez fournir une alternative visible** :

```css
/* ✅ Bon : remplacer par un style personnalisé clair */
button:focus {
  outline: 3px solid #007bff;
  outline-offset: 2px;
}

/* Ou avec une bordure */
button:focus {
  outline: none; /* OK seulement si vous ajoutez une alternative */
  border: 3px solid #007bff;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.3);
}
```

---

### `:focus-visible` - La solution moderne 🆕

`:focus-visible` affiche le focus **uniquement pour la navigation au clavier**, pas pour les clics de souris.

```css
/* Style moderne recommandé */
button {
  outline: none; /* Retirer le outline par défaut */
}

/* Focus visible uniquement au clavier */
button:focus-visible {
  outline: 3px solid #007bff;
  outline-offset: 2px;
}

/* Pas de outline au clic de souris */
button:focus:not(:focus-visible) {
  outline: none;
}
```

**Avantage** : Les utilisateurs de souris ne voient pas le outline, mais les utilisateurs au clavier le voient toujours !

**Support** : Bien supporté dans les navigateurs modernes (Chrome 86+, Firefox 85+, Safari 15.4+).

---

### Bonnes pratiques pour le focus

#### ✅ À faire :

1. **Toujours avoir un indicateur de focus visible**
2. Utiliser un contraste suffisant (ratio 3:1 minimum)
3. Rendre le focus facilement identifiable (épaisseur, couleur)
4. Tester votre site en naviguant uniquement au clavier

#### ❌ À éviter :

1. Ne jamais supprimer le outline sans alternative
2. Ne pas utiliser des couleurs trop subtiles
3. Ne pas avoir le même style pour hover et focus (confusion)

---

## Rendre un élément personnalisé accessible au clavier

Si vous créez un composant personnalisé, vous devez gérer **manuellement** l'accessibilité au clavier.

### Exemple : Un bouton personnalisé (div)

```html
<div
  class="custom-button"
  tabindex="0"
  role="button"
  onclick="direBonjour()"
>
  Cliquer
</div>
```

⚠️ **Problème** : Ce "bouton" ne fonctionne qu'au clic de souris, pas au clavier !

---

### ✅ Solution : Gérer les événements clavier

```html
<div
  class="custom-button"
  tabindex="0"
  role="button"
  onclick="direBonjour()"
  onkeydown="gererClavier(event)"
>
  Cliquer
</div>
```

```javascript
function gererClavier(event) {
  // Enter ou Espace active le bouton
  if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault(); // Empêche le défilement avec Espace
    direBonjour();
  }
}

function direBonjour() {
  alert('Bonjour !');
}
```

**Maintenant, le bouton fonctionne avec Enter et Espace !**

---

### Exemple complet : Menu déroulant accessible

```html
<div class="menu">
  <button
    id="menu-button"
    aria-expanded="false"
    aria-controls="menu-list"
    onclick="toggleMenu()"
    onkeydown="gererClavierMenu(event)"
  >
    Menu ▼
  </button>

  <ul id="menu-list" hidden>
    <li><a href="/accueil">Accueil</a></li>
    <li><a href="/services">Services</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</div>
```

```javascript
function toggleMenu() {
  const button = document.getElementById('menu-button');
  const menu = document.getElementById('menu-list');
  const isExpanded = button.getAttribute('aria-expanded') === 'true';

  button.setAttribute('aria-expanded', !isExpanded);
  menu.hidden = isExpanded;

  // Si on ouvre, focus sur le premier élément
  if (!isExpanded) {
    menu.querySelector('a').focus();
  }
}

function gererClavierMenu(event) {
  const button = document.getElementById('menu-button');
  const isExpanded = button.getAttribute('aria-expanded') === 'true';

  if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault();
    toggleMenu();
  }

  // Escape ferme le menu
  if (event.key === 'Escape' && isExpanded) {
    toggleMenu();
    button.focus(); // Remettre le focus sur le bouton
  }

  // Flèche bas ouvre et focus le premier élément
  if (event.key === 'ArrowDown' && !isExpanded) {
    event.preventDefault();
    toggleMenu();
  }
}
```

---

## L'ordre de tabulation (Tab order)

L'ordre dans lequel les éléments reçoivent le focus est **crucial** pour une bonne expérience utilisateur.

### Ordre naturel = Ordre du DOM

Par défaut, l'ordre de tabulation suit **l'ordre des éléments dans le HTML** :

```html
<!-- L'ordre de Tab suit l'ordre du code -->
<button>Premier</button>      <!-- Tab 1 -->
<input type="text">           <!-- Tab 2 -->
<a href="...">Lien</a>        <!-- Tab 3 -->
<button>Dernier</button>      <!-- Tab 4 -->
```

---

### ⚠️ Problème : Ordre visuel vs ordre DOM

Avec CSS (Flexbox, Grid, position), vous pouvez **changer l'ordre visuel** sans changer l'ordre du DOM :

```html
<div style="display: flex; flex-direction: column-reverse;">
  <button>Visuellement en bas</button>   <!-- Mais Tab 1 -->
  <button>Visuellement en haut</button>  <!-- Mais Tab 2 -->
</div>
```

**Résultat** : L'ordre de tabulation ne correspond pas à l'ordre visuel → **Expérience déroutante !**

---

### ✅ Solution : Alignez l'ordre DOM et l'ordre visuel

**Principe** : L'ordre de tabulation doit correspondre à l'ordre visuel logique.

```html
<!-- Réorganisez votre HTML pour avoir le bon ordre -->
<button>Visuellement en haut</button>   <!-- Tab 1 -->
<button>Visuellement en bas</button>    <!-- Tab 2 -->
```

**Puis utilisez CSS pour l'arrangement visuel :**

```css
/* Si nécessaire, inversez visuellement */
.container {
  display: flex;
  flex-direction: column-reverse;
}
```

---

## Pièges à clavier (Keyboard Traps)

Un **piège à clavier** se produit quand un utilisateur ne peut **pas sortir** d'un élément avec le clavier.

### ❌ Exemple de piège

```html
<!-- Modale qui piège le focus -->
<div class="modale" tabindex="0">
  <h2>Titre de la modale</h2>
  <p>Contenu...</p>
  <!-- Pas de bouton "Fermer" accessible -->
  <!-- L'utilisateur est bloqué ! -->
</div>
```

---

### ✅ Solution : Gestion correcte du focus

Pour une modale accessible :

```html
<div
  class="modale"
  role="dialog"
  aria-modal="true"
  aria-labelledby="modale-titre"
>
  <h2 id="modale-titre">Titre</h2>
  <p>Contenu...</p>

  <button onclick="fermerModale()">Fermer</button>
</div>
```

```javascript
let elementAvantModale;

function ouvrirModale() {
  // Sauvegarder l'élément qui avait le focus
  elementAvantModale = document.activeElement;

  const modale = document.querySelector('.modale');
  modale.hidden = false;

  // Mettre le focus sur le premier élément focusable
  modale.querySelector('button').focus();

  // Piéger le focus dans la modale
  document.addEventListener('keydown', piegerFocusDansModale);
}

function fermerModale() {
  const modale = document.querySelector('.modale');
  modale.hidden = true;

  // Retirer le piège
  document.removeEventListener('keydown', piegerFocusDansModale);

  // Restaurer le focus
  if (elementAvantModale) {
    elementAvantModale.focus();
  }
}

function piegerFocusDansModale(e) {
  if (e.key === 'Tab') {
    const modale = document.querySelector('.modale');
    const focusables = modale.querySelectorAll(
      'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
    );

    const premier = focusables[0];
    const dernier = focusables[focusables.length - 1];

    // Tab sur le dernier élément : retour au premier
    if (e.shiftKey && document.activeElement === premier) {
      dernier.focus();
      e.preventDefault();
    } else if (!e.shiftKey && document.activeElement === dernier) {
      premier.focus();
      e.preventDefault();
    }
  }

  // Escape ferme la modale
  if (e.key === 'Escape') {
    fermerModale();
  }
}
```

**Ce code :**
- ✅ Piège le focus dans la modale (Tab boucle)
- ✅ Permet de fermer avec Escape
- ✅ Restaure le focus après fermeture

---

## Skip links (Liens d'évitement)

Les **skip links** permettent aux utilisateurs au clavier de **sauter le contenu répétitif** (navigation, bannière) pour aller directement au contenu principal.

### Exemple de skip link

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <title>Mon site</title>
  <style>
    /* Skip link caché par défaut */
    .skip-link {
      position: absolute;
      top: -40px;
      left: 0;
      background: #000;
      color: #fff;
      padding: 8px;
      text-decoration: none;
      z-index: 100;
    }

    /* Visible au focus */
    .skip-link:focus {
      top: 0;
    }
  </style>
</head>
<body>
  <!-- Skip link : premier élément de la page -->
  <a href="#main-content" class="skip-link">
    Aller au contenu principal
  </a>

  <header>
    <nav>
      <!-- Navigation longue... -->
      <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/services">Services</a></li>
        <!-- 20 autres liens... -->
      </ul>
    </nav>
  </header>

  <!-- Contenu principal -->
  <main id="main-content" tabindex="-1">
    <h1>Titre de la page</h1>
    <p>Contenu principal...</p>
  </main>
</body>
</html>
```

**Comment ça fonctionne ?**
1. Le skip link est le **premier élément** focusable de la page
2. Il est caché visuellement par défaut
3. Quand il reçoit le focus (première pression sur Tab), **il devient visible**
4. Cliquer dessus (Enter) **saute directement au contenu principal**

**Avantage** : Un utilisateur au clavier n'a pas à tabber à travers 50 liens de navigation à chaque page !

---

## Checklist : Votre site est-il navigable au clavier ?

### Test rapide (5 minutes) 🧪

1. **Débranchez votre souris** (ou ne l'utilisez pas)
2. Utilisez **uniquement Tab, Enter, Espace et les flèches**
3. Essayez de :
   - ✅ Naviguer dans tout le site
   - ✅ Ouvrir les menus
   - ✅ Remplir les formulaires
   - ✅ Soumettre les formulaires
   - ✅ Ouvrir et fermer les modales
   - ✅ Utiliser tous les boutons
   - ✅ Voir où vous êtes (indicateur de focus)

**Si vous ne pouvez pas faire l'une de ces actions, votre site a un problème d'accessibilité.**

---

### Checklist détaillée ✅

- [ ] Tous les éléments interactifs sont accessibles avec Tab
- [ ] L'ordre de tabulation est logique (correspond à l'ordre visuel)
- [ ] Le focus est toujours visible (outline ou alternative)
- [ ] Les boutons fonctionnent avec Enter et Espace
- [ ] Les menus peuvent être ouverts et fermés au clavier
- [ ] Les modales peuvent être fermées avec Escape
- [ ] Les modales piègent le focus correctement
- [ ] Un skip link permet de sauter la navigation
- [ ] Pas d'éléments piégés (keyboard traps)
- [ ] Les formulaires sont navigables et soumissibles
- [ ] Les messages d'erreur reçoivent le focus
- [ ] Aucun `tabindex` avec des valeurs positives
- [ ] Pas de `outline: none` sans alternative

---

## Outils pour tester la navigation au clavier

### Tester manuellement ⌨️

**Le meilleur test** : utilisez votre site avec le clavier uniquement !

```
1. Ouvrez votre site
2. Appuyez sur Tab
3. Naviguez dans toute la page
4. Essayez toutes les fonctionnalités
5. Notez les problèmes
```

---

### Extensions navigateur 🔧

1. **Tab Visualizer** (Chrome) : Montre l'ordre de tabulation
2. **WAVE** : Identifie les problèmes d'accessibilité
3. **axe DevTools** : Audit automatique

---

### DevTools du navigateur 🛠️

Dans Chrome/Firefox DevTools :
- Onglet **"Accessibility"**
- Voir l'arbre d'accessibilité
- Inspecter le focus

---

## Exemples de patterns accessibles

### Bouton avec icône

```html
<button aria-label="Fermer" onclick="fermer()">
  ✕
</button>
```

```css
button:focus-visible {
  outline: 3px solid #007bff;
  outline-offset: 2px;
}
```

---

### Lien avec indication visuelle et textuelle

```html
<a href="/download" download>
  📥 Télécharger
  <span class="sr-only">(PDF, 2 MB)</span>
</a>
```

```css
/* Texte visible uniquement pour les lecteurs d'écran */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

---

### Toggle switch accessible

```html
<label class="toggle">
  <input type="checkbox" role="switch" aria-checked="false">
  <span class="toggle-label">Mode sombre</span>
</label>
```

```css
.toggle input:focus-visible + .toggle-label::before {
  outline: 3px solid #007bff;
  outline-offset: 2px;
}
```

---

## Résumé des bonnes pratiques

### ✅ À faire :

1. **Tester régulièrement** avec le clavier uniquement
2. Utiliser des **éléments HTML natifs** (button, a, input...)
3. Fournir un **indicateur de focus visible** clair
4. Respecter l'**ordre logique** de tabulation
5. Gérer les **événements clavier** (Enter, Espace, Escape)
6. Ajouter des **skip links**
7. Gérer correctement les **modales** (piège de focus)
8. Documenter les **raccourcis clavier** personnalisés

### ❌ À éviter :

1. Supprimer le outline sans alternative
2. Utiliser `tabindex` avec des valeurs positives
3. Créer des pièges à clavier
4. Ignorer les événements clavier sur les éléments personnalisés
5. Avoir un ordre de tabulation illogique
6. Oublier de tester au clavier

---

## Conclusion

La navigation au clavier est **fondamentale** pour l'accessibilité web. Un site qui fonctionne bien au clavier est :

- ✅ **Accessible** à des millions de personnes
- ✅ **Plus facile à utiliser** pour tous
- ✅ **Mieux construit** techniquement
- ✅ **Conforme** aux standards et à la loi

**La bonne nouvelle** : rendre un site accessible au clavier n'est pas compliqué si vous suivez les bonnes pratiques dès le début !

**Prochain objectif** : Assurer un bon contraste et une bonne lisibilité pour tous vos utilisateurs.

---

## Ressources complémentaires

- [MDN - Keyboard-navigable JavaScript widgets](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Keyboard-navigable_JavaScript_widgets)
- [WebAIM - Keyboard Accessibility](https://webaim.org/techniques/keyboard/)
- [W3C - Keyboard](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html)
- [a11y-101 - Keyboard Navigation](https://a11y-101.com/design/keyboard-navigation)

⏭️ [Contraste et lisibilité](/06-integration-html-css-javascript/03-accessibilite-web/04-contraste-lisibilite.md)
