🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.11 - removeEventListener

## Introduction

Nous avons appris à ajouter des écouteurs d'événements avec `addEventListener()`. Mais saviez-vous qu'il est tout aussi important de savoir les **retirer** ?

Retirer un écouteur d'événement permet de :
- **Libérer de la mémoire** (éviter les fuites mémoire)
- **Éviter des comportements indésirables** (actions multiples non voulues)
- **Améliorer les performances** (moins d'écouteurs actifs)
- **Gérer proprement le cycle de vie** de vos composants

Dans cette leçon, nous allons apprendre à utiliser `removeEventListener()` correctement.

## Syntaxe de base

```javascript
element.removeEventListener(type, fonction);
```

### Paramètres

- **`type`** : Le type d'événement (ex: `'click'`, `'keydown'`)
- **`fonction`** : La **même référence** de fonction utilisée dans `addEventListener()`

### Règle d'or

Pour pouvoir retirer un écouteur, vous devez utiliser **exactement la même référence de fonction** que lors de l'ajout.

## Exemple simple qui fonctionne

```html
<button id="bouton">Cliquez-moi</button>
<button id="arreter">Arrêter l'écouteur</button>
<p id="compteur">Clics : 0</p>
```

```javascript
const bouton = document.getElementById('bouton');
const arreter = document.getElementById('arreter');
const compteur = document.getElementById('compteur');
let nombre = 0;

// Fonction nommée (importante !)
function compterClics() {
    nombre++;
    compteur.textContent = `Clics : ${nombre}`;
}

// Ajouter l'écouteur
bouton.addEventListener('click', compterClics);

// Retirer l'écouteur
arreter.addEventListener('click', () => {
    bouton.removeEventListener('click', compterClics); // ✅ Fonctionne
    arreter.textContent = 'Écouteur retiré ✓';
    arreter.disabled = true;
});
```

**Pourquoi ça fonctionne ?**
- Nous utilisons une **fonction nommée** (`compterClics`)
- Nous passons la **même référence** à `removeEventListener()`

## Le piège des fonctions anonymes

### ❌ Ceci NE fonctionne PAS

```javascript
const bouton = document.getElementById('bouton');

// Ajouter avec une fonction anonyme
bouton.addEventListener('click', function() {
    console.log('Clic !');
});

// ❌ IMPOSSIBLE de retirer cette fonction !
bouton.removeEventListener('click', function() {
    console.log('Clic !');
});

// Pourquoi ? Les deux fonctions sont différentes !
// Même si le code est identique, ce sont deux objets distincts en mémoire
```

### Pourquoi ça ne marche pas ?

```javascript
// Chaque fonction anonyme est un objet unique
const fonction1 = function() { console.log('Hello'); };
const fonction2 = function() { console.log('Hello'); };

console.log(fonction1 === fonction2); // false
// Même si le code est identique, ce sont deux objets différents !
```

### ✅ Solution : Utiliser une fonction nommée

```javascript
const bouton = document.getElementById('bouton');

// Définir la fonction d'abord
function direBonjour() {
    console.log('Bonjour !');
}

// Ajouter
bouton.addEventListener('click', direBonjour);

// Retirer plus tard
bouton.removeEventListener('click', direBonjour); // ✅ Fonctionne !
```

### Alternative : Stocker la fonction fléchée

```javascript
const bouton = document.getElementById('bouton');

// Stocker la fonction fléchée dans une variable
const monGestionnaire = () => {
    console.log('Clic !');
};

// Ajouter
bouton.addEventListener('click', monGestionnaire);

// Retirer
bouton.removeEventListener('click', monGestionnaire); // ✅ Fonctionne !
```

## Cas d'usage pratiques

### Cas 1 : Événement qui ne doit se déclencher qu'une fois

```html
<button id="boutonUneFois">Cliquez une seule fois</button>
<p id="message"></p>
```

```javascript
const bouton = document.getElementById('boutonUneFois');
const message = document.getElementById('message');

function afficherMessage() {
    message.textContent = 'Vous avez cliqué ! (une seule fois)';

    // Se retirer automatiquement après la première exécution
    bouton.removeEventListener('click', afficherMessage);
    bouton.disabled = true;
}

bouton.addEventListener('click', afficherMessage);
```

**Alternative moderne : Option `once`**

```javascript
// ✅ Plus simple avec l'option { once: true }
bouton.addEventListener('click', () => {
    message.textContent = 'Vous avez cliqué ! (une seule fois)';
    bouton.disabled = true;
}, { once: true });

// L'écouteur est automatiquement retiré après le premier déclenchement
```

### Cas 2 : Activer/Désactiver un écouteur

```html
<button id="cible">Cible</button>
<button id="toggle">Activer/Désactiver</button>
<p id="statut">Actif</p>
```

```javascript
const cible = document.getElementById('cible');
const toggle = document.getElementById('toggle');
const statut = document.getElementById('statut');
let estActif = true;

function gererClic() {
    console.log('Clic sur la cible !');
}

// Ajouter l'écouteur initialement
cible.addEventListener('click', gererClic);

toggle.addEventListener('click', () => {
    if (estActif) {
        cible.removeEventListener('click', gererClic);
        statut.textContent = 'Inactif';
        toggle.textContent = 'Activer';
    } else {
        cible.addEventListener('click', gererClic);
        statut.textContent = 'Actif';
        toggle.textContent = 'Désactiver';
    }
    estActif = !estActif;
});
```

### Cas 3 : Nettoyage lors de la suppression d'un élément

```html
<div id="conteneur">
    <button id="ajouter">Ajouter un élément</button>
</div>
```

```javascript
const conteneur = document.getElementById('conteneur');
const btnAjouter = document.getElementById('ajouter');
let compteur = 0;

btnAjouter.addEventListener('click', () => {
    compteur++;
    const div = document.createElement('div');
    div.innerHTML = `
        Élément ${compteur}
        <button class="supprimer">Supprimer</button>
    `;

    const btnSupprimer = div.querySelector('.supprimer');

    // Fonction de suppression
    function supprimerElement() {
        // ⚠️ IMPORTANT : Retirer l'écouteur AVANT de supprimer l'élément
        btnSupprimer.removeEventListener('click', supprimerElement);
        div.remove();
        console.log(`Élément ${compteur} supprimé et nettoyé`);
    }

    btnSupprimer.addEventListener('click', supprimerElement);
    conteneur.appendChild(div);
});
```

### Cas 4 : Timer avec arrêt manuel

```html
<button id="demarrer">Démarrer</button>
<button id="arreter">Arrêter</button>
<p id="temps">0 secondes</p>
```

```javascript
const btnDemarrer = document.getElementById('demarrer');
const btnArreter = document.getElementById('arreter');
const temps = document.getElementById('temps');
let secondes = 0;
let intervalId = null;

function demarrerTimer() {
    if (intervalId) return; // Déjà en cours

    intervalId = setInterval(() => {
        secondes++;
        temps.textContent = `${secondes} secondes`;
    }, 1000);

    btnDemarrer.disabled = true;
    btnArreter.disabled = false;
}

function arreterTimer() {
    if (intervalId) {
        clearInterval(intervalId);
        intervalId = null;
    }

    btnDemarrer.disabled = false;
    btnArreter.disabled = true;
}

btnDemarrer.addEventListener('click', demarrerTimer);
btnArreter.addEventListener('click', arreterTimer);
```

### Cas 5 : Modal avec gestion propre des événements

```html
<button id="ouvrirModal">Ouvrir la modal</button>

<div id="modal" style="display: none;">
    <div class="modal-content">
        <h2>Ma Modal</h2>
        <p>Contenu de la modal</p>
        <button id="fermerModal">Fermer</button>
    </div>
</div>
<div id="overlay" style="display: none;"></div>
```

```javascript
const btnOuvrir = document.getElementById('ouvrirModal');
const modal = document.getElementById('modal');
const overlay = document.getElementById('overlay');
const btnFermer = document.getElementById('fermerModal');

function fermerModal() {
    modal.style.display = 'none';
    overlay.style.display = 'none';

    // ⚠️ IMPORTANT : Retirer les écouteurs temporaires
    document.removeEventListener('keydown', gererEchap);
    overlay.removeEventListener('click', fermerModal);
}

function gererEchap(event) {
    if (event.key === 'Escape') {
        fermerModal();
    }
}

function ouvrirModal() {
    modal.style.display = 'block';
    overlay.style.display = 'block';

    // Ajouter des écouteurs temporaires
    document.addEventListener('keydown', gererEchap);
    overlay.addEventListener('click', fermerModal);
}

btnOuvrir.addEventListener('click', ouvrirModal);
btnFermer.addEventListener('click', fermerModal);
```

## Gestion de la mémoire et fuites mémoire

### Qu'est-ce qu'une fuite mémoire ?

Une **fuite mémoire** se produit quand votre application garde en mémoire des objets qui ne sont plus utilisés. Avec les événements, cela arrive quand :
- Vous supprimez un élément DOM sans retirer ses écouteurs
- Vous ajoutez des écouteurs en boucle sans jamais les retirer

### Exemple de fuite mémoire

```javascript
// ❌ FUITE MÉMOIRE POTENTIELLE
const conteneur = document.getElementById('conteneur');

for (let i = 0; i < 1000; i++) {
    const div = document.createElement('div');
    div.textContent = `Élément ${i}`;

    // Ajouter un écouteur
    div.addEventListener('click', function() {
        console.log(`Cliqué sur ${i}`);
    });

    conteneur.appendChild(div);
}

// Plus tard, si vous faites :
conteneur.innerHTML = ''; // ❌ Les écouteurs restent en mémoire !
```

**Pourquoi c'est un problème ?**
- Les 1000 fonctions restent en mémoire
- Si vous répétez cette opération, la mémoire s'accumule
- L'application devient de plus en plus lente

### ✅ Solution 1 : Utiliser la délégation

```javascript
// ✅ MEILLEUR : Délégation d'événements (1 seul écouteur)
const conteneur = document.getElementById('conteneur');

for (let i = 0; i < 1000; i++) {
    const div = document.createElement('div');
    div.textContent = `Élément ${i}`;
    div.dataset.index = i;
    conteneur.appendChild(div);
}

// Un seul écouteur sur le parent
conteneur.addEventListener('click', (event) => {
    if (event.target.dataset.index) {
        console.log(`Cliqué sur ${event.target.dataset.index}`);
    }
});

// Nettoyer est simple
conteneur.innerHTML = ''; // Pas de fuite mémoire
```

### ✅ Solution 2 : Retirer les écouteurs explicitement

```javascript
// ✅ CORRECT : Retirer les écouteurs avant de supprimer
const conteneur = document.getElementById('conteneur');
const ecouteurs = new Map(); // Stocker les références

for (let i = 0; i < 1000; i++) {
    const div = document.createElement('div');
    div.textContent = `Élément ${i}`;

    const gestionnaire = () => console.log(`Cliqué sur ${i}`);
    div.addEventListener('click', gestionnaire);

    ecouteurs.set(div, gestionnaire); // Stocker la référence
    conteneur.appendChild(div);
}

// Nettoyer proprement
function nettoyerConteneur() {
    conteneur.querySelectorAll('div').forEach(div => {
        const gestionnaire = ecouteurs.get(div);
        if (gestionnaire) {
            div.removeEventListener('click', gestionnaire);
            ecouteurs.delete(div);
        }
    });
    conteneur.innerHTML = '';
}
```

## Options de addEventListener et removeEventListener

Les deux méthodes peuvent accepter un troisième paramètre optionnel.

### Options disponibles

```javascript
element.addEventListener('click', fonction, {
    capture: false,  // Phase de capturing ou bubbling
    once: false,     // Retirer automatiquement après 1 déclenchement
    passive: false   // Ne jamais appeler preventDefault()
});
```

### Option `once` - Retrait automatique

```javascript
// L'écouteur est automatiquement retiré après le premier déclenchement
bouton.addEventListener('click', () => {
    console.log('Ne se déclenche qu\'une fois');
}, { once: true });

// Équivalent à :
function direBonjour() {
    console.log('Ne se déclenche qu\'une fois');
    bouton.removeEventListener('click', direBonjour);
}
bouton.addEventListener('click', direBonjour);
```

### ⚠️ Important pour removeEventListener

Pour retirer un écouteur avec options, vous devez passer **les mêmes options** :

```javascript
const options = { capture: true };

// Ajouter
element.addEventListener('click', maFonction, options);

// Retirer avec les MÊMES options
element.removeEventListener('click', maFonction, options); // ✅

// ❌ Ceci ne fonctionne PAS
element.removeEventListener('click', maFonction); // Options différentes
```

## Patterns de gestion des écouteurs

### Pattern 1 : Classe avec nettoyage

```javascript
class Composant {
    constructor(element) {
        this.element = element;
        this.ecouteurs = [];

        this.init();
    }

    // Ajouter un écouteur et le mémoriser
    ajouterEcouteur(type, handler) {
        this.element.addEventListener(type, handler);
        this.ecouteurs.push({ type, handler });
    }

    // Retirer tous les écouteurs
    nettoyer() {
        this.ecouteurs.forEach(({ type, handler }) => {
            this.element.removeEventListener(type, handler);
        });
        this.ecouteurs = [];
    }

    init() {
        this.ajouterEcouteur('click', () => {
            console.log('Clic');
        });

        this.ajouterEcouteur('mouseover', () => {
            console.log('Survol');
        });
    }
}

// Utilisation
const element = document.getElementById('monElement');
const composant = new Composant(element);

// Plus tard, nettoyer complètement
composant.nettoyer();
```

### Pattern 2 : AbortController (moderne)

```javascript
// ✅ MODERNE : Utiliser AbortController pour gérer plusieurs écouteurs
const controller = new AbortController();
const signal = controller.signal;

// Ajouter plusieurs écouteurs avec le même signal
bouton.addEventListener('click', handler1, { signal });
bouton.addEventListener('mouseover', handler2, { signal });
document.addEventListener('keydown', handler3, { signal });

// Retirer TOUS les écouteurs d'un coup
controller.abort(); // ✅ Tous les écouteurs sont retirés !
```

**Exemple pratique avec AbortController :**

```javascript
const bouton = document.getElementById('bouton');
const statut = document.getElementById('statut');
let controller = null;

function demarrerEcoute() {
    // Créer un nouveau controller
    controller = new AbortController();
    const signal = controller.signal;

    // Ajouter plusieurs écouteurs
    bouton.addEventListener('click', () => {
        console.log('Clic');
    }, { signal });

    bouton.addEventListener('mouseover', () => {
        statut.textContent = 'Survolé';
    }, { signal });

    bouton.addEventListener('mouseout', () => {
        statut.textContent = '';
    }, { signal });

    console.log('Écoute démarrée');
}

function arreterEcoute() {
    if (controller) {
        controller.abort(); // Retirer tous les écouteurs
        controller = null;
        console.log('Écoute arrêtée');
    }
}

// Utilisation
demarrerEcoute();
// ... plus tard
arreterEcoute();
```

### Pattern 3 : Gestion avec WeakMap

```javascript
// Pour des cas avancés : associer des données aux éléments
const ecouteursParElement = new WeakMap();

function ajouterEcouteurGere(element, type, handler) {
    element.addEventListener(type, handler);

    if (!ecouteursParElement.has(element)) {
        ecouteursParElement.set(element, []);
    }

    ecouteursParElement.get(element).push({ type, handler });
}

function retirerTousLesEcouteurs(element) {
    const ecouteurs = ecouteursParElement.get(element);

    if (ecouteurs) {
        ecouteurs.forEach(({ type, handler }) => {
            element.removeEventListener(type, handler);
        });
        ecouteursParElement.delete(element);
    }
}
```

## Debugging : Vérifier les écouteurs actifs

### Chrome DevTools

1. Ouvrir les DevTools (F12)
2. Onglet "Elements"
3. Sélectionner un élément
4. Panneau "Event Listeners" à droite
5. Voir tous les écouteurs attachés

### Console API : getEventListeners()

```javascript
// Dans la console Chrome uniquement
const bouton = document.getElementById('bouton');
getEventListeners(bouton);

// Affiche tous les écouteurs actifs sur l'élément
```

### Ajouter des logs pour tracer

```javascript
function ajouterEcouteurAvecLog(element, type, handler, nom) {
    console.log(`➕ Ajout écouteur "${nom}" (${type})`);
    element.addEventListener(type, handler);
}

function retirerEcouteurAvecLog(element, type, handler, nom) {
    console.log(`➖ Retrait écouteur "${nom}" (${type})`);
    element.removeEventListener(type, handler);
}

// Utilisation
const monHandler = () => console.log('Clic');
ajouterEcouteurAvecLog(bouton, 'click', monHandler, 'Handler principal');
retirerEcouteurAvecLog(bouton, 'click', monHandler, 'Handler principal');
```

## Erreurs fréquentes

### Erreur 1 : Fonction anonyme

```javascript
// ❌ ERREUR : Impossible de retirer
bouton.addEventListener('click', () => console.log('Clic'));
bouton.removeEventListener('click', () => console.log('Clic')); // Ne marche pas

// ✅ CORRECT
const handler = () => console.log('Clic');
bouton.addEventListener('click', handler);
bouton.removeEventListener('click', handler);
```

### Erreur 2 : Mauvais paramètres

```javascript
// ❌ ERREUR : Type d'événement différent
bouton.addEventListener('click', handler);
bouton.removeEventListener('mousedown', handler); // Type différent !

// ✅ CORRECT
bouton.addEventListener('click', handler);
bouton.removeEventListener('click', handler);
```

### Erreur 3 : Options différentes

```javascript
// ❌ ERREUR : Options différentes
bouton.addEventListener('click', handler, { capture: true });
bouton.removeEventListener('click', handler); // Options manquantes

// ✅ CORRECT
const options = { capture: true };
bouton.addEventListener('click', handler, options);
bouton.removeEventListener('click', handler, options);
```

### Erreur 4 : Retirer un écouteur qui n'existe pas

```javascript
// ⚠️ Pas d'erreur, mais aucun effet
bouton.removeEventListener('click', handler); // Si jamais ajouté

// JavaScript ne génère PAS d'erreur si l'écouteur n'existe pas
// Il ignore simplement l'appel
```

## Bonnes pratiques

### ✅ 1. Toujours utiliser des fonctions nommées ou stockées

```javascript
// ✅ BIEN
const handler = () => { };
element.addEventListener('click', handler);
element.removeEventListener('click', handler);

// ❌ ÉVITER
element.addEventListener('click', () => { });
```

### ✅ 2. Nettoyer lors de la suppression d'éléments

```javascript
// ✅ BIEN
function supprimerElement(element) {
    // Retirer les écouteurs d'abord
    element.removeEventListener('click', handler);
    // Puis supprimer
    element.remove();
}
```

### ✅ 3. Préférer la délégation quand possible

```javascript
// ✅ MEILLEUR : Pas besoin de removeEventListener
parent.addEventListener('click', (event) => {
    if (event.target.matches('.item')) {
        // Gestion
    }
});
```

### ✅ 4. Utiliser { once: true } pour les actions uniques

```javascript
// ✅ SIMPLE ET CLAIR
bouton.addEventListener('click', handler, { once: true });

// Au lieu de :
function handler() {
    // Code
    bouton.removeEventListener('click', handler);
}
```

### ✅ 5. Utiliser AbortController pour plusieurs écouteurs

```javascript
// ✅ MODERNE ET PRATIQUE
const controller = new AbortController();
element.addEventListener('click', h1, { signal: controller.signal });
element.addEventListener('mouseover', h2, { signal: controller.signal });

// Retirer tous en une fois
controller.abort();
```

### ✅ 6. Documenter pourquoi vous retirez un écouteur

```javascript
// ✅ BIEN DOCUMENTÉ
function fermerModal() {
    modal.style.display = 'none';

    // Retirer l'écouteur Escape car la modal est fermée
    document.removeEventListener('keydown', gererEchap);
}
```

## Tableau récapitulatif

| Situation | Recommandation |
|-----------|----------------|
| **Action unique** | Utiliser `{ once: true }` |
| **Plusieurs écouteurs** | Utiliser `AbortController` |
| **Élément supprimé** | Retirer écouteurs avant suppression |
| **Nombreux éléments** | Utiliser délégation (éviter add/remove) |
| **Modal temporaire** | Retirer écouteurs à la fermeture |
| **Fonction anonyme** | ❌ Impossible à retirer |
| **Fonction nommée** | ✅ Retrait possible |

## Ce qu'il faut retenir

✅ **removeEventListener()** retire un écouteur d'événement

✅ **Même référence de fonction** requise (pas de fonctions anonymes !)

✅ **Nettoyer les écouteurs** pour éviter les fuites mémoire

✅ **{ once: true }** : retrait automatique après 1 déclenchement

✅ **AbortController** : retirer plusieurs écouteurs d'un coup (moderne)

✅ **Préférer la délégation** pour éviter d'avoir à gérer add/remove

✅ **Debugging** : Chrome DevTools > Event Listeners

✅ **Pas d'erreur** si vous essayez de retirer un écouteur inexistant

## Conclusion du chapitre sur les événements

Félicitations ! Vous avez terminé le chapitre complet sur les événements JavaScript. Vous maîtrisez maintenant :

1. ✅ Les principes des événements
2. ✅ addEventListener() - la méthode moderne
3. ✅ Les événements de souris
4. ✅ Les événements de clavier
5. ✅ Les événements de formulaire
6. ✅ L'objet Event et ses propriétés
7. ✅ target vs currentTarget
8. ✅ La propagation (bubbling et capturing)
9. ✅ preventDefault() et stopPropagation()
10. ✅ La délégation d'événements
11. ✅ removeEventListener()

Vous êtes maintenant capable de créer des interfaces web riches et interactives !

---


⏭️ [Programmation asynchrone (Introduction)](/05-javascript-moderne-fondamentaux/11-programmation-asynchrone/README.md)
