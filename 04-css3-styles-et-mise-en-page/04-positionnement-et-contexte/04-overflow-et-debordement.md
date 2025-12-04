🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 4.4.4 - Overflow et débordement

## Introduction

Que se passe-t-il quand le **contenu d'un élément est plus grand** que l'élément lui-même ? Par défaut, le contenu **déborde** (overflow). La propriété `overflow` vous permet de **contrôler ce comportement**.

### Le problème du débordement

```
┌─────────────────┐
│  Conteneur      │
│  [Contenu qui   │
│   dépasse...]   │ ← Déborde du conteneur !
└─────────────────┘
   qui continue ici
```

**Exemples courants** :
- Un texte trop long dans une boîte de taille fixe
- Une image plus grande que son conteneur
- Un menu déroulant qui sort de l'écran
- Un tableau trop large pour l'écran mobile

---

## 1. La propriété `overflow`

### Syntaxe de base

```css
.element {
  overflow: valeur;
}
```

### Les quatre valeurs principales

#### `visible` (valeur par défaut)

Le contenu déborde **librement** en dehors du conteneur.

```css
.box {
  width: 200px;
  height: 100px;
  overflow: visible; /* Valeur par défaut */
}
```

**Résultat visuel** :

```
┌─────────────────┐
│  Box (200×100)  │
│  Lorem ipsum    │
└─────────────────┘
  dolor sit amet    ← Déborde librement
  consectetur
```

#### `hidden`

Le contenu qui déborde est **masqué** (coupé).

```css
.box {
  width: 200px;
  height: 100px;
  overflow: hidden; /* Cache ce qui déborde */
}
```

**Résultat visuel** :

```
┌─────────────────┐
│  Box (200×100)  │
│  Lorem ipsum    │
└─────────────────┘
   (reste caché)
```

#### `scroll`

Ajoute des **barres de défilement** (toujours visibles, même si pas nécessaire).

```css
.box {
  width: 200px;
  height: 100px;
  overflow: scroll; /* Scrollbars toujours présentes */
}
```

**Résultat visuel** :

```
┌─────────────────┐▲
│  Box (200×100)  ││ ← Barre verticale
│  Lorem ipsum    ││
└─────────────────┘▼
◄─────────────────► ← Barre horizontale (même si pas nécessaire)
```

#### `auto`

Ajoute des barres de défilement **uniquement si nécessaire**.

```css
.box {
  width: 200px;
  height: 100px;
  overflow: auto; /* Scrollbars seulement si besoin */
}
```

**Résultat visuel** :

```
Si le contenu déborde :
┌─────────────────┐▲
│  Box (200×100)  ││ ← Barre apparaît
│  Lorem ipsum    ││
└─────────────────┘▼

Si le contenu tient :
┌─────────────────┐
│  Box (200×100)  │
│  Lorem ipsum    │  ← Pas de barre
└─────────────────┘
```

---

## 2. Exemple complet des quatre valeurs

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Overflow - Les 4 valeurs</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 50px;
      background-color: #f5f5f5;
    }

    .container {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 30px;
      max-width: 1000px;
      margin: 0 auto;
    }

    .box {
      width: 250px;
      height: 150px;
      padding: 20px;
      background-color: white;
      border: 3px solid #333;
      border-radius: 8px;
    }

    .box h3 {
      margin: 0 0 10px 0;
      color: #667eea;
    }

    .visible {
      overflow: visible;
    }

    .hidden {
      overflow: hidden;
    }

    .scroll {
      overflow: scroll;
    }

    .auto {
      overflow: auto;
    }
  </style>
</head>
<body>
  <h1>Les 4 valeurs de overflow</h1>

  <div class="container">
    <div class="box visible">
      <h3>overflow: visible</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Le contenu déborde librement en dehors de la boîte.</p>
    </div>

    <div class="box hidden">
      <h3>overflow: hidden</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Le contenu qui déborde est masqué.</p>
    </div>

    <div class="box scroll">
      <h3>overflow: scroll</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Des barres de défilement apparaissent toujours.</p>
    </div>

    <div class="box auto">
      <h3>overflow: auto</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Les barres apparaissent seulement si nécessaire.</p>
    </div>
  </div>
