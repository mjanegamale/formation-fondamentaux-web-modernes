🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.4.4 Validation native HTML5

## Introduction

Avant HTML5, la validation des formulaires nécessitait obligatoirement du JavaScript ou une validation côté serveur après l'envoi. HTML5 a changé la donne en introduisant la **validation native**, directement intégrée dans le navigateur.

Avec la validation native HTML5, vous pouvez :
- Vérifier que les champs obligatoires sont remplis
- Valider automatiquement les formats (email, URL, nombre)
- Définir des règles personnalisées (expressions régulières)
- Limiter les valeurs (longueur, plage de nombres, dates)
- Tout cela **sans écrire une ligne de JavaScript** !

Dans ce chapitre, nous allons découvrir tous les outils de validation que HTML5 met à votre disposition.

---

## Pourquoi utiliser la validation native ?

### Avantages

**✅ Simplicité**
- Pas besoin de JavaScript (pour les cas basiques)
- Attributs HTML simples à comprendre
- Fonctionne immédiatement

**✅ Performance**
- Validation instantanée côté client
- Pas d'aller-retour serveur pour vérifier
- Meilleure expérience utilisateur

**✅ Accessibilité**
- Messages d'erreur natifs dans la langue du navigateur
- Compatible avec les lecteurs d'écran
- Standards du web respectés

**✅ Compatibilité**
- Supporté par tous les navigateurs modernes
- Dégradation gracieuse sur les anciens navigateurs

### Limites

**⚠️ Important à comprendre :**

La validation HTML5 est une **première ligne de défense**, mais :

1. **Elle peut être contournée** (désactivation JavaScript, manipulation HTML)
2. **Elle n'est pas suffisante seule** : Validation serveur OBLIGATOIRE
3. **Messages parfois limités** : Personnalisation difficile sans JavaScript
4. **Comportement variable** selon les navigateurs

```
┌─────────────────────────────────────────────┐
│  Validation HTML5 (Côté Client)             │
│  ↓                                          │
│  Validation JavaScript avancée (optionnel)  │
│  ↓                                          │
│  Validation Serveur (OBLIGATOIRE)           │
└─────────────────────────────────────────────┘
```

**Règle d'or :** La validation HTML5 améliore l'expérience utilisateur, mais ne remplace JAMAIS la validation serveur.

---

## L'attribut `required` - Champ obligatoire

### Fonctionnement

L'attribut `required` rend un champ obligatoire. Le formulaire ne peut pas être soumis si le champ est vide.

```html
<label for="nom">Nom * :</label>
<input type="text" id="nom" name="nom" required>
```

**Comportement :**
- Si l'utilisateur essaie de soumettre avec le champ vide, le navigateur affiche un message d'erreur
- Le focus est automatiquement placé sur le premier champ invalide
- La soumission du formulaire est bloquée

### Exemples

```html
<!-- Champ texte obligatoire -->
<input type="text" name="nom" required>

<!-- Email obligatoire -->
<input type="email" name="email" required>

<!-- Textarea obligatoire -->
<textarea name="message" required></textarea>

<!-- Select obligatoire -->
<select name="pays" required>
    <option value="">-- Choisir --</option>
    <option value="FR">France</option>
    <option value="BE">Belgique</option>
</select>

<!-- Checkbox obligatoire -->
<input type="checkbox" name="cgu" value="accepte" required>
<label for="cgu">J'accepte les CGU</label>

<!-- Au moins un radio obligatoire -->
<input type="radio" name="civilite" value="mr" required>
<label>M.</label>
<input type="radio" name="civilite" value="mme" required>
<label>Mme</label>
```

### ⚠️ Cas particuliers

#### Select avec required

Pour qu'un `<select>` avec `required` fonctionne, la première option doit avoir une valeur vide :

```html
<!-- ✅ BON : option vide par défaut -->
<select name="pays" required>
    <option value="">-- Sélectionner un pays --</option>
    <option value="FR">France</option>
    <option value="BE">Belgique</option>
</select>

<!-- ❌ MAUVAIS : pas d'option vide -->
<select name="pays" required>
    <option value="FR">France</option>
    <option value="BE">Belgique</option>
</select>
<!-- L'utilisateur ne pourra pas "ne rien choisir", donc required ne sert à rien -->
```

#### Radio buttons

Pour les radio buttons, `required` doit être sur **tous les boutons** du groupe (même si un seul suffit techniquement) :

```html
<!-- ✅ RECOMMANDÉ : required sur tous -->
<input type="radio" id="oui" name="reponse" value="oui" required>
<label for="oui">Oui</label>

<input type="radio" id="non" name="reponse" value="non" required>
<label for="non">Non</label>
```

---

