🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.4.1 Structure de formulaire et méthodes (GET/POST)

## Introduction

Les formulaires HTML sont l'un des éléments les plus importants du web interactif. Ils permettent aux utilisateurs de communiquer avec votre site : s'inscrire, se connecter, effectuer une recherche, laisser un commentaire, passer une commande, et bien plus encore.

Sans formulaires, le web ne serait qu'une collection de pages statiques. Avec eux, vous créez une véritable interaction avec vos visiteurs.

Dans ce chapitre, nous allons découvrir la structure fondamentale des formulaires HTML5 et comprendre comment les données sont envoyées au serveur avec les méthodes GET et POST.

---

## La balise `<form>`

### Structure de base

Un formulaire HTML est créé avec la balise `<form>` qui enveloppe tous les éléments du formulaire :

```html
<form>
    <!-- Tous les champs du formulaire vont ici -->
</form>
```

La balise `<form>` est un **conteneur** qui définit :
- Où les données seront envoyées (attribut `action`)
- Comment elles seront envoyées (attribut `method`)
- Le type de données (attribut `enctype`, pour les fichiers)

### Exemple simple et complet

```html
<form action="/traitement" method="post">
    <label for="nom">Nom :</label>
    <input type="text" id="nom" name="nom">

    <button type="submit">Envoyer</button>
</form>
```

**Décortiquons cet exemple :**
- `<form>` : Conteneur du formulaire
- `action="/traitement"` : Où envoyer les données
- `method="post"` : Comment envoyer les données
- `<label>` : Étiquette du champ
- `<input>` : Champ de saisie
- `<button>` : Bouton d'envoi

---

## Les attributs essentiels de `<form>`

### 1. `action` - Où envoyer les données

L'attribut `action` spécifie l'URL vers laquelle les données du formulaire seront envoyées :

```html
<!-- Envoyer vers une page sur votre site -->
<form action="/contact.php" method="post">
    <!-- champs -->
</form>

<!-- Envoyer vers une URL complète -->
<form action="https://example.com/api/contact" method="post">
    <!-- champs -->
</form>

<!-- Envoyer vers la page actuelle (par défaut) -->
<form action="" method="post">
    <!-- champs -->
</form>
```

**Notes importantes :**

- Si `action` est vide ou omis, le formulaire est soumis à la page actuelle
- L'URL peut être relative (`/contact`) ou absolue (`https://...`)
- Cette URL doit pointer vers un script serveur capable de traiter les données (PHP, Node.js, Python, etc.)

```html
<!-- ✅ BON : action vers un script de traitement -->
<form action="/traiter-inscription.php" method="post">
    <!-- champs d'inscription -->
</form>

<!-- ⚠️ Action vide : soumet à la page actuelle -->
<form action="" method="post">
    <!-- champs -->
</form>

<!-- ❌ ATTENTION : action vers une page HTML simple (ne traitera rien) -->
<form action="merci.html" method="post">
    <!-- Les données seront perdues ! -->
</form>
```

### 2. `method` - Comment envoyer les données

L'attribut `method` définit la méthode HTTP utilisée pour envoyer les données. Il y a deux méthodes principales :

#### **GET** (par défaut)
#### **POST**

Nous allons les détailler dans la section suivante.

### 3. `enctype` - Type d'encodage

L'attribut `enctype` spécifie comment les données du formulaire doivent être encodées lors de l'envoi. **Obligatoire pour l'upload de fichiers.**

```html
<!-- Par défaut : pour les formulaires classiques -->
<form action="/traitement" method="post" enctype="application/x-www-form-urlencoded">
    <!-- champs texte, email, etc. -->
</form>

<!-- Pour l'upload de fichiers : OBLIGATOIRE -->
<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="fichier">
    <button type="submit">Envoyer</button>
</form>

<!-- Pour du texte brut (rare) -->
<form action="/traitement" method="post" enctype="text/plain">
    <!-- champs -->
</form>
```

**Valeurs possibles :**

| Valeur | Usage | Quand l'utiliser |
|--------|-------|------------------|
| `application/x-www-form-urlencoded` | Par défaut | Formulaires classiques |
| `multipart/form-data` | Upload de fichiers | **Obligatoire** pour `<input type="file">` |
| `text/plain` | Texte brut | Rarement utilisé |

**Règle simple** : Dès que vous avez un `<input type="file">`, utilisez `enctype="multipart/form-data"` !

