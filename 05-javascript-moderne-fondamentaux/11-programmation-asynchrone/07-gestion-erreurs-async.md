🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.11.7 - Gestion d'erreurs avec try/catch en async 🆕

## Introduction

La **gestion d'erreurs** est cruciale en programmation asynchrone. Quand vous faites des requêtes réseau, chargez des fichiers ou interagissez avec des APIs, beaucoup de choses peuvent mal tourner :
- Pas de connexion Internet
- Le serveur ne répond pas (timeout)
- Données invalides
- Ressource introuvable (404)
- Erreurs serveur (500)

Avec `async/await`, la gestion d'erreurs devient **simple et familière** grâce à `try/catch`, exactement comme en code synchrone. C'est l'un des grands avantages d'async/await par rapport aux Promises classiques.

## Rappel : try/catch en code synchrone

Avant de voir try/catch en asynchrone, rappelons le fonctionnement de base :

```javascript
// Code synchrone
function diviser(a, b) {
    if (b === 0) {
        throw new Error('Division par zéro !');
    }
    return a / b;
}

try {
    const resultat = diviser(10, 2);
    console.log('Résultat :', resultat); // 5

    const erreur = diviser(10, 0); // Lance une erreur
    console.log('Cette ligne ne s\'exécute jamais');

} catch (error) {
    console.error('Erreur capturée :', error.message);
}

// Résultat :
// Résultat : 5
// Erreur capturée : Division par zéro !
```

**Principe** :
- `try` : Bloc de code à essayer
- `catch` : Bloc exécuté si une erreur se produit
- `throw` : Lancer une erreur

## try/catch avec async/await

Avec async/await, le fonctionnement est **exactement le même** :

```javascript
async function chargerUtilisateur(id) {
    try {
        const response = await fetch(`/api/users/${id}`);

        if (!response.ok) {
            throw new Error(`Erreur HTTP : ${response.status}`);
        }

        const user = await response.json();
        console.log('Utilisateur :', user.name);
        return user;

    } catch (error) {
        console.error('Erreur lors du chargement :', error.message);
        return null;
    }
}

chargerUtilisateur(1);
```

### Que capture le catch ?

Le bloc `catch` capture **toutes les erreurs** qui se produisent dans le `try` :

1. **Erreurs lancées avec throw** :
```javascript
try {
    throw new Error('Erreur personnalisée');
} catch (error) {
    console.log(error.message); // 'Erreur personnalisée'
}
```

2. **Erreurs de Promises rejetées** :
```javascript
try {
    await Promise.reject('Promise rejetée');
} catch (error) {
    console.log(error); // 'Promise rejetée'
}
```

3. **Erreurs réseau (fetch)** :
```javascript
try {
    await fetch('https://serveur-inexistant.xyz');
} catch (error) {
    console.log('Erreur réseau'); // Pas de connexion
}
```

4. **Erreurs de parsing JSON** :
```javascript
try {
    const response = await fetch('/api/data');
    const data = await response.json(); // Si le contenu n'est pas du JSON valide
} catch (error) {
    console.log('Erreur de parsing JSON');
}
```

## Exemple pratique : Formulaire de connexion

```html
<form id="formConnexion">
    <input type="email" id="email" placeholder="Email" required>
    <input type="password" id="password" placeholder="Mot de passe" required>
    <button type="submit">Se connecter</button>
</form>
<p id="message"></p>
<div id="spinner" style="display: none;">Connexion en cours...</div>
```

