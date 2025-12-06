🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.11.4 - Promises : création et utilisation (.then, .catch, .finally) 🆕

## Introduction

Les **Promises** (Promesses) sont la solution moderne pour gérer le code asynchrone en JavaScript. Elles ont été introduites dans ES6 (2015) pour résoudre le problème du **callback hell** que nous avons vu dans la leçon précédente.

Une Promise représente une **valeur qui sera disponible maintenant, plus tard, ou jamais**. C'est comme une promesse dans la vraie vie : quelqu'un vous promet de faire quelque chose, et cette promesse peut être tenue (succès) ou brisée (échec).

Dans cette leçon, nous allons apprendre à créer et utiliser des Promises.

## Qu'est-ce qu'une Promise ?

### Définition simple

Une **Promise** est un objet qui représente le résultat **futur** d'une opération asynchrone.

### Analogie du monde réel : Commander au restaurant

Imaginez que vous commandez un plat au restaurant :

```
Vous : "Je voudrais une pizza, s'il vous plaît"
Serveur : "D'accord, voici votre ticket numéro 42"
         (← C'est la Promise !)

La Promise a 3 états possibles :

1. EN ATTENTE (Pending)
   Le cuisinier prépare votre pizza
   Vous attendez, mais vous pouvez faire autre chose

2. RÉUSSIE (Fulfilled/Resolved)
   ✅ "Pizza numéro 42 prête !"
   Vous récupérez votre pizza

3. ÉCHOUÉE (Rejected)
   ❌ "Désolé, nous n'avons plus de mozzarella"
   Vous gérez le problème (commander autre chose)
```

### Les trois états d'une Promise

```javascript
// État 1 : PENDING (en attente)
const maPromise = new Promise((resolve, reject) => {
    // Code asynchrone en cours...
});

// État 2 : FULFILLED (réussie)
// → La Promise appelle resolve(valeur)

// État 3 : REJECTED (échouée)
// → La Promise appelle reject(erreur)
```

**Important** : Une Promise ne peut changer d'état qu'**une seule fois**. Une fois résolue ou rejetée, elle reste dans cet état définitivement.

## Créer une Promise

### Syntaxe de base

```javascript
const maPromise = new Promise((resolve, reject) => {
    // Code asynchrone ici

    // Si succès :
    resolve(valeur);

    // Si échec :
    reject(erreur);
});
```

### Paramètres du constructeur

La fonction passée au constructeur `Promise` reçoit deux paramètres :
- **`resolve`** : Fonction à appeler en cas de succès
- **`reject`** : Fonction à appeler en cas d'échec

### Premier exemple simple

```javascript
const promesseSimple = new Promise((resolve, reject) => {
    const nombre = Math.random();

    if (nombre > 0.5) {
        resolve('Succès ! Nombre : ' + nombre);
    } else {
        reject('Échec ! Nombre : ' + nombre);
    }
});

console.log(promesseSimple);
// Promise { <pending> } ou Promise { <fulfilled> } ou Promise { <rejected> }
```

### Exemple avec setTimeout

```javascript
function attendreDeuxSecondes() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('2 secondes écoulées !');
        }, 2000);
    });
}

console.log('Démarrage...');
const promesse = attendreDeuxSecondes();
console.log('Promise créée :', promesse); // Promise { <pending> }

// Après 2 secondes, la promise sera résolue
```

## Utiliser une Promise avec .then()

### Syntaxe

```javascript
maPromise.then(
    (valeur) => {
        // Code exécuté si la promise réussit
        console.log('Succès :', valeur);
    }
);
```

### Exemple complet

