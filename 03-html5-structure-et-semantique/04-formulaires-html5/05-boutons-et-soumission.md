🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.4.5 Boutons et gestion de soumission

## Introduction

Les boutons sont l'élément final et essentiel d'un formulaire : ils permettent à l'utilisateur de **soumettre** ses données, de **réinitialiser** le formulaire, ou d'effectuer d'autres actions. Bien que cela puisse sembler simple, il existe plusieurs façons de créer des boutons, chacune avec ses spécificités et ses cas d'usage.

Dans ce chapitre, nous allons explorer :
- Les différents types de boutons disponibles
- Comment gérer la soumission d'un formulaire
- Les événements liés aux formulaires
- Les bonnes pratiques pour une expérience utilisateur optimale

---

## Les différents types de boutons

### 1. `<button>` - Le bouton moderne (RECOMMANDÉ)

La balise `<button>` est la méthode **moderne et recommandée** pour créer des boutons dans les formulaires.

```html
<button type="submit">Envoyer</button>
```

**Avantages :**
- ✅ Plus flexible : peut contenir du HTML (icônes, images, texte formaté)
- ✅ Plus facile à styliser avec CSS
- ✅ Meilleure sémantique
- ✅ Comportement plus prévisible

**Structure :**
```html
<button type="type-du-bouton">
    Contenu du bouton (texte, HTML, icônes...)
</button>
```

### 2. `<input type="submit">` - Le bouton classique

La méthode historique, encore valide mais moins flexible :

```html
<input type="submit" value="Envoyer">
```

**Limites :**
- ❌ Ne peut contenir que du texte (pas de HTML)
- ❌ Moins flexible pour le style
- ❌ Attribut `value` pour le texte (moins intuitif)

**Recommandation :** Préférez `<button>` dans les nouveaux projets.

---

## Les types de boutons (`type`)

L'attribut `type` définit le comportement du bouton. Il existe trois valeurs principales :

### `type="submit"` - Soumettre le formulaire

**C'est le type par défaut** pour les boutons dans un formulaire.

```html
<form action="/contact" method="post">
    <!-- Champs du formulaire -->

    <!-- Ces deux boutons font la même chose -->
    <button type="submit">Envoyer</button>
    <button>Envoyer</button> <!-- type="submit" par défaut -->
</form>
```

**Comportement :**
1. Déclenche la validation HTML5
2. Si valide, soumet le formulaire vers l'URL `action`
3. Déclenche l'événement `submit` sur le formulaire

**⚠️ Important :** Dans un formulaire, **un bouton sans `type` est considéré comme `type="submit"`** !

```html
<form>
    <!-- ⚠️ Ce bouton soumettra le formulaire ! -->
    <button onclick="fonctionJS()">Cliquez-moi</button>

    <!-- ✅ BON : type="button" pour éviter la soumission -->
    <button type="button" onclick="fonctionJS()">Cliquez-moi</button>
</form>
```

### `type="reset"` - Réinitialiser le formulaire

Efface tous les champs du formulaire et les remet à leurs valeurs par défaut.

```html
<form>
    <input type="text" name="nom" value="Jean">

    <button type="submit">Envoyer</button>
    <button type="reset">Réinitialiser</button>
</form>
```

**Comportement :**
- Tous les champs reprennent leur valeur `value` par défaut
- Les champs vides redeviennent vides
- Ne soumet PAS le formulaire

