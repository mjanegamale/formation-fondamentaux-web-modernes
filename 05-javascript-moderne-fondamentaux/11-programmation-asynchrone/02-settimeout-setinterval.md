🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.11.2 - setTimeout et setInterval 🆕

## Introduction

Maintenant que vous comprenez pourquoi l'asynchrone est nécessaire, découvrons nos deux premières fonctions asynchrones : **`setTimeout()`** et **`setInterval()`**.

Ces deux fonctions permettent de :
- **`setTimeout`** : Exécuter du code **une fois** après un délai
- **`setInterval`** : Exécuter du code **répétitivement** à intervalles réguliers

Ce sont les fonctions asynchrones les plus simples à comprendre, et un excellent point de départ pour maîtriser la programmation asynchrone.

## setTimeout() - Exécuter après un délai

### Syntaxe de base

```javascript
setTimeout(fonction, delai);
```

- **`fonction`** : La fonction à exécuter (callback)
- **`delai`** : Le délai en **millisecondes** (1000ms = 1 seconde)

### Premier exemple simple

```javascript
console.log('Début');

setTimeout(() => {
    console.log('Ceci apparaît après 2 secondes');
}, 2000);

console.log('Fin');

// Résultat :
// Début
// Fin
// (attente de 2 secondes)
// Ceci apparaît après 2 secondes
```

**Remarquez** : "Fin" s'affiche AVANT le message du setTimeout, même si setTimeout est écrit avant dans le code !

### Avec une fonction nommée

```javascript
function direBonjour() {
    console.log('Bonjour !');
}

// Exécuter direBonjour après 3 secondes
setTimeout(direBonjour, 3000);

console.log('Le timer est lancé');

// Résultat :
// Le timer est lancé
// (attente de 3 secondes)
// Bonjour !
```

### Passer des paramètres à la fonction

```javascript
function saluer(nom, age) {
    console.log(`Bonjour ${nom}, tu as ${age} ans !`);
}

// Les paramètres après le délai sont passés à la fonction
setTimeout(saluer, 2000, 'Alice', 25);

// Résultat (après 2 secondes) :
// Bonjour Alice, tu as 25 ans !
```

### Alternative avec une fonction fléchée

```javascript
const nom = 'Bob';

setTimeout(() => {
    console.log(`Salut ${nom} !`);
}, 1000);

// Avec une fonction fléchée, vous pouvez utiliser les variables
// de la portée extérieure directement
```

## Exemples pratiques avec setTimeout

### Exemple 1 : Message de bienvenue retardé

```html
<h1 id="titre">Chargement...</h1>
```

```javascript
const titre = document.getElementById('titre');

// Attendre 1 seconde avant d'afficher le vrai titre
setTimeout(() => {
    titre.textContent = 'Bienvenue sur mon site !';
}, 1000);
```

### Exemple 2 : Cacher une notification après 3 secondes

```html
<div id="notification" style="background: green; color: white; padding: 10px;">
    Message sauvegardé avec succès !
</div>
```

```javascript
const notification = document.getElementById('notification');

// Cacher la notification après 3 secondes
setTimeout(() => {
    notification.style.display = 'none';
}, 3000);
```

### Exemple 3 : Animation de texte qui apparaît mot par mot

```html
<p id="texte"></p>
```

```javascript
const texte = document.getElementById('texte');
const mots = ['Bonjour', 'je', 'suis', 'un', 'texte', 'animé'];
let index = 0;

function afficherMot() {
    if (index < mots.length) {
        texte.textContent += mots[index] + ' ';
        index++;

        // Afficher le prochain mot après 500ms
        setTimeout(afficherMot, 500);
    }
}

afficherMot();

// Résultat : Les mots apparaissent un par un toutes les 500ms
```

### Exemple 4 : Compte à rebours

```html
<h2 id="compteur">3</h2>
<p id="message"></p>
```

```javascript
const compteur = document.getElementById('compteur');
const message = document.getElementById('message');
let temps = 3;

function decompter() {
    if (temps > 0) {
        compteur.textContent = temps;
        temps--;
        setTimeout(decompter, 1000); // Rappel après 1 seconde
    } else {
        compteur.textContent = '🎉';
        message.textContent = 'C\'est parti !';
    }
}

decompter();

// Résultat : Compte à rebours de 3 à 0, puis affiche "C'est parti !"
```

## clearTimeout() - Annuler un timeout

Vous pouvez **annuler** un setTimeout avant qu'il ne se déclenche.

### Syntaxe

```javascript
const timerId = setTimeout(fonction, delai);

// Annuler le timeout
clearTimeout(timerId);
```

