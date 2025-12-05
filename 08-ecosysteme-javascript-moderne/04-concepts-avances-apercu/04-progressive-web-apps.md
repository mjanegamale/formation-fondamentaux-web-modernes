🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.4.4 Progressive Web Apps (PWA) 🆕

## Introduction

Une **Progressive Web App (PWA)** est une application web qui se comporte comme une application native installée sur votre téléphone ou ordinateur. C'est le meilleur des deux mondes : la facilité d'une page web combinée à l'expérience d'une vraie application.

> 💡 **En résumé** : Une PWA est un site web qui peut être installé sur votre appareil, fonctionner hors ligne, envoyer des notifications, et s'afficher en plein écran comme une application mobile.

**Exemples de PWA célèbres :**
- Twitter Lite
- Instagram (version web)
- Spotify Web Player
- Pinterest
- Starbucks

---

## Qu'est-ce qui rend une application "Progressive" ?

### Une application web classique

```
Site web normal
    ↓
Navigateur nécessaire
    ↓
Toujours en ligne
    ↓
Pas d'icône sur l'écran d'accueil
    ↓
Barre d'adresse visible
```

### Une Progressive Web App

```
PWA
    ↓
Peut être installée
    ↓
Fonctionne hors ligne
    ↓
Icône sur l'écran d'accueil
    ↓
Affichage plein écran (comme une app native)
    ↓
Notifications possibles
    ↓
Mise à jour automatique
```

---

## Les caractéristiques d'une PWA

Une PWA doit être :

### 1. **Progressive** (Progressive)
Fonctionne pour tous les utilisateurs, quel que soit leur navigateur

### 2. **Responsive** (Adaptative)
S'adapte à tous les écrans : mobile, tablette, desktop

### 3. **Connectivity Independent** (Indépendante de la connexion)
Fonctionne hors ligne ou avec une connexion faible

### 4. **App-like** (Comme une application)
Navigation et interactions fluides

### 5. **Fresh** (À jour)
Toujours la dernière version grâce aux Service Workers

### 6. **Safe** (Sécurisée)
Servie via HTTPS pour éviter l'espionnage

### 7. **Discoverable** (Découvrable)
Identifiable comme "application" par les moteurs de recherche

### 8. **Re-engageable** (Réengageante)
Notifications push pour ramener les utilisateurs

### 9. **Installable** (Installable)
Peut être ajoutée à l'écran d'accueil sans App Store

### 10. **Linkable** (Partageable par lien)
Facilement partageable via une URL

---

## Les technologies clés d'une PWA

Une PWA repose sur **trois piliers techniques** :

### 1. HTTPS (Sécurité)
Connexion sécurisée obligatoire

### 2. Service Workers (Fonctionnement hors ligne)
Script JavaScript qui tourne en arrière-plan

### 3. Web App Manifest (Installation)
Fichier JSON qui décrit l'application

---

## 1. HTTPS : La sécurité avant tout

### Pourquoi HTTPS est obligatoire ?

Les PWA utilisent des fonctionnalités sensibles (géolocalisation, caméra, stockage). HTTPS garantit que personne ne peut intercepter ou modifier les données.

```
HTTP (non sécurisé)  ❌
    ↓
Pas de PWA possible

HTTPS (sécurisé)  ✅
    ↓
PWA possible
```

### Comment obtenir HTTPS ?

**Pour le développement :**
- `localhost` est automatiquement considéré comme sécurisé
- Pas besoin de certificat en développement local

