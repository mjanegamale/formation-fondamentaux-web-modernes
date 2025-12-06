🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.4 - Événements de clavier

## Introduction

Les événements de clavier permettent de détecter quand l'utilisateur appuie sur une touche du clavier. Ils sont essentiels pour créer des interactions riches : raccourcis clavier, jeux, formulaires intelligents, éditeurs de texte, et bien plus encore.

Dans cette leçon, nous allons explorer les événements de clavier et apprendre à détecter précisément quelle touche a été pressée.

## Les événements de clavier

Il existe deux événements principaux pour le clavier :

| Événement | Se déclenche quand... | Utilisation courante |
|-----------|----------------------|---------------------|
| `keydown` | Une touche est **enfoncée** | Détection de touches, raccourcis, jeux |
| `keyup` | Une touche est **relâchée** | Fin d'action, validation |
| ~~`keypress`~~ | ❌ **Déprécié** - Ne plus utiliser | Remplacé par `keydown` |

> **Important** : `keypress` est déprécié et ne doit plus être utilisé. Utilisez toujours `keydown` à la place.

## 1. L'événement keydown

### Quand se déclenche-t-il ?

L'événement `keydown` se déclenche dès qu'une touche du clavier est **enfoncée**, avant même que le caractère n'apparaisse à l'écran.

### Exemple simple

```html
<input type="text" id="champTexte" placeholder="Tapez quelque chose">
<p id="message"></p>
```

```javascript
const champ = document.getElementById('champTexte');
const message = document.getElementById('message');

champ.addEventListener('keydown', () => {
    message.textContent = 'Vous avez appuyé sur une touche !';
});
```

### Caractéristique importante : Répétition automatique

Si vous **maintenez** une touche enfoncée, l'événement `keydown` se déclenche **en continu** (répétition automatique) :

```javascript
let compteur = 0;

champ.addEventListener('keydown', () => {
    compteur++;
    console.log(`keydown déclenché ${compteur} fois`);
});

// Si vous maintenez une touche : 1, 2, 3, 4, 5...
```

## 2. L'événement keyup

### Quand se déclenche-t-il ?

L'événement `keyup` se déclenche quand une touche du clavier est **relâchée**.

### Exemple

```html
<input type="text" id="champTexte" placeholder="Tapez quelque chose">
<p id="status"></p>
```

```javascript
const champ = document.getElementById('champTexte');
const status = document.getElementById('status');

champ.addEventListener('keydown', () => {
    status.textContent = '⌨️ Touche enfoncée';
    status.style.color = 'red';
});

champ.addEventListener('keyup', () => {
    status.textContent = '✓ Touche relâchée';
    status.style.color = 'green';
});
```

### Différence clé avec keydown

- **keydown** : Se déclenche **en continu** si vous maintenez la touche
- **keyup** : Se déclenche **une seule fois** quand vous relâchez

## Détecter quelle touche a été pressée

L'objet `KeyboardEvent` contient toutes les informations sur la touche pressée.

### La propriété `key` (recommandée)

La propriété `key` renvoie la valeur de la touche pressée sous forme de chaîne :

```javascript
document.addEventListener('keydown', (event) => {
    console.log('Touche pressée :', event.key);
});

// Exemples de valeurs :
// 'a', 'b', 'c' pour les lettres
// '1', '2', '3' pour les chiffres
// 'Enter' pour Entrée
// ' ' (espace) pour la barre d'espace
// 'ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight' pour les flèches
// 'Escape' pour Échap
// 'Shift', 'Control', 'Alt' pour les modificateurs
```

### Exemple : Réagir à la touche Enter

```html
<input type="text" id="champNom" placeholder="Entrez votre nom">
<p id="salutation"></p>
```

```javascript
const champ = document.getElementById('champNom');
const salutation = document.getElementById('salutation');

champ.addEventListener('keydown', (event) => {
    if (event.key === 'Enter') {
        salutation.textContent = `Bonjour ${champ.value} !`;
    }
});
```

### Exemple : Navigation avec les flèches

```html
<div id="personnage" style="position: absolute; top: 100px; left: 100px; width: 50px; height: 50px; background: red; border-radius: 50%;"></div>
<p>Utilisez les flèches pour déplacer le personnage</p>
```