### 4. `name` - Identifier le formulaire

L'attribut `name` donne un nom au formulaire (utile en JavaScript) :

```html
<form name="formulaire-contact" action="/contact" method="post">
    <!-- champs -->
</form>
```

Vous pourrez ensuite y accéder en JavaScript :
```javascript
// Accéder au formulaire
document.forms['formulaire-contact'];
// ou
document.forms.formulaireContact;
```

### 5. `id` - Identifier uniquement

Comme pour tous les éléments HTML, `id` permet d'identifier le formulaire :

```html
<form id="contact-form" action="/contact" method="post">
    <!-- champs -->
</form>
```

### 6. `target` - Où afficher la réponse

L'attribut `target` définit où afficher la réponse après soumission :

```html
<!-- Ouvrir dans la même fenêtre (par défaut) -->
<form action="/contact" method="post" target="_self">
    <!-- champs -->
</form>

<!-- Ouvrir dans un nouvel onglet -->
<form action="/recherche" method="get" target="_blank">
    <!-- champs -->
</form>

<!-- Ouvrir dans un iframe -->
<form action="/newsletter" method="post" target="iframe-resultat">
    <!-- champs -->
</form>
<iframe name="iframe-resultat"></iframe>
```

**Valeurs courantes :**
- `_self` : Page actuelle (par défaut)
- `_blank` : Nouvel onglet
- `_parent` : Frame parent
- `_top` : Fenêtre principale
- `nom-iframe` : Iframe spécifique

⚠️ **Note** : L'ouverture dans un nouvel onglet (`_blank`) est généralement déconseillée pour les formulaires, sauf cas particuliers.

### 7. `autocomplete` - Autocomplétion

Active ou désactive l'autocomplétion du navigateur :

```html
<!-- Activer l'autocomplétion (par défaut, recommandé) -->
<form action="/login" method="post" autocomplete="on">
    <input type="email" name="email">
    <input type="password" name="password">
</form>

<!-- Désactiver l'autocomplétion (rare, pour données sensibles) -->
<form action="/secure" method="post" autocomplete="off">
    <input type="text" name="code-secret">
</form>
```

**Bonnes pratiques :**
- Laissez `autocomplete="on"` par défaut (meilleure UX)
- Désactivez uniquement pour des données très sensibles
- Vous pouvez aussi contrôler l'autocomplétion au niveau de chaque champ

### 8. `novalidate` - Désactiver la validation HTML5

Désactive la validation native du navigateur :

```html
<!-- Avec validation native (par défaut, recommandé) -->
<form action="/contact" method="post">
    <input type="email" name="email" required>
    <button type="submit">Envoyer</button>
</form>

<!-- Sans validation native (gérer en JavaScript) -->
<form action="/contact" method="post" novalidate>
    <input type="email" name="email" required>
    <button type="submit">Envoyer</button>
</form>
```

⚠️ **Attention** : Utilisez `novalidate` uniquement si vous implémentez votre propre validation en JavaScript. Sinon, gardez la validation native !

---

## Les méthodes GET et POST

C'est l'un des concepts les plus importants des formulaires. Comprendre la différence entre GET et POST est essentiel pour créer des formulaires sécurisés et fonctionnels.

### La méthode GET

#### Comment fonctionne GET ?

Avec la méthode GET, les données du formulaire sont **ajoutées à l'URL** sous forme de paramètres :

```html
<form action="/recherche" method="get">
    <input type="text" name="q" placeholder="Rechercher...">
    <button type="submit">Rechercher</button>
</form>
```

**Si l'utilisateur tape "html tutoriel" et soumet le formulaire, l'URL deviendra :**

```
https://example.com/recherche?q=html+tutoriel
```

Les données sont visibles dans la barre d'adresse après le `?`.

#### Caractéristiques de GET

**✅ Avantages :**
- **URL bookmarkable** : L'utilisateur peut enregistrer la page en favoris
- **Partage facile** : On peut copier/coller l'URL
- **Rechargement simple** : Recharger la page réexécute la recherche
- **Historique** : Les recherches restent dans l'historique du navigateur
- **Cache navigateur** : Les résultats peuvent être mis en cache

**❌ Inconvénients :**
- **Limite de taille** : ~2000 caractères maximum dans l'URL
- **Pas de sécurité** : Les données sont visibles dans l'URL
- **Pas pour données sensibles** : Mots de passe, informations bancaires visibles
- **Pas pour grandes données** : Limité par la longueur de l'URL

