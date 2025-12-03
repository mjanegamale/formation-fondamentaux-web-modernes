🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.4.3 Labels, fieldsets et accessibilité

## Introduction

Un formulaire bien conçu ne se limite pas à avoir les bons types d'inputs. Pour qu'il soit vraiment professionnel, utilisable par tous et conforme aux standards du web, il doit être **correctement structuré et accessible**.

Dans ce chapitre, nous allons découvrir trois éléments fondamentaux :
- **`<label>`** : Pour associer des étiquettes aux champs
- **`<fieldset>`** et **`<legend>`** : Pour grouper et organiser les champs
- **Les principes d'accessibilité** : Pour que tous les utilisateurs puissent utiliser vos formulaires

Ces éléments sont souvent négligés par les débutants, mais ils sont **essentiels** pour créer des formulaires professionnels et inclusifs.

---

## Pourquoi l'accessibilité est-elle importante ?

### Qui sont les utilisateurs concernés ?

L'accessibilité ne concerne pas uniquement les personnes handicapées :

1. **Personnes malvoyantes ou non-voyantes** : Utilisent des lecteurs d'écran
2. **Personnes avec mobilité réduite** : Navigation au clavier uniquement
3. **Personnes âgées** : Peuvent avoir des difficultés motrices ou visuelles
4. **Utilisateurs temporairement handicapés** : Bras cassé, yeux fatigués
5. **Utilisateurs situationnels** : Soleil sur l'écran, mains occupées
6. **Tous les utilisateurs** : Meilleure UX pour tout le monde !

### Avantages de l'accessibilité

**Pour les utilisateurs :**
- Formulaires utilisables par tous
- Navigation facilitée
- Moins d'erreurs de saisie

**Pour vous (développeur/propriétaire) :**
- **SEO amélioré** : Google valorise l'accessibilité
- **Conformité légale** : Obligatoire dans de nombreux pays
- **Public élargi** : Plus d'utilisateurs potentiels
- **Image professionnelle** : Montre votre sérieux

---

## La balise `<label>` - L'étiquette des champs

### Qu'est-ce qu'un label ?

Un **label** (étiquette en français) est un texte qui décrit à quoi sert un champ de formulaire. C'est la question à laquelle l'utilisateur doit répondre.

```html
<label for="nom">Nom :</label>
<input type="text" id="nom" name="nom">
```

Sans label, l'utilisateur ne sait pas ce qu'il doit saisir dans le champ !

### Pourquoi utiliser `<label>` ?

#### 1. Accessibilité

Les lecteurs d'écran lisent le label pour indiquer à l'utilisateur ce qu'il doit saisir :

```html
<!-- ✅ ACCESSIBLE : Le lecteur annonce "Nom, champ texte" -->
<label for="nom">Nom :</label>
<input type="text" id="nom" name="nom">

<!-- ❌ PAS ACCESSIBLE : Le lecteur annonce juste "champ texte" -->
<input type="text" name="nom">
```

#### 2. Zone cliquable élargie

Cliquer sur le label active automatiquement le champ associé :

```html
<label for="email">Email :</label>
<input type="email" id="email" name="email">
```

**Avantage énorme** :
- Plus facile à cliquer (zone plus grande)
- Particulièrement utile pour les checkbox et radio (petits)
- Meilleur sur mobile (cibles tactiles plus grandes)

#### 3. Sémantique et structure

Le label donne un sens au formulaire, pour :
- Les moteurs de recherche (SEO)
- Les navigateurs (autocomplétion intelligente)
- La maintenance du code (plus clair)

---

## Comment associer un label à un input ?

Il existe deux méthodes principales pour associer un label à un input.

### Méthode 1 : Association explicite avec `for` et `id` (RECOMMANDÉE)

C'est la méthode **recommandée** et la plus courante :

```html
<label for="prenom">Prénom :</label>
<input type="text" id="prenom" name="prenom">
```

**Comment ça fonctionne :**
1. L'attribut `for` du label contient l'ID du champ
2. L'attribut `id` du champ correspond à cet ID
3. Le navigateur associe automatiquement les deux

