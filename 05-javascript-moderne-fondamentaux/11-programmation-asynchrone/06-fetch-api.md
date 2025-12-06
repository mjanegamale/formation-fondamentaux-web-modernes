🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.11.6 - Fetch API : requêtes HTTP modernes 🆕

## Introduction

L'**API Fetch** est l'outil moderne pour faire des **requêtes HTTP** en JavaScript. Elle permet de communiquer avec des serveurs et des APIs pour :
- Récupérer des données (GET)
- Envoyer des données (POST)
- Mettre à jour des données (PUT)
- Supprimer des données (DELETE)

Fetch remplace l'ancienne API `XMLHttpRequest` (XHR) avec une syntaxe **simple**, **moderne** et basée sur les **Promises**. Elle fonctionne parfaitement avec `async/await` que nous venons d'apprendre.

## Pourquoi Fetch ?

### Avant : XMLHttpRequest (l'ancienne méthode ❌)

```javascript
// ❌ ANCIENNE MÉTHODE : XMLHttpRequest (verbeux et complexe)
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/users');

xhr.onload = function() {
    if (xhr.status === 200) {
        const data = JSON.parse(xhr.responseText);
        console.log(data);
    } else {
        console.error('Erreur');
    }
};

xhr.onerror = function() {
    console.error('Erreur réseau');
};

xhr.send();

// Compliqué, verbeux, difficile à lire
```

### Maintenant : Fetch (moderne ✅)

```javascript
// ✅ MODERNE : Fetch API (simple et clair)
fetch('https://api.example.com/users')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Erreur:', error));

// Simple, basé sur les Promises, facile à lire
```

### Avec async/await (encore mieux ✅)

```javascript
// ✅ ENCORE MIEUX : Fetch avec async/await
async function chargerUtilisateurs() {
    try {
        const response = await fetch('https://api.example.com/users');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Erreur:', error);
    }
}

chargerUtilisateurs();
```

## Syntaxe de base

```javascript
fetch(url, options)
    .then(response => {
        // Traiter la réponse
    })
    .catch(error => {
        // Gérer les erreurs
    });
```

- **`url`** : L'URL à laquelle faire la requête
- **`options`** : Objet de configuration (optionnel, méthode, headers, body, etc.)

## Requête GET simple

### Exemple de base

```javascript
fetch('https://jsonplaceholder.typicode.com/users/1')
    .then(response => response.json())
    .then(user => {
        console.log('Nom:', user.name);
        console.log('Email:', user.email);
    })
    .catch(error => {
        console.error('Erreur:', error);
    });
```

### Avec async/await (recommandé)

```javascript
async function recupererUtilisateur(id) {
    try {
        const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
        const user = await response.json();

        console.log('Nom:', user.name);
        console.log('Email:', user.email);

        return user;
    } catch (error) {
        console.error('Erreur:', error);
    }
}

recupererUtilisateur(1);
```

### Afficher dans une page

```html
<button id="charger">Charger utilisateur</button>
<div id="resultat"></div>
```

```javascript
const bouton = document.getElementById('charger');
const resultat = document.getElementById('resultat');

bouton.addEventListener('click', async () => {
    try {
        resultat.textContent = 'Chargement...';

        const response = await fetch('https://jsonplaceholder.typicode.com/users/1');
        const user = await response.json();

        resultat.innerHTML = `
            <h3>${user.name}</h3>
            <p>Email: ${user.email}</p>
            <p>Téléphone: ${user.phone}</p>
        `;
    } catch (error) {
        resultat.textContent = 'Erreur de chargement';
        console.error(error);
    }
});
```

## L'objet Response

Quand vous faites un `fetch()`, vous recevez un objet **Response** :

```javascript
const response = await fetch('https://api.example.com/data');

console.log(response.status);      // 200, 404, 500, etc.
console.log(response.statusText);  // "OK", "Not Found", etc.
console.log(response.ok);          // true si status 200-299
console.log(response.headers);     // Headers de la réponse
console.log(response.url);         // URL finale (après redirections)
```

