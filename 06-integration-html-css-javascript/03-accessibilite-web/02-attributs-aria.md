🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.3.2 - Attributs ARIA de base

## Qu'est-ce qu'ARIA ?

**ARIA** signifie **Accessible Rich Internet Applications** (Applications Internet Riches Accessibles). C'est une spécification technique du W3C qui permet d'**améliorer l'accessibilité** des applications web, particulièrement les interfaces dynamiques et interactives.

### Le problème qu'ARIA résout

HTML est conçu principalement pour des **documents statiques**. Mais les sites web modernes sont des **applications interactives** avec :
- Des menus déroulants
- Des onglets
- Des modales (popups)
- Des notifications
- Du contenu qui se charge dynamiquement

Les lecteurs d'écran et autres technologies d'assistance ont parfois du mal à comprendre ces éléments complexes. **ARIA fournit des informations supplémentaires** pour les aider.

---

## La règle d'or d'ARIA

> **"Le meilleur ARIA, c'est pas d'ARIA"**

Avant d'utiliser ARIA, demandez-vous toujours :

### ✅ Utilisez d'abord du HTML sémantique natif

```html
<!-- ❌ Mauvais : utiliser ARIA inutilement -->
<div role="button" tabindex="0" onclick="...">Cliquez ici</div>

<!-- ✅ Bon : utiliser l'élément HTML natif -->
<button onclick="...">Cliquez ici</button>
```

**Pourquoi ?**
- Les éléments HTML natifs ont déjà l'accessibilité intégrée
- Ils sont testés et fonctionnent correctement
- Ils sont plus simples et moins susceptibles d'erreurs

### Quand utiliser ARIA alors ?

Utilisez ARIA uniquement quand :
1. **Il n'existe pas d'élément HTML natif** pour ce que vous voulez faire
2. Vous devez **enrichir** un élément existant avec des informations supplémentaires
3. Vous créez des **composants personnalisés** complexes (accordéons, onglets, etc.)

---

## Les 3 catégories d'attributs ARIA

ARIA se compose de trois types d'attributs :

### 1. **Roles** (rôles) 🎭
Définissent **ce qu'est** un élément

### 2. **Properties** (propriétés) 🏷️
Définissent **les caractéristiques** d'un élément (rarement modifiées)

### 3. **States** (états) 🔄
Définissent **l'état actuel** d'un élément (peuvent changer dynamiquement)

---

## Les Roles ARIA les plus courants

Les roles décrivent le **type** d'un élément pour les technologies d'assistance.

### Role `button`

Pour indiquer qu'un élément est un bouton cliquable :

```html
<!-- Si vous DEVEZ utiliser une div comme bouton -->
<div role="button" tabindex="0" onclick="fairQuelqueChose()">
  Cliquez ici
</div>
```

⚠️ **Rappel** : Préférez toujours `<button>` qui a déjà ce rôle !

---

### Role `navigation`

Pour identifier une zone de navigation :

```html
<nav role="navigation">
  <ul>
    <li><a href="/">Accueil</a></li>
    <li><a href="/about">À propos</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

ℹ️ **Note** : `<nav>` a déjà implicitement ce rôle, mais l'ajouter explicitement peut améliorer la compatibilité avec les anciens lecteurs d'écran.

---

### Role `main`

Pour identifier le contenu principal de la page :

```html
<main role="main">
  <h1>Titre de l'article</h1>
  <p>Contenu principal...</p>
</main>
```

---

### Role `banner`

Pour l'en-tête principal du site (utilisé avec `<header>`) :

```html
<header role="banner">
  <img src="logo.png" alt="Logo de l'entreprise">
  <nav>...</nav>
</header>
```

---

### Role `contentinfo`

Pour le pied de page (utilisé avec `<footer>`) :

```html
<footer role="contentinfo">
  <p>&copy; 2025 Mon Site Web</p>
</footer>
```

---

### Role `alert`

Pour des messages d'alerte importants :

```html
<div role="alert">
  ⚠️ Attention : Votre session expire dans 5 minutes.
</div>
```

Le lecteur d'écran **annoncera immédiatement** ce contenu, même s'il est ajouté dynamiquement.

---

### Role `dialog`

Pour des fenêtres modales :

```html
<div role="dialog" aria-labelledby="dialog-title" aria-modal="true">
  <h2 id="dialog-title">Confirmer la suppression</h2>
  <p>Êtes-vous sûr de vouloir supprimer cet élément ?</p>
  <button>Oui</button>
  <button>Non</button>
