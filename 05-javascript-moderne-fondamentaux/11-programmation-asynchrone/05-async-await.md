🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.11.5 - Async/Await : la syntaxe moderne 🆕

## Introduction

Les **Promises** ont résolu le problème du callback hell, mais elles peuvent encore être un peu verbeuses avec leurs `.then()` et `.catch()`.

En 2017, JavaScript a introduit **async/await**, une syntaxe qui rend le code asynchrone aussi **simple à lire que du code synchrone**. C'est la façon **moderne et recommandée** d'écrire du code asynchrone aujourd'hui.

Async/await n'est pas une nouvelle façon de gérer l'asynchrone : c'est du **"sucre syntaxique"** au-dessus des Promises. Cela signifie que sous le capot, ça utilise toujours des Promises, mais avec une syntaxe bien plus agréable.

## Le problème avec .then()

Même si les Promises sont mieux que les callbacks, le code peut encore être difficile à lire :

```javascript
// Avec .then() - Fonctionnel mais verbeux
recupererUtilisateur(1)
    .then(utilisateur => {
        console.log('Utilisateur :', utilisateur.nom);
        return recupererArticles(utilisateur.id);
    })
    .then(articles => {
        console.log('Articles :', articles.length);
        return recupererCommentaires(articles[0].id);
    })
    .then(commentaires => {
        console.log('Commentaires :', commentaires.length);
    })
    .catch(erreur => {
        console.error('Erreur :', erreur);
    });
```

**Problèmes** :
- Beaucoup de `.then()`
- Syntaxe de callback (fonctions fléchées)
- Pas évident de partager des variables entre les `.then()`

## La solution : Async/Await

Avec async/await, le même code devient :

```javascript
// Avec async/await - Simple et lisible
async function chargerDonnees() {
    try {
        const utilisateur = await recupererUtilisateur(1);
        console.log('Utilisateur :', utilisateur.nom);

        const articles = await recupererArticles(utilisateur.id);
        console.log('Articles :', articles.length);

        const commentaires = await recupererCommentaires(articles[0].id);
        console.log('Commentaires :', commentaires.length);
    } catch (erreur) {
        console.error('Erreur :', erreur);
    }
}

chargerDonnees();
```

**Avantages** :
- ✅ Ressemble à du code synchrone
- ✅ Facile à lire de haut en bas
- ✅ Variables facilement accessibles
- ✅ Gestion d'erreurs avec try/catch familier

## Syntaxe de base

### Le mot-clé `async`

Pour utiliser `await`, vous devez être dans une fonction **async** :

```javascript
// Déclarer une fonction async
async function maFonction() {
    // Code asynchrone ici
}

// Ou avec une fonction fléchée
const maFonction = async () => {
    // Code asynchrone ici
};
```

**Important** : Une fonction `async` retourne **toujours** une Promise.

```javascript
async function direBonjour() {
    return 'Bonjour';
}

// Équivalent à :
function direBonjourPromise() {
    return Promise.resolve('Bonjour');
}

// Utilisation
direBonjour().then(message => {
    console.log(message); // 'Bonjour'
});
```

### Le mot-clé `await`

`await` **attend** qu'une Promise se résolve et retourne sa valeur :

```javascript
async function exemple() {
    // Attend que la Promise se résolve
    const resultat = await maPromise;

    // Cette ligne ne s'exécute qu'après la résolution
    console.log(resultat);
}
```

**Règle** : `await` ne peut être utilisé **qu'à l'intérieur** d'une fonction `async`.

```javascript
// ❌ ERREUR : await en dehors d'une fonction async
const resultat = await maPromise; // SyntaxError

// ✅ CORRECT : await dans une fonction async
async function maFonction() {
    const resultat = await maPromise; // OK
}
```

## Premier exemple simple

### Avec setTimeout

