🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.1.4 Debugging Asynchrone (Promises, async/await)

## Introduction

Le code asynchrone est l'un des concepts les plus puissants de JavaScript moderne... mais aussi l'un des plus difficiles à débugger ! Les requêtes API, les timers, les chargements de fichiers : tout ce qui ne s'exécute pas immédiatement est asynchrone.

Dans cette section, nous allons découvrir comment **maîtriser le debugging du code asynchrone** avec les outils modernes des DevTools. Vous allez comprendre pourquoi c'est différent et comment devenir efficace !

---

## Pourquoi le code asynchrone est-il difficile à débugger ?

### Le problème fondamental

Avec du code **synchrone** (normal), tout s'exécute **dans l'ordre** :

```javascript
console.log("1. Début");
const resultat = calculer(); // S'exécute immédiatement
console.log("2. Résultat:", resultat);
console.log("3. Fin");
```

**Ordre d'exécution** : 1 → 2 → 3 (prévisible ✅)

Avec du code **asynchrone**, l'ordre change :

```javascript
console.log("1. Début");
fetch('/api/data').then(resultat => {
  console.log("3. Résultat:", resultat); // S'exécute plus tard !
});
console.log("2. Fin");
```

**Ordre réel** : 1 → 2 → 3 (imprévisible au premier regard ❓)

### Analogie : La cafétéria

**Code synchrone** : Vous faites la queue à la cafétéria. Vous attendez que la personne devant vous soit servie avant d'avancer. Tout le monde attend son tour. C'est lent mais prévisible.

**Code asynchrone** : Vous commandez un café, on vous donne un numéro, et vous attendez ailleurs. Pendant ce temps, d'autres personnes peuvent commander. Quand votre café est prêt, on appelle votre numéro. C'est rapide mais moins prévisible.

### Les défis du debugging asynchrone

1. **Le call stack se "réinitialise"**
   - Une Promise exécute son code plus tard
   - Le call stack original n'existe plus
   - Difficile de savoir d'où vient l'appel

2. **Les erreurs perdent leur contexte**
   ```javascript
   fetch('/api/data')
     .then(response => response.json())
     .then(data => {
       traiterDonnees(data); // ❌ Si erreur ici, le call stack est incomplet
     });
   ```

3. **Plusieurs choses se passent en même temps**
   - Plusieurs Promises en parallèle
   - Difficile de suivre laquelle fait quoi

4. **Les points d'arrêt classiques ne suffisent pas**
   - Le code asynchrone peut "sauter" vos breakpoints

---

## Rappel : Promises et async/await

### Les Promises (vues en 5.11.4)

Une **Promise** représente une valeur qui **sera disponible plus tard** :

```javascript
fetch('/api/users')
  .then(response => response.json())    // Quand la réponse arrive
  .then(users => console.log(users))    // Quand le JSON est parsé
  .catch(error => console.error(error)); // Si une erreur se produit
```