**Règles importantes :**
- L'`id` doit être **unique** sur toute la page
- La valeur de `for` doit **exactement correspondre** à l'`id`
- Respectez la casse (majuscules/minuscules)

```html
<!-- ✅ BON : for correspond à id -->
<label for="email">Email :</label>
<input type="email" id="email" name="email">

<!-- ❌ MAUVAIS : for ne correspond pas à id -->
<label for="email">Email :</label>
<input type="email" id="Email" name="email">

<!-- ❌ MAUVAIS : pas d'id sur l'input -->
<label for="email">Email :</label>
<input type="email" name="email">
```

**Avantages de cette méthode :**
- ✅ Fonctionne partout (y compris si label et input ne sont pas côte à côte)
- ✅ Structure flexible
- ✅ Plus facile à styliser avec CSS
- ✅ Standard recommandé

### Méthode 2 : Label englobant (implicite)

Le label entoure directement l'input :

```html
<label>
    Prénom :
    <input type="text" name="prenom">
</label>
```

**Avantages :**
- Pas besoin d'`id` et `for`
- Plus compact

**Inconvénients :**
- Moins flexible pour le CSS
- Moins courant
- Peut créer des problèmes avec certains lecteurs d'écran

**Recommandation :** Préférez la méthode 1 (for/id) dans la plupart des cas.

---

## Placement du label

### Pour les champs texte : Label AVANT

```html
<!-- ✅ RECOMMANDÉ pour text, email, password, etc. -->
<label for="nom">Nom :</label>
<input type="text" id="nom" name="nom">
```

### Pour checkbox et radio : Label APRÈS

```html
<!-- ✅ RECOMMANDÉ pour checkbox et radio -->
<input type="checkbox" id="newsletter" name="newsletter" value="oui">
<label for="newsletter">S'abonner à la newsletter</label>

<input type="radio" id="oui" name="reponse" value="oui">
<label for="oui">Oui</label>
```

**Pourquoi après ?**
- Plus naturel visuellement
- Zone cliquable inclut le texte à côté de la case
- Convention standard du web

---

## Labels obligatoires et optionnels

### Indiquer les champs obligatoires

Il existe plusieurs façons d'indiquer qu'un champ est obligatoire :

#### Méthode 1 : Astérisque (*) - La plus courante

```html
<label for="nom">Nom * :</label>
<input type="text" id="nom" name="nom" required>

<label for="email">Email * :</label>
<input type="email" id="email" name="email" required>
```

Ajoutez une légende en haut du formulaire :

```html
<form action="/contact" method="post">
    <p><small>* Champs obligatoires</small></p>

    <label for="nom">Nom * :</label>
    <input type="text" id="nom" name="nom" required>

    <!-- autres champs -->
</form>
```

#### Méthode 2 : Mot "obligatoire"

```html
<label for="email">
    Email <span class="requis">(obligatoire)</span> :
</label>
<input type="email" id="email" name="email" required>
```

#### Méthode 3 : Balise `<abbr>` pour l'accessibilité

```html
<label for="nom">
    Nom <abbr title="obligatoire" aria-label="obligatoire">*</abbr> :
</label>
<input type="text" id="nom" name="nom" required>
```

Le lecteur d'écran lira "Nom, obligatoire".

### Indiquer les champs optionnels

Si la majorité des champs sont obligatoires, indiquez plutôt ceux qui sont optionnels :

```html
<label for="telephone">Téléphone <span class="optionnel">(optionnel)</span> :</label>
<input type="tel" id="telephone" name="telephone">
```

**Recommandation :** Choisissez une approche et restez cohérent sur tout le formulaire.

---

## Styling des labels avec CSS

### Styles de base

```css
label {
    display: block;        /* Sur sa propre ligne */
    margin-bottom: 0.5rem;
    font-weight: 600;      /* En gras */
    color: #333;
}

/* Champs obligatoires */
.requis,
label abbr {
    color: #e74c3c;        /* Rouge */
    font-weight: bold;
}

/* Champs optionnels */
.optionnel {
    font-weight: normal;
    color: #7f8c8d;        /* Gris */
    font-size: 0.9em;
}
```

