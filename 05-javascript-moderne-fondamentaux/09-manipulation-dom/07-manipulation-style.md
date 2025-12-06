🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.9.7 - Manipulation du style en ligne

## Introduction

Vous savez maintenant manipuler le contenu et les attributs des éléments HTML. Il est temps d'apprendre à **modifier leur apparence** en changeant leurs styles CSS directement avec JavaScript !

JavaScript vous permet de modifier les propriétés CSS d'un élément en temps réel, créant ainsi des effets dynamiques et interactifs.

> **Note importante :** Bien que JavaScript puisse modifier les styles, il est généralement **préférable d'utiliser des classes CSS** pour les changements de style. Nous verrons pourquoi et quand utiliser chaque approche !

---

## La propriété style

### Qu'est-ce que element.style ?

Chaque élément du DOM possède une propriété **`style`** qui donne accès à ses **styles en ligne** (inline styles).

**Exemple HTML :**
```html
<div id="box" style="color: red; font-size: 20px;">Mon texte</div>
```

**JavaScript :**
```javascript
let box = document.getElementById('box');

// Accéder à la propriété style
console.log(box.style);  // Objet CSSStyleDeclaration
```

### Styles en ligne vs styles CSS

Il est important de comprendre la différence :

**Styles en ligne (inline)** :
```html
<div style="color: red; background: blue;">
```

**Styles dans une feuille CSS** :
```css
.ma-classe {
    color: red;
    background: blue;
}
```

**Important :** La propriété `element.style` ne permet d'accéder qu'aux **styles en ligne**, pas aux styles définis dans les feuilles CSS externes ou internes !

---

## Lire les styles en ligne

### Syntaxe

```javascript
element.style.propriété
```

**Attention :** Les noms de propriétés CSS sont convertis en **camelCase** en JavaScript.

### Conversion CSS → JavaScript

| CSS | JavaScript |
|-----|------------|
| `color` | `color` |
| `font-size` | `fontSize` |
| `background-color` | `backgroundColor` |
| `margin-top` | `marginTop` |
| `border-radius` | `borderRadius` |
| `text-align` | `textAlign` |
| `padding-left` | `paddingLeft` |

**Règle :** Retirez les tirets et mettez en majuscule la lettre suivante.

### Exemples de lecture

**HTML :**
```html
<div id="box" style="color: red; font-size: 20px; background-color: lightblue;">
    Contenu
</div>
```

**JavaScript :**
```javascript
let box = document.getElementById('box');

// Lire les styles
console.log(box.style.color);           // "red"
console.log(box.style.fontSize);        // "20px"
console.log(box.style.backgroundColor); // "lightblue"
```

### Styles non définis en ligne

Si un style n'est pas défini en ligne, la propriété retourne une **chaîne vide** :

```html
<div id="box">Sans styles en ligne</div>
```

```javascript
let box = document.getElementById('box');

console.log(box.style.color);  // "" (chaîne vide)
```

**Même si l'élément a des styles CSS** définis ailleurs, `element.style` ne les voit pas !

---

## Modifier les styles en ligne

### Syntaxe

```javascript
element.style.propriété = 'valeur';
```

### Exemples basiques

```javascript
let box = document.getElementById('box');

// Changer la couleur du texte
box.style.color = 'blue';

// Changer la taille de police
box.style.fontSize = '24px';

// Changer la couleur de fond
box.style.backgroundColor = 'yellow';

// Changer plusieurs propriétés
box.style.width = '300px';
box.style.height = '200px';
box.style.border = '2px solid black';
box.style.padding = '20px';
box.style.margin = '10px';
```

### Valeurs avec unités

**⚠️ Important :** N'oubliez pas les unités !

```javascript
// ❌ Incorrect - pas d'unité
element.style.width = 200;        // Ne fonctionne pas
element.style.fontSize = 16;      // Ne fonctionne pas

// ✅ Correct - avec unité
element.style.width = '200px';
element.style.fontSize = '16px';

// Autres unités possibles
element.style.width = '50%';
element.style.fontSize = '1.5em';
element.style.margin = '2rem';
```

### Valeurs calculées

Vous pouvez aussi utiliser des calculs :

```javascript
let box = document.getElementById('box');
let largeur = 100;

// Calculer et appliquer
box.style.width = (largeur * 2) + 'px';  // "200px"

// Avec des variables
let taille = 16;
box.style.fontSize = taille + 'px';      // "16px"
```