```javascript
const form = document.getElementById('formConnexion');
const message = document.getElementById('message');
const spinner = document.getElementById('spinner');

async function connecter(email, password) {
    try {
        // Valider les entrées
        if (!email || !password) {
            throw new Error('Email et mot de passe requis');
        }

        if (!email.includes('@')) {
            throw new Error('Email invalide');
        }

        // Faire la requête
        const response = await fetch('/api/login', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ email, password })
        });

        // Vérifier le statut
        if (response.status === 401) {
            throw new Error('Email ou mot de passe incorrect');
        }

        if (response.status === 429) {
            throw new Error('Trop de tentatives. Réessayez plus tard.');
        }

        if (!response.ok) {
            throw new Error('Erreur serveur. Réessayez plus tard.');
        }

        // Parser la réponse
        const data = await response.json();

        // Succès !
        return data;

    } catch (error) {
        // Relancer l'erreur pour que l'appelant puisse la gérer
        throw error;
    }
}

form.addEventListener('submit', async (event) => {
    event.preventDefault();

    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;

    // Afficher le spinner
    spinner.style.display = 'block';
    message.textContent = '';

    try {
        const data = await connecter(email, password);

        // Succès
        message.textContent = '✅ Connexion réussie !';
        message.style.color = 'green';

        // Rediriger après 1 seconde
        setTimeout(() => {
            window.location.href = '/dashboard';
        }, 1000);

    } catch (error) {
        // Afficher l'erreur à l'utilisateur
        message.textContent = '❌ ' + error.message;
        message.style.color = 'red';

    } finally {
        // Toujours masquer le spinner
        spinner.style.display = 'none';
    }
});
```

## Le bloc finally

### Qu'est-ce que finally ?

Le bloc `finally` s'exécute **toujours**, qu'il y ait une erreur ou non. C'est parfait pour le nettoyage :

```javascript
async function chargerDonnees() {
    afficherSpinner();

    try {
        const response = await fetch('/api/data');
        const data = await response.json();
        afficherDonnees(data);
    } catch (error) {
        afficherErreur(error.message);
    } finally {
        cacherSpinner(); // Toujours exécuté
    }
}
```

### Cas d'usage typiques de finally

```javascript
async function traiterFichier() {
    let fichier = null;

    try {
        fichier = await ouvrirFichier('data.txt');
        const contenu = await lireFichier(fichier);
        await traiterContenu(contenu);

    } catch (error) {
        console.error('Erreur de traitement :', error);

    } finally {
        // Toujours fermer le fichier, même en cas d'erreur
        if (fichier) {
            await fermerFichier(fichier);
        }
    }
}
```

### Exemple : Indicateurs de chargement

```javascript
async function sauvegarder() {
    const bouton = document.getElementById('btnSauvegarder');

    try {
        // Désactiver le bouton pendant la sauvegarde
        bouton.disabled = true;
        bouton.textContent = 'Sauvegarde...';

        await envoyerDonnees();

        alert('Sauvegarde réussie !');

    } catch (error) {
        alert('Erreur de sauvegarde : ' + error.message);

    } finally {
        // Toujours réactiver le bouton
        bouton.disabled = false;
        bouton.textContent = 'Sauvegarder';
    }
}
```

## Gestion d'erreurs à plusieurs niveaux

### Capturer à différents endroits

Vous pouvez gérer les erreurs à plusieurs niveaux :

```javascript
// Niveau 1 : Fonction bas niveau
async function recupererDonnees(url) {
    try {
        const response = await fetch(url);

        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }

        return await response.json();

    } catch (error) {
        // Logger l'erreur
        console.error('Erreur dans recupererDonnees:', error);

        // Relancer pour que l'appelant puisse aussi la gérer
        throw error;
    }
}

// Niveau 2 : Fonction métier
async function chargerProduits() {
    try {
        const produits = await recupererDonnees('/api/produits');
        return produits;

    } catch (error) {
        console.error('Impossible de charger les produits');

        // Relancer avec un message plus spécifique
        throw new Error('Chargement des produits impossible');
    }
}

// Niveau 3 : Interface utilisateur
async function afficherProduits() {
    try {
        const produits = await chargerProduits();
        afficher(produits);

    } catch (error) {
        // Afficher à l'utilisateur
        alert('Erreur : ' + error.message);
    }
}
```

### Quand relancer l'erreur ?

```javascript
async function fonctionUtilitaire() {
    try {
        // Opération
        const result = await operation();
        return result;

    } catch (error) {
        // Logger pour le débogage
        console.error('Détails techniques :', error);

        // Relancer pour que l'appelant puisse gérer
        throw new Error('Opération impossible');
    }
}

async function fonctionUI() {
    try {
        await fonctionUtilitaire();

    } catch (error) {
        // Gérer et NE PAS relancer (niveau final)
        afficherMessageErreur(error.message);
    }
}
```

