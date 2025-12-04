🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 6.4.3 - Ordre de chargement des scripts

## Pourquoi l'ordre de chargement des scripts est-il important ?

L'ordre de chargement des scripts JavaScript a un **impact majeur** sur :
- ⚡ **La vitesse de chargement** de votre page
- 👁️ **L'expérience visuelle** de l'utilisateur
- 🐛 **Les erreurs potentielles** dans votre code
- 📊 **Les performances globales** de votre site

### Le problème

Par défaut, quand le navigateur rencontre une balise `<script>` :
1. Il **arrête** de parser le HTML
2. Il **télécharge** le fichier JavaScript
3. Il **exécute** le script
4. Seulement après, il **reprend** le parsing du HTML

**Conséquence** : Si vos scripts sont mal placés, l'utilisateur voit une **page blanche** pendant plusieurs secondes !

---

## Comprendre le chargement d'une page web

### Sans JavaScript - Flux normal 📄

Quand il n'y a pas de JavaScript, le navigateur parse le HTML de haut en bas :

```
HTML parsing ━━━━━━━━━━━━━━━━━━━━━━▶ Page affichée
      ↓            ↓           ↓
    <head>       <body>      </html>
```

**Temps** : ~100-200ms pour une page simple
**Expérience** : Fluide, le contenu apparaît progressivement

---

### Avec JavaScript (comportement par défaut) - Blocage ⛔

Avec des scripts placés dans le `<head>` :

```html
<!DOCTYPE html>
<html>
<head>
  <script src="gros-script.js"></script> ← Le navigateur s'arrête ici !
</head>
<body>
  <h1>Mon site</h1>
  <!-- L'utilisateur ne voit rien encore... -->
</body>
</html>
```

**Chronologie** :
```
HTML parsing ━━▶ STOP ⛔
                  ↓
              Télécharge script (500ms)
                  ↓
              Exécute script (200ms)
                  ↓
HTML parsing ━━━━━━━━━━━━▶ Page affichée

Total : 700ms d'attente avant de voir quoi que ce soit !
```

**Expérience utilisateur** : Page blanche pendant 700ms → **Mauvais !**

---

## Les différentes positions de scripts

### 1. Scripts dans le `<head>` (sans attributs) ❌

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ❌ Mauvais : bloque le rendu -->
  <script src="script.js"></script>
</head>
<body>
  <h1>Titre</h1>
  <p>Contenu...</p>
</body>
</html>
```

**Comportement** :
```
1. Parse <head>
2. Rencontre <script>
3. ⛔ STOP : télécharge et exécute
4. Reprend le parsing
5. Affiche <body>
```

**Problèmes** :
- ❌ Page blanche pendant le téléchargement
- ❌ Script exécuté avant que le DOM soit prêt
- ❌ `document.getElementById()` ne trouve rien (éléments pas encore créés)

**Quand l'utiliser** : Presque jamais ! Sauf pour des scripts critiques très légers.

---

### 2. Scripts à la fin du `<body>` ✅ (ancienne méthode)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Titre</h1>
  <p>Contenu...</p>

  <!-- ✅ Mieux : exécuté après le HTML -->
  <script src="script.js"></script>
</body>
</html>
```

**Comportement** :
```
1. Parse <head>
2. Affiche <body> progressivement
3. L'utilisateur voit le contenu ✓
4. Rencontre <script>
5. Télécharge et exécute
```

