🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.5 - Événements de formulaire

## Introduction

Les formulaires sont omniprésents sur le web : connexion, inscription, recherche, commentaires, etc. Les événements de formulaire permettent de créer des expériences utilisateur riches et interactives : validation en temps réel, suggestions automatiques, champs intelligents, et bien plus encore.

Dans cette leçon, nous allons explorer les événements essentiels pour travailler avec les formulaires.

## Vue d'ensemble des événements de formulaire

Voici les principaux événements de formulaire que vous utiliserez :

| Événement | Se déclenche quand... | Utilisation courante |
|-----------|----------------------|---------------------|
| `submit` | Le formulaire est soumis | Validation avant envoi |
| `input` | La valeur d'un champ change (en temps réel) | Validation instantanée, compteur de caractères |
| `change` | La valeur change ET l'élément perd le focus | Sélecteurs, cases à cocher |
| `focus` | Un champ reçoit le focus (devient actif) | Afficher des aides, modifier le style |
| `blur` | Un champ perd le focus (devient inactif) | Validation à la sortie du champ |

## 1. L'événement submit

### Quand se déclenche-t-il ?

L'événement `submit` se déclenche quand un formulaire est soumis, soit par :
- Un clic sur un bouton de type `submit`
- La touche `Enter` dans un champ texte du formulaire

### ⚠️ Comportement par défaut

Par défaut, la soumission d'un formulaire **recharge la page**. C'est presque toujours ce qu'on veut éviter en JavaScript moderne.

### Empêcher le rechargement de la page

Utilisez `event.preventDefault()` pour empêcher le comportement par défaut :

```html
<form id="monFormulaire">
    <input type="text" name="nom" placeholder="Votre nom" required>
    <button type="submit">Envoyer</button>
</form>
<p id="resultat"></p>
```

```javascript
const formulaire = document.getElementById('monFormulaire');
const resultat = document.getElementById('resultat');

formulaire.addEventListener('submit', (event) => {
    event.preventDefault(); // ⚠️ IMPORTANT : Empêche le rechargement

    const nom = event.target.nom.value;
    resultat.textContent = `Formulaire soumis pour : ${nom}`;
});
```

### ⚠️ Où attacher l'événement ?

L'événement `submit` s'attache au **formulaire** (`<form>`), **PAS** au bouton :

```javascript
// ✅ CORRECT - Sur le formulaire
formulaire.addEventListener('submit', handleSubmit);

// ❌ FAUX - Sur le bouton
bouton.addEventListener('click', handleSubmit);
```

**Pourquoi ?** Parce que le formulaire peut être soumis de plusieurs façons (bouton, touche Enter, etc.).

### Exemple : Validation avant soumission

```html
<form id="formInscription">
    <input type="email" id="email" placeholder="Email" required>
    <input type="password" id="password" placeholder="Mot de passe" required>
    <button type="submit">S'inscrire</button>
</form>
<p id="erreur" style="color: red;"></p>
```

```javascript
const form = document.getElementById('formInscription');
const erreur = document.getElementById('erreur');

form.addEventListener('submit', (event) => {
    event.preventDefault();

    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;

    // Validation personnalisée
    if (password.length < 8) {
        erreur.textContent = 'Le mot de passe doit contenir au moins 8 caractères';
        return;
    }

    if (!email.includes('@')) {
        erreur.textContent = 'Email invalide';
        return;
    }

    // Si tout est OK
    erreur.textContent = '';
    console.log('Formulaire valide !');
    console.log('Email:', email);
    console.log('Password:', password);

    // Ici, vous enverriez les données au serveur
});
```

### Accéder aux valeurs du formulaire

Il existe plusieurs façons d'accéder aux valeurs :

#### Méthode 1 : Via l'attribut `name`

```html
<form id="form">
    <input type="text" name="username" value="John">
    <input type="email" name="email" value="john@example.com">
</form>
```

```javascript
form.addEventListener('submit', (event) => {
    event.preventDefault();

    // Via event.target
    console.log(event.target.username.value); // "John"
    console.log(event.target.email.value);    // "john@example.com"
});
```

#### Méthode 2 : Via `getElementById`

```javascript
form.addEventListener('submit', (event) => {
    event.preventDefault();

    const username = document.getElementById('username').value;
    const email = document.getElementById('email').value;
});
```