```javascript
function telechargerImage(url) {
    return new Promise((resolve, reject) => {
        console.log('Téléchargement de', url, '...');

        // Simuler un téléchargement
        setTimeout(() => {
            const image = { url, width: 800, height: 600 };
            resolve(image); // Succès !
        }, 2000);
    });
}

// Utilisation
telechargerImage('photo.jpg').then((image) => {
    console.log('Image téléchargée :', image);
    console.log('Dimensions :', image.width, 'x', image.height);
});

console.log('Le code continue pendant le téléchargement...');

// Résultat :
// Téléchargement de photo.jpg ...
// Le code continue pendant le téléchargement...
// (attente de 2 secondes)
// Image téléchargée : { url: 'photo.jpg', width: 800, height: 600 }
// Dimensions : 800 x 600
```

## Gérer les erreurs avec .catch()

### Syntaxe

```javascript
maPromise
    .then((valeur) => {
        console.log('Succès :', valeur);
    })
    .catch((erreur) => {
        console.error('Erreur :', erreur);
    });
```

### Exemple avec gestion d'erreur

```javascript
function telechargerImageAvecErreur(url) {
    return new Promise((resolve, reject) => {
        console.log('Téléchargement de', url, '...');

        setTimeout(() => {
            const reussi = Math.random() > 0.5;

            if (reussi) {
                resolve({ url, width: 800, height: 600 });
            } else {
                reject('Erreur réseau : impossible de télécharger');
            }
        }, 1000);
    });
}

// Utilisation avec gestion d'erreur
telechargerImageAvecErreur('photo.jpg')
    .then((image) => {
        console.log('✓ Image téléchargée :', image);
    })
    .catch((erreur) => {
        console.error('✗ Erreur :', erreur);
    });

// Résultat (aléatoire) :
// Téléchargement de photo.jpg ...
// Soit : ✓ Image téléchargée : { url: 'photo.jpg', ... }
// Soit : ✗ Erreur : Erreur réseau : impossible de télécharger
```

## .finally() - Code qui s'exécute toujours

### Syntaxe

```javascript
maPromise
    .then((valeur) => {
        console.log('Succès');
    })
    .catch((erreur) => {
        console.error('Erreur');
    })
    .finally(() => {
        console.log('Terminé (succès ou échec)');
    });
```

### Exemple pratique : Indicateur de chargement

```html
<button id="charger">Charger les données</button>
<div id="spinner" style="display: none;">Chargement...</div>
<div id="resultat"></div>
```

```javascript
const bouton = document.getElementById('charger');
const spinner = document.getElementById('spinner');
const resultat = document.getElementById('resultat');

function chargerDonnees() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const succes = Math.random() > 0.3;

            if (succes) {
                resolve(['Article 1', 'Article 2', 'Article 3']);
            } else {
                reject('Erreur de connexion');
            }
        }, 2000);
    });
}

bouton.addEventListener('click', () => {
    // Afficher le spinner
    spinner.style.display = 'block';
    resultat.textContent = '';

    chargerDonnees()
        .then((articles) => {
            resultat.textContent = 'Articles : ' + articles.join(', ');
        })
        .catch((erreur) => {
            resultat.textContent = '❌ ' + erreur;
            resultat.style.color = 'red';
        })
        .finally(() => {
            // Toujours masquer le spinner, succès ou échec
            spinner.style.display = 'none';
        });
});
```

## Chaînage de Promises

### Le pouvoir du chaînage

Contrairement aux callbacks, les Promises peuvent être **chaînées** de manière élégante :

```javascript
promesse1
    .then(resultat1 => {
        return promesse2;
    })
    .then(resultat2 => {
        return promesse3;
    })
    .then(resultat3 => {
        console.log('Tout est terminé !');
    })
    .catch(erreur => {
        console.error('Erreur à n\'importe quelle étape :', erreur);
    });
```

### Exemple concret : Traitement d'image