---

## Exemples pratiques

### Exemple 1 : Changer la couleur au clic

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Changement de couleur</title>
</head>
<body>
    <div id="box" style="width: 200px; height: 200px; background-color: blue;">
        Cliquez-moi !
    </div>

    <script>
        let box = document.getElementById('box');

        box.addEventListener('click', function() {
            // Changer la couleur de fond
            this.style.backgroundColor = 'red';
        });
    </script>
</body>
</html>
```

### Exemple 2 : Agrandir/Rétrécir un élément

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Redimensionnement</title>
</head>
<body>
    <div id="box" style="width: 100px; height: 100px; background-color: green;">
    </div>

    <button id="bigger">Plus grand</button>
    <button id="smaller">Plus petit</button>

    <script>
        let box = document.getElementById('box');
        let biggerBtn = document.getElementById('bigger');
        let smallerBtn = document.getElementById('smaller');

        let size = 100;

        biggerBtn.addEventListener('click', function() {
            size += 20;
            box.style.width = size + 'px';
            box.style.height = size + 'px';
        });

        smallerBtn.addEventListener('click', function() {
            if (size > 20) {
                size -= 20;
                box.style.width = size + 'px';
                box.style.height = size + 'px';
            }
        });
    </script>
</body>
</html>
```

### Exemple 3 : Afficher/Masquer un élément

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Afficher/Masquer</title>
</head>
<body>
    <div id="message" style="padding: 20px; background-color: lightblue;">
        Ceci est un message important !
    </div>

    <button id="toggle">Afficher/Masquer</button>

    <script>
        let message = document.getElementById('message');
        let toggleBtn = document.getElementById('toggle');

        toggleBtn.addEventListener('click', function() {
            if (message.style.display === 'none') {
                message.style.display = 'block';
            } else {
                message.style.display = 'none';
            }
        });
    </script>
</body>
</html>
```

### Exemple 4 : Changer les styles au survol (sans CSS)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Effet de survol</title>
</head>
<body>
    <button id="btn">Survolez-moi !</button>

    <script>
        let btn = document.getElementById('btn');

        // Au survol
        btn.addEventListener('mouseenter', function() {
            this.style.backgroundColor = 'blue';
            this.style.color = 'white';
            this.style.fontSize = '20px';
            this.style.cursor = 'pointer';
        });

        // Quand on quitte
        btn.addEventListener('mouseleave', function() {
            this.style.backgroundColor = '';
            this.style.color = '';
            this.style.fontSize = '';
        });
    </script>
</body>
</html>
```

**Note :** Pour les effets de survol, il est **préférable d'utiliser CSS** (`:hover`) plutôt que JavaScript !

---

## Supprimer un style en ligne

Pour supprimer un style en ligne, assignez-lui une **chaîne vide** :

```javascript
let box = document.getElementById('box');

// Définir un style
box.style.color = 'red';

// Supprimer ce style
box.style.color = '';
```

L'élément reprendra alors le style défini dans les feuilles CSS, ou le style par défaut du navigateur.

---

## cssText - Définir plusieurs styles à la fois

### Le problème

Définir plusieurs styles un par un peut être verbeux :

```javascript
element.style.color = 'red';
element.style.fontSize = '20px';
element.style.backgroundColor = 'yellow';
element.style.padding = '10px';
element.style.border = '2px solid black';
```

### La solution : cssText

La propriété **`cssText`** permet de définir plusieurs styles en une seule fois :

```javascript
element.style.cssText = 'color: red; font-size: 20px; background-color: yellow; padding: 10px;';
```

### Exemple complet

```html
<div id="box">Mon contenu</div>

<script>
    let box = document.getElementById('box');

    // Définir plusieurs styles à la fois
    box.style.cssText = `
        width: 300px;
        height: 200px;
        background-color: lightblue;
        color: darkblue;
        padding: 20px;
        border: 3px solid navy;
        border-radius: 10px;
        text-align: center;
        font-size: 18px;
    `;
</script>
```

### ⚠️ Attention avec cssText

`cssText` **remplace** tous les styles en ligne existants :

```javascript
element.style.cssText = 'color: red;';  // Définit uniquement color
element.style.cssText = 'font-size: 20px;';  // ❌ Supprime color !
```