## Validation automatique par type d'input

Certains types d'inputs ont une validation automatique intégrée.

### `type="email"` - Format email

```html
<label for="email">Email :</label>
<input type="email" id="email" name="email" required>
```

**Validation automatique :**
- Vérifie la présence de `@`
- Vérifie qu'il y a du texte avant et après `@`
- Vérifie la présence d'un point dans le domaine

```
Accepté : jean@example.com
Refusé : jean@example (pas de domaine complet)
Refusé : jean.example.com (pas de @)
Refusé : @example.com (pas de partie locale)
```

**Permettre plusieurs emails :**

```html
<input type="email" name="emails" multiple required>
<!-- Accepte : email1@ex.com, email2@ex.com -->
```

### `type="url"` - Format URL

```html
<label for="site">Site web :</label>
<input type="url" id="site" name="site" required>
```

**Validation automatique :**
- Vérifie la présence d'un protocole (`http://` ou `https://`)
- Vérifie la structure générale d'une URL

```
Accepté : https://example.com
Accepté : http://example.com
Refusé : example.com (pas de protocole)
Refusé : www.example.com (pas de protocole)
```

### `type="number"` - Nombre

```html
<label for="age">Âge :</label>
<input type="number" id="age" name="age" min="18" max="120" required>
```

**Validation automatique :**
- Accepte uniquement des nombres
- Respecte `min` et `max` si spécifiés
- Respecte `step` si spécifié

### `type="date"`, `type="time"`, etc.

Les types de date ont une validation automatique de format :

```html
<!-- Format YYYY-MM-DD obligatoire -->
<input type="date" name="naissance" min="1900-01-01" max="2024-12-31" required>

<!-- Format HH:MM obligatoire -->
<input type="time" name="heure" min="09:00" max="18:00" required>
```

---

## Attributs de validation

HTML5 offre plusieurs attributs pour définir des règles de validation précises.

### `minlength` et `maxlength` - Longueur de texte

Définit la longueur minimale et maximale d'un champ texte.

```html
<!-- Nom d'utilisateur : 3 à 20 caractères -->
<label for="username">Nom d'utilisateur :</label>
<input type="text"
       id="username"
       name="username"
       minlength="3"
       maxlength="20"
       required>

<!-- Mot de passe : minimum 8 caractères -->
<label for="password">Mot de passe :</label>
<input type="password"
       id="password"
       name="password"
       minlength="8"
       required>

<!-- Tweet : maximum 280 caractères -->
<textarea name="tweet" maxlength="280" required></textarea>
```

**Notes :**
- `maxlength` **empêche physiquement** de taper plus de caractères
- `minlength` valide uniquement à la soumission
- Les espaces comptent dans la longueur

### `min` et `max` - Plage de valeurs

Pour les nombres, dates et heures.

```html
<!-- Âge entre 18 et 120 -->
<input type="number" name="age" min="18" max="120" required>

<!-- Quantité entre 1 et 100 -->
<input type="number" name="quantite" min="1" max="100" value="1" required>

<!-- Date entre aujourd'hui et dans 1 an -->
<input type="date"
       name="reservation"
       min="2024-12-03"
       max="2025-12-03"
       required>

<!-- Heure entre 9h et 18h -->
<input type="time" name="rdv" min="09:00" max="18:00" required>

<!-- Prix minimum 0.01 -->
<input type="number" name="prix" min="0.01" step="0.01" required>
```

### `step` - Incrément

Définit l'incrément autorisé pour les nombres et dates.

```html
<!-- Nombre entier uniquement (pas de décimales) -->
<input type="number" name="entier" step="1">

<!-- Nombres avec 2 décimales (prix) -->
<input type="number" name="prix" step="0.01" min="0">

<!-- Incréments de 5 -->
<input type="number" name="age" min="18" max="120" step="5">

<!-- Pas de 30 minutes -->
<input type="time" name="heure" step="1800">
<!-- 1800 secondes = 30 minutes -->
```

**Valeurs spéciales :**
- `step="1"` : Entiers (défaut pour number)
- `step="0.01"` : 2 décimales (prix)
- `step="0.1"` : 1 décimale
- `step="any"` : Aucune restriction

### `pattern` - Expression régulière (regex)

L'attribut le plus puissant : permet de définir un motif personnalisé avec une expression régulière.