```javascript
const personnage = document.getElementById('personnage');
let positionX = 100;
let positionY = 100;
const vitesse = 10;

document.addEventListener('keydown', (event) => {
    if (event.key === 'ArrowUp') {
        positionY -= vitesse;
        personnage.style.top = positionY + 'px';
    } else if (event.key === 'ArrowDown') {
        positionY += vitesse;
        personnage.style.top = positionY + 'px';
    } else if (event.key === 'ArrowLeft') {
        positionX -= vitesse;
        personnage.style.left = positionX + 'px';
    } else if (event.key === 'ArrowRight') {
        positionX += vitesse;
        personnage.style.left = positionX + 'px';
    }
});
```

### La propriété `code` (position physique de la touche)

La propriété `code` renvoie le code de la touche basé sur sa **position physique** sur le clavier :

```javascript
document.addEventListener('keydown', (event) => {
    console.log('Code :', event.code);
    console.log('Key :', event.key);
});

// Exemples :
// Code: 'KeyA', Key: 'a' (ou 'A' si Maj enfoncé)
// Code: 'Digit1', Key: '1'
// Code: 'Enter', Key: 'Enter'
// Code: 'Space', Key: ' '
```

### Quand utiliser `key` ou `code` ?

| Situation | Propriété à utiliser | Raison |
|-----------|---------------------|--------|
| Détection de caractères (a, b, c, 1, 2) | `key` | Prend en compte le layout du clavier |
| Raccourcis clavier (Ctrl+S) | `key` | Plus intuitif |
| Jeux vidéo (WASD pour bouger) | `code` | Position physique constante |
| Touches spéciales (Enter, Escape) | `key` | Plus lisible |

### ⚠️ Propriété `keyCode` (obsolète)

Vous verrez peut-être `event.keyCode` dans du vieux code. **Ne l'utilisez plus**, c'est déprécié :

```javascript
// ❌ DÉPRÉCIÉ - Ne faites pas ça
if (event.keyCode === 13) { // 13 = Enter
    // Code...
}

// ✅ MODERNE - Faites ça
if (event.key === 'Enter') {
    // Code...
}
```

## Touches modificatrices (Ctrl, Shift, Alt)

Les touches modificatrices peuvent être détectées via des propriétés booléennes de l'événement.

### Propriétés disponibles

```javascript
document.addEventListener('keydown', (event) => {
    console.log('Ctrl enfoncé ?', event.ctrlKey);   // true ou false
    console.log('Shift enfoncé ?', event.shiftKey); // true ou false
    console.log('Alt enfoncé ?', event.altKey);     // true ou false
    console.log('Meta enfoncé ?', event.metaKey);   // Cmd (Mac) ou Win (Windows)
});
```

### Exemple : Raccourci Ctrl+S pour sauvegarder

```html
<textarea id="editeur" style="width: 100%; height: 200px;" placeholder="Écrivez quelque chose..."></textarea>
<p id="status">Non sauvegardé</p>
```

```javascript
const editeur = document.getElementById('editeur');
const status = document.getElementById('status');

document.addEventListener('keydown', (event) => {
    // Ctrl+S (ou Cmd+S sur Mac)
    if ((event.ctrlKey || event.metaKey) && event.key === 's') {
        event.preventDefault(); // Empêche la sauvegarde native du navigateur

        // Simuler une sauvegarde
        status.textContent = '✓ Sauvegardé !';
        status.style.color = 'green';

        setTimeout(() => {
            status.textContent = 'Non sauvegardé';
            status.style.color = 'black';
        }, 2000);
    }
});
```

### Exemple : Raccourcis clavier multiples

```html
<div id="contenu">
    <h2>Raccourcis disponibles :</h2>
    <ul>
        <li>Ctrl+B : Texte en gras</li>
        <li>Ctrl+I : Texte en italique</li>
        <li>Ctrl+U : Texte souligné</li>
    </ul>
    <div id="demo" contenteditable="true" style="border: 1px solid #ddd; padding: 10px; min-height: 100px;">
        Sélectionnez du texte et utilisez les raccourcis
    </div>
</div>
```

```javascript
document.addEventListener('keydown', (event) => {
    if (event.ctrlKey || event.metaKey) {
        if (event.key === 'b') {
            event.preventDefault();
            document.execCommand('bold');
        } else if (event.key === 'i') {
            event.preventDefault();
            document.execCommand('italic');
        } else if (event.key === 'u') {
            event.preventDefault();
            document.execCommand('underline');
        }
    }
});
```

## Combinaisons de touches courantes

Voici des exemples de combinaisons de touches fréquemment utilisées :