```javascript
function telecharger(url) {
    return new Promise((resolve, reject) => {
        console.log('📥 Téléchargement :', url);
        setTimeout(() => resolve({ url, data: 'image_data' }), 1000);
    });
}

function redimensionner(image) {
    return new Promise((resolve, reject) => {
        console.log('📐 Redimensionnement...');
        setTimeout(() => {
            resolve({ ...image, width: 400, height: 300 });
        }, 1000);
    });
}

function appliquerFiltre(image) {
    return new Promise((resolve, reject) => {
        console.log('🎨 Application du filtre...');
        setTimeout(() => {
            resolve({ ...image, filtre: 'sepia' });
        }, 1000);
    });
}

function sauvegarder(image) {
    return new Promise((resolve, reject) => {
        console.log('💾 Sauvegarde...');
        setTimeout(() => {
            resolve('Image sauvegardée : ' + image.url);
        }, 1000);
    });
}

// Chaînage élégant !
telecharger('photo.jpg')
    .then(image => redimensionner(image))
    .then(image => appliquerFiltre(image))
    .then(image => sauvegarder(image))
    .then(message => {
        console.log('✅', message);
    })
    .catch(erreur => {
        console.error('❌ Erreur :', erreur);
    })
    .finally(() => {
        console.log('🏁 Traitement terminé');
    });

// Résultat :
// 📥 Téléchargement : photo.jpg
// 📐 Redimensionnement...
// 🎨 Application du filtre...
// 💾 Sauvegarde...
// ✅ Image sauvegardée : photo.jpg
// 🏁 Traitement terminé
```

### Syntaxe simplifiée pour le chaînage

Quand vous retournez directement une valeur dans `.then()`, elle est automatiquement transformée en Promise :

```javascript
Promise.resolve(5)
    .then(x => x * 2)      // Retourne 10 (automatiquement wrapped dans une Promise)
    .then(x => x + 3)      // Retourne 13
    .then(x => x / 2)      // Retourne 6.5
    .then(resultat => {
        console.log('Résultat final :', resultat); // 6.5
    });
```

## Comparaison : Callbacks vs Promises

### ❌ Avec Callbacks (callback hell)

```javascript
recupererUtilisateur(id, (erreur, utilisateur) => {
    if (erreur) {
        gererErreur(erreur);
        return;
    }

    recupererArticles(utilisateur.id, (erreur, articles) => {
        if (erreur) {
            gererErreur(erreur);
            return;
        }

        recupererCommentaires(articles[0].id, (erreur, commentaires) => {
            if (erreur) {
                gererErreur(erreur);
                return;
            }

            afficher(utilisateur, articles, commentaires);
        });
    });
});

// 😱 3 niveaux d'indentation, gestion d'erreurs répétée
```

### ✅ Avec Promises

```javascript
recupererUtilisateur(id)
    .then(utilisateur => recupererArticles(utilisateur.id))
    .then(articles => recupererCommentaires(articles[0].id))
    .then(commentaires => {
        afficher(utilisateur, articles, commentaires);
    })
    .catch(erreur => {
        gererErreur(erreur); // Une seule gestion d'erreurs !
    });

// 😊 Linéaire, facile à lire, une gestion d'erreurs
```

## Exemples pratiques complets

### Exemple 1 : Authentification utilisateur

```javascript
function validerEmail(email) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const estValide = email.includes('@');
            if (estValide) {
                resolve(email);
            } else {
                reject('Email invalide');
            }
        }, 500);
    });
}

function verifierCompte(email) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const compteExiste = email !== 'nouveau@example.com';
            if (compteExiste) {
                resolve({ email, id: 123 });
            } else {
                reject('Compte inexistant');
            }
        }, 1000);
    });
}

function recupererDonnees(compte) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve({
                ...compte,
                nom: 'Alice',
                role: 'admin'
            });
        }, 800);
    });
}

// Utilisation
const email = 'alice@example.com';

validerEmail(email)
    .then(emailValide => {
        console.log('✓ Email valide');
        return verifierCompte(emailValide);
    })
    .then(compte => {
        console.log('✓ Compte trouvé');
        return recupererDonnees(compte);
    })
    .then(utilisateur => {
        console.log('✓ Données récupérées');
        console.log('Bienvenue', utilisateur.nom);
    })
    .catch(erreur => {
        console.error('✗ Erreur :', erreur);
    })
    .finally(() => {
        console.log('Processus de connexion terminé');
    });
```

