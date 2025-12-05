🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.4.2 APIs modernes : Fetch, Storage, Geolocation 🆕

## Introduction

Les navigateurs modernes offrent de nombreuses **APIs** (Application Programming Interfaces) qui permettent à JavaScript d'interagir avec le navigateur et l'environnement de l'utilisateur. Ces APIs sont des outils intégrés qui donnent accès à des fonctionnalités puissantes sans avoir besoin de bibliothèques externes.

> 💡 **Une API web**, c'est un ensemble de fonctions JavaScript fournies par le navigateur pour réaliser des tâches spécifiques : récupérer des données sur Internet, stocker des informations localement, accéder à la position géographique, etc.

Dans ce chapitre, nous allons explorer trois APIs essentielles du web moderne.

---

## 1. Fetch API : Récupérer des données sur Internet

### Qu'est-ce que Fetch ?

**Fetch** est l'API moderne pour effectuer des requêtes HTTP en JavaScript. Elle remplace l'ancienne méthode `XMLHttpRequest` (XHR) qui était complexe et difficile à utiliser.

Fetch permet de :
- Récupérer des données depuis un serveur (API REST, fichiers JSON, etc.)
- Envoyer des données vers un serveur
- Télécharger des images, des fichiers
- Communiquer avec des services externes

### Syntaxe de base

```javascript
fetch(url)
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Erreur:', error);
  });
```

### Exemple simple : Récupérer des données

```javascript
// Récupérer une liste d'utilisateurs depuis une API
fetch('https://jsonplaceholder.typicode.com/users')
  .then(response => {
    // Vérifier que la requête a réussi
    if (!response.ok) {
      throw new Error('Erreur réseau');
    }
    return response.json();
  })
  .then(users => {
    console.log('Utilisateurs récupérés:', users);
    // Afficher les noms
    users.forEach(user => {
      console.log(user.name);
    });
  })
  .catch(error => {
    console.error('Erreur lors de la récupération:', error);
  });
```

### Avec async/await (syntaxe moderne)

```javascript
async function recupererUtilisateurs() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');

    if (!response.ok) {
      throw new Error('Erreur réseau');
    }

    const users = await response.json();
    console.log('Utilisateurs:', users);
    return users;

  } catch (error) {
    console.error('Erreur:', error);
  }
}

recupererUtilisateurs();
```

### Envoyer des données (POST)

```javascript
async function creerUtilisateur(nom, email) {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        name: nom,
        email: email
      })
    });

    const data = await response.json();
    console.log('Utilisateur créé:', data);
    return data;

  } catch (error) {
    console.error('Erreur:', error);
  }
}

creerUtilisateur('Alice Dupont', 'alice@example.com');
```

### Options de configuration Fetch

```javascript
fetch(url, {
  method: 'GET',           // GET, POST, PUT, DELETE, PATCH
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer token123'
  },
  body: JSON.stringify(data),  // Données à envoyer (POST/PUT)
  mode: 'cors',            // cors, no-cors, same-origin
  credentials: 'same-origin'  // same-origin, include, omit
});
```

### Gérer différents types de réponses

```javascript
// JSON (le plus courant)
const data = await response.json();

// Texte brut
const text = await response.text();

// Blob (images, fichiers)
const blob = await response.blob();

// FormData
const formData = await response.formData();
```

### Exemple pratique : Afficher des articles

```javascript
async function afficherArticles() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=5');
    const articles = await response.json();

    const container = document.getElementById('articles');

    articles.forEach(article => {
      const articleElement = document.createElement('div');
      articleElement.innerHTML = `
        <h3>${article.title}</h3>
        <p>${article.body}</p>
      `;
      container.appendChild(articleElement);
    });

  } catch (error) {
    console.error('Erreur de chargement:', error);
  }
}

afficherArticles();
```

---

## 2. Web Storage API : Stocker des données localement

### Qu'est-ce que Web Storage ?

Web Storage permet de **stocker des données directement dans le navigateur de l'utilisateur**. Ces données persistent même après la fermeture de la page (pour localStorage) ou sont disponibles pendant la session (pour sessionStorage).

Il existe deux types de stockage :

1. **localStorage** : Les données persistent indéfiniment
2. **sessionStorage** : Les données sont supprimées à la fermeture de l'onglet

### localStorage : Stockage permanent

#### Méthodes de base

```javascript
// Stocker une valeur
localStorage.setItem('nom', 'Alice');
localStorage.setItem('age', '30');

// Récupérer une valeur
const nom = localStorage.getItem('nom');
console.log(nom);  // "Alice"

// Supprimer une valeur
localStorage.removeItem('age');

// Tout supprimer
localStorage.clear();

// Vérifier le nombre d'éléments
console.log(localStorage.length);
```