```javascript
// Fonction helper qui retourne une Promise
function attendre(ms) {
    return new Promise(resolve => {
        setTimeout(resolve, ms);
    });
}

// Utilisation avec async/await
async function demo() {
    console.log('Début');

    await attendre(2000); // Attend 2 secondes
    console.log('2 secondes écoulées');

    await attendre(1000); // Attend 1 seconde de plus
    console.log('3 secondes au total');
}

demo();

// Résultat :
// Début
// (attente de 2 secondes)
// 2 secondes écoulées
// (attente de 1 seconde)
// 3 secondes au total
```

### Comparaison avec .then()

```javascript
// Avec .then()
function demoThen() {
    console.log('Début');

    attendre(2000)
        .then(() => {
            console.log('2 secondes écoulées');
            return attendre(1000);
        })
        .then(() => {
            console.log('3 secondes au total');
        });
}

// Avec async/await - BEAUCOUP plus lisible !
async function demoAsync() {
    console.log('Début');

    await attendre(2000);
    console.log('2 secondes écoulées');

    await attendre(1000);
    console.log('3 secondes au total');
}
```

## Gestion d'erreurs avec try/catch

### Syntaxe

```javascript
async function maFonction() {
    try {
        const resultat = await operationRisquee();
        console.log('Succès :', resultat);
    } catch (erreur) {
        console.error('Erreur :', erreur);
    }
}
```

### Exemple complet

```javascript
function telechargerImage(url) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const reussi = Math.random() > 0.3;

            if (reussi) {
                resolve({ url, width: 800, height: 600 });
            } else {
                reject(new Error('Échec du téléchargement'));
            }
        }, 1000);
    });
}

// Avec async/await
async function afficherImage(url) {
    try {
        console.log('Téléchargement...');

        const image = await telechargerImage(url);

        console.log('✓ Image téléchargée :', image);
        console.log('Dimensions :', image.width, 'x', image.height);
    } catch (erreur) {
        console.error('✗ Erreur :', erreur.message);
    }
}

afficherImage('photo.jpg');

// Résultat (aléatoire) :
// Téléchargement...
// Soit : ✓ Image téléchargée : { url: 'photo.jpg', ... }
// Soit : ✗ Erreur : Échec du téléchargement
```

### Avec finally

Comme les Promises, vous pouvez ajouter un bloc `finally` :

```javascript
async function chargerDonnees() {
    afficherSpinner();

    try {
        const donnees = await fetch('/api/data');
        console.log(donnees);
    } catch (erreur) {
        console.error(erreur);
    } finally {
        cacherSpinner(); // Toujours exécuté
    }
}
```

## Exemples pratiques

### Exemple 1 : Authentification utilisateur

```javascript
async function connecterUtilisateur(email, password) {
    try {
        console.log('🔐 Connexion en cours...');

        // Valider l'email
        const emailValide = await validerEmail(email);
        console.log('✓ Email validé');

        // Vérifier les identifiants
        const utilisateur = await verifierIdentifiants(emailValide, password);
        console.log('✓ Identifiants corrects');

        // Créer une session
        const session = await creerSession(utilisateur.id);
        console.log('✓ Session créée');

        // Rediriger
        window.location.href = '/dashboard';

    } catch (erreur) {
        console.error('❌ Erreur de connexion :', erreur.message);
        afficherErreur('Connexion impossible : ' + erreur.message);
    }
}

// Utilisation
connecterUtilisateur('alice@example.com', 'motdepasse123');
```

### Exemple 2 : Traitement d'image séquentiel

```javascript
function telecharger(url) {
    return new Promise(resolve => {
        setTimeout(() => resolve({ url, data: 'image_data' }), 1000);
    });
}

function redimensionner(image) {
    return new Promise(resolve => {
        setTimeout(() => resolve({ ...image, width: 400, height: 300 }), 800);
    });
}

function appliquerFiltre(image) {
    return new Promise(resolve => {
        setTimeout(() => resolve({ ...image, filtre: 'sepia' }), 600);
    });
}

function sauvegarder(image) {
    return new Promise(resolve => {
        setTimeout(() => resolve('Image sauvegardée : ' + image.url), 500);
    });
}

// Avec async/await - Facile à lire !
async function traiterImage(url) {
    try {
        console.log('📥 Téléchargement...');
        const image = await telecharger(url);

        console.log('📐 Redimensionnement...');
        const imageRedim = await redimensionner(image);

        console.log('🎨 Application du filtre...');
        const imageFiltree = await appliquerFiltre(imageRedim);

        console.log('💾 Sauvegarde...');
        const resultat = await sauvegarder(imageFiltree);

        console.log('✅', resultat);
    } catch (erreur) {
        console.error('❌ Erreur :', erreur);
    }
}

traiterImage('photo.jpg');

// Résultat :
// 📥 Téléchargement...
// 📐 Redimensionnement...
// 🎨 Application du filtre...
// 💾 Sauvegarde...
// ✅ Image sauvegardée : photo.jpg
```

