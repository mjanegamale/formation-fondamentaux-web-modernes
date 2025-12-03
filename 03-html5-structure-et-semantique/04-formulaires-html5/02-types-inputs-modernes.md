🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.4.2 Types d'inputs modernes

## Introduction

HTML5 a révolutionné les formulaires en introduisant de nombreux nouveaux types d'`<input>`. Avant HTML5, nous étions limités à quelques types basiques comme `text`, `password`, `checkbox` et `radio`. Aujourd'hui, nous disposons de types spécialisés qui :

- **Améliorent l'expérience utilisateur** (claviers adaptés sur mobile, sélecteurs natifs)
- **Facilitent la validation** (formats email, URL, nombres)
- **Réduisent le besoin de JavaScript** (validation native du navigateur)
- **Sont accessibles** (meilleure sémantique pour les technologies d'assistance)

Dans ce chapitre, nous allons explorer tous les types d'inputs disponibles en HTML5, leurs spécificités et leurs cas d'usage.

---

## Structure de base d'un input

Avant de plonger dans les différents types, rappelons la structure de base :

```html
<label for="identifiant">Étiquette :</label>
<input type="type-ici"
       id="identifiant"
       name="nom-pour-envoi"
       placeholder="Texte d'aide"
       required>
```

**Éléments essentiels :**
- `type` : Définit le type d'input
- `id` : Identifiant unique (pour le label)
- `name` : Nom pour l'envoi des données (obligatoire !)
- `placeholder` : Texte indicatif (optionnel)
- `required` : Rend le champ obligatoire (optionnel)

---

## Types d'inputs pour le texte

### 1. `type="text"` - Texte simple (par défaut)

C'est le type par défaut, pour toute saisie de texte court sur une ligne.

```html
<label for="nom">Nom :</label>
<input type="text"
       id="nom"
       name="nom"
       placeholder="Jean Dupont"
       required>
```

**Quand l'utiliser :**
- Nom, prénom
- Adresse
- Ville
- Tout texte court non spécialisé

**Attributs utiles :**
```html
<input type="text"
       name="ville"
       minlength="2"           <!-- Longueur minimale -->
       maxlength="50"          <!-- Longueur maximale -->
       pattern="[A-Za-z\s]+"   <!-- Expression régulière (que des lettres) -->
       required>
```

### 2. `type="email"` - Adresse email

**Spécialement conçu pour les adresses email.**

```html
<label for="email">Email :</label>
<input type="email"
       id="email"
       name="email"
       placeholder="jean@example.com"
       required>
```

**✅ Avantages :**
- **Validation automatique** : Le navigateur vérifie que c'est une adresse email valide
- **Clavier adapté sur mobile** : Affiche @ et .com facilement
- **Meilleur pour l'accessibilité** : Les lecteurs d'écran annoncent "champ email"

```html
<!-- Le navigateur vérifie que le format est valide -->
<input type="email" name="email" required>
<!-- Accepte : jean@example.com -->
<!-- Refuse : jean@example (pas de domaine) -->
<!-- Refuse : jean.example.com (pas de @) -->
```

**Permettre plusieurs emails :**
```html
<input type="email"
       name="emails"
       multiple
       placeholder="email1@ex.com, email2@ex.com">
```

### 3. `type="password"` - Mot de passe

**Les caractères sont masqués pour la confidentialité.**

```html
<label for="password">Mot de passe :</label>
<input type="password"
       id="password"
       name="password"
       minlength="8"
       required>
```

**Caractéristiques :**
- Les caractères sont affichés comme `••••••••`
- Empêche la copie (pour la sécurité)
- Désactive souvent l'autocomplétion

**Attributs recommandés :**
```html
<input type="password"
       name="password"
       minlength="8"              <!-- Minimum 8 caractères -->
       maxlength="128"            <!-- Maximum 128 caractères -->
       autocomplete="new-password" <!-- Pour nouveau mot de passe -->
       required>
```

**Bonnes pratiques :**
```html
<!-- Création de compte -->
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

<!-- Connexion -->
<div>
    <label for="password">Mot de passe :</label>
    <input type="password"
           id="password"
           name="password"
           autocomplete="current-password"
           required>
</div>
```

### 4. `type="tel"` - Numéro de téléphone

**Pour les numéros de téléphone.**

```html
<label for="telephone">Téléphone :</label>
<input type="tel"
       id="telephone"
       name="telephone"
       placeholder="+33 6 12 34 56 78"
       pattern="[0-9\s\+\-]+"
       required>
```

**✅ Avantages :**
- **Clavier numérique sur mobile** : Facilite la saisie
- **Pas de validation stricte par défaut** : Les formats de téléphone varient selon les pays

**Note importante :** Contrairement à `type="email"`, `type="tel"` n'a pas de validation automatique. Vous devez utiliser l'attribut `pattern` pour forcer un format :

```html
<!-- Format français : 06 12 34 56 78 ou +33 6 12 34 56 78 -->
<input type="tel"
       name="tel"
       pattern="^(\+33|0)[1-9](\s?\d{2}){4}$"
       placeholder="06 12 34 56 78">

<!-- Format international simple -->
<input type="tel"
       name="tel"
       pattern="[\+]?[0-9\s\-]{8,20}"
       placeholder="+33 6 12 34 56 78">
```

### 5. `type="url"` - Adresse web

**Pour les URLs (adresses de sites web).**

```html
<label for="site">Site web :</label>
<input type="url"
       id="site"
       name="site"
       placeholder="https://example.com"
       required>
```

**✅ Avantages :**
- **Validation automatique** : Vérifie que c'est une URL valide
- **Clavier adapté sur mobile** : Affiche .com, .fr, etc.

```html
<!-- Accepte : https://example.com -->
<!-- Accepte : http://example.com -->
<!-- Refuse : example.com (pas de protocole) -->
<!-- Refuse : ht://example (protocole invalide) -->
<input type="url" name="site" required>
```

### 6. `type="search"` - Champ de recherche

**Optimisé pour les recherches.**

```html
<label for="recherche">Rechercher :</label>
<input type="search"
       id="recherche"
       name="q"
       placeholder="Tapez votre recherche...">
```

**✅ Avantages :**
- **Icône de recherche** : Certains navigateurs affichent une loupe
- **Bouton X pour effacer** : Apparaît automatiquement quand on tape
- **Sémantique claire** : Indique que c'est une recherche

**Utilisation typique avec GET :**
```html
<form action="/recherche" method="get">
    <input type="search"
           name="q"
           placeholder="Rechercher sur le site..."
           autocomplete="off">
    <button type="submit">🔍 Rechercher</button>
</form>
```

---

## Types d'inputs pour les nombres

### 7. `type="number"` - Nombre

**Pour saisir des valeurs numériques.**

```html
<label for="age">Âge :</label>
<input type="number"
       id="age"
       name="age"
       min="18"
       max="120"
       step="1"
       required>
```

**Caractéristiques :**
- **Flèches +/- pour incrémenter/décrémenter**
- **Clavier numérique sur mobile**
- **Validation automatique** : Refuse les lettres

**Attributs spécifiques :**
```html
<input type="number"
       name="quantite"
       min="1"          <!-- Valeur minimale -->
       max="100"        <!-- Valeur maximale -->
       step="1"         <!-- Incrément (1 par défaut) -->
       value="10">      <!-- Valeur par défaut -->
```

**Exemples pratiques :**

```html
<!-- Âge (entiers seulement) -->
<input type="number" name="age" min="0" max="150" step="1">

<!-- Prix (avec décimales) -->
<input type="number" name="prix" min="0" step="0.01" placeholder="19.99">

<!-- Quantité de produits -->
<input type="number" name="quantite" min="1" max="99" value="1">

<!-- Note (de 0 à 20) -->
<input type="number" name="note" min="0" max="20" step="0.5" placeholder="10.5">
```

**⚠️ Attention :** Pour les numéros de téléphone, de carte bancaire, ou autres "nombres" qui ne sont pas destinés à des calculs, utilisez `type="tel"` ou `type="text"` avec `pattern`, pas `type="number"` !

### 8. `type="range"` - Curseur (slider)

**Pour sélectionner une valeur dans une plage avec un curseur.**

```html
<label for="volume">Volume :</label>
<input type="range"
       id="volume"
       name="volume"
       min="0"
       max="100"
       value="50"
       step="1">
<output for="volume">50</output>
```

**Caractéristiques :**
- **Interface visuelle (slider)** : L'utilisateur fait glisser un curseur
- **Pas de saisie manuelle** : Uniquement interaction visuelle
- **Valeur par défaut au milieu** si non spécifiée

**Attributs :**
```html
<input type="range"
       name="luminosite"
       min="0"          <!-- Valeur minimale -->
       max="100"        <!-- Valeur maximale -->
       value="75"       <!-- Valeur par défaut -->
       step="5">        <!-- Incrément par 5 -->
```

**Exemple avec affichage de la valeur en JavaScript :**

```html
<label for="temperature">Température souhaitée :</label>
<input type="range"
       id="temperature"
       name="temperature"
       min="15"
       max="30"
       value="20"
       oninput="afficherValeur(this.value)">
<output id="temp-value">20°C</output>

<script>
function afficherValeur(val) {
    document.getElementById('temp-value').textContent = val + '°C';
}
</script>
```

**Cas d'usage :**
- Volume sonore
- Luminosité
- Zoom
- Note/évaluation
- Filtres de prix
- Réglages d'intensité

---

## Types d'inputs pour les dates et heures

HTML5 offre plusieurs types pour gérer dates et heures, avec des sélecteurs natifs (calendriers) selon les navigateurs.

### 9. `type="date"` - Date

**Pour sélectionner une date (jour/mois/année).**

```html
<label for="naissance">Date de naissance :</label>
<input type="date"
       id="naissance"
       name="date_naissance"
       min="1900-01-01"
       max="2024-12-31"
       required>
```

**Format :** `YYYY-MM-DD` (2024-12-03)

**Caractéristiques :**
- **Sélecteur de date visuel** (calendrier) dans la plupart des navigateurs
- **Validation automatique** : Refuse les dates invalides
- **Format standardisé** : Toujours envoyé au format ISO (YYYY-MM-DD)

**Attributs :**
```html
<input type="date"
       name="date_evenement"
       min="2024-01-01"      <!-- Date minimale -->
       max="2025-12-31"      <!-- Date maximale -->
       value="2024-12-03">   <!-- Date par défaut -->
```

**Exemples :**

```html
<!-- Date de naissance (pas dans le futur) -->
<input type="date"
       name="naissance"
       max="2024-12-31">

<!-- Date de rendez-vous (uniquement dans le futur) -->
<input type="date"
       name="rdv"
       min="2024-12-03">

<!-- Date dans une plage spécifique -->
<input type="date"
       name="reservation"
       min="2024-12-10"
       max="2025-01-31">
```

### 10. `type="time"` - Heure

**Pour sélectionner une heure (heures:minutes).**

```html
<label for="heure">Heure de rendez-vous :</label>
<input type="time"
       id="heure"
       name="heure"
       min="09:00"
       max="18:00"
       required>
```

**Format :** `HH:MM` (14:30) ou `HH:MM:SS` avec secondes

**Exemples :**

```html
<!-- Heure de rendez-vous (9h à 18h) -->
<input type="time"
       name="heure_rdv"
       min="09:00"
       max="18:00"
       step="1800">  <!-- Pas de 30 minutes (1800 secondes) -->

<!-- Heure d'alarme -->
<input type="time"
       name="alarme"
       value="07:00">
```

### 11. `type="datetime-local"` - Date et heure

**Pour sélectionner une date ET une heure.**

```html
<label for="datetime">Date et heure :</label>
<input type="datetime-local"
       id="datetime"
       name="datetime"
       required>
```

**Format :** `YYYY-MM-DDTHH:MM` (2024-12-03T14:30)

**Exemple :**

```html
<!-- Rendez-vous avec date et heure -->
<input type="datetime-local"
       name="rendez_vous"
       min="2024-12-03T09:00"
       max="2024-12-31T18:00">
```

### 12. `type="month"` - Mois et année

**Pour sélectionner un mois et une année.**

```html
<label for="mois">Mois de départ :</label>
<input type="month"
       id="mois"
       name="mois"
       min="2024-01"
       max="2025-12">
```

**Format :** `YYYY-MM` (2024-12)

**Cas d'usage :**
- Date d'expiration de carte bancaire
- Mois de naissance
- Période d'abonnement

```html
<!-- Date d'expiration de carte -->
<label for="expiration">Date d'expiration (MM/AA) :</label>
<input type="month"
       name="expiration"
       min="2024-12">
```

### 13. `type="week"` - Semaine

**Pour sélectionner une semaine de l'année.**

```html
<label for="semaine">Semaine de livraison :</label>
<input type="week"
       id="semaine"
       name="semaine">
```

**Format :** `YYYY-Www` (2024-W49 = semaine 49 de 2024)

**Usage rare**, principalement pour planifications spécifiques.

---

## Type d'input pour les couleurs

### 14. `type="color"` - Sélecteur de couleur

**Pour choisir une couleur avec un sélecteur visuel.**

```html
<label for="couleur">Couleur préférée :</label>
<input type="color"
       id="couleur"
       name="couleur"
       value="#3498db">
```

**Caractéristiques :**
- **Sélecteur de couleurs natif** (color picker)
- **Format hexadécimal** : Toujours au format #RRGGBB
- **Valeur par défaut** : #000000 (noir) si non spécifié

**Exemples :**

```html
<!-- Couleur de personnalisation -->
<label for="couleur-theme">Couleur du thème :</label>
<input type="color"
       name="couleur_theme"
       value="#2c3e50">

<!-- Couleur de texte -->
<label for="text-color">Couleur du texte :</label>
<input type="color"
       name="text_color"
       value="#ffffff">
```

**Note :** La valeur est TOUJOURS envoyée au format hexadécimal (#RRGGBB).

---

## Types d'inputs pour choix multiples

### 15. `type="checkbox"` - Case à cocher

**Pour des choix multiples (on/off, oui/non, sélection multiple).**

```html
<input type="checkbox"
       id="newsletter"
       name="newsletter"
       value="oui">
<label for="newsletter">S'abonner à la newsletter</label>
```

**Caractéristiques :**
- **État binaire** : coché ou non coché
- **Envoi conditionnel** : Envoyé uniquement si coché
- **Valeur par défaut** : "on" si l'attribut `value` est omis

**Important :** Placez le `<label>` APRÈS pour une meilleure UX au clic.

**Exemples :**

```html
<!-- Case unique (conditions) -->
<input type="checkbox"
       id="conditions"
       name="conditions"
       value="accepte"
       required>
<label for="conditions">
    J'accepte les <a href="/cgu">conditions d'utilisation</a>
</label>

<!-- Plusieurs cases (intérêts multiples) -->
<fieldset>
    <legend>Vos centres d'intérêt :</legend>

    <input type="checkbox" id="sport" name="interets[]" value="sport">
    <label for="sport">Sport</label>

    <input type="checkbox" id="musique" name="interets[]" value="musique">
    <label for="musique">Musique</label>

    <input type="checkbox" id="lecture" name="interets[]" value="lecture">
    <label for="lecture">Lecture</label>

    <input type="checkbox" id="cinema" name="interets[]" value="cinema">
    <label for="cinema">Cinéma</label>
</fieldset>
```

**Cocher par défaut :**
```html
<input type="checkbox"
       id="newsletter"
       name="newsletter"
       value="oui"
       checked>
<label for="newsletter">S'abonner à la newsletter</label>
```

### 16. `type="radio"` - Bouton radio

**Pour un choix unique parmi plusieurs options.**

```html
<fieldset>
    <legend>Civilité :</legend>

    <input type="radio" id="mr" name="civilite" value="monsieur" required>
    <label for="mr">Monsieur</label>

    <input type="radio" id="mme" name="civilite" value="madame" required>
    <label for="mme">Madame</label>

    <input type="radio" id="autre" name="civilite" value="autre" required>
    <label for="autre">Autre</label>
</fieldset>
```

**⚠️ Règle cruciale :** Tous les boutons radio d'un même groupe doivent avoir le **même `name`** !

**Caractéristiques :**
- **Choix exclusif** : Un seul peut être sélectionné
- **Même `name`** : Obligatoire pour les grouper
- **Déselection impossible** : Une fois sélectionné, il faut choisir un autre

**Exemples :**

```html
<!-- Question à choix unique -->
<fieldset>
    <legend>Niveau d'expérience :</legend>

    <input type="radio" id="debutant" name="niveau" value="debutant">
    <label for="debutant">Débutant</label>

    <input type="radio" id="intermediaire" name="niveau" value="intermediaire">
    <label for="intermediaire">Intermédiaire</label>

    <input type="radio" id="avance" name="niveau" value="avance">
    <label for="avance">Avancé</label>
</fieldset>

<!-- Avec option par défaut -->
<fieldset>
    <legend>Moyen de paiement :</legend>

    <input type="radio" id="carte" name="paiement" value="carte" checked>
    <label for="carte">Carte bancaire</label>

    <input type="radio" id="paypal" name="paiement" value="paypal">
    <label for="paypal">PayPal</label>

    <input type="radio" id="virement" name="paiement" value="virement">
    <label for="virement">Virement</label>
</fieldset>
```

**Checkbox vs Radio :**

| Critère | Checkbox | Radio |
|---------|----------|-------|
| **Choix** | Multiple | Un seul |
| **Déselection** | Possible (cliquer à nouveau) | Impossible |
| **Utilisation** | Options indépendantes | Choix exclusifs |
| **Name** | Peut être différent | Doit être identique |

---

## Type d'input pour fichiers

### 17. `type="file"` - Upload de fichier

**Pour permettre l'upload de fichiers.**

```html
<label for="photo">Télécharger une photo :</label>
<input type="file"
       id="photo"
       name="photo"
       accept="image/*"
       required>
```

**⚠️ IMPORTANT :** Le formulaire DOIT avoir `enctype="multipart/form-data"` et `method="post"` :

```html
<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="fichier" accept="image/*" required>
    <button type="submit">Envoyer</button>
</form>
```

**Attributs spécifiques :**

```html
<input type="file"
       name="document"
       accept=".pdf,.doc,.docx"  <!-- Types de fichiers acceptés -->
       multiple>                  <!-- Permet plusieurs fichiers -->
```

**Exemples avec `accept` :**

```html
<!-- Uniquement des images -->
<input type="file" name="photo" accept="image/*">

<!-- Images spécifiques -->
<input type="file" name="photo" accept="image/png, image/jpeg, image/jpg">

<!-- Documents PDF -->
<input type="file" name="document" accept=".pdf">

<!-- Documents Word -->
<input type="file" name="document" accept=".doc,.docx">

<!-- Feuilles de calcul Excel -->
<input type="file" name="fichier" accept=".xls,.xlsx">

<!-- Plusieurs types -->
<input type="file" name="fichier" accept=".pdf,.doc,.docx,.jpg,.png">

<!-- Fichiers audio -->
<input type="file" name="audio" accept="audio/*">

<!-- Fichiers vidéo -->
<input type="file" name="video" accept="video/*">
```

**Upload multiple :**

```html
<label for="photos">Sélectionner plusieurs photos :</label>
<input type="file"
       id="photos"
       name="photos[]"
       accept="image/*"
       multiple>
```

**Note :** Le `[]` dans le name (`photos[]`) est une convention pour indiquer au serveur que c'est un tableau de fichiers.

---

## Type d'input caché

### 18. `type="hidden"` - Champ caché

**Pour envoyer des données invisibles pour l'utilisateur.**

```html
<input type="hidden" name="user_id" value="12345">
<input type="hidden" name="action" value="modifier">
<input type="hidden" name="token" value="abc123xyz">
```

**Caractéristiques :**
- **Invisible** pour l'utilisateur
- **Envoyé avec le formulaire** comme les autres champs
- **Utile pour** : IDs, tokens de sécurité, actions, etc.

**⚠️ Sécurité :** Les champs cachés restent visibles dans le code source de la page ! Ne les utilisez pas pour des données sensibles.

**Cas d'usage :**

```html
<form action="/modifier-profil" method="post">
    <!-- ID de l'utilisateur (caché) -->
    <input type="hidden" name="user_id" value="42">

    <!-- Token CSRF pour sécurité -->
    <input type="hidden" name="csrf_token" value="abc123xyz789">

    <!-- Champs visibles -->
    <input type="text" name="nom" placeholder="Nom">
    <input type="email" name="email" placeholder="Email">

    <button type="submit">Modifier</button>
</form>
```

---

## Types d'inputs pour boutons

### 19. `type="submit"` - Bouton d'envoi

**Soumet le formulaire.**

```html
<input type="submit" value="Envoyer le formulaire">
<!-- ou mieux (plus flexible) -->
<button type="submit">Envoyer le formulaire</button>
```

**Recommandation :** Préférez `<button type="submit">` car il permet d'inclure des icônes, images, etc.

### 20. `type="reset"` - Bouton de réinitialisation

**Efface tous les champs du formulaire.**

```html
<input type="reset" value="Réinitialiser">
<!-- ou -->
<button type="reset">Réinitialiser</button>
```

**⚠️ Attention :** Rarement recommandé car frustrant pour l'utilisateur (clic accidentel).

### 21. `type="button"` - Bouton neutre

**Ne fait rien par défaut, utilisé avec JavaScript.**

```html
<input type="button" value="Calculer" onclick="calculer()">
<!-- ou mieux -->
<button type="button" onclick="afficherAide()">Aide</button>
```

### 22. `type="image"` - Bouton image

**Bouton d'envoi avec une image.**

```html
<input type="image"
       src="bouton-envoyer.png"
       alt="Envoyer le formulaire"
       width="100"
       height="40">
```

**⚠️ Peu utilisé aujourd'hui.** Préférez `<button>` avec une image à l'intérieur :

```html
<button type="submit">
    <img src="icone.png" alt="">
    Envoyer
</button>
```

---

## Tableau récapitulatif des types

| Type | Usage | Validation native | Clavier mobile |
|------|-------|-------------------|----------------|
| **text** | Texte général | Non | Standard |
| **email** | Email | ✅ Oui (format email) | @ et .com |
| **password** | Mot de passe | Non | Standard (masqué) |
| **tel** | Téléphone | Non | Numérique |
| **url** | URL | ✅ Oui (format URL) | .com |
| **search** | Recherche | Non | Standard + X |
| **number** | Nombre | ✅ Oui (numérique) | Numérique |
| **range** | Curseur | Non | - |
| **date** | Date | ✅ Oui (format date) | Calendrier |
| **time** | Heure | ✅ Oui (format heure) | Sélecteur |
| **datetime-local** | Date + heure | ✅ Oui | Calendrier + heure |
| **month** | Mois/année | ✅ Oui | Sélecteur |
| **week** | Semaine | ✅ Oui | Sélecteur |
| **color** | Couleur | ✅ Oui (hexa) | Sélecteur |
| **checkbox** | Choix multiple | Non | - |
| **radio** | Choix unique | Non | - |
| **file** | Upload | Non | Fichiers |
| **hidden** | Données cachées | Non | - |

---

## Attributs communs importants

### `placeholder` - Texte indicatif

Affiche un texte d'aide qui disparaît lors de la saisie :

```html
<input type="text"
       name="nom"
       placeholder="Ex: Jean Dupont">
```

**⚠️ Attention :** Le placeholder n'est PAS un label ! Toujours avoir un `<label>` en plus.

```html
<!-- ❌ MAUVAIS : que du placeholder -->
<input type="email" placeholder="Email">

<!-- ✅ BON : label + placeholder -->
<label for="email">Email :</label>
<input type="email" id="email" name="email" placeholder="jean@example.com">
```

### `required` - Champ obligatoire

Rend le champ obligatoire (validation native) :

```html
<input type="text" name="nom" required>
```

Le navigateur empêchera la soumission si le champ est vide.

### `readonly` - Lecture seule

L'utilisateur ne peut pas modifier la valeur :

```html
<input type="text" name="user_id" value="12345" readonly>
```

**readonly vs disabled :**
- `readonly` : Valeur envoyée avec le formulaire
- `disabled` : Valeur NON envoyée

### `disabled` - Désactivé

Le champ est grisé et non modifiable, et sa valeur n'est PAS envoyée :

```html
<input type="text" name="ancien_email" value="ancien@example.com" disabled>
```

### `autocomplete` - Autocomplétion

Contrôle l'autocomplétion du navigateur :

```html
<!-- Activer (par défaut) -->
<input type="email" name="email" autocomplete="email">

<!-- Désactiver -->
<input type="text" name="code" autocomplete="off">
```

**Valeurs spécifiques utiles :**
- `name` : Nom complet
- `given-name` : Prénom
- `family-name` : Nom de famille
- `email` : Email
- `tel` : Téléphone
- `street-address` : Adresse
- `postal-code` : Code postal
- `country` : Pays
- `cc-number` : Numéro de carte bancaire
- `cc-exp` : Date d'expiration carte
- `new-password` : Nouveau mot de passe
- `current-password` : Mot de passe actuel

### `pattern` - Expression régulière

Définit un motif (regex) que la valeur doit respecter :

```html
<!-- Code postal français (5 chiffres) -->
<input type="text"
       name="code_postal"
       pattern="[0-9]{5}"
       title="5 chiffres requis">

<!-- Plaque d'immatriculation -->
<input type="text"
       name="plaque"
       pattern="[A-Z]{2}-[0-9]{3}-[A-Z]{2}"
       placeholder="AA-123-BB">

<!-- Nom d'utilisateur (lettres, chiffres, tiret, underscore) -->
<input type="text"
       name="username"
       pattern="[a-zA-Z0-9_-]{3,16}"
       title="3 à 16 caractères, lettres, chiffres, - ou _">
```

**Attribut `title`** : Affiche un message d'aide si la validation échoue.

### `minlength` et `maxlength` - Longueur

Définissent la longueur minimale et maximale :

```html
<input type="text"
       name="username"
       minlength="3"
       maxlength="20">
```

### `min`, `max`, `step` - Pour les nombres et dates

```html
<!-- Nombre de 1 à 100, par pas de 5 -->
<input type="number" name="quantite" min="1" max="100" step="5">

<!-- Date entre aujourd'hui et dans 1 an -->
<input type="date" name="reservation" min="2024-12-03" max="2025-12-03">
```

---

## Exemples de formulaires complets

### Exemple 1 : Formulaire de contact

```html
<form action="/contact" method="post">
    <h2>Nous contacter</h2>

    <div>
        <label for="nom">Nom complet * :</label>
        <input type="text"
               id="nom"
               name="nom"
               placeholder="Jean Dupont"
               required>
    </div>

    <div>
        <label for="email">Email * :</label>
        <input type="email"
               id="email"
               name="email"
               placeholder="jean@example.com"
               autocomplete="email"
               required>
    </div>

    <div>
        <label for="telephone">Téléphone :</label>
        <input type="tel"
               id="telephone"
               name="telephone"
               placeholder="06 12 34 56 78"
               pattern="[0-9\s]{10,14}"
               autocomplete="tel">
    </div>

    <div>
        <label for="sujet">Sujet * :</label>
        <select id="sujet" name="sujet" required>
            <option value="">-- Choisir --</option>
            <option value="info">Demande d'information</option>
            <option value="devis">Demande de devis</option>
            <option value="support">Support technique</option>
            <option value="autre">Autre</option>
        </select>
    </div>

    <div>
        <label for="message">Message * :</label>
        <textarea id="message"
                  name="message"
                  rows="6"
                  placeholder="Votre message..."
                  required></textarea>
    </div>

    <div>
        <input type="checkbox"
               id="copie"
               name="copie"
               value="oui">
        <label for="copie">Recevoir une copie par email</label>
    </div>

    <button type="submit">Envoyer le message</button>
</form>
```

### Exemple 2 : Formulaire de réservation

```html
<form action="/reserver" method="post">
    <h2>Réservation de chambre</h2>

    <div>
        <label for="checkin">Date d'arrivée * :</label>
        <input type="date"
               id="checkin"
               name="date_arrivee"
               min="2024-12-03"
               required>
    </div>

    <div>
        <label for="checkout">Date de départ * :</label>
        <input type="date"
               id="checkout"
               name="date_depart"
               min="2024-12-04"
               required>
    </div>

    <div>
        <label for="adultes">Nombre d'adultes * :</label>
        <input type="number"
               id="adultes"
               name="adultes"
               min="1"
               max="4"
               value="2"
               required>
    </div>

    <div>
        <label for="enfants">Nombre d'enfants :</label>
        <input type="number"
               id="enfants"
               name="enfants"
               min="0"
               max="3"
               value="0">
    </div>

    <fieldset>
        <legend>Type de chambre * :</legend>

        <input type="radio" id="simple" name="type_chambre" value="simple" required>
        <label for="simple">Chambre simple (80€/nuit)</label><br>

        <input type="radio" id="double" name="type_chambre" value="double" required>
        <label for="double">Chambre double (120€/nuit)</label><br>

        <input type="radio" id="suite" name="type_chambre" value="suite" required>
        <label for="suite">Suite (200€/nuit)</label>
    </fieldset>

    <fieldset>
        <legend>Options supplémentaires :</legend>

        <input type="checkbox" id="petit-dej" name="options[]" value="petit-dejeuner">
        <label for="petit-dej">Petit-déjeuner (+12€/pers)</label><br>

        <input type="checkbox" id="parking" name="options[]" value="parking">
        <label for="parking">Parking (+10€/jour)</label><br>

        <input type="checkbox" id="wifi" name="options[]" value="wifi">
        <label for="wifi">WiFi premium (+5€/jour)</label>
    </fieldset>

    <div>
        <label for="remarques">Remarques particulières :</label>
        <textarea id="remarques"
                  name="remarques"
                  rows="4"
                  placeholder="Allergies, préférences..."></textarea>
    </div>

    <button type="submit">Réserver maintenant</button>
</form>
```

### Exemple 3 : Formulaire d'inscription

```html
<form action="/inscription" method="post">
    <h2>Créer un compte</h2>

    <div>
        <label for="username">Nom d'utilisateur * :</label>
        <input type="text"
               id="username"
               name="username"
               pattern="[a-zA-Z0-9_-]{3,20}"
               title="3 à 20 caractères, lettres, chiffres, - ou _"
               autocomplete="username"
               required>
    </div>

    <div>
        <label for="email">Email * :</label>
        <input type="email"
               id="email"
               name="email"
               autocomplete="email"
               required>
    </div>

    <div>
        <label for="password">Mot de passe * :</label>
        <input type="password"
               id="password"
               name="password"
               minlength="8"
               autocomplete="new-password"
               required>
        <small>Minimum 8 caractères</small>
    </div>

    <div>
        <label for="password-confirm">Confirmer le mot de passe * :</label>
        <input type="password"
               id="password-confirm"
               name="password_confirm"
               minlength="8"
               autocomplete="new-password"
               required>
    </div>

    <div>
        <label for="naissance">Date de naissance * :</label>
        <input type="date"
               id="naissance"
               name="date_naissance"
               max="2006-12-31"
               autocomplete="bday"
               required>
        <small>Vous devez avoir au moins 18 ans</small>
    </div>

    <div>
        <label for="pays">Pays * :</label>
        <select id="pays" name="pays" autocomplete="country" required>
            <option value="">-- Sélectionner --</option>
            <option value="FR">France</option>
            <option value="BE">Belgique</option>
            <option value="CH">Suisse</option>
            <option value="CA">Canada</option>
        </select>
    </div>

    <div>
        <input type="checkbox"
               id="newsletter"
               name="newsletter"
               value="oui">
        <label for="newsletter">Recevoir la newsletter</label>
    </div>

    <div>
        <input type="checkbox"
               id="cgu"
               name="cgu"
               value="accepte"
               required>
        <label for="cgu">
            J'accepte les <a href="/cgu" target="_blank">conditions générales d'utilisation</a> *
        </label>
    </div>

    <button type="submit">Créer mon compte</button>
</form>
```

---

## Bonnes pratiques

### ✅ À FAIRE

1. **Choisir le bon type d'input** pour chaque donnée
```html
<!-- ✅ BON : email pour email -->
<input type="email" name="email">

<!-- ❌ MAUVAIS : text pour email -->
<input type="text" name="email">
```

2. **Toujours avoir un label associé**
```html
<!-- ✅ BON -->
<label for="nom">Nom :</label>
<input type="text" id="nom" name="nom">
```

3. **Utiliser `autocomplete` approprié**
```html
<input type="email" name="email" autocomplete="email">
<input type="tel" name="tel" autocomplete="tel">
```

4. **Ajouter des `placeholder` informatifs**
```html
<input type="tel"
       name="tel"
       placeholder="06 12 34 56 78"
       pattern="[0-9\s]{10,14}">
```

5. **Valider avec `pattern` quand nécessaire**
```html
<input type="text"
       name="code_postal"
       pattern="[0-9]{5}"
       title="Code postal à 5 chiffres">
```

6. **Utiliser `min`/`max` pour limiter les plages**
```html
<input type="number" name="age" min="18" max="120">
<input type="date" name="rdv" min="2024-12-03">
```

### ❌ À ÉVITER

1. **Utiliser `type="text"` pour tout**
```html
<!-- ❌ MAUVAIS -->
<input type="text" name="email">
<input type="text" name="telephone">
<input type="text" name="date">

<!-- ✅ BON -->
<input type="email" name="email">
<input type="tel" name="telephone">
<input type="date" name="date">
```

2. **Oublier l'attribut `name`**
```html
<!-- ❌ MAUVAIS : pas de name, donnée perdue -->
<input type="text" id="nom">

<!-- ✅ BON -->
<input type="text" id="nom" name="nom">
```

3. **Utiliser `placeholder` comme label**
```html
<!-- ❌ MAUVAIS : pas accessible -->
<input type="text" placeholder="Votre nom">

<!-- ✅ BON -->
<label for="nom">Nom :</label>
<input type="text" id="nom" name="nom" placeholder="Ex: Jean Dupont">
```

4. **Oublier `enctype` pour les fichiers**
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

---

## Points clés à retenir

1. **HTML5 offre 22+ types d'inputs** pour tous les usages
2. **Choisissez le bon type** : améliore UX, validation, accessibilité
3. **Types essentiels modernes** : email, tel, url, number, date, color
4. **Validation native gratuite** : email, url, number, date, pattern
5. **Clavier mobile adapté** : email (@), tel (chiffres), url (.com)
6. **Checkbox** = choix multiples, **Radio** = choix unique
7. **Upload de fichiers** = obligatoirement `enctype="multipart/form-data"`
8. **Toujours un `name`** pour envoyer la donnée
9. **Attributs utiles** : placeholder, required, pattern, min/max
10. **Label obligatoire** : jamais que du placeholder

---

## Prochaine étape

Maintenant que vous connaissez tous les types d'inputs disponibles, nous allons découvrir dans le prochain chapitre comment structurer correctement vos formulaires avec les balises **`<label>`, `<fieldset>` et `<legend>`** pour améliorer l'accessibilité et l'organisation de vos formulaires.

⏭️ [Labels, fieldsets et accessibilité](/03-html5-structure-et-semantique/04-formulaires-html5/03-labels-fieldsets-accessibilite.md)