#### Stocker des objets (avec JSON)

localStorage ne peut stocker que des chaînes de caractères. Pour les objets, il faut les convertir :

```javascript
// Stocker un objet
const utilisateur = {
  nom: 'Alice',
  age: 30,
  ville: 'Paris'
};

localStorage.setItem('utilisateur', JSON.stringify(utilisateur));

// Récupérer l'objet
const userJSON = localStorage.getItem('utilisateur');
const user = JSON.parse(userJSON);
console.log(user.nom);  // "Alice"
```

#### Exemple pratique : Sauvegarder les préférences

```javascript
// Sauvegarder le thème choisi par l'utilisateur
function definirTheme(theme) {
  localStorage.setItem('theme', theme);
  document.body.className = theme;
}

// Charger le thème au démarrage
function chargerTheme() {
  const theme = localStorage.getItem('theme') || 'clair';
  document.body.className = theme;
}

// Utilisation
chargerTheme();  // Au chargement de la page

document.getElementById('btnThemeSombre').addEventListener('click', () => {
  definirTheme('sombre');
});

document.getElementById('btnThemeClair').addEventListener('click', () => {
  definirTheme('clair');
});
```

#### Exemple : Liste de tâches persistante

```javascript
class GestionnaireTaches {
  constructor() {
    this.taches = this.chargerTaches();
  }

  chargerTaches() {
    const tachesJSON = localStorage.getItem('taches');
    return tachesJSON ? JSON.parse(tachesJSON) : [];
  }

  sauvegarderTaches() {
    localStorage.setItem('taches', JSON.stringify(this.taches));
  }

  ajouterTache(texte) {
    this.taches.push({
      id: Date.now(),
      texte: texte,
      terminee: false
    });
    this.sauvegarderTaches();
  }

  supprimerTache(id) {
    this.taches = this.taches.filter(t => t.id !== id);
    this.sauvegarderTaches();
  }

  obtenirTaches() {
    return this.taches;
  }
}

// Utilisation
const gestionnaire = new GestionnaireTaches();
gestionnaire.ajouterTache('Apprendre JavaScript');
console.log(gestionnaire.obtenirTaches());
```

### sessionStorage : Stockage temporaire

sessionStorage fonctionne **exactement comme localStorage**, mais les données sont supprimées à la fermeture de l'onglet :

```javascript
// Stocker temporairement
sessionStorage.setItem('panier', JSON.stringify(articles));

// Récupérer
const panier = JSON.parse(sessionStorage.getItem('panier'));

// Les données disparaissent quand l'onglet est fermé
```

**Cas d'usage de sessionStorage :**
- Formulaires en plusieurs étapes
- Paniers temporaires
- États temporaires de l'application
- Données de navigation

### Limites et précautions

#### Capacité de stockage
- Environ **5-10 MB** par domaine (selon le navigateur)
- Vérifier avant de stocker de grandes quantités

```javascript
try {
  localStorage.setItem('cle', valeur);
} catch (e) {
  if (e.name === 'QuotaExceededError') {
    console.error('Stockage plein !');
  }
}
```

#### Sécurité
- ⚠️ **Ne jamais stocker** de données sensibles (mots de passe, tokens, informations bancaires)
- Les données sont visibles en clair dans les DevTools
- Accessibles par tout script JavaScript du domaine

```javascript
// ❌ MAUVAIS
localStorage.setItem('motDePasse', 'secret123');

// ✅ BON
// Stocker seulement des préférences, cache, états UI
localStorage.setItem('langue', 'fr');
localStorage.setItem('accordeonOuvert', 'true');
```

---

## 3. Geolocation API : Accéder à la position de l'utilisateur

### Qu'est-ce que Geolocation ?

L'API **Geolocation** permet d'obtenir la position géographique de l'utilisateur (latitude, longitude). Elle nécessite l'**autorisation explicite** de l'utilisateur pour des raisons de confidentialité.

### Vérifier la disponibilité

```javascript
if ('geolocation' in navigator) {
  console.log('Geolocation disponible');
} else {
  console.log('Geolocation non supportée');
}
```

### Obtenir la position actuelle

```javascript
navigator.geolocation.getCurrentPosition(
  // Succès
  (position) => {
    const lat = position.coords.latitude;
    const lon = position.coords.longitude;
    console.log(`Position: ${lat}, ${lon}`);
  },
  // Erreur
  (error) => {
    console.error('Erreur:', error.message);
  }
);
```

### Exemple complet avec gestion d'erreurs