## Erreurs personnalisées

### Créer des types d'erreurs

```javascript
// Classe d'erreur personnalisée
class ErreurValidation extends Error {
    constructor(message) {
        super(message);
        this.name = 'ErreurValidation';
    }
}

class ErreurReseau extends Error {
    constructor(message, status) {
        super(message);
        this.name = 'ErreurReseau';
        this.status = status;
    }
}

class ErreurAuthentification extends Error {
    constructor(message) {
        super(message);
        this.name = 'ErreurAuthentification';
    }
}

// Utilisation
async function creerUtilisateur(donnees) {
    try {
        // Validation
        if (!donnees.email) {
            throw new ErreurValidation('Email requis');
        }

        if (!donnees.email.includes('@')) {
            throw new ErreurValidation('Email invalide');
        }

        // Requête
        const response = await fetch('/api/users', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(donnees)
        });

        if (response.status === 401) {
            throw new ErreurAuthentification('Non autorisé');
        }

        if (!response.ok) {
            throw new ErreurReseau('Erreur serveur', response.status);
        }

        return await response.json();

    } catch (error) {
        // Gérer différemment selon le type
        if (error instanceof ErreurValidation) {
            console.error('Validation :', error.message);
            afficherErreurFormulaire(error.message);
        } else if (error instanceof ErreurAuthentification) {
            console.error('Auth :', error.message);
            redirigerVersLogin();
        } else if (error instanceof ErreurReseau) {
            console.error('Réseau :', error.message, error.status);
            afficherErreurServeur();
        } else {
            console.error('Erreur inconnue :', error);
            afficherErreurGenerique();
        }

        throw error;
    }
}
```

## Gestion d'erreurs avec Promise.all()

### Le problème

Avec `Promise.all()`, si **une seule** Promise échoue, tout échoue :

```javascript
async function chargerTout() {
    try {
        const [users, posts, comments] = await Promise.all([
            fetch('/api/users').then(r => r.json()),
            fetch('/api/posts').then(r => r.json()),
            fetch('/api/comments').then(r => r.json())
        ]);

        return { users, posts, comments };

    } catch (error) {
        // Si UNE requête échoue, on perd TOUT
        console.error('Au moins une requête a échoué');
        return null;
    }
}
```

### Solution 1 : Promise.allSettled()

```javascript
async function chargerToutRobuste() {
    const resultats = await Promise.allSettled([
        fetch('/api/users').then(r => r.json()),
        fetch('/api/posts').then(r => r.json()),
        fetch('/api/comments').then(r => r.json())
    ]);

    // Récupérer les succès et les échecs
    const users = resultats[0].status === 'fulfilled' ? resultats[0].value : [];
    const posts = resultats[1].status === 'fulfilled' ? resultats[1].value : [];
    const comments = resultats[2].status === 'fulfilled' ? resultats[2].value : [];

    // Logger les échecs
    resultats.forEach((resultat, index) => {
        if (resultat.status === 'rejected') {
            console.error(`Requête ${index} échouée :`, resultat.reason);
        }
    });

    return { users, posts, comments };
}
```

### Solution 2 : Wrapper chaque Promise

```javascript
async function chargerAvecDefaut(url, defaut = null) {
    try {
        const response = await fetch(url);
        if (!response.ok) throw new Error('Erreur HTTP');
        return await response.json();
    } catch (error) {
        console.error(`Erreur pour ${url}:`, error);
        return defaut;
    }
}

async function chargerToutAvecDefauts() {
    const [users, posts, comments] = await Promise.all([
        chargerAvecDefaut('/api/users', []),
        chargerAvecDefaut('/api/posts', []),
        chargerAvecDefaut('/api/comments', [])
    ]);

    // Aucune erreur ne remonte, on a toujours des valeurs
    return { users, posts, comments };
}
```

## Patterns de gestion d'erreurs

### Pattern 1 : Retry (réessayer)