```html
<!-- Code postal français (5 chiffres) -->
<input type="text"
       name="code_postal"
       pattern="[0-9]{5}"
       title="Code postal à 5 chiffres"
       placeholder="75001"
       required>

<!-- Téléphone français -->
<input type="tel"
       name="telephone"
       pattern="0[1-9][0-9]{8}"
       title="Numéro à 10 chiffres commençant par 0"
       placeholder="0612345678"
       required>

<!-- Plaque d'immatriculation française -->
<input type="text"
       name="plaque"
       pattern="[A-Z]{2}-[0-9]{3}-[A-Z]{2}"
       title="Format: AA-123-BB"
       placeholder="AB-123-CD"
       required>

<!-- Nom d'utilisateur (lettres, chiffres, -, _) -->
<input type="text"
       name="username"
       pattern="[a-zA-Z0-9_-]{3,16}"
       title="3 à 16 caractères : lettres, chiffres, tiret ou underscore"
       required>

<!-- Mot de passe fort -->
<input type="password"
       name="password"
       pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}"
       title="Minimum 8 caractères avec au moins une majuscule, une minuscule et un chiffre"
       required>
```

**Attribut `title` :** Très important ! Il définit le message d'aide affiché si la validation échoue.

#### Syntaxe des regex courantes

```html
<!-- Exactement 5 chiffres -->
pattern="[0-9]{5}"

<!-- 3 à 16 caractères alphanumériques -->
pattern="[a-zA-Z0-9]{3,16}"

<!-- Que des lettres (avec espaces) -->
pattern="[A-Za-zÀ-ÿ\s]+"

<!-- Email personnalisé (plus strict) -->
pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"

<!-- Hexadécimal (couleur) -->
pattern="#[0-9A-Fa-f]{6}"

<!-- URL simple -->
pattern="https?://.+"

<!-- Numéro de téléphone international -->
pattern="\+?[0-9\s\-\(\)]+"
```

**⚠️ Attention :** L'attribut `pattern` est validé par rapport à la **valeur entière** du champ, pas à une partie.

---

## Messages d'erreur natifs

### Messages par défaut

Chaque navigateur affiche ses propres messages d'erreur natifs :

**Chrome (français) :**
- Champ vide + required : "Veuillez remplir ce champ."
- Email invalide : "Veuillez inclure un '@' dans l'adresse e-mail."
- Pattern non respecté : "Veuillez respecter le format demandé."

**Firefox (français) :**
- Champ vide + required : "Veuillez remplir ce champ."
- Email invalide : "Veuillez saisir une adresse e-mail."

Les messages sont automatiquement dans la langue du navigateur.

### Améliorer les messages avec `title`

L'attribut `title` fournit des informations supplémentaires dans la bulle d'erreur :

```html
<!-- Sans title : message générique -->
<input type="text"
       name="code"
       pattern="[0-9]{6}"
       required>
<!-- Message : "Veuillez respecter le format demandé." -->

<!-- Avec title : message plus précis -->
<input type="text"
       name="code"
       pattern="[0-9]{6}"
       title="Code à 6 chiffres"
       required>
<!-- Message : "Veuillez respecter le format demandé. Code à 6 chiffres" -->
```

**Conseil :** Toujours ajouter un `title` explicite avec `pattern`.

---

## Personnaliser les messages d'erreur avec JavaScript

Pour des messages complètement personnalisés, utilisez `setCustomValidity()` en JavaScript.

### Méthode `setCustomValidity()`

```html
<form id="mon-formulaire">
    <label for="email">Email :</label>
    <input type="email" id="email" name="email" required>

    <button type="submit">Envoyer</button>
</form>

<script>
const emailInput = document.getElementById('email');

emailInput.addEventListener('invalid', function(e) {
    if (emailInput.validity.valueMissing) {
        emailInput.setCustomValidity('Merci de renseigner votre adresse email');
    } else if (emailInput.validity.typeMismatch) {
        emailInput.setCustomValidity('Cette adresse email semble incorrecte');
    }
});

// IMPORTANT : Reset le message quand l'utilisateur tape
emailInput.addEventListener('input', function() {
    emailInput.setCustomValidity('');
});
</script>
```

**⚠️ CRUCIAL :** Il faut réinitialiser le message avec `setCustomValidity('')` quand l'utilisateur modifie le champ, sinon il reste bloqué !

### Exemple : Vérifier que deux mots de passe correspondent

```html
<form>
    <div>
        <label for="password">Mot de passe :</label>
        <input type="password" id="password" name="password" minlength="8" required>
    </div>

    <div>
        <label for="password-confirm">Confirmer le mot de passe :</label>
        <input type="password" id="password-confirm" name="password_confirm" required>
    </div>

    <button type="submit">S'inscrire</button>
</form>

<script>
const password = document.getElementById('password');
const passwordConfirm = document.getElementById('password-confirm');

function validatePassword() {
    if (password.value !== passwordConfirm.value) {
        passwordConfirm.setCustomValidity('Les mots de passe ne correspondent pas');
    } else {
        passwordConfirm.setCustomValidity('');
    }
}

password.addEventListener('change', validatePassword);
passwordConfirm.addEventListener('input', validatePassword);
</script>
```