### Exemple 3 : API de recettes

```javascript
// Fonctions simulant des appels API
function rechercherRecette(nom) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const recettes = {
                'carbonara': { id: 1, nom: 'Carbonara' },
                'bouillabaisse': { id: 2, nom: 'Bouillabaisse' }
            };

            const recette = recettes[nom.toLowerCase()];
            if (recette) {
                resolve(recette);
            } else {
                reject(new Error('Recette non trouvée'));
            }
        }, 500);
    });
}

function recupererIngredients(recetteId) {
    return new Promise(resolve => {
        setTimeout(() => {
            const ingredients = {
                1: ['pâtes', 'œufs', 'bacon', 'parmesan'],
                2: ['poissons', 'safran', 'tomates', 'ail']
            };
            resolve(ingredients[recetteId]);
        }, 400);
    });
}

function recupererInstructions(recetteId) {
    return new Promise(resolve => {
        setTimeout(() => {
            const instructions = {
                1: ['Cuire les pâtes', 'Mélanger œufs et parmesan', 'Faire revenir le bacon'],
                2: ['Préparer le bouillon', 'Ajouter les poissons', 'Cuire 30 minutes']
            };
            resolve(instructions[recetteId]);
        }, 300);
    });
}

// Avec async/await
async function afficherRecette(nom) {
    try {
        console.log('🔍 Recherche de la recette...');
        const recette = await rechercherRecette(nom);
        console.log('✓ Recette trouvée :', recette.nom);

        console.log('📦 Récupération des ingrédients...');
        const ingredients = await recupererIngredients(recette.id);

        console.log('📝 Récupération des instructions...');
        const instructions = await recupererInstructions(recette.id);

        // Affichage
        console.log('\n=== RECETTE ===');
        console.log('Nom :', recette.nom);
        console.log('\nIngrédients :');
        ingredients.forEach(ing => console.log('  -', ing));
        console.log('\nInstructions :');
        instructions.forEach((inst, i) => console.log(`  ${i + 1}.`, inst));

    } catch (erreur) {
        console.error('❌', erreur.message);
    }
}

afficherRecette('carbonara');
```

### Exemple 4 : Formulaire d'inscription

```html
<form id="formInscription">
    <input type="email" id="email" placeholder="Email" required>
    <input type="password" id="password" placeholder="Mot de passe" required>
    <button type="submit">S'inscrire</button>
</form>
<p id="message"></p>
```

```javascript
const form = document.getElementById('formInscription');
const messageElement = document.getElementById('message');

// Fonctions simulant des vérifications
async function verifierEmailDisponible(email) {
    // Simuler un appel API
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (email === 'existe@example.com') {
                reject(new Error('Email déjà utilisé'));
            } else {
                resolve(true);
            }
        }, 1000);
    });
}

async function creerCompte(email, password) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve({ id: 123, email });
        }, 1500);
    });
}

async function envoyerEmailConfirmation(userId) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(true);
        }, 800);
    });
}

// Gestionnaire de soumission
form.addEventListener('submit', async (event) => {
    event.preventDefault();

    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;

    messageElement.textContent = 'Inscription en cours...';
    messageElement.style.color = 'blue';

    try {
        // Vérifier la disponibilité de l'email
        await verifierEmailDisponible(email);
        messageElement.textContent = 'Création du compte...';

        // Créer le compte
        const compte = await creerCompte(email, password);
        messageElement.textContent = 'Envoi de l\'email de confirmation...';

        // Envoyer l'email de confirmation
        await envoyerEmailConfirmation(compte.id);

        // Succès
        messageElement.textContent = '✅ Inscription réussie ! Vérifiez vos emails.';
        messageElement.style.color = 'green';
        form.reset();

    } catch (erreur) {
        messageElement.textContent = '❌ ' + erreur.message;
        messageElement.style.color = 'red';
    }
});
```