**⚠️ Attention :** Le bouton reset est généralement **déconseillé** :
- Frustrant si cliqué par erreur
- Rarement utile (l'utilisateur peut rafraîchir la page)
- Peut être confondu avec le bouton submit

```html
<!-- ❌ ÉVITER : risque de clic accidentel -->
<button type="submit">Envoyer</button>
<button type="reset">Réinitialiser</button>

<!-- ✅ MIEUX : confirmation avant reset -->
<button type="submit">Envoyer</button>
<button type="button" onclick="confirmerReset()">Réinitialiser</button>

<script>
function confirmerReset() {
    if (confirm('Voulez-vous vraiment réinitialiser le formulaire ?')) {
        document.getElementById('mon-formulaire').reset();
    }
}
</script>
```

### `type="button"` - Bouton neutre

Un bouton qui ne fait **rien par défaut**. Utilisé avec JavaScript pour des actions personnalisées.

```html
<button type="button" onclick="afficherAide()">Aide ?</button>
<button type="button" onclick="calculer()">Calculer</button>
<button type="button" id="ajouter-champ">Ajouter un champ</button>
```

**Utilisations courantes :**
- Actions JavaScript personnalisées
- Ouvrir des modals
- Ajouter/supprimer des champs dynamiquement
- Navigation (avec JavaScript)
- Calculateurs, compteurs, etc.

```html
<form>
    <div id="champs-email">
        <input type="email" name="email[]" placeholder="Email 1">
    </div>

    <!-- Ajouter un champ email sans soumettre -->
    <button type="button" onclick="ajouterEmail()">
        + Ajouter un email
    </button>

    <button type="submit">Envoyer</button>
</form>

<script>
let compteur = 1;
function ajouterEmail() {
    compteur++;
    const container = document.getElementById('champs-email');
    const newInput = document.createElement('input');
    newInput.type = 'email';
    newInput.name = 'email[]';
    newInput.placeholder = `Email ${compteur}`;
    container.appendChild(newInput);
}
</script>
```

---

## `<button>` vs `<input type="submit">`

### Comparaison détaillée

```html
<!-- ✅ RECOMMANDÉ : <button> -->
<button type="submit">
    <span class="icon">📧</span>
    Envoyer le message
</button>

<!-- ⚠️ ANCIEN : <input> -->
<input type="submit" value="Envoyer le message">
```

| Critère | `<button>` | `<input type="submit">` |
|---------|-----------|------------------------|
| **Contenu HTML** | ✅ Oui (icônes, spans, etc.) | ❌ Texte uniquement |
| **Flexibilité CSS** | ✅ Excellente | ⚠️ Limitée |
| **Texte du bouton** | Entre balises | Attribut `value` |
| **Accessibilité** | ✅ Très bonne | ✅ Bonne |
| **Standard moderne** | ✅ Recommandé | ⚠️ Legacy |

### Exemples de contenu enrichi avec `<button>`

```html
<!-- Bouton avec icône -->
<button type="submit">
    <svg class="icon" width="16" height="16">
        <!-- SVG content -->
    </svg>
    Envoyer
</button>

<!-- Bouton avec image -->
<button type="submit">
    <img src="icon-send.png" alt="" width="20" height="20">
    Envoyer le message
</button>

<!-- Bouton avec plusieurs lignes -->
<button type="submit" class="big-button">
    <strong>Finaliser la commande</strong>
    <small>Paiement sécurisé</small>
</button>

<!-- Bouton avec loader -->
<button type="submit" id="submit-btn">
    <span class="text">Envoyer</span>
    <span class="loader" style="display: none;">⏳</span>
</button>
```

**Avec `<input>`, impossible de faire ça !**

```html
<!-- ❌ Impossible avec input -->
<input type="submit" value="<img src='icon.png'> Envoyer">
<!-- Le HTML est affiché comme du texte brut -->
```

---

## Événements de soumission

### L'événement `submit`

L'événement `submit` se déclenche quand le formulaire est soumis (validation réussie).

```html
<form id="mon-formulaire">
    <input type="email" name="email" required>
    <button type="submit">Envoyer</button>
</form>

<script>
const form = document.getElementById('mon-formulaire');

form.addEventListener('submit', function(event) {
    console.log('Formulaire soumis !');

    // Accéder aux données
    const email = event.target.email.value;
    console.log('Email:', email);
});
</script>
```

**Points importants :**
- Se déclenche **uniquement si la validation réussit**
- `event.target` est le formulaire
- Par défaut, recharge la page (comportement natif)

### Empêcher la soumission avec `preventDefault()`

Pour traiter le formulaire en JavaScript sans recharger la page :

```html
<form id="contact-form">
    <input type="text" name="nom" required>
    <input type="email" name="email" required>
    <button type="submit">Envoyer</button>
</form>

<script>
const form = document.getElementById('contact-form');

form.addEventListener('submit', function(event) {
    // Empêcher le comportement par défaut (rechargement)
    event.preventDefault();

    // Traiter les données en JavaScript
    const formData = new FormData(event.target);

    console.log('Nom:', formData.get('nom'));
    console.log('Email:', formData.get('email'));

    // Envoyer avec fetch, AJAX, etc.
    envoyerAuServeur(formData);
});

function envoyerAuServeur(data) {
    // Simulation d'envoi
    console.log('Envoi en cours...');

    // Exemple avec fetch
    fetch('/api/contact', {
        method: 'POST',
        body: data
    })
    .then(response => response.json())
    .then(result => {
        console.log('Succès:', result);
        alert('Message envoyé !');
    })
    .catch(error => {
        console.error('Erreur:', error);
        alert('Erreur lors de l\'envoi');
    });
}
</script>
```

### L'événement `click` sur le bouton

Vous pouvez aussi écouter le clic sur le bouton (moins recommandé) :

```html
<form>
    <input type="text" name="nom" required>
    <button type="submit" id="btn-submit">Envoyer</button>
</form>

<script>
const btn = document.getElementById('btn-submit');

// ⚠️ MOINS BON : sur le bouton
btn.addEventListener('click', function(event) {
    event.preventDefault();
    console.log('Bouton cliqué');
});

// ✅ MEILLEUR : sur le formulaire
form.addEventListener('submit', function(event) {
    event.preventDefault();
    console.log('Formulaire soumis');
});
</script>
```

**Pourquoi préférer `submit` ?**
- ✅ Capture aussi la soumission par `Enter`
- ✅ Plus sémantique
- ✅ Fonctionne même si plusieurs boutons
- ✅ Validation HTML5 exécutée avant

---

## Soumettre un formulaire en JavaScript

### Méthode 1 : `form.submit()` (sans validation)

```javascript
const form = document.getElementById('mon-formulaire');

// Soumet le formulaire sans validation
form.submit();
```

**⚠️ Attention :** Cette méthode **ne déclenche PAS** :
- La validation HTML5
- L'événement `submit`

**Utile uniquement dans des cas spécifiques.**

### Méthode 2 : `button.click()` (avec validation)

```javascript
const form = document.getElementById('mon-formulaire');
const submitButton = form.querySelector('button[type="submit"]');

// Simule un clic sur le bouton
submitButton.click();
```

**Avantage :** Déclenche la validation et l'événement `submit`.

### Méthode 3 : `requestSubmit()` (moderne, recommandée)

```javascript
const form = document.getElementById('mon-formulaire');

// Soumet avec validation et événement submit
form.requestSubmit();
```

**✅ RECOMMANDÉ :** Méthode moderne qui :
- Déclenche la validation HTML5
- Déclenche l'événement `submit`
- Comportement natif complet

**Compatibilité :** Navigateurs modernes (Safari 16+, Chrome 76+, Firefox 75+)

### Exemple : Soumission programmée

```html
<form id="auto-submit-form">
    <input type="text" name="recherche" placeholder="Rechercher...">
    <!-- Pas de bouton submit visible -->
</form>

<script>
const form = document.getElementById('auto-submit-form');
const input = form.querySelector('input[name="recherche"]');

// Soumettre automatiquement après 2 secondes d'inactivité
let timeout;
input.addEventListener('input', function() {
    clearTimeout(timeout);
    timeout = setTimeout(() => {
        console.log('Auto-soumission...');
        form.requestSubmit();
    }, 2000);
});

form.addEventListener('submit', function(e) {
    e.preventDefault();
    console.log('Recherche:', input.value);
    // Effectuer la recherche
});
</script>
```

---

## Boutons multiples dans un formulaire

Un formulaire peut avoir plusieurs boutons submit avec des actions différentes.

### Identifier quel bouton a été cliqué

#### Méthode 1 : Attribut `name` et `value`

```html
<form action="/traiter" method="post">
    <input type="text" name="article" value="Mon article">

    <!-- Différents boutons avec name/value -->
    <button type="submit" name="action" value="sauvegarder">
        Sauvegarder comme brouillon
    </button>

    <button type="submit" name="action" value="publier">
        Publier
    </button>

    <button type="submit" name="action" value="supprimer">
        Supprimer
    </button>
</form>
```

**Côté serveur (PHP par exemple) :**
```php
if ($_POST['action'] === 'sauvegarder') {
    // Sauvegarder comme brouillon
} elseif ($_POST['action'] === 'publier') {
    // Publier l'article
} elseif ($_POST['action'] === 'supprimer') {
    // Supprimer l'article
}
```

#### Méthode 2 : Avec JavaScript

```html
<form id="article-form">
    <textarea name="contenu" required></textarea>

    <button type="submit" data-action="draft">
        💾 Brouillon
    </button>

    <button type="submit" data-action="publish">
        ✅ Publier
    </button>
</form>

<script>
const form = document.getElementById('article-form');

form.addEventListener('submit', function(e) {
    e.preventDefault();

    // Récupérer le bouton qui a été cliqué
    const clickedButton = e.submitter;
    const action = clickedButton.dataset.action;

    console.log('Action:', action);

    const formData = new FormData(form);
    formData.append('action', action);

    // Envoyer au serveur
    fetch('/api/article', {
        method: 'POST',
        body: formData
    })
    .then(response => response.json())
    .then(data => {
        if (action === 'draft') {
            alert('Brouillon sauvegardé');
        } else {
            alert('Article publié !');
        }
    });
});
</script>
```

**Propriété `e.submitter` :** Retourne le bouton qui a soumis le formulaire (moderne).

### Attributs `formaction`, `formmethod`, etc.

Vous pouvez surcharger les attributs du formulaire pour un bouton spécifique :

```html
<form action="/save" method="post">
    <input type="text" name="data">

    <!-- Bouton normal : POST vers /save -->
    <button type="submit">Sauvegarder</button>

    <!-- Bouton spécial : GET vers /preview -->
    <button type="submit"
            formaction="/preview"
            formmethod="get"
            formtarget="_blank">
        Prévisualiser
    </button>

    <!-- Bouton sans validation -->
    <button type="submit"
            formaction="/save-draft"
            formnovalidate>
        Brouillon (sans validation)
    </button>
</form>
```

**Attributs disponibles :**
- `formaction` : Surcharge `action`
- `formmethod` : Surcharge `method`
- `formenctype` : Surcharge `enctype`
- `formtarget` : Surcharge `target`
- `formnovalidate` : Désactive la validation pour ce bouton

---

## États des boutons

### Bouton désactivé (`disabled`)

Un bouton désactivé ne peut pas être cliqué :

```html
<button type="submit" disabled>Envoyer</button>
```

**Comportement :**
- Grisé visuellement par défaut
- Aucun événement `click`
- Ne peut pas recevoir le focus
- Curseur "non autorisé" au survol

**Activation/désactivation dynamique :**

```html
<form id="contact-form">
    <input type="text" id="nom" name="nom" required>
    <input type="email" id="email" name="email" required>

    <button type="submit" id="submit-btn" disabled>
        Envoyer
    </button>
</form>

<script>
const form = document.getElementById('contact-form');
const submitBtn = document.getElementById('submit-btn');
const inputs = form.querySelectorAll('input[required]');

// Activer le bouton uniquement si tous les champs requis sont remplis
function checkForm() {
    let allFilled = true;

    inputs.forEach(input => {
        if (input.value.trim() === '') {
            allFilled = false;
        }
    });

    submitBtn.disabled = !allFilled;
}

inputs.forEach(input => {
    input.addEventListener('input', checkForm);
});

// Vérification initiale
checkForm();
</script>
```

### Bouton en cours de chargement (loading state)

Très important pour les soumissions asynchrones :

```html
<form id="async-form">
    <input type="email" name="email" required>

    <button type="submit" id="submit-btn">
        <span class="btn-text">Envoyer</span>
        <span class="btn-loader" style="display: none;">
            ⏳ Envoi en cours...
        </span>
    </button>
</form>

<style>
.btn-loader {
    animation: pulse 1.5s ease-in-out infinite;
}

@keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.5; }
}
</style>

<script>
const form = document.getElementById('async-form');
const submitBtn = document.getElementById('submit-btn');
const btnText = submitBtn.querySelector('.btn-text');
const btnLoader = submitBtn.querySelector('.btn-loader');

form.addEventListener('submit', async function(e) {
    e.preventDefault();

    // Désactiver le bouton et afficher le loader
    submitBtn.disabled = true;
    btnText.style.display = 'none';
    btnLoader.style.display = 'inline';

    try {
        const formData = new FormData(form);
        const response = await fetch('/api/submit', {
            method: 'POST',
            body: formData
        });

        if (response.ok) {
            alert('Envoyé avec succès !');
            form.reset();
        } else {
            alert('Erreur lors de l\'envoi');
        }
    } catch (error) {
        console.error('Erreur:', error);
        alert('Erreur réseau');
    } finally {
        // Réactiver le bouton
        submitBtn.disabled = false;
        btnText.style.display = 'inline';
        btnLoader.style.display = 'none';
    }
});
</script>
```

### Exemple avancé : Bouton avec compteur de clics

```html
<form>
    <input type="text" name="message" required>

    <button type="submit" id="submit-btn">
        Envoyer
    </button>
</form>

<script>
const submitBtn = document.getElementById('submit-btn');
let clickCount = 0;
let cooldown = false;

submitBtn.addEventListener('click', function(e) {
    if (cooldown) {
        e.preventDefault();
        return;
    }

    clickCount++;

    if (clickCount >= 3) {
        // Protection anti-spam
        e.preventDefault();
        cooldown = true;
        submitBtn.disabled = true;
        submitBtn.textContent = 'Veuillez patienter (5s)';

        setTimeout(() => {
            cooldown = false;
            clickCount = 0;
            submitBtn.disabled = false;
            submitBtn.textContent = 'Envoyer';
        }, 5000);
    }
});
</script>
```

---

## Soumission par la touche `Enter`

Par défaut, appuyer sur `Enter` dans un champ texte soumet le formulaire.

### Comportement par défaut

```html
<form action="/recherche" method="get">
    <input type="search" name="q" placeholder="Rechercher...">
    <!-- Pas de bouton : Enter soumet quand même -->
</form>
```

**Règle :** Si le formulaire contient un seul champ texte et pas de bouton, `Enter` soumet.

### Empêcher la soumission par Enter

```html
<form id="no-enter-form">
    <input type="text" name="champ1">
    <input type="text" name="champ2">
</form>

<script>
const form = document.getElementById('no-enter-form');

form.addEventListener('keydown', function(e) {
    // Empêcher la soumission sur Enter
    if (e.key === 'Enter' || e.keyCode === 13) {
        e.preventDefault();
        return false;
    }
});
</script>
```

### Soumettre uniquement sur Enter dans un champ spécifique

```html
<form id="smart-form">
    <input type="text" name="nom" placeholder="Nom (Enter = rien)">
    <input type="search"
           name="recherche"
           id="search-input"
           placeholder="Recherche (Enter = soumettre)">

    <button type="submit">Rechercher</button>
</form>

<script>
const form = document.getElementById('smart-form');
const searchInput = document.getElementById('search-input');

// Empêcher Enter partout sauf dans le champ recherche
form.addEventListener('keydown', function(e) {
    if (e.key === 'Enter' && e.target !== searchInput) {
        e.preventDefault();
    }
});
</script>
```

---

## Accessibilité des boutons

### Labels et texte visible

**✅ BON : Texte clair**
```html
<button type="submit">Envoyer le formulaire</button>
```

**❌ MAUVAIS : Seulement une icône**
```html
<button type="submit">➤</button>
```

**✅ SOLUTION : Icône + texte ou aria-label**
```html
<!-- Option 1 : Icône + texte -->
<button type="submit">
    <span aria-hidden="true">➤</span>
    Envoyer
</button>

<!-- Option 2 : aria-label -->
<button type="submit" aria-label="Envoyer le formulaire">
    ➤
</button>
```

### Indication de l'état

```html
<!-- Bouton avec état chargement accessible -->
<button type="submit"
        id="submit-btn"
        aria-busy="false">
    Envoyer
</button>

<script>
const btn = document.getElementById('submit-btn');

form.addEventListener('submit', function(e) {
    e.preventDefault();

    // Indiquer le chargement aux lecteurs d'écran
    btn.setAttribute('aria-busy', 'true');
    btn.textContent = 'Envoi en cours...';

    // ... traitement

    // Après envoi
    btn.setAttribute('aria-busy', 'false');
    btn.textContent = 'Envoyer';
});
</script>
```

### Focus visible

Assurez-vous que le focus du bouton est visible :

```css
button:focus {
    outline: 2px solid #3498db;
    outline-offset: 2px;
}

/* Ne jamais faire ça ! */
button:focus {
    outline: none; /* ❌ MAUVAIS pour l'accessibilité */
}
```

---

## Exemples complets

### Exemple 1 : Formulaire avec confirmation

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Formulaire avec confirmation</title>
    <style>
        .form-group {
            margin-bottom: 1rem;
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

        .button-group {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
        }

        button {
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 4px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s;
        }

        .btn-primary {
            background: #3498db;
            color: white;
        }

        .btn-primary:hover {
            background: #2980b9;
        }

        .btn-secondary {
            background: #95a5a6;
            color: white;
        }

        .btn-danger {
            background: #e74c3c;
            color: white;
        }

        button:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
            opacity: 0.6;
        }
    </style>
</head>
<body>
    <h1>Supprimer votre compte</h1>

    <form id="delete-form">
        <p><strong>⚠️ Attention :</strong> Cette action est irréversible.</p>

        <div class="form-group">
            <label for="confirmation">
                Tapez "SUPPRIMER" pour confirmer :
            </label>
            <input type="text"
                   id="confirmation"
                   name="confirmation"
                   autocomplete="off"
                   required>
        </div>

        <div class="form-group">
            <label for="password">
                Mot de passe :
            </label>
            <input type="password"
                   id="password"
                   name="password"
                   required>
        </div>

        <div class="button-group">
            <button type="button"
                    class="btn-secondary"
                    onclick="window.history.back()">
                Annuler
            </button>

            <button type="submit"
                    id="delete-btn"
                    class="btn-danger"
                    disabled>
                Supprimer définitivement mon compte
            </button>
        </div>
    </form>

    <script>
    const form = document.getElementById('delete-form');
    const confirmInput = document.getElementById('confirmation');
    const deleteBtn = document.getElementById('delete-btn');

    // Activer le bouton uniquement si "SUPPRIMER" est tapé
    confirmInput.addEventListener('input', function() {
        deleteBtn.disabled = (this.value !== 'SUPPRIMER');
    });

    // Confirmation supplémentaire à la soumission
    form.addEventListener('submit', function(e) {
        e.preventDefault();

        const confirmed = confirm(
            '⚠️ DERNIÈRE CONFIRMATION\n\n' +
            'Êtes-vous absolument sûr de vouloir supprimer votre compte ?\n' +
            'Cette action est IRRÉVERSIBLE.'
        );

        if (confirmed) {
            // Désactiver le bouton pendant le traitement
            deleteBtn.disabled = true;
            deleteBtn.textContent = '🗑️ Suppression en cours...';

            // Simuler l'envoi
            setTimeout(() => {
                alert('Compte supprimé avec succès');
                // Redirection
                // window.location.href = '/';
            }, 2000);
        }
    });
    </script>
</body>
</html>
```

### Exemple 2 : Formulaire de recherche avec suggestions

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Recherche avec auto-submit</title>
    <style>
        .search-container {
            position: relative;
            max-width: 600px;
            margin: 2rem auto;
        }

        .search-form {
            display: flex;
            gap: 0.5rem;
        }

        .search-input {
            flex: 1;
            padding: 0.75rem 1rem;
            border: 2px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }

        .search-input:focus {
            outline: none;
            border-color: #3498db;
        }

        .search-btn {
            padding: 0.75rem 1.5rem;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
        }

        .search-btn:hover {
            background: #2980b9;
        }

        .loading {
            opacity: 0.6;
            pointer-events: none;
        }

        .results {
            margin-top: 1rem;
            padding: 1rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            background: #f9f9f9;
        }

        .result-item {
            padding: 0.5rem;
            margin-bottom: 0.5rem;
            background: white;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <div class="search-container">
        <h1>Recherche de produits</h1>

        <form id="search-form" class="search-form">
            <input type="search"
                   id="search-input"
                   name="q"
                   class="search-input"
                   placeholder="Rechercher un produit..."
                   autocomplete="off"
                   required>

            <button type="submit" class="search-btn">
                <span class="btn-icon">🔍</span>
                <span class="btn-text">Rechercher</span>
            </button>
        </form>

        <div id="results" class="results" style="display: none;"></div>
    </div>

    <script>
    const form = document.getElementById('search-form');
    const input = document.getElementById('search-input');
    const resultsDiv = document.getElementById('results');
    let searchTimeout;

    // Recherche automatique après 500ms d'inactivité
    input.addEventListener('input', function() {
        clearTimeout(searchTimeout);

        if (this.value.length >= 3) {
            searchTimeout = setTimeout(() => {
                performSearch(this.value);
            }, 500);
        } else {
            resultsDiv.style.display = 'none';
        }
    });

    // Recherche au submit
    form.addEventListener('submit', function(e) {
        e.preventDefault();
        performSearch(input.value);
    });

    function performSearch(query) {
        if (!query) return;

        // Afficher le loading
        form.classList.add('loading');
        resultsDiv.style.display = 'block';
        resultsDiv.innerHTML = '<p>🔄 Recherche en cours...</p>';

        // Simuler une requête API
        setTimeout(() => {
            // Résultats simulés
            const results = [
                `Résultat 1 pour "${query}"`,
                `Résultat 2 pour "${query}"`,
                `Résultat 3 pour "${query}"`
            ];

            displayResults(results);
            form.classList.remove('loading');
        }, 1000);
    }

    function displayResults(results) {
        if (results.length === 0) {
            resultsDiv.innerHTML = '<p>Aucun résultat trouvé</p>';
            return;
        }

        const html = results.map(result =>
            `<div class="result-item">${result}</div>`
        ).join('');

        resultsDiv.innerHTML = `
            <h3>Résultats (${results.length}) :</h3>
            ${html}
        `;
    }
    </script>
</body>
</html>
```

### Exemple 3 : Formulaire multi-étapes

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Formulaire multi-étapes</title>
    <style>
        .wizard {
            max-width: 600px;
            margin: 2rem auto;
            padding: 2rem;
            border: 1px solid #ddd;
            border-radius: 8px;
        }

        .wizard-steps {
            display: flex;
            justify-content: space-between;
            margin-bottom: 2rem;
        }

        .step {
            flex: 1;
            text-align: center;
            padding: 0.5rem;
            position: relative;
        }

        .step::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 100%;
            height: 2px;
            background: #ddd;
            z-index: -1;
        }

        .step:last-child::after {
            display: none;
        }

        .step.active {
            color: #3498db;
            font-weight: bold;
        }

        .step.completed {
            color: #27ae60;
        }

        .wizard-content .step-content {
            display: none;
        }

        .wizard-content .step-content.active {
            display: block;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        input, select {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid #ddd;
            border-radius: 4px;
        }

        .wizard-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 2rem;
        }

        button {
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
        }

        .btn-secondary {
            background: #95a5a6;
            color: white;
        }

        .btn-primary {
            background: #3498db;
            color: white;
        }

        .btn-success {
            background: #27ae60;
            color: white;
        }
    </style>
