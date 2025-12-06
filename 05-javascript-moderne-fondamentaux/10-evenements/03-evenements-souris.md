🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.3 - Événements de souris

## Introduction

Les événements de souris sont probablement les événements les plus utilisés en développement web. Ils permettent de créer des interactions riches : boutons cliquables, menus déroulants, info-bulles, galeries d'images interactives, et bien plus encore.

Dans cette leçon, nous allons explorer en détail tous les événements liés à la souris et apprendre quand utiliser chacun d'entre eux.

## Vue d'ensemble des événements de souris

Voici les principaux événements de souris que vous utiliserez :

| Événement | Se déclenche quand... | Utilisation courante |
|-----------|----------------------|---------------------|
| `click` | L'utilisateur clique (appuie et relâche) | Boutons, liens, actions principales |
| `dblclick` | L'utilisateur double-clique | Actions spéciales, sélection |
| `mousedown` | Le bouton de la souris est enfoncé | Début de glisser-déposer |
| `mouseup` | Le bouton de la souris est relâché | Fin de glisser-déposer |
| `mouseover` | La souris entre dans un élément (+ enfants) | Effets au survol |
| `mouseout` | La souris sort d'un élément (+ enfants) | Fin d'effets au survol |
| `mouseenter` | La souris entre dans un élément (enfants ignorés) | Effets au survol (plus précis) |
| `mouseleave` | La souris sort d'un élément (enfants ignorés) | Fin d'effets au survol (plus précis) |
| `mousemove` | La souris bouge sur un élément | Suivi de position, curseurs personnalisés |

## 1. L'événement click

C'est l'événement le plus utilisé en développement web.

### Quand se déclenche-t-il ?

L'événement `click` se déclenche quand l'utilisateur :
1. Appuie sur le bouton de la souris (mousedown)
2. **ET** relâche le bouton au même endroit (mouseup)

### Exemple simple

```html
<button id="monBouton">Cliquez-moi</button>
<p id="resultat"></p>
```

```javascript
const bouton = document.getElementById('monBouton');
const resultat = document.getElementById('resultat');

bouton.addEventListener('click', () => {
    resultat.textContent = 'Vous avez cliqué !';
});
```

### Exemple : Compteur de clics

```html
<button id="btnCompter">Cliquez</button>
<p>Clics : <span id="compteur">0</span></p>
```

```javascript
const bouton = document.getElementById('btnCompter');
const compteur = document.getElementById('compteur');
let nombreClics = 0;

bouton.addEventListener('click', () => {
    nombreClics++;
    compteur.textContent = nombreClics;
});
```

### Exemple : Basculer une classe (toggle)

```html
<button id="btnToggle">Basculer</button>
<div id="boite" class="boite">Contenu de la boîte</div>
```

```css
.boite {
    background-color: lightblue;
    padding: 20px;
    transition: background-color 0.3s;
}

.actif {
    background-color: lightcoral;
}
```

```javascript
const bouton = document.getElementById('btnToggle');
const boite = document.getElementById('boite');

bouton.addEventListener('click', () => {
    boite.classList.toggle('actif');
});
```

### Informations disponibles avec l'objet Event

```javascript
bouton.addEventListener('click', (event) => {
    console.log('Position X :', event.clientX); // Position horizontale
    console.log('Position Y :', event.clientY); // Position verticale
    console.log('Élément cliqué :', event.target); // L'élément
    console.log('Bouton de souris :', event.button); // 0=gauche, 1=milieu, 2=droit
});
```

## 2. L'événement dblclick

### Quand se déclenche-t-il ?

L'événement `dblclick` se déclenche quand l'utilisateur double-clique rapidement sur un élément.

### Exemple : Sélectionner du texte

```html
<p id="texte">Double-cliquez sur moi pour me sélectionner</p>
```

```javascript
const texte = document.getElementById('texte');

texte.addEventListener('dblclick', () => {
    texte.style.backgroundColor = 'yellow';
    texte.style.fontWeight = 'bold';
});
```

### Exemple : Agrandir une image

```html
<img id="image" src="photo.jpg" alt="Photo" style="width: 200px; cursor: pointer;">
```

```javascript
const image = document.getElementById('image');
let estAgrandie = false;

image.addEventListener('dblclick', () => {
    if (estAgrandie) {
        image.style.width = '200px';
    } else {
        image.style.width = '400px';
    }
    estAgrandie = !estAgrandie;
});
```