Pour ajouter sans supprimer, utilisez `+=` :

```javascript
element.style.cssText += 'color: red;';
element.style.cssText += 'font-size: 20px;';  // ✅ Conserve color
```

---

## getComputedStyle() - Lire les styles réels

### Le problème

Comme nous l'avons vu, `element.style` ne lit que les styles **en ligne**. Si un élément a des styles définis dans une feuille CSS, `element.style` ne les voit pas.

**Exemple :**
```html
<style>
    .box {
        color: red;
        font-size: 20px;
    }
</style>

<div id="myBox" class="box">Texte</div>

<script>
    let box = document.getElementById('myBox');
    console.log(box.style.color);     // "" (vide !)
    console.log(box.style.fontSize);  // "" (vide !)
</script>
```

### La solution : getComputedStyle()

Pour lire les styles **réellement appliqués** (calculés), utilisez `window.getComputedStyle()` :

```javascript
let styles = window.getComputedStyle(element);
```

### Exemple

```html
<style>
    .box {
        color: red;
        font-size: 20px;
        background-color: lightblue;
    }
</style>

<div id="myBox" class="box">Texte</div>

<script>
    let box = document.getElementById('myBox');

    // Récupérer les styles calculés
    let styles = window.getComputedStyle(box);

    console.log(styles.color);            // "rgb(255, 0, 0)" (rouge en RGB)
    console.log(styles.fontSize);         // "20px"
    console.log(styles.backgroundColor);  // "rgb(173, 216, 230)"
</script>
```

### Différences importantes

```javascript
let box = document.getElementById('myBox');

// Styles en ligne uniquement
console.log(box.style.color);  // Peut être vide

// Styles calculés (réels)
let computed = window.getComputedStyle(box);
console.log(computed.color);   // Toujours une valeur (si style appliqué)
```

### Lecture seule

**Important :** `getComputedStyle()` est en **lecture seule**. Vous ne pouvez pas modifier les styles avec :

```javascript
let styles = window.getComputedStyle(box);
styles.color = 'blue';  // ❌ Ne fonctionne pas !

// Pour modifier, utilisez element.style
box.style.color = 'blue';  // ✅ Fonctionne
```

---

## Propriétés CSS courantes en JavaScript

Voici un tableau de référence des propriétés CSS les plus utilisées :

| CSS | JavaScript | Exemple de valeur |
|-----|------------|-------------------|
| `color` | `color` | `'red'`, `'#ff0000'`, `'rgb(255,0,0)'` |
| `background-color` | `backgroundColor` | `'blue'`, `'#0000ff'` |
| `font-size` | `fontSize` | `'16px'`, `'1.5em'` |
| `font-family` | `fontFamily` | `'Arial, sans-serif'` |
| `font-weight` | `fontWeight` | `'bold'`, `'700'` |
| `text-align` | `textAlign` | `'center'`, `'left'`, `'right'` |
| `width` | `width` | `'100px'`, `'50%'` |
| `height` | `height` | `'200px'`, `'100vh'` |
| `margin` | `margin` | `'10px'`, `'10px 20px'` |
| `margin-top` | `marginTop` | `'10px'` |
| `padding` | `padding` | `'15px'` |
| `border` | `border` | `'2px solid black'` |
| `border-radius` | `borderRadius` | `'5px'`, `'50%'` |
| `display` | `display` | `'block'`, `'none'`, `'flex'` |
| `visibility` | `visibility` | `'visible'`, `'hidden'` |
| `opacity` | `opacity` | `'0.5'`, `'1'` |
| `position` | `position` | `'relative'`, `'absolute'` |
| `top` | `top` | `'10px'` |
| `left` | `left` | `'20px'` |
| `z-index` | `zIndex` | `'10'`, `'999'` |
| `cursor` | `cursor` | `'pointer'`, `'not-allowed'` |
| `overflow` | `overflow` | `'hidden'`, `'scroll'` |
| `box-shadow` | `boxShadow` | `'0 2px 4px rgba(0,0,0,0.1)'` |
| `transform` | `transform` | `'rotate(45deg)'`, `'scale(1.2)'` |
| `transition` | `transition` | `'all 0.3s ease'` |

---

## Styles vs Classes CSS : Quelle approche choisir ?

### Le débat

Faut-il modifier les styles directement ou utiliser des classes CSS ?