**Avantages** :
- ✅ Page visible rapidement
- ✅ DOM déjà créé (pas d'erreur avec getElementById)
- ✅ Expérience utilisateur améliorée

**Inconvénients** :
- ⚠️ Le script ne commence à charger qu'à la fin
- ⚠️ Sur connexion lente, les interactions peuvent être retardées

**Quand l'utiliser** : Bonne pratique classique, toujours valide aujourd'hui.

---

### 3. Scripts avec attribut `defer` ✅ (moderne, recommandé)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ✅ Moderne : defer -->
  <script src="script.js" defer></script>
</head>
<body>
  <h1>Titre</h1>
  <p>Contenu...</p>
</body>
</html>
```

**Comportement** :
```
1. Parse <head>
2. Rencontre <script defer>
3. ✓ Lance le téléchargement EN PARALLÈLE
4. Continue le parsing (pas de blocage !)
5. Affiche le contenu
6. Quand le HTML est complètement parsé → exécute le script
```

**Chronologie visuelle** :
```
HTML parsing ━━━━━━━━━━━━━━━━━━▶ Page complète
     ↓
  Téléchargement script (en parallèle)
     ↓━━━━━━━━━━━━━━━━━━━━━━━━▶ Script prêt
                                    ↓
                              Exécution script
```

**Avantages** :
- ✅ Pas de blocage du parsing
- ✅ Page visible rapidement
- ✅ Script téléchargé en parallèle (gain de temps)
- ✅ Exécuté après le DOM complet
- ✅ Ordre d'exécution préservé (si plusieurs scripts defer)

**Inconvénients** :
- Aucun ! C'est la méthode recommandée.

**Quand l'utiliser** : **Par défaut pour tous vos scripts principaux !**

---

### 4. Scripts avec attribut `async` ⚡ (asynchrone)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- Async : pour scripts indépendants -->
  <script src="analytics.js" async></script>
</head>
<body>
  <h1>Titre</h1>
  <p>Contenu...</p>
</body>
</html>
```

**Comportement** :
```
1. Parse <head>
2. Rencontre <script async>
3. ✓ Lance le téléchargement EN PARALLÈLE
4. Continue le parsing
5. DÈS QUE le script est téléchargé :
   ⛔ STOP, exécute le script
6. Reprend le parsing
```

**Chronologie visuelle** :
```
HTML parsing ━━━━━━━━▶⛔━━━━━━━━▶ Page complète
     ↓               ↑
  Téléchargement   Exécution
     ↓━━━━━━━━━━━━━┘
```

**Avantages** :
- ✅ Téléchargement en parallèle
- ✅ Exécution dès que possible (pas d'attente)

**Inconvénients** :
- ❌ Interrompt le parsing pour s'exécuter
- ❌ Ordre d'exécution non garanti (si plusieurs scripts async)
- ❌ DOM peut ne pas être complet au moment de l'exécution

**Quand l'utiliser** :
- Scripts **indépendants** (analytics, publicités)
- Scripts qui **n'interagissent pas** avec le DOM
- Scripts qui **ne dépendent d'aucun autre script**

---

## Tableau comparatif : defer vs async vs normal

| Caractéristique | Normal (sans attribut) | `defer` | `async` |
|-----------------|----------------------|---------|---------|
| **Téléchargement** | Bloque le parsing | En parallèle | En parallèle |
| **Exécution** | Immédiate (bloque) | Après parsing HTML | Dès téléchargement fini |
| **Ordre garanti** | ✅ Oui | ✅ Oui | ❌ Non |
| **DOM disponible** | ⚠️ Partiel | ✅ Complet | ❌ Peut-être pas |
| **Blocage rendu** | ❌ Oui | ✅ Non | ⚠️ Bref |
| **Usage recommandé** | Fin du body | **Scripts principaux** | Scripts indépendants |

---

## Visualisation : Normal vs Defer vs Async

### Script Normal (dans `<head>`)

```
┌─────────────────────────────────────────────────┐
│ Chronologie                                     │
├─────────────────────────────────────────────────┤
│                                                 │
│ HTML parsing ━━▶⛔                              │
│                  │                              │
│                  ↓ Télécharge script            │
│                  ↓━━━━━━━━━━━┐                  │
│                              ↓ Exécute          │
│                              ↓━━━━┐             │
│                                   ↓             │
│ HTML parsing ━━━━━━━━━━━━━━━━━━━━▶              │
│                                                 │
│ Affichage : ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜✅             │
│             └─ Attente ─┘                       │
└─────────────────────────────────────────────────┘
```

---

### Script avec `defer`

```
┌─────────────────────────────────────────────────┐
│ Chronologie                                     │
├─────────────────────────────────────────────────┤
│                                                 │
│ HTML parsing ━━━━━━━━━━━━━━━━━━━━▶              │
│      │                                          │
│      ↓ Télécharge en parallèle                  │
│      ↓━━━━━━━━━━━━━━━━━━━━━━━━┐                 │
│                                  ↓ Exécute      │
│                                  ↓━━━━┐         │
│                                       ✅        │
│                                                 │
│ Affichage : ✅✅✅✅✅✅✅✅✅✅               │
│             └─ Visible immédiatement ─┘         │
└─────────────────────────────────────────────────┘
```

---

### Script avec `async`

```
┌─────────────────────────────────────────────────┐
│ Chronologie                                     │
├─────────────────────────────────────────────────┤
│                                                 │
│ HTML parsing ━━━━━━━━▶⛔━━━━━━━━━▶              │
│      │                 │                        │
│      ↓ Télécharge      ↓ Exécute                │
│      ↓━━━━━━━━━━━━━━━┘                          │
│                                                 │
│ Affichage : ✅✅✅⬜⬜✅✅✅✅✅               │
│                     └─ Brève pause ─┘           │
└─────────────────────────────────────────────────┘
```

---

## Exemples pratiques

### Exemple 1 : Site simple avec un script principal

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon Site</title>
  <link rel="stylesheet" href="styles.css">

  <!-- ✅ Script principal avec defer -->
  <script src="main.js" defer></script>
</head>
<body>
  <header>
    <h1>Mon Site Web</h1>
    <nav>
      <ul>
        <li><a href="/">Accueil</a></li>
        <li><a href="/about">À propos</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <h2>Bienvenue</h2>
    <p>Contenu de la page...</p>
    <button id="btn">Cliquer</button>
  </main>

  <footer>
    <p>&copy; 2025 Mon Site</p>
  </footer>
</body>
</html>
```

**Pourquoi `defer` ?**
- Le script peut interagir avec le DOM (bouton #btn)
- Le DOM est garanti d'être complet
- Pas de blocage du rendu

---

### Exemple 2 : Plusieurs scripts avec dépendances

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ✅ Scripts avec defer : ordre préservé -->
  <script src="jquery.min.js" defer></script>
  <script src="utils.js" defer></script>     <!-- Dépend de jQuery -->
  <script src="main.js" defer></script>       <!-- Dépend de utils.js -->
</head>
<body>
  <h1>Mon Site</h1>
</body>
</html>
```

**Ordre d'exécution garanti** :
1. jquery.min.js
2. utils.js (peut utiliser jQuery)
3. main.js (peut utiliser utils et jQuery)

**Avantage de `defer`** : Préserve l'ordre même avec téléchargements parallèles.

---

### Exemple 3 : Bibliothèque externe + script principal

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ✅ Bibliothèque depuis CDN avec defer -->
  <script
    src="https://cdn.jsdelivr.net/npm/chart.js@3.9.1/dist/chart.min.js"
    defer
  ></script>

  <!-- ✅ Script principal qui utilise Chart.js -->
  <script src="charts.js" defer></script>
</head>
<body>
  <canvas id="myChart"></canvas>
</body>
</html>
```

---

### Exemple 4 : Script d'analytics (indépendant)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ✅ Script principal -->
  <script src="main.js" defer></script>

  <!-- ✅ Analytics avec async (indépendant) -->
  <script src="https://www.google-analytics.com/analytics.js" async></script>
</head>
<body>
  <h1>Mon Site</h1>
</body>
</html>
```

**Pourquoi `async` pour analytics ?**
- N'interagit pas avec le DOM
- Indépendant du reste du code
- On veut qu'il s'exécute le plus tôt possible
- L'ordre n'importe pas

---

### Exemple 5 : Script critique (rare)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ⚠️ Script critique qui doit bloquer -->
  <script>
    // Configuration critique avant tout chargement
    window.APP_CONFIG = {
      apiUrl: 'https://api.example.com',
      version: '1.0.0'
    };
  </script>

  <!-- ✅ Scripts normaux avec defer -->
  <script src="main.js" defer></script>
</head>
<body>
  <h1>Mon Site</h1>
</body>
</html>
```

**Cas d'usage du script inline sans defer** :
- Configuration globale nécessaire immédiatement
- Code très court (quelques lignes)
- Doit s'exécuter avant tout autre script

---

## Cas d'usage spécifiques

### 1. Scripts de personnalisation du thème (dark mode)

Pour éviter un "flash" de thème incorrect :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- Script inline SANS defer : s'exécute immédiatement -->
  <script>
    // Applique le thème sauvegardé avant l'affichage
    const savedTheme = localStorage.getItem('theme') || 'light';
    document.documentElement.setAttribute('data-theme', savedTheme);
  </script>

  <link rel="stylesheet" href="styles.css">
  <script src="main.js" defer></script>
</head>
<body>
  <h1>Mon Site</h1>
  <button id="theme-toggle">Changer de thème</button>
</body>
</html>
```

**Pourquoi sans `defer` ?**
- Doit s'exécuter AVANT le CSS pour éviter le flash
- Code très court (rapide)

---

### 2. Chargement conditionnel

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <script>
    // Détecte si on est sur mobile
    if (window.innerWidth < 768) {
      // Charge un script spécifique mobile
      const script = document.createElement('script');
      script.src = 'mobile.js';
      script.defer = true;
      document.head.appendChild(script);
    }
  </script>

  <script src="main.js" defer></script>
</head>
<body>
  <h1>Mon Site</h1>
</body>
</html>
```

---

### 3. Module ES6 (type="module")

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ✅ Les modules se comportent comme defer par défaut -->
  <script type="module" src="app.js"></script>
</head>
<body>
  <h1>Mon Site</h1>
</body>
</html>
```

**Important** : `type="module"` a un comportement `defer` automatique !

---

### 4. Plusieurs scripts async (ordre non garanti)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- Ces scripts s'exécuteront dans un ordre aléatoire -->
  <script src="analytics.js" async></script>
  <script src="ads.js" async></script>
  <script src="chat-widget.js" async></script>

  <!-- Script principal avec ordre garanti -->
  <script src="main.js" defer></script>
</head>
<body>
  <h1>Mon Site</h1>
</body>
</html>
```

**Résultat** :
- Les 3 scripts async s'exécutent dès qu'ils sont téléchargés
- L'ordre peut être : chat → analytics → ads (variable)
- main.js s'exécute toujours en dernier

---

## Bonnes pratiques

### ✅ Règles générales

#### 1. **Par défaut : utilisez `defer`**

```html
<head>
  <!-- ✅ Méthode recommandée -->
  <script src="main.js" defer></script>
</head>
```

---

#### 2. **Scripts indépendants : utilisez `async`**

```html
<head>
  <!-- ✅ Analytics, publicités, widgets -->
  <script src="analytics.js" async></script>
</head>
```

---

#### 3. **Ordre de priorité : CSS avant JS**

```html
<head>
  <!-- ✅ CSS en premier pour éviter FOUC -->
  <link rel="stylesheet" href="styles.css">

  <!-- JS après -->
  <script src="main.js" defer></script>
</head>
```

**FOUC** = Flash Of Unstyled Content (contenu non stylé visible brièvement).

---

#### 4. **Scripts critiques : inline dans `<head>`**

```html
<head>
  <!-- ✅ Configuration critique -->
  <script>
    window.CONFIG = { apiKey: 'abc123' };
  </script>

  <script src="main.js" defer></script>
</head>
```

Mais gardez ces scripts **très courts** (< 10 lignes).

---

#### 5. **Grouper les scripts similaires**

```html
<head>
  <!-- Scripts principaux (defer) -->
  <script src="jquery.js" defer></script>
  <script src="utils.js" defer></script>
  <script src="main.js" defer></script>

  <!-- Scripts indépendants (async) -->
  <script src="analytics.js" async></script>
  <script src="ads.js" async></script>
</head>
```

---

#### 6. **Minimiser le nombre de scripts**

```html
<!-- ❌ Mauvais : 10 petits scripts -->
<script src="utils.js" defer></script>
<script src="helpers.js" defer></script>
<script src="validators.js" defer></script>
<!-- ... 7 autres ... -->

<!-- ✅ Bon : 1 script bundlé -->
<script src="app.bundle.js" defer></script>
```

Regroupez vos scripts avec un bundler (Webpack, Vite).

---

### ❌ Erreurs courantes à éviter

#### 1. Scripts dans `<head>` sans defer/async

```html
<!-- ❌ Bloque le rendu -->
<head>
  <script src="heavy-script.js"></script>
</head>
```

**Solution** :
```html
<!-- ✅ Ajoutez defer -->
<head>
  <script src="heavy-script.js" defer></script>
</head>
```

---

#### 2. Scripts avant le CSS

```html
<head>
  <!-- ❌ Mauvais ordre -->
  <script src="main.js" defer></script>
  <link rel="stylesheet" href="styles.css">
</head>
```

**Solution** :
```html
<head>
  <!-- ✅ CSS en premier -->
  <link rel="stylesheet" href="styles.css">
  <script src="main.js" defer></script>
</head>
```

---

#### 3. Utiliser async pour des scripts dépendants

```html
<head>
  <!-- ❌ utils.js peut s'exécuter avant jquery ! -->
  <script src="jquery.js" async></script>
  <script src="utils.js" async></script> <!-- Dépend de jQuery -->
</head>
```

**Solution** :
```html
<head>
  <!-- ✅ Utilisez defer pour garantir l'ordre -->
  <script src="jquery.js" defer></script>
  <script src="utils.js" defer></script>
</head>
```

---

#### 4. defer sur un script inline

```html
<!-- ❌ defer ne fonctionne pas sur les scripts inline -->
<script defer>
  console.log('Hello');
</script>
```

**Note** : `defer` et `async` ne fonctionnent que sur les scripts **externes** (avec `src`).

---

#### 5. Multiples versions de la même bibliothèque

```html
<head>
  <!-- ❌ jQuery chargé 2 fois ! -->
  <script src="jquery-3.6.0.js" defer></script>
  <script src="plugin-with-jquery.js" defer></script>
  <!-- Le plugin inclut jQuery aussi → conflit -->
</head>
```

---

## Impact sur les performances

### Mesurer l'impact avec DevTools

#### 1. Onglet Network

```
1. Ouvrir DevTools (F12)
2. Onglet "Network"
3. Recharger la page
4. Observer :
   - Waterfall : ordre de téléchargement
   - Timing : temps de chargement
   - Bloquage du rendu
```

---

#### 2. Onglet Performance

```
1. Onglet "Performance"
2. Cliquer sur Record
3. Recharger la page
4. Arrêter l'enregistrement
5. Analyser :
   - Parse HTML
   - Evaluate Script
   - Blocking time
```

---

#### 3. Lighthouse

```
1. Onglet "Lighthouse"
2. Lancer l'audit
3. Consulter :
   - First Contentful Paint (FCP)
   - Time to Interactive (TTI)
   - Total Blocking Time (TBT)
```

**Métriques cibles** :
- FCP < 1.8s
- TTI < 3.8s
- TBT < 200ms

---

### Comparaison des performances

#### Test : Page avec script de 500 KB

**Sans defer (dans `<head>`)** :
```
First Contentful Paint : 2.5s ❌
Time to Interactive : 3.2s ❌
Total Blocking Time : 800ms ❌
```

**Avec defer** :
```
First Contentful Paint : 0.8s ✅
Time to Interactive : 1.5s ✅
Total Blocking Time : 100ms ✅
```

**Amélioration** : 68% plus rapide !

---

## Stratégies avancées

### 1. Chargement différé (Lazy Loading)

Pour les scripts non essentiels, chargez-les après l'affichage initial :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- ✅ Scripts essentiels -->
  <script src="main.js" defer></script>
</head>
<body>
  <h1>Mon Site</h1>

  <script>
    // Charge les scripts non essentiels après le chargement
    window.addEventListener('load', function() {
      // Chargement différé du chat
      const chatScript = document.createElement('script');
      chatScript.src = 'chat-widget.js';
      chatScript.async = true;
      document.body.appendChild(chatScript);

      // Chargement différé des analytics
      const analyticsScript = document.createElement('script');
      analyticsScript.src = 'analytics.js';
      analyticsScript.async = true;
      document.body.appendChild(analyticsScript);
    });
  </script>
</body>
</html>
```

**Avantage** : Page interactive plus rapidement, widgets chargés ensuite.

---

### 2. Préchargement (Preload)

Commencer à télécharger un script avant qu'il soit nécessaire :

```html
<head>
  <meta charset="UTF-8">
  <title>Mon Site</title>

  <!-- Préchargement : télécharge mais n'exécute pas -->
  <link rel="preload" href="important.js" as="script">

  <!-- Utilisation plus tard -->
  <script src="important.js" defer></script>
</head>
```

**Cas d'usage** : Scripts importants mais pas immédiats.

---

### 3. DNS Prefetch pour CDN

```html
<head>
  <!-- Résolution DNS en avance -->
  <link rel="dns-prefetch" href="https://cdn.example.com">

  <!-- Script depuis le CDN -->
  <script src="https://cdn.example.com/library.js" defer></script>
</head>
```

---

### 4. Code Splitting

Avec des bundlers modernes (Webpack, Vite), divisez votre code :

```javascript
// main.js

// Chargement immédiat
import { init } from './core.js';
init();

// Chargement à la demande
button.addEventListener('click', async () => {
  const { openModal } = await import('./modal.js');
  openModal();
});
```

**Résultat** : Seul le code nécessaire est chargé initialement.

---

## Checklist d'optimisation ✅

### Audit de vos scripts

- [ ] **Tous les scripts ont `defer` ou `async`**
  - Scripts principaux → `defer`
  - Scripts indépendants → `async`

- [ ] **CSS chargé avant JavaScript**
  ```html
  <link rel="stylesheet" href="styles.css">
  <script src="main.js" defer></script>
  ```

- [ ] **Pas de scripts bloquants dans `<head>`**
  - Sauf scripts critiques inline très courts

- [ ] **Scripts avec dépendances : ordre préservé**
  - Utilisez `defer` pour garantir l'ordre

- [ ] **Scripts lourds : lazy loaded**
  - Widgets, analytics → chargés après l'affichage initial

- [ ] **Nombre de scripts minimisé**
  - Bundler pour regrouper les fichiers

- [ ] **Scripts minifiés en production**
  - Fichiers .min.js

- [ ] **Métriques de performance vérifiées**
  - Lighthouse score > 90
  - FCP < 1.8s
  - TTI < 3.8s

---

## Récapitulatif : Quelle méthode choisir ?

### Arbre de décision 🌳

```
Votre script interagit avec le DOM ?
├─ OUI
│  ├─ Dépend d'autres scripts ?
│  │  ├─ OUI → defer (ordre garanti)
│  │  └─ NON → defer (sûr)
│  └─
└─ NON (script indépendant)
   ├─ Analytics, publicités, widgets ?
   │  └─ OUI → async
   └─ Configuration critique ?
      └─ OUI → inline dans <head> (sans defer)
```

---

### Tableau de recommandations

| Type de script | Méthode recommandée | Exemple |
|----------------|---------------------|---------|
| **Script principal** | `defer` | `<script src="main.js" defer></script>` |
| **Bibliothèque + script** | `defer` (les deux) | jQuery + votre code |
| **Analytics** | `async` | Google Analytics |
| **Publicités** | `async` | AdSense |
| **Chat widget** | `async` ou lazy load | Intercom, LiveChat |
| **Config critique** | Inline sans defer | Theme, langue |
| **Module ES6** | `type="module"` | `<script type="module" src="app.js">` |

---

## Exemples de structures complètes

### Structure simple (site vitrine)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon Site Vitrine</title>

  <!-- CSS en premier -->
  <link rel="stylesheet" href="styles.css">

  <!-- Script principal avec defer -->
  <script src="main.js" defer></script>

  <!-- Analytics en async -->
  <script src="https://www.google-analytics.com/analytics.js" async></script>
</head>
<body>
  <header>
    <h1>Mon Site</h1>
  </header>

  <main>
    <p>Contenu...</p>
  </main>

  <footer>
    <p>&copy; 2025</p>
  </footer>
</body>
</html>
```

---

### Structure avancée (application web)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon Application</title>

  <!-- Préconnexions -->
  <link rel="preconnect" href="https://cdn.example.com">
  <link rel="dns-prefetch" href="https://analytics.google.com">

  <!-- Configuration critique (inline, très court) -->
  <script>
    window.APP_CONFIG = {
      apiUrl: 'https://api.example.com',
      env: 'production'
    };
  </script>

  <!-- CSS -->
  <link rel="stylesheet" href="styles.min.css">

  <!-- Scripts principaux avec defer (ordre garanti) -->
  <script src="https://cdn.example.com/vue@3.2.js" defer></script>
  <script src="utils.min.js" defer></script>
  <script src="app.min.js" defer></script>

  <!-- Scripts indépendants avec async -->
  <script src="https://www.google-analytics.com/analytics.js" async></script>
</head>
<body>
  <div id="app">
    <!-- Vue.js monte ici -->
  </div>

  <!-- Lazy loading des scripts non essentiels -->
  <script>
    window.addEventListener('load', function() {
      // Chat widget après chargement initial
      const chat = document.createElement('script');
      chat.src = 'chat-widget.js';
      chat.async = true;
      document.body.appendChild(chat);
    });
  </script>
</body>
</html>
```

---

## Conclusion

L'ordre de chargement des scripts est **crucial** pour les performances de votre site web. En suivant les bonnes pratiques de cette section, vous pouvez :

- ⚡ **Réduire de 50-70%** le temps de chargement perçu
- 👁️ **Améliorer l'expérience utilisateur** (contenu visible plus rapidement)
- 🔍 **Améliorer votre SEO** (Google favorise les sites rapides)
- 📊 **Optimiser les Core Web Vitals**

**Points clés à retenir** :

1. **Par défaut : `defer`** pour tous vos scripts principaux
2. **`async`** uniquement pour les scripts indépendants (analytics, publicités)
3. **CSS avant JavaScript** pour éviter le FOUC
4. **Minimiser le nombre de scripts** (bundling)
5. **Tester les performances** avec Lighthouse

**La règle d'or** : Si vous hésitez, utilisez `defer`. C'est le choix le plus sûr et performant dans 90% des cas.

Dans la prochaine section, nous verrons comment réduire le nombre de requêtes HTTP pour améliorer encore les performances.

---

## Ressources complémentaires

### Documentation
- [MDN - The Script element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script)
- [MDN - defer attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-defer)
- [MDN - async attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-async)

### Articles
- [JavaScript Loading Priorities](https://addyosmani.com/blog/script-priorities/)
- [Efficiently load JavaScript with defer and async](https://flaviocopes.com/javascript-async-defer/)
- [Web.dev - Optimize JavaScript execution](https://web.dev/optimize-javascript-execution/)

### Outils
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [WebPageTest](https://www.webpagetest.org/)
- [GTmetrix](https://gtmetrix.com/)

⏭️ [Réduction des requêtes HTTP](/06-integration-html-css-javascript/04-performance-optimisation/04-reduction-requetes-http.md)