#### Méthode 3 : Via `FormData` (moderne)

```javascript
form.addEventListener('submit', (event) => {
    event.preventDefault();

    const formData = new FormData(event.target);

    console.log(formData.get('username')); // "John"
    console.log(formData.get('email'));    // "john@example.com"

    // Ou créer un objet
    const data = Object.fromEntries(formData);
    console.log(data); // { username: "John", email: "john@example.com" }
});
```

## 2. L'événement input

### Quand se déclenche-t-il ?

L'événement `input` se déclenche **immédiatement** à chaque modification de la valeur d'un champ. C'est l'événement le plus réactif.

### Caractéristiques

- Se déclenche **à chaque caractère tapé**
- Se déclenche aussi pour copier/coller
- Fonctionne avec : `<input>`, `<textarea>`, `<select>` avec `contenteditable`

### Exemple : Compteur de caractères

```html
<textarea id="message" maxlength="280" placeholder="Écrivez votre message..."></textarea>
<p><span id="compteur">0</span> / 280 caractères</p>
```

```javascript
const message = document.getElementById('message');
const compteur = document.getElementById('compteur');

message.addEventListener('input', () => {
    compteur.textContent = message.value.length;
});
```

### Exemple : Validation en temps réel

```html
<input type="text" id="username" placeholder="Nom d'utilisateur">
<p id="feedback"></p>
```

```javascript
const username = document.getElementById('username');
const feedback = document.getElementById('feedback');

username.addEventListener('input', () => {
    const valeur = username.value;

    if (valeur.length === 0) {
        feedback.textContent = '';
        feedback.style.color = '';
    } else if (valeur.length < 3) {
        feedback.textContent = '❌ Trop court (minimum 3 caractères)';
        feedback.style.color = 'red';
    } else if (/[^a-zA-Z0-9_]/.test(valeur)) {
        feedback.textContent = '❌ Caractères spéciaux non autorisés';
        feedback.style.color = 'red';
    } else {
        feedback.textContent = '✓ Nom d'utilisateur valide';
        feedback.style.color = 'green';
    }
});
```

### Exemple : Recherche en temps réel

```html
<input type="text" id="recherche" placeholder="Rechercher un fruit...">
<ul id="resultats"></ul>
```

```javascript
const recherche = document.getElementById('recherche');
const resultats = document.getElementById('resultats');

const fruits = [
    'Pomme', 'Poire', 'Banane', 'Orange', 'Fraise',
    'Cerise', 'Raisin', 'Ananas', 'Kiwi', 'Mangue'
];

recherche.addEventListener('input', () => {
    const terme = recherche.value.toLowerCase();
    resultats.innerHTML = '';

    if (terme.length > 0) {
        const correspondances = fruits.filter(fruit =>
            fruit.toLowerCase().includes(terme)
        );

        if (correspondances.length === 0) {
            resultats.innerHTML = '<li>Aucun résultat</li>';
        } else {
            correspondances.forEach(fruit => {
                const li = document.createElement('li');
                li.textContent = fruit;
                resultats.appendChild(li);
            });
        }
    }
});
```

### Exemple : Formatage automatique (numéro de téléphone)

```html
<input type="text" id="telephone" placeholder="Téléphone" maxlength="14">
<p id="apercu"></p>
```

```javascript
const telephone = document.getElementById('telephone');
const apercu = document.getElementById('apercu');

telephone.addEventListener('input', (event) => {
    let valeur = event.target.value.replace(/\D/g, ''); // Garder que les chiffres

    // Formater : 06 12 34 56 78
    if (valeur.length > 0) {
        valeur = valeur.match(/.{1,2}/g).join(' ');
    }

    event.target.value = valeur;
    apercu.textContent = valeur ? `Format : ${valeur}` : '';
});
```

## 3. L'événement change

### Quand se déclenche-t-il ?

L'événement `change` se déclenche quand :
1. La valeur d'un champ **change**
2. **ET** le champ **perd le focus**

### Différence avec input

| Critère | input | change |
|---------|-------|--------|
| **Déclenchement** | À chaque modification | Quand le champ perd le focus |
| **Fréquence** | Très fréquent | Moins fréquent |
| **Utilisation** | Validation temps réel | Validation finale |
| **Champs texte** | Chaque caractère | À la sortie du champ |
| **Select/Checkbox** | Immédiat | Immédiat |