</div>
```

---

## Les States et Properties essentiels

### `aria-label` 🏷️

Fournit un **nom accessible** à un élément (alternative au texte visible) :

```html
<!-- Bouton avec une icône sans texte -->
<button aria-label="Fermer la fenêtre">
  ✕
</button>

<!-- Champ de recherche -->
<input type="search" aria-label="Rechercher sur le site">
```

**Quand l'utiliser ?**
- Pour les boutons avec seulement des icônes
- Pour clarifier la fonction d'un élément

---

### `aria-labelledby` 🔗

Lie un élément à un autre élément qui sert de **label** :

```html
<h2 id="section-title">Paramètres du compte</h2>
<section aria-labelledby="section-title">
  <!-- Contenu de la section -->
</section>
```

**Avantage** : Vous pouvez réutiliser un texte déjà visible sans duplication.

---

### `aria-describedby` 📝

Fournit une **description supplémentaire** d'un élément :

```html
<label for="password">Mot de passe</label>
<input
  type="password"
  id="password"
  aria-describedby="password-hint"
>
<p id="password-hint">
  Le mot de passe doit contenir au moins 8 caractères.
</p>
```

Le lecteur d'écran lira : "Mot de passe, champ de saisie. Le mot de passe doit contenir au moins 8 caractères."

---

### `aria-hidden` 👻

Masque un élément des technologies d'assistance (mais pas visuellement) :

```html
<!-- Icône décorative, pas besoin de la lire -->
<span class="icon" aria-hidden="true">🎨</span>
<span>Galerie d'art</span>
```

**Cas d'usage courants** :
- Icônes purement décoratives
- Contenu dupliqué
- Éléments visuels sans signification sémantique

⚠️ **Attention** : Ne cachez jamais du contenu important !

---

### `aria-expanded` 🔽

Indique si un élément est **déplié ou replié** :

```html
<!-- Menu déroulant fermé -->
<button
  aria-expanded="false"
  aria-controls="submenu"
  onclick="toggleMenu()"
>
  Catégories
</button>

<ul id="submenu" hidden>
  <li>Électronique</li>
  <li>Vêtements</li>
  <li>Livres</li>
</ul>
```

```javascript
function toggleMenu() {
  const button = document.querySelector('button');
  const menu = document.getElementById('submenu');
  const isExpanded = button.getAttribute('aria-expanded') === 'true';

  // Inverser l'état
  button.setAttribute('aria-expanded', !isExpanded);
  menu.hidden = isExpanded;
}
```

---

### `aria-current` 📍

Indique l'**élément actuel** dans une navigation :

```html
<nav>
  <ul>
    <li><a href="/">Accueil</a></li>
    <li><a href="/services" aria-current="page">Services</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

**Valeurs possibles** :
- `page` : page actuelle
- `step` : étape actuelle (dans un processus)
- `location` : localisation actuelle
- `date` : date actuelle
- `time` : heure actuelle
- `true` : élément actuel (générique)

---

### `aria-live` 📢

Annonce les **changements dynamiques** de contenu :

```html
<div aria-live="polite">
  Aucune nouvelle notification
</div>
```

Quand le contenu change :
```html
<div aria-live="polite">
  Vous avez 3 nouvelles notifications
</div>
```

**Valeurs** :
- `off` (défaut) : pas d'annonce
- `polite` : annonce quand l'utilisateur a fini ce qu'il fait
- `assertive` : interrompt et annonce immédiatement (à utiliser avec parcimonie !)

**Cas d'usage** :
- Notifications
- Messages de validation de formulaire
- Résultats de recherche qui se mettent à jour

---

### `aria-required` ⚠️

Indique qu'un champ est **obligatoire** :

```html
<label for="email">Email *</label>
<input
  type="email"
  id="email"
  aria-required="true"
>
```

⚠️ **Note** : Préférez l'attribut HTML5 `required` quand c'est possible :

```html
<input type="email" id="email" required>
```

---

### `aria-invalid` ❌

Indique qu'un champ contient une **erreur** :

```html
<label for="email">Email</label>
<input
  type="email"
  id="email"
  aria-invalid="true"
  aria-describedby="email-error"
>
<span id="email-error" role="alert">
  Veuillez entrer une adresse email valide
</span>
```

**Valeurs** :
- `false` (défaut) : pas d'erreur
- `true` : contient une erreur
- `grammar` : erreur grammaticale
- `spelling` : erreur d'orthographe

