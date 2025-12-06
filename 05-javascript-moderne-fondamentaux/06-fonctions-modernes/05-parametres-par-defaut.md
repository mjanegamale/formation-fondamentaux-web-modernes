🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.6.5 - Paramètres par défaut (ES6) 🆕

## Introduction

Les **paramètres par défaut** sont une fonctionnalité moderne d'ES6 qui permet d'assigner des valeurs par défaut aux paramètres de fonction. Si un argument n'est pas fourni (ou vaut `undefined`), la valeur par défaut est utilisée automatiquement.

Cette fonctionnalité rend votre code plus propre, plus lisible et plus robuste.

## Le problème avant ES6

Avant ES6, si un paramètre n'était pas fourni, il valait `undefined`, ce qui pouvait causer des problèmes.

### Exemple du problème

```javascript
function saluer(prenom) {
  console.log("Bonjour " + prenom);
}

saluer("Alice");  // Affiche : "Bonjour Alice"
saluer();         // Affiche : "Bonjour undefined" ❌
```

### Solution avant ES6 (ancienne méthode)

Il fallait vérifier manuellement et assigner une valeur par défaut :

```javascript
function saluer(prenom) {
  // Méthode 1 : avec if
  if (prenom === undefined) {
    prenom = "Invité";
  }
  console.log("Bonjour " + prenom);
}

// Méthode 2 : avec l'opérateur ||
function saluer(prenom) {
  prenom = prenom || "Invité";
  console.log("Bonjour " + prenom);
}

saluer("Alice");  // Affiche : "Bonjour Alice"
saluer();         // Affiche : "Bonjour Invité" ✅
```

**Problème :** C'est verbeux et répétitif, surtout avec plusieurs paramètres.

## Solution ES6 : Paramètres par défaut 🆕

Avec ES6, vous pouvez définir des valeurs par défaut **directement dans la signature de la fonction** :

### Syntaxe

```javascript
function nomFonction(parametre = valeurParDefaut) {
  // Code
}
```

### Exemple simple

```javascript
function saluer(prenom = "Invité") {
  console.log("Bonjour " + prenom);
}

saluer("Alice");  // Affiche : "Bonjour Alice"
saluer();         // Affiche : "Bonjour Invité" ✅
```

**C'est tout !** Beaucoup plus simple et lisible.

## Syntaxe avec arrow functions

Les paramètres par défaut fonctionnent aussi avec les arrow functions :

```javascript
const saluer = (prenom = "Invité") => {
  console.log("Bonjour " + prenom);
};

// Ou en version ultra-concise
const saluer = (prenom = "Invité") => console.log("Bonjour " + prenom);
```

## Plusieurs paramètres avec valeurs par défaut

Vous pouvez définir des valeurs par défaut pour plusieurs paramètres :

```javascript
function creerUtilisateur(nom = "Anonyme", age = 18, ville = "Paris") {
  console.log(nom + ", " + age + " ans, habite à " + ville);
}

creerUtilisateur();                          // "Anonyme, 18 ans, habite à Paris"
creerUtilisateur("Alice");                   // "Alice, 18 ans, habite à Paris"
creerUtilisateur("Alice", 25);               // "Alice, 25 ans, habite à Paris"
creerUtilisateur("Alice", 25, "Lyon");       // "Alice, 25 ans, habite à Lyon"
```

## Mélanger paramètres obligatoires et optionnels

Vous pouvez avoir des paramètres **sans** valeur par défaut (obligatoires) et des paramètres **avec** valeur par défaut (optionnels) :

```javascript
function reservation(nom, nombrePersonnes = 2, heure = "19h00") {
  console.log("Réservation pour " + nom);
  console.log("Nombre de personnes : " + nombrePersonnes);
  console.log("Heure : " + heure);
}

reservation("Dupont");
// Réservation pour Dupont
// Nombre de personnes : 2
// Heure : 19h00

reservation("Martin", 4);
// Réservation pour Martin
// Nombre de personnes : 4
// Heure : 19h00

reservation("Leroy", 6, "20h30");
// Réservation pour Leroy
// Nombre de personnes : 6
// Heure : 20h30
```

**Bonne pratique :** Placez les paramètres obligatoires **en premier**, les optionnels **après**.

## undefined vs null : différence importante

### undefined déclenche la valeur par défaut

```javascript
function afficher(message = "Message par défaut") {
  console.log(message);
}

afficher(undefined);  // Affiche : "Message par défaut"
```

### null ne déclenche PAS la valeur par défaut

```javascript
function afficher(message = "Message par défaut") {
  console.log(message);
}

afficher(null);  // Affiche : "null"
```