### Propriétés importantes

| Propriété | Description | Exemple |
|-----------|-------------|---------|
| `status` | Code de statut HTTP | `200`, `404`, `500` |
| `statusText` | Texte du statut | `"OK"`, `"Not Found"` |
| `ok` | `true` si status 200-299 | `true` ou `false` |
| `headers` | En-têtes de réponse | `Headers` object |
| `url` | URL de la réponse | `"https://..."` |

## Méthodes de lecture du corps (body)

Une fois que vous avez la Response, vous devez extraire les données :

### .json() - Données JSON

```javascript
const response = await fetch('https://api.example.com/users');
const data = await response.json(); // Parse JSON automatiquement

console.log(data); // Objet ou tableau JavaScript
```

### .text() - Texte brut

```javascript
const response = await fetch('https://example.com/fichier.txt');
const text = await response.text();

console.log(text); // String
```

### .blob() - Fichiers binaires (images, etc.)

```javascript
const response = await fetch('https://example.com/image.jpg');
const blob = await response.blob();

const imageUrl = URL.createObjectURL(blob);
document.querySelector('img').src = imageUrl;
```

### .arrayBuffer() - Données binaires brutes

```javascript
const response = await fetch('https://example.com/file.bin');
const buffer = await response.arrayBuffer();
```

### .formData() - Données de formulaire

```javascript
const response = await fetch('https://example.com/form-data');
const formData = await response.formData();
```

## Vérifier le statut de la réponse

### ⚠️ Important : Fetch ne rejette pas sur les erreurs HTTP !

```javascript
// ⚠️ ATTENTION : Ceci ne marche pas comme prévu
try {
    const response = await fetch('https://api.example.com/404');
    const data = await response.json();
} catch (error) {
    // Cette erreur ne se déclenchera PAS pour un 404 !
    console.error(error);
}
```

**Pourquoi ?** Fetch ne considère pas les erreurs HTTP (404, 500, etc.) comme des erreurs. Il ne rejette que pour les **erreurs réseau** (pas de connexion, etc.).

### ✅ Solution : Vérifier response.ok

```javascript
async function recupererDonnees() {
    try {
        const response = await fetch('https://api.example.com/data');

        // Vérifier si la requête a réussi
        if (!response.ok) {
            throw new Error(`Erreur HTTP: ${response.status}`);
        }

        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Erreur:', error);
    }
}
```

### Pattern de vérification complet

```javascript
async function fetchAvecVerification(url) {
    try {
        const response = await fetch(url);

        if (!response.ok) {
            // Créer une erreur détaillée
            const errorText = await response.text();
            throw new Error(`${response.status} ${response.statusText}: ${errorText}`);
        }

        return await response.json();
    } catch (error) {
        console.error('Erreur lors de la requête:', error.message);
        throw error;
    }
}

// Utilisation
try {
    const data = await fetchAvecVerification('https://api.example.com/data');
    console.log(data);
} catch (error) {
    alert('Impossible de charger les données');
}
```

## Requête POST - Envoyer des données

### Syntaxe de base

```javascript
fetch(url, {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
})
```

### Exemple : Créer un utilisateur

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

        if (!response.ok) {
            throw new Error('Erreur lors de la création');
        }

        const nouveauUtilisateur = await response.json();
        console.log('Utilisateur créé:', nouveauUtilisateur);

        return nouveauUtilisateur;
    } catch (error) {
        console.error('Erreur:', error);
    }
}

creerUtilisateur('Alice', 'alice@example.com');
```

### Exemple : Formulaire de contact

```html
<form id="formContact">
    <input type="text" id="nom" placeholder="Nom" required>
    <input type="email" id="email" placeholder="Email" required>
    <textarea id="message" placeholder="Message" required></textarea>
    <button type="submit">Envoyer</button>