### Exemple 2 : API de recettes

```javascript
function rechercherRecette(nom) {
    return new Promise((resolve, reject) => {
        console.log('🔍 Recherche de recette :', nom);

        setTimeout(() => {
            const recettes = {
                'carbonara': { id: 1, nom: 'Carbonara', difficulte: 'facile' },
                'bouillabaisse': { id: 2, nom: 'Bouillabaisse', difficulte: 'difficile' }
            };

            const recette = recettes[nom.toLowerCase()];

            if (recette) {
                resolve(recette);
            } else {
                reject('Recette non trouvée');
            }
        }, 1000);
    });
}

function recupererIngredients(recetteId) {
    return new Promise((resolve, reject) => {
        console.log('📦 Récupération des ingrédients...');

        setTimeout(() => {
            const ingredients = {
                1: ['pâtes', 'œufs', 'bacon', 'parmesan'],
                2: ['poissons', 'safran', 'tomates', 'ail']
            };

            resolve(ingredients[recetteId]);
        }, 800);
    });
}

function recupererInstructions(recetteId) {
    return new Promise((resolve, reject) => {
        console.log('📝 Récupération des instructions...');

        setTimeout(() => {
            const instructions = {
                1: ['Cuire les pâtes', 'Mélanger œufs et parmesan', 'Faire revenir le bacon', 'Mélanger le tout'],
                2: ['Préparer le bouillon', 'Ajouter les poissons', 'Cuire 30 minutes']
            };

            resolve(instructions[recetteId]);
        }, 600);
    });
}

// Utilisation
rechercherRecette('carbonara')
    .then(recette => {
        console.log('✓ Recette trouvée :', recette.nom);

        // Récupérer ingredients ET instructions en parallèle
        return Promise.all([
            Promise.resolve(recette),
            recupererIngredients(recette.id),
            recupererInstructions(recette.id)
        ]);
    })
    .then(([recette, ingredients, instructions]) => {
        console.log('\n=== RECETTE COMPLÈTE ===');
        console.log('Nom :', recette.nom);
        console.log('Difficulté :', recette.difficulte);
        console.log('\nIngrédients :');
        ingredients.forEach(ing => console.log('  -', ing));
        console.log('\nInstructions :');
        instructions.forEach((inst, i) => console.log(`  ${i + 1}.`, inst));
    })
    .catch(erreur => {
        console.error('❌', erreur);
    });
```

### Exemple 3 : Upload de fichier avec progression

```html
<input type="file" id="fichier">
<button id="upload">Upload</button>
<progress id="barre" value="0" max="100" style="width: 300px;"></progress>
<p id="statut"></p>
```

```javascript
const inputFichier = document.getElementById('fichier');
const boutonUpload = document.getElementById('upload');
const barre = document.getElementById('barre');
const statut = document.getElementById('statut');

function simulerUpload(fichier) {
    return new Promise((resolve, reject) => {
        let progression = 0;

        const interval = setInterval(() => {
            progression += 10;
            barre.value = progression;
            statut.textContent = `Upload : ${progression}%`;

            if (progression >= 100) {
                clearInterval(interval);

                // Simuler succès ou échec
                if (fichier.size < 5000000) { // Moins de 5 Mo
                    resolve({
                        nom: fichier.name,
                        url: 'https://server.com/files/' + fichier.name
                    });
                } else {
                    reject('Fichier trop volumineux');
                }
            }
        }, 300);
    });
}

boutonUpload.addEventListener('click', () => {
    const fichier = inputFichier.files[0];

    if (!fichier) {
        alert('Sélectionnez un fichier');
        return;
    }

    statut.textContent = 'Upload en cours...';
    barre.value = 0;

    simulerUpload(fichier)
        .then(fichierUploade => {
            statut.textContent = '✅ Upload terminé !';
            statut.style.color = 'green';
            console.log('Fichier disponible à :', fichierUploade.url);
        })
        .catch(erreur => {
            statut.textContent = '❌ ' + erreur;
            statut.style.color = 'red';
            barre.value = 0;
        })
        .finally(() => {
            boutonUpload.disabled = false;
        });
});
```

