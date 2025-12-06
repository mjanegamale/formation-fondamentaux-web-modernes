🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.12.6 Utilisation des breakpoints dans DevTools 🔧

## Introduction

Les breakpoints (points d'arrêt) sont l'un des outils les plus puissants pour déboguer votre code JavaScript. Ils vous permettent de **mettre en pause l'exécution** de votre programme à un moment précis pour inspecter l'état de vos variables et comprendre ce qui se passe réellement.

> 💡 **Analogie** : Un breakpoint c'est comme mettre le film sur pause pour examiner une scène image par image. Au lieu de deviner ce qui se passe, vous pouvez voir exactement l'état de votre programme à un instant T.

---

## Qu'est-ce qu'un breakpoint ?

Un **breakpoint** (point d'arrêt) est un marqueur que vous placez dans votre code pour dire au navigateur : "Arrête-toi ici et laisse-moi examiner la situation".

### Pourquoi utiliser des breakpoints ?

**Sans breakpoint :**
```javascript
function calculerTotal(prix, quantite) {
    const sousTotal = prix * quantite;
    const taxe = sousTotal * 0.20;
    const total = sousTotal + taxe;
    return total;
}

const resultat = calculerTotal(100, 3);
console.log(resultat);  // Qu'est-ce qui s'est passé exactement ?
```

**Avec breakpoint :**
- Vous voyez la valeur de `prix` et `quantite` au moment exact
- Vous pouvez vérifier `sousTotal` avant le calcul de la taxe
- Vous inspectez `taxe` pour vérifier le calcul
- Vous suivez l'exécution ligne par ligne

---

## Ouvrir les DevTools

### Raccourcis clavier

- **Windows/Linux** : F12 ou Ctrl + Shift + I
- **Mac** : Cmd + Option + I

### Par le menu

1. Clic droit n'importe où sur la page
2. Choisir "Inspecter" ou "Inspecter l'élément"

### Onglet Sources

Pour utiliser les breakpoints, allez dans l'onglet **Sources** (ou **Débogueur** dans Firefox).

**Structure de l'onglet Sources :**
- **Panneau gauche** : Liste des fichiers
- **Panneau central** : Code source
- **Panneau droit** : Outils de debugging (variables, call stack, etc.)

---

## Types de breakpoints

### 1. Breakpoint de ligne (Line Breakpoint)

C'est le type le plus courant : l'exécution s'arrête à une ligne précise.

#### Comment ajouter un breakpoint de ligne ?

**Méthode 1 : Clic dans la gouttière**

1. Ouvrez l'onglet Sources
2. Sélectionnez votre fichier JavaScript
3. Cliquez sur le **numéro de ligne** où vous voulez arrêter
4. Un point bleu apparaît 🔵

```javascript
function calculerPrix(prix, quantite) {
    const sousTotal = prix * quantite;  // 🔵 Clic sur le numéro de ligne
    const taxe = sousTotal * 0.20;
    return sousTotal + taxe;
}
```

**Méthode 2 : Instruction debugger dans le code**

```javascript
function calculerPrix(prix, quantite) {
    debugger;  // ⚠️ L'exécution s'arrête ici automatiquement
    const sousTotal = prix * quantite;
    const taxe = sousTotal * 0.20;
    return sousTotal + taxe;
}
```

> ⚠️ **Important** : N'oubliez pas de retirer les instructions `debugger` avant de mettre votre code en production !

#### Activer/Désactiver un breakpoint

- **Clic sur le point bleu** : désactive temporairement (devient gris)
- **Re-clic** : réactive le breakpoint
- **Clic droit > Remove breakpoint** : supprime définitivement

---

### 2. Breakpoint conditionnel (Conditional Breakpoint)

S'arrête seulement si une condition est vraie. Très utile dans les boucles !

#### Comment créer un breakpoint conditionnel ?

1. **Clic droit** sur le numéro de ligne
2. Sélectionner **"Add conditional breakpoint"**
3. Entrer la condition (ex: `i === 50`)
4. Un point orange apparaît 🟠

**Exemple :**

```javascript
for (let i = 0; i < 100; i++) {
    // 🟠 Breakpoint conditionnel : i === 50
    console.log(i);
    // S'arrête seulement quand i vaut 50
}
```

**Cas d'usage pratiques :**

```javascript
// S'arrêter pour un utilisateur spécifique
function traiterUtilisateur(user) {
    // Breakpoint conditionnel : user.id === 123
    console.log(user.nom);
}

// S'arrêter quand une variable atteint une valeur
function incrementer() {
    compteur++;
    // Breakpoint conditionnel : compteur > 1000
    console.log(compteur);
}

// S'arrêter sur les valeurs nulles/undefined
function traiterDonnees(data) {
    // Breakpoint conditionnel : data === null || data === undefined
    return data.valeur;
}
```

---

### 3. Breakpoint sur événement (Event Listener Breakpoint)

S'arrête quand un événement spécifique se produit (clic, clavier, etc.).

#### Comment utiliser ?

1. Dans le panneau droit des DevTools
2. Trouver la section **"Event Listener Breakpoints"**
3. Cocher le type d'événement souhaité

**Types d'événements disponibles :**

- **Mouse** : click, dblclick, mousedown, mouseup, mouseover
- **Keyboard** : keydown, keypress, keyup
- **Touch** : touchstart, touchend, touchmove
- **Form** : submit, reset, change
- **Timer** : setTimeout, setInterval
- **Script** : Script First Statement
- Et beaucoup d'autres...

**Exemple :**

```javascript
document.querySelector('#monBouton').addEventListener('click', function() {
    // Le debugger s'arrête ici si "Mouse > click" est coché
    console.log("Bouton cliqué !");
});
```

---

### 4. Breakpoint d'exception (Exception Breakpoint)

S'arrête automatiquement quand une erreur se produit.

#### Comment activer ?

Dans l'onglet Sources, cherchez l'icône **pause** (⏸️) et cochez :
- **"Pause on exceptions"** : s'arrête sur toutes les erreurs
- **"Pause on caught exceptions"** : s'arrête même sur les erreurs gérées avec try/catch

**Exemple :**

```javascript
try {
    const utilisateur = null;
    console.log(utilisateur.nom);  // ⏸️ S'arrête ici si activé
} catch (erreur) {
    console.error(erreur);
}
```

**Quand l'utiliser ?**
- Quand vous avez une erreur mais ne savez pas où
- Pour déboguer des erreurs intermittentes
- Pour comprendre le contexte d'une erreur

---

### 5. Breakpoint DOM (DOM Breakpoint)

S'arrête quand un élément HTML est modifié.

#### Comment créer ?

1. Allez dans l'onglet **Elements/Éléments**
2. **Clic droit** sur un élément
3. **Break on** > Choisir :
   - **Subtree modifications** : quand un enfant est ajouté/supprimé
   - **Attribute modifications** : quand un attribut change
   - **Node removal** : quand l'élément est supprimé

**Exemple :**

```html
<div id="container">
    <p>Contenu original</p>
</div>
```

```javascript
// Break on "Subtree modifications" sur #container
const container = document.querySelector('#container');
container.innerHTML = '<p>Nouveau contenu</p>';  // ⏸️ S'arrête ici
```

**Cas d'usage :**
- Trouver quel code modifie un élément
- Déboguer des changements DOM inattendus
- Comprendre quand une classe CSS est ajoutée/supprimée

---

## Contrôles de débogage (Debugging Controls)

Quand l'exécution est en pause sur un breakpoint, vous avez plusieurs boutons de contrôle :

### Les 5 boutons principaux

```
▶️ Resume (F8) - Reprendre l'exécution
⤵️ Step Over (F10) - Passer à la ligne suivante
⤴️ Step Into (F11) - Entrer dans la fonction
⤴️ Step Out (Shift+F11) - Sortir de la fonction actuelle
⏸️ Pause - Mettre en pause manuellement
```

### 1. Resume / Continue (▶️ ou F8)

**Reprend l'exécution** jusqu'au prochain breakpoint ou la fin du programme.

```javascript
function exemple() {
    console.log("Ligne 1");  // ⏸️ Breakpoint ici
    console.log("Ligne 2");
    console.log("Ligne 3");  // ⏸️ Breakpoint ici aussi
    console.log("Ligne 4");
}
```

Si vous appuyez sur **Resume** au premier breakpoint, le code continue jusqu'au second breakpoint.

---

### 2. Step Over (⤵️ ou F10)

**Exécute la ligne courante** et passe à la ligne suivante, **sans entrer** dans les fonctions.

```javascript
function addition(a, b) {
    return a + b;
}

function principale() {
    console.log("Début");       // ⏸️ En pause ici
    const resultat = addition(5, 3);  // F10 → exécute toute la fonction addition
    console.log(resultat);      // ⏸️ Arrive ici directement
}
```

**Utilisation :** Quand vous voulez avancer rapidement sans explorer les détails.

---

### 3. Step Into (⤴️ ou F11)

**Entre dans la fonction** appelée sur la ligne courante pour la déboguer en détail.

```javascript
function addition(a, b) {
    return a + b;               // ⏸️ Arrive ici si Step Into
}

function principale() {
    console.log("Début");       // ⏸️ En pause ici
    const resultat = addition(5, 3);  // F11 → entre dans addition()
    console.log(resultat);
}
```

**Utilisation :** Quand vous voulez voir exactement ce qui se passe dans une fonction.

---

### 4. Step Out (⤴️ ou Shift+F11)

**Sort de la fonction actuelle** et revient à l'appelant.

```javascript
function sousCalcul(x) {
    const y = x * 2;           // ⏸️ En pause ici
    return y;                  // Shift+F11 → sort directement
}

function calculPrincipal() {
    const resultat = sousCalcul(5);  // ⏸️ Revient ici
    console.log(resultat);
}
```

**Utilisation :** Quand vous êtes dans une fonction et voulez revenir rapidement à l'appelant.

---

## Panneaux d'inspection pendant le debugging

### Panneau Scope (Portée)

Affiche toutes les variables accessibles au point d'arrêt actuel.

**Structure :**
- **Local** : variables de la fonction actuelle
- **Global** : variables globales (window, document, etc.)
- **Closure** : variables des fonctions parentes (si applicable)

**Exemple :**

```javascript
const global = "Je suis global";

function externe() {
    const variableExterne = "Externe";

    function interne() {
        const variableLocale = "Locale";
        debugger;  // ⏸️ Pause ici
        // Scope affiche : Local, Closure (variableExterne), Global
    }

    interne();
}

externe();
```

### Panneau Watch (Surveillance)

Permet de surveiller des expressions spécifiques.

#### Comment ajouter une expression ?

1. Cliquez sur **"+"** dans le panneau Watch
2. Entrez une expression, par exemple :
   - `prix * quantite`
   - `utilisateur.nom`
   - `tableau.length`
   - `x > 100`

**Avantage :** Les expressions sont réévaluées à chaque pas, vous voyez leur évolution en temps réel.

### Panneau Call Stack (Pile d'appels)

Montre la **chaîne d'appels** de fonctions qui a mené au point actuel.

```javascript
function a() {
    b();
}

function b() {
    c();
}

function c() {
    debugger;  // ⏸️ Pause ici
}

a();
```

**Call Stack affiche :**
```
c (ligne 10)
b (ligne 6)
a (ligne 2)
(anonymous) (ligne 13)
```

Vous pouvez **cliquer** sur chaque fonction pour voir son code et ses variables !

---

## Workflow de debugging typique

### Scénario : Bug dans un calcul

**Le problème :**
```javascript
function calculerRemise(prix, pourcentage) {
    const remise = prix * pourcentage;
    const prixFinal = prix - remise;
    return prixFinal;
}

const resultat = calculerRemise(100, 20);
console.log(resultat);  // Résultat incorrect : -1900 au lieu de 80
```

**Étapes de debugging :**

1. **Placer un breakpoint** au début de la fonction
   ```javascript
   function calculerRemise(prix, pourcentage) {
       debugger;  // ⏸️ Ou clic sur le numéro de ligne
       const remise = prix * pourcentage;
       // ...
   ```

2. **Exécuter le code** - L'exécution s'arrête au breakpoint

3. **Inspecter les paramètres** dans le panneau Scope
   ```
   Local:
     prix: 100 ✅
     pourcentage: 20 ⚠️ (devrait être 0.20)
   ```

4. **Step Over (F10)** pour exécuter le calcul de remise

5. **Vérifier la valeur de remise** dans Scope
   ```
   Local:
     remise: 2000 ❌ (20% de 100 devrait être 20)
   ```

6. **Problème identifié !** Le pourcentage est 20 au lieu de 0.20

**Correction :**
```javascript
function calculerRemise(prix, pourcentageDecimal) {
    const remise = prix * pourcentageDecimal;
    const prixFinal = prix - remise;
    return prixFinal;
}

const resultat = calculerRemise(100, 0.20);  // ✅ Correction ici
console.log(resultat);  // 80 ✅
```

---

## Techniques avancées

### 1. Breakpoint dans un callback

```javascript
fetch('https://api.example.com/users')
    .then(response => {
        debugger;  // ⏸️ S'arrête quand la réponse arrive
        return response.json();
    })
    .then(data => {
        console.log(data);
    });
```

### 2. Breakpoint dans une boucle (avec condition)

```javascript
const tableau = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

for (let i = 0; i < tableau.length; i++) {
    // Breakpoint conditionnel : tableau[i] > 5
    console.log(tableau[i]);  // ⏸️ S'arrête seulement pour 6, 7, 8, 9, 10
}
```

### 3. Logpoint (Chrome uniquement)

Un **logpoint** affiche un message sans arrêter l'exécution.

**Comment créer :**
1. Clic droit sur le numéro de ligne
2. "Add logpoint"
3. Entrer le message : `"Valeur de i:", i`

**Avantage :** Comme un console.log mais sans modifier le code !

```javascript
for (let i = 0; i < 5; i++) {
    // 📍 Logpoint : "Itération", i
    // Affiche dans la console sans s'arrêter
}
```

### 4. Blackboxing (Ignorer du code)

Permet d'ignorer certains fichiers (comme les librairies) pendant le debugging.

**Comment :**
1. Onglet Sources
2. Clic droit sur un fichier
3. "Blackbox script"

**Effet :** Step Into ignorera ce fichier automatiquement.

---

## Console Commands pendant le debugging

Quand l'exécution est en pause, vous pouvez utiliser la console pour :

### Évaluer des expressions

```javascript
// Dans la console pendant le breakpoint
> prix * 2
200
> utilisateur.nom.toUpperCase()
"ALICE"
```

### Modifier des variables

```javascript
// Dans la console
> pourcentage = 0.20
0.20
// Puis continuez l'exécution avec les nouvelles valeurs !
```

### Tester du code

```javascript
// Dans la console
> const test = prix * 0.15
> test
15
```

---

## Raccourcis clavier utiles

| Raccourci | Action | Description |
|-----------|--------|-------------|
| **F8** | Resume | Continue l'exécution |
| **F10** | Step Over | Ligne suivante (sans entrer) |
| **F11** | Step Into | Entre dans la fonction |
| **Shift+F11** | Step Out | Sort de la fonction |
| **Ctrl+Shift+E** | Run snippet | Exécute du code dans Sources > Snippets |
| **Ctrl+P** | Ouvrir fichier | Recherche rapide de fichier |
| **Ctrl+Shift+F** | Rechercher | Recherche dans tous les fichiers |

---

## Astuces pratiques

### 1. Debugging de code minifié

Si votre code est minifié, cliquez sur **{}** (Pretty print) en bas du panneau Sources pour le reformater.

### 2. Snippets pour tests rapides

1. Onglet Sources > Snippets
2. New snippet
3. Écrivez du code de test
4. Ctrl+Enter pour exécuter

### 3. Copier la stack trace

Clic droit dans le panneau Call Stack > Copy stack trace

### 4. Désactiver tous les breakpoints temporairement

Icône de breakpoint en haut à gauche (devient gris)

### 5. Breakpoint sur la première ligne d'un script

Event Listener Breakpoints > Script > Script First Statement

---

## Exemple complet de session de debugging

**Code avec bug :**

```javascript
function calculerMoyenne(notes) {
    let total = 0;

    for (let i = 0; i <= notes.length; i++) {  // ⚠️ Bug : <= au lieu de <
        total += notes[i];
    }

    return total / notes.length;
}

const notes = [15, 18, 12, 16];
const moyenne = calculerMoyenne(notes);
console.log("Moyenne:", moyenne);  // NaN ❌
```

**Session de debugging :**

1. **Placer un breakpoint** dans la boucle for
2. **F5** pour recharger la page
3. **Inspecter i et notes.length** :
   ```
   Local:
     i: 0
     notes: [15, 18, 12, 16]
     notes.length: 4
   ```
4. **F10** plusieurs fois pour avancer dans la boucle
5. **Remarquer que i atteint 4** (notes[4] = undefined)
6. **Watch** : ajouter `notes[i]` → voir undefined à la dernière itération
7. **Bug trouvé** : `i <= notes.length` devrait être `i < notes.length`

**Correction :**
```javascript
for (let i = 0; i < notes.length; i++) {  // ✅
    total += notes[i];
}
```

---

## Comparaison : console.log vs Breakpoints

| Aspect | console.log | Breakpoints |
|--------|-------------|-------------|
| **Rapidité** | ✅ Rapide à ajouter | ⏱️ Nécessite de naviguer dans DevTools |
| **Précision** | ❌ Voit seulement ce qu'on log | ✅ Voit TOUT l'état du programme |
| **Modification code** | ❌ Doit modifier le code | ✅ Pas de modification |
| **Boucles** | ❌ Pollue la console | ✅ Breakpoint conditionnel |
| **Code asynchrone** | 🤷 Timing difficile | ✅ Pause au bon moment |
| **Exploration** | ❌ Limité | ✅ Peut tout explorer |

**Conclusion :** Utilisez les deux ! console.log pour des vérifications rapides, breakpoints pour du debugging approfondi.

---

## Points clés à retenir

1. **Les breakpoints mettent en pause** l'exécution pour inspecter l'état

2. **Il existe plusieurs types** : ligne, conditionnel, événement, exception, DOM

3. **Step Over, Step Into, Step Out** contrôlent l'avancement du debugging

4. **Le panneau Scope** montre toutes les variables accessibles

5. **La Call Stack** montre le chemin d'exécution

6. **Les breakpoints conditionnels** sont parfaits pour les boucles

7. **debugger;** dans le code crée un breakpoint automatique

8. **N'oubliez pas de retirer** les instructions debugger en production

---

## Conclusion

Les breakpoints sont un outil **indispensable** pour tout développeur JavaScript. Ils transforment le debugging d'un jeu de devinettes en une investigation méthodique et précise.

Au début, ils peuvent sembler complexes, mais avec la pratique, vous ne pourrez plus vous en passer !

> 💡 **Conseil final** : Commencez simplement avec des breakpoints de ligne et Step Over/Step Into. Une fois à l'aise, explorez les breakpoints conditionnels et DOM. Votre efficacité de debugging va être multipliée par 10 !

**Prochaines étapes :** Pratiquez ! Mettez des breakpoints dans votre code, explorez les variables, suivez le flux d'exécution. C'est en pratiquant qu'on maîtrise ces outils.

⏭️ [Concepts avancés](/05-javascript-moderne-fondamentaux/13-concepts-avances/README.md)