```javascript
function obtenirPosition() {
  // Vérifier que l'API est disponible
  if (!('geolocation' in navigator)) {
    alert('La géolocalisation n\'est pas supportée par votre navigateur');
    return;
  }

  // Afficher un message de chargement
  console.log('Récupération de votre position...');

  navigator.geolocation.getCurrentPosition(
    // Callback de succès
    (position) => {
      const coords = {
        latitude: position.coords.latitude,
        longitude: position.coords.longitude,
        precision: position.coords.accuracy,
        altitude: position.coords.altitude,
        vitesse: position.coords.speed
      };

      console.log('Position obtenue:', coords);
      afficherSurCarte(coords.latitude, coords.longitude);
    },

    // Callback d'erreur
    (error) => {
      switch(error.code) {
        case error.PERMISSION_DENIED:
          console.error('Permission refusée par l\'utilisateur');
          break;
        case error.POSITION_UNAVAILABLE:
          console.error('Position indisponible');
          break;
        case error.TIMEOUT:
          console.error('Délai d\'attente dépassé');
          break;
        default:
          console.error('Erreur inconnue');
      }
    },

    // Options
    {
      enableHighAccuracy: true,  // Précision maximale (utilise GPS si disponible)
      timeout: 5000,             // Temps max d'attente (5 secondes)
      maximumAge: 0              // Ne pas utiliser de position en cache
    }
  );
}

obtenirPosition();
```

### Suivre la position en temps réel

```javascript
let watchId;

function demarrerSuivi() {
  watchId = navigator.geolocation.watchPosition(
    (position) => {
      const lat = position.coords.latitude;
      const lon = position.coords.longitude;
      console.log(`Nouvelle position: ${lat}, ${lon}`);
      mettreAJourCarte(lat, lon);
    },
    (error) => {
      console.error('Erreur de suivi:', error);
    },
    {
      enableHighAccuracy: true,
      maximumAge: 0
    }
  );
}

function arreterSuivi() {
  if (watchId) {
    navigator.geolocation.clearWatch(watchId);
    console.log('Suivi arrêté');
  }
}

// Utilisation
demarrerSuivi();
// ... plus tard
arreterSuivi();
```

### Exemple pratique : Afficher la météo locale

```javascript
async function afficherMeteoLocale() {
  try {
    // 1. Obtenir la position
    const position = await new Promise((resolve, reject) => {
      navigator.geolocation.getCurrentPosition(resolve, reject);
    });

    const lat = position.coords.latitude;
    const lon = position.coords.longitude;

    // 2. Récupérer la météo via une API
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=VOTRE_CLE_API&units=metric&lang=fr`
    );
    const meteo = await response.json();

    // 3. Afficher les informations
    console.log(`Météo à ${meteo.name}:`);
    console.log(`Température: ${meteo.main.temp}°C`);
    console.log(`Conditions: ${meteo.weather[0].description}`);

  } catch (error) {
    console.error('Erreur:', error);
  }
}
```

### Exemple : Calculer la distance entre deux points

```javascript
function calculerDistance(lat1, lon1, lat2, lon2) {
  const R = 6371; // Rayon de la Terre en km
  const dLat = (lat2 - lat1) * Math.PI / 180;
  const dLon = (lon2 - lon1) * Math.PI / 180;

  const a =
    Math.sin(dLat/2) * Math.sin(dLat/2) +
    Math.cos(lat1 * Math.PI / 180) * Math.cos(lat2 * Math.PI / 180) *
    Math.sin(dLon/2) * Math.sin(dLon/2);

  const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
  const distance = R * c;

  return distance.toFixed(2); // Distance en km
}