</body>
</html>
```

---

## 3. `overflow-x` et `overflow-y` : Contrôle par axe

Vous pouvez contrôler le débordement **séparément** pour chaque axe.

### Syntaxe

```css
.element {
  overflow-x: valeur; /* Axe horizontal (gauche-droite) */
  overflow-y: valeur; /* Axe vertical (haut-bas) */
}
```

### Exemple : Scroll horizontal uniquement

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Overflow-x</title>
  <style>
    .code-container {
      width: 100%;
      max-width: 600px;
      margin: 50px auto;
      background-color: #1e1e1e;
      color: #dcdcdc;
      padding: 20px;
      border-radius: 8px;
      font-family: 'Courier New', monospace;

      overflow-x: auto;   /* Scroll horizontal si nécessaire */
      overflow-y: hidden; /* Pas de scroll vertical */
    }

    .code-container pre {
      margin: 0;
      white-space: nowrap; /* Empêche le retour à la ligne */
    }
  </style>
</head>
<body>
  <div class="code-container">
    <pre>
function calculateSomethingVeryLongThatDoesNotFitInTheScreen() {
  const result = performComplexCalculation(param1, param2, param3);
  return result;
}
    </pre>
  </div>
</body>
</html>
```

**Résultat** : Une barre de défilement horizontale apparaît, mais pas verticale.

### Exemple : Scroll vertical uniquement

```css
.chat-messages {
  width: 300px;
  height: 400px;
  overflow-x: hidden; /* Cache le débordement horizontal */
  overflow-y: auto;   /* Scroll vertical si nécessaire */
}
```

### Combinaisons courantes

```css
/* Scroll vertical, pas horizontal */
.element {
  overflow-x: hidden;
  overflow-y: auto;
}

/* Scroll horizontal, pas vertical */
.element {
  overflow-x: auto;
  overflow-y: hidden;
}

/* Pas de scroll du tout */
.element {
  overflow-x: hidden;
  overflow-y: hidden;
}
/* OU plus court : */
.element {
  overflow: hidden;
}

/* Scroll dans les deux directions si besoin */
.element {
  overflow: auto;
}
/* Équivalent à : */
.element {
  overflow-x: auto;
  overflow-y: auto;
}
```

---

## 4. Cas d'usage pratiques