```javascript
async function fetchAvecRetry(url, tentatives = 3) {
    for (let i = 0; i < tentatives; i++) {
        try {
            const response = await fetch(url);

            if (!response.ok) {
                throw new Error(`HTTP ${response.status}`);
            }

            return await response.json();

        } catch (error) {
            console.log(`Tentative ${i + 1}/${tentatives} échouée`);

            // Si c'est la dernière tentative, relancer l'erreur
            if (i === tentatives - 1) {
                throw new Error(`Échec après ${tentatives} tentatives`);
            }

            // Attendre avant de réessayer (exponential backoff)
            await new Promise(resolve => setTimeout(resolve, 1000 * (i + 1)));
        }
    }
}

// Utilisation
try {
    const data = await fetchAvecRetry('/api/data');
    console.log('Données récupérées :', data);
} catch (error) {
    console.error('Impossible de récupérer les données :', error);
}
```

### Pattern 2 : Fallback (solution de repli)

```javascript
async function chargerAvecFallback(urlPrincipale, urlSecondaire) {
    try {
        // Essayer l'URL principale
        const response = await fetch(urlPrincipale);

        if (!response.ok) {
            throw new Error('URL principale inaccessible');
        }

        return await response.json();

    } catch (error) {
        console.warn('URL principale échouée, tentative avec URL secondaire');

        try {
            // Essayer l'URL de secours
            const response = await fetch(urlSecondaire);

            if (!response.ok) {
                throw new Error('URL secondaire inaccessible');
            }

            return await response.json();

        } catch (errorSecondaire) {
            // Les deux ont échoué
            throw new Error('Toutes les sources de données sont inaccessibles');
        }
    }
}

// Utilisation
try {
    const data = await chargerAvecFallback(
        'https://api-principale.com/data',
        'https://api-backup.com/data'
    );
} catch (error) {
    console.error('Aucune source disponible');
}
```

### Pattern 3 : Circuit Breaker (disjoncteur)

```javascript
class CircuitBreaker {
    constructor(seuil = 5) {
        this.echecs = 0;
        this.seuil = seuil;
        this.etatOuvert = false;
    }

    async executer(fn) {
        // Si le circuit est ouvert, refuser immédiatement
        if (this.etatOuvert) {
            throw new Error('Circuit ouvert - service temporairement indisponible');
        }

        try {
            const resultat = await fn();

            // Succès : réinitialiser le compteur
            this.echecs = 0;

            return resultat;

        } catch (error) {
            this.echecs++;

            // Si on dépasse le seuil, ouvrir le circuit
            if (this.echecs >= this.seuil) {
                this.etatOuvert = true;
                console.error('Circuit ouvert après', this.seuil, 'échecs');

                // Fermer automatiquement après 30 secondes
                setTimeout(() => {
                    this.etatOuvert = false;
                    this.echecs = 0;
                    console.log('Circuit refermé');
                }, 30000);
            }

            throw error;
        }
    }
}

// Utilisation
const breaker = new CircuitBreaker(3);

async function chargerDonnees() {
    try {
        const data = await breaker.executer(async () => {
            const response = await fetch('/api/data');
            if (!response.ok) throw new Error('Erreur HTTP');
            return response.json();
        });

        console.log('Données :', data);

    } catch (error) {
        console.error('Erreur :', error.message);
    }
}
```

## Exemple complet : Application météo

```html
<div id="app">
    <input type="text" id="ville" placeholder="Nom de la ville">
    <button id="rechercher">Rechercher</button>

    <div id="spinner" style="display: none;">Chargement...</div>
    <div id="erreur" style="display: none; color: red;"></div>
    <div id="resultat" style="display: none;"></div>
</div>
```