**Explication :** `undefined` signifie "pas de valeur fournie", tandis que `null` est considéré comme une valeur fournie (qui est `null`).

### Autres valeurs "falsy" ne déclenchent pas non plus

```javascript
function compter(nombre = 10) {
  console.log("Nombre : " + nombre);
}

compter(0);      // Affiche : "Nombre : 0" (pas la valeur par défaut)
compter("");     // Affiche : "Nombre : " (pas la valeur par défaut)
compter(false);  // Affiche : "Nombre : false" (pas la valeur par défaut)
```

**Important :** Seul `undefined` (ou l'absence d'argument) déclenche la valeur par défaut.

## Valeurs par défaut calculées

Les valeurs par défaut peuvent être des **expressions** ou des **appels de fonction** :

### Expression simple

```javascript
function calculerPrix(prix, taxe = prix * 0.2) {
  return prix + taxe;
}

console.log(calculerPrix(100));      // 120 (taxe = 100 * 0.2 = 20)
console.log(calculerPrix(100, 15));  // 115 (taxe fournie = 15)
```

### Appel de fonction

```javascript
function obtenirDateActuelle() {
  return new Date().toLocaleDateString();
}

function enregistrerLog(message, date = obtenirDateActuelle()) {
  console.log("[" + date + "] " + message);
}

enregistrerLog("Connexion réussie");
// Affiche : [05/12/2025] Connexion réussie

enregistrerLog("Déconnexion", "01/12/2025");
// Affiche : [01/12/2025] Déconnexion
```

**Important :** La fonction est **appelée uniquement** si le paramètre n'est pas fourni.

### Expression avec autre paramètre

Un paramètre par défaut peut utiliser la valeur d'un paramètre précédent :

```javascript
function creerMessage(nom, salutation = "Bonjour " + nom) {
  console.log(salutation);
}

creerMessage("Alice");                    // Affiche : "Bonjour Alice"
creerMessage("Bob", "Salut Bob !");       // Affiche : "Salut Bob !"
```

**⚠️ Limitation :** Vous ne pouvez utiliser que les paramètres **précédents** (déclarés avant) :

```javascript
// ❌ Ne fonctionne pas
function exemple(a = b, b = 5) {  // b n'est pas encore défini !
  console.log(a, b);
}

// ✅ Fonctionne
function exemple(b = 5, a = b) {  // b est défini avant a
  console.log(a, b);
}
```

## Exemples pratiques complets

### Exemple 1 : Calculateur de TVA

```javascript
const calculerPrixTTC = (prixHT, tauxTVA = 20) => {
  const montantTVA = prixHT * (tauxTVA / 100);
  return prixHT + montantTVA;
};

console.log(calculerPrixTTC(100));      // 120€ (TVA 20% par défaut)
console.log(calculerPrixTTC(100, 5.5)); // 105.5€ (TVA 5.5%)
console.log(calculerPrixTTC(50));       // 60€ (TVA 20% par défaut)
```

### Exemple 2 : Création de profil utilisateur

```javascript
function creerProfil(pseudo, role = "utilisateur", actif = true) {
  return {
    pseudo: pseudo,
    role: role,
    actif: actif,
    dateCreation: new Date()
  };
}

const user1 = creerProfil("Alice");
console.log(user1);
// { pseudo: "Alice", role: "utilisateur", actif: true, dateCreation: ... }

const user2 = creerProfil("Bob", "admin");
console.log(user2);
// { pseudo: "Bob", role: "admin", actif: true, dateCreation: ... }

const user3 = creerProfil("Charlie", "moderateur", false);
console.log(user3);
// { pseudo: "Charlie", role: "moderateur", actif: false, dateCreation: ... }
```

### Exemple 3 : Formateur de message

```javascript
const creerNotification = (
  texte,
  type = "info",
  duree = 3000,
  son = true
) => {
  return {
    message: texte,
    type: type,
    afficherPendant: duree + "ms",
    jouerSon: son
  };
};

console.log(creerNotification("Sauvegarde réussie"));
// { message: "Sauvegarde réussie", type: "info", afficherPendant: "3000ms", jouerSon: true }

console.log(creerNotification("Erreur détectée", "error", 5000));
// { message: "Erreur détectée", type: "error", afficherPendant: "5000ms", jouerSon: true }

console.log(creerNotification("Mise à jour", "success", 2000, false));
// { message: "Mise à jour", type: "success", afficherPendant: "2000ms", jouerSon: false }
```

### Exemple 4 : Fonction de recherche