### Labels en ligne (côte à côte avec l'input)

```css
.form-group {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
}

.form-group label {
    width: 150px;
    margin-right: 1rem;
    margin-bottom: 0;
}

.form-group input {
    flex: 1;
}
```

```html
<div class="form-group">
    <label for="nom">Nom :</label>
    <input type="text" id="nom" name="nom">
</div>
```

---

## La balise `<fieldset>` - Grouper les champs

### Qu'est-ce qu'un fieldset ?

`<fieldset>` permet de **grouper** des champs liés entre eux et de leur donner un titre avec `<legend>`.

```html
<fieldset>
    <legend>Coordonnées</legend>

    <label for="nom">Nom :</label>
    <input type="text" id="nom" name="nom">

    <label for="prenom">Prénom :</label>
    <input type="text" id="prenom" name="prenom">
</fieldset>
```

### Pourquoi utiliser fieldset ?

#### 1. Organisation visuelle

Les fieldsets créent des sections claires dans votre formulaire.

#### 2. Accessibilité

Les lecteurs d'écran annoncent la légende quand l'utilisateur entre dans le groupe :

```html
<fieldset>
    <legend>Informations personnelles</legend>
    <!-- champs -->
</fieldset>
```

**Le lecteur d'écran annonce :** "Groupe, Informations personnelles"

#### 3. Sémantique

Indique clairement la structure du formulaire au navigateur et aux moteurs de recherche.

---

## La balise `<legend>` - Titre du groupe

`<legend>` est le titre d'un `<fieldset>`. Elle doit être le **premier élément** à l'intérieur du fieldset.

```html
<fieldset>
    <legend>Civilité</legend>

    <input type="radio" id="mr" name="civilite" value="monsieur">
    <label for="mr">Monsieur</label>

    <input type="radio" id="mme" name="civilite" value="madame">
    <label for="mme">Madame</label>
</fieldset>
```

**Règles :**
- Une seule `<legend>` par `<fieldset>`
- Toujours en premier dans le fieldset
- Texte court et descriptif

---

## Quand utiliser fieldset et legend ?

### Cas d'usage obligatoires

#### 1. Groupes de radio buttons

**Toujours** utiliser fieldset pour des radio buttons :

```html
<fieldset>
    <legend>Moyen de paiement * :</legend>

    <input type="radio" id="carte" name="paiement" value="carte" required>
    <label for="carte">Carte bancaire</label>

    <input type="radio" id="paypal" name="paiement" value="paypal" required>
    <label for="paypal">PayPal</label>

    <input type="radio" id="virement" name="paiement" value="virement" required>
    <label for="virement">Virement</label>
</fieldset>
```

**Pourquoi ?** Les lecteurs d'écran ont besoin du contexte (legend) pour comprendre à quoi correspondent les choix.

#### 2. Groupes de checkboxes liés

```html
<fieldset>
    <legend>Vos centres d'intérêt :</legend>

    <input type="checkbox" id="sport" name="interets[]" value="sport">
    <label for="sport">Sport</label>

    <input type="checkbox" id="musique" name="interets[]" value="musique">
    <label for="musique">Musique</label>

    <input type="checkbox" id="lecture" name="interets[]" value="lecture">
    <label for="lecture">Lecture</label>
</fieldset>
```

### Cas d'usage recommandés

#### 3. Sections de formulaire

Organiser les grandes sections d'un formulaire complexe :

```html
<form action="/inscription" method="post">
    <fieldset>
        <legend>Informations personnelles</legend>
        <!-- nom, prénom, date de naissance -->
    </fieldset>

    <fieldset>
        <legend>Coordonnées</legend>
        <!-- email, téléphone, adresse -->
    </fieldset>

    <fieldset>
        <legend>Identifiants de connexion</legend>
        <!-- nom d'utilisateur, mot de passe -->
    </fieldset>
</form>
```