---

### `aria-controls` 🎮

Identifie les éléments **contrôlés** par un élément :

```html
<button
  aria-expanded="false"
  aria-controls="menu-content"
>
  Menu
</button>

<div id="menu-content" hidden>
  <!-- Contenu du menu -->
</div>
```

Indique au lecteur d'écran que le bouton contrôle le div `menu-content`.

---

## Exemple complet : Accordéon accessible

Voyons comment combiner plusieurs attributs ARIA pour créer un accordéon accessible :

```html
<div class="accordion">

  <!-- Premier élément -->
  <h3>
    <button
      id="accordion-button-1"
      aria-expanded="false"
      aria-controls="accordion-panel-1"
      class="accordion-button"
    >
      Qu'est-ce que l'accessibilité web ?
    </button>
  </h3>
  <div
    id="accordion-panel-1"
    role="region"
    aria-labelledby="accordion-button-1"
    hidden
  >
    <p>L'accessibilité web consiste à rendre les sites utilisables par tous...</p>
  </div>

  <!-- Deuxième élément -->
  <h3>
    <button
      id="accordion-button-2"
      aria-expanded="false"
      aria-controls="accordion-panel-2"
      class="accordion-button"
    >
      Pourquoi est-ce important ?
    </button>
  </h3>
  <div
    id="accordion-panel-2"
    role="region"
    aria-labelledby="accordion-button-2"
    hidden
  >
    <p>C'est important pour l'inclusion, la conformité légale...</p>
  </div>

</div>
```

```javascript
// JavaScript pour rendre l'accordéon fonctionnel
const buttons = document.querySelectorAll('.accordion-button');

buttons.forEach(button => {
  button.addEventListener('click', () => {
    const expanded = button.getAttribute('aria-expanded') === 'true';
    const panel = document.getElementById(button.getAttribute('aria-controls'));

    // Inverser l'état
    button.setAttribute('aria-expanded', !expanded);
    panel.hidden = expanded;
  });
});
```

**Ce qui rend cet accordéon accessible :**
- ✅ `aria-expanded` indique l'état ouvert/fermé
- ✅ `aria-controls` lie le bouton au panneau
- ✅ `aria-labelledby` lie le panneau au titre
- ✅ Navigable au clavier (ce sont des vrais `<button>`)
- ✅ L'attribut `hidden` masque le contenu replié

---

## Exemple complet : Notification dynamique

Une zone de notification qui annonce les nouveaux messages :

```html
<div
  id="notification-area"
  role="status"
  aria-live="polite"
  aria-atomic="true"
  class="notification"
>
  <!-- Les notifications apparaîtront ici -->
</div>
```

```javascript
function showNotification(message) {
  const notificationArea = document.getElementById('notification-area');
  notificationArea.textContent = message;

  // Effacer après 5 secondes
  setTimeout(() => {
    notificationArea.textContent = '';
  }, 5000);
}

// Utilisation
showNotification('✅ Votre profil a été mis à jour avec succès');
```

**Explication :**
- `role="status"` indique que c'est une zone de statut
- `aria-live="polite"` annonce les changements sans interrompre
- `aria-atomic="true"` annonce tout le contenu (pas juste ce qui a changé)

---

## Les erreurs courantes à éviter

### ❌ Erreur 1 : Utiliser ARIA quand le HTML suffit

```html
<!-- ❌ Mauvais -->
<div role="button" tabindex="0">Cliquer</div>

<!-- ✅ Bon -->
<button>Cliquer</button>
```

---

### ❌ Erreur 2 : Conflits entre HTML et ARIA

```html
<!-- ❌ Mauvais : le <button> a déjà le rôle button -->
<button role="link">Ne faites pas ça</button>

<!-- ✅ Bon : utilisez l'élément approprié -->
<a href="...">Bon élément</a>
```

**Règle** : Ne changez pas le rôle natif d'un élément HTML !

---

### ❌ Erreur 3 : Oublier de mettre à jour les états ARIA

```javascript
// ❌ Mauvais : on ouvre le menu mais on oublie aria-expanded
function ouvrirMenu() {
  document.getElementById('menu').hidden = false;
  // Manque : button.setAttribute('aria-expanded', 'true');
}

// ✅ Bon : toujours synchroniser
function ouvrirMenu() {
  const button = document.querySelector('[aria-controls="menu"]');
  const menu = document.getElementById('menu');

  menu.hidden = false;
  button.setAttribute('aria-expanded', 'true');
}
```