</form>
<p id="statut"></p>
```

```javascript
const form = document.getElementById('formContact');
const statut = document.getElementById('statut');

form.addEventListener('submit', async (event) => {
    event.preventDefault();

    const nom = document.getElementById('nom').value;
    const email = document.getElementById('email').value;
    const message = document.getElementById('message').value;

    statut.textContent = 'Envoi en cours...';

    try {
        const response = await fetch('https://api.example.com/contact', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ nom, email, message })
        });

        if (!response.ok) {
            throw new Error('Erreur d\'envoi');
        }

        const resultat = await response.json();

        statut.textContent = '✅ Message envoyé avec succès !';
        statut.style.color = 'green';
        form.reset();

    } catch (error) {
        statut.textContent = '❌ Erreur : ' + error.message;
        statut.style.color = 'red';
    }
});
```

## Autres méthodes HTTP

### PUT - Mettre à jour

```javascript
async function mettreAJourUtilisateur(id, modifications) {
    try {
        const response = await fetch(`https://api.example.com/users/${id}`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(modifications)
        });

        if (!response.ok) {
            throw new Error('Erreur de mise à jour');
        }

        const utilisateurMisAJour = await response.json();
        console.log('Utilisateur mis à jour:', utilisateurMisAJour);

        return utilisateurMisAJour;
    } catch (error) {
        console.error('Erreur:', error);
    }
}

mettreAJourUtilisateur(1, { name: 'Alice Dupont', email: 'alice.dupont@example.com' });
```

### PATCH - Mise à jour partielle

```javascript
async function modifierEmail(id, nouvelEmail) {
    try {
        const response = await fetch(`https://api.example.com/users/${id}`, {
            method: 'PATCH',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ email: nouvelEmail })
        });

        if (!response.ok) {
            throw new Error('Erreur de modification');
        }

        const resultat = await response.json();
        console.log('Email modifié:', resultat);

        return resultat;
    } catch (error) {
        console.error('Erreur:', error);
    }
}

modifierEmail(1, 'nouveau@example.com');
```

### DELETE - Supprimer

```javascript
async function supprimerUtilisateur(id) {
    try {
        const response = await fetch(`https://api.example.com/users/${id}`, {
            method: 'DELETE'
        });

        if (!response.ok) {
            throw new Error('Erreur de suppression');
        }

        console.log('Utilisateur supprimé avec succès');
        return true;
    } catch (error) {
        console.error('Erreur:', error);
        return false;
    }
}

supprimerUtilisateur(1);
```

## Headers (en-têtes)

### Ajouter des headers personnalisés

```javascript
const response = await fetch('https://api.example.com/data', {
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer TOKEN_SECRET',
        'X-Custom-Header': 'valeur'
    }
});
```

### Headers communs

| Header | Description | Exemple |
|--------|-------------|---------|
| `Content-Type` | Type de contenu envoyé | `'application/json'` |
| `Authorization` | Token d'authentification | `'Bearer abc123'` |
| `Accept` | Type de contenu attendu | `'application/json'` |
| `Accept-Language` | Langue préférée | `'fr-FR'` |

### Lire les headers de la réponse

```javascript
const response = await fetch('https://api.example.com/data');

// Lire un header spécifique
const contentType = response.headers.get('Content-Type');
console.log('Type de contenu:', contentType);

// Lister tous les headers
for (let [key, value] of response.headers) {
    console.log(`${key}: ${value}`);
}
```

## Exemple complet : Application CRUD

```html
<div id="app">
    <h2>Gestion des utilisateurs</h2>

    <!-- Formulaire d'ajout -->
    <form id="formAjout">
        <input type="text" id="nom" placeholder="Nom" required>
        <input type="email" id="email" placeholder="Email" required>
        <button type="submit">Ajouter</button>
    </form>

    <!-- Liste des utilisateurs -->
    <ul id="listeUtilisateurs"></ul>

    <!-- Messages -->
    <p id="message"></p>