**Pour la production :**
- Certificat SSL/TLS (souvent gratuit avec Let's Encrypt)
- Hébergeurs comme Netlify, Vercel, GitHub Pages offrent HTTPS automatiquement

---

## 2. Service Workers : Le cœur d'une PWA

### Qu'est-ce qu'un Service Worker ?

Un **Service Worker** est un script JavaScript qui s'exécute en arrière-plan, séparément de la page web. Il agit comme un **proxy** entre votre application et le réseau.

```
Votre site web
    ↓
Service Worker (intercepte les requêtes)
    ↓
    ├─→ Cache (hors ligne) ✅
    └─→ Réseau (en ligne) 🌐
```

### Ce que peut faire un Service Worker

- ✅ Mettre en cache des fichiers
- ✅ Intercepter les requêtes réseau
- ✅ Fonctionner hors ligne
- ✅ Recevoir des notifications push
- ✅ Synchroniser en arrière-plan
- ❌ Ne peut PAS accéder au DOM directement
- ❌ Ne peut PAS utiliser localStorage

### Exemple basique de Service Worker

**1. Enregistrer le Service Worker (dans votre fichier JS principal) :**

```javascript
// app.js
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/sw.js')
      .then(registration => {
        console.log('Service Worker enregistré ✅', registration);
      })
      .catch(error => {
        console.log('Échec de l\'enregistrement ❌', error);
      });
  });
}
```

**2. Créer le Service Worker (fichier séparé) :**

```javascript
// sw.js
const CACHE_NAME = 'mon-app-v1';
const urlsToCache = [
  '/',
  '/index.html',
  '/styles.css',
  '/app.js',
  '/images/logo.png'
];

// Installation : mise en cache des fichiers
self.addEventListener('install', event => {
  console.log('Service Worker: Installation');

  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => {
        console.log('Fichiers mis en cache');
        return cache.addAll(urlsToCache);
      })
  );
});

// Activation : nettoyage des anciens caches
self.addEventListener('activate', event => {
  console.log('Service Worker: Activation');

  event.waitUntil(
    caches.keys().then(cacheNames => {
      return Promise.all(
        cacheNames.map(cacheName => {
          if (cacheName !== CACHE_NAME) {
            console.log('Suppression ancien cache:', cacheName);
            return caches.delete(cacheName);
          }
        })
      );
    })
  );
});

// Interception des requêtes
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        // Retourner depuis le cache si disponible
        if (response) {
          return response;
        }
        // Sinon, récupérer depuis le réseau
        return fetch(event.request);
      })
  );
});
```

### Cycle de vie d'un Service Worker

```
1. INSTALLATION (install)
   ↓
   Mise en cache des fichiers
   ↓
2. ACTIVATION (activate)
   ↓
   Nettoyage des anciens caches
   ↓
3. INTERCEPTION (fetch)
   ↓
   Gestion des requêtes
   ↓
4. MISE À JOUR
   ↓
   Nouveau cycle si le fichier change
```

### Stratégies de cache

#### Cache First (Cache d'abord)
```javascript
// Idéal pour les ressources statiques (images, CSS, JS)
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => response || fetch(event.request))
  );
});
```

#### Network First (Réseau d'abord)
```javascript
// Idéal pour les données dynamiques (API)
self.addEventListener('fetch', event => {
  event.respondWith(
    fetch(event.request)
      .then(response => {
        // Mettre en cache pour plus tard
        const clonedResponse = response.clone();
        caches.open(CACHE_NAME).then(cache => {
          cache.put(event.request, clonedResponse);
        });
        return response;
      })
      .catch(() => {
        // Si échec réseau, utiliser le cache
        return caches.match(event.request);
      })
  );
});
```

#### Stale While Revalidate
```javascript
// Retourne le cache immédiatement, puis met à jour en arrière-plan
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.open(CACHE_NAME).then(cache => {
      return cache.match(event.request).then(cachedResponse => {
        const fetchPromise = fetch(event.request).then(networkResponse => {
          cache.put(event.request, networkResponse.clone());
          return networkResponse;
        });
        return cachedResponse || fetchPromise;
      });
    })
  );
});
```

---

## 3. Web App Manifest : Rendre l'application installable

### Qu'est-ce que le Manifest ?

Le **manifest.json** est un fichier JSON qui décrit votre application : nom, icônes, couleurs, mode d'affichage, etc.

### Exemple de manifest.json

```json
{
  "name": "Mon Application Géniale",
  "short_name": "MonApp",
  "description": "Une super application web progressive",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#2196f3",
  "orientation": "portrait",
  "icons": [
    {
      "src": "/images/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/images/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

### Propriétés importantes

#### name et short_name
```json
{
  "name": "Mon Application Géniale",  // Nom complet
  "short_name": "MonApp"              // Nom court sous l'icône
}
```

#### start_url
```json
{
  "start_url": "/"  // Page de démarrage quand on lance l'app
}
```

#### display
```json
{
  "display": "standalone"  // Mode d'affichage
}
```

**Options de display :**
- `standalone` : Comme une app native (sans barre d'adresse)
- `fullscreen` : Plein écran total
- `minimal-ui` : Barre minimale
- `browser` : Dans le navigateur normal

#### theme_color et background_color
```json
{
  "theme_color": "#2196f3",      // Couleur de la barre de statut
  "background_color": "#ffffff"  // Couleur de l'écran de chargement
}
```

#### icons
```json
{
  "icons": [
    {
      "src": "/images/icon-72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "/images/icon-96.png",
      "sizes": "96x96",
      "type": "image/png"
    },
    {
      "src": "/images/icon-128.png",
      "sizes": "128x128",
      "type": "image/png"
    },
    {
      "src": "/images/icon-144.png",
      "sizes": "144x144",
      "type": "image/png"
    },
    {
      "src": "/images/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/images/icon-512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any maskable"
    }
  ]
}
```

**Tailles d'icônes recommandées :** 72, 96, 128, 144, 192, 512 pixels

### Lier le manifest dans le HTML

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon Application PWA</title>

  <!-- Lien vers le manifest -->
  <link rel="manifest" href="/manifest.json">

  <!-- Theme color pour Safari/iOS -->
  <meta name="theme-color" content="#2196f3">

  <!-- Icône pour iOS -->
  <link rel="apple-touch-icon" href="/images/icon-192.png">
</head>
<body>
  <!-- Contenu de l'application -->
</body>
</html>
```

---

## Installation de la PWA

### Prompt d'installation

Quand une PWA remplit tous les critères, le navigateur affiche automatiquement un **prompt d'installation**.

**Critères pour déclencher le prompt :**
1. ✅ Servie via HTTPS
2. ✅ Manifest valide avec nom, icônes, start_url
3. ✅ Service Worker enregistré
4. ✅ L'utilisateur a visité le site au moins deux fois avec au moins 5 minutes entre les visites

### Personnaliser le prompt d'installation

```javascript
let deferredPrompt;

// Capturer l'événement beforeinstallprompt
window.addEventListener('beforeinstallprompt', (e) => {
  // Empêcher le prompt automatique
  e.preventDefault();

  // Sauvegarder l'événement pour plus tard
  deferredPrompt = e;

  // Afficher votre propre bouton d'installation
  document.getElementById('installButton').style.display = 'block';
});

// Quand l'utilisateur clique sur votre bouton
document.getElementById('installButton').addEventListener('click', async () => {
  if (deferredPrompt) {
    // Afficher le prompt
    deferredPrompt.prompt();

    // Attendre la réponse de l'utilisateur
    const { outcome } = await deferredPrompt.userChoice;

    if (outcome === 'accepted') {
      console.log('Utilisateur a accepté l\'installation');
    } else {
      console.log('Utilisateur a refusé l\'installation');
    }

    deferredPrompt = null;
    document.getElementById('installButton').style.display = 'none';
  }
});

// Détecter quand l'app est installée
window.addEventListener('appinstalled', () => {
  console.log('PWA installée avec succès !');
  deferredPrompt = null;
});
```

### HTML pour le bouton d'installation

```html
<button id="installButton" style="display: none;">
  📱 Installer l'application
</button>
```

---

## Notifications Push

Les PWA peuvent envoyer des notifications, même quand l'application n'est pas ouverte.

### Demander la permission

```javascript
async function demanderPermissionNotifications() {
  if ('Notification' in window) {
    const permission = await Notification.requestPermission();

    if (permission === 'granted') {
      console.log('Permission accordée ✅');
      afficherNotification();
    } else if (permission === 'denied') {
      console.log('Permission refusée ❌');
    }
  }
}

function afficherNotification() {
  if (Notification.permission === 'granted') {
    navigator.serviceWorker.ready.then(registration => {
      registration.showNotification('Nouvelle notification', {
        body: 'Ceci est le contenu de la notification',
        icon: '/images/icon-192.png',
        badge: '/images/badge.png',
        vibrate: [200, 100, 200],
        tag: 'notification-tag',
        actions: [
          { action: 'open', title: 'Ouvrir' },
          { action: 'close', title: 'Fermer' }
        ]
      });
    });
  }
}
```

### Gérer les clics sur les notifications (dans le Service Worker)

```javascript
// sw.js
self.addEventListener('notificationclick', event => {
  event.notification.close();

  if (event.action === 'open') {
    // Ouvrir l'application
    clients.openWindow('/');
  }

  // Ou focuser sur l'onglet existant
  event.waitUntil(
    clients.matchAll({ type: 'window' }).then(clientList => {
      for (let client of clientList) {
        if (client.url === '/' && 'focus' in client) {
          return client.focus();
        }
      }
      return clients.openWindow('/');
    })
  );
});
```

---

## Exemple complet : PWA simple

### Structure du projet

```
mon-pwa/
├── index.html
├── manifest.json
├── sw.js
├── app.js
├── styles.css
└── images/
    ├── icon-192.png
    └── icon-512.png
```

### index.html

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ma PWA</title>

  <link rel="manifest" href="/manifest.json">
  <link rel="stylesheet" href="/styles.css">
  <meta name="theme-color" content="#2196f3">
  <link rel="apple-touch-icon" href="/images/icon-192.png">
</head>
<body>
  <header>
    <h1>Ma Progressive Web App</h1>
  </header>

  <main>
    <p>Cette application fonctionne hors ligne !</p>
    <button id="installButton" style="display: none;">
      📱 Installer l'application
    </button>
    <button id="notifyButton">
      🔔 Afficher une notification
    </button>
  </main>

  <div id="status">
    <p>Statut : <span id="networkStatus">En ligne</span></p>
  </div>

  <script src="/app.js"></script>
</body>
</html>
```

### manifest.json

```json
{
  "name": "Ma Progressive Web App",
  "short_name": "Ma PWA",
  "description": "Une PWA d'exemple",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#2196f3",
  "orientation": "portrait",
  "icons": [
    {
      "src": "/images/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/images/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

### app.js

```javascript
// Enregistrer le Service Worker
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/sw.js')
      .then(reg => console.log('Service Worker enregistré ✅'))
      .catch(err => console.log('Erreur Service Worker ❌', err));
  });
}

// Installation de l'app
let deferredPrompt;

window.addEventListener('beforeinstallprompt', (e) => {
  e.preventDefault();
  deferredPrompt = e;
  document.getElementById('installButton').style.display = 'block';
});

document.getElementById('installButton').addEventListener('click', async () => {
  if (deferredPrompt) {
    deferredPrompt.prompt();
    const { outcome } = await deferredPrompt.userChoice;
    console.log('Résultat installation:', outcome);
    deferredPrompt = null;
    document.getElementById('installButton').style.display = 'none';
  }
});

// Notifications
document.getElementById('notifyButton').addEventListener('click', async () => {
  if ('Notification' in window) {
    const permission = await Notification.requestPermission();
    if (permission === 'granted') {
      navigator.serviceWorker.ready.then(registration => {
        registration.showNotification('Ma PWA', {
          body: 'Ceci est une notification de test !',
          icon: '/images/icon-192.png',
          vibrate: [200, 100, 200]
        });
      });
    }
  }
});

// Détection en ligne/hors ligne
window.addEventListener('online', () => {
  document.getElementById('networkStatus').textContent = 'En ligne';
  document.getElementById('networkStatus').style.color = 'green';
});

window.addEventListener('offline', () => {
  document.getElementById('networkStatus').textContent = 'Hors ligne';
  document.getElementById('networkStatus').style.color = 'red';
});
```

### sw.js

```javascript
const CACHE_NAME = 'ma-pwa-v1';
const urlsToCache = [
  '/',
  '/index.html',
  '/styles.css',
  '/app.js',
  '/images/icon-192.png',
  '/images/icon-512.png'
];

// Installation
self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(urlsToCache))
  );
});

// Activation
self.addEventListener('activate', event => {
  event.waitUntil(
    caches.keys().then(cacheNames => {
      return Promise.all(
        cacheNames.map(cacheName => {
          if (cacheName !== CACHE_NAME) {
            return caches.delete(cacheName);
          }
        })
      );
    })
  );
});

// Interception des requêtes
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => response || fetch(event.request))
  );
});

// Gestion des clics sur notifications
self.addEventListener('notificationclick', event => {
  event.notification.close();
  event.waitUntil(
    clients.openWindow('/')
  );
});
```

---

## Tester votre PWA

### Dans Chrome DevTools

1. Ouvrir DevTools (F12)
2. Aller dans l'onglet **Application**
3. Vérifier :
   - **Manifest** : Toutes les propriétés sont valides
   - **Service Workers** : Enregistré et actif
   - **Cache Storage** : Fichiers mis en cache
   - **Storage** : Vérifier les données stockées

### Test d'installation

1. Servir via HTTPS (ou localhost)
2. Ouvrir dans Chrome/Edge
3. Chercher l'icône d'installation dans la barre d'adresse
4. Ou utiliser le menu : "Installer l'application..."

### Lighthouse Audit

Chrome DevTools inclut **Lighthouse** pour auditer votre PWA :

1. DevTools > **Lighthouse**
2. Sélectionner **Progressive Web App**
3. Cliquer sur **Generate report**
4. Voir les recommandations

---

## Avantages des PWA

### Pour les utilisateurs

- ✅ **Installation facile** : Pas besoin d'App Store
- ✅ **Poids léger** : Moins lourdes que les apps natives
- ✅ **Mises à jour automatiques** : Toujours la dernière version
- ✅ **Fonctionne hors ligne** : Accès même sans connexion
- ✅ **Rapide** : Chargement instantané depuis le cache
- ✅ **Lien partageable** : Partage par URL

### Pour les développeurs

- ✅ **Un seul code** : Web, mobile, desktop
- ✅ **Pas d'App Store** : Publication immédiate
- ✅ **SEO** : Référençable par les moteurs de recherche
- ✅ **Coût réduit** : Moins cher qu'une app native
- ✅ **Mise à jour simple** : Déploiement instantané
- ✅ **Technologies web** : HTML/CSS/JS standard

---

## Inconvénients et limitations

### Limites techniques

❌ **Accès limité aux fonctionnalités natives** :
- Pas d'accès complet aux contacts, calendrier
- Bluetooth limité
- NFC partiel

❌ **Support iOS limité** :
- Notifications push pas supportées sur iOS
- Moins d'intégration système
- Limitations de stockage

❌ **Taille du cache limitée** :
- Selon le navigateur et l'appareil
- Peut être vidé automatiquement

### Différences avec les apps natives

| Fonctionnalité | PWA | App Native |
|----------------|-----|------------|
| Installation | Via navigateur | Via App Store |
| Mise à jour | Automatique | Manuel |
| Hors ligne | ✅ Oui | ✅ Oui |
| Notifications | ⚠️ Limitées iOS | ✅ Complètes |
| Accès matériel | ⚠️ Limité | ✅ Complet |
| Performance | ⚠️ Bonne | ✅ Excellente |
| Coût développement | 💰 Faible | 💰💰💰 Élevé |

---

## Quand créer une PWA ?

### ✅ Bonnes situations pour une PWA

- Site de contenu (blog, actualités, magazine)
- Application de productivité (notes, todo, planning)
- E-commerce (boutique en ligne)
- Réseau social
- Application métier web
- Portfolio / CV en ligne
- Application de réservation

### ⚠️ Situations où une app native est préférable

- Jeux 3D complexes
- Application nécessitant un accès complet au matériel
- Application nécessitant des performances maximales
- Besoin de fonctionnalités iOS spécifiques

### 💡 Approche hybride

Beaucoup d'entreprises créent **les deux** :
- PWA pour le web
- App native pour iOS/Android

Exemples : Twitter, Instagram, Spotify

---

## Outils et ressources

### Générateurs de PWA

**Workbox (par Google)**
Librairie pour simplifier les Service Workers :
```bash
npm install workbox-cli --global
workbox wizard
```

**PWA Builder**
Outil en ligne pour générer manifest et Service Worker :
https://www.pwabuilder.com/

### Frameworks avec support PWA intégré

- **Next.js** (React) : Plugin next-pwa
- **Nuxt.js** (Vue) : Module @nuxtjs/pwa
- **Angular** : @angular/pwa
- **Vite** : Plugin vite-plugin-pwa

### Outils de test

- **Lighthouse** : Audit PWA intégré à Chrome
- **PWA Testing Tool** : https://www.pwabuilder.com/
- **Can I Use** : Vérifier la compatibilité

---

## Compatibilité navigateur

### Excellent support

- ✅ **Chrome** (Android et Desktop) : Support complet
- ✅ **Edge** : Support complet
- ✅ **Firefox** : Support complet
- ✅ **Samsung Internet** : Support complet

### Support partiel

⚠️ **Safari** (iOS et macOS) :
- Service Workers : ✅
- Manifest : ✅
- Installation : ✅
- Notifications push : ❌ (iOS uniquement)
- Background sync : ❌

### Vérifier le support

```javascript
// Service Workers
if ('serviceWorker' in navigator) {
  console.log('Service Workers supportés');
}

// Notifications
if ('Notification' in window) {
  console.log('Notifications supportées');
}

// Background Sync
if ('sync' in navigator.serviceWorker) {
  console.log('Background Sync supporté');
}
```

---

## Bonnes pratiques

### 1. Toujours servir en HTTPS

```
✅ https://monsite.com
❌ http://monsite.com
```

### 2. Stratégie de cache adaptée

```javascript
// Ressources statiques : Cache First
// API/Données : Network First
// Images : Cache First avec fallback
```

### 3. Expérience hors ligne soignée

```javascript
// Page hors ligne personnalisée
self.addEventListener('fetch', event => {
  event.respondWith(
    fetch(event.request).catch(() => {
      return caches.match('/offline.html');
    })
  );
});
```

### 4. Tester sur vrais appareils

- Tester sur plusieurs navigateurs
- Tester sur mobile et desktop
- Tester hors ligne
- Tester l'installation

### 5. Optimiser les performances

```javascript
// Précharger les ressources critiques
<link rel="preload" href="style.css" as="style">
<link rel="preload" href="app.js" as="script">

// Lazy loading des images
<img loading="lazy" src="image.jpg" alt="Description">
```

---

## Points clés à retenir

1. **PWA = Site web amélioré** : Installation, hors ligne, notifications
2. **Trois piliers** : HTTPS, Service Workers, Web App Manifest
3. **Service Workers** : Cache, hors ligne, notifications en arrière-plan
4. **Manifest** : Métadonnées pour l'installation (nom, icônes, couleurs)
5. **Installation facile** : Pas d'App Store, installation en un clic
6. **Expérience utilisateur** : Rapide, fluide, comme une app native
7. **Un seul code** : Fonctionne partout (web, mobile, desktop)
8. **Limitations iOS** : Notifications push non supportées
9. **Lighthouse** : Outil d'audit pour tester votre PWA
10. **Progressive** : Amélioration progressive, fonctionne pour tous

---

## Pour aller plus loin

Les PWA représentent l'avenir du web en combinant le meilleur des applications web et natives. Elles sont particulièrement adaptées aux projets où vous voulez :
- Une expérience utilisateur optimale
- Un développement multiplateforme simplifié
- Des coûts de développement réduits
- Une distribution sans App Store

### Ressources recommandées :

- **web.dev/progressive-web-apps** : Guide complet par Google
- **MDN PWA** : Documentation technique détaillée
- **PWA Builder** : Générateur et outils
- **Workbox** : Librairie de Service Workers
- **PWA Stats** : Études de cas et statistiques

> 🎯 **Prochaine étape** : Transformez un projet web existant en PWA ! Commencez simplement en ajoutant un manifest et un Service Worker basique pour le mode hors ligne.

⏭️ [Parcours d'apprentissage](/08-ecosysteme-javascript-moderne/05-parcours-apprentissage/README.md)