### ⚠️ Attention : click ET dblclick ensemble

Si vous attachez à la fois `click` et `dblclick` sur le même élément, le double-clic déclenchera **d'abord** deux événements `click`, **puis** un événement `dblclick`.

```javascript
element.addEventListener('click', () => {
    console.log('Clic simple'); // S'affichera 2 fois lors d'un double-clic
});

element.addEventListener('dblclick', () => {
    console.log('Double-clic'); // S'affichera 1 fois
});
```

## 3. Les événements mousedown et mouseup

Ces événements permettent de détecter les phases du clic.

### mousedown
Se déclenche quand le bouton de la souris est **enfoncé** (avant de le relâcher).

### mouseup
Se déclenche quand le bouton de la souris est **relâché**.

### Exemple : Changer la couleur pendant le clic

```html
<button id="bouton">Appuyez et maintenez</button>
```

```javascript
const bouton = document.getElementById('bouton');

bouton.addEventListener('mousedown', () => {
    bouton.style.backgroundColor = 'red';
    console.log('Bouton enfoncé');
});

bouton.addEventListener('mouseup', () => {
    bouton.style.backgroundColor = '';
    console.log('Bouton relâché');
});
```

### Exemple : Glisser-déposer simple (concept)

```javascript
let estEnTrainDeGlisser = false;

element.addEventListener('mousedown', () => {
    estEnTrainDeGlisser = true;
    console.log('Début du glissement');
});

document.addEventListener('mouseup', () => {
    if (estEnTrainDeGlisser) {
        estEnTrainDeGlisser = false;
        console.log('Fin du glissement');
    }
});
```

## 4. L'événement mouseover

### Quand se déclenche-t-il ?

L'événement `mouseover` se déclenche quand le pointeur de la souris **entre** dans l'élément **ou dans l'un de ses enfants**.

### Exemple simple

```html
<div id="boite" style="width: 200px; height: 200px; background: lightblue;">
    Passez la souris ici
</div>
<p id="message"></p>
```

```javascript
const boite = document.getElementById('boite');
const message = document.getElementById('message');

boite.addEventListener('mouseover', () => {
    message.textContent = 'La souris est sur la boîte !';
    boite.style.backgroundColor = 'lightcoral';
});
```

### ⚠️ Particularité : Se déclenche sur les enfants

```html
<div id="parent" style="padding: 20px; background: lightblue;">
    Parent
    <div id="enfant" style="padding: 10px; background: lightgreen;">
        Enfant
    </div>
</div>
```

```javascript
const parent = document.getElementById('parent');

parent.addEventListener('mouseover', (event) => {
    console.log('mouseover déclenché sur :', event.target.id);
});

// Résultat : se déclenchera quand vous entrez dans le parent
// ET quand vous entrez dans l'enfant
```

## 5. L'événement mouseout

### Quand se déclenche-t-il ?

L'événement `mouseout` se déclenche quand le pointeur de la souris **sort** de l'élément **ou entre dans l'un de ses enfants**.

### Exemple : Remettre la couleur d'origine

```html
<div id="boite" style="width: 200px; height: 200px; background: lightblue;">
    Passez la souris ici
</div>
```

```javascript
const boite = document.getElementById('boite');

boite.addEventListener('mouseover', () => {
    boite.style.backgroundColor = 'lightcoral';
});

boite.addEventListener('mouseout', () => {
    boite.style.backgroundColor = 'lightblue';
});
```

### Exemple : Info-bulle simple

```html
<button id="boutonInfo">Survolez-moi</button>
<div id="infobulle" style="display: none; background: black; color: white; padding: 5px;">
    Ceci est une info-bulle
</div>
```

```javascript
const bouton = document.getElementById('boutonInfo');
const infobulle = document.getElementById('infobulle');

bouton.addEventListener('mouseover', () => {
    infobulle.style.display = 'block';
});

bouton.addEventListener('mouseout', () => {
    infobulle.style.display = 'none';
});
```

## 6. L'événement mouseenter

### Quand se déclenche-t-il ?

L'événement `mouseenter` se déclenche quand le pointeur de la souris **entre** dans l'élément. Contrairement à `mouseover`, il **ne se déclenche PAS** sur les éléments enfants.

### Différence clé avec mouseover

```html
<div id="parent" style="padding: 20px; background: lightblue;">
    Parent
    <div id="enfant" style="padding: 10px; background: lightgreen;">
        Enfant
    </div>
</div>
```

