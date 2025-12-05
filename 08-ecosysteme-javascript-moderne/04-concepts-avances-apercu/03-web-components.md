🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.4.3 Web Components 🆕

## Introduction

Les **Web Components** sont une technologie native du navigateur qui permet de créer des **composants HTML réutilisables et encapsulés**. Ils permettent de construire des éléments personnalisés qui fonctionnent partout, sans framework.

> 💡 **En résumé** : Les Web Components vous permettent de créer vos propres balises HTML personnalisées, comme `<ma-carte>`, `<menu-deroulant>` ou `<galerie-photos>`, qui fonctionnent exactement comme les balises HTML natives (`<button>`, `<input>`, etc.).

**Exemple d'utilisation :**
```html
<!-- Au lieu de ça : -->
<div class="carte-utilisateur">
  <img src="avatar.jpg" class="avatar">
  <h3 class="nom">Alice Dupont</h3>
  <p class="role">Développeuse</p>
</div>

<!-- On peut créer ça : -->
<carte-utilisateur
  nom="Alice Dupont"
  role="Développeuse"
  avatar="avatar.jpg">
</carte-utilisateur>
```

---

## Pourquoi les Web Components ?

### Le problème sans Web Components

Quand vous développez une application web, vous répétez souvent le même code HTML/CSS/JS :

```html
<!-- Page 1 -->
<div class="bouton-personnalise">
  <span class="icone">★</span>
  <span class="texte">Favoris</span>
</div>

<!-- Page 2 - même code répété ! -->
<div class="bouton-personnalise">
  <span class="icone">🏠</span>
  <span class="texte">Accueil</span>
</div>
```

**Problèmes :**
- Code dupliqué
- Difficile à maintenir
- CSS peut entrer en conflit
- Pas réutilisable facilement

### La solution avec Web Components

```html
<!-- Définir le composant une fois -->
<script>
  // Définition du composant
</script>

<!-- Utiliser partout -->
<bouton-icone icone="★" texte="Favoris"></bouton-icone>
<bouton-icone icone="🏠" texte="Accueil"></bouton-icone>
```

**Avantages :**
- ✅ Réutilisable
- ✅ Encapsulé (pas de conflits CSS)
- ✅ Maintenable
- ✅ Standard du web (pas de dépendance externe)

---

## Les trois technologies des Web Components

Les Web Components reposent sur **trois technologies principales** :

### 1. Custom Elements (Éléments personnalisés)
Créer vos propres balises HTML

### 2. Shadow DOM
Encapsuler le HTML et CSS du composant

### 3. HTML Templates
Définir des morceaux de HTML réutilisables

Voyons chacune en détail avec des exemples simples.

---

## 1. Custom Elements : Créer ses propres balises

### Principe de base

Un Custom Element est une classe JavaScript qui définit le comportement d'une nouvelle balise HTML.

### Premier exemple simple

```javascript
// 1. Créer une classe qui étend HTMLElement
class MonMessage extends HTMLElement {
  constructor() {
    super(); // Toujours appeler super() en premier

    // Définir le contenu
    this.innerHTML = `
      <div style="padding: 1rem; background: #e3f2fd; border-left: 4px solid #2196f3;">
        <strong>Info :</strong> Ceci est un message personnalisé !
      </div>
    `;
  }
}

// 2. Enregistrer le custom element
customElements.define('mon-message', MonMessage);
```

**Utilisation dans le HTML :**
```html
<!DOCTYPE html>
<html>
<head>
  <title>Web Components</title>
</head>
<body>
  <!-- Utiliser le composant -->
  <mon-message></mon-message>

  <script src="composant.js"></script>
</body>
</html>
```

### Règles importantes pour les noms

❌ **Invalide** :
```javascript
customElements.define('message', MonMessage); // Pas de tiret
customElements.define('Message', MonMessage);  // Majuscule
```

✅ **Valide** :
```javascript
customElements.define('mon-message', MonMessage);
customElements.define('app-header', AppHeader);
customElements.define('user-profile', UserProfile);
```

> 📌 **Règle** : Le nom doit contenir au moins un tiret (-) pour éviter les conflits avec les balises HTML futures.

### Exemple avec attributs