</head>
<body>
    <div class="wizard">
        <div class="wizard-steps">
            <div class="step active" data-step="1">
                <div>1. Informations</div>
            </div>
            <div class="step" data-step="2">
                <div>2. Adresse</div>
            </div>
            <div class="step" data-step="3">
                <div>3. Confirmation</div>
            </div>
        </div>

        <form id="wizard-form">
            <!-- Étape 1 -->
            <div class="wizard-content">
                <div class="step-content active" data-step="1">
                    <h2>Informations personnelles</h2>

                    <div class="form-group">
                        <label for="prenom">Prénom * :</label>
                        <input type="text" id="prenom" name="prenom" required>
                    </div>

                    <div class="form-group">
                        <label for="nom">Nom * :</label>
                        <input type="text" id="nom" name="nom" required>
                    </div>

                    <div class="form-group">
                        <label for="email">Email * :</label>
                        <input type="email" id="email" name="email" required>
                    </div>
                </div>

                <!-- Étape 2 -->
                <div class="step-content" data-step="2">
                    <h2>Adresse de livraison</h2>

                    <div class="form-group">
                        <label for="adresse">Adresse * :</label>
                        <input type="text" id="adresse" name="adresse" required>
                    </div>

                    <div class="form-group">
                        <label for="ville">Ville * :</label>
                        <input type="text" id="ville" name="ville" required>
                    </div>

                    <div class="form-group">
                        <label for="code_postal">Code postal * :</label>
                        <input type="text"
                               id="code_postal"
                               name="code_postal"
                               pattern="[0-9]{5}"
                               required>
                    </div>
                </div>

                <!-- Étape 3 -->
                <div class="step-content" data-step="3">
                    <h2>Confirmation</h2>
                    <div id="summary"></div>
                </div>
            </div>

            <div class="wizard-buttons">
                <button type="button"
                        id="prev-btn"
                        class="btn-secondary"
                        style="display: none;">
                    ← Précédent
                </button>

                <button type="button"
                        id="next-btn"
                        class="btn-primary">
                    Suivant →
                </button>

                <button type="submit"
                        id="submit-btn"
                        class="btn-success"
                        style="display: none;">
                    ✓ Valider
                </button>
            </div>
        </form>
    </div>

    <script>
    let currentStep = 1;
    const totalSteps = 3;

    const form = document.getElementById('wizard-form');
    const prevBtn = document.getElementById('prev-btn');
    const nextBtn = document.getElementById('next-btn');
    const submitBtn = document.getElementById('submit-btn');

    function showStep(step) {
        // Masquer tous les contenus
        document.querySelectorAll('.step-content').forEach(content => {
            content.classList.remove('active');
        });

        // Afficher le contenu de l'étape
        document.querySelector(`.step-content[data-step="${step}"]`)
            .classList.add('active');

        // Mettre à jour les indicateurs d'étape
        document.querySelectorAll('.wizard-steps .step').forEach((stepEl, index) => {
            stepEl.classList.remove('active', 'completed');
            if (index + 1 < step) {
                stepEl.classList.add('completed');
            } else if (index + 1 === step) {
                stepEl.classList.add('active');
            }
        });

        // Afficher/masquer les boutons
        prevBtn.style.display = step === 1 ? 'none' : 'inline-block';
        nextBtn.style.display = step === totalSteps ? 'none' : 'inline-block';
        submitBtn.style.display = step === totalSteps ? 'inline-block' : 'none';

        // Afficher le résumé à l'étape 3
        if (step === 3) {
            showSummary();
        }
    }

    function validateCurrentStep() {
        const currentContent = document.querySelector(`.step-content[data-step="${currentStep}"]`);
        const inputs = currentContent.querySelectorAll('input[required]');

        let isValid = true;
        inputs.forEach(input => {
            if (!input.checkValidity()) {
                input.reportValidity();
                isValid = false;
            }
        });

        return isValid;
    }

    function showSummary() {
        const formData = new FormData(form);
        const summary = document.getElementById('summary');

        summary.innerHTML = `
            <p><strong>Nom :</strong> ${formData.get('prenom')} ${formData.get('nom')}</p>
            <p><strong>Email :</strong> ${formData.get('email')}</p>
            <p><strong>Adresse :</strong> ${formData.get('adresse')}</p>
            <p><strong>Ville :</strong> ${formData.get('code_postal')} ${formData.get('ville')}</p>
        `;
    }

    nextBtn.addEventListener('click', function() {
        if (validateCurrentStep()) {
            currentStep++;
            showStep(currentStep);
        }
    });

    prevBtn.addEventListener('click', function() {
        currentStep--;
        showStep(currentStep);
    });

    form.addEventListener('submit', function(e) {
        e.preventDefault();

        submitBtn.disabled = true;
        submitBtn.textContent = '⏳ Envoi en cours...';

        // Simuler l'envoi
        setTimeout(() => {
            alert('✅ Formulaire soumis avec succès !');
            submitBtn.disabled = false;
            submitBtn.textContent = '✓ Valider';
        }, 2000);
    });

    // Initialisation
    showStep(1);
    </script>