```javascript
const parent = document.getElementById('parent');

// Avec mouseover (se déclenche sur le parent ET l'enfant)
parent.addEventListener('mouseover', () => {
    console.log('mouseover - Se déclenche plusieurs fois');
});

// Avec mouseenter (ne se déclenche que sur le parent)
parent.addEventListener('mouseenter', () => {
    console.log('mouseenter - Se déclenche une seule fois');
});
```

### Exemple : Effet au survol propre

```html
<div class="carte" style="padding: 20px; background: white; border: 1px solid #ddd;">
    <h3>Titre de la carte</h3>
    <p>Description de la carte</p>
    <button>En savoir plus</button>
</div>
```

```javascript
const carte = document.querySelector('.carte');

carte.addEventListener('mouseenter', () => {
    carte.style.boxShadow = '0 4px 8px rgba(0,0,0,0.2)';
    carte.style.transform = 'translateY(-5px)';
});

carte.addEventListener('mouseleave', () => {
    carte.style.boxShadow = '';
    carte.style.transform = '';
});
```

## 7. L'événement mouseleave

### Quand se déclenche-t-il ?

L'événement `mouseleave` se déclenche quand le pointeur de la souris **sort** de l'élément. Contrairement à `mouseout`, il **ne se déclenche PAS** quand on entre dans un élément enfant.

### Utilisation recommandée

Pour la plupart des cas d'usage, préférez **mouseenter/mouseleave** à **mouseover/mouseout** car ils sont plus prévisibles et ne se déclenchent pas sur les enfants.

## Comparaison : mouseover/mouseout VS mouseenter/mouseleave

### Tableau comparatif

| Critère | mouseover / mouseout | mouseenter / mouseleave |
|---------|---------------------|------------------------|
| **Se déclenche sur les enfants** | ✅ Oui | ❌ Non |
| **Bulle (bubbling)** | ✅ Oui | ❌ Non |
| **Prévisible** | ⚠️ Moyen | ✅ Très |
| **Recommandé pour effets au survol** | ❌ Non | ✅ Oui |

### Exemple visuel de la différence

```html
<div id="conteneur" style="padding: 30px; background: lightblue;">
    CONTENEUR
    <div id="enfant" style="padding: 20px; background: lightgreen;">
        ENFANT
    </div>
</div>
<p id="log"></p>
```

```javascript
const conteneur = document.getElementById('conteneur');
const log = document.getElementById('log');
let compteurOver = 0;
let compteurEnter = 0;

// mouseover se déclenche sur le conteneur ET l'enfant
conteneur.addEventListener('mouseover', () => {
    compteurOver++;
    log.textContent = `mouseover: ${compteurOver} fois | mouseenter: ${compteurEnter} fois`;
});

// mouseenter ne se déclenche que sur le conteneur
conteneur.addEventListener('mouseenter', () => {
    compteurEnter++;
    log.textContent = `mouseover: ${compteurOver} fois | mouseenter: ${compteurEnter} fois`;
});

// Résultat : quand vous passez du conteneur à l'enfant,
// mouseover se déclenche à nouveau, mais pas mouseenter
```

### Quand utiliser quoi ?

#### ✅ Utilisez mouseenter / mouseleave quand :
- Vous voulez un simple effet au survol
- Vous ne voulez pas que l'événement se déclenche sur les enfants
- Vous créez des menus, des cartes, des boutons

#### ⚠️ Utilisez mouseover / mouseout quand :
- Vous avez besoin que l'événement remonte (bubbling)
- Vous devez détecter l'entrée dans les enfants
- Cas d'usage très spécifiques

## 8. L'événement mousemove

### Quand se déclenche-t-il ?

L'événement `mousemove` se déclenche **en continu** quand la souris bouge sur un élément.

### ⚠️ Attention : Performance

Cet événement se déclenche **très souvent** (plusieurs fois par seconde). Il faut l'utiliser avec précaution pour ne pas ralentir votre page.

### Exemple : Suivre la position de la souris

```html
<div id="zone" style="width: 400px; height: 300px; background: lightblue; position: relative;">
    Déplacez la souris
    <div id="curseur" style="position: absolute; width: 10px; height: 10px; background: red; border-radius: 50%;"></div>
</div>
<p id="coords"></p>
```