```javascript
class CarteUtilisateur extends HTMLElement {
  constructor() {
    super();

    // Récupérer les attributs
    const nom = this.getAttribute('nom') || 'Anonyme';
    const role = this.getAttribute('role') || 'Utilisateur';

    this.innerHTML = `
      <div style="border: 1px solid #ddd; padding: 1rem; border-radius: 8px;">
        <h3 style="margin: 0 0 0.5rem 0;">${nom}</h3>
        <p style="margin: 0; color: #666;">${role}</p>
      </div>
    `;
  }
}

customElements.define('carte-utilisateur', CarteUtilisateur);
```

**Utilisation :**
```html
<carte-utilisateur nom="Alice Dupont" role="Développeuse"></carte-utilisateur>
<carte-utilisateur nom="Bob Martin" role="Designer"></carte-utilisateur>
```

---

## 2. Shadow DOM : Encapsulation

### Qu'est-ce que le Shadow DOM ?

Le **Shadow DOM** crée une **frontière** entre votre composant et le reste de la page :
- Le CSS du composant ne fuit pas vers l'extérieur
- Le CSS de la page n'affecte pas le composant
- Le JavaScript du composant est isolé

### Exemple sans Shadow DOM (problème)

```javascript
class BoutonSimple extends HTMLElement {
  constructor() {
    super();
    this.innerHTML = `
      <style>
        button { background: blue; color: white; }
      </style>
      <button>Cliquez-moi</button>
    `;
  }
}
customElements.define('bouton-simple', BoutonSimple);
```

```html
<style>
  /* Ce CSS affecte TOUS les boutons, même ceux dans le composant ! */
  button { background: red !important; }
</style>

<bouton-simple></bouton-simple>
<!-- Le bouton sera rouge, pas bleu -->
```

### Exemple avec Shadow DOM (solution)

```javascript
class BoutonIsole extends HTMLElement {
  constructor() {
    super();

    // 1. Créer un Shadow DOM
    const shadow = this.attachShadow({ mode: 'open' });

    // 2. Ajouter du contenu dans le Shadow DOM
    shadow.innerHTML = `
      <style>
        /* Ce CSS est isolé dans le composant */
        button {
          background: blue;
          color: white;
          padding: 0.5rem 1rem;
          border: none;
          border-radius: 4px;
          cursor: pointer;
        }
        button:hover {
          background: darkblue;
        }
      </style>
      <button>Cliquez-moi</button>
    `;
  }
}

customElements.define('bouton-isole', BoutonIsole);
```

**Maintenant, le CSS externe n'affecte plus le composant !**

```html
<style>
  button { background: red !important; }
</style>

<button>Bouton normal (rouge)</button>
<bouton-isole></bouton-isole> <!-- Bouton bleu, protégé -->
```

### Mode open vs closed

```javascript
// Mode 'open' : accessible depuis l'extérieur
const shadow = this.attachShadow({ mode: 'open' });
// On peut accéder : element.shadowRoot

// Mode 'closed' : privé
const shadow = this.attachShadow({ mode: 'closed' });
// shadowRoot est null depuis l'extérieur
```

> 💡 **Conseil** : Utilisez généralement `{ mode: 'open' }` pour faciliter le debugging.

---

## 3. HTML Templates : Modèles réutilisables

### Le tag `<template>`

La balise `<template>` permet de définir du HTML qui n'est pas affiché directement mais peut être cloné et utilisé par JavaScript.

### Exemple basique

```html
<!-- Définir le template dans le HTML -->
<template id="carte-template">
  <style>
    .carte {
      border: 1px solid #ddd;
      padding: 1rem;
      border-radius: 8px;
      margin: 0.5rem;
    }
    .titre {
      margin: 0 0 0.5rem 0;
      color: #333;
    }
    .description {
      margin: 0;
      color: #666;
    }
  </style>
  <div class="carte">
    <h3 class="titre"></h3>
    <p class="description"></p>
  </div>
</template>

<script>
  class CarteProduit extends HTMLElement {
    constructor() {
      super();

      // Créer Shadow DOM
      const shadow = this.attachShadow({ mode: 'open' });

      // Récupérer le template
      const template = document.getElementById('carte-template');
      const clone = template.content.cloneNode(true);

      // Personnaliser le contenu
      clone.querySelector('.titre').textContent = this.getAttribute('titre');
      clone.querySelector('.description').textContent = this.getAttribute('description');

      // Ajouter au Shadow DOM
      shadow.appendChild(clone);
    }
  }

  customElements.define('carte-produit', CarteProduit);
</script>

<!-- Utilisation -->
<carte-produit
  titre="Ordinateur Portable"
  description="15 pouces, 16 GB RAM">
</carte-produit>
```