#### Quand utiliser GET ?

**✅ Utilisez GET pour :**
- **Recherches** (Google, recherche sur site)
- **Filtres** (trier, filtrer des résultats)
- **Pagination** (page 1, page 2, etc.)
- **Navigation** (catégories, tags)
- **Partage de résultats** (liens vers une recherche spécifique)

```html
<!-- ✅ Excellent pour une recherche -->
<form action="/recherche" method="get">
    <input type="search" name="q" placeholder="Rechercher...">
    <button type="submit">🔍 Rechercher</button>
</form>
<!-- URL résultante : /recherche?q=terme -->

<!-- ✅ Parfait pour des filtres -->
<form action="/produits" method="get">
    <select name="categorie">
        <option value="tous">Tous</option>
        <option value="electronique">Électronique</option>
        <option value="vetements">Vêtements</option>
    </select>
    <select name="tri">
        <option value="prix-asc">Prix croissant</option>
        <option value="prix-desc">Prix décroissant</option>
    </select>
    <button type="submit">Filtrer</button>
</form>
<!-- URL résultante : /produits?categorie=electronique&tri=prix-asc -->
```

#### Quand NE PAS utiliser GET ?

**❌ N'utilisez JAMAIS GET pour :**
- **Mots de passe** (visibles dans l'URL et l'historique !)
- **Informations bancaires**
- **Données personnelles sensibles**
- **Création/modification de données** (inscriptions, commandes)
- **Upload de fichiers**
- **Grandes quantités de données**

```html
<!-- ❌ DANGEREUX : mot de passe en GET -->
<form action="/login" method="get">
    <input type="text" name="username">
    <input type="password" name="password">
    <button type="submit">Connexion</button>
</form>
<!-- URL résultante : /login?username=jean&password=motdepasse123
     Le mot de passe est VISIBLE dans l'URL ! -->
```

### La méthode POST

#### Comment fonctionne POST ?

Avec la méthode POST, les données du formulaire sont **envoyées dans le corps de la requête HTTP**, pas dans l'URL :

```html
<form action="/inscription" method="post">
    <input type="text" name="nom" placeholder="Nom">
    <input type="email" name="email" placeholder="Email">
    <input type="password" name="password" placeholder="Mot de passe">
    <button type="submit">S'inscrire</button>
</form>
```

**Après soumission, l'URL reste :**
```
https://example.com/inscription
```

Les données sont invisibles dans l'URL et envoyées de manière séparée.

#### Caractéristiques de POST

**✅ Avantages :**
- **Sécurité relative** : Données non visibles dans l'URL
- **Pas de limite de taille** : Peut envoyer beaucoup de données
- **Upload de fichiers** : Possible avec POST
- **Données sensibles** : Adapté pour mots de passe, infos perso
- **Pas dans l'historique** : Les données ne restent pas dans l'historique du navigateur

**❌ Inconvénients :**
- **Pas bookmarkable** : Impossible de mettre en favoris
- **Avertissement au rechargement** : Le navigateur demande confirmation
- **Pas de partage** : On ne peut pas copier/coller l'URL avec les données
- **Pas de cache** : Les résultats ne sont pas mis en cache

#### Quand utiliser POST ?

**✅ Utilisez POST pour :**
- **Connexion** (login avec mot de passe)
- **Inscription** (création de compte)
- **Contact** (envoi de message)
- **Commande** (achat en ligne)
- **Upload de fichiers**
- **Création/modification de données** sur le serveur
- **Formulaires avec données sensibles**

```html
<!-- ✅ Parfait pour connexion -->
<form action="/login" method="post">
    <label for="email">Email :</label>
    <input type="email" id="email" name="email" required>

    <label for="password">Mot de passe :</label>
    <input type="password" id="password" name="password" required>

    <button type="submit">Se connecter</button>
</form>

<!-- ✅ Excellent pour inscription -->
<form action="/inscription" method="post">
    <input type="text" name="prenom" placeholder="Prénom" required>
    <input type="text" name="nom" placeholder="Nom" required>
    <input type="email" name="email" placeholder="Email" required>
    <input type="password" name="password" placeholder="Mot de passe" required>
    <input type="tel" name="telephone" placeholder="Téléphone">

    <button type="submit">Créer mon compte</button>
</form>

<!-- ✅ Indispensable pour upload -->
<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="photo" accept="image/*" required>
    <input type="text" name="description" placeholder="Description">
    <button type="submit">Envoyer la photo</button>
</form>
```