```javascript
const zone = document.getElementById('zone');
const curseur = document.getElementById('curseur');
const coords = document.getElementById('coords');

zone.addEventListener('mousemove', (event) => {
    // Position relative à la zone
    const x = event.offsetX;
    const y = event.offsetY;

    // Déplacer le curseur
    curseur.style.left = x + 'px';
    curseur.style.top = y + 'px';

    // Afficher les coordonnées
    coords.textContent = `X: ${x}, Y: ${y}`;
});
```

### Exemple : Effet de parallaxe simple

```html
<div id="scene" style="width: 100%; height: 300px; background: linear-gradient(to bottom, #87CEEB, #fff); position: relative; overflow: hidden;">
    <div id="nuage" style="position: absolute; top: 50px; left: 50%; font-size: 40px;">☁️</div>
</div>
```

```javascript
const scene = document.getElementById('scene');
const nuage = document.getElementById('nuage');

scene.addEventListener('mousemove', (event) => {
    const x = event.clientX / window.innerWidth;
    const y = event.clientY / window.innerHeight;

    // Le nuage suit la souris avec un effet de décalage
    nuage.style.left = (50 + x * 10) + '%';
    nuage.style.top = (50 + y * 10) + 'px';
});
```

## Propriétés utiles de l'objet Event pour la souris

Voici les propriétés les plus utilisées de l'objet Event pour les événements de souris :

### Propriétés de position

```javascript
element.addEventListener('click', (event) => {
    // Position par rapport à la fenêtre du navigateur
    console.log('clientX:', event.clientX);
    console.log('clientY:', event.clientY);

    // Position par rapport à la page (avec défilement)
    console.log('pageX:', event.pageX);
    console.log('pageY:', event.pageY);

    // Position par rapport à l'élément ciblé
    console.log('offsetX:', event.offsetX);
    console.log('offsetY:', event.offsetY);

    // Position par rapport à l'écran
    console.log('screenX:', event.screenX);
    console.log('screenY:', event.screenY);
});
```

### Propriétés de bouton et de modificateurs

```javascript
element.addEventListener('click', (event) => {
    // Quel bouton de la souris ?
    // 0 = bouton gauche, 1 = bouton milieu, 2 = bouton droit
    console.log('Bouton:', event.button);

    // Touches modificatrices enfoncées ?
    console.log('Ctrl enfoncé ?', event.ctrlKey);
    console.log('Shift enfoncé ?', event.shiftKey);
    console.log('Alt enfoncé ?', event.altKey);
    console.log('Meta enfoncé ?', event.metaKey); // Cmd sur Mac, Win sur Windows
});
```

### Exemple : Clic avec Ctrl pour sélection multiple

```javascript
const elements = document.querySelectorAll('.item');

elements.forEach(item => {
    item.addEventListener('click', (event) => {
        if (event.ctrlKey) {
            // Clic avec Ctrl : ajouter à la sélection
            item.classList.toggle('selectionne');
        } else {
            // Clic normal : sélection unique
            elements.forEach(el => el.classList.remove('selectionne'));
            item.classList.add('selectionne');
        }
    });
});
```

## Exemples pratiques complets

### Exemple 1 : Menu déroulant

```html
<div class="menu">
    <button id="btnMenu">Menu</button>
    <div id="sousMenu" style="display: none; background: white; border: 1px solid #ddd; padding: 10px;">
        <a href="#">Option 1</a><br>
        <a href="#">Option 2</a><br>
        <a href="#">Option 3</a>
    </div>
</div>
```

```javascript
const menu = document.querySelector('.menu');
const sousMenu = document.getElementById('sousMenu');

menu.addEventListener('mouseenter', () => {
    sousMenu.style.display = 'block';
});

menu.addEventListener('mouseleave', () => {
    sousMenu.style.display = 'none';
});
```

### Exemple 2 : Galerie d'images avec prévisualisation

```html
<div class="galerie">
    <img src="thumb1.jpg" class="miniature" data-grand="image1.jpg" alt="Image 1">
    <img src="thumb2.jpg" class="miniature" data-grand="image2.jpg" alt="Image 2">
    <img src="thumb3.jpg" class="miniature" data-grand="image3.jpg" alt="Image 3">
</div>
<div id="preview" style="display: none; position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: rgba(0,0,0,0.8); padding: 20px;">
    <img id="grandImage" src="" alt="" style="max-width: 80vw; max-height: 80vh;">
</div>
```