```javascript
function rechercher(
  termes,
  sensibleCasse = false,
  motComplet = false,
  limite = 10
) {
  console.log("Recherche :", termes);
  console.log("Sensible à la casse :", sensibleCasse);
  console.log("Mot complet uniquement :", motComplet);
  console.log("Nombre de résultats max :", limite);
}

rechercher("JavaScript");
// Recherche : JavaScript
// Sensible à la casse : false
// Mot complet uniquement : false
// Nombre de résultats max : 10

rechercher("React", true, true, 20);
// Recherche : React
// Sensible à la casse : true
// Mot complet uniquement : true
// Nombre de résultats max : 20
```

### Exemple 5 : Configuration de requête HTTP

```javascript
const faireFetch = (
  url,
  methode = "GET",
  headers = { "Content-Type": "application/json" },
  timeout = 5000
) => {
  console.log("URL :", url);
  console.log("Méthode :", methode);
  console.log("Headers :", headers);
  console.log("Timeout :", timeout + "ms");
  // Ici irait le code de la vraie requête
};

faireFetch("https://api.example.com/users");
// URL : https://api.example.com/users
// Méthode : GET
// Headers : { "Content-Type": "application/json" }
// Timeout : 5000ms

faireFetch("https://api.example.com/users", "POST");
// URL : https://api.example.com/users
// Méthode : POST
// Headers : { "Content-Type": "application/json" }
// Timeout : 5000ms
```

## Combiner avec la déstructuration

Les paramètres par défaut fonctionnent très bien avec la déstructuration d'objets (concept avancé que vous verrez plus tard) :

```javascript
function creerCarte({
  titre = "Sans titre",
  description = "Pas de description",
  couleur = "bleu"
} = {}) {
  console.log("Titre :", titre);
  console.log("Description :", description);
  console.log("Couleur :", couleur);
}

creerCarte({ titre: "Ma carte" });
// Titre : Ma carte
// Description : Pas de description
// Couleur : bleu

creerCarte({});
// Titre : Sans titre
// Description : Pas de description
// Couleur : bleu

creerCarte();  // Notez le = {} après la déstructuration
// Titre : Sans titre
// Description : Pas de description
// Couleur : bleu
```

Le `= {}` après les accolades permet d'appeler la fonction sans argument du tout.

## Passer undefined explicitement

Vous pouvez passer `undefined` explicitement pour "sauter" un paramètre et utiliser sa valeur par défaut :

```javascript
function commander(plat, boisson = "eau", dessert = "fruit") {
  console.log("Plat :", plat);
  console.log("Boisson :", boisson);
  console.log("Dessert :", dessert);
}

// Je veux le plat et le dessert, mais pas la boisson par défaut
commander("Pizza", undefined, "Glace");
// Plat : Pizza
// Boisson : eau (valeur par défaut)
// Dessert : Glace
```

**Astuce :** C'est utile quand vous voulez utiliser la valeur par défaut d'un paramètre du milieu.

## Comparaison avec l'ancienne méthode

### Avant ES6 (verbeux)

```javascript
function creerLien(texte, url, target, classe) {
  texte = texte || "Cliquez ici";
  url = url || "#";
  target = target || "_self";
  classe = classe || "lien";

  return '<a href="' + url + '" target="' + target + '" class="' + classe + '">' +
         texte + '</a>';
}
```

**Problèmes :**
- Beaucoup de code répétitif
- Ne fonctionne pas bien avec les valeurs "falsy" (0, "", false)
- Moins lisible

### Avec ES6 (propre)

```javascript
function creerLien(
  texte = "Cliquez ici",
  url = "#",
  target = "_self",
  classe = "lien"
) {
  return '<a href="' + url + '" target="' + target + '" class="' + classe + '">' +
         texte + '</a>';
}
```

**Avantages :**
- ✅ Plus concis et lisible
- ✅ Gère correctement `undefined`
- ✅ Valeurs par défaut visibles dans la signature
- ✅ Permet les valeurs "falsy" comme arguments réels

## Quand utiliser les paramètres par défaut ?

### ✅ Utilisez-les pour :

- **Valeurs communes** : quand un paramètre a souvent la même valeur
- **Configuration** : options avec des valeurs sensées par défaut
- **Rétrocompatibilité** : ajouter des paramètres sans casser le code existant
- **Simplifier les appels** : réduire le nombre d'arguments à passer

### Exemples de bons cas d'usage

```javascript
// Configuration d'animation
function animer(element, duree = 300, easing = "ease-in-out") { }

// Pagination
function afficherPage(page = 1, elementsParPage = 20) { }

// Formatage
function formaterDate(date, format = "DD/MM/YYYY", locale = "fr-FR") { }

// Timeout
function attendre(ms = 1000) { }
```