---

## Tableau comparatif GET vs POST

| Critère | GET | POST |
|---------|-----|------|
| **Visibilité** | Données dans l'URL | Données cachées |
| **Sécurité** | ❌ Faible (visible) | ✅ Meilleure |
| **Taille des données** | ❌ Limitée (~2000 char) | ✅ Illimitée |
| **Bookmarkable** | ✅ Oui | ❌ Non |
| **Cache navigateur** | ✅ Oui | ❌ Non |
| **Historique** | ✅ Reste dans l'historique | ❌ Non |
| **Upload fichiers** | ❌ Impossible | ✅ Possible |
| **Rechargement** | ✅ Simple | ⚠️ Confirmation |
| **Mots de passe** | ❌ JAMAIS | ✅ Oui |
| **Usage typique** | Recherche, filtres | Inscription, connexion |

---

## Comment les données sont-elles formatées ?

### Avec GET

Les données sont encodées dans l'URL sous forme de paires `nom=valeur` séparées par `&` :

```html
<form action="/recherche" method="get">
    <input type="text" name="q" value="html">
    <input type="text" name="page" value="1">
</form>
```

**URL résultante :**
```
/recherche?q=html&page=1
```

**Format :** `?nom1=valeur1&nom2=valeur2&nom3=valeur3`

**Encodage des caractères spéciaux :**
- Espaces → `+` ou `%20`
- Caractères spéciaux → Codes hexadécimaux

Exemple : "développement web" → `d%C3%A9veloppement+web`

### Avec POST