**États d'une Promise** :
- ⏳ **Pending** : En attente (la requête est en cours)
- ✅ **Fulfilled** : Réussie (les données sont arrivées)
- ❌ **Rejected** : Échouée (une erreur s'est produite)

### Async/await (vu en 5.11.5)

**Async/await** est la syntaxe moderne pour travailler avec les Promises :

```javascript
async function chargerUtilisateurs() {
  try {
    const response = await fetch('/api/users'); // Attend la réponse
    const users = await response.json();        // Attend le parsing
    console.log(users);
  } catch (error) {
    console.error(error);
  }
}
```

**Avantages** :
- ✅ Code qui ressemble à du code synchrone
- ✅ Plus lisible et plus facile à comprendre
- ✅ **Beaucoup plus facile à débugger** !

---

## Débugger des Promises

### Problème avec les Promises traditionnelles

```javascript
function chargerUtilisateur(id) {
  fetch(`/api/users/${id}`)
    .then(response => {
      // 🔵 Point d'arrêt ici
      return response.json();
    })
    .then(user => {
      // 🔵 Point d'arrêt ici
      console.log(user);
      return traiterUtilisateur(user);
    })
    .then(result => {
      // 🔵 Point d'arrêt ici
      afficherResultat(result);
    })
    .catch(error => {
      console.error(error);
    });
}
```

**Difficultés** :
- ❌ Call stack incomplet à chaque `.then()`
- ❌ Impossible de voir d'où vient la Promise
- ❌ Difficile de suivre le flux de données

### Solution 1 : Points d'arrêt multiples

Placez un point d'arrêt **dans chaque** `.then()` :

```javascript
fetch('/api/data')
  .then(response => {
    // 🔵 Breakpoint 1 : vérifier la réponse
    console.log('Response:', response);
    return response.json();
  })
  .then(data => {
    // 🔵 Breakpoint 2 : vérifier les données
    console.log('Data:', data);
    return traiter(data);
  })
  .then(resultat => {
    // 🔵 Breakpoint 3 : vérifier le résultat
    console.log('Résultat:', resultat);
  });
```

**Workflow** :
1. Le code s'arrête au breakpoint 1 → vous inspectez `response`
2. Cliquez "Continue" → le code s'arrête au breakpoint 2
3. Vous inspectez `data`, etc.

### Solution 2 : Ajouter des console.log stratégiques

```javascript
fetch('/api/data')
  .then(response => {
    console.log('✅ Réponse reçue:', response.status);
    return response.json();
  })
  .then(data => {
    console.log('✅ Données parsées:', data);
    return traiter(data);
  })
  .catch(error => {
    console.error('❌ Erreur:', error.message);
  });
```

Les emojis et les messages clairs vous aident à suivre le flux !

### Solution 3 : Convertir en async/await

**Le meilleur choix** pour débugger :

```javascript
// ❌ DIFFICILE à débugger (Promises)
function chargerUtilisateur(id) {
  return fetch(`/api/users/${id}`)
    .then(response => response.json())
    .then(user => traiterUtilisateur(user))
    .then(result => afficherResultat(result));
}

// ✅ FACILE à débugger (async/await)
async function chargerUtilisateur(id) {
  const response = await fetch(`/api/users/${id}`);
  const user = await response.json();
  const result = await traiterUtilisateur(user);
  afficherResultat(result);
  return result;
}
```

Avec async/await, vous placez UN SEUL breakpoint et vous avancez ligne par ligne comme du code normal !

---

## Débugger async/await

### Avantages pour le debugging

Async/await transforme le code asynchrone en code qui **ressemble** à du code synchrone :

```javascript
async function exemple() {
  console.log("1. Début");

  const data = await fetch('/api/data');  // 🔵 Un seul breakpoint suffit !
  console.log("2. Données reçues");

  const parsed = await data.json();
  console.log("3. Données parsées");

  const result = await traiter(parsed);
  console.log("4. Traitement terminé");

  return result;
}
```

**Bénéfices** :
- ✅ **Un seul breakpoint** suffit
- ✅ **Step Over (F10)** fonctionne naturellement
- ✅ **Call stack plus clair** et plus complet
- ✅ **Variables accessibles** à chaque étape

### Placement de breakpoint

Placez votre breakpoint **avant** le premier `await` :

```javascript
async function chargerDonnees() {
  // 🔵 Point d'arrêt ici
  const response = await fetch('/api/data');
  const data = await response.json();
  const processed = await traiter(data);
  return processed;
}
```

Ensuite, utilisez **F10 (Step Over)** pour avancer ligne par ligne.

### Exemple pratique : Débugger une requête API

```javascript
async function afficherUtilisateur(id) {
  try {
    // 🔵 Point d'arrêt ici
    console.log('Chargement de l\'utilisateur', id);

    const response = await fetch(`/api/users/${id}`);
    console.log('Réponse reçue:', response.status);

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    const user = await response.json();
    console.log('Utilisateur:', user);

    const element = document.getElementById('user-info');
    element.textContent = `${user.nom} - ${user.email}`;

  } catch (error) {
    console.error('Erreur:', error.message);
    alert('Impossible de charger l\'utilisateur');
  }
}
```

**Workflow de debugging** :
1. Placez le breakpoint à la première ligne
2. Appelez `afficherUtilisateur(42)`
3. Le code s'arrête → Watch : `id = 42`
4. **F10** → `response` est maintenant disponible
5. Inspectez `response.status`, `response.ok`
6. **F10** → `user` est maintenant disponible
7. Inspectez `user.nom`, `user.email`
8. Continuez jusqu'à la fin

### Watch expressions utiles pour async/await

Ajoutez ces expressions dans le panneau Watch :

```javascript
// État de la réponse
response
response?.status
response?.ok

// Données
user
user?.nom
user?.email

// Conditions
response?.ok === false
user === null
user === undefined
```

---

## Débugger les erreurs asynchrones

### Le problème des erreurs non capturées

```javascript
async function chargerDonnees() {
  const data = await fetch('/api/data');
  const json = await data.json();
  // ❌ Si json.items n'existe pas :
  return json.items.map(item => item.nom);
}

chargerDonnees(); // Erreur non capturée !
```

**Conséquence** : L'erreur apparaît dans la console, mais le contexte est perdu.

### Solution : Toujours utiliser try/catch

```javascript
async function chargerDonnees() {
  try {
    const data = await fetch('/api/data');
    const json = await data.json();

    // 🔵 Breakpoint dans le try
    if (!json.items) {
      throw new Error('Items manquants');
    }

    return json.items.map(item => item.nom);

  } catch (error) {
    // 🔵 Breakpoint dans le catch
    console.error('Erreur de chargement:', error);
    return []; // Valeur par défaut
  }
}
```

**Avantages** :
- ✅ Erreurs capturées et gérées
- ✅ Contexte préservé
- ✅ Breakpoint dans le `catch` pour débugger

### Technique : Breakpoint sur "Pause on exceptions"

Dans les DevTools :

1. Ouvrez l'onglet **Sources**
2. Cliquez sur l'icône **pause** (⏸️) avec symbole stop
3. Cochez **"Pause on caught exceptions"**

Maintenant, le debugger s'arrêtera **automatiquement** quand une erreur se produit, même dans un try/catch !

**Utilisation** :
- Vous voyez exactement où l'erreur se produit
- Le call stack est disponible
- Les variables sont accessibles
- Vous comprenez le contexte de l'erreur

---

## Débugger plusieurs Promises en parallèle

### Promise.all : Plusieurs requêtes simultanées

```javascript
async function chargerDonneesComplete() {
  try {
    // 🔵 Point d'arrêt ici
    console.log('Chargement en parallèle...');

    const [users, posts, comments] = await Promise.all([
      fetch('/api/users').then(r => r.json()),
      fetch('/api/posts').then(r => r.json()),
      fetch('/api/comments').then(r => r.json())
    ]);

    // 🔵 Point d'arrêt ici aussi
    console.log('Tout est chargé !');
    console.log('Users:', users.length);
    console.log('Posts:', posts.length);
    console.log('Comments:', comments.length);

    return { users, posts, comments };

  } catch (error) {
    console.error('Erreur:', error);
  }
}
```

**Debugging** :
1. Breakpoint avant `Promise.all`
2. **F10** → Le code attend que TOUTES les Promises soient résolues
3. Breakpoint après → Inspectez `users`, `posts`, `comments`

**Watch expressions** :
```javascript
users
users?.length
posts
posts?.length
comments
comments?.length
```

### Promise.race : La plus rapide gagne

```javascript
async function chargerAvecTimeout() {
  const timeout = new Promise((_, reject) => {
    setTimeout(() => reject(new Error('Timeout')), 5000);
  });

  const data = fetch('/api/data').then(r => r.json());

  try {
    // 🔵 Point d'arrêt ici
    const result = await Promise.race([data, timeout]);
    console.log('Résultat:', result);
    return result;
  } catch (error) {
    console.error('Erreur ou timeout:', error.message);
  }
}
```

La première Promise qui termine (succès ou erreur) gagne !

---

## Techniques avancées de debugging asynchrone

### Technique 1 : Nommer vos Promises

Donnez des noms explicites à vos Promises pour mieux les identifier :

```javascript
async function chargerDonnees() {
  const promiseUsers = fetch('/api/users');
  const promisePosts = fetch('/api/posts');

  // 🔵 Breakpoint ici
  const responseUsers = await promiseUsers;
  const responsePosts = await promisePosts;

  // Les noms clairs aident au debugging !
}
```

### Technique 2 : Logs détaillés

Ajoutez des logs avec timestamps et contexte :

```javascript
async function chargerUtilisateur(id) {
  console.time(`Chargement user ${id}`);

  console.log(`[${new Date().toISOString()}] Début chargement ${id}`);
  const response = await fetch(`/api/users/${id}`);
  console.log(`[${new Date().toISOString()}] Réponse reçue`);

  const user = await response.json();
  console.log(`[${new Date().toISOString()}] Données parsées`);

  console.timeEnd(`Chargement user ${id}`);
  return user;
}
```

**Affiche** :
```
[2025-12-04T10:30:00.000Z] Début chargement 42
[2025-12-04T10:30:00.250Z] Réponse reçue
[2025-12-04T10:30:00.300Z] Données parsées
Chargement user 42: 300ms
```

Vous voyez exactement combien de temps prend chaque étape !

### Technique 3 : Wrapper de debugging

Créez une fonction wrapper pour logger automatiquement :

```javascript
async function fetchDebug(url, options) {
  console.log(`🌐 Fetch: ${url}`);
  console.time(url);

  try {
    const response = await fetch(url, options);
    console.log(`✅ ${url} → ${response.status}`);
    console.timeEnd(url);
    return response;
  } catch (error) {
    console.error(`❌ ${url} →`, error.message);
    console.timeEnd(url);
    throw error;
  }
}

// Utilisation
async function exemple() {
  const data = await fetchDebug('/api/data');
  // Logs automatiques !
}
```

### Technique 4 : Débugger les race conditions

Les **race conditions** sont des bugs difficiles où l'ordre d'exécution cause des problèmes :

```javascript
let utilisateurActuel = null;

async function chargerUtilisateur(id) {
  // 🔵 Point d'arrêt ici
  console.log(`Chargement de ${id}, actuel: ${utilisateurActuel?.id}`);

  const response = await fetch(`/api/users/${id}`);
  const user = await response.json();

  // ⚠️ Pendant l'attente, un autre appel peut avoir changé utilisateurActuel !
  // 🔵 Point d'arrêt ici aussi
  console.log(`Avant assignment: ${utilisateurActuel?.id}, nouveau: ${user.id}`);

  utilisateurActuel = user;
  afficherUtilisateur(utilisateurActuel);
}

// Si appelé rapidement :
chargerUtilisateur(1);
chargerUtilisateur(2); // Peut arriver avant que 1 soit fini !
```

**Watch expressions pour détecter** :
```javascript
utilisateurActuel
utilisateurActuel?.id
user.id
utilisateurActuel?.id === user.id
```

---

## Onglet Network : Débugger les requêtes

### Ouvrir l'onglet Network

1. DevTools → Onglet **Network**
2. Rechargez la page ou déclenchez vos requêtes
3. Vous voyez **toutes les requêtes** HTTP

### Informations disponibles

Pour chaque requête :

**Colonnes principales** :
- **Name** : URL de la requête
- **Status** : Code HTTP (200, 404, 500...)
- **Type** : Type de ressource (xhr, fetch, document...)
- **Size** : Taille des données
- **Time** : Durée de la requête

### Inspecter une requête

Cliquez sur une requête pour voir les détails :

#### Onglet Headers
```
Request URL: https://api.example.com/users/42
Request Method: GET
Status Code: 200 OK
```

#### Onglet Response
```json
{
  "id": 42,
  "nom": "Alice",
  "email": "alice@example.com"
}
```

#### Onglet Timing
```
Queueing: 0.5 ms
DNS Lookup: 12 ms
Connecting: 45 ms
Waiting (TTFB): 250 ms
Content Download: 2 ms
Total: 309.5 ms
```

### Filtrer les requêtes

**Filtres utiles** :
- **XHR** : Requêtes AJAX/fetch
- **JS** : Fichiers JavaScript
- **CSS** : Fichiers CSS
- **Img** : Images

### Débugger une API lente

```javascript
async function chargerDonneesLentes() {
  console.time('API');
  const response = await fetch('/api/slow-endpoint');
  console.timeEnd('API');
  // "API: 3500ms" → Trop lent !
}
```

**Dans Network** :
1. Trouvez la requête `/api/slow-endpoint`
2. Regardez l'onglet **Timing**
3. Identifiez le goulot : DNS ? Connexion ? Serveur ?

### Reproduire une requête

Clic droit sur une requête → **Copy** → **Copy as fetch** :

```javascript
fetch("https://api.example.com/users/42", {
  "headers": {
    "accept": "application/json"
  },
  "method": "GET"
});
```

Vous pouvez coller ce code dans la console pour reproduire exactement la requête !

---

## Débugger avec la Console

### console.table pour les tableaux

```javascript
async function chargerUtilisateurs() {
  const response = await fetch('/api/users');
  const users = await response.json();

  // 📊 Affichage tabulaire automatique !
  console.table(users);
}
```

**Affiche** :
```
┌─────┬────┬─────────┬──────────────────────┐
│(idx)│ id │  nom    │       email          │
├─────┼────┼─────────┼──────────────────────┤
│  0  │ 1  │ Alice   │ alice@example.com    │
│  1  │ 2  │ Bob     │ bob@example.com      │
│  2  │ 3  │ Charlie │ charlie@example.com  │
└─────┴────┴─────────┴──────────────────────┘
```

Beaucoup plus lisible que `console.log` !

### console.group pour organiser

```javascript
async function chargerTout() {
  console.group('🌐 Chargement des données');

  console.log('Chargement des utilisateurs...');
  const users = await fetch('/api/users').then(r => r.json());
  console.log('✅ Utilisateurs:', users.length);

  console.log('Chargement des posts...');
  const posts = await fetch('/api/posts').then(r => r.json());
  console.log('✅ Posts:', posts.length);

  console.groupEnd();
  console.log('Tout est chargé !');
}
```

**Affiche** :
```
▼ 🌐 Chargement des données
    Chargement des utilisateurs...
    ✅ Utilisateurs: 10
    Chargement des posts...
    ✅ Posts: 50
  Tout est chargé !
```

Organisé et pliable !

### console.time pour mesurer

```javascript
async function testerPerformance() {
  console.time('Promise.all');
  await Promise.all([
    fetch('/api/users'),
    fetch('/api/posts'),
    fetch('/api/comments')
  ]);
  console.timeEnd('Promise.all');

  console.time('Séquentiel');
  await fetch('/api/users');
  await fetch('/api/posts');
  await fetch('/api/comments');
  console.timeEnd('Séquentiel');
}
```

**Affiche** :
```
Promise.all: 450ms
Séquentiel: 1200ms
```

`Promise.all` est 2.6× plus rapide !

---

## Patterns de debugging courants

### Pattern 1 : Vérifier l'état de la réponse

```javascript
async function chargerDonnees() {
  const response = await fetch('/api/data');

  // 🔍 Vérifications détaillées
  console.log('Status:', response.status);
  console.log('OK:', response.ok);
  console.log('Headers:', response.headers);

  if (!response.ok) {
    const errorText = await response.text();
    console.error('Erreur serveur:', errorText);
    throw new Error(`HTTP ${response.status}: ${errorText}`);
  }

  return await response.json();
}
```

### Pattern 2 : Valider les données reçues

```javascript
async function chargerUtilisateur(id) {
  const response = await fetch(`/api/users/${id}`);
  const user = await response.json();

  // 🔍 Validation détaillée
  console.log('User reçu:', user);
  console.log('Type:', typeof user);
  console.log('Keys:', Object.keys(user));
  console.log('A un nom?', 'nom' in user);
  console.log('A un email?', 'email' in user);

  if (!user.nom || !user.email) {
    throw new Error('Données utilisateur incomplètes');
  }

  return user;
}
```

### Pattern 3 : Timeout avec Promise.race

```javascript
async function fetchAvecTimeout(url, timeoutMs = 5000) {
  const fetchPromise = fetch(url);

  const timeoutPromise = new Promise((_, reject) => {
    setTimeout(() => {
      reject(new Error(`Timeout après ${timeoutMs}ms`));
    }, timeoutMs);
  });

  try {
    // 🔵 Breakpoint ici
    const response = await Promise.race([fetchPromise, timeoutPromise]);
    console.log('✅ Réponse dans les temps');
    return response;
  } catch (error) {
    console.error('❌ Erreur ou timeout:', error.message);
    throw error;
  }
}
```

### Pattern 4 : Retry automatique

```javascript
async function fetchAvecRetry(url, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      // 🔵 Breakpoint ici
      console.log(`Tentative ${i + 1}/${maxRetries}`);

      const response = await fetch(url);

      if (response.ok) {
        console.log('✅ Succès');
        return response;
      }

      console.warn(`⚠️ Échec (${response.status}), retry...`);

    } catch (error) {
      console.error(`❌ Erreur tentative ${i + 1}:`, error.message);

      if (i === maxRetries - 1) {
        throw error; // Dernière tentative, on abandonne
      }

      // Attendre avant de retry
      await new Promise(resolve => setTimeout(resolve, 1000 * (i + 1)));
    }
  }
}
```

---

## Checklist de debugging asynchrone

Quand vous débuggez du code async, suivez cette checklist :

### ✅ Avant de débugger

- [ ] Convertir les Promises `.then()` en `async/await` si possible
- [ ] Ajouter des `try/catch` partout
- [ ] Activer "Pause on exceptions" dans DevTools
- [ ] Ouvrir l'onglet Network

### ✅ Pendant le debugging

- [ ] Placer un breakpoint au début de la fonction async
- [ ] Vérifier `response.ok` et `response.status`
- [ ] Inspecter les données reçues avec `console.log` ou `console.table`
- [ ] Vérifier que les données ont la structure attendue
- [ ] Regarder les timings dans l'onglet Network

### ✅ Pour les erreurs

- [ ] Vérifier le call stack (même s'il est incomplet)
- [ ] Regarder le message d'erreur exact
- [ ] Vérifier le status HTTP de la requête
- [ ] Inspecter la réponse brute (onglet Response dans Network)
- [ ] Tester la requête directement dans la console

### ✅ Pour les performances

- [ ] Utiliser `console.time` / `console.timeEnd`
- [ ] Vérifier les timings dans l'onglet Network
- [ ] Identifier les requêtes lentes
- [ ] Envisager `Promise.all` pour paralléliser

---

## Erreurs courantes et solutions

### "Cannot read property of undefined"

```javascript
async function exemple() {
  const response = await fetch('/api/data');
  const data = await response.json();
  console.log(data.items.length); // ❌ Si items est undefined
}
```

**Solution** : Vérifiez toujours l'existence

```javascript
async function exemple() {
  const response = await fetch('/api/data');
  const data = await response.json();

  // 🔵 Breakpoint ici
  console.log('Data:', data);
  console.log('Has items?', 'items' in data);

  if (!data.items) {
    throw new Error('Items manquants dans la réponse');
  }

  console.log(data.items.length);
}
```

### "Unhandled Promise Rejection"

```javascript
async function exemple() {
  await fetch('/api/data'); // ❌ Pas de try/catch !
}

exemple(); // Si erreur, elle n'est pas capturée
```

**Solution** : Toujours gérer les erreurs

```javascript
async function exemple() {
  try {
    await fetch('/api/data');
  } catch (error) {
    console.error('Erreur:', error);
  }
}

// Ou à l'appel :
exemple().catch(error => {
  console.error('Erreur:', error);
});
```

### "Résultats dans le désordre"

```javascript
// ❌ Problème : les requêtes peuvent finir dans n'importe quel ordre
ids.forEach(async (id) => {
  const user = await fetch(`/api/users/${id}`);
  afficher(user); // Ordre imprévisible !
});
```

**Solution** : Utiliser Promise.all

```javascript
// ✅ Les résultats sont dans l'ordre !
const promises = ids.map(id => fetch(`/api/users/${id}`));
const responses = await Promise.all(promises);
const users = await Promise.all(responses.map(r => r.json()));
users.forEach(user => afficher(user));
```

---

## Points clés à retenir

🔄 **Async = Exécution différée**
- Le code ne s'exécute pas dans l'ordre écrit
- Utilisez les DevTools pour suivre le flux réel

✨ **Async/await > Promises**
- Plus facile à lire et à débugger
- Call stack plus clair
- Un seul breakpoint suffit souvent

🛡️ **Toujours utiliser try/catch**
- Capture les erreurs
- Préserve le contexte
- Permet le debugging

🌐 **Onglet Network = Vérité**
- Voyez toutes les requêtes
- Inspectez les réponses
- Analysez les performances

🔍 **Techniques essentielles**
- `console.time` / `console.timeEnd` pour la performance
- `console.table` pour les tableaux
- `console.group` pour organiser
- "Pause on exceptions" pour les erreurs

📊 **Watch expressions**
- `response?.ok`
- `response?.status`
- `data?.length`
- `typeof data`

---

## Pour aller plus loin

Le debugging asynchrone est une compétence qui s'acquiert avec la pratique. Plus vous débuggerez de code async, plus vous développerez des réflexes et des intuitions.

**Conseil final** : Quand c'est possible, préférez **async/await** aux Promises classiques. C'est non seulement plus moderne, mais aussi infiniment plus facile à débugger !

---

> 💡 **Citation sur l'asynchrone** :
> *"Le code asynchrone, c'est comme jongler : ce n'est pas compliqué une fois qu'on a compris le truc, mais au début, tout tombe par terre !"*
>
> Avec les bons outils de debugging, vous allez devenir un expert jongleur ! 🤹

⏭️ [Performance et optimisation](/07-debugging-et-outils-avances/02-performance-optimisation/README.md)