## Créer des Promises résolues ou rejetées immédiatement

### Promise.resolve()

Crée une Promise déjà résolue :

```javascript
const promesseReussie = Promise.resolve('Valeur immédiate');

promesseReussie.then(valeur => {
    console.log(valeur); // 'Valeur immédiate'
});

// Équivalent à :
const promesse = new Promise(resolve => {
    resolve('Valeur immédiate');
});
```

**Utilisation courante** : Convertir une valeur en Promise pour l'utiliser dans un chaînage.

### Promise.reject()

Crée une Promise déjà rejetée :

```javascript
const promesseEchouee = Promise.reject('Erreur immédiate');

promesseEchouee.catch(erreur => {
    console.error(erreur); // 'Erreur immédiate'
});
```

### Exemple pratique

```javascript
function recupererDonnees(source) {
    // Si données en cache, retourner immédiatement
    if (cache[source]) {
        return Promise.resolve(cache[source]);
    }

    // Sinon, faire une vraie requête
    return fetch(source).then(response => response.json());
}

// Utilisation identique dans les deux cas
recupererDonnees('api/users')
    .then(donnees => {
        console.log(donnees);
    });
```

## Gestion d'erreurs avancée

### Erreurs dans .then()

Si une erreur est levée dans un `.then()`, elle est automatiquement capturée par le `.catch()` suivant :

```javascript
Promise.resolve(10)
    .then(x => {
        console.log('x =', x);
        throw new Error('Oups !');
    })
    .then(x => {
        console.log('Cette ligne ne s\'exécutera jamais');
    })
    .catch(erreur => {
        console.error('Erreur capturée :', erreur.message); // 'Oups !'
    });
```

### Récupération après erreur

Vous pouvez "récupérer" après une erreur :

```javascript
Promise.reject('Erreur initiale')
    .catch(erreur => {
        console.log('Gestion de l\'erreur :', erreur);
        return 'Valeur de récupération';
    })
    .then(valeur => {
        console.log('Continuation normale :', valeur); // 'Valeur de récupération'
    });
```

### Exemple : Retry (réessayer en cas d'échec)

```javascript
function fetchAvecRetry(url, tentatives = 3) {
    return fetch(url)
        .catch(erreur => {
            if (tentatives > 1) {
                console.log(`Échec, ${tentatives - 1} tentatives restantes...`);
                return fetchAvecRetry(url, tentatives - 1);
            } else {
                throw erreur;
            }
        });
}

fetchAvecRetry('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log('Données reçues :', data))
    .catch(erreur => console.error('Échec après 3 tentatives'));
```

## Pièges courants

### Piège 1 : Oublier de retourner la Promise

```javascript
// ❌ ERREUR : Ne retourne pas la promise
Promise.resolve(1)
    .then(x => {
        Promise.resolve(x * 2); // Promise ignorée !
    })
    .then(x => {
        console.log(x); // undefined
    });

// ✅ CORRECT : Retourner la promise
Promise.resolve(1)
    .then(x => {
        return Promise.resolve(x * 2);
    })
    .then(x => {
        console.log(x); // 2
    });
```

### Piège 2 : Ne pas gérer les erreurs

```javascript
// ⚠️ DANGEREUX : Pas de .catch()
maPromise.then(resultat => {
    console.log(resultat);
});

// Si la promise est rejetée, erreur non gérée !

// ✅ TOUJOURS ajouter .catch()
maPromise
    .then(resultat => {
        console.log(resultat);
    })
    .catch(erreur => {
        console.error(erreur);
    });
```