---

## Cycle de vie d'un Custom Element

Les Custom Elements ont des **méthodes de cycle de vie** qui sont appelées automatiquement :

```javascript
class MonComposant extends HTMLElement {
  constructor() {
    super();
    console.log('1. Élément créé');
  }

  // Appelé quand l'élément est ajouté au DOM
  connectedCallback() {
    console.log('2. Élément connecté au DOM');
  }

  // Appelé quand l'élément est retiré du DOM
  disconnectedCallback() {
    console.log('3. Élément déconnecté du DOM');
  }

  // Appelé quand un attribut observé change
  attributeChangedCallback(name, oldValue, newValue) {
    console.log(`4. Attribut ${name} changé : ${oldValue} → ${newValue}`);
  }

  // Définir quels attributs observer
  static get observedAttributes() {
    return ['nom', 'age'];
  }
}

customElements.define('mon-composant', MonComposant);
```

### Exemple pratique : Compteur

```javascript
class CompteurSimple extends HTMLElement {
  constructor() {
    super();
    this.count = 0;

    const shadow = this.attachShadow({ mode: 'open' });
    shadow.innerHTML = `
      <style>
        .compteur {
          display: flex;
          gap: 1rem;
          align-items: center;
          padding: 1rem;
          border: 2px solid #333;
          border-radius: 8px;
          width: fit-content;
        }
        button {
          padding: 0.5rem 1rem;
          cursor: pointer;
          font-size: 1rem;
          border: none;
          border-radius: 4px;
        }
        .increment { background: #4caf50; color: white; }
        .decrement { background: #f44336; color: white; }
        .valeur {
          font-size: 2rem;
          font-weight: bold;
          min-width: 3rem;
          text-align: center;
        }
      </style>
      <div class="compteur">
        <button class="decrement">-</button>
        <span class="valeur">0</span>
        <button class="increment">+</button>
      </div>
    `;
  }

  connectedCallback() {
    // Ajouter les événements quand le composant est dans le DOM
    const shadow = this.shadowRoot;
    const valeur = shadow.querySelector('.valeur');

    shadow.querySelector('.increment').addEventListener('click', () => {
      this.count++;
      valeur.textContent = this.count;
    });

    shadow.querySelector('.decrement').addEventListener('click', () => {
      this.count--;
      valeur.textContent = this.count;
    });
  }
}

customElements.define('compteur-simple', CompteurSimple);
```

**Utilisation :**
```html
<compteur-simple></compteur-simple>
```

---

## Slots : Insérer du contenu personnalisé

Les **slots** permettent de passer du contenu HTML à l'intérieur de votre composant.

### Exemple de base

```javascript
class CarteAvecSlot extends HTMLElement {
  constructor() {
    super();

    const shadow = this.attachShadow({ mode: 'open' });
    shadow.innerHTML = `
      <style>
        .carte {
          border: 2px solid #2196f3;
          padding: 1rem;
          border-radius: 8px;
          background: white;
        }
        .en-tete {
          border-bottom: 1px solid #ddd;
          padding-bottom: 0.5rem;
          margin-bottom: 0.5rem;
        }
      </style>
      <div class="carte">
        <div class="en-tete">
          <slot name="titre">Titre par défaut</slot>
        </div>
        <div class="contenu">
          <slot>Contenu par défaut</slot>
        </div>
      </div>
    `;
  }
}

customElements.define('carte-slot', CarteAvecSlot);
```

**Utilisation avec slots nommés :**
```html
<carte-slot>
  <h2 slot="titre">Mon Titre Personnalisé</h2>
  <p>Ceci est mon contenu personnalisé.</p>
  <button>Action</button>
</carte-slot>
```

### Slot par défaut

```html
<!-- Sans contenu : utilise le contenu par défaut -->
<carte-slot></carte-slot>

<!-- Avec contenu : remplace le contenu par défaut -->
<carte-slot>
  <p>Mon contenu custom</p>
</carte-slot>
```

---

## Exemple complet : Composant d'évaluation par étoiles

Créons un composant réutilisable pour afficher et modifier une note :

```javascript
class EvaluationEtoiles extends HTMLElement {
  constructor() {
    super();

    const shadow = this.attachShadow({ mode: 'open' });

    shadow.innerHTML = `
      <style>
        .container {
          display: inline-flex;
          gap: 0.25rem;
          font-size: 1.5rem;
        }
        .etoile {
          cursor: pointer;
          user-select: none;
          transition: transform 0.1s;
        }
        .etoile:hover {
          transform: scale(1.2);
        }
        .etoile.remplie {
          color: gold;
        }
        .etoile.vide {
          color: #ccc;
        }
      </style>
      <div class="container"></div>
    `;

    this.note = parseInt(this.getAttribute('note')) || 0;
    this.max = parseInt(this.getAttribute('max')) || 5;
  }

  connectedCallback() {
    this.afficher();

    // Rendre les étoiles cliquables
    const container = this.shadowRoot.querySelector('.container');
    container.addEventListener('click', (e) => {
      if (e.target.classList.contains('etoile')) {
        const nouvelleNote = parseInt(e.target.dataset.valeur);
        this.changerNote(nouvelleNote);
      }
    });
  }

  afficher() {
    const container = this.shadowRoot.querySelector('.container');
    container.innerHTML = '';

    for (let i = 1; i <= this.max; i++) {
      const etoile = document.createElement('span');
      etoile.className = i <= this.note ? 'etoile remplie' : 'etoile vide';
      etoile.textContent = '★';
      etoile.dataset.valeur = i;
      container.appendChild(etoile);
    }
  }

  changerNote(nouvelleNote) {
    this.note = nouvelleNote;
    this.setAttribute('note', nouvelleNote);
    this.afficher();

    // Émettre un événement personnalisé
    this.dispatchEvent(new CustomEvent('change', {
      detail: { note: nouvelleNote },
      bubbles: true
    }));
  }

  static get observedAttributes() {
    return ['note', 'max'];
  }

  attributeChangedCallback(name, oldValue, newValue) {
    if (oldValue !== newValue) {
      this[name] = parseInt(newValue);
      if (this.isConnected) {
        this.afficher();
      }
    }
  }
}

customElements.define('evaluation-etoiles', EvaluationEtoiles);
```

**Utilisation :**
```html
<evaluation-etoiles note="3" max="5"></evaluation-etoiles>

<script>
  // Écouter les changements
  document.querySelector('evaluation-etoiles').addEventListener('change', (e) => {
    console.log('Nouvelle note :', e.detail.note);
  });
</script>
```

---

## Communication entre composants

### Événements personnalisés

Les composants peuvent émettre des événements pour communiquer :

```javascript
class BoutonNotification extends HTMLElement {
  constructor() {
    super();

    const shadow = this.attachShadow({ mode: 'open' });
    shadow.innerHTML = `
      <button>Envoyer notification</button>
    `;

    shadow.querySelector('button').addEventListener('click', () => {
      // Émettre un événement personnalisé
      this.dispatchEvent(new CustomEvent('notification', {
        detail: { message: 'Hello !' },
        bubbles: true,  // L'événement remonte dans le DOM
        composed: true  // Traverse le Shadow DOM
      }));
    });
  }
}

customElements.define('bouton-notification', BoutonNotification);
```

**Écouter l'événement :**
```html
<bouton-notification></bouton-notification>

<script>
  document.querySelector('bouton-notification').addEventListener('notification', (e) => {
    alert(e.detail.message);
  });
</script>
```

---

## Web Components vs Frameworks

### Quand utiliser Web Components ?

✅ **Bonnes situations :**
- Composants réutilisables simples (boutons, cartes, badges)
- Widgets à intégrer sur plusieurs sites
- Pas de dépendance externe souhaitée
- Intégration dans des projets existants (multi-framework)
- Standards web et pérennité

⚠️ **Situations où un framework peut être mieux :**
- Applications complexes avec beaucoup d'état partagé
- Besoin de routing avancé
- Écosystème et outils étendus requis
- Grande communauté et ressources

### Comparaison

| Critère | Web Components | Frameworks (React/Vue) |
|---------|----------------|------------------------|
| Standards | Natif navigateur | Bibliothèque tierce |
| Taille | Léger | Plus lourd |
| Apprentissage | Moyennement simple | Courbe d'apprentissage |
| Écosystème | Limité | Très riche |
| Compatibilité | Tous frameworks | Propre écosystème |
| Performance | Excellente | Très bonne |

### Utilisation combinée

Vous pouvez utiliser Web Components **avec** un framework :

```jsx
// React
function App() {
  return (
    <div>
      <h1>Mon App React</h1>
      <evaluation-etoiles note="4"></evaluation-etoiles>
    </div>
  );
}
```

---

## Compatibilité navigateur

### Support natif

✅ **Excellent support moderne :**
- Chrome 54+
- Firefox 63+
- Safari 10+
- Edge 79+

### Polyfills pour anciens navigateurs

Pour supporter les anciens navigateurs, utilisez les polyfills :

```html
<script src="https://unpkg.com/@webcomponents/webcomponentsjs@2/webcomponents-loader.js"></script>
```

---

## Bonnes pratiques

### 1. Nommage cohérent

```javascript
// ✅ BON : préfixe cohérent
customElements.define('app-header', AppHeader);
customElements.define('app-footer', AppFooter);
customElements.define('app-card', AppCard);

// ❌ ÉVITER : noms incohérents
customElements.define('header-component', Header);
customElements.define('my-footer', Footer);
```

### 2. Toujours utiliser Shadow DOM

```javascript
class MonComposant extends HTMLElement {
  constructor() {
    super();
    // ✅ Utiliser Shadow DOM pour l'encapsulation
    const shadow = this.attachShadow({ mode: 'open' });
  }
}
```

### 3. Nettoyer dans disconnectedCallback

```javascript
class ComposantAvecTimer extends HTMLElement {
  connectedCallback() {
    this.timer = setInterval(() => {
      console.log('Tick');
    }, 1000);
  }

  disconnectedCallback() {
    // ✅ Important : nettoyer les timers, événements, etc.
    if (this.timer) {
      clearInterval(this.timer);
    }
  }
}
```

### 4. Gérer les attributs proprement

```javascript
class MonComposant extends HTMLElement {
  static get observedAttributes() {
    return ['nom', 'age'];
  }

  get nom() {
    return this.getAttribute('nom');
  }

  set nom(valeur) {
    this.setAttribute('nom', valeur);
  }

  attributeChangedCallback(name, oldValue, newValue) {
    if (oldValue !== newValue && this.isConnected) {
      this.render();
    }
  }
}
```

### 5. Séparer la logique et le rendu

```javascript
class MonComposant extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
  }

  connectedCallback() {
    this.render();
    this.attachEvents();
  }

  render() {
    // Logique de rendu
    this.shadowRoot.innerHTML = `...`;
  }

  attachEvents() {
    // Logique des événements
    this.shadowRoot.querySelector('button').addEventListener('click', ...);
  }
}
```

---

## Exemple final : Carte produit complète

```javascript
class CarteProduit extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
  }

  connectedCallback() {
    this.render();
    this.attachEvents();
  }

  render() {
    const nom = this.getAttribute('nom') || 'Produit';
    const prix = this.getAttribute('prix') || '0';
    const image = this.getAttribute('image') || 'placeholder.jpg';
    const enStock = this.hasAttribute('en-stock');

    this.shadowRoot.innerHTML = `
      <style>
        .carte {
          border: 1px solid #ddd;
          border-radius: 8px;
          overflow: hidden;
          width: 250px;
          box-shadow: 0 2px 8px rgba(0,0,0,0.1);
          transition: transform 0.2s;
        }
        .carte:hover {
          transform: translateY(-4px);
          box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }
        .image {
          width: 100%;
          height: 200px;
          object-fit: cover;
        }
        .contenu {
          padding: 1rem;
        }
        .nom {
          margin: 0 0 0.5rem 0;
          font-size: 1.2rem;
          color: #333;
        }
        .prix {
          font-size: 1.5rem;
          font-weight: bold;
          color: #2196f3;
          margin: 0.5rem 0;
        }
        .statut {
          display: inline-block;
          padding: 0.25rem 0.5rem;
          border-radius: 4px;
          font-size: 0.875rem;
          font-weight: 500;
        }
        .en-stock {
          background: #4caf50;
          color: white;
        }
        .rupture {
          background: #f44336;
          color: white;
        }
        button {
          width: 100%;
          padding: 0.75rem;
          margin-top: 1rem;
          background: #2196f3;
          color: white;
          border: none;
          border-radius: 4px;
          font-size: 1rem;
          cursor: pointer;
          transition: background 0.2s;
        }
        button:hover {
          background: #1976d2;
        }
        button:disabled {
          background: #ccc;
          cursor: not-allowed;
        }
      </style>
      <div class="carte">
        <img src="${image}" alt="${nom}" class="image">
        <div class="contenu">
          <h3 class="nom">${nom}</h3>
          <div class="prix">${prix} €</div>
          <span class="statut ${enStock ? 'en-stock' : 'rupture'}">
            ${enStock ? 'En stock' : 'Rupture de stock'}
          </span>
          <button ${!enStock ? 'disabled' : ''}>
            ${enStock ? 'Ajouter au panier' : 'Indisponible'}
          </button>
        </div>
      </div>
    `;
  }

  attachEvents() {
    const button = this.shadowRoot.querySelector('button');
    if (button) {
      button.addEventListener('click', () => {
        this.dispatchEvent(new CustomEvent('ajout-panier', {
          detail: {
            nom: this.getAttribute('nom'),
            prix: this.getAttribute('prix')
          },
          bubbles: true,
          composed: true
        }));
      });
    }
  }

  static get observedAttributes() {
    return ['nom', 'prix', 'image', 'en-stock'];
  }

  attributeChangedCallback() {
    if (this.isConnected) {
      this.render();
      this.attachEvents();
    }
  }
}

customElements.define('carte-produit', CarteProduit);
```

**Utilisation :**
```html
<carte-produit
  nom="Ordinateur Portable"
  prix="999"
  image="laptop.jpg"
  en-stock>
</carte-produit>

<carte-produit
  nom="Smartphone"
  prix="699"
  image="phone.jpg">
</carte-produit>

<script>
  document.querySelectorAll('carte-produit').forEach(carte => {
    carte.addEventListener('ajout-panier', (e) => {
      console.log('Ajouté au panier:', e.detail);
    });
  });
</script>
```

---

## Points clés à retenir

1. **Web Components = Standard web** : Pas de framework requis
2. **Trois technologies** : Custom Elements, Shadow DOM, Templates
3. **Encapsulation complète** : CSS et JavaScript isolés
4. **Réutilisables** : Fonctionnent partout, même avec des frameworks
5. **Cycle de vie** : constructor, connectedCallback, disconnectedCallback, attributeChangedCallback
6. **Communication** : Attributs (entrée) et événements personnalisés (sortie)
7. **Slots** : Pour passer du contenu HTML personnalisé
8. **Bonnes pratiques** : Nommage avec tiret, Shadow DOM, nettoyage

---

## Pour aller plus loin

Les Web Components sont une technologie puissante pour créer des composants réutilisables sans dépendances. Ils sont parfaits pour :
- Systèmes de design
- Bibliothèques de composants partagées
- Widgets intégrables
- Micro-frontends

### Ressources recommandées :
- **MDN Web Docs** : Documentation complète
- **webcomponents.org** : Exemples et composants
- **Lit** : Bibliothèque légère pour simplifier les Web Components
- **Stencil** : Compilateur de Web Components

> 🎯 **Conseil** : Commencez par créer des composants simples (boutons, badges, cartes) avant de passer à des composants complexes. Les Web Components brillent pour les composants UI réutilisables !

⏭️ [Progressive Web Apps (PWA)](/08-ecosysteme-javascript-moderne/04-concepts-avances-apercu/04-progressive-web-apps.md)