### Exemple pratique : Bouton d'annulation

```html
<button id="demarrer">Démarrer le timer (3s)</button>
<button id="annuler">Annuler</button>
<p id="status"></p>
```

```javascript
const btnDemarrer = document.getElementById('demarrer');
const btnAnnuler = document.getElementById('annuler');
const status = document.getElementById('status');
let timerId = null;

btnDemarrer.addEventListener('click', () => {
    status.textContent = 'Timer lancé...';

    timerId = setTimeout(() => {
        status.textContent = '✓ Timer terminé !';
    }, 3000);
});

btnAnnuler.addEventListener('click', () => {
    if (timerId) {
        clearTimeout(timerId);
        status.textContent = '❌ Timer annulé';
        timerId = null;
    }
});
```

### Exemple : Recherche avec délai (debouncing)

```html
<input type="text" id="recherche" placeholder="Tapez pour rechercher...">
<p id="resultats"></p>
```

```javascript
const champRecherche = document.getElementById('recherche');
const resultats = document.getElementById('resultats');
let timerId = null;

champRecherche.addEventListener('input', (event) => {
    const terme = event.target.value;

    // Annuler le timer précédent
    if (timerId) {
        clearTimeout(timerId);
    }

    // Créer un nouveau timer
    timerId = setTimeout(() => {
        if (terme.length > 0) {
            resultats.textContent = `Recherche pour : "${terme}"`;
            // Ici, vous feriez une vraie requête à une API
        } else {
            resultats.textContent = '';
        }
    }, 500); // Attendre 500ms après la dernière frappe
});

// Avantage : Ne lance la recherche que quand l'utilisateur a fini de taper
// Évite de faire 10 recherches si l'utilisateur tape 10 lettres rapidement
```

## setInterval() - Répéter à intervalles réguliers

### Syntaxe de base

```javascript
setInterval(fonction, intervalle);
```

- **`fonction`** : La fonction à exécuter
- **`intervalle`** : L'intervalle en millisecondes entre chaque exécution

### Premier exemple simple

```javascript
let compteur = 0;

setInterval(() => {
    compteur++;
    console.log('Compteur :', compteur);
}, 1000);

// Résultat :
// Compteur : 1     (après 1 seconde)
// Compteur : 2     (après 2 secondes)
// Compteur : 3     (après 3 secondes)
// ... (continue indéfiniment)
```

**⚠️ Attention** : `setInterval` continue **indéfiniment** jusqu'à ce que vous l'arrêtiez avec `clearInterval` !

### Avec une fonction nommée

```javascript
function afficherHeure() {
    const maintenant = new Date();
    const heureFormatee = maintenant.toLocaleTimeString();
    console.log('Il est :', heureFormatee);
}

// Afficher l'heure toutes les secondes
setInterval(afficherHeure, 1000);
```

## Exemples pratiques avec setInterval

### Exemple 1 : Horloge en temps réel

```html
<h1 id="horloge">00:00:00</h1>
```

```javascript
const horloge = document.getElementById('horloge');

function mettreAJourHorloge() {
    const maintenant = new Date();
    const heures = String(maintenant.getHours()).padStart(2, '0');
    const minutes = String(maintenant.getMinutes()).padStart(2, '0');
    const secondes = String(maintenant.getSeconds()).padStart(2, '0');

    horloge.textContent = `${heures}:${minutes}:${secondes}`;
}

// Mettre à jour immédiatement
mettreAJourHorloge();

// Puis mettre à jour toutes les secondes
setInterval(mettreAJourHorloge, 1000);
```

### Exemple 2 : Chronomètre

```html
<h2 id="chronometre">00:00</h2>
<button id="demarrer">Démarrer</button>
<button id="arreter">Arrêter</button>
<button id="reinitialiser">Réinitialiser</button>
```

```javascript
const affichage = document.getElementById('chronometre');
const btnDemarrer = document.getElementById('demarrer');
const btnArreter = document.getElementById('arreter');
const btnReinitialiser = document.getElementById('reinitialiser');

let secondes = 0;
let intervalId = null;

function afficherTemps() {
    const minutes = Math.floor(secondes / 60);
    const sec = secondes % 60;
    affichage.textContent =
        `${String(minutes).padStart(2, '0')}:${String(sec).padStart(2, '0')}`;
}

btnDemarrer.addEventListener('click', () => {
    if (intervalId) return; // Déjà démarré

    intervalId = setInterval(() => {
        secondes++;
        afficherTemps();
    }, 1000);
});

btnArreter.addEventListener('click', () => {
    if (intervalId) {
        clearInterval(intervalId);
        intervalId = null;
    }
});

btnReinitialiser.addEventListener('click', () => {
    if (intervalId) {
        clearInterval(intervalId);
        intervalId = null;
    }
    secondes = 0;
    afficherTemps();
});
```