Les données sont envoyées dans le corps de la requête HTTP (invisible pour l'utilisateur) :

```
POST /inscription HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

nom=Dupont&prenom=Jean&email=jean@example.com
```

L'utilisateur ne voit que l'URL de base : `/inscription`

---

## L'attribut `name` : Crucial pour l'envoi des données

**⚠️ TRÈS IMPORTANT** : Chaque champ de formulaire doit avoir un attribut `name` pour que ses données soient envoyées !

```html
<!-- ✅ BON : name présent, données envoyées -->
<input type="text" name="nom" value="Dupont">
<!-- Enverra : nom=Dupont -->

<!-- ❌ MAUVAIS : pas de name, données PERDUES -->
<input type="text" value="Dupont">
<!-- N'enverra RIEN ! -->
```

**Exemple complet :**

```html
<form action="/contact" method="post">
    <!-- ✅ Sera envoyé -->
    <input type="text" name="nom" placeholder="Votre nom">

    <!-- ✅ Sera envoyé -->
    <input type="email" name="email" placeholder="Votre email">

    <!-- ❌ NE sera PAS envoyé (pas de name) -->
    <input type="text" placeholder="Ce champ n'a pas de name">

    <!-- ✅ Sera envoyé -->
    <textarea name="message"></textarea>

    <button type="submit">Envoyer</button>
</form>
```

**Données envoyées :** `nom=...&email=...&message=...`

Le troisième champ sera **ignoré** car il n'a pas d'attribut `name` !

---

## Structure HTML complète d'un formulaire

Voici la structure recommandée d'un formulaire professionnel :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulaire de contact</title>
</head>
<body>
    <h1>Contactez-nous</h1>

    <form action="/traiter-contact.php" method="post">
        <!-- Champ nom -->
        <div>
            <label for="nom">Nom complet :</label>
            <input type="text"
                   id="nom"
                   name="nom"
                   placeholder="Jean Dupont"
                   required>
        </div>

        <!-- Champ email -->
        <div>
            <label for="email">Email :</label>
            <input type="email"
                   id="email"
                   name="email"
                   placeholder="jean@example.com"
                   required>
        </div>

        <!-- Champ sujet -->
        <div>
            <label for="sujet">Sujet :</label>
            <select id="sujet" name="sujet" required>
                <option value="">-- Choisir --</option>
                <option value="question">Question</option>
                <option value="support">Support technique</option>
                <option value="autre">Autre</option>
            </select>
        </div>

        <!-- Champ message -->
        <div>
            <label for="message">Message :</label>
            <textarea id="message"
                      name="message"
                      rows="5"
                      placeholder="Votre message..."
                      required></textarea>
        </div>

        <!-- Bouton d'envoi -->
        <div>
            <button type="submit">Envoyer le message</button>
        </div>
    </form>
</body>
</html>
```

**Points clés :**
1. Balise `<form>` avec `action` et `method`
2. Chaque champ a un `<label>` associé via `for="id"`
3. Chaque champ a un `id` (pour le label) et un `name` (pour l'envoi)
4. Bouton `<button type="submit">` pour soumettre
5. Utilisation de `required` pour validation de base

---

## Types de boutons dans un formulaire

### 1. `type="submit"` - Envoyer le formulaire

C'est le bouton principal qui soumet le formulaire :

```html
<button type="submit">Envoyer</button>
<!-- ou -->
<input type="submit" value="Envoyer">
```

**Comportement :** Valide et envoie le formulaire vers l'URL `action`.

### 2. `type="reset"` - Réinitialiser

Efface tous les champs du formulaire :

```html
<button type="reset">Réinitialiser</button>
<!-- ou -->
<input type="reset" value="Réinitialiser">
```

⚠️ **Attention :** Rarement utilisé car frustrant pour l'utilisateur (risque de clic accidentel).

### 3. `type="button"` - Bouton neutre

Ne fait rien par défaut (utilisé avec JavaScript) :

```html
<button type="button" onclick="afficherAide()">Aide</button>
```

**Important :** Si vous omettez `type`, la valeur par défaut dans un formulaire est `submit` !

```html
<form action="/contact" method="post">
    <input type="text" name="nom">

    <!-- ⚠️ Ce bouton soumettra le formulaire (type="submit" par défaut) -->
    <button>Envoyer</button>

    <!-- ✅ Mieux : expliciter le type -->
    <button type="submit">Envoyer</button>
</form>
```

---

## Exemples pratiques complets

### Exemple 1 : Formulaire de recherche (GET)

```html
<form action="/recherche" method="get">
    <label for="search">Rechercher sur le site :</label>
    <input type="search"
           id="search"
           name="q"
           placeholder="Tapez votre recherche..."
           required>
    <button type="submit">🔍 Rechercher</button>
</form>
```

**URL après soumission (exemple) :**
```
/recherche?q=html+css+tutoriel
```

### Exemple 2 : Formulaire de connexion (POST)

```html
<form action="/login" method="post">
    <h2>Connexion</h2>

    <div>
        <label for="username">Nom d'utilisateur ou email :</label>
        <input type="text"
               id="username"
               name="username"
               autocomplete="username"
               required>
    </div>

    <div>
        <label for="password">Mot de passe :</label>
        <input type="password"
               id="password"
               name="password"
               autocomplete="current-password"
               required>
    </div>

    <div>
        <input type="checkbox" id="remember" name="remember" value="1">
        <label for="remember">Se souvenir de moi</label>
    </div>

    <button type="submit">Se connecter</button>

    <p>
        <a href="/mot-de-passe-oublie">Mot de passe oublié ?</a>
    </p>
</form>
```

### Exemple 3 : Formulaire d'inscription (POST)

```html
<form action="/inscription" method="post">
    <h2>Créer un compte</h2>

    <div>
        <label for="prenom">Prénom :</label>
        <input type="text"
               id="prenom"
               name="prenom"
               autocomplete="given-name"
               required>
    </div>

    <div>
        <label for="nom">Nom :</label>
        <input type="text"
               id="nom"
               name="nom"
               autocomplete="family-name"
               required>
    </div>

    <div>
        <label for="email">Email :</label>
        <input type="email"
               id="email"
               name="email"
               autocomplete="email"
               required>
    </div>

    <div>
        <label for="password">Mot de passe :</label>
        <input type="password"
               id="password"
               name="password"
               autocomplete="new-password"
               minlength="8"
               required>
    </div>

    <div>
        <label for="password-confirm">Confirmer le mot de passe :</label>
        <input type="password"
               id="password-confirm"
               name="password_confirm"
               autocomplete="new-password"
               minlength="8"
               required>
    </div>

    <div>
        <input type="checkbox"
               id="conditions"
               name="conditions"
               value="accepte"
               required>
        <label for="conditions">
            J'accepte les <a href="/cgu">conditions d'utilisation</a>
        </label>
    </div>

    <button type="submit">Créer mon compte</button>
</form>
```

### Exemple 4 : Upload de fichier (POST avec multipart)

```html
<form action="/upload-photo" method="post" enctype="multipart/form-data">
    <h2>Télécharger une photo</h2>

    <div>
        <label for="photo">Sélectionner une photo :</label>
        <input type="file"
               id="photo"
               name="photo"
               accept="image/*"
               required>
    </div>

    <div>
        <label for="titre">Titre de la photo :</label>
        <input type="text"
               id="titre"
               name="titre"
               placeholder="Vacances en montagne"
               required>
    </div>

    <div>
        <label for="description">Description (optionnelle) :</label>
        <textarea id="description"
                  name="description"
                  rows="4"
                  placeholder="Décrivez votre photo..."></textarea>
    </div>

    <button type="submit">Télécharger</button>
</form>
```

**⚠️ CRUCIAL :** L'attribut `enctype="multipart/form-data"` est **OBLIGATOIRE** pour l'upload de fichiers !

---

## Bonnes pratiques

### ✅ À FAIRE

1. **Toujours spécifier `method`** explicitement (`get` ou `post`)
```html
<!-- ✅ BON -->
<form action="/contact" method="post">
```

2. **Utiliser POST pour les données sensibles**
```html
<!-- ✅ BON : POST pour mot de passe -->
<form action="/login" method="post">
```

3. **Utiliser GET pour les recherches et filtres**
```html
<!-- ✅ BON : GET pour recherche -->
<form action="/recherche" method="get">
```

4. **Ajouter `enctype` pour l'upload de fichiers**
```html
<!-- ✅ BON : enctype pour fichiers -->
<form method="post" enctype="multipart/form-data">
```

5. **Donner un `name` à chaque champ**
```html
<!-- ✅ BON : chaque champ a un name -->
<input type="text" name="nom" id="nom">
```

6. **Associer labels et inputs**
```html
<!-- ✅ BON : label associé via for/id -->
<label for="email">Email :</label>
<input type="email" id="email" name="email">
```

### ❌ À ÉVITER

1. **Ne pas oublier l'attribut `name`**
```html
<!-- ❌ MAUVAIS : pas de name, donnée perdue -->
<input type="text" id="nom">
```

2. **Ne pas utiliser GET pour les mots de passe**
```html
<!-- ❌ DANGEREUX : mot de passe visible dans l'URL -->
<form action="/login" method="get">
    <input type="password" name="password">
</form>
```

3. **Ne pas oublier `enctype` pour les fichiers**
```html
<!-- ❌ MAUVAIS : upload ne fonctionnera pas -->
<form action="/upload" method="post">
    <input type="file" name="photo">
</form>

<!-- ✅ BON -->
<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="photo">
</form>
```

4. **Ne pas utiliser `target="_blank"` sans raison**
```html
<!-- ❌ MAUVAIS : frustrant pour l'utilisateur -->
<form action="/contact" method="post" target="_blank">
```

---

## Points clés à retenir

1. **`<form>` est le conteneur** de tous les éléments du formulaire
2. **`action`** définit où envoyer les données
3. **`method`** définit comment envoyer (GET ou POST)
4. **GET** : données dans l'URL, pour recherches et filtres
5. **POST** : données cachées, pour connexion, inscription, données sensibles
6. **`enctype="multipart/form-data"`** est obligatoire pour l'upload de fichiers
7. **Chaque champ doit avoir un `name`** pour être envoyé
8. **Utilisez POST par défaut**, sauf pour recherches/filtres

---

## Règle de décision simple

**Utilisez GET si :**
- ✅ C'est une recherche
- ✅ Ce sont des filtres/tri
- ✅ L'URL doit être bookmarkable
- ✅ Les données ne sont PAS sensibles

**Utilisez POST si :**
- ✅ Ce sont des données sensibles (mot de passe, infos perso)
- ✅ C'est une création/modification de données
- ✅ Il y a upload de fichiers
- ✅ Il y a beaucoup de données
- ✅ En cas de doute !

---

## Prochaine étape

Maintenant que vous maîtrisez la structure des formulaires et les méthodes GET/POST, nous allons découvrir dans le prochain chapitre les **types d'inputs modernes** introduits par HTML5 : email, tel, date, color, range, et bien d'autres qui facilitent la saisie et améliorent l'expérience utilisateur.

⏭️ [Types d'inputs modernes](/03-html5-structure-et-semantique/04-formulaires-html5/02-types-inputs-modernes.md)