**Modifier les styles (JavaScript) :**
```javascript
element.style.color = 'red';
element.style.fontSize = '20px';
```

**Utiliser des classes (CSS + JavaScript) :**
```css
.highlight {
    color: red;
    font-size: 20px;
}
```
```javascript
element.classList.add('highlight');
```

### Avantages et inconvénients

#### Modifier les styles directement

**✅ Avantages :**
- Valeurs dynamiques (calculées en temps réel)
- Pas besoin de CSS prédéfini
- Contrôle précis

**❌ Inconvénients :**
- Code JavaScript plus verbeux
- Mélange présentation et logique
- Moins performant
- Plus difficile à maintenir

#### Utiliser des classes CSS

**✅ Avantages :**
- Séparation des préoccupations (CSS = style, JS = logique)
- Plus facile à maintenir
- Meilleur pour les animations
- Plus performant
- Réutilisable

**❌ Inconvénients :**
- Nécessite de définir les classes à l'avance
- Moins flexible pour les valeurs dynamiques

### Recommandations

**Utilisez les classes CSS quand :**
- ✅ Vous avez des styles prédéfinis
- ✅ Vous voulez réutiliser les mêmes styles
- ✅ Vous gérez plusieurs propriétés ensemble
- ✅ Vous créez des animations ou transitions

**Modifiez les styles directement quand :**
- ✅ Les valeurs sont calculées dynamiquement
- ✅ Vous modifiez une seule propriété ponctuellement
- ✅ Les valeurs dépendent de l'interaction utilisateur
- ✅ Vous ne pouvez pas prédéfinir tous les cas

### Exemples comparatifs

#### Scénario 1 : Afficher/Masquer (préférez les classes)

```javascript
// ❌ Moins bien : style direct
element.style.display = 'none';

// ✅ Mieux : classe CSS
element.classList.add('hidden');
```

```css
.hidden {
    display: none;
}
```

#### Scénario 2 : Positions dynamiques (style direct OK)

```javascript
// ✅ Valeurs calculées : style direct approprié
let x = event.clientX;
let y = event.clientY;
tooltip.style.left = x + 'px';
tooltip.style.top = y + 'px';
```

#### Scénario 3 : État actif (préférez les classes)

```javascript
// ❌ Moins bien
button.style.backgroundColor = 'blue';
button.style.color = 'white';
button.style.fontWeight = 'bold';

// ✅ Mieux
button.classList.add('active');
```

```css
.active {
    background-color: blue;
    color: white;
    font-weight: bold;
}
```

---

## Exemples avancés

### Exemple 1 : Animation de progression

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Barre de progression</title>
    <style>
        #progress-bar {
            width: 100%;
            height: 30px;
            background-color: #e0e0e0;
            border-radius: 15px;
            overflow: hidden;
        }
        #progress-fill {
            height: 100%;
            background-color: #4caf50;
            width: 0%;
            transition: width 0.3s ease;
        }
    </style>
</head>
<body>
    <h2>Progression : <span id="percent">0</span>%</h2>
    <div id="progress-bar">
        <div id="progress-fill"></div>
    </div>
    <button id="start">Démarrer</button>

    <script>
        let fill = document.getElementById('progress-fill');
        let percentText = document.getElementById('percent');
        let startBtn = document.getElementById('start');

        startBtn.addEventListener('click', function() {
            let progress = 0;

            let interval = setInterval(function() {
                progress += 1;

                // Modifier la largeur dynamiquement
                fill.style.width = progress + '%';
                percentText.textContent = progress;

                if (progress >= 100) {
                    clearInterval(interval);
                }
            }, 50);
        });
    </script>