```javascript
const ville = document.getElementById('ville');
const boutonRechercher = document.getElementById('rechercher');
const spinner = document.getElementById('spinner');
const erreur = document.getElementById('erreur');
const resultat = document.getElementById('resultat');

// Erreurs personnalisées
class ErreurVilleInconnue extends Error {
    constructor(ville) {
        super(`Ville "${ville}" non trouvée`);
        this.name = 'ErreurVilleInconnue';
    }
}

class ErreurAPI extends Error {
    constructor(message, code) {
        super(message);
        this.name = 'ErreurAPI';
        this.code = code;
    }
}

// Fonction principale
async function recupererMeteo(nomVille) {
    // Validation
    if (!nomVille || nomVille.trim() === '') {
        throw new Error('Veuillez entrer un nom de ville');
    }

    try {
        // Simuler un appel API
        const response = await fetch(
            `https://api.openweathermap.org/data/2.5/weather?q=${nomVille}&appid=VOTRE_CLE`
        );

        // Gérer les différents codes d'erreur
        if (response.status === 404) {
            throw new ErreurVilleInconnue(nomVille);
        }

        if (response.status === 401) {
            throw new ErreurAPI('Clé API invalide', 401);
        }

        if (response.status === 429) {
            throw new ErreurAPI('Limite de requêtes atteinte', 429);
        }

        if (!response.ok) {
            throw new ErreurAPI(`Erreur serveur: ${response.status}`, response.status);
        }

        const data = await response.json();
        return data;

    } catch (error) {
        // Distinguer erreur réseau vs erreur API
        if (error instanceof TypeError) {
            throw new Error('Erreur de connexion. Vérifiez votre connexion Internet.');
        }

        // Relancer les autres erreurs
        throw error;
    }
}

// Afficher la météo
function afficherMeteo(data) {
    resultat.style.display = 'block';
    resultat.innerHTML = `
        <h2>${data.name}</h2>
        <p>Température : ${Math.round(data.main.temp - 273.15)}°C</p>
        <p>Conditions : ${data.weather[0].description}</p>
        <p>Humidité : ${data.main.humidity}%</p>
    `;
}

// Afficher une erreur
function afficherErreur(message) {
    erreur.style.display = 'block';
    erreur.textContent = message;
}

// Cacher tous les éléments
function toutCacher() {
    spinner.style.display = 'none';
    erreur.style.display = 'none';
    resultat.style.display = 'none';
}

// Gestionnaire d'événement
boutonRechercher.addEventListener('click', async () => {
    const nomVille = ville.value.trim();

    // Réinitialiser l'affichage
    toutCacher();
    spinner.style.display = 'block';

    try {
        const meteo = await recupererMeteo(nomVille);
        afficherMeteo(meteo);

    } catch (error) {
        // Gérer les différents types d'erreurs
        if (error instanceof ErreurVilleInconnue) {
            afficherErreur('❌ ' + error.message);
        } else if (error instanceof ErreurAPI) {
            if (error.code === 429) {
                afficherErreur('⏰ Trop de requêtes. Réessayez dans 1 minute.');
            } else {
                afficherErreur('⚠️ Erreur du service météo. Réessayez plus tard.');
            }
        } else {
            afficherErreur('❌ ' + error.message);
        }

        // Logger pour le débogage
        console.error('Erreur détaillée :', error);

    } finally {
        spinner.style.display = 'none';
    }
});

// Rechercher avec la touche Entrée
ville.addEventListener('keypress', (e) => {
    if (e.key === 'Enter') {
        boutonRechercher.click();
    }
});
```

## Pièges courants

### Piège 1 : Oublier le try/catch

```javascript
// ❌ DANGEREUX : Pas de gestion d'erreurs
async function mauvais() {
    const data = await fetch('/api/data');
    return data.json(); // Si ça échoue, erreur non gérée !
}

// ✅ CORRECT
async function correct() {
    try {
        const response = await fetch('/api/data');
        return await response.json();
    } catch (error) {
        console.error('Erreur :', error);
        return null;
    }
}
```

### Piège 2 : Catch vide

```javascript
// ❌ MAUVAIS : Catch qui ne fait rien
try {
    await operation();
} catch (error) {
    // Silence total, impossible de déboguer
}

// ✅ AU MINIMUM : Logger
try {
    await operation();
} catch (error) {
    console.error('Erreur opération :', error);
    throw error; // Relancer si nécessaire
}
```

### Piège 3 : Ne pas vérifier response.ok avec fetch

```javascript
// ❌ ERREUR : Oublie de vérifier le statut
try {
    const response = await fetch('/api/data');
    const data = await response.json(); // Peut échouer si 404/500
} catch (error) {
    // N'attrape PAS les erreurs HTTP !
}