## Exécuter plusieurs Promises en parallèle

### Le problème avec await séquentiel

Si vous utilisez `await` plusieurs fois de suite, les opérations s'exécutent **séquentiellement** :

```javascript
async function charger() {
    const utilisateur = await recupererUtilisateur();  // 1 seconde
    const articles = await recupererArticles();        // 1 seconde
    const commentaires = await recupererCommentaires(); // 1 seconde

    // Total : 3 secondes
}
```

### Solution : Promise.all() avec async/await

Pour exécuter en **parallèle** :

```javascript
async function chargerParallele() {
    // Lancer toutes les Promises en même temps
    const [utilisateur, articles, commentaires] = await Promise.all([
        recupererUtilisateur(),
        recupererArticles(),
        recupererCommentaires()
    ]);

    // Total : 1 seconde (la plus lente)
    console.log(utilisateur, articles, commentaires);
}
```

### Exemple pratique

```javascript
async function chargerDashboard() {
    try {
        console.log('Chargement du dashboard...');

        // Exécuter 4 requêtes en parallèle
        const [user, stats, notifications, settings] = await Promise.all([
            fetch('/api/user').then(r => r.json()),
            fetch('/api/stats').then(r => r.json()),
            fetch('/api/notifications').then(r => r.json()),
            fetch('/api/settings').then(r => r.json())
        ]);

        console.log('Tout est chargé !');
        afficherDashboard(user, stats, notifications, settings);

    } catch (erreur) {
        console.error('Erreur lors du chargement :', erreur);
    }
}
```

## Comparaison : .then() vs async/await

### Scénario : Charger des données utilisateur

#### Avec .then()

```javascript
function chargerProfilThen(userId) {
    return recupererUtilisateur(userId)
        .then(utilisateur => {
            console.log('Utilisateur :', utilisateur.nom);
            return recupererPhoto(utilisateur.photoId);
        })
        .then(photo => {
            console.log('Photo récupérée');
            return photo;
        })
        .catch(erreur => {
            console.error('Erreur :', erreur);
            throw erreur;
        });
}
```

#### Avec async/await

```javascript
async function chargerProfilAsync(userId) {
    try {
        const utilisateur = await recupererUtilisateur(userId);
        console.log('Utilisateur :', utilisateur.nom);

        const photo = await recupererPhoto(utilisateur.photoId);
        console.log('Photo récupérée');

        return photo;
    } catch (erreur) {
        console.error('Erreur :', erreur);
        throw erreur;
    }
}
```

**Avantages async/await** :
- ✅ Plus lisible (comme du code synchrone)
- ✅ Variables facilement accessibles
- ✅ try/catch familier
- ✅ Moins de niveaux d'indentation

## Boucles avec async/await

### Traiter des items séquentiellement

```javascript
async function traiterListe(items) {
    for (const item of items) {
        // Chaque item est traité l'un après l'autre
        await traiterItem(item);
        console.log('Item traité :', item);
    }

    console.log('Tous les items traités');
}

const items = ['A', 'B', 'C'];
traiterListe(items);

// Résultat (séquentiel) :
// Item traité : A
// Item traité : B
// Item traité : C
// Tous les items traités
```

### Traiter des items en parallèle

```javascript
async function traiterListeParallele(items) {
    // map retourne un tableau de Promises
    const promises = items.map(item => traiterItem(item));

    // Attendre que toutes se terminent
    const resultats = await Promise.all(promises);

    console.log('Tous les items traités :', resultats);
}

const items = ['A', 'B', 'C'];
traiterListeParallele(items);

// Tous les items sont traités en même temps !
```