```javascript
document.addEventListener('keydown', (event) => {

    // Ctrl+S ou Cmd+S : Sauvegarder
    if ((event.ctrlKey || event.metaKey) && event.key === 's') {
        event.preventDefault();
        console.log('Sauvegarder');
    }

    // Ctrl+Z ou Cmd+Z : Annuler
    if ((event.ctrlKey || event.metaKey) && event.key === 'z') {
        event.preventDefault();
        console.log('Annuler');
    }

    // Ctrl+Shift+Z : Rétablir
    if ((event.ctrlKey || event.metaKey) && event.shiftKey && event.key === 'z') {
        event.preventDefault();
        console.log('Rétablir');
    }

    // Ctrl+C : Copier
    if ((event.ctrlKey || event.metaKey) && event.key === 'c') {
        console.log('Copier');
    }

    // Ctrl+V : Coller
    if ((event.ctrlKey || event.metaKey) && event.key === 'v') {
        console.log('Coller');
    }

    // Escape : Fermer/Annuler
    if (event.key === 'Escape') {
        console.log('Échap pressé');
    }
});
```

## Empêcher le comportement par défaut

Certaines touches ont un comportement par défaut dans le navigateur. Utilisez `event.preventDefault()` pour l'empêcher.

### Exemple : Empêcher la tabulation

```html
<input type="text" id="champ1" placeholder="Champ 1">
<input type="text" id="champ2" placeholder="Champ 2">
<p>Essayez d'appuyer sur Tab dans le premier champ</p>
```

```javascript
const champ1 = document.getElementById('champ1');

champ1.addEventListener('keydown', (event) => {
    if (event.key === 'Tab') {
        event.preventDefault();
        console.log('Tab bloqué !');
    }
});
```

### Exemple : Empêcher la touche Espace dans un champ

```html
<input type="text" id="username" placeholder="Nom d'utilisateur (sans espaces)">
```

```javascript
const username = document.getElementById('username');

username.addEventListener('keydown', (event) => {
    if (event.key === ' ') {
        event.preventDefault();
        console.log('Les espaces ne sont pas autorisés');
    }
});
```

## Exemples pratiques complets

### Exemple 1 : Validateur de formulaire en temps réel

```html
<input type="password" id="motDePasse" placeholder="Mot de passe">
<div id="force">
    <div id="barreForce" style="width: 0%; height: 5px; background: red; transition: width 0.3s;"></div>
</div>
<p id="message"></p>
```

```javascript
const motDePasse = document.getElementById('motDePasse');
const barreForce = document.getElementById('barreForce');
const message = document.getElementById('message');

motDePasse.addEventListener('keyup', () => {
    const mdp = motDePasse.value;
    let force = 0;

    if (mdp.length >= 8) force += 25;
    if (/[a-z]/.test(mdp) && /[A-Z]/.test(mdp)) force += 25;
    if (/[0-9]/.test(mdp)) force += 25;
    if (/[^a-zA-Z0-9]/.test(mdp)) force += 25;

    barreForce.style.width = force + '%';

    if (force <= 25) {
        barreForce.style.backgroundColor = 'red';
        message.textContent = 'Faible';
    } else if (force <= 50) {
        barreForce.style.backgroundColor = 'orange';
        message.textContent = 'Moyen';
    } else if (force <= 75) {
        barreForce.style.backgroundColor = 'yellow';
        message.textContent = 'Bon';
    } else {
        barreForce.style.backgroundColor = 'green';
        message.textContent = 'Excellent';
    }
});
```

### Exemple 2 : Recherche instantanée

```html
<input type="text" id="recherche" placeholder="Rechercher...">
<ul id="resultats"></ul>
```

```javascript
const recherche = document.getElementById('recherche');
const resultats = document.getElementById('resultats');

const donnees = [
    'JavaScript', 'Python', 'Java', 'C++', 'Ruby',
    'PHP', 'Swift', 'Kotlin', 'TypeScript', 'Go'
];

recherche.addEventListener('keyup', () => {
    const terme = recherche.value.toLowerCase();
    resultats.innerHTML = '';

    if (terme.length > 0) {
        const correspondances = donnees.filter(item =>
            item.toLowerCase().includes(terme)
        );

        correspondances.forEach(item => {
            const li = document.createElement('li');
            li.textContent = item;
            resultats.appendChild(li);
        });
    }
});
```

### Exemple 3 : Jeu simple (attraper les lettres)

```html
<div id="jeu" style="width: 400px; height: 300px; border: 2px solid black; position: relative; background: #f0f0f0;">
    <div id="score">Score : 0</div>
    <div id="lettreCible" style="position: absolute; font-size: 48px; font-weight: bold;"></div>
</div>
<p id="instructions">Appuyez sur la lettre affichée !</p>
```