### Exemple : Différence input vs change sur un champ texte

```html
<input type="text" id="demo">
<p>input : <span id="countInput">0</span></p>
<p>change : <span id="countChange">0</span></p>
```

```javascript
const demo = document.getElementById('demo');
const countInput = document.getElementById('countInput');
const countChange = document.getElementById('countChange');
let compteurInput = 0;
let compteurChange = 0;

demo.addEventListener('input', () => {
    compteurInput++;
    countInput.textContent = compteurInput;
});

demo.addEventListener('change', () => {
    compteurChange++;
    countChange.textContent = compteurChange;
});

// Tapez plusieurs caractères : input augmente à chaque caractère
// Cliquez ailleurs : change augmente une seule fois
```

### Utilisation typique : Select, Checkbox, Radio

Pour les `<select>`, `<input type="checkbox">`, et `<input type="radio">`, `change` se déclenche **immédiatement** :

#### Exemple : Select (liste déroulante)

```html
<select id="pays">
    <option value="">Choisissez un pays</option>
    <option value="FR">France</option>
    <option value="BE">Belgique</option>
    <option value="CH">Suisse</option>
</select>
<p id="selection"></p>
```

```javascript
const pays = document.getElementById('pays');
const selection = document.getElementById('selection');

pays.addEventListener('change', (event) => {
    const valeur = event.target.value;
    const texte = event.target.options[event.target.selectedIndex].text;

    if (valeur) {
        selection.textContent = `Vous avez sélectionné : ${texte} (${valeur})`;
    }
});
```

#### Exemple : Checkbox

```html
<label>
    <input type="checkbox" id="accepte">
    J'accepte les conditions
</label>
<button id="btnSoumettre" disabled>Soumettre</button>
```

```javascript
const accepte = document.getElementById('accepte');
const btnSoumettre = document.getElementById('btnSoumettre');

accepte.addEventListener('change', (event) => {
    btnSoumettre.disabled = !event.target.checked;
});
```

#### Exemple : Radio buttons

```html
<p>Choisissez votre abonnement :</p>
<label><input type="radio" name="abonnement" value="gratuit"> Gratuit</label><br>
<label><input type="radio" name="abonnement" value="premium"> Premium (9.99€)</label><br>
<label><input type="radio" name="abonnement" value="entreprise"> Entreprise (49.99€)</label>
<p id="prix"></p>
```

```javascript
const radios = document.querySelectorAll('input[name="abonnement"]');
const prix = document.getElementById('prix');

const tarifs = {
    gratuit: '0€',
    premium: '9.99€/mois',
    entreprise: '49.99€/mois'
};

radios.forEach(radio => {
    radio.addEventListener('change', (event) => {
        prix.textContent = `Prix : ${tarifs[event.target.value]}`;
    });
});
```

## 4. L'événement focus

### Quand se déclenche-t-il ?