</body>
</html>
```

---

## Bonnes pratiques

### ✅ À FAIRE

1. **Utiliser `<button type="submit">`**
```html
<!-- ✅ RECOMMANDÉ -->
<button type="submit">Envoyer</button>
```

2. **Toujours spécifier le `type`**
```html
<!-- ✅ BON : type explicite -->
<button type="button" onclick="action()">Action</button>
<button type="submit">Envoyer</button>
```

3. **Texte de bouton clair et explicite**
```html
<!-- ✅ BON : action claire -->
<button type="submit">Créer mon compte</button>

<!-- ❌ VAGUE -->
<button type="submit">OK</button>
```

4. **Désactiver pendant le traitement**
```javascript
// ✅ BON : évite les doubles soumissions
button.disabled = true;
// ... traitement
button.disabled = false;
```

5. **Feedback visuel pour le loading**
```html
<!-- ✅ BON : l'utilisateur sait que ça charge -->
<button type="submit" id="btn">
    <span class="text">Envoyer</span>
    <span class="loader" hidden>⏳</span>
</button>
```

### ❌ À ÉVITER

1. **Oublier le `type` dans un formulaire**
```html
<!-- ❌ MAUVAIS : soumettra le formulaire -->
<button onclick="autreAction()">Cliquez</button>