</div>
```

```javascript
const API_URL = 'https://jsonplaceholder.typicode.com/users';
const listeUtilisateurs = document.getElementById('listeUtilisateurs');
const formAjout = document.getElementById('formAjout');
const message = document.getElementById('message');

// 1. READ - Charger tous les utilisateurs (GET)
async function chargerUtilisateurs() {
    try {
        message.textContent = 'Chargement...';

        const response = await fetch(API_URL);

        if (!response.ok) {
            throw new Error('Erreur de chargement');
        }

        const utilisateurs = await response.json();
        afficherUtilisateurs(utilisateurs.slice(0, 5)); // Limiter à 5

        message.textContent = '';
    } catch (error) {
        message.textContent = '❌ ' + error.message;
    }
}

// Afficher les utilisateurs
function afficherUtilisateurs(utilisateurs) {
    listeUtilisateurs.innerHTML = '';

    utilisateurs.forEach(user => {
        const li = document.createElement('li');
        li.innerHTML = `
            <strong>${user.name}</strong> - ${user.email}
            <button onclick="supprimerUtilisateur(${user.id})">Supprimer</button>
            <button onclick="modifierUtilisateur(${user.id})">Modifier</button>
        `;
        listeUtilisateurs.appendChild(li);
    });
}

// 2. CREATE - Ajouter un utilisateur (POST)
formAjout.addEventListener('submit', async (event) => {
    event.preventDefault();

    const nom = document.getElementById('nom').value;
    const email = document.getElementById('email').value;

    try {
        message.textContent = 'Ajout en cours...';

        const response = await fetch(API_URL, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ name: nom, email: email })
        });

        if (!response.ok) {
            throw new Error('Erreur lors de l\'ajout');
        }

        const nouveauUtilisateur = await response.json();
        console.log('Utilisateur ajouté:', nouveauUtilisateur);

        message.textContent = '✅ Utilisateur ajouté !';
        message.style.color = 'green';

        formAjout.reset();
        chargerUtilisateurs(); // Recharger la liste

    } catch (error) {
        message.textContent = '❌ ' + error.message;
        message.style.color = 'red';
    }
});

// 3. UPDATE - Modifier un utilisateur (PUT)
async function modifierUtilisateur(id) {
    const nouveauNom = prompt('Nouveau nom:');
    const nouvelEmail = prompt('Nouvel email:');

    if (!nouveauNom || !nouvelEmail) return;

    try {
        message.textContent = 'Modification en cours...';

        const response = await fetch(`${API_URL}/${id}`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ name: nouveauNom, email: nouvelEmail })
        });

        if (!response.ok) {
            throw new Error('Erreur de modification');
        }

        message.textContent = '✅ Utilisateur modifié !';
        message.style.color = 'green';

        chargerUtilisateurs();

    } catch (error) {
        message.textContent = '❌ ' + error.message;
        message.style.color = 'red';
    }
}

// 4. DELETE - Supprimer un utilisateur (DELETE)
async function supprimerUtilisateur(id) {
    if (!confirm('Voulez-vous vraiment supprimer cet utilisateur ?')) {
        return;
    }

    try {
        message.textContent = 'Suppression en cours...';

        const response = await fetch(`${API_URL}/${id}`, {
            method: 'DELETE'
        });

        if (!response.ok) {
            throw new Error('Erreur de suppression');
        }

        message.textContent = '✅ Utilisateur supprimé !';
        message.style.color = 'green';

        chargerUtilisateurs();

    } catch (error) {
        message.textContent = '❌ ' + error.message;
        message.style.color = 'red';
    }
}

// Charger les utilisateurs au démarrage
chargerUtilisateurs();
```

## Envoyer des fichiers (FormData)

### Upload d'un fichier

```html
<input type="file" id="fichier">
<button id="upload">Uploader</button>
<p id="progression"></p>
```

```javascript
const inputFichier = document.getElementById('fichier');
const boutonUpload = document.getElementById('upload');
const progression = document.getElementById('progression');