#### 4. Adresses multiples

```html
<fieldset>
    <legend>Adresse de facturation</legend>
    <!-- champs adresse -->
</fieldset>

<fieldset>
    <legend>Adresse de livraison</legend>
    <!-- champs adresse -->
</fieldset>
```

### Quand NE PAS utiliser fieldset ?

**N'utilisez pas fieldset pour :**
- Un seul champ isolé
- Des champs sans relation logique
- Juste pour le style (utilisez `<div>` à la place)

```html
<!-- ❌ INUTILE : un seul champ -->
<fieldset>
    <legend>Nom</legend>
    <input type="text" name="nom">
</fieldset>

<!-- ✅ MIEUX : pas de fieldset -->
<label for="nom">Nom :</label>
<input type="text" id="nom" name="nom">
```

---

## Styling de fieldset et legend

### Styles par défaut (souvent moches)

Par défaut, les navigateurs appliquent une bordure et un style particulier :

```css
/* Reset des styles par défaut */
fieldset {
    border: none;
    padding: 0;
    margin: 0;
}

legend {
    padding: 0;
}
```

### Styles modernes

```css
fieldset {
    border: 2px solid #ddd;
    border-radius: 8px;
    padding: 1.5rem;
    margin-bottom: 2rem;
    background-color: #f9f9f9;
}

legend {
    padding: 0 0.5rem;
    font-weight: bold;
    font-size: 1.1em;
    color: #2c3e50;
}
```

### Style minimaliste

```css
fieldset {
    border: none;
    border-left: 4px solid #3498db;
    padding: 1rem 0 1rem 1.5rem;
    margin-bottom: 2rem;
    background-color: #f8f9fa;
}

legend {
    font-weight: 600;
    color: #3498db;
    font-size: 1.2em;
    margin-bottom: 1rem;
}
```

---

## Accessibilité : Navigation au clavier

### Ordre de tabulation

L'ordre de navigation au clavier (`Tab`) doit être **logique et naturel** :

```html
<!-- ✅ BON : ordre logique -->
<form>
    <label for="nom">Nom :</label>
    <input type="text" id="nom" name="nom" tabindex="1">

    <label for="prenom">Prénom :</label>
    <input type="text" id="prenom" name="prenom" tabindex="2">

    <label for="email">Email :</label>
    <input type="email" id="email" name="email" tabindex="3">

    <button type="submit" tabindex="4">Envoyer</button>
</form>
```

**Note :** Dans la plupart des cas, ne spécifiez pas `tabindex`. L'ordre naturel du HTML est suffisant.

### Attribut `tabindex`

```html
<!-- tabindex="0" : ordre normal, focus possible -->
<div tabindex="0">Div focusable</div>

<!-- tabindex="-1" : pas dans l'ordre Tab, mais focusable en JS -->
<div tabindex="-1">Skip dans navigation</div>

<!-- tabindex="1+" : ordre personnalisé (éviter) -->
<input type="text" tabindex="5">
```

**⚠️ Attention :** Évitez d'utiliser des valeurs positives de `tabindex`, ça perturbe l'ordre naturel.

### Focus visible

Assurez-vous que le focus est visible :

```css
/* Ne jamais faire ça ! */
*:focus {
    outline: none; /* ❌ MAUVAIS */
}

/* À la place, personnalisez */
input:focus,
textarea:focus,
select:focus {
    outline: 2px solid #3498db;
    outline-offset: 2px;
}
```

---

## Attributs ARIA pour l'accessibilité

ARIA (Accessible Rich Internet Applications) améliore l'accessibilité des formulaires.

### `aria-label` - Label invisible

Fournit un label sans affichage visuel :

```html
<button type="submit" aria-label="Envoyer le formulaire">
    <span class="icon">📧</span>
</button>
```

Le lecteur d'écran lira "Envoyer le formulaire" au lieu de juste l'icône.

### `aria-labelledby` - Label existant