// Utilisation
navigator.geolocation.getCurrentPosition((position) => {
  const maPosLat = position.coords.latitude;
  const maPosLon = position.coords.longitude;

  // Tour Eiffel : 48.8584, 2.2945
  const distance = calculerDistance(
    maPosLat, maPosLon,
    48.8584, 2.2945
  );

  console.log(`Vous êtes à ${distance} km de la Tour Eiffel`);
});
```

### Considérations importantes

#### 1. Vie privée
- Toujours demander la permission
- Expliquer pourquoi vous avez besoin de la position
- Permettre à l'utilisateur de refuser

```javascript
function demanderLocalisation() {
  // Expliquer d'abord
  const message = "Nous avons besoin de votre position pour afficher les restaurants à proximité.";

  if (confirm(message)) {
    navigator.geolocation.getCurrentPosition(/* ... */);
  }
}
```

#### 2. Précision
- `enableHighAccuracy: true` consomme plus de batterie
- La précision varie selon l'appareil (GPS > WiFi > IP)
- En intérieur, la précision peut être faible

#### 3. Performance
- Ne pas demander la position trop souvent
- Utiliser `maximumAge` pour accepter une position en cache
- Arrêter `watchPosition` quand ce n'est plus nécessaire

---

## Compatibilité et support navigateur

### Fetch API
✅ Supporté par tous les navigateurs modernes (depuis 2015)
- Chrome 42+
- Firefox 39+
- Safari 10.1+
- Edge 14+

Pour les anciens navigateurs, utiliser un polyfill.

### Web Storage
✅ Excellent support (depuis 2009)
- Tous les navigateurs modernes
- Internet Explorer 8+

### Geolocation
✅ Excellent support (depuis 2010)
- Tous les navigateurs modernes
- ⚠️ Nécessite HTTPS (sauf localhost)

```javascript
// Vérifier le support
if ('fetch' in window) { /* Fetch disponible */ }
if ('localStorage' in window) { /* Storage disponible */ }
if ('geolocation' in navigator) { /* Geolocation disponible */ }
```

---

## Comparaison avec les anciennes méthodes

### Fetch vs XMLHttpRequest

```javascript
// ❌ Ancienne méthode (XMLHttpRequest)
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data');
xhr.onload = function() {
  if (xhr.status === 200) {
    const data = JSON.parse(xhr.responseText);
    console.log(data);
  }
};
xhr.onerror = function() {
  console.error('Erreur');
};
xhr.send();

// ✅ Nouvelle méthode (Fetch)
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Erreur:', error));
```

### Storage vs Cookies

**Cookies (ancien)** :
- Envoyés automatiquement avec chaque requête HTTP
- Limités à 4 KB
- Complexes à manipuler

**localStorage/sessionStorage (moderne)** :
- Restent côté client
- 5-10 MB de capacité
- API simple et intuitive

---

## Bonnes pratiques

### 1. Toujours gérer les erreurs

```javascript
// Fetch
try {
  const response = await fetch(url);
  if (!response.ok) throw new Error('Erreur réseau');
  const data = await response.json();
} catch (error) {
  console.error('Erreur:', error);
}

// Storage
try {
  localStorage.setItem('key', value);
} catch (e) {
  console.error('Erreur de stockage:', e);
}

// Geolocation
navigator.geolocation.getCurrentPosition(success, error);
```

### 2. Vérifier la disponibilité

```javascript
if ('fetch' in window && 'localStorage' in window && 'geolocation' in navigator) {
  // Toutes les APIs sont disponibles
} else {
  // Proposer une alternative
}
```

### 3. Optimiser les requêtes

```javascript
// Mettre en cache les résultats
async function obtenirDonneesAvecCache(url) {
  // Vérifier le cache
  const cache = localStorage.getItem(url);
  if (cache) {
    const { data, timestamp } = JSON.parse(cache);
    // Cache valide 5 minutes
    if (Date.now() - timestamp < 5 * 60 * 1000) {
      return data;
    }
  }

  // Sinon, récupérer et mettre en cache
  const response = await fetch(url);
  const data = await response.json();
  localStorage.setItem(url, JSON.stringify({
    data,
    timestamp: Date.now()
  }));
  return data;
}
```

---

## Points clés à retenir

1. **Fetch API** : Méthode moderne pour les requêtes HTTP, remplace XMLHttpRequest
2. **Web Storage** : Stockage local simple (localStorage permanent, sessionStorage temporaire)
3. **Geolocation** : Accès à la position GPS avec permission utilisateur
4. **Toujours gérer les erreurs** : Ces APIs peuvent échouer
5. **Vérifier la compatibilité** : Tester la disponibilité avant utilisation
6. **Respecter la vie privée** : Demander permission, expliquer l'utilisation
7. **Optimiser** : Cache, limiter les requêtes, économiser la batterie

---

## Pour aller plus loin

Ces trois APIs sont les fondations du web moderne, mais il existe de nombreuses autres APIs disponibles :

- **Service Workers** : Pour le mode hors ligne (PWA)
- **Web Notifications** : Notifications système
- **IndexedDB** : Base de données locale
- **Web Audio** : Manipulation audio
- **Canvas / WebGL** : Graphiques 2D/3D
- **WebRTC** : Communication temps réel (vidéo, audio)

Maîtriser Fetch, Storage et Geolocation vous donne une excellente base pour explorer ces APIs plus avancées.

> 🎯 **Prochaine étape** : Pratiquez en créant une application météo qui utilise les trois APIs : Geolocation pour la position, Fetch pour les données météo, et localStorage pour sauvegarder les villes favorites !

⏭️ [Web Components](/08-ecosysteme-javascript-moderne/04-concepts-avances-apercu/03-web-components.md)