```javascript
const jeu = document.getElementById('jeu');
const lettreCible = document.getElementById('lettreCible');
const scoreElement = document.getElementById('score');
let score = 0;
let lettreActuelle = '';

function genererLettre() {
    const lettres = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    lettreActuelle = lettres[Math.floor(Math.random() * lettres.length)];
    lettreCible.textContent = lettreActuelle;

    // Position aléatoire
    lettreCible.style.left = Math.random() * 350 + 'px';
    lettreCible.style.top = Math.random() * 250 + 'px';
}

document.addEventListener('keydown', (event) => {
    if (event.key.toUpperCase() === lettreActuelle) {
        score++;
        scoreElement.textContent = 'Score : ' + score;
        genererLettre();
    }
});

// Démarrer le jeu
genererLettre();
```

### Exemple 4 : Calculatrice au clavier

```html
<div id="calculatrice">
    <input type="text" id="affichage" readonly style="width: 200px; font-size: 24px; text-align: right;">
    <p>Utilisez les chiffres et +, -, *, /, Enter pour calculer</p>
</div>
```

```javascript
const affichage = document.getElementById('affichage');
let valeurActuelle = '';

document.addEventListener('keydown', (event) => {
    const touche = event.key;

    // Chiffres
    if (/^[0-9]$/.test(touche)) {
        valeurActuelle += touche;
        affichage.value = valeurActuelle;
    }

    // Opérateurs
    if (['+', '-', '*', '/'].includes(touche)) {
        valeurActuelle += ' ' + touche + ' ';
        affichage.value = valeurActuelle;
    }

    // Point décimal
    if (touche === '.') {
        valeurActuelle += touche;
        affichage.value = valeurActuelle;
    }

    // Calculer (Enter)
    if (touche === 'Enter') {
        try {
            const resultat = eval(valeurActuelle);
            affichage.value = resultat;
            valeurActuelle = resultat.toString();
        } catch (e) {
            affichage.value = 'Erreur';
            valeurActuelle = '';
        }
    }

    // Effacer (Escape ou Backspace)
    if (touche === 'Escape') {
        valeurActuelle = '';
        affichage.value = '';
    }

    if (touche === 'Backspace') {
        valeurActuelle = valeurActuelle.slice(0, -1);
        affichage.value = valeurActuelle;
    }
});
```

## Touches spéciales : valeurs de la propriété `key`

Voici les valeurs courantes de `event.key` pour les touches spéciales :

### Touches de navigation
```javascript
'ArrowUp'      // Flèche haut
'ArrowDown'    // Flèche bas
'ArrowLeft'    // Flèche gauche
'ArrowRight'   // Flèche droite
'Home'         // Début
'End'          // Fin
'PageUp'       // Page précédente
'PageDown'     // Page suivante
```

### Touches d'édition
```javascript
'Backspace'    // Retour arrière
'Delete'       // Supprimer
'Enter'        // Entrée
'Tab'          // Tabulation
'Escape'       // Échap
' '            // Espace (caractère espace)
```

### Touches de fonction
```javascript
'F1', 'F2', 'F3', ..., 'F12'  // Touches F1 à F12
```

### Touches modificatrices
```javascript
'Shift'        // Majuscule
'Control'      // Ctrl
'Alt'          // Alt
'Meta'         // Cmd (Mac) ou Win (Windows)
'CapsLock'     // Verrouillage majuscules
```

## Propriétés utiles de KeyboardEvent

Voici un résumé des propriétés les plus utilisées :

```javascript
document.addEventListener('keydown', (event) => {
    // Informations sur la touche
    console.log('key:', event.key);           // Valeur de la touche
    console.log('code:', event.code);         // Code de position physique
    console.log('keyCode:', event.keyCode);   // ❌ Déprécié, ne pas utiliser

    // Touches modificatrices
    console.log('ctrlKey:', event.ctrlKey);   // Ctrl enfoncé ?
    console.log('shiftKey:', event.shiftKey); // Shift enfoncé ?
    console.log('altKey:', event.altKey);     // Alt enfoncé ?
    console.log('metaKey:', event.metaKey);   // Meta (Cmd/Win) enfoncé ?

    // Répétition
    console.log('repeat:', event.repeat);     // true si maintenu

    // Type d'événement
    console.log('type:', event.type);         // 'keydown' ou 'keyup'

    // Élément cible
    console.log('target:', event.target);     // L'élément qui a le focus
});
```