// ✅ CORRECT
try {
    const response = await fetch('/api/data');

    if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
    }

    const data = await response.json();
} catch (error) {
    // Attrape TOUTES les erreurs
}
```

### Piège 4 : Finally qui retourne une valeur

```javascript
// ⚠️ ATTENTION : Le return dans finally écrase tout
async function bizarre() {
    try {
        return 'succès';
    } catch (error) {
        return 'erreur';
    } finally {
        return 'finally'; // ❌ Écrase les autres returns !
    }
}

console.log(await bizarre()); // 'finally' (inattendu !)

// ✅ CORRECT : Finally ne doit pas retourner de valeur
async function correct() {
    try {
        return 'succès';
    } catch (error) {
        return 'erreur';
    } finally {
        console.log('Nettoyage'); // Pas de return
    }
}
```

## Bonnes pratiques

### ✅ 1. Toujours gérer les erreurs

```javascript
// ✅ BIEN : Toujours un try/catch pour les fonctions async
async function maFonction() {
    try {
        const result = await operationAsyncrone();
        return result;
    } catch (error) {
        console.error('Erreur :', error);
        throw error;
    }
}
```

### ✅ 2. Créer des erreurs personnalisées

```javascript
// ✅ BIEN : Types d'erreurs clairs
class ErreurValidation extends Error {
    constructor(message) {
        super(message);
        this.name = 'ErreurValidation';
    }
}

// Utilisation
if (!email.includes('@')) {
    throw new ErreurValidation('Email invalide');
}
```

### ✅ 3. Logger pour le débogage

```javascript
// ✅ BIEN : Logger les détails
try {
    await operation();
} catch (error) {
    console.error('Erreur dans operation:', {
        message: error.message,
        stack: error.stack,
        timestamp: new Date().toISOString()
    });

    // Afficher un message simple à l'utilisateur
    afficherErreur('Une erreur est survenue');
}
```

### ✅ 4. Utiliser finally pour le nettoyage

```javascript
// ✅ BIEN : Nettoyage dans finally
async function traiter() {
    let ressource = null;

    try {
        ressource = await acquerir();
        await utiliser(ressource);
    } catch (error) {
        console.error('Erreur :', error);
    } finally {
        if (ressource) {
            await liberer(ressource);
        }
    }
}
```

### ✅ 5. Fournir des messages d'erreur utiles

```javascript
// ❌ MAUVAIS : Message vague
throw new Error('Erreur');

// ✅ BIEN : Message descriptif
throw new Error('Impossible de charger l\'utilisateur avec l\'ID 123 : serveur inaccessible');
```

## Ce qu'il faut retenir

✅ **try/catch** fonctionne exactement pareil avec async/await qu'en synchrone

✅ **catch** capture toutes les erreurs (throw, Promise rejetée, erreurs réseau)

✅ **finally** s'exécute toujours (parfait pour le nettoyage)

✅ **Toujours vérifier response.ok** avec fetch (ne rejette que sur erreur réseau)

✅ **Erreurs personnalisées** : créer des classes pour différents types d'erreurs

✅ **Promise.allSettled()** : pour gérer plusieurs Promises sans qu'une erreur annule tout

✅ **Patterns utiles** : retry, fallback, circuit breaker

✅ **Toujours logger** les erreurs pour le débogage

✅ **Messages clairs** pour les utilisateurs

✅ **Ne jamais ignorer les erreurs** (catch vide)

## Conclusion du chapitre

Félicitations ! Vous avez maintenant terminé le chapitre complet sur la **programmation asynchrone** en JavaScript.

Vous maîtrisez :
1. ✅ Les concepts de l'asynchrone et pourquoi c'est nécessaire
2. ✅ setTimeout et setInterval
3. ✅ Le callback hell et ses problèmes
4. ✅ Les Promises (.then, .catch, .finally)
5. ✅ Async/await (syntaxe moderne)
6. ✅ Fetch API pour les requêtes HTTP
7. ✅ La gestion d'erreurs avec try/catch

Vous êtes maintenant capable de créer des applications web modernes qui communiquent avec des APIs, gèrent des opérations asynchrones complexes, et offrent une excellente expérience utilisateur !

---


⏭️ [Gestion des erreurs](/05-javascript-moderne-fondamentaux/12-gestion-erreurs/README.md)