Référence un élément existant comme label :

```html
<h2 id="form-title">Inscription à la newsletter</h2>
<form aria-labelledby="form-title">
    <!-- champs -->
</form>
```

### `aria-describedby` - Description supplémentaire

Fournit une aide contextuelle :

```html
<label for="password">Mot de passe :</label>
<input type="password"
       id="password"
       name="password"
       aria-describedby="password-help"
       required>
<small id="password-help">
    Minimum 8 caractères, au moins une majuscule et un chiffre
</small>
```

Le lecteur d'écran lira le label puis la description.

### `aria-required` - Champ obligatoire

Indique qu'un champ est obligatoire (en plus de `required`) :

```html
<label for="email">Email * :</label>
<input type="email"
       id="email"
       name="email"
       required
       aria-required="true">
```

### `aria-invalid` - Champ invalide

Indique qu'un champ contient une erreur :

```html
<label for="email">Email * :</label>
<input type="email"
       id="email"
       name="email"
       aria-invalid="true"
       aria-describedby="email-error">
<span id="email-error" role="alert">
    Veuillez entrer une adresse email valide
</span>
```

---

## Messages d'erreur accessibles

### Structure recommandée

```html
<div class="form-group">
    <label for="email">Email * :</label>
    <input type="email"
           id="email"
           name="email"
           class="error"
           aria-invalid="true"
           aria-describedby="email-error"
           required>
    <span id="email-error" class="error-message" role="alert">
        ⚠️ Veuillez entrer une adresse email valide
    </span>
</div>
```

**CSS associé :**

```css
.form-group {
    margin-bottom: 1.5rem;
}

input.error {
    border-color: #e74c3c;
    background-color: #fee;
}

.error-message {
    display: block;
    color: #e74c3c;
    font-size: 0.9em;
    margin-top: 0.25rem;
}

.error-message[role="alert"] {
    /* Les lecteurs d'écran annonceront ce message */
}
```

### Résumé des erreurs en haut

Pour les formulaires longs, ajoutez un résumé des erreurs en haut :

```html
<div class="error-summary" role="alert" aria-labelledby="error-heading">
    <h2 id="error-heading">Erreurs dans le formulaire</h2>
    <p>Veuillez corriger les erreurs suivantes :</p>
    <ul>
        <li><a href="#email">Email : Format invalide</a></li>
        <li><a href="#password">Mot de passe : Trop court (minimum 8 caractères)</a></li>
        <li><a href="#conditions">Vous devez accepter les conditions d'utilisation</a></li>
    </ul>
</div>
```

Les liens permettent de sauter directement au champ en erreur.

---

## Exemples complets et accessibles

### Exemple 1 : Formulaire de contact accessible