### Exemple 3 : Slider/Carrousel automatique

```html
<div id="slider">
    <img id="image" src="image1.jpg" alt="Image">
</div>
<p id="position">1 / 3</p>
```

```javascript
const image = document.getElementById('image');
const position = document.getElementById('position');

const images = ['image1.jpg', 'image2.jpg', 'image3.jpg'];
let index = 0;

function changerImage() {
    index = (index + 1) % images.length; // Revient à 0 après la dernière
    image.src = images[index];
    position.textContent = `${index + 1} / ${images.length}`;
}

// Changer d'image toutes les 3 secondes
setInterval(changerImage, 3000);
```

### Exemple 4 : Barre de progression animée

```html
<div style="width: 300px; height: 30px; background: #ddd;">
    <div id="barre" style="width: 0%; height: 100%; background: green; transition: width 0.1s;"></div>
</div>
<p id="pourcentage">0%</p>
```

```javascript
const barre = document.getElementById('barre');
const pourcentage = document.getElementById('pourcentage');
let progression = 0;

const intervalId = setInterval(() => {
    if (progression >= 100) {
        clearInterval(intervalId); // Arrêter à 100%
        return;
    }

    progression += 1;
    barre.style.width = progression + '%';
    pourcentage.textContent = progression + '%';
}, 50); // Augmenter de 1% toutes les 50ms
```

### Exemple 5 : Animation de texte clignotant

```html
<h2 id="texte">IMPORTANT</h2>
```

```javascript
const texte = document.getElementById('texte');
let visible = true;

setInterval(() => {
    if (visible) {
        texte.style.opacity = '0';
    } else {
        texte.style.opacity = '1';
    }
    visible = !visible;
}, 500); // Clignote toutes les 500ms
```

## clearInterval() - Arrêter un intervalle

### Syntaxe

```javascript
const intervalId = setInterval(fonction, intervalle);

// Arrêter l'intervalle
clearInterval(intervalId);
```

### Exemple : Arrêter après un certain temps

```javascript
let compteur = 0;

const intervalId = setInterval(() => {
    compteur++;
    console.log('Compteur :', compteur);

    // Arrêter après 5 exécutions
    if (compteur >= 5) {
        clearInterval(intervalId);
        console.log('Intervalle arrêté');
    }
}, 1000);

// Résultat :
// Compteur : 1
// Compteur : 2
// Compteur : 3
// Compteur : 4
// Compteur : 5
// Intervalle arrêté
```

## Différences setTimeout vs setInterval