---

## L'API Constraint Validation

JavaScript offre une API complète pour interagir avec la validation HTML5.

### Propriété `validity`

L'objet `validity` contient l'état de validation d'un champ :

```javascript
const input = document.getElementById('email');

// L'objet validity contient :
console.log(input.validity);

/*
ValidityState {
    valueMissing: false,     // required non rempli
    typeMismatch: false,     // type invalide (email, url)
    patternMismatch: false,  // pattern non respecté
    tooLong: false,          // > maxlength
    tooShort: false,         // < minlength
    rangeUnderflow: false,   // < min
    rangeOverflow: false,    // > max
    stepMismatch: false,     // step non respecté
    badInput: false,         // entrée invalide
    customError: false,      // setCustomValidity() utilisé
    valid: true              // Globalement valide
}
*/
```

### Méthode `checkValidity()`

Vérifie la validité et déclenche l'événement `invalid` si invalide :

```javascript
const form = document.getElementById('mon-formulaire');

form.addEventListener('submit', function(e) {
    if (!form.checkValidity()) {
        e.preventDefault();
        console.log('Formulaire invalide');
    }
});
```

### Méthode `reportValidity()`

Comme `checkValidity()` mais affiche aussi les messages d'erreur natifs :

```javascript
const form = document.getElementById('mon-formulaire');

// Valider et afficher les erreurs
if (!form.reportValidity()) {
    console.log('Des erreurs sont présentes');
}
```

### Propriété `validationMessage`

Contient le message d'erreur actuel :

```javascript
const input = document.getElementById('email');

console.log(input.validationMessage);
// "Veuillez remplir ce champ" ou message personnalisé
```

### Exemple complet de validation JavaScript

```html
<form id="contact-form">
    <div>
        <label for="nom">Nom :</label>
        <input type="text" id="nom" name="nom" required>
        <span class="error" id="nom-error"></span>
    </div>

    <div>
        <label for="email">Email :</label>
        <input type="email" id="email" name="email" required>
        <span class="error" id="email-error"></span>
    </div>

    <button type="submit">Envoyer</button>
</form>

<script>
const form = document.getElementById('contact-form');
const inputs = form.querySelectorAll('input');

// Valider un champ individuel
function validateField(input) {
    const errorSpan = document.getElementById(input.id + '-error');

    if (!input.validity.valid) {
        // Champ invalide
        input.classList.add('invalid');

        // Message personnalisé
        let message = '';
        if (input.validity.valueMissing) {
            message = 'Ce champ est obligatoire';
        } else if (input.validity.typeMismatch) {
            message = 'Format invalide';
        } else if (input.validity.tooShort) {
            message = `Minimum ${input.minLength} caractères`;
        }

        errorSpan.textContent = message;
        return false;
    } else {
        // Champ valide
        input.classList.remove('invalid');
        errorSpan.textContent = '';
        return true;
    }
}

// Valider tous les champs
inputs.forEach(input => {
    input.addEventListener('blur', function() {
        validateField(input);
    });

    input.addEventListener('input', function() {
        if (input.classList.contains('invalid')) {
            validateField(input);
        }
    });
});

// Validation à la soumission
form.addEventListener('submit', function(e) {
    let isValid = true;

    inputs.forEach(input => {
        if (!validateField(input)) {
            isValid = false;
        }
    });

    if (!isValid) {
        e.preventDefault();
        inputs[0].focus(); // Focus sur le premier champ invalide
    }
});
</script>

<style>
.invalid {
    border-color: #e74c3c;
    background-color: #fee;
}

.error {
    display: block;
    color: #e74c3c;
    font-size: 0.9em;
    margin-top: 0.25rem;
}
</style>
```

---

## Pseudo-classes CSS pour la validation

HTML5 offre des pseudo-classes CSS pour styliser les champs selon leur état de validation.

### `:valid` et `:invalid`

```css
/* Champ valide */
input:valid {
    border-color: #27ae60;
    background-color: #eafaf1;
}

/* Champ invalide */
input:invalid {
    border-color: #e74c3c;
    background-color: #fee;
}
```

**⚠️ Problème :** Un champ vide avec `required` est considéré `:invalid` dès le chargement !

**Solution :** Utiliser `:invalid` uniquement après interaction :

```css
/* Invalide uniquement après avoir quitté le champ */
input:invalid:not(:focus):not(:placeholder-shown) {
    border-color: #e74c3c;
}

/* Ou après soumission (ajouter une classe au formulaire) */
form.submitted input:invalid {
    border-color: #e74c3c;
}
```