boutonUpload.addEventListener('click', async () => {
    const fichier = inputFichier.files[0];

    if (!fichier) {
        alert('Sélectionnez un fichier');
        return;
    }

    // Créer un FormData
    const formData = new FormData();
    formData.append('file', fichier);
    formData.append('nom', 'Mon fichier');

    try {
        progression.textContent = 'Upload en cours...';

        const response = await fetch('https://api.example.com/upload', {
            method: 'POST',
            body: formData // Pas besoin de Content-Type, fetch le gère automatiquement
        });

        if (!response.ok) {
            throw new Error('Erreur d\'upload');
        }

        const resultat = await response.json();

        progression.textContent = '✅ Fichier uploadé : ' + resultat.url;
        progression.style.color = 'green';

    } catch (error) {
        progression.textContent = '❌ Erreur : ' + error.message;
        progression.style.color = 'red';
    }
});
```

## Options avancées

### Timeout (annulation automatique)

```javascript
async function fetchAvecTimeout(url, timeout = 5000) {
    // Créer un AbortController
    const controller = new AbortController();
    const signal = controller.signal;

    // Créer un timer pour annuler après X ms
    const timeoutId = setTimeout(() => controller.abort(), timeout);

    try {
        const response = await fetch(url, { signal });
        clearTimeout(timeoutId);

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        return await response.json();
    } catch (error) {
        clearTimeout(timeoutId);

        if (error.name === 'AbortError') {
            throw new Error('Requête annulée (timeout)');
        }

        throw error;
    }
}

// Utilisation
try {
    const data = await fetchAvecTimeout('https://api.example.com/slow', 3000);
    console.log(data);
} catch (error) {
    console.error('Erreur:', error.message);
}
```

### Mode CORS

```javascript
const response = await fetch('https://api.example.com/data', {
    mode: 'cors', // 'cors', 'no-cors', 'same-origin'
    credentials: 'include' // Envoyer les cookies
});
```

### Cache

```javascript
const response = await fetch('https://api.example.com/data', {
    cache: 'no-cache' // 'default', 'no-cache', 'reload', 'force-cache', 'only-if-cached'
});
```

## Pièges courants

### Piège 1 : Oublier await sur .json()

```javascript
// ❌ ERREUR : Oublier await
async function mauvais() {
    const response = await fetch(url);
    const data = response.json(); // Retourne une Promise, pas les données !
    console.log(data.name); // undefined
}

// ✅ CORRECT
async function correct() {
    const response = await fetch(url);
    const data = await response.json(); // Bien attendre
    console.log(data.name); // OK
}
```

### Piège 2 : Ne pas vérifier response.ok

```javascript
// ❌ DANGEREUX : Pas de vérification
async function dangereux() {
    const response = await fetch(url);
    const data = await response.json(); // Peut échouer si 404/500
    return data;
}

// ✅ SÛR
async function sur() {
    const response = await fetch(url);

    if (!response.ok) {
        throw new Error(`Erreur: ${response.status}`);
    }

    const data = await response.json();
    return data;
}
```

### Piège 3 : Appeler .json() deux fois

```javascript
// ❌ ERREUR : .json() ne peut être appelé qu'une fois
async function mauvais() {
    const response = await fetch(url);
    const data1 = await response.json();
    const data2 = await response.json(); // ERREUR: body already used
}

// ✅ CORRECT : Stocker le résultat
async function correct() {
    const response = await fetch(url);
    const data = await response.json();

    // Utiliser data plusieurs fois
    console.log(data);
    afficher(data);
}
```

### Piège 4 : Oublier JSON.stringify()

```javascript
// ❌ ERREUR : Envoyer un objet directement
fetch(url, {
    method: 'POST',
    body: { name: 'Alice' } // ERREUR: [object Object]
});