| Critère | setTimeout | setInterval |
|---------|-----------|-------------|
| **Exécutions** | Une seule fois | Répété indéfiniment |
| **Usage** | Délai, action retardée | Horloge, animation, polling |
| **Arrêt** | clearTimeout() | clearInterval() |
| **Auto-arrêt** | Oui (après 1 exécution) | Non (continue jusqu'à clearInterval) |

### Exemple comparatif

```javascript
// setTimeout : exécute UNE fois après 2 secondes
setTimeout(() => {
    console.log('setTimeout : Une seule fois');
}, 2000);

// setInterval : exécute TOUTES LES 2 secondes
setInterval(() => {
    console.log('setInterval : Répété');
}, 2000);

// Résultat après 6 secondes :
// setTimeout : Une seule fois (1 fois)
// setInterval : Répété (3 fois)
```

## Pièges courants et solutions

### Piège 1 : Oublier de stocker l'ID

```javascript
// ❌ ERREUR : Impossible d'arrêter
setInterval(() => {
    console.log('Impossible à arrêter !');
}, 1000);

// ✅ CORRECT : Stocker l'ID
const intervalId = setInterval(() => {
    console.log('Peut être arrêté');
}, 1000);

// Plus tard
clearInterval(intervalId);
```

### Piège 2 : Oublier clearInterval

```javascript
// ❌ FUITE MÉMOIRE : L'intervalle continue même si l'élément est supprimé
function creerHorloge() {
    const div = document.createElement('div');

    setInterval(() => {
        div.textContent = new Date().toLocaleTimeString();
    }, 1000);

    document.body.appendChild(div);
}

creerHorloge();
// Si plus tard on supprime la div, l'intervalle continue en mémoire !

// ✅ CORRECT : Retourner l'ID pour pouvoir l'arrêter
function creerHorlogeCorrect() {
    const div = document.createElement('div');

    const intervalId = setInterval(() => {
        div.textContent = new Date().toLocaleTimeString();
    }, 1000);

    document.body.appendChild(div);

    return { div, intervalId }; // Retourner les deux
}

const horloge = creerHorlogeCorrect();
// Plus tard, pour nettoyer :
clearInterval(horloge.intervalId);
horloge.div.remove();
```

### Piège 3 : Utiliser setInterval pour setTimeout

```javascript
// ❌ MAUVAIS : Utiliser setInterval pour une seule exécution
const intervalId = setInterval(() => {
    console.log('Une seule fois');
    clearInterval(intervalId); // Doit s'arrêter manuellement
}, 1000);

// ✅ MIEUX : Utiliser setTimeout
setTimeout(() => {
    console.log('Une seule fois');
}, 1000); // S'arrête automatiquement
```

### Piège 4 : Le délai n'est pas exact

```javascript
// ⚠️ ATTENTION : Le délai est un MINIMUM, pas une garantie
setTimeout(() => {
    console.log('Environ 1 seconde');
}, 1000);

// Si le navigateur est occupé, ça peut prendre plus de 1 seconde
```

### Piège 5 : Interval drift (dérive temporelle)

```javascript
// ❌ PROBLÈME : setInterval peut dériver dans le temps
let compteur = 0;
setInterval(() => {
    compteur++;
    console.log(compteur);

    // Si cette opération prend du temps, l'intervalle dérive
    operationLongue();
}, 1000);

// ✅ SOLUTION : Utiliser setTimeout récursif
function executerChaqueSec() {
    compteur++;
    console.log(compteur);

    setTimeout(executerChaqueSec, 1000);
}
executerChaqueSec();
```

## setTimeout récursif vs setInterval

### Avec setInterval (intervalle fixe)

```javascript
setInterval(() => {
    console.log('Tick');
    // Si cette fonction prend 200ms, le prochain tick sera 800ms plus tard
}, 1000);

// Timeline :
// 0ms: Tick (prend 200ms)
// 1000ms: Tick (prend 200ms)
// 2000ms: Tick (prend 200ms)
```

### Avec setTimeout récursif (délai après exécution)

```javascript
function tick() {
    console.log('Tick');
    // Attend 1000ms APRÈS la fin de l'exécution
    setTimeout(tick, 1000);
}
tick();

// Timeline :
// 0ms: Tick (prend 200ms)
// 1200ms: Tick (prend 200ms)
// 2400ms: Tick (prend 200ms)
```

**Quand utiliser quoi ?**
- **setInterval** : Quand la fonction est rapide et le timing exact n'est pas critique
- **setTimeout récursif** : Quand vous voulez garantir un délai entre les exécutions

## Exemples avancés

### Exemple 1 : Système de notifications avec queue

```html
<div id="notifications"></div>
```

```javascript
const conteneur = document.getElementById('notifications');
const queue = [];

function afficherNotification(message) {
    const notif = document.createElement('div');
    notif.textContent = message;
    notif.style.cssText = 'background: blue; color: white; padding: 10px; margin: 5px;';
    conteneur.appendChild(notif);

    // Retirer après 3 secondes
    setTimeout(() => {
        notif.remove();
    }, 3000);
}

function traiterQueue() {
    if (queue.length > 0) {
        const message = queue.shift();
        afficherNotification(message);
    }
}

// Traiter la queue toutes les secondes
setInterval(traiterQueue, 1000);

// Utilisation
queue.push('Message 1');
queue.push('Message 2');
queue.push('Message 3');
// Les messages apparaissent un par un, toutes les secondes
```

### Exemple 2 : Auto-save (sauvegarde automatique)

```html
<textarea id="editeur" style="width: 100%; height: 200px;"></textarea>
<p id="statut">Non sauvegardé</p>
```

```javascript
const editeur = document.getElementById('editeur');
const statut = document.getElementById('statut');
let contenuPrecedent = '';
let aSauvegarder = false;

// Détecter les changements
editeur.addEventListener('input', () => {
    aSauvegarder = true;
    statut.textContent = 'Modifications non sauvegardées...';
});

// Vérifier toutes les 5 secondes s'il faut sauvegarder
setInterval(() => {
    if (aSauvegarder) {
        const contenu = editeur.value;

        // Simuler une sauvegarde
        console.log('Sauvegarde...', contenu);
        localStorage.setItem('brouillon', contenu);

        statut.textContent = '✓ Sauvegardé automatiquement';
        aSauvegarder = false;

        // Effacer le message après 2 secondes
        setTimeout(() => {
            statut.textContent = '';
        }, 2000);
    }
}, 5000);

// Charger le brouillon au démarrage
window.addEventListener('load', () => {
    const brouillon = localStorage.getItem('brouillon');
    if (brouillon) {
        editeur.value = brouillon;
    }
});
```

### Exemple 3 : Animation d'une balle qui rebondit

```html
<div id="terrain" style="width: 400px; height: 300px; border: 1px solid black; position: relative;">
    <div id="balle" style="width: 20px; height: 20px; background: red; border-radius: 50%; position: absolute; top: 0; left: 0;"></div>
</div>
```

```javascript
const balle = document.getElementById('balle');
let x = 0;
let y = 0;
let vitesseX = 2;
let vitesseY = 2;

const intervalId = setInterval(() => {
    // Mettre à jour la position
    x += vitesseX;
    y += vitesseY;

    // Rebondir sur les bords
    if (x >= 380 || x <= 0) {
        vitesseX = -vitesseX;
    }
    if (y >= 280 || y <= 0) {
        vitesseY = -vitesseY;
    }

    // Appliquer la position
    balle.style.left = x + 'px';
    balle.style.top = y + 'px';
}, 16); // ~60 FPS (1000ms / 60 = 16.6ms)
```

## Bonnes pratiques

### ✅ 1. Toujours stocker l'ID pour pouvoir arrêter

```javascript
// ✅ BIEN
const timerId = setTimeout(() => { }, 1000);
const intervalId = setInterval(() => { }, 1000);

// Pouvoir arrêter plus tard
clearTimeout(timerId);
clearInterval(intervalId);
```

### ✅ 2. Nettoyer les timers quand nécessaire

```javascript
// ✅ BIEN : Nettoyer au démontage d'un composant
class Composant {
    constructor() {
        this.intervalId = null;
    }

    demarrer() {
        this.intervalId = setInterval(() => {
            console.log('Tick');
        }, 1000);
    }

    arreter() {
        if (this.intervalId) {
            clearInterval(this.intervalId);
            this.intervalId = null;
        }
    }
}
```

### ✅ 3. Utiliser des constantes pour les délais

```javascript
// ✅ BIEN : Constantes nommées
const UNE_SECONDE = 1000;
const CINQ_SECONDES = 5000;

setTimeout(sauvegarder, CINQ_SECONDES);
setInterval(rafraichir, UNE_SECONDE);

// Au lieu de :
setTimeout(sauvegarder, 5000); // 5000 quoi ? Pas clair
```

### ✅ 4. Vérifier avant de clearTimeout/clearInterval

```javascript
// ✅ BIEN
if (timerId) {
    clearTimeout(timerId);
    timerId = null;
}

// Évite les erreurs si timerId est undefined ou déjà cleared
```

### ✅ 5. Préférer setTimeout récursif pour les opérations longues

```javascript
// ✅ BIEN pour opérations qui peuvent prendre du temps
function verifierMails() {
    // Opération potentiellement longue
    recupererMails().then(() => {
        // Attendre 30 secondes APRÈS avoir fini
        setTimeout(verifierMails, 30000);
    });
}
verifierMails();
```

## Ce qu'il faut retenir

✅ **setTimeout(fn, ms)** : exécute une fois après un délai

✅ **setInterval(fn, ms)** : exécute répétitivement à intervalles réguliers

✅ **clearTimeout(id)** : annule un setTimeout

✅ **clearInterval(id)** : arrête un setInterval

✅ **Toujours stocker l'ID** pour pouvoir arrêter

✅ **setInterval continue indéfiniment** : ne pas oublier clearInterval

✅ **Le délai est en millisecondes** (1000ms = 1 seconde)

✅ **Le délai n'est pas exact** : c'est un minimum

✅ **Nettoyer les timers** pour éviter les fuites mémoire

## Dans la prochaine leçon

Maintenant que vous maîtrisez setTimeout et setInterval, nous allons découvrir un problème courant en JavaScript asynchrone : le **callback hell** (l'enfer des callbacks).

Vous découvrirez :
- Ce qu'est le callback hell et pourquoi c'est problématique
- Les difficultés de gérer des opérations asynchrones imbriquées
- Pourquoi on a besoin de meilleures solutions (Promises, async/await)
- Des exemples concrets de code difficile à maintenir

---


⏭️ [Le problème des callbacks (callback hell)](/05-javascript-moderne-fondamentaux/11-programmation-asynchrone/03-callback-hell.md)