<!-- ✅ BON -->
<button type="button" onclick="autreAction()">Cliquez</button>
```

2. **Bouton reset trop accessible**
```html
<!-- ❌ RISQUÉ : clic accidentel -->
<button type="submit">Envoyer</button>
<button type="reset">Réinitialiser</button>
```

3. **Plusieurs boutons submit sans distinction**
```html
<!-- ❌ CONFUS : lequel fait quoi ? -->
<button type="submit">Envoyer</button>
<button type="submit">Soumettre</button>

<!-- ✅ CLAIR -->
<button type="submit" name="action" value="draft">Brouillon</button>
<button type="submit" name="action" value="publish">Publier</button>
```

4. **Pas de feedback pendant l'envoi**
```javascript
// ❌ MAUVAIS : utilisateur ne sait pas si ça fonctionne
form.addEventListener('submit', async (e) => {
    e.preventDefault();
    await envoyerDonnees();
});

// ✅ BON : feedback clair
form.addEventListener('submit', async (e) => {
    e.preventDefault();
    button.disabled = true;
    button.textContent = 'Envoi en cours...';
    await envoyerDonnees();
    button.disabled = false;
    button.textContent = 'Envoyer';
});
```

5. **Soumettre avec `form.submit()` sans raison**
```javascript
// ❌ ÉVITER : contourne la validation
form.submit();