---

### ❌ Erreur 4 : Abuser d'aria-label

```html
<!-- ❌ Mauvais : aria-label remplace le texte visible -->
<button aria-label="Soumettre le formulaire">
  Envoyer
</button>
<!-- Le lecteur d'écran dira "Soumettre le formulaire", pas "Envoyer" -->

<!-- ✅ Bon : laissez le texte visible parler -->
<button>Envoyer</button>
```

**Utilisez `aria-label` uniquement quand il n'y a pas de texte visible.**

---

### ❌ Erreur 5 : Cacher du contenu important avec aria-hidden

```html
<!-- ❌ Mauvais : masque du contenu essentiel -->
<h1 aria-hidden="true">Titre important</h1>

<!-- ✅ Bon : masquez uniquement le décoratif -->
<span aria-hidden="true">🎉</span>
<span>Félicitations !</span>
```

---

## Tableau récapitulatif des attributs ARIA essentiels

| Attribut | Type | Usage | Exemple |
|----------|------|-------|---------|
| `role` | Role | Définir le type d'élément | `role="button"` |
| `aria-label` | Property | Nommer un élément | `aria-label="Fermer"` |
| `aria-labelledby` | Property | Lier à un label existant | `aria-labelledby="title"` |
| `aria-describedby` | Property | Ajouter une description | `aria-describedby="hint"` |
| `aria-hidden` | State | Masquer aux lecteurs d'écran | `aria-hidden="true"` |
| `aria-expanded` | State | Indiquer si déplié/replié | `aria-expanded="false"` |
| `aria-current` | State | Marquer l'élément actuel | `aria-current="page"` |
| `aria-live` | Property | Annoncer les changements | `aria-live="polite"` |
| `aria-required` | Property | Champ obligatoire | `aria-required="true"` |
| `aria-invalid` | State | Champ en erreur | `aria-invalid="true"` |
| `aria-controls` | Property | Élément contrôlé | `aria-controls="menu"` |

---

## Tester vos attributs ARIA

### Outils recommandés :

1. **Lecteurs d'écran** 🔊
   - NVDA (Windows, gratuit)
   - VoiceOver (Mac, intégré)
   - Testez réellement votre site !

2. **Extensions navigateur** 🔧
   - WAVE (Web Accessibility Evaluation Tool)
   - axe DevTools
   - Accessibility Insights

3. **DevTools** 🛠️
   - Onglet "Accessibility" dans Chrome/Firefox
   - Voir l'arbre d'accessibilité

4. **Lighthouse** 💡
   - Audit automatique dans Chrome DevTools

---

## Bonnes pratiques à retenir

### ✅ À faire :

1. **Privilégiez toujours le HTML sémantique natif**
2. Utilisez ARIA seulement quand nécessaire
3. Testez avec un vrai lecteur d'écran
4. Gardez les états ARIA synchronisés avec l'interface
5. Documentez vos choix ARIA dans les commentaires

### ❌ À éviter :

1. N'utilisez pas ARIA si le HTML suffit
2. Ne changez pas le rôle natif des éléments HTML
3. N'oubliez pas de mettre à jour les états dynamiques
4. Ne cachez pas du contenu important avec `aria-hidden`
5. N'abusez pas d'`aria-label` sur des éléments avec du texte visible

---

## Conclusion

ARIA est un **outil puissant** pour améliorer l'accessibilité des applications web modernes, mais il doit être utilisé avec **discernement** :

- 🏗️ **Fondation** : HTML sémantique d'abord
- 🎨 **Enrichissement** : ARIA pour compléter quand nécessaire
- 🧪 **Validation** : Testez toujours avec des lecteurs d'écran
- 🔄 **Maintenance** : Gardez les états synchronisés

**ARIA bien utilisé rend le web plus inclusif. ARIA mal utilisé peut créer plus de problèmes qu'il n'en résout.**

Dans la prochaine section, nous verrons comment assurer une **navigation au clavier** efficace pour tous vos utilisateurs.

---

## Ressources complémentaires

- [MDN Web Docs - ARIA](https://developer.mozilla.org/fr/docs/Web/Accessibility/ARIA)
- [W3C - WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [ARIA examples - W3C](https://www.w3.org/TR/wai-aria-practices/examples/)

⏭️ [Navigation au clavier](/06-integration-html-css-javascript/03-accessibilite-web/03-navigation-clavier.md)