### Exemple : Télécharger plusieurs images

```javascript
async function telechargerImages(urls) {
    console.log('Téléchargement de', urls.length, 'images...');

    // Méthode 1 : Séquentiel (lent)
    // for (const url of urls) {
    //     await telecharger(url);
    // }

    // Méthode 2 : Parallèle (rapide)
    const promises = urls.map(url => telecharger(url));
    const images = await Promise.all(promises);

    console.log('Toutes les images téléchargées !');
    return images;
}

const urls = ['image1.jpg', 'image2.jpg', 'image3.jpg'];
telechargerImages(urls);
```

## async/await au niveau top-level (ES2022)

Depuis ES2022, vous pouvez utiliser `await` **en dehors** d'une fonction async dans les modules :

```javascript
// Dans un fichier .js en mode module
// Pas besoin de wrapper dans une fonction async !

const utilisateur = await recupererUtilisateur(1);
console.log(utilisateur);

const donnees = await fetch('/api/data').then(r => r.json());
console.log(donnees);

// Très pratique pour les scripts et l'initialisation
```

**Note** : Cela ne fonctionne que dans les modules ES6, pas dans les scripts classiques.

## Pièges courants

### Piège 1 : Oublier `await`

```javascript
async function maFonction() {
    // ❌ ERREUR : Oublier await
    const resultat = recupererDonnees(); // resultat est une Promise !
    console.log(resultat.nom); // undefined

    // ✅ CORRECT : Avec await
    const resultat = await recupererDonnees();
    console.log(resultat.nom); // OK
}
```

### Piège 2 : Utiliser `await` dans une boucle forEach

```javascript
// ❌ NE FONCTIONNE PAS : forEach n'attend pas les Promises
async function mauvaiseFacon(items) {
    items.forEach(async (item) => {
        await traiter(item); // N'attend PAS vraiment
    });
    console.log('Terminé ?'); // S'affiche immédiatement !
}

// ✅ CORRECT : Utiliser for...of
async function bonneFacon(items) {
    for (const item of items) {
        await traiter(item); // Attend vraiment
    }
    console.log('Vraiment terminé');
}

// ✅ ALTERNATIVE : map + Promise.all
async function enParallele(items) {
    await Promise.all(items.map(item => traiter(item)));
    console.log('Tout traité en parallèle');
}
```

### Piège 3 : Ne pas gérer les erreurs

```javascript
// ❌ DANGEREUX : Pas de try/catch
async function sansTryCatch() {
    const resultat = await operationRisquee();
    // Si ça échoue, erreur non gérée !
}

// ✅ CORRECT : Toujours utiliser try/catch
async function avecTryCatch() {
    try {
        const resultat = await operationRisquee();
    } catch (erreur) {
        console.error('Erreur gérée :', erreur);
    }
}
```

### Piège 4 : Oublier que async retourne toujours une Promise

```javascript
async function obtenirNombre() {
    return 42;
}

// ❌ ERREUR
const nombre = obtenirNombre(); // Promise, pas 42 !
console.log(nombre + 10); // NaN

// ✅ CORRECT
const nombre = await obtenirNombre(); // Dans une fonction async
console.log(nombre + 10); // 52

// ✅ OU
obtenirNombre().then(nombre => {
    console.log(nombre + 10); // 52
});
```

## Bonnes pratiques

### ✅ 1. Toujours utiliser try/catch

```javascript
async function maFonction() {
    try {
        const resultat = await operationAsyncrone();
        return resultat;
    } catch (erreur) {
        console.error('Erreur :', erreur);
        throw erreur; // ou gérer différemment
    }
}
```

### ✅ 2. Utiliser Promise.all() pour le parallélisme

```javascript
// ❌ LENT : Séquentiel (3 secondes)
async function lent() {
    const a = await operation1(); // 1s
    const b = await operation2(); // 1s
    const c = await operation3(); // 1s
}

// ✅ RAPIDE : Parallèle (1 seconde)
async function rapide() {
    const [a, b, c] = await Promise.all([
        operation1(),
        operation2(),
        operation3()
    ]);
}
```