// ✅ MIEUX : déclenche la validation
form.requestSubmit();
```

---

## Points clés à retenir

1. **`<button>` est recommandé** sur `<input type="submit">`
2. **Trois types principaux** : `submit`, `reset`, `button`
3. **Toujours spécifier `type`** dans un formulaire
4. **`type="button"` pour actions JavaScript** sans soumission
5. **Événement `submit` sur le formulaire** plutôt que `click` sur le bouton
6. **`preventDefault()` pour traitement JavaScript** sans rechargement
7. **Boutons multiples** : utiliser `name`/`value` ou `data-action`
8. **État désactivé pendant traitement** : évite les doubles soumissions
9. **Feedback visuel** : loading, progression, confirmation
10. **Accessibilité** : texte clair, aria-labels, focus visible

---

## Conclusion de la section Formulaires

Félicitations ! Vous avez maintenant une **maîtrise complète des formulaires HTML5** :

- ✅ Structure et méthodes (GET/POST)
- ✅ Types d'inputs modernes
- ✅ Labels, fieldsets et accessibilité
- ✅ Validation native HTML5
- ✅ Boutons et gestion de soumission

Les formulaires sont au cœur de l'interaction web. Avec ces connaissances, vous pouvez créer des formulaires professionnels, accessibles, sécurisés et offrant une excellente expérience utilisateur.

**Prochaine étape :** Dans la section suivante, nous découvrirons les **tableaux HTML**, qui permettent d'organiser et de présenter des données tabulaires de manière structurée et accessible.

⏭️ [Tableaux](/03-html5-structure-et-semantique/05-tableaux/README.md)