### Cas 1 : Zone de chat scrollable

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Chat scrollable</title>
  <style>
    .chat-widget {
      width: 350px;
      height: 500px;
      background: white;
      border: 1px solid #ddd;
      border-radius: 10px;
      display: flex;
      flex-direction: column;
      margin: 50px auto;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    .chat-header {
      padding: 20px;
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      border-radius: 10px 10px 0 0;
    }

    .chat-messages {
      flex: 1;
      padding: 20px;
      overflow-y: auto;   /* Scroll vertical */
      overflow-x: hidden; /* Pas de scroll horizontal */
    }

    .message {
      background-color: #f0f0f0;
      padding: 10px 15px;
      border-radius: 20px;
      margin-bottom: 10px;
      max-width: 80%;
    }

    .message.sent {
      background-color: #667eea;
      color: white;
      margin-left: auto;
    }

    .chat-input {
      padding: 20px;
      border-top: 1px solid #ddd;
    }

    .chat-input input {
      width: 100%;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 20px;
      box-sizing: border-box;
    }
  </style>
</head>
<body>
  <div class="chat-widget">
    <div class="chat-header">
      <h3 style="margin: 0;">Chat Support</h3>
    </div>

    <div class="chat-messages">
      <div class="message">Bonjour ! Comment puis-je vous aider ?</div>
      <div class="message sent">J'ai une question sur mon compte</div>
      <div class="message">Bien sûr, je suis là pour ça.</div>
      <div class="message sent">Comment changer mon mot de passe ?</div>
      <div class="message">Allez dans Paramètres > Sécurité</div>
      <div class="message sent">Merci !</div>
      <div class="message">Avec plaisir. Autre chose ?</div>
      <div class="message sent">Non, c'est tout</div>
      <div class="message">Excellente journée !</div>
      <!-- Ajoutez plus de messages pour tester le scroll -->
    </div>

    <div class="chat-input">
      <input type="text" placeholder="Tapez votre message...">
    </div>
  </div>
</body>
</html>
```

---

### Cas 2 : Tableau large sur mobile

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Tableau scrollable</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }

    .table-wrapper {
      width: 100%;
      overflow-x: auto; /* Scroll horizontal sur petit écran */
      -webkit-overflow-scrolling: touch; /* Scroll fluide sur iOS */
    }

    table {
      width: 100%;
      min-width: 600px; /* Largeur minimum du tableau */
      border-collapse: collapse;
      background: white;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    th {
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      padding: 15px;
      text-align: left;
      white-space: nowrap;
    }

    td {
      padding: 15px;
      border-bottom: 1px solid #ddd;
    }

    tr:hover {
      background-color: #f5f5f5;
    }
  </style>
</head>
<body>
  <h1>Tableau Responsive</h1>
  <p>Réduisez la largeur de la fenêtre pour voir le scroll horizontal.</p>

  <div class="table-wrapper">
    <table>
      <thead>
        <tr>
          <th>Nom</th>
          <th>Prénom</th>
          <th>Email</th>
          <th>Téléphone</th>
          <th>Ville</th>
          <th>Statut</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Dupont</td>
          <td>Jean</td>
          <td>jean.dupont@email.com</td>
          <td>06 12 34 56 78</td>
          <td>Paris</td>
          <td>Actif</td>
        </tr>
        <tr>
          <td>Martin</td>
          <td>Sophie</td>
          <td>sophie.martin@email.com</td>
          <td>06 23 45 67 89</td>
          <td>Lyon</td>
          <td>Actif</td>
        </tr>
        <tr>
          <td>Bernard</td>
          <td>Pierre</td>
          <td>pierre.bernard@email.com</td>
          <td>06 34 56 78 90</td>
          <td>Marseille</td>
          <td>Inactif</td>
        </tr>
      </tbody>
    </table>
  </div>
</body>
</html>
```

---

### Cas 3 : Galerie d'images avec scroll horizontal

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Galerie horizontale</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 50px 20px;
      background-color: #1a1a1a;
    }

    h1 {
      color: white;
      text-align: center;
      margin-bottom: 30px;
    }

    .gallery {
      display: flex;
      gap: 20px;
      overflow-x: auto;   /* Scroll horizontal */
      overflow-y: hidden; /* Pas de scroll vertical */
      padding: 20px 0;
      -webkit-overflow-scrolling: touch; /* Scroll fluide */
    }

    /* Cacher la scrollbar sur Webkit */
    .gallery::-webkit-scrollbar {
      height: 8px;
    }

    .gallery::-webkit-scrollbar-track {
      background: #333;
      border-radius: 10px;
    }

    .gallery::-webkit-scrollbar-thumb {
      background: #667eea;
      border-radius: 10px;
    }

    .gallery-item {
      flex: 0 0 300px; /* Largeur fixe, ne rétrécit pas */
      height: 200px;
      background: linear-gradient(135deg, #667eea, #764ba2);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 24px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>Galerie à scroll horizontal</h1>

  <div class="gallery">
    <div class="gallery-item">Image 1</div>
    <div class="gallery-item">Image 2</div>
    <div class="gallery-item">Image 3</div>
    <div class="gallery-item">Image 4</div>
    <div class="gallery-item">Image 5</div>
    <div class="gallery-item">Image 6</div>
    <div class="gallery-item">Image 7</div>
  </div>
</body>
</html>
```

---

### Cas 4 : Modal avec contenu scrollable

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Modal scrollable</title>
  <style>
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .modal {
      background: white;
      border-radius: 10px;
      width: 100%;
      max-width: 600px;
      max-height: 80vh; /* Maximum 80% de la hauteur de l'écran */
      display: flex;
      flex-direction: column;
    }

    .modal-header {
      padding: 20px;
      border-bottom: 1px solid #ddd;
    }

    .modal-body {
      padding: 20px;
      overflow-y: auto; /* Scroll si le contenu dépasse */
      flex: 1;
    }

    .modal-footer {
      padding: 20px;
      border-top: 1px solid #ddd;
      display: flex;
      justify-content: flex-end;
      gap: 10px;
    }

    .btn {
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .btn-primary {
      background: #667eea;
      color: white;
    }

    .btn-secondary {
      background: #ddd;
    }
  </style>
</head>
<body>
  <div class="modal-overlay">
    <div class="modal">
      <div class="modal-header">
        <h2 style="margin: 0;">Conditions d'utilisation</h2>
      </div>

      <div class="modal-body">
        <h3>1. Acceptation des conditions</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>

        <h3>2. Utilisation du service</h3>
        <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua...</p>

        <h3>3. Propriété intellectuelle</h3>
        <p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris...</p>

        <h3>4. Confidentialité</h3>
        <p>Duis aute irure dolor in reprehenderit in voluptate velit esse...</p>

        <h3>5. Limitation de responsabilité</h3>
        <p>Excepteur sint occaecat cupidatat non proident, sunt in culpa...</p>

        <!-- Ajoutez plus de contenu pour tester le scroll -->
      </div>

      <div class="modal-footer">
        <button class="btn btn-secondary">Refuser</button>
        <button class="btn btn-primary">Accepter</button>
      </div>
    </div>
  </div>
</body>
</html>
```

---

## 5. Personnaliser les scrollbars

### Pour les navigateurs Webkit (Chrome, Safari, Edge)

```css
/* La scrollbar elle-même */
.element::-webkit-scrollbar {
  width: 12px;  /* Largeur verticale */
  height: 12px; /* Hauteur horizontale */
}

/* Le fond de la scrollbar */
.element::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 10px;
}

/* Le curseur de la scrollbar */
.element::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 10px;
}

/* Le curseur au survol */
.element::-webkit-scrollbar-thumb:hover {
  background: #555;
}
```

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Scrollbar personnalisée</title>
  <style>
    .custom-scroll {
      width: 400px;
      height: 300px;
      margin: 50px auto;
      padding: 20px;
      background: white;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      overflow-y: auto;
    }

    /* Personnalisation de la scrollbar */
    .custom-scroll::-webkit-scrollbar {
      width: 10px;
    }

    .custom-scroll::-webkit-scrollbar-track {
      background: #f0f0f0;
      border-radius: 10px;
    }

    .custom-scroll::-webkit-scrollbar-thumb {
      background: linear-gradient(135deg, #667eea, #764ba2);
      border-radius: 10px;
    }

    .custom-scroll::-webkit-scrollbar-thumb:hover {
      background: linear-gradient(135deg, #764ba2, #667eea);
    }
  </style>
</head>
<body>
  <div class="custom-scroll">
    <h2>Scrollbar personnalisée</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
    <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua...</p>
    <p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris...</p>
    <p>Duis aute irure dolor in reprehenderit in voluptate velit esse...</p>
    <p>Excepteur sint occaecat cupidatat non proident...</p>
    <p>Sunt in culpa qui officia deserunt mollit anim id est laborum...</p>
  </div>
</body>
</html>
```

### Cacher complètement les scrollbars

```css
/* Webkit (Chrome, Safari, Edge) */
.element::-webkit-scrollbar {
  display: none;
}

/* Firefox */
.element {
  scrollbar-width: none;
}

/* Pour tous les navigateurs */
.element {
  -ms-overflow-style: none;  /* IE et Edge ancien */
  scrollbar-width: none;      /* Firefox */
}

.element::-webkit-scrollbar {
  display: none;              /* Chrome, Safari, Edge */
}
```

**⚠️ Attention** : Cacher les scrollbars peut nuire à l'accessibilité. L'utilisateur ne saura pas qu'il peut scroller !

---

## 6. Propriétés liées : `text-overflow`

### Le problème du texte trop long

Quand un texte est trop long pour tenir sur une ligne :

```
┌─────────────────────────┐
│ Titre très très très... │ ← Déborde
└─────────────────────────┘
```

### Solution avec `text-overflow: ellipsis`

```css
.element {
  white-space: nowrap;      /* Empêche le retour à la ligne */
  overflow: hidden;         /* Cache le débordement */
  text-overflow: ellipsis;  /* Ajoute "..." */
}
```

**Résultat** :

```
┌─────────────────────────┐
│ Titre très très tr...   │ ← Points de suspension
└─────────────────────────┘
```

### Exemple pratique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Text Overflow</title>
  <style>
    .card {
      width: 300px;
      background: white;
      border-radius: 10px;
      padding: 20px;
      margin: 50px auto;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    .card-title {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 10px;

      /* Ellipsis sur une ligne */
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .card-description {
      color: #666;

      /* Ellipsis sur plusieurs lignes (Webkit uniquement) */
      display: -webkit-box;
      -webkit-line-clamp: 3; /* Nombre de lignes */
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
  </style>
</head>
<body>
  <div class="card">
    <h2 class="card-title">
      Ceci est un titre très très long qui va être tronqué avec des points de suspension
    </h2>
    <p class="card-description">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
    </p>
  </div>
</body>
</html>
```

**Résultat** :
- Le titre est tronqué sur une ligne avec "..."
- La description est limitée à 3 lignes avec "..."

---

## 7. Propriété `overflow-wrap` (anciennement `word-wrap`)

### Le problème des mots très longs

```
┌─────────────────────────┐
│ https://www.example.com/│
very-long-url-that-does-not-fit
└─────────────────────────┘
```

Le mot déborde car il est trop long et ne peut pas être coupé.

### Solution avec `overflow-wrap`

```css
.element {
  overflow-wrap: break-word; /* Coupe les mots longs */
}
```

**Résultat** :

```
┌─────────────────────────┐
│ https://www.example.com/│
│ very-long-url-that-does-│
│ not-fit                 │
└─────────────────────────┘
```

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Overflow Wrap</title>
  <style>
    .container {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 30px;
      max-width: 800px;
      margin: 50px auto;
    }

    .box {
      padding: 20px;
      background: white;
      border: 2px solid #ddd;
      border-radius: 10px;
      word-break: break-all; /* Alternative plus agressive */
    }

    .box h3 {
      margin-top: 0;
    }

    .no-wrap {
      /* Comportement par défaut */
    }

    .with-wrap {
      overflow-wrap: break-word;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="box no-wrap">
      <h3>Sans overflow-wrap</h3>
      <p>URL courte : example.com</p>
      <p>URL longue : https://www.example.com/very-long-path/that/continues/forever</p>
    </div>

    <div class="box with-wrap">
      <h3>Avec overflow-wrap</h3>
      <p>URL courte : example.com</p>
      <p>URL longue : https://www.example.com/very-long-path/that/continues/forever</p>
    </div>
  </div>
</body>
</html>
```

### Différence entre `overflow-wrap` et `word-break`

```css
/* overflow-wrap: break-word */
/* Coupe seulement si le mot ne tient pas */
.element {
  overflow-wrap: break-word;
}

/* word-break: break-all */
/* Coupe agressivement, même au milieu d'un mot normal */
.element {
  word-break: break-all;
}
```

**Recommandation** : Utilisez `overflow-wrap: break-word` plutôt que `word-break: break-all` pour préserver la lisibilité.

---

## 8. Tableau récapitulatif

### Propriété `overflow`

| Valeur | Comportement | Quand utiliser |
|--------|-------------|----------------|
| `visible` | Déborde librement | Presque jamais (valeur par défaut) |
| `hidden` | Masque le débordement | Cacher ce qui dépasse, créer des effets |
| `scroll` | Scrollbars toujours visibles | Rarement (préférer `auto`) |
| `auto` | Scrollbars si nécessaire | **Le plus utilisé** ✅ |

### Propriétés par axe

| Propriété | Contrôle |
|-----------|----------|
| `overflow-x` | Axe horizontal uniquement |
| `overflow-y` | Axe vertical uniquement |
| `overflow` | Les deux axes |

### Propriétés de texte

| Propriété | Usage |
|-----------|-------|
| `text-overflow: ellipsis` | Ajouter "..." au texte tronqué |
| `overflow-wrap: break-word` | Couper les mots longs |
| `word-break: break-all` | Couper agressivement (à éviter) |

---

## 9. Bonnes pratiques

### ✅ À faire

```css
/* Utiliser auto plutôt que scroll */
.element {
  overflow: auto; /* ✅ Barres seulement si nécessaire */
}

/* Combiner avec max-height pour limiter la hauteur */
.chat {
  max-height: 400px;
  overflow-y: auto;
}

/* Scroll fluide sur mobile */
.scroll-container {
  overflow: auto;
  -webkit-overflow-scrolling: touch;
}

/* Ellipsis pour les titres */
.title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

### ❌ À éviter

```css
/* Éviter overflow: scroll (barres toujours visibles) */
.element {
  overflow: scroll; /* ❌ Préférer auto */
}

/* Éviter d'utiliser overflow: hidden pour corriger des layouts */
.container {
  overflow: hidden; /* ❌ Cache peut-être des éléments importants */
}

/* Éviter de cacher les scrollbars sans bonne raison */
.element::-webkit-scrollbar {
  display: none; /* ⚠️ Problème d'accessibilité */
}
```

---

## 10. Cas pratiques avancés

### Sticky header avec contenu scrollable

```css
.container {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.header {
  position: sticky;
  top: 0;
  background: white;
  z-index: 10;
}

.content {
  flex: 1;
  overflow-y: auto; /* Le contenu scroll, pas le header */
}
```

### Scroll snap (galerie)

```css
.gallery {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
}

.gallery-item {
  scroll-snap-align: start;
  flex: 0 0 100%;
}
```

### Zone de texte avec hauteur limitée

```css
textarea {
  max-height: 200px;
  overflow-y: auto;
  resize: vertical;
}
```

---

## Points clés à retenir

✅ **`overflow: auto`** est la valeur la plus utilisée (scrollbars si nécessaire)

✅ **`overflow: hidden`** masque ce qui déborde (utile pour des effets)

✅ **`overflow-x` et `overflow-y`** permettent un contrôle par axe

✅ **`text-overflow: ellipsis`** ajoute "..." aux textes tronqués

✅ **`overflow-wrap: break-word`** coupe les mots très longs

✅ **Personnalisez les scrollbars** avec `::-webkit-scrollbar` (Webkit)

✅ **Pensez à l'accessibilité** : ne cachez pas les scrollbars sans raison

---

## Erreurs courantes à éviter

❌ **Oublier white-space avec text-overflow**
```css
/* ❌ Ne fonctionne pas */
.element {
  overflow: hidden;
  text-overflow: ellipsis;
}

/* ✅ Fonctionne */
.element {
  white-space: nowrap; /* NÉCESSAIRE */
  overflow: hidden;
  text-overflow: ellipsis;
}
```

❌ **Utiliser overflow: scroll au lieu de auto**
```css
/* ❌ Barres toujours visibles */
.element { overflow: scroll; }

/* ✅ Barres seulement si besoin */
.element { overflow: auto; }
```

❌ **Cacher les scrollbars sans alternative**
```css
/* ❌ L'utilisateur ne sait pas qu'il peut scroller */
.element::-webkit-scrollbar { display: none; }

/* ✅ Garder les scrollbars visibles */
```

---

## Conclusion

La propriété `overflow` est **essentielle** pour contrôler le débordement du contenu. Elle est particulièrement utile pour :

- Créer des zones scrollables (chat, modal, tableaux)
- Limiter la hauteur de certains contenus
- Gérer les tableaux larges sur mobile
- Créer des galeries à défilement horizontal
- Tronquer élégamment les textes longs

Combinée avec `text-overflow`, `overflow-wrap` et la personnalisation des scrollbars, vous avez tous les outils pour gérer le débordement de manière professionnelle et accessible.

---


Vous avez terminé la section sur le positionnement et le contexte ! Dans la prochaine section, nous verrons comment rendre vos sites **responsive** et adaptés à toutes les tailles d'écran. 🎉

⏭️ [Responsive Design](/04-css3-styles-et-mise-en-page/05-responsive-design/README.md)