### ✅ 3. Extraire les fonctions async

```javascript
// ✅ BIEN : Fonctions réutilisables
async function chargerUtilisateur(id) {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
}

async function sauvegarderUtilisateur(utilisateur) {
    const response = await fetch('/api/users', {
        method: 'POST',
        body: JSON.stringify(utilisateur)
    });
    return response.json();
}

// Utilisation claire
async function mettreAJourProfil(id, modifications) {
    const utilisateur = await chargerUtilisateur(id);
    const utilisateurModifie = { ...utilisateur, ...modifications };
    await sauvegarderUtilisateur(utilisateurModifie);
}
```

### ✅ 4. Documenter les fonctions async

```javascript
/**
 * Récupère les détails d'un utilisateur depuis l'API
 * @param {number} userId - L'ID de l'utilisateur
 * @returns {Promise<Object>} Les données utilisateur
 * @throws {Error} Si l'utilisateur n'existe pas
 */
async function recupererUtilisateur(userId) {
    const response = await fetch(`/api/users/${userId}`);

    if (!response.ok) {
        throw new Error('Utilisateur non trouvé');
    }

    return response.json();
}
```

### ✅ 5. Préférer async/await à .then() pour la lisibilité

```javascript
// ⚠️ MOINS LISIBLE (mais valide)
function avecThen() {
    return fetch('/api/data')
        .then(r => r.json())
        .then(data => processData(data))
        .then(result => saveResult(result));
}

// ✅ PLUS LISIBLE
async function avecAsync() {
    const response = await fetch('/api/data');
    const data = await response.json();
    const result = await processData(data);
    await saveResult(result);
}
```

## Quand utiliser async/await vs .then()

### Utilisez async/await quand :

- ✅ Vous écrivez du **nouveau code**
- ✅ La **lisibilité** est importante
- ✅ Vous avez besoin de **variables partagées** entre étapes
- ✅ Vous voulez utiliser **try/catch** pour les erreurs
- ✅ Vous devez faire des **boucles** avec async

### Utilisez .then() quand :

- ⚠️ Vous ne pouvez pas utiliser `async` (contraintes)
- ⚠️ Vous voulez **chaîner simplement** sans logique complexe
- ⚠️ Vous maintenez du **code existant** en .then()

**Recommandation** : Dans 99% des cas, utilisez **async/await** pour du nouveau code. C'est la façon moderne et recommandée.

## Ce qu'il faut retenir

✅ **async** : Déclare une fonction asynchrone (retourne toujours une Promise)

✅ **await** : Attend qu'une Promise se résolve (uniquement dans une fonction async)

✅ **try/catch** : Gérer les erreurs de manière synchrone

✅ **async/await** ressemble à du code synchrone mais est asynchrone

✅ **Promise.all()** : Exécuter plusieurs opérations en parallèle

✅ **for...of** : Pour les boucles avec await (pas forEach !)

✅ **Toujours** gérer les erreurs avec try/catch

✅ **Préférer async/await** à .then() pour la lisibilité

✅ **Une fonction async retourne toujours une Promise**

✅ **Top-level await** : Possible dans les modules (ES2022+)

## Dans la prochaine leçon

Félicitations ! Vous maîtrisez maintenant les trois façons de gérer l'asynchrone en JavaScript : callbacks, Promises, et async/await.

Dans la prochaine leçon, nous découvrirons **fetch()** et les **requêtes HTTP**, qui permettent de communiquer avec des serveurs et des APIs.

Vous découvrirez :
- Comment utiliser l'API Fetch moderne
- Les requêtes GET, POST, PUT, DELETE
- Gérer les réponses (JSON, texte, etc.)
- Les headers et la configuration
- Gestion d'erreurs réseau

---


⏭️ [Fetch API : requêtes HTTP modernes](/05-javascript-moderne-fondamentaux/11-programmation-asynchrone/06-fetch-api.md)