## Bonnes pratiques

### 1. Valeurs par défaut significatives

```javascript
// ❌ Valeur par défaut arbitraire
function creerUtilisateur(nom, age = 0) {  // 0 n'a pas de sens pour un âge
  // ...
}

// ✅ Valeur par défaut logique ou null/undefined
function creerUtilisateur(nom, age = null) {  // null indique "non renseigné"
  // ...
}
```

### 2. Ordre des paramètres

```javascript
// ❌ Paramètres obligatoires après les optionnels
function maFonction(x = 10, y) {  // Difficile à utiliser !
  // ...
}

// ✅ Obligatoires d'abord, optionnels après
function maFonction(y, x = 10) {
  // ...
}
```

### 3. Documentation claire

```javascript
/**
 * Crée une carte de produit
 * @param {string} nom - Nom du produit (obligatoire)
 * @param {number} prix - Prix en euros (obligatoire)
 * @param {boolean} enStock - Disponibilité (défaut: true)
 * @param {string} image - URL de l'image (défaut: "placeholder.jpg")
 */
function creerCarte(nom, prix, enStock = true, image = "placeholder.jpg") {
  // ...
}
```

### 4. Ne pas abuser des paramètres par défaut

```javascript
// ❌ Trop de paramètres, même avec valeurs par défaut
function faireAction(a, b = 1, c = 2, d = 3, e = 4, f = 5, g = 6) {
  // Difficile à utiliser et maintenir
}

// ✅ Utiliser un objet de configuration à la place
function faireAction(requis, options = {}) {
  const config = {
    b: 1,
    c: 2,
    d: 3,
    e: 4,
    f: 5,
    g: 6,
    ...options  // Fusionne les options fournies
  };
  // ...
}
```

## Erreurs courantes à éviter

### ❌ Erreur 1 : Confondre null et undefined

```javascript
function afficher(message = "Défaut") {
  console.log(message);
}

afficher(null);       // Affiche : "null" (PAS la valeur par défaut)
afficher(undefined);  // Affiche : "Défaut" ✅
```

### ❌ Erreur 2 : Utiliser un paramètre ultérieur dans une valeur par défaut

```javascript
// ❌ Ne fonctionne pas : b n'est pas encore défini
function exemple(a = b * 2, b = 5) {
  console.log(a, b);
}

// ✅ Correct : utiliser les paramètres précédents
function exemple(b = 5, a = b * 2) {
  console.log(a, b);
}
```

### ❌ Erreur 3 : Oublier que l'expression est évaluée à chaque appel

```javascript
function ajouterItem(item, liste = []) {
  liste.push(item);
  return liste;
}

// Chaque appel crée un NOUVEAU tableau
console.log(ajouterItem("a"));  // ["a"]
console.log(ajouterItem("b"));  // ["b"] (pas ["a", "b"])
```

**Note :** C'est généralement le comportement souhaité. Contrairement à Python, JavaScript crée une nouvelle valeur par défaut à chaque appel.

## Points clés à retenir

1. **Syntaxe ES6** : `function f(param = valeur) { }`

2. **Déclenché par** : `undefined` ou absence d'argument

3. **PAS déclenché par** : `null`, `0`, `""`, `false`

4. **Peut être** : valeur simple, expression, appel de fonction

5. **Ordre** : paramètres obligatoires d'abord, optionnels après

6. **Lisibilité** : valeurs par défaut visibles dans la signature

7. **Combinaison** : fonctionne avec arrow functions et déstructuration

8. **Alternative** : à l'ancienne méthode avec `||` (plus propre et plus fiable)

## Prochaines étapes

Maintenant que vous maîtrisez les paramètres par défaut, vous êtes prêt pour :

- Les **rest parameters** (`...args`) (5.6.6) - capturer un nombre variable d'arguments
- La **portée et le scope** (5.6.8) - comprendre où les variables sont accessibles
- Les **callbacks** (5.6.10) - passer des fonctions en arguments

Les paramètres par défaut sont une fonctionnalité ES6 essentielle qui rend votre code plus robuste et plus facile à utiliser. Vous les rencontrerez partout dans le JavaScript moderne !

---

**Note :** Les paramètres par défaut sont l'une des améliorations les plus appréciées d'ES6. Ils éliminent beaucoup de code répétitif et rendent les fonctions plus intuitives à utiliser. C'est une fonctionnalité que vous utiliserez constamment dans votre développement quotidien.

⏭️ [Rest parameters (...args)](/05-javascript-moderne-fondamentaux/06-fonctions-modernes/06-rest-parameters.md)