```html
<form action="/contact" method="post">
    <h2>Formulaire de contact</h2>
    <p><small>* Champs obligatoires</small></p>

    <!-- Informations personnelles -->
    <fieldset>
        <legend>Vos coordonnées</legend>

        <div class="form-group">
            <label for="nom">
                Nom <abbr title="obligatoire" aria-label="obligatoire">*</abbr> :
            </label>
            <input type="text"
                   id="nom"
                   name="nom"
                   autocomplete="family-name"
                   required
                   aria-required="true">
        </div>

        <div class="form-group">
            <label for="prenom">
                Prénom <abbr title="obligatoire" aria-label="obligatoire">*</abbr> :
            </label>
            <input type="text"
                   id="prenom"
                   name="prenom"
                   autocomplete="given-name"
                   required
                   aria-required="true">
        </div>

        <div class="form-group">
            <label for="email">
                Email <abbr title="obligatoire" aria-label="obligatoire">*</abbr> :
            </label>
            <input type="email"
                   id="email"
                   name="email"
                   autocomplete="email"
                   required
                   aria-required="true">
        </div>

        <div class="form-group">
            <label for="telephone">
                Téléphone <span class="optionnel">(optionnel)</span> :
            </label>
            <input type="tel"
                   id="telephone"
                   name="telephone"
                   autocomplete="tel">
        </div>
    </fieldset>

    <!-- Sujet du message -->
    <fieldset>
        <legend>
            Objet de votre message <abbr title="obligatoire" aria-label="obligatoire">*</abbr>
        </legend>

        <input type="radio"
               id="info"
               name="sujet"
               value="information"
               required>
        <label for="info">Demande d'information</label>

        <input type="radio"
               id="support"
               name="sujet"
               value="support"
               required>
        <label for="support">Support technique</label>

        <input type="radio"
               id="autre"
               name="sujet"
               value="autre"
               required>
        <label for="autre">Autre</label>
    </fieldset>

    <!-- Message -->
    <div class="form-group">
        <label for="message">
            Votre message <abbr title="obligatoire" aria-label="obligatoire">*</abbr> :
        </label>
        <textarea id="message"
                  name="message"
                  rows="6"
                  required
                  aria-required="true"
                  aria-describedby="message-help"></textarea>
        <small id="message-help">Minimum 10 caractères</small>
    </div>

    <!-- Options -->
    <div class="form-group">
        <input type="checkbox"
               id="copie"
               name="copie"
               value="oui">
        <label for="copie">Recevoir une copie par email</label>
    </div>

    <div class="form-group">
        <input type="checkbox"
               id="rgpd"
               name="rgpd"
               value="accepte"
               required
               aria-required="true">
        <label for="rgpd">
            J'accepte que mes données soient utilisées pour traiter ma demande
            <abbr title="obligatoire" aria-label="obligatoire">*</abbr>
        </label>
    </div>

    <!-- Boutons -->
    <div class="form-actions">
        <button type="submit">Envoyer le message</button>
        <button type="reset">Réinitialiser</button>
    </div>
</form>
```

### Exemple 2 : Formulaire d'inscription accessible

```html
<form action="/inscription" method="post" novalidate>
    <h1 id="form-title">Créer un compte</h1>
    <p><small>Tous les champs sont obligatoires</small></p>

    <!-- Identifiants -->
    <fieldset>
        <legend>Identifiants de connexion</legend>

        <div class="form-group">
            <label for="username">Nom d'utilisateur :</label>
            <input type="text"
                   id="username"
                   name="username"
                   autocomplete="username"
                   pattern="[a-zA-Z0-9_-]{3,20}"
                   required
                   aria-required="true"
                   aria-describedby="username-help">
            <small id="username-help">
                3 à 20 caractères, lettres, chiffres, - ou _
            </small>
        </div>

        <div class="form-group">
            <label for="email">Email :</label>
            <input type="email"
                   id="email"
                   name="email"
                   autocomplete="email"
                   required
                   aria-required="true">
        </div>

        <div class="form-group">
            <label for="password">Mot de passe :</label>
            <input type="password"
                   id="password"
                   name="password"
                   autocomplete="new-password"
                   minlength="8"
                   required
                   aria-required="true"
                   aria-describedby="password-help">
            <small id="password-help">
                Minimum 8 caractères, incluant majuscule, minuscule et chiffre
            </small>
        </div>

        <div class="form-group">
            <label for="password-confirm">Confirmer le mot de passe :</label>
            <input type="password"
                   id="password-confirm"
                   name="password_confirm"
                   autocomplete="new-password"
                   minlength="8"
                   required
                   aria-required="true">
        </div>
    </fieldset>

    <!-- Informations personnelles -->
    <fieldset>
        <legend>Informations personnelles</legend>

        <div class="form-group">
            <label for="prenom">Prénom :</label>
            <input type="text"
                   id="prenom"
                   name="prenom"
                   autocomplete="given-name"
                   required
                   aria-required="true">
        </div>

        <div class="form-group">
            <label for="nom">Nom :</label>
            <input type="text"
                   id="nom"
                   name="nom"
                   autocomplete="family-name"
                   required
                   aria-required="true">
        </div>

        <div class="form-group">
            <label for="naissance">Date de naissance :</label>
            <input type="date"
                   id="naissance"
                   name="date_naissance"
                   max="2006-12-31"
                   autocomplete="bday"
                   required
                   aria-required="true"
                   aria-describedby="naissance-help">
            <small id="naissance-help">
                Vous devez avoir au moins 18 ans
            </small>
        </div>
    </fieldset>

    <!-- Genre -->
    <fieldset>
        <legend>Genre :</legend>

        <input type="radio"
               id="homme"
               name="genre"
               value="homme">
        <label for="homme">Homme</label>

        <input type="radio"
               id="femme"
               name="genre"
               value="femme">
        <label for="femme">Femme</label>

        <input type="radio"
               id="autre"
               name="genre"
               value="autre">
        <label for="autre">Autre</label>

        <input type="radio"
               id="non-precise"
               name="genre"
               value="non-precise"
               checked>
        <label for="non-precise">Ne souhaite pas préciser</label>
    </fieldset>

    <!-- Préférences -->
    <fieldset>
        <legend>Préférences (optionnelles)</legend>

        <input type="checkbox"
               id="newsletter"
               name="newsletter"
               value="oui">
        <label for="newsletter">Recevoir la newsletter hebdomadaire</label>

        <input type="checkbox"
               id="notifications"
               name="notifications"
               value="oui">
        <label for="notifications">Recevoir des notifications par email</label>
    </fieldset>

    <!-- Conditions -->
    <div class="form-group">
        <input type="checkbox"
               id="cgu"
               name="cgu"
               value="accepte"
               required
               aria-required="true">
        <label for="cgu">
            J'accepte les
            <a href="/cgu" target="_blank">conditions générales d'utilisation</a>
        </label>
    </div>

    <!-- Bouton -->
    <button type="submit">Créer mon compte</button>
</form>
```