```javascript
const miniatures = document.querySelectorAll('.miniature');
const preview = document.getElementById('preview');
const grandImage = document.getElementById('grandImage');

miniatures.forEach(mini => {
    mini.addEventListener('mouseenter', () => {
        grandImage.src = mini.dataset.grand;
        preview.style.display = 'block';
    });
});

preview.addEventListener('mouseleave', () => {
    preview.style.display = 'none';
});
```

### Exemple 3 : Carte interactive qui suit la souris

```html
<div class="carte-container" style="perspective: 1000px;">
    <div id="carte" style="width: 300px; height: 400px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 20px; transition: transform 0.1s;">
        <h2 style="color: white; padding: 20px;">Ma Carte</h2>
    </div>
</div>
```

```javascript
const carte = document.getElementById('carte');

carte.addEventListener('mousemove', (event) => {
    const rect = carte.getBoundingClientRect();
    const x = event.clientX - rect.left;
    const y = event.clientY - rect.top;

    const centerX = rect.width / 2;
    const centerY = rect.height / 2;

    const rotateX = (y - centerY) / 10;
    const rotateY = (centerX - x) / 10;

    carte.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
});

carte.addEventListener('mouseleave', () => {
    carte.style.transform = 'rotateX(0) rotateY(0)';
});
```

## Bonnes pratiques

### ✅ 1. Préférer mouseenter/mouseleave pour les effets au survol

```javascript
// ✅ BIEN - Plus prévisible
element.addEventListener('mouseenter', ajouterEffet);
element.addEventListener('mouseleave', retirerEffet);

// ⚠️ ÉVITER - Peut se déclencher sur les enfants
element.addEventListener('mouseover', ajouterEffet);
element.addEventListener('mouseout', retirerEffet);
```

### ✅ 2. Optimiser mousemove avec throttle ou debounce

Pour des raisons de performance, limitez la fréquence d'exécution de mousemove :

```javascript
let dernierTemps = 0;
const delai = 16; // ~60fps

element.addEventListener('mousemove', (event) => {
    const maintenant = Date.now();

    if (maintenant - dernierTemps >= delai) {
        // Votre code ici
        dernierTemps = maintenant;
    }
});
```

### ✅ 3. Nettoyer les événements quand nécessaire

```javascript
function afficherMessage() {
    console.log('Clic détecté');
}

// Ajouter
element.addEventListener('click', afficherMessage);

// Retirer quand vous n'en avez plus besoin
element.removeEventListener('click', afficherMessage);
```

### ✅ 4. Vérifier l'existence de l'élément

```javascript
const element = document.getElementById('monElement');

if (element) {
    element.addEventListener('click', maFonction);
}
```

## Résumé des événements de souris

| Événement | Quand ? | Bubblin | Recommandé pour |
|-----------|---------|----------|-----------------|
| **click** | Clic complet | ✅ | Actions principales |
| **dblclick** | Double-clic | ✅ | Actions spéciales |
| **mousedown** | Bouton enfoncé | ✅ | Début glisser-déposer |
| **mouseup** | Bouton relâché | ✅ | Fin glisser-déposer |
| **mouseover** | Entre (+ enfants) | ✅ | Cas spécifiques |
| **mouseout** | Sort (+ enfants) | ✅ | Cas spécifiques |
| **mouseenter** | Entre (pas enfants) | ❌ | Effets au survol ⭐ |
| **mouseleave** | Sort (pas enfants) | ❌ | Effets au survol ⭐ |
| **mousemove** | Bouge | ✅ | Suivi position |

## Ce qu'il faut retenir

✅ **click** est l'événement de souris le plus utilisé

✅ **mouseenter/mouseleave** sont préférables à mouseover/mouseout pour les effets au survol

✅ **dblclick** déclenche aussi deux événements click avant lui

✅ **mousemove** se déclenche très souvent : attention aux performances

✅ **L'objet Event** contient de nombreuses informations : position, bouton, touches modificatrices

✅ **Toujours vérifier** que l'élément existe avant d'attacher un événement

## Dans la prochaine leçon

Maintenant que vous maîtrisez les événements de souris, nous allons explorer les **événements de clavier** : keydown, keyup, et comment détecter quelle touche a été pressée.

Vous découvrirez :
- Comment détecter les touches du clavier
- La différence entre keydown et keyup
- Comment créer des raccourcis clavier
- La gestion des combinaisons de touches (Ctrl+S, etc.)

---


⏭️ [Événements de clavier : keydown, keyup](/05-javascript-moderne-fondamentaux/10-evenements/04-evenements-clavier.md)