// ✅ CORRECT : Stringifier l'objet
fetch(url, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name: 'Alice' })
});
```

## Bonnes pratiques

### ✅ 1. Toujours vérifier response.ok

```javascript
async function fetchSafe(url) {
    const response = await fetch(url);

    if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }

    return response.json();
}
```

### ✅ 2. Créer une fonction wrapper réutilisable

```javascript
async function api(url, options = {}) {
    try {
        const response = await fetch(url, {
            headers: {
                'Content-Type': 'application/json',
                ...options.headers
            },
            ...options
        });

        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }

        return await response.json();
    } catch (error) {
        console.error('Erreur API:', error);
        throw error;
    }
}

// Utilisation simplifiée
const users = await api('/api/users');
const newUser = await api('/api/users', {
    method: 'POST',
    body: JSON.stringify({ name: 'Alice' })
});
```

### ✅ 3. Gérer le loading et les erreurs dans l'UI

```javascript
async function chargerDonnees() {
    const spinner = document.getElementById('spinner');
    const erreur = document.getElementById('erreur');
    const contenu = document.getElementById('contenu');

    try {
        // Afficher le spinner
        spinner.style.display = 'block';
        erreur.style.display = 'none';

        const response = await fetch('/api/data');

        if (!response.ok) {
            throw new Error('Erreur de chargement');
        }

        const data = await response.json();

        // Afficher les données
        contenu.innerHTML = afficherData(data);

    } catch (error) {
        // Afficher l'erreur
        erreur.textContent = error.message;
        erreur.style.display = 'block';

    } finally {
        // Toujours masquer le spinner
        spinner.style.display = 'none';
    }
}
```

### ✅ 4. Utiliser des constantes pour les URLs

```javascript
const API_BASE = 'https://api.example.com';
const ENDPOINTS = {
    users: `${API_BASE}/users`,
    posts: `${API_BASE}/posts`,
    comments: `${API_BASE}/comments`
};

// Utilisation
const users = await fetch(ENDPOINTS.users).then(r => r.json());
```

### ✅ 5. Ajouter un timeout

```javascript
async function fetchAvecTimeout(url, timeout = 5000) {
    const controller = new AbortController();

    const timeoutId = setTimeout(() => controller.abort(), timeout);

    try {
        const response = await fetch(url, { signal: controller.signal });
        clearTimeout(timeoutId);
        return response;
    } catch (error) {
        clearTimeout(timeoutId);
        throw error;
    }
}
```

## Ce qu'il faut retenir

✅ **Fetch** est l'API moderne pour les requêtes HTTP

✅ **Retourne une Promise** : utilisable avec .then() ou async/await

✅ **GET par défaut** : `fetch(url)` fait une requête GET

✅ **POST/PUT/DELETE** : spécifier `method` dans les options

✅ **response.ok** : vérifier TOUJOURS le statut de la réponse

✅ **response.json()** : parser le JSON (retourne une Promise)

✅ **Headers** : Content-Type, Authorization, etc.

✅ **FormData** : pour uploader des fichiers

✅ **Fetch ne rejette que sur erreur réseau** : pas sur 404/500

✅ **Async/await recommandé** : plus lisible que .then()

## Dans la prochaine leçon

Félicitations ! Vous maîtrisez maintenant la programmation asynchrone en JavaScript : callbacks, Promises, async/await, et Fetch API.

Dans la prochaine leçon, nous explorerons **la gestion d'erreurs avancée** en JavaScript.

Vous découvrirez :
- Les différents types d'erreurs
- Comment créer des erreurs personnalisées
- try/catch avancé
- Le débogage efficace
- Les bonnes pratiques de gestion d'erreurs

---


⏭️ [Gestion d'erreurs avec try/catch en async](/05-javascript-moderne-fondamentaux/11-programmation-asynchrone/07-gestion-erreurs-async.md)