---

## Checklist d'accessibilité des formulaires

### ✅ Labels

- [ ] Chaque champ a un `<label>` associé
- [ ] Association correcte avec `for` et `id`
- [ ] Labels visibles (pas que des placeholders)
- [ ] Champs obligatoires clairement indiqués

### ✅ Fieldsets

- [ ] Radio buttons groupés dans `<fieldset>` avec `<legend>`
- [ ] Checkboxes liés groupés dans `<fieldset>`
- [ ] Sections complexes organisées avec `<fieldset>`

### ✅ Navigation clavier

- [ ] Tous les champs accessibles au clavier (`Tab`)
- [ ] Ordre de tabulation logique
- [ ] Focus visible sur tous les éléments interactifs
- [ ] Pas de `outline: none` sans alternative

### ✅ ARIA

- [ ] `aria-required` sur les champs obligatoires
- [ ] `aria-invalid` sur les champs en erreur
- [ ] `aria-describedby` pour les aides et erreurs
- [ ] `role="alert"` sur les messages d'erreur

### ✅ Messages

- [ ] Messages d'erreur clairs et spécifiques
- [ ] Erreurs annoncées aux lecteurs d'écran
- [ ] Résumé des erreurs en haut pour les longs formulaires
- [ ] Messages de succès accessibles

### ✅ Contraste et visibilité

- [ ] Contraste suffisant (4.5:1 minimum)
- [ ] Taille de texte lisible (16px minimum)
- [ ] États visuels clairs (focus, hover, error)
- [ ] Pas uniquement de la couleur pour signaler une erreur

### ✅ Autocomplete

- [ ] Attribut `autocomplete` approprié sur chaque champ
- [ ] Aide à la saisie pour les utilisateurs

---

## Bonnes pratiques récapitulatives

### ✅ À FAIRE

1. **Toujours utiliser `<label>`**
```html
<!-- ✅ BON -->
<label for="email">Email :</label>
<input type="email" id="email" name="email">
```

2. **Grouper les radio/checkbox avec fieldset**
```html
<!-- ✅ BON -->
<fieldset>
    <legend>Civilité :</legend>
    <input type="radio" id="mr" name="civilite" value="mr">
    <label for="mr">M.</label>
    <!-- autres options -->
</fieldset>
```

