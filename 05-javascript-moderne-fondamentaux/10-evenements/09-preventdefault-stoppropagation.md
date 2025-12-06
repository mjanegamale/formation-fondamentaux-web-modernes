🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.10.9 - preventDefault() et stopPropagation()

## Introduction

Nous avons vu dans les leçons précédentes que les événements ont :
- Un **comportement par défaut** (ex: un lien navigue vers une URL, un formulaire se soumet)
- Une **propagation** (l'événement remonte dans le DOM)

JavaScript nous donne deux méthodes puissantes pour contrôler ces aspects :
- **`preventDefault()`** : empêche le comportement par défaut
- **`stopPropagation()`** : arrête la propagation

Ces deux méthodes sont **indépendantes** et répondent à des besoins différents. Comprendre quand utiliser l'une ou l'autre est essentiel.

## preventDefault() - Empêcher le comportement par défaut

### Qu'est-ce que le comportement par défaut ?

Certains éléments HTML ont des **actions automatiques** déclenchées par les événements :

| Élément | Événement | Comportement par défaut |
|---------|-----------|------------------------|
| `<a href>` | click | Naviguer vers l'URL |
| `<form>` | submit | Soumettre et recharger la page |
| `<input type="checkbox">` | click | Cocher/décocher la case |
| `<select>` | change | Changer la valeur |
| Clic droit | contextmenu | Afficher le menu contextuel |
| Texte sélectionné | copy | Copier dans le presse-papier |

### Syntaxe

```javascript
element.addEventListener('event', (event) => {
    event.preventDefault();
});
```

### Exemple 1 : Empêcher la navigation d'un lien

```html
<a href="https://www.example.com" id="lien">Cliquez-moi</a>
```

```javascript
const lien = document.getElementById('lien');

lien.addEventListener('click', (event) => {
    event.preventDefault(); // Empêche la navigation
    console.log('Lien cliqué, mais pas de navigation !');
});
```

**Résultat** : Le lien ne mène plus nulle part. Le comportement par défaut (navigation) est bloqué.

### Exemple 2 : Empêcher la soumission d'un formulaire

C'est l'usage le plus courant de `preventDefault()` :

```html
<form id="monFormulaire">
    <input type="text" name="nom" placeholder="Nom" required>
    <input type="email" name="email" placeholder="Email" required>
    <button type="submit">Envoyer</button>
</form>
<p id="resultat"></p>
```

```javascript
const formulaire = document.getElementById('monFormulaire');
const resultat = document.getElementById('resultat');

formulaire.addEventListener('submit', (event) => {
    event.preventDefault(); // ⚠️ CRUCIAL : Empêche le rechargement de la page

    // Récupérer les valeurs
    const nom = event.target.nom.value;
    const email = event.target.email.value;

    // Validation personnalisée
    if (nom.length < 3) {
        resultat.textContent = 'Le nom doit contenir au moins 3 caractères';
        resultat.style.color = 'red';
        return;
    }

    // Si tout est OK
    resultat.textContent = `Formulaire soumis pour ${nom} (${email})`;
    resultat.style.color = 'green';

    // Ici, vous pourriez envoyer les données avec fetch()
});
```

**Sans `preventDefault()`** : La page se rechargerait et vous perdriez toutes vos données.

### Exemple 3 : Empêcher le menu contextuel (clic droit)

```html
<div id="zone" style="width: 300px; height: 200px; background: lightblue;">
    Essayez de faire un clic droit ici
</div>
```

```javascript
const zone = document.getElementById('zone');

zone.addEventListener('contextmenu', (event) => {
    event.preventDefault();
    console.log('Menu contextuel bloqué !');

    // Vous pourriez afficher votre propre menu personnalisé
    alert('Menu personnalisé au lieu du menu du navigateur');
});
```

### Exemple 4 : Empêcher la copie de texte

```html
<p id="texteProtege">Ce texte ne peut pas être copié (essayez Ctrl+C)</p>
```

```javascript
const texte = document.getElementById('texteProtege');

texte.addEventListener('copy', (event) => {
    event.preventDefault();
    alert('La copie est désactivée sur ce texte !');
});
```

### Exemple 5 : Empêcher le comportement de la touche Espace

```html
<button id="bouton">Appuyez sur Espace</button>
```

```javascript
const bouton = document.getElementById('bouton');

bouton.addEventListener('keydown', (event) => {
    if (event.key === ' ') {
        event.preventDefault(); // Empêche le défilement de la page
        console.log('Espace détectée, mais pas de scroll !');
    }
});
```

### Exemple 6 : Lien qui ouvre une modal au lieu de naviguer

```html
<a href="details.html" id="lienModal">Voir les détails</a>

<div id="modal" style="display: none; position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: white; padding: 20px; box-shadow: 0 0 10px rgba(0,0,0,0.5);">
    <h2>Détails</h2>
    <p>Contenu de la modal</p>
    <button id="fermerModal">Fermer</button>
</div>
<div id="overlay" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5);"></div>
```

```javascript
const lienModal = document.getElementById('lienModal');
const modal = document.getElementById('modal');
const overlay = document.getElementById('overlay');
const fermerModal = document.getElementById('fermerModal');

lienModal.addEventListener('click', (event) => {
    event.preventDefault(); // Ne pas naviguer vers details.html

    // Afficher la modal à la place
    modal.style.display = 'block';
    overlay.style.display = 'block';
});

fermerModal.addEventListener('click', () => {
    modal.style.display = 'none';
    overlay.style.display = 'none';
});

overlay.addEventListener('click', () => {
    modal.style.display = 'none';
    overlay.style.display = 'none';
});
```

## stopPropagation() - Arrêter la propagation

### À quoi ça sert ?

`stopPropagation()` **arrête la propagation** de l'événement dans le DOM. L'événement ne remonte pas (bubbling) ou ne descend pas (capturing) aux éléments parents ou enfants.

### Syntaxe

```javascript
element.addEventListener('event', (event) => {
    event.stopPropagation();
});
```

### Rappel : La propagation

Sans `stopPropagation()`, un événement remonte :

```html
<div id="parent" style="padding: 30px; background: lightblue;">
    PARENT
    <button id="enfant">ENFANT</button>
</div>
```

```javascript
const parent = document.getElementById('parent');
const enfant = document.getElementById('enfant');

parent.addEventListener('click', () => {
    console.log('Parent cliqué');
});

enfant.addEventListener('click', () => {
    console.log('Enfant cliqué');
});

// Clic sur ENFANT affiche :
// "Enfant cliqué"
// "Parent cliqué"  ← L'événement a remonté !
```

### Avec stopPropagation()

```javascript
const parent = document.getElementById('parent');
const enfant = document.getElementById('enfant');

parent.addEventListener('click', () => {
    console.log('Parent cliqué');
});

enfant.addEventListener('click', (event) => {
    event.stopPropagation(); // Arrêter la remontée
    console.log('Enfant cliqué');
});

// Clic sur ENFANT affiche SEULEMENT :
// "Enfant cliqué"
// (L'événement ne remonte pas au parent)
```

### Exemple 1 : Modal qui ne se ferme pas au clic interne

```html
<div id="overlay" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7);">
    <div id="modal" style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); background: white; padding: 30px; border-radius: 8px;">
        <h2>Ma Modal</h2>
        <p>Ceci est le contenu de la modal</p>
        <button id="action">Action</button>
    </div>
</div>
```

```javascript
const overlay = document.getElementById('overlay');
const modal = document.getElementById('modal');

// Fermer la modal au clic sur l'overlay
overlay.addEventListener('click', () => {
    overlay.style.display = 'none';
    console.log('Modal fermée');
});

// Empêcher la fermeture au clic sur la modal elle-même
modal.addEventListener('click', (event) => {
    event.stopPropagation(); // Le clic ne remonte pas à overlay
    console.log('Clic sur la modal (ne ferme pas)');
});
```

**Pourquoi c'est important ?** Sans `stopPropagation()`, cliquer n'importe où dans la modal (même sur le texte ou le bouton) fermerait la modal car l'événement remonterait à l'overlay.

### Exemple 2 : Bouton dans une carte cliquable

```html
<div class="carte" id="carte1" data-id="1" style="padding: 20px; border: 1px solid #ddd; cursor: pointer;">
    <h3>Produit 1</h3>
    <p>Description du produit</p>
    <button class="ajouter-panier">Ajouter au panier</button>
</div>
```

```javascript
const carte = document.getElementById('carte1');
const bouton = carte.querySelector('.ajouter-panier');

// Clic sur la carte entière : ouvrir les détails
carte.addEventListener('click', () => {
    console.log('Ouvrir les détails du produit');
    window.location.href = '/produit/1';
});

// Clic sur le bouton : ajouter au panier SANS ouvrir les détails
bouton.addEventListener('click', (event) => {
    event.stopPropagation(); // Ne pas déclencher le clic de la carte
    console.log('Produit ajouté au panier');
    alert('Produit ajouté au panier !');
});
```

### Exemple 3 : Menu déroulant

```html
<div id="dropdown">
    <button id="btnMenu">Menu ▼</button>
    <ul id="liste" style="display: none; position: absolute; background: white; border: 1px solid #ddd; list-style: none; padding: 10px;">
        <li><a href="#option1">Option 1</a></li>
        <li><a href="#option2">Option 2</a></li>
        <li><a href="#option3">Option 3</a></li>
    </ul>
</div>
```

```javascript
const btnMenu = document.getElementById('btnMenu');
const liste = document.getElementById('liste');
const dropdown = document.getElementById('dropdown');

// Ouvrir le menu
btnMenu.addEventListener('click', (event) => {
    event.stopPropagation(); // Empêcher la fermeture immédiate
    liste.style.display = liste.style.display === 'none' ? 'block' : 'none';
});

// Empêcher la fermeture au clic dans le menu
dropdown.addEventListener('click', (event) => {
    event.stopPropagation();
});

// Fermer le menu au clic ailleurs dans le document
document.addEventListener('click', () => {
    liste.style.display = 'none';
});
```

### Exemple 4 : Liste de tâches avec bouton supprimer

```html
<ul id="listeTaches">
    <li class="tache">
        <span class="texte">Tâche 1</span>
        <button class="supprimer">✕</button>
    </li>
    <li class="tache">
        <span class="texte">Tâche 2</span>
        <button class="supprimer">✕</button>
    </li>
</ul>
```

```javascript
const liste = document.getElementById('listeTaches');

liste.addEventListener('click', (event) => {
    const tache = event.target.closest('.tache');
    if (!tache) return;

    // Supprimer la tâche
    if (event.target.classList.contains('supprimer')) {
        event.stopPropagation(); // Ne pas basculer "terminée"
        tache.remove();
        return;
    }

    // Basculer terminée/non terminée
    if (event.target.classList.contains('texte')) {
        const texte = event.target;
        texte.style.textDecoration =
            texte.style.textDecoration === 'line-through' ? 'none' : 'line-through';
    }
});
```

## Différence entre preventDefault() et stopPropagation()

### Résumé visuel

```
preventDefault()
┌─────────────────────────────────────┐
│ Empêche le comportement par défaut  │
│ - Lien : pas de navigation          │
│ - Formulaire : pas de soumission    │
│ - Checkbox : pas de changement      │
└─────────────────────────────────────┘

stopPropagation()
┌─────────────────────────────────────┐
│ Arrête la propagation dans le DOM   │
│ - L'événement ne remonte pas        │
│ - Les parents ne sont pas notifiés  │
└─────────────────────────────────────┘
```

### Tableau comparatif

| Critère | preventDefault() | stopPropagation() |
|---------|------------------|-------------------|
| **Objectif** | Empêcher l'action par défaut | Arrêter la propagation |
| **Affecte** | Le comportement de l'élément | Les éléments parents/enfants |
| **Exemples** | Ne pas soumettre un formulaire | Ne pas fermer une modal |
| **Impact sur propagation** | Aucun (événement remonte toujours) | Arrêt complet de la remontée |
| **Impact sur action par défaut** | Bloque l'action | Aucun (action se produit) |
| **Usage fréquent** | Très fréquent | Modéré |

### Exemple montrant la différence

```html
<div id="parent" style="padding: 30px; background: lightblue;">
    PARENT
    <a href="https://www.example.com" id="lien">Lien</a>
</div>
```

#### Scénario 1 : preventDefault() seul

```javascript
const parent = document.getElementById('parent');
const lien = document.getElementById('lien');

parent.addEventListener('click', () => {
    console.log('Parent cliqué');
});

lien.addEventListener('click', (event) => {
    event.preventDefault(); // Empêche la navigation
    console.log('Lien cliqué');
});

// Résultat du clic sur le lien :
// "Lien cliqué"
// "Parent cliqué"  ← L'événement remonte toujours !
// Mais pas de navigation vers example.com
```

#### Scénario 2 : stopPropagation() seul

```javascript
parent.addEventListener('click', () => {
    console.log('Parent cliqué');
});

lien.addEventListener('click', (event) => {
    event.stopPropagation(); // Arrête la propagation
    console.log('Lien cliqué');
});

// Résultat du clic sur le lien :
// "Lien cliqué"
// Pas "Parent cliqué" ← L'événement ne remonte pas
// MAIS navigation vers example.com (action par défaut)
```

#### Scénario 3 : Les deux ensemble

```javascript
parent.addEventListener('click', () => {
    console.log('Parent cliqué');
});

lien.addEventListener('click', (event) => {
    event.preventDefault();     // Empêche la navigation
    event.stopPropagation();    // Arrête la propagation
    console.log('Lien cliqué');
});

// Résultat du clic sur le lien :
// "Lien cliqué" seulement
// Pas de navigation ET pas de propagation
```

## Cas d'usage combinés

### Exemple 1 : Formulaire dans une modal

```html
<div id="modalFormulaire" style="position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: white; padding: 20px;">
    <h2>Inscription</h2>
    <form id="formInscription">
        <input type="text" name="nom" placeholder="Nom" required>
        <input type="email" name="email" placeholder="Email" required>
        <button type="submit">S'inscrire</button>
    </form>
</div>
<div id="overlayFormulaire" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5);"></div>
```

```javascript
const modal = document.getElementById('modalFormulaire');
const overlay = document.getElementById('overlayFormulaire');
const form = document.getElementById('formInscription');

// Empêcher la fermeture au clic dans la modal
modal.addEventListener('click', (event) => {
    event.stopPropagation(); // Ne pas fermer
});

// Fermer au clic sur l'overlay
overlay.addEventListener('click', () => {
    modal.style.display = 'none';
    overlay.style.display = 'none';
});

// Gérer la soumission du formulaire
form.addEventListener('submit', (event) => {
    event.preventDefault(); // Ne pas recharger la page

    const nom = event.target.nom.value;
    const email = event.target.email.value;

    console.log('Inscription :', nom, email);

    // Fermer la modal après soumission
    modal.style.display = 'none';
    overlay.style.display = 'none';

    alert(`Inscription réussie pour ${nom} !`);
});
```

### Exemple 2 : Galerie d'images avec liens

```html
<div class="galerie">
    <div class="image-conteneur">
        <img src="photo1.jpg" alt="Photo 1">
        <a href="photo1-full.jpg" class="lien-zoom" target="_blank">🔍 Zoom</a>
        <button class="btn-favoris">❤️ Favoris</button>
    </div>
</div>
```

```javascript
const conteneur = document.querySelector('.image-conteneur');
const lienZoom = conteneur.querySelector('.lien-zoom');
const btnFavoris = conteneur.querySelector('.btn-favoris');

// Clic sur le conteneur : afficher les détails
conteneur.addEventListener('click', () => {
    console.log('Afficher les détails de l\'image');
});

// Clic sur le lien zoom : ouvrir en grand
lienZoom.addEventListener('click', (event) => {
    event.stopPropagation(); // Ne pas afficher les détails
    // Le lien s'ouvre normalement (pas de preventDefault)
    console.log('Ouverture du zoom');
});

// Clic sur favoris : ajouter aux favoris
btnFavoris.addEventListener('click', (event) => {
    event.stopPropagation(); // Ne pas afficher les détails
    console.log('Ajouté aux favoris');
    btnFavoris.textContent = '💚 Ajouté';
});
```

### Exemple 3 : Drag and drop avec formulaire

```html
<div id="zone-drop" style="width: 300px; height: 200px; border: 2px dashed #ccc; padding: 20px;">
    <p>Glissez un fichier ici</p>
    <form id="formUpload">
        <input type="file" name="fichier">
        <button type="submit">Envoyer</button>
    </form>
</div>
```

```javascript
const zone = document.getElementById('zone-drop');
const form = document.getElementById('formUpload');

// Empêcher le comportement par défaut du drag and drop
zone.addEventListener('dragover', (event) => {
    event.preventDefault(); // Permettre le drop
    zone.style.background = '#e0e0e0';
});

zone.addEventListener('dragleave', () => {
    zone.style.background = '';
});

zone.addEventListener('drop', (event) => {
    event.preventDefault(); // Empêcher l'ouverture du fichier
    event.stopPropagation(); // Empêcher d'autres handlers

    zone.style.background = '';

    const fichiers = event.dataTransfer.files;
    console.log('Fichiers déposés :', fichiers.length);
});

// Soumission du formulaire
form.addEventListener('submit', (event) => {
    event.preventDefault(); // Ne pas recharger la page
    event.stopPropagation(); // Ne pas déclencher d'autres événements

    const fichier = event.target.fichier.files[0];
    if (fichier) {
        console.log('Fichier sélectionné :', fichier.name);
        // Envoyer avec fetch()
    }
});
```

## Pièges courants et erreurs à éviter

### Piège 1 : Oublier preventDefault() sur les formulaires

```javascript
// ❌ ERREUR : La page va se recharger
form.addEventListener('submit', () => {
    console.log('Soumission...');
    // Traitement...
});

// ✅ CORRECT
form.addEventListener('submit', (event) => {
    event.preventDefault(); // Empêcher le rechargement
    console.log('Soumission...');
    // Traitement...
});
```

### Piège 2 : Utiliser stopPropagation() par défaut

```javascript
// ❌ MAUVAISE HABITUDE
element.addEventListener('click', (event) => {
    event.stopPropagation(); // Pourquoi ? Peut casser d'autres fonctionnalités
    // Code...
});

// ✅ UTILISER SEULEMENT SI NÉCESSAIRE
element.addEventListener('click', (event) => {
    // Arrêter seulement si vous avez une bonne raison
    if (raisonValide) {
        event.stopPropagation();
    }
    // Code...
});
```

### Piège 3 : Confondre les deux méthodes

```javascript
// ❌ ERREUR : Vouloir empêcher la navigation mais utiliser stopPropagation
lien.addEventListener('click', (event) => {
    event.stopPropagation(); // N'empêche PAS la navigation !
});

// ✅ CORRECT : Utiliser preventDefault pour empêcher la navigation
lien.addEventListener('click', (event) => {
    event.preventDefault(); // Empêche la navigation
});
```

### Piège 4 : Bloquer tous les comportements par défaut

```javascript
// ❌ TROP RADICAL
document.addEventListener('click', (event) => {
    event.preventDefault(); // Bloque TOUS les clics !
});

// ✅ ÊTRE SPÉCIFIQUE
document.querySelectorAll('.lien-special').forEach(lien => {
    lien.addEventListener('click', (event) => {
        event.preventDefault(); // Seulement pour certains liens
    });
});
```

## Vérifier si le comportement par défaut a été empêché

Vous pouvez vérifier si `preventDefault()` a été appelé avec `event.defaultPrevented` :

```javascript
element.addEventListener('click', (event) => {
    if (event.defaultPrevented) {
        console.log('Le comportement par défaut a déjà été empêché');
        return; // Ne rien faire
    }

    // Votre logique...
});
```

## Bonnes pratiques

### ✅ 1. Toujours preventDefault() sur les formulaires

```javascript
// ✅ SYSTÉMATIQUE pour les formulaires
form.addEventListener('submit', (event) => {
    event.preventDefault();
    // Validation et traitement
});
```

### ✅ 2. Utiliser stopPropagation() avec parcimonie

```javascript
// ✅ BON USAGE : Cas d'usage clair et documenté
modal.addEventListener('click', (event) => {
    // Empêcher la fermeture de la modal au clic interne
    event.stopPropagation();
});

// ⚠️ À ÉVITER : Usage sans raison claire
element.addEventListener('click', (event) => {
    event.stopPropagation(); // Pourquoi ?
});
```

### ✅ 3. Documenter l'usage de ces méthodes

```javascript
// ✅ BIEN DOCUMENTÉ
lien.addEventListener('click', (event) => {
    // Empêcher la navigation : on affiche une modal à la place
    event.preventDefault();
    afficherModal();
});
```

### ✅ 4. Préférer la délégation à stopPropagation()

```javascript
// ⚠️ UTILISE stopPropagation
bouton.addEventListener('click', (event) => {
    event.stopPropagation();
    // Code...
});

// ✅ MEILLEUR : Délégation avec vérification
parent.addEventListener('click', (event) => {
    if (event.target.matches('.bouton')) {
        // Code...
        // Pas besoin de stopPropagation
    }
});
```

### ✅ 5. Tester les deux comportements

Avant d'ajouter `preventDefault()` ou `stopPropagation()`, testez pour voir si c'est vraiment nécessaire :

```javascript
element.addEventListener('click', (event) => {
    console.log('Avec comportement par défaut');
    // Testez d'abord

    // Ajoutez seulement si nécessaire :
    // event.preventDefault();
    // event.stopPropagation();
});
```

## Résumé visuel

```
┌─────────────────────────────────────────────────────────┐
│                    ÉVÉNEMENT CLICK                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Sans méthodes :                                        │
│  ✓ Comportement par défaut se produit                   │
│  ✓ Événement remonte aux parents                        │
│                                                         │
│  event.preventDefault() :                               │
│  ✗ Comportement par défaut bloqué                       │
│  ✓ Événement remonte toujours                           │
│                                                         │
│  event.stopPropagation() :                              │
│  ✓ Comportement par défaut se produit                   │
│  ✗ Événement ne remonte PAS                             │
│                                                         │
│  Les deux ensemble :                                    │
│  ✗ Comportement par défaut bloqué                       │
│  ✗ Événement ne remonte PAS                             │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Ce qu'il faut retenir

✅ **preventDefault()** empêche le **comportement par défaut** de l'élément

✅ **stopPropagation()** arrête la **propagation** de l'événement dans le DOM

✅ **Les deux sont indépendants** : vous pouvez utiliser l'un sans l'autre

✅ **preventDefault()** est très utilisé (formulaires, liens)

✅ **stopPropagation()** doit être utilisé avec parcimonie

✅ **Toujours** utiliser preventDefault() sur les formulaires en JavaScript moderne

✅ **Documenter** pourquoi vous utilisez ces méthodes

✅ **event.defaultPrevented** permet de vérifier si preventDefault() a été appelé

## Dans la prochaine leçon

Maintenant que vous maîtrisez preventDefault() et stopPropagation(), nous allons voir la **délégation d'événements** en profondeur.

Vous découvrirez :
- Comment gérer efficacement de nombreux éléments
- Les avantages de performance
- Les techniques avancées de délégation
- Des cas d'usage pratiques

---


⏭️ [Délégation d'événements](/05-javascript-moderne-fondamentaux/10-evenements/10-delegation-evenements.md)