## Bonnes pratiques

### ✅ 1. Utiliser `key` au lieu de `keyCode`

```javascript
// ✅ BIEN - Moderne et lisible
if (event.key === 'Enter') { }

// ❌ ÉVITER - Déprécié
if (event.keyCode === 13) { }
```

### ✅ 2. Vérifier Ctrl ET Meta pour les raccourcis (compatibilité Mac)

```javascript
// ✅ BIEN - Fonctionne sur Mac et Windows
if ((event.ctrlKey || event.metaKey) && event.key === 's') {
    event.preventDefault();
    sauvegarder();
}

// ⚠️ PAS OPTIMAL - Ne marche pas sur Mac
if (event.ctrlKey && event.key === 's') {
    sauvegarder();
}
```

### ✅ 3. Utiliser keydown pour la plupart des cas

```javascript
// ✅ BIEN - Réagit immédiatement
document.addEventListener('keydown', handleKey);

// ⚠️ MOINS RÉACTIF - Attend que la touche soit relâchée
document.addEventListener('keyup', handleKey);
```

### ✅ 4. Nettoyer les événements globaux

Si vous attachez des événements au `document`, pensez à les retirer quand nécessaire :

```javascript
function handleKeyPress(event) {
    console.log(event.key);
}

// Ajouter
document.addEventListener('keydown', handleKeyPress);

// Retirer quand vous n'en avez plus besoin
document.removeEventListener('keydown', handleKeyPress);
```

### ✅ 5. Attention aux champs de formulaire

Les événements de clavier sur `document` se déclenchent aussi dans les champs de formulaire :

```javascript
document.addEventListener('keydown', (event) => {
    // Ignorer si l'utilisateur tape dans un input
    if (event.target.tagName === 'INPUT' || event.target.tagName === 'TEXTAREA') {
        return;
    }

    // Votre code pour les raccourcis globaux
    if (event.key === 'Escape') {
        fermerModal();
    }
});
```

## Différence entre keydown et keyup

### Tableau comparatif

| Critère | keydown | keyup |
|---------|---------|-------|
| **Déclenchement** | Touche enfoncée | Touche relâchée |
| **Répétition** | ✅ Oui (si maintenu) | ❌ Non |
| **Vitesse** | Plus rapide | Plus lent |
| **Usage typique** | Raccourcis, jeux, navigation | Validation, fin d'action |
| **Recommandé pour** | La plupart des cas | Cas spécifiques |

### Exemple visuel de la différence

```html
<input type="text" id="demo">
<p>keydown : <span id="countDown">0</span></p>
<p>keyup : <span id="countUp">0</span></p>
```

```javascript
const demo = document.getElementById('demo');
const countDown = document.getElementById('countDown');
const countUp = document.getElementById('countUp');
let compteurDown = 0;
let compteurUp = 0;

demo.addEventListener('keydown', () => {
    compteurDown++;
    countDown.textContent = compteurDown;
});

demo.addEventListener('keyup', () => {
    compteurUp++;
    countUp.textContent = compteurUp;
});

// Maintenez une touche : keydown augmente rapidement,
// keyup n'augmente qu'une fois quand vous relâchez
```

## Ce qu'il faut retenir

✅ **keydown** se déclenche quand une touche est enfoncée (le plus utilisé)

✅ **keyup** se déclenche quand une touche est relâchée

✅ **event.key** donne la valeur de la touche ('a', 'Enter', 'ArrowUp', etc.)

✅ **event.code** donne la position physique ('KeyA', 'Enter', 'ArrowUp', etc.)

✅ **Les modificateurs** sont détectables via `ctrlKey`, `shiftKey`, `altKey`, `metaKey`

✅ **event.preventDefault()** empêche le comportement par défaut

✅ **keypress est déprécié**, utilisez keydown à la place

✅ **Vérifier Ctrl ET Meta** pour la compatibilité Mac/Windows

## Dans la prochaine leçon

Maintenant que vous maîtrisez les événements de souris et de clavier, nous allons explorer les **événements de formulaire** : submit, change, input, focus, blur.

Vous découvrirez :
- Comment valider un formulaire avant soumission
- Comment réagir aux changements de valeur en temps réel
- La gestion du focus sur les champs
- La création de formulaires interactifs

---


⏭️ [Événements de formulaire : submit, change, input, focus, blur](/05-javascript-moderne-fondamentaux/10-evenements/05-evenements-formulaire.md)