3. **Indiquer clairement les champs obligatoires**
```html
<!-- ✅ BON -->
<label for="nom">Nom * :</label>
<input type="text" id="nom" name="nom" required aria-required="true">
```

4. **Associer les messages d'aide**
```html
<!-- ✅ BON -->
<label for="password">Mot de passe :</label>
<input type="password" id="password" name="password" aria-describedby="pwd-help">
<small id="pwd-help">Minimum 8 caractères</small>
```

5. **Rendre le focus visible**
```css
/* ✅ BON */
input:focus {
    outline: 2px solid #3498db;
    outline-offset: 2px;
}
```

### ❌ À ÉVITER

1. **Pas de label**
```html
<!-- ❌ MAUVAIS -->
<input type="text" placeholder="Nom">
```

2. **Placeholder comme label**
```html
<!-- ❌ MAUVAIS : disparaît à la saisie -->
<input type="email" placeholder="Email">

<!-- ✅ BON -->
<label for="email">Email :</label>
<input type="email" id="email" name="email" placeholder="exemple@mail.com">
```

3. **Supprimer le focus outline**
```css
/* ❌ DANGEREUX */
*:focus {
    outline: none;
}
```

4. **Radio/checkbox sans contexte**
```html
<!-- ❌ MAUVAIS : pas de fieldset -->
<input type="radio" id="oui" name="reponse" value="oui">
<label for="oui">Oui</label>

<!-- ✅ BON -->
<fieldset>
    <legend>Acceptez-vous ?</legend>
    <input type="radio" id="oui" name="reponse" value="oui">
    <label for="oui">Oui</label>
</fieldset>
```

5. **Erreur uniquement visuelle (couleur)**
```html
<!-- ❌ MAUVAIS : juste une bordure rouge -->
<input type="email" style="border-color: red;">

<!-- ✅ BON : indication accessible -->
<input type="email"
       aria-invalid="true"
       aria-describedby="email-error">
<span id="email-error" role="alert">Format email invalide</span>
```

---

## Outils de test d'accessibilité

### Extensions navigateur

- **WAVE** : Évalue l'accessibilité de votre page
- **axe DevTools** : Audit d'accessibilité intégré
- **Lighthouse** : Inclus dans Chrome DevTools

### Lecteurs d'écran

- **NVDA** (Windows) : Gratuit
- **JAWS** (Windows) : Payant
- **VoiceOver** (Mac/iOS) : Intégré
- **TalkBack** (Android) : Intégré

### Tests manuels

1. **Navigation au clavier** : Parcourez tout le formulaire avec `Tab`
2. **Zoom à 200%** : Vérifiez que tout reste lisible
3. **Désactiver CSS** : Le formulaire reste-t-il compréhensible ?
4. **Lecteur d'écran** : Testez avec un vrai lecteur

---

## Points clés à retenir

1. **`<label>` est obligatoire** pour chaque champ de formulaire
2. **Association for/id** : La méthode recommandée
3. **`<fieldset>` + `<legend>`** : Obligatoire pour radio/checkbox groupés
4. **Indiquez les champs obligatoires** clairement (*)
5. **ARIA améliore l'accessibilité** : aria-required, aria-invalid, aria-describedby
6. **Focus visible** : Ne jamais supprimer sans alternative
7. **Navigation clavier** : Testez avec la touche Tab
8. **Messages d'erreur accessibles** : role="alert", aria-describedby
9. **L'accessibilité profite à tous**, pas seulement aux personnes handicapées
10. **Testez avec de vrais outils** : lecteurs d'écran, navigation clavier

---

## Prochaine étape

Maintenant que vous savez structurer correctement vos formulaires pour l'accessibilité, nous allons découvrir dans le prochain chapitre la **validation native HTML5**, qui permet de vérifier les données avant l'envoi au serveur, sans écrire une ligne de JavaScript !

⏭️ [Validation native HTML5](/03-html5-structure-et-semantique/04-formulaires-html5/04-validation-native-html5.md)