### `:required` et `:optional`

```css
/* Champs obligatoires */
input:required {
    border-left: 3px solid #e74c3c;
}

/* Champs optionnels */
input:optional {
    border-left: 3px solid #95a5a6;
}
```

### `:in-range` et `:out-of-range`

Pour les inputs de type `number`, `date`, `time` :

```css
/* Valeur dans la plage autorisée */
input[type="number"]:in-range {
    border-color: #27ae60;
}

/* Valeur hors de la plage */
input[type="number"]:out-of-range {
    border-color: #e74c3c;
}
```

### `:placeholder-shown`

Détecte si le placeholder est visible (champ vide) :

```css
/* Style quand le champ est vide */
input:placeholder-shown {
    border-color: #bdc3c7;
}

/* Afficher le label uniquement quand le champ est rempli */
input:not(:placeholder-shown) + label {
    display: block;
}
```

### Exemple complet de styling

```html
<style>
.form-group {
    position: relative;
    margin-bottom: 1.5rem;
}

.form-group input {
    width: 100%;
    padding: 0.75rem;
    border: 2px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
    transition: all 0.3s ease;
}

/* État initial */
.form-group input:focus {
    outline: none;
    border-color: #3498db;
    box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

/* Champ valide (après interaction) */
.form-group input:valid:not(:placeholder-shown) {
    border-color: #27ae60;
}

/* Icône de validation */
.form-group input:valid:not(:placeholder-shown) {
    background-image: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 20 20"><path fill="%2327ae60" d="M0 11l2-2 5 5L18 3l2 2L7 18z"/></svg>');
    background-repeat: no-repeat;
    background-position: right 0.75rem center;
    background-size: 1.25rem;
    padding-right: 2.5rem;
}

/* Champ invalide (après interaction) */
.form-group input:invalid:not(:focus):not(:placeholder-shown) {
    border-color: #e74c3c;
    background-color: #fff5f5;
}

/* Icône d'erreur */
.form-group input:invalid:not(:focus):not(:placeholder-shown) {
    background-image: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 20 20"><path fill="%23e74c3c" d="M10 0C4.5 0 0 4.5 0 10s4.5 10 10 10 10-4.5 10-10S15.5 0 10 0zm1 15H9v-2h2v2zm0-4H9V5h2v6z"/></svg>');
    background-repeat: no-repeat;
    background-position: right 0.75rem center;
    background-size: 1.25rem;
    padding-right: 2.5rem;
}

/* Champs obligatoires */
.form-group input:required {
    border-left-width: 4px;
}
</style>

<form>
    <div class="form-group">
        <label for="email">Email :</label>
        <input type="email"
               id="email"
               name="email"
               placeholder="votre@email.com"
               required>
    </div>

    <div class="form-group">
        <label for="age">Âge :</label>
        <input type="number"
               id="age"
               name="age"
               min="18"
               max="120"
               placeholder="18"
               required>
    </div>

    <button type="submit">Envoyer</button>
</form>
```

---

## Désactiver la validation : `novalidate`

### Sur le formulaire entier

L'attribut `novalidate` sur `<form>` désactive toute la validation HTML5 :

```html
<form action="/contact" method="post" novalidate>
    <input type="email" name="email" required>
    <button type="submit">Envoyer</button>
</form>
```

**Quand l'utiliser :**
- Vous implémentez votre propre validation JavaScript
- Vous voulez tester sans validation
- Formulaires complexes avec logique personnalisée

### Sur un bouton spécifique

L'attribut `formnovalidate` sur un bouton désactive la validation pour ce bouton uniquement :

```html
<form action="/save" method="post">
    <input type="email" name="email" required>

    <!-- Soumet avec validation -->
    <button type="submit">Enregistrer</button>

    <!-- Soumet SANS validation (brouillon) -->
    <button type="submit" formnovalidate>Sauvegarder comme brouillon</button>
</form>
```

---

## Exemples pratiques complets