### Piège 3 : Créer une nouvelle Promise inutilement

```javascript
// ❌ Anti-pattern : Promise Constructor Antipattern
function mauvaiseFonction() {
    return new Promise((resolve, reject) => {
        autrePromise().then(resultat => {
            resolve(resultat);
        }).catch(erreur => {
            reject(erreur);
        });
    });
}

// ✅ MIEUX : Retourner directement la promise
function bonneFonction() {
    return autrePromise();
}
```

### Piège 4 : Chaîner avec .then(successFn, errorFn)

```javascript
// ⚠️ FORME DÉCONSEILLÉE (syntaxe old-school)
maPromise.then(
    resultat => console.log(resultat),
    erreur => console.error(erreur)
);

// ✅ PRÉFÉRER .catch()
maPromise
    .then(resultat => console.log(resultat))
    .catch(erreur => console.error(erreur));

// Pourquoi ? Avec .catch(), les erreurs dans le premier .then() sont aussi capturées
```

## Bonnes pratiques

### ✅ 1. Toujours retourner dans .then()

```javascript
// ✅ BIEN
promesse
    .then(x => {
        return autreFonction(x); // Retourner
    })
    .then(y => {
        console.log(y);
    });
```

### ✅ 2. Toujours ajouter .catch()

```javascript
// ✅ BIEN
promesse
    .then(handleSuccess)
    .catch(handleError); // Ne jamais oublier !
```

### ✅ 3. Utiliser .finally() pour le nettoyage

```javascript
// ✅ BIEN
afficherSpinner();

fetchData()
    .then(processData)
    .catch(handleError)
    .finally(() => {
        cacherSpinner(); // Toujours masquer le spinner
    });
```

### ✅ 4. Chaîner au lieu d'imbriquer

```javascript
// ❌ ÉVITER : Imbrication (retour du callback hell !)
promesse1.then(res1 => {
    promesse2.then(res2 => {
        promesse3.then(res3 => {
            console.log(res3);
        });
    });
});

// ✅ PRÉFÉRER : Chaînage
promesse1
    .then(res1 => promesse2)
    .then(res2 => promesse3)
    .then(res3 => console.log(res3));
```

### ✅ 5. Nommer les fonctions pour plus de clarté

```javascript
// ✅ BIEN
fetchUser(id)
    .then(enrichUserData)
    .then(validateUser)
    .then(saveToDatabase)
    .then(sendConfirmationEmail)
    .catch(handleError);

// Plus lisible que des fonctions fléchées partout
```

## Ce qu'il faut retenir

✅ **Promise** = objet représentant une valeur future (succès ou échec)

✅ **3 états** : pending (attente), fulfilled (réussie), rejected (échouée)

✅ **Créer** : `new Promise((resolve, reject) => { })`

✅ **resolve(valeur)** : marquer comme réussie

✅ **reject(erreur)** : marquer comme échouée

✅ **.then(fn)** : gérer le succès

✅ **.catch(fn)** : gérer les erreurs

✅ **.finally(fn)** : code qui s'exécute toujours

✅ **Chaînage** : `.then().then().then()` pour séquencer

✅ **Toujours retourner** dans .then() pour continuer le chaînage

✅ **Toujours ajouter .catch()** pour gérer les erreurs

## Dans la prochaine leçon

Maintenant que vous maîtrisez les bases des Promises, nous allons découvrir des méthodes très utiles : **Promise.all()**, **Promise.race()**, **Promise.allSettled()** et **Promise.any()**.

Vous découvrirez :
- Comment exécuter plusieurs Promises en parallèle
- Comment attendre que toutes se terminent
- Comment récupérer la plus rapide
- Les différences entre les méthodes et quand les utiliser

---


⏭️ [Async/Await : la syntaxe moderne](/05-javascript-moderne-fondamentaux/11-programmation-asynchrone/05-async-await.md)