</body>
</html>
```

### Exemple 2 : Palette de couleurs

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Palette de couleurs</title>
    <style>
        #color-box {
            width: 200px;
            height: 200px;
            background-color: white;
            border: 2px solid black;
            margin: 20px;
        }
        input {
            margin: 10px;
        }
    </style>
</head>
<body>
    <h2>Créez votre couleur</h2>
    <div id="color-box"></div>

    <label>Rouge: <input type="range" id="red" min="0" max="255" value="255"></label>
    <span id="red-value">255</span><br>

    <label>Vert: <input type="range" id="green" min="0" max="255" value="255"></label>
    <span id="green-value">255</span><br>

    <label>Bleu: <input type="range" id="blue" min="0" max="255" value="255"></label>
    <span id="blue-value">255</span><br>

    <p>Code couleur : <span id="color-code">#ffffff</span></p>

    <script>
        let box = document.getElementById('color-box');
        let redSlider = document.getElementById('red');
        let greenSlider = document.getElementById('green');
        let blueSlider = document.getElementById('blue');

        function updateColor() {
            let r = redSlider.value;
            let g = greenSlider.value;
            let b = blueSlider.value;

            // Créer la couleur RGB
            let color = `rgb(${r}, ${g}, ${b})`;

            // Appliquer la couleur
            box.style.backgroundColor = color;

            // Afficher les valeurs
            document.getElementById('red-value').textContent = r;
            document.getElementById('green-value').textContent = g;
            document.getElementById('blue-value').textContent = b;

            // Convertir en hexadécimal
            let hex = '#' +
                      parseInt(r).toString(16).padStart(2, '0') +
                      parseInt(g).toString(16).padStart(2, '0') +
                      parseInt(b).toString(16).padStart(2, '0');
            document.getElementById('color-code').textContent = hex;
        }

        redSlider.addEventListener('input', updateColor);
        greenSlider.addEventListener('input', updateColor);
        blueSlider.addEventListener('input', updateColor);

        // Initialiser
        updateColor();
    </script>
</body>
</html>
```

---

## Bonnes pratiques

### ✅ À faire

```javascript
// Utiliser camelCase pour les propriétés
element.style.backgroundColor = 'blue';  // ✅

// Inclure les unités
element.style.width = '200px';  // ✅

// Vérifier l'existence de l'élément
if (element) {
    element.style.color = 'red';
}

// Utiliser getComputedStyle pour lire les styles réels
let styles = window.getComputedStyle(element);
console.log(styles.color);

// Préférer les classes pour les changements complexes
element.classList.add('highlight');  // ✅ Mieux que plusieurs style.*
```

### ❌ À éviter

```javascript
// Oublier les unités
element.style.width = 200;  // ❌ Ne fonctionne pas

// Utiliser la syntaxe CSS
element.style['background-color'] = 'blue';  // ❌ Fonctionne mais évitez
element.style.backgroundColor = 'blue';       // ✅ Mieux

// Modifier beaucoup de styles un par un
element.style.color = 'red';
element.style.fontSize = '20px';
element.style.backgroundColor = 'yellow';
// ✅ Mieux : utiliser cssText ou une classe

// Essayer de modifier getComputedStyle
let styles = window.getComputedStyle(element);
styles.color = 'blue';  // ❌ Ne fonctionne pas (lecture seule)
```

---

## Points clés à retenir

✅ **`element.style`** permet de modifier les styles en ligne

✅ Les propriétés CSS sont converties en **camelCase** (background-color → backgroundColor)

✅ **Toujours inclure les unités** ('200px', '50%', '1.5em')

✅ `element.style` lit uniquement les **styles en ligne**, pas les styles CSS

✅ **`getComputedStyle()`** lit les styles réellement appliqués (lecture seule)

✅ **`cssText`** permet de définir plusieurs styles à la fois

✅ Assigner `''` (chaîne vide) **supprime** un style en ligne

✅ **Préférez les classes CSS** pour les changements de style complexes

✅ Utilisez les styles directs pour les **valeurs dynamiques calculées**

✅ La séparation des préoccupations : CSS pour les styles, JS pour la logique

---

## Ce qui vient ensuite

Maintenant que vous savez manipuler les styles directement, vous allez apprendre une méthode **encore meilleure** pour la plupart des cas : la manipulation des **classes CSS** avec `classList` !

Cette approche est plus propre, plus maintenable et plus performante pour gérer les changements de style.

---

## Ressources supplémentaires

- 📖 [MDN - HTMLElement.style](https://developer.mozilla.org/fr/docs/Web/API/HTMLElement/style)
- 📖 [MDN - window.getComputedStyle()](https://developer.mozilla.org/fr/docs/Web/API/Window/getComputedStyle)
- 📖 [MDN - CSSStyleDeclaration](https://developer.mozilla.org/fr/docs/Web/API/CSSStyleDeclaration)
- 💡 [Liste complète des propriétés CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Reference)

---


⏭️ [Classes CSS : classList (add, remove, toggle, contains)](/05-javascript-moderne-fondamentaux/09-manipulation-dom/08-classlist.md)