### Exemple 1 : Formulaire de contact avec validation complète

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contact</title>
    <style>
        .form-group {
            margin-bottom: 1.5rem;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        input, textarea, select {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #3498db;
        }

        /* Validation visuelle */
        input:valid:not(:placeholder-shown),
        textarea:valid:not(:placeholder-shown) {
            border-color: #27ae60;
        }

        input:invalid:not(:focus):not(:placeholder-shown),
        textarea:invalid:not(:focus):not(:placeholder-shown) {
            border-color: #e74c3c;
        }

        .requis {
            color: #e74c3c;
        }

        small {
            display: block;
            margin-top: 0.25rem;
            color: #7f8c8d;
            font-size: 0.9em;
        }

        button {
            background-color: #3498db;
            color: white;
            padding: 0.75rem 2rem;
            border: none;
            border-radius: 4px;
            font-size: 1rem;
            cursor: pointer;
        }

        button:hover {
            background-color: #2980b9;
        }
    </style>
</head>
<body>
    <h1>Contactez-nous</h1>

    <form action="/contact" method="post">
        <p><small><span class="requis">*</span> Champs obligatoires</small></p>

        <div class="form-group">
            <label for="nom">
                Nom complet <span class="requis">*</span> :
            </label>
            <input type="text"
                   id="nom"
                   name="nom"
                   minlength="2"
                   maxlength="100"
                   placeholder="Jean Dupont"
                   required>
            <small>Entre 2 et 100 caractères</small>
        </div>

        <div class="form-group">
            <label for="email">
                Email <span class="requis">*</span> :
            </label>
            <input type="email"
                   id="email"
                   name="email"
                   placeholder="jean@example.com"
                   autocomplete="email"
                   required>
        </div>

        <div class="form-group">
            <label for="telephone">
                Téléphone <span class="requis">*</span> :
            </label>
            <input type="tel"
                   id="telephone"
                   name="telephone"
                   pattern="0[1-9][0-9]{8}"
                   title="Numéro français à 10 chiffres commençant par 0"
                   placeholder="0612345678"
                   required>
            <small>Format : 0612345678</small>
        </div>

        <div class="form-group">
            <label for="sujet">
                Sujet <span class="requis">*</span> :
            </label>
            <select id="sujet" name="sujet" required>
                <option value="">-- Choisir un sujet --</option>
                <option value="info">Demande d'information</option>
                <option value="devis">Demande de devis</option>
                <option value="support">Support technique</option>
                <option value="autre">Autre</option>
            </select>
        </div>

        <div class="form-group">
            <label for="message">
                Message <span class="requis">*</span> :
            </label>
            <textarea id="message"
                      name="message"
                      rows="6"
                      minlength="10"
                      maxlength="500"
                      placeholder="Votre message..."
                      required></textarea>
            <small>Entre 10 et 500 caractères</small>
        </div>

        <div class="form-group">
            <input type="checkbox"
                   id="copie"
                   name="copie"
                   value="oui">
            <label for="copie" style="display: inline; font-weight: normal;">
                Recevoir une copie par email
            </label>
        </div>

        <button type="submit">Envoyer le message</button>
    </form>
</body>
</html>
```

### Exemple 2 : Formulaire d'inscription avec validation JavaScript

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Inscription</title>
    <style>
        .form-group {
            margin-bottom: 1.5rem;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        input {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid #ddd;
            border-radius: 4px;
        }

        .error-message {
            display: none;
            color: #e74c3c;
            font-size: 0.9em;
            margin-top: 0.25rem;
        }

        .error-message.visible {
            display: block;
        }

        input.invalid {
            border-color: #e74c3c;
            background-color: #fff5f5;
        }

        input.valid {
            border-color: #27ae60;
        }

        .password-strength {
            height: 4px;
            background: #ddd;
            border-radius: 2px;
            margin-top: 0.5rem;
            overflow: hidden;
        }

        .password-strength-bar {
            height: 100%;
            width: 0%;
            transition: all 0.3s;
        }

        .password-strength-bar.weak {
            width: 33%;
            background: #e74c3c;
        }

        .password-strength-bar.medium {
            width: 66%;
            background: #f39c12;
        }

        .password-strength-bar.strong {
            width: 100%;
            background: #27ae60;
        }

        button {
            background: #3498db;
            color: white;
            padding: 0.75rem 2rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
        }
    </style>
</head>
<body>
    <h1>Créer un compte</h1>

    <form id="signup-form" action="/inscription" method="post" novalidate>
        <div class="form-group">
            <label for="username">Nom d'utilisateur * :</label>
            <input type="text"
                   id="username"
                   name="username"
                   minlength="3"
                   maxlength="20"
                   pattern="[a-zA-Z0-9_-]+"
                   required>
            <span class="error-message" id="username-error"></span>
        </div>

        <div class="form-group">
            <label for="email">Email * :</label>
            <input type="email" id="email" name="email" required>
            <span class="error-message" id="email-error"></span>
        </div>

        <div class="form-group">
            <label for="password">Mot de passe * :</label>
            <input type="password"
                   id="password"
                   name="password"
                   minlength="8"
                   required>
            <div class="password-strength">
                <div class="password-strength-bar" id="strength-bar"></div>
            </div>
            <span class="error-message" id="password-error"></span>
        </div>

        <div class="form-group">
            <label for="password-confirm">Confirmer le mot de passe * :</label>
            <input type="password"
                   id="password-confirm"
                   name="password_confirm"
                   required>
            <span class="error-message" id="password-confirm-error"></span>
        </div>

        <button type="submit">Créer mon compte</button>
    </form>

    <script>
    const form = document.getElementById('signup-form');
    const username = document.getElementById('username');
    const email = document.getElementById('email');
    const password = document.getElementById('password');
    const passwordConfirm = document.getElementById('password-confirm');

    // Validation du nom d'utilisateur
    function validateUsername() {
        const value = username.value;
        const errorMsg = document.getElementById('username-error');

        if (value.length === 0) {
            showError(username, errorMsg, 'Le nom d\'utilisateur est obligatoire');
            return false;
        } else if (value.length < 3) {
            showError(username, errorMsg, 'Minimum 3 caractères');
            return false;
        } else if (!/^[a-zA-Z0-9_-]+$/.test(value)) {
            showError(username, errorMsg, 'Uniquement lettres, chiffres, - et _');
            return false;
        } else {
            showValid(username, errorMsg);
            return true;
        }
    }

    // Validation de l'email
    function validateEmail() {
        const value = email.value;
        const errorMsg = document.getElementById('email-error');

        if (value.length === 0) {
            showError(email, errorMsg, 'L\'email est obligatoire');
            return false;
        } else if (!email.validity.valid) {
            showError(email, errorMsg, 'Format d\'email invalide');
            return false;
        } else {
            showValid(email, errorMsg);
            return true;
        }
    }

    // Validation du mot de passe
    function validatePassword() {
        const value = password.value;
        const errorMsg = document.getElementById('password-error');
        const strengthBar = document.getElementById('strength-bar');

        if (value.length === 0) {
            showError(password, errorMsg, 'Le mot de passe est obligatoire');
            strengthBar.className = 'password-strength-bar';
            return false;
        } else if (value.length < 8) {
            showError(password, errorMsg, 'Minimum 8 caractères');
            strengthBar.className = 'password-strength-bar weak';
            return false;
        }

        // Force du mot de passe
        let strength = 0;
        if (value.length >= 8) strength++;
        if (/[a-z]/.test(value)) strength++;
        if (/[A-Z]/.test(value)) strength++;
        if (/[0-9]/.test(value)) strength++;
        if (/[^a-zA-Z0-9]/.test(value)) strength++;

        if (strength < 3) {
            showError(password, errorMsg, 'Mot de passe faible : ajoutez majuscules, minuscules et chiffres');
            strengthBar.className = 'password-strength-bar weak';
            return false;
        } else if (strength === 3) {
            showValid(password, errorMsg);
            strengthBar.className = 'password-strength-bar medium';
            return true;
        } else {
            showValid(password, errorMsg);
            strengthBar.className = 'password-strength-bar strong';
            return true;
        }
    }

    // Validation de la confirmation
    function validatePasswordConfirm() {
        const errorMsg = document.getElementById('password-confirm-error');

        if (passwordConfirm.value.length === 0) {
            showError(passwordConfirm, errorMsg, 'Veuillez confirmer le mot de passe');
            return false;
        } else if (password.value !== passwordConfirm.value) {
            showError(passwordConfirm, errorMsg, 'Les mots de passe ne correspondent pas');
            return false;
        } else {
            showValid(passwordConfirm, errorMsg);
            return true;
        }
    }

    // Fonctions utilitaires
    function showError(input, errorElement, message) {
        input.classList.add('invalid');
        input.classList.remove('valid');
        errorElement.textContent = message;
        errorElement.classList.add('visible');
    }

    function showValid(input, errorElement) {
        input.classList.remove('invalid');
        input.classList.add('valid');
        errorElement.classList.remove('visible');
    }

    // Événements
    username.addEventListener('blur', validateUsername);
    username.addEventListener('input', function() {
        if (username.classList.contains('invalid')) {
            validateUsername();
        }
    });

    email.addEventListener('blur', validateEmail);
    email.addEventListener('input', function() {
        if (email.classList.contains('invalid')) {
            validateEmail();
        }
    });

    password.addEventListener('input', validatePassword);
    passwordConfirm.addEventListener('input', validatePasswordConfirm);

    // Soumission
    form.addEventListener('submit', function(e) {
        e.preventDefault();

        const isValid =
            validateUsername() &&
            validateEmail() &&
            validatePassword() &&
            validatePasswordConfirm();

        if (isValid) {
            console.log('Formulaire valide, soumission...');
            // form.submit();
            alert('Formulaire valide ! (soumission désactivée pour la démo)');
        } else {
            console.log('Formulaire invalide');
        }
    });
    </script>
</body>
</html>
```

---

## Bonnes pratiques

### ✅ À FAIRE

1. **Utiliser les types d'inputs appropriés**
```html
<!-- ✅ BON : validation automatique -->
<input type="email" name="email" required>
<input type="url" name="site" required>
<input type="number" name="age" min="18" required>
```

2. **Combiner plusieurs attributs de validation**
```html
<!-- ✅ BON : validation complète -->
<input type="text"
       name="username"
       minlength="3"
       maxlength="20"
       pattern="[a-zA-Z0-9_-]+"
       title="3 à 20 caractères : lettres, chiffres, - ou _"
       required>
```

3. **Toujours ajouter `title` avec `pattern`**
```html
<!-- ✅ BON : message explicite -->
<input type="tel"
       name="tel"
       pattern="0[0-9]{9}"
       title="Numéro français à 10 chiffres"
       required>
```

4. **Styliser les états de validation**
```css
/* ✅ BON : feedback visuel */
input:valid:not(:placeholder-shown) {
    border-color: green;
}

input:invalid:not(:focus):not(:placeholder-shown) {
    border-color: red;
}
```

5. **Valider côté serveur AUSSI**
```php
// ✅ OBLIGATOIRE : validation serveur
if (empty($_POST['email']) || !filter_var($_POST['email'], FILTER_VALIDATE_EMAIL)) {
    die('Email invalide');
}
```

### ❌ À ÉVITER

1. **Se fier uniquement à la validation client**
```html
<!-- ❌ DANGEREUX : peut être contourné -->
<input type="email" name="email" required>
<!-- TOUJOURS valider côté serveur aussi ! -->
```

2. **Oublier `title` avec `pattern`**
```html
<!-- ❌ MAUVAIS : message générique peu utile -->
<input type="text" pattern="[0-9]{5}" required>

<!-- ✅ BON : message explicite -->
<input type="text"
       pattern="[0-9]{5}"
       title="Code postal à 5 chiffres"
       required>
```

3. **Styliser `:invalid` sans conditions**
```css
/* ❌ MAUVAIS : rouge dès le chargement -->
input:invalid {
    border-color: red;
}

/* ✅ BON : rouge après interaction */
input:invalid:not(:focus):not(:placeholder-shown) {
    border-color: red;
}
```

4. **Oublier de reset `setCustomValidity()`**
```javascript
// ❌ MAUVAIS : l'erreur reste bloquée
input.setCustomValidity('Erreur');

// ✅ BON : reset à l'input
input.addEventListener('input', function() {
    input.setCustomValidity('');
});
```

5. **Messages d'erreur non accessibles**
```html
<!-- ❌ MAUVAIS : erreur pas annoncée -->
<input type="email" class="error">
<span class="error-msg">Email invalide</span>

<!-- ✅ BON : lié avec aria-describedby -->
<input type="email"
       aria-invalid="true"
       aria-describedby="email-error">
<span id="email-error" role="alert">Email invalide</span>
```

---

## Résumé des attributs de validation

| Attribut | Usage | Exemple |
|----------|-------|---------|
| `required` | Champ obligatoire | `<input required>` |
| `type` | Validation automatique | `type="email"`, `type="url"` |
| `minlength` | Longueur minimale | `minlength="8"` |
| `maxlength` | Longueur maximale | `maxlength="100"` |
| `min` | Valeur minimale | `min="18"` |
| `max` | Valeur maximale | `max="120"` |
| `step` | Incrément | `step="0.01"` |
| `pattern` | Expression régulière | `pattern="[0-9]{5}"` |
| `title` | Message d'aide | `title="Format requis"` |

---

## Points clés à retenir

1. **HTML5 offre une validation native puissante** sans JavaScript
2. **`required`** rend un champ obligatoire
3. **Types d'inputs** (email, url, number) ont une validation automatique
4. **`pattern`** permet des règles personnalisées avec regex
5. **`min`, `max`, `minlength`, `maxlength`, `step`** contrôlent les plages
6. **`title`** améliore les messages d'erreur
7. **Pseudo-classes CSS** (`:valid`, `:invalid`) pour le feedback visuel
8. **JavaScript** permet des messages personnalisés (setCustomValidity)
9. **`novalidate`** désactive la validation HTML5
10. **Validation serveur OBLIGATOIRE** : la validation client ne suffit JAMAIS !

---

## Prochaine étape

Maintenant que vous maîtrisez la validation des formulaires, nous allons voir dans le prochain chapitre comment gérer la **soumission des formulaires** avec les boutons, les différents types de boutons, et les événements liés à la soumission.

⏭️ [Boutons et gestion de soumission](/03-html5-structure-et-semantique/04-formulaires-html5/05-boutons-et-soumission.md)