L'événement `focus` se déclenche quand un élément **reçoit le focus**, c'est-à-dire devient actif (l'utilisateur peut y taper).

### Comment un élément reçoit le focus ?

- L'utilisateur **clique** sur le champ
- L'utilisateur utilise la touche **Tab**
- Via JavaScript avec `element.focus()`

### Exemple : Afficher une aide au focus

```html
<input type="text" id="email" placeholder="Email">
<p id="aide" style="display: none; color: #666;">
    ℹ️ Entrez votre adresse email complète (ex: nom@exemple.com)
</p>
```

```javascript
const email = document.getElementById('email');
const aide = document.getElementById('aide');

email.addEventListener('focus', () => {
    aide.style.display = 'block';
});

email.addEventListener('blur', () => {
    aide.style.display = 'none';
});
```

### Exemple : Changer le style au focus

```html
<style>
    .champ-actif {
        border: 2px solid #4CAF50;
        background-color: #f0fff0;
    }
</style>

<input type="text" id="nom" placeholder="Nom">
<input type="text" id="prenom" placeholder="Prénom">
```

```javascript
const champs = document.querySelectorAll('input[type="text"]');

champs.forEach(champ => {
    champ.addEventListener('focus', () => {
        champ.classList.add('champ-actif');
    });

    champ.addEventListener('blur', () => {
        champ.classList.remove('champ-actif');
    });
});
```

### Exemple : Sélectionner automatiquement le contenu

```html
<input type="text" id="code" value="CODE-PROMO-2024">
<p>Cliquez dans le champ pour sélectionner automatiquement le code</p>
```

```javascript
const code = document.getElementById('code');

code.addEventListener('focus', () => {
    code.select(); // Sélectionne tout le texte
});
```

## 5. L'événement blur

### Quand se déclenche-t-il ?

L'événement `blur` se déclenche quand un élément **perd le focus**, c'est-à-dire devient inactif.

### Utilisation typique

L'événement `blur` est parfait pour la **validation finale** d'un champ quand l'utilisateur passe au champ suivant.

### Exemple : Validation à la sortie du champ

```html
<input type="email" id="email" placeholder="Email">
<p id="erreurEmail" style="color: red;"></p>

<input type="password" id="password" placeholder="Mot de passe">
<p id="erreurPassword" style="color: red;"></p>
```

```javascript
const email = document.getElementById('email');
const erreurEmail = document.getElementById('erreurEmail');

email.addEventListener('blur', () => {
    if (!email.value.includes('@')) {
        erreurEmail.textContent = 'Email invalide';
        email.style.borderColor = 'red';
    } else {
        erreurEmail.textContent = '';
        email.style.borderColor = '';
    }
});

const password = document.getElementById('password');
const erreurPassword = document.getElementById('erreurPassword');

password.addEventListener('blur', () => {
    if (password.value.length < 8) {
        erreurPassword.textContent = 'Le mot de passe doit contenir au moins 8 caractères';
        password.style.borderColor = 'red';
    } else {
        erreurPassword.textContent = '';
        password.style.borderColor = '';
    }
});
```

### Exemple : Formater la valeur à la sortie

```html
<input type="text" id="montant" placeholder="Montant">
<p id="apercu"></p>
```

```javascript
const montant = document.getElementById('montant');
const apercu = document.getElementById('apercu');

montant.addEventListener('blur', () => {
    const valeur = parseFloat(montant.value);

    if (!isNaN(valeur)) {
        montant.value = valeur.toFixed(2); // Format : 2 décimales
        apercu.textContent = `Montant : ${valeur.toFixed(2)} €`;
    }
});
```

## Exemples pratiques complets

### Exemple 1 : Formulaire de connexion complet

```html
<form id="formConnexion">
    <div>
        <input type="email" id="loginEmail" placeholder="Email" required>
        <span id="emailFeedback"></span>
    </div>

    <div>
        <input type="password" id="loginPassword" placeholder="Mot de passe" required>
        <span id="passwordFeedback"></span>
    </div>

    <button type="submit" id="btnConnexion">Se connecter</button>
</form>
<p id="messageConnexion"></p>
```

```javascript
const formConnexion = document.getElementById('formConnexion');
const loginEmail = document.getElementById('loginEmail');
const loginPassword = document.getElementById('loginPassword');
const emailFeedback = document.getElementById('emailFeedback');
const passwordFeedback = document.getElementById('passwordFeedback');
const messageConnexion = document.getElementById('messageConnexion');

// Validation email en temps réel
loginEmail.addEventListener('input', () => {
    if (loginEmail.value.includes('@')) {
        emailFeedback.textContent = '✓';
        emailFeedback.style.color = 'green';
    } else {
        emailFeedback.textContent = '❌';
        emailFeedback.style.color = 'red';
    }
});

// Validation password en temps réel
loginPassword.addEventListener('input', () => {
    if (loginPassword.value.length >= 8) {
        passwordFeedback.textContent = '✓';
        passwordFeedback.style.color = 'green';
    } else {
        passwordFeedback.textContent = '❌';
        passwordFeedback.style.color = 'red';
    }
});

// Soumission
formConnexion.addEventListener('submit', (event) => {
    event.preventDefault();

    if (!loginEmail.value.includes('@')) {
        messageConnexion.textContent = 'Email invalide';
        messageConnexion.style.color = 'red';
        return;
    }

    if (loginPassword.value.length < 8) {
        messageConnexion.textContent = 'Mot de passe trop court';
        messageConnexion.style.color = 'red';
        return;
    }

    messageConnexion.textContent = 'Connexion réussie !';
    messageConnexion.style.color = 'green';
});
```

### Exemple 2 : Formulaire avec confirmation de mot de passe

```html
<form id="formInscription">
    <input type="password" id="mdp" placeholder="Mot de passe">
    <input type="password" id="mdpConfirm" placeholder="Confirmer le mot de passe">
    <p id="match"></p>
    <button type="submit">S'inscrire</button>
</form>
```

```javascript
const mdp = document.getElementById('mdp');
const mdpConfirm = document.getElementById('mdpConfirm');
const match = document.getElementById('match');

function verifierCorrespondance() {
    if (mdp.value && mdpConfirm.value) {
        if (mdp.value === mdpConfirm.value) {
            match.textContent = '✓ Les mots de passe correspondent';
            match.style.color = 'green';
        } else {
            match.textContent = '❌ Les mots de passe ne correspondent pas';
            match.style.color = 'red';
        }
    } else {
        match.textContent = '';
    }
}

mdp.addEventListener('input', verifierCorrespondance);
mdpConfirm.addEventListener('input', verifierCorrespondance);
```

### Exemple 3 : Calcul automatique (total de commande)

```html
<form id="formCommande">
    <label>
        Quantité :
        <input type="number" id="quantite" value="1" min="1">
    </label>

    <label>
        Prix unitaire :
        <input type="number" id="prixUnitaire" value="10" step="0.01">
    </label>

    <p>Total : <strong id="total">10.00 €</strong></p>
</form>
```

```javascript
const quantite = document.getElementById('quantite');
const prixUnitaire = document.getElementById('prixUnitaire');
const total = document.getElementById('total');

function calculerTotal() {
    const q = parseFloat(quantite.value) || 0;
    const p = parseFloat(prixUnitaire.value) || 0;
    const t = q * p;

    total.textContent = t.toFixed(2) + ' €';
}

quantite.addEventListener('input', calculerTotal);
prixUnitaire.addEventListener('input', calculerTotal);
```

### Exemple 4 : Auto-complétion / Suggestions

```html
<input type="text" id="ville" placeholder="Entrez une ville" autocomplete="off">
<ul id="suggestions" style="border: 1px solid #ddd; max-height: 150px; overflow-y: auto; display: none;"></ul>
```

```javascript
const ville = document.getElementById('ville');
const suggestions = document.getElementById('suggestions');

const villes = [
    'Paris', 'Lyon', 'Marseille', 'Toulouse', 'Nice',
    'Nantes', 'Strasbourg', 'Montpellier', 'Bordeaux', 'Lille'
];

ville.addEventListener('input', () => {
    const terme = ville.value.toLowerCase();
    suggestions.innerHTML = '';

    if (terme.length > 0) {
        const correspondances = villes.filter(v =>
            v.toLowerCase().startsWith(terme)
        );

        if (correspondances.length > 0) {
            suggestions.style.display = 'block';
            correspondances.forEach(v => {
                const li = document.createElement('li');
                li.textContent = v;
                li.style.cursor = 'pointer';
                li.style.padding = '5px';

                li.addEventListener('click', () => {
                    ville.value = v;
                    suggestions.style.display = 'none';
                });

                suggestions.appendChild(li);
            });
        } else {
            suggestions.style.display = 'none';
        }
    } else {
        suggestions.style.display = 'none';
    }
});

// Cacher les suggestions si on clique ailleurs
ville.addEventListener('blur', () => {
    setTimeout(() => {
        suggestions.style.display = 'none';
    }, 200);
});
```

### Exemple 5 : Formulaire multi-étapes

```html
<form id="formMultiEtapes">
    <div id="etape1" class="etape">
        <h3>Étape 1 : Informations personnelles</h3>
        <input type="text" id="nom" placeholder="Nom" required>
        <input type="text" id="prenom" placeholder="Prénom" required>
        <button type="button" id="btnEtape1">Suivant</button>
    </div>

    <div id="etape2" class="etape" style="display: none;">
        <h3>Étape 2 : Contact</h3>
        <input type="email" id="emailEtape2" placeholder="Email" required>
        <input type="tel" id="tel" placeholder="Téléphone" required>
        <button type="button" id="btnRetour1">Retour</button>
        <button type="submit">Envoyer</button>
    </div>
</form>
```

```javascript
const etape1 = document.getElementById('etape1');
const etape2 = document.getElementById('etape2');
const btnEtape1 = document.getElementById('btnEtape1');
const btnRetour1 = document.getElementById('btnRetour1');

btnEtape1.addEventListener('click', () => {
    const nom = document.getElementById('nom').value;
    const prenom = document.getElementById('prenom').value;

    if (nom && prenom) {
        etape1.style.display = 'none';
        etape2.style.display = 'block';
    } else {
        alert('Veuillez remplir tous les champs');
    }
});

btnRetour1.addEventListener('click', () => {
    etape2.style.display = 'none';
    etape1.style.display = 'block';
});
```

## Bonnes pratiques

### ✅ 1. Toujours utiliser preventDefault() sur submit

```javascript
// ✅ BIEN - Empêche le rechargement
form.addEventListener('submit', (event) => {
    event.preventDefault();
    // Votre code
});

// ❌ MAUVAIS - La page va se recharger
form.addEventListener('submit', () => {
    // Votre code
});
```

### ✅ 2. Choisir le bon événement

```javascript
// Pour validation temps réel
champ.addEventListener('input', validerTempsReel);

// Pour validation finale
champ.addEventListener('blur', validerFinal);

// Pour select/checkbox/radio
element.addEventListener('change', handleChange);
```

### ✅ 3. Donner un retour visuel à l'utilisateur

```javascript
champ.addEventListener('input', () => {
    if (estValide(champ.value)) {
        champ.style.borderColor = 'green';
        feedback.textContent = '✓';
    } else {
        champ.style.borderColor = 'red';
        feedback.textContent = '❌';
    }
});
```

### ✅ 4. Valider côté client ET côté serveur

La validation JavaScript côté client améliore l'expérience utilisateur, mais **ne remplace pas** la validation côté serveur (pour la sécurité).

### ✅ 5. Utiliser les attributs HTML5 de validation

Combinez JavaScript avec les attributs HTML5 :

```html
<input type="email" required minlength="3" maxlength="50">
<input type="number" min="0" max="100" step="5">
<input type="text" pattern="[A-Za-z]{3,}">
```

### ✅ 6. Désactiver le bouton pendant la soumission

```javascript
form.addEventListener('submit', async (event) => {
    event.preventDefault();

    const bouton = event.target.querySelector('button[type="submit"]');
    bouton.disabled = true;
    bouton.textContent = 'Envoi en cours...';

    try {
        // Envoyer les données
        await envoyerDonnees();
        alert('Succès !');
    } catch (erreur) {
        alert('Erreur : ' + erreur.message);
    } finally {
        bouton.disabled = false;
        bouton.textContent = 'Envoyer';
    }
});
```

## Résumé des événements de formulaire

| Événement | Quand | Fréquence | Utilisation |
|-----------|-------|-----------|-------------|
| **submit** | Formulaire soumis | Une fois | Validation finale, envoi données |
| **input** | Valeur change (immédiat) | Très fréquent | Validation temps réel, compteurs |
| **change** | Valeur change + perd focus | Modéré | Select, checkbox, radio |
| **focus** | Reçoit le focus | Une fois | Afficher aides, styles |
| **blur** | Perd le focus | Une fois | Validation finale du champ |

## Ce qu'il faut retenir

✅ **submit** s'attache au `<form>`, pas au bouton

✅ **Toujours utiliser preventDefault()** sur submit pour éviter le rechargement

✅ **input** est parfait pour la validation en temps réel (chaque caractère)

✅ **change** est idéal pour select, checkbox, radio (et validation finale des champs texte)

✅ **focus/blur** permettent d'améliorer l'expérience utilisateur (aides, styles)

✅ **Combiner plusieurs événements** pour une validation complète

✅ **Valider côté client ET serveur** pour sécurité et UX

## Dans la prochaine leçon

Maintenant que vous maîtrisez les événements de formulaire, nous allons explorer **l'objet Event** en détail et ses propriétés utiles.

Vous découvrirez :
- Les propriétés communes de l'objet Event
- La différence entre target et currentTarget
- Comment manipuler et inspecter les événements
- Les méthodes importantes (preventDefault, stopPropagation)

---


⏭️ [L'objet Event et ses propriétés](/05-javascript-moderne-fondamentaux/10-evenements/06-objet-event.md)
