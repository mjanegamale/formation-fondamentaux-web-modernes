🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3.7 - Méthodes split et join

## Introduction

Les méthodes **`split()`** et **`join()`** sont deux méthodes complémentaires qui permettent de convertir entre **strings** et **tableaux** (arrays).

- **`split()`** : découpe une string en tableau selon un séparateur
- **`join()`** : assemble les éléments d'un tableau en une string

Ces méthodes sont essentielles pour manipuler du texte structuré : listes, CSV, tags, chemins de fichiers, URLs, etc.

**Relation entre les deux méthodes :**

```javascript
// String → Tableau (split)
const string = "a,b,c";
const tableau = string.split(",");  // ["a", "b", "c"]

// Tableau → String (join)
const nouvelleString = tableau.join("-");  // "a-b-c"
```

---

## split() - Découper une string en tableau

### Syntaxe

```javascript
string.split(separateur, limite)
```

- **`separateur`** : caractère(s) qui servent à découper (obligatoire)
- **`limite`** : nombre maximum d'éléments à retourner (optionnel)

### Retourne

Un **tableau** (array) contenant les morceaux de la string.

### Utilisation de base

```javascript
const phrase = "Bonjour le monde";
const mots = phrase.split(" ");

console.log(mots);
// ["Bonjour", "le", "monde"]

console.log(typeof mots);     // "object" (c'est un tableau)
console.log(Array.isArray(mots)); // true
console.log(mots.length);     // 3
```

### Exemples avec différents séparateurs

#### Séparation par virgule

```javascript
const liste = "pomme,banane,orange";
const fruits = liste.split(",");

console.log(fruits);
// ["pomme", "banane", "orange"]
```

#### Séparation par point-virgule

```javascript
const donnees = "Alice;25;Paris";
const infos = donnees.split(";");

console.log(infos);
// ["Alice", "25", "Paris"]
```

#### Séparation par espace

```javascript
const texte = "JavaScript est génial";
const mots = texte.split(" ");

console.log(mots);
// ["JavaScript", "est", "génial"]
```

#### Séparation par slash (chemins)

```javascript
const chemin = "dossier/sous-dossier/fichier.txt";
const parties = chemin.split("/");

console.log(parties);
// ["dossier", "sous-dossier", "fichier.txt"]
```

### Split sans paramètre ou avec chaîne vide

#### Sans paramètre (ou undefined)

```javascript
const texte = "Bonjour";
const resultat = texte.split();

console.log(resultat);
// ["Bonjour"] - Un tableau avec un seul élément
```

#### Avec chaîne vide ""

```javascript
const mot = "Bonjour";
const caracteres = mot.split("");

console.log(caracteres);
// ["B", "o", "n", "j", "o", "u", "r"]

// Chaque caractère devient un élément du tableau !
```

**Astuce** : `split("")` est très utile pour obtenir tous les caractères individuellement.

### Paramètre limite

Le second paramètre limite le nombre d'éléments retournés :

```javascript
const texte = "un,deux,trois,quatre,cinq";

console.log(texte.split(","));      // ["un", "deux", "trois", "quatre", "cinq"]
console.log(texte.split(",", 3));   // ["un", "deux", "trois"]
console.log(texte.split(",", 1));   // ["un"]
```

**Note** : Les éléments au-delà de la limite sont simplement ignorés.

### Cas d'usage pratiques de split()

#### 1. Parser un fichier CSV

```javascript
const ligneCSV = "Alice,Dupont,25,Paris";
const donnees = ligneCSV.split(",");

const prenom = donnees[0];    // "Alice"
const nom = donnees[1];       // "Dupont"
const age = donnees[2];       // "25"
const ville = donnees[3];     // "Paris"

console.log(`${prenom} ${nom}, ${age} ans, habite à ${ville}`);
// Alice Dupont, 25 ans, habite à Paris
```

#### 2. Extraire les tags d'un article

```javascript
const tags = "javascript,react,nodejs,webdev";
const tableauTags = tags.split(",");

console.log(tableauTags);
// ["javascript", "react", "nodejs", "webdev"]

// Afficher chaque tag
tableauTags.forEach(tag => console.log(`#${tag}`));
```

#### 3. Compter les mots d'un texte

```javascript
const texte = "JavaScript est un langage de programmation génial";
const mots = texte.split(" ");
const nombreDeMots = mots.length;

console.log(`Ce texte contient ${nombreDeMots} mots.`);
// Ce texte contient 7 mots.
```

#### 4. Parser une URL

```javascript
const url = "https://www.example.com/blog/article-123";
const parties = url.split("/");

console.log(parties);
// ["https:", "", "www.example.com", "blog", "article-123"]

const domaine = parties[2];      // "www.example.com"
const section = parties[3];      // "blog"
const articleId = parties[4];    // "article-123"
```

#### 5. Analyser un nom complet

```javascript
const nomComplet = "Alice Marie Dupont";
const parties = nomComplet.split(" ");

const prenom = parties[0];              // "Alice"
const prenoms = parties.slice(0, -1);   // ["Alice", "Marie"]
const nom = parties[parties.length - 1]; // "Dupont"

console.log(`Prénom: ${prenom}, Nom: ${nom}`);
// Prénom: Alice, Nom: Dupont
```

#### 6. Inverser un texte mot par mot

```javascript
const phrase = "Bonjour le monde";
const mots = phrase.split(" ");
const inverse = mots.reverse().join(" ");

console.log(inverse);
// "monde le Bonjour"
```

---

## join() - Assembler un tableau en string

### Syntaxe

```javascript
tableau.join(separateur)
```

- **`separateur`** : caractère(s) à insérer entre les éléments (optionnel, par défaut ",")

### Retourne

Une **string** contenant tous les éléments du tableau assemblés.

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange"];
const liste = fruits.join(", ");

console.log(liste);
// "pomme, banane, orange"

console.log(typeof liste); // "string"
```

### Exemples avec différents séparateurs

#### Séparateur : virgule

```javascript
const mots = ["JavaScript", "est", "génial"];
const phrase = mots.join(", ");

console.log(phrase);
// "JavaScript, est, génial"
```

#### Séparateur : espace

```javascript
const mots = ["Bonjour", "le", "monde"];
const phrase = mots.join(" ");

console.log(phrase);
// "Bonjour le monde"
```

#### Séparateur : tiret

```javascript
const parties = ["2025", "12", "05"];
const date = parties.join("-");

console.log(date);
// "2025-12-05"
```

#### Séparateur : slash

```javascript
const repertoires = ["utilisateur", "documents", "projet"];
const chemin = repertoires.join("/");

console.log(chemin);
// "utilisateur/documents/projet"
```

#### Sans séparateur (chaîne vide)

```javascript
const lettres = ["B", "o", "n", "j", "o", "u", "r"];
const mot = lettres.join("");

console.log(mot);
// "Bonjour"
```

#### Séparateur par défaut (virgule)

```javascript
const nombres = [1, 2, 3, 4, 5];
const liste = nombres.join();

console.log(liste);
// "1,2,3,4,5"
```

### Cas d'usage pratiques de join()

#### 1. Créer une phrase à partir de mots

```javascript
const mots = ["J'", "aime", "JavaScript"];
const phrase = mots.join(" ");

console.log(phrase);
// "J' aime JavaScript"
```

#### 2. Formater une liste HTML

```javascript
const produits = ["Ordinateur", "Clavier", "Souris"];
const listeHTML = "<ul><li>" + produits.join("</li><li>") + "</li></ul>";

console.log(listeHTML);
// <ul><li>Ordinateur</li><li>Clavier</li><li>Souris</li></ul>
```

#### 3. Créer un slug d'URL

```javascript
const titre = ["Mon", "Premier", "Article"];
const slug = titre.join("-").toLowerCase();

console.log(slug);
// "mon-premier-article"
```

#### 4. Générer un fichier CSV

```javascript
const entete = ["Prénom", "Nom", "Age", "Ville"];
const ligne1 = ["Alice", "Dupont", "25", "Paris"];
const ligne2 = ["Bob", "Martin", "30", "Lyon"];

const csv = [
    entete.join(","),
    ligne1.join(","),
    ligne2.join(",")
].join("\n");

console.log(csv);
// Prénom,Nom,Age,Ville
// Alice,Dupont,25,Paris
// Bob,Martin,30,Lyon
```

#### 5. Afficher des tags

```javascript
const tags = ["javascript", "webdev", "tutorial"];
const affichageTags = tags.map(tag => `#${tag}`).join(" ");

console.log(affichageTags);
// "#javascript #webdev #tutorial"
```

#### 6. Créer un chemin de navigation (breadcrumb)

```javascript
const navigation = ["Accueil", "Blog", "JavaScript", "Article"];
const breadcrumb = navigation.join(" > ");

console.log(breadcrumb);
// "Accueil > Blog > JavaScript > Article"
```

---

## Combiner split() et join()

La vraie puissance apparaît quand on combine les deux méthodes pour transformer des strings.

### Remplacer tous les caractères

```javascript
const texte = "Bonjour le monde";

// Remplacer tous les espaces par des tirets
const resultat = texte.split(" ").join("-");

console.log(resultat);
// "Bonjour-le-monde"
```

### Nettoyer et reformater

```javascript
const input = "pomme, banane,  orange,   kiwi";

// Nettoyer les espaces et reformater
const propre = input
    .split(",")
    .map(fruit => fruit.trim())
    .join(", ");

console.log(propre);
// "pomme, banane, orange, kiwi"
```

### Inverser un texte mot par mot

```javascript
const phrase = "JavaScript est génial";
const inverse = phrase.split(" ").reverse().join(" ");

console.log(inverse);
// "génial est JavaScript"
```

### Inverser les caractères d'un mot

```javascript
const mot = "Bonjour";
const inverse = mot.split("").reverse().join("");

console.log(inverse);
// "ruojnoB"
```

### Créer un acronyme

```javascript
const phrase = "HyperText Markup Language";
const acronyme = phrase
    .split(" ")
    .map(mot => mot[0])
    .join("")
    .toUpperCase();

console.log(acronyme);
// "HTML"
```

### Transformer un chemin

```javascript
const cheminWindows = "C:\\Users\\Documents\\fichier.txt";
const cheminUnix = cheminWindows.split("\\").join("/");

console.log(cheminUnix);
// "C:/Users/Documents/fichier.txt"
```

### Masquer des données sensibles

```javascript
const email = "alice.dupont@example.com";
const parties = email.split("@");
const nomUtilisateur = parties[0];
const domaine = parties[1];

// Masquer une partie du nom
const debut = nomUtilisateur.slice(0, 2);
const masque = debut + "***@" + domaine;

console.log(masque);
// "al***@example.com"
```

---

## Cas pratiques avancés

### 1. Parser et formater une date

```javascript
const dateISO = "2025-12-05";
const [annee, mois, jour] = dateISO.split("-");

const dateFR = [jour, mois, annee].join("/");
console.log(dateFR); // "05/12/2025"
```

### 2. Extraire et nettoyer des tags

```javascript
const inputTags = "#javascript, #webdev, #tutorial, #coding";

const tags = inputTags
    .split(",")
    .map(tag => tag.trim().replace("#", ""))
    .filter(tag => tag.length > 0);

console.log(tags);
// ["javascript", "webdev", "tutorial", "coding"]

// Reformater pour l'affichage
console.log(tags.join(", "));
// "javascript, webdev, tutorial, coding"
```

### 3. Parser des paramètres d'URL

```javascript
const queryString = "nom=Alice&age=25&ville=Paris";

const params = {};
queryString.split("&").forEach(paire => {
    const [cle, valeur] = paire.split("=");
    params[cle] = valeur;
});

console.log(params);
// { nom: "Alice", age: "25", ville: "Paris" }
```

### 4. Formater un numéro de téléphone

```javascript
const telephone = "0612345678";
const chiffres = telephone.split("");

// Grouper par paires
const formate = [
    chiffres.slice(0, 2).join(""),
    chiffres.slice(2, 4).join(""),
    chiffres.slice(4, 6).join(""),
    chiffres.slice(6, 8).join(""),
    chiffres.slice(8, 10).join("")
].join(" ");

console.log(formate);
// "06 12 34 56 78"
```

### 5. Analyser un texte

```javascript
const texte = "JavaScript est un langage de programmation. Il est très populaire.";

// Compter les phrases
const phrases = texte.split(". ");
console.log(`Nombre de phrases: ${phrases.length}`);

// Compter les mots
const mots = texte.split(" ");
console.log(`Nombre de mots: ${mots.length}`);

// Mots uniques
const motsUniques = [...new Set(mots.map(m => m.toLowerCase()))];
console.log(`Mots uniques: ${motsUniques.length}`);
```

### 6. Créer un générateur de slug

```javascript
function creerSlug(titre) {
    return titre
        .toLowerCase()
        .trim()
        .split(" ")
        .join("-")
        .replace(/[^a-z0-9-]/g, "");
}

console.log(creerSlug("Mon Super Article !"));
// "mon-super-article"

console.log(creerSlug("JavaScript : Guide Complet"));
// "javascript-guide-complet"
```

---

## Gestion des cas particuliers

### Séparateur non trouvé

Si le séparateur n'existe pas dans la string, `split()` retourne un tableau avec la string complète :

```javascript
const texte = "Bonjour";
const resultat = texte.split(",");

console.log(resultat);
// ["Bonjour"]
console.log(resultat.length); // 1
```

### Séparateurs multiples consécutifs

Les séparateurs multiples créent des éléments vides :

```javascript
const texte = "a,,b,,,c";
const parties = texte.split(",");

console.log(parties);
// ["a", "", "b", "", "", "c"]
```

**Solution** : filtrer les éléments vides :

```javascript
const texte = "a,,b,,,c";
const parties = texte.split(",").filter(element => element !== "");

console.log(parties);
// ["a", "b", "c"]
```

### Espaces multiples

```javascript
const texte = "Bonjour    le     monde";
const mots = texte.split(" ");

console.log(mots);
// ["Bonjour", "", "", "", "le", "", "", "", "", "monde"]

// Solution : utiliser une regex
const motsPropres = texte.split(/\s+/);
console.log(motsPropres);
// ["Bonjour", "le", "monde"]
```

### Join avec types mixtes

`join()` convertit automatiquement les éléments en strings :

```javascript
const mixte = [1, "deux", true, null, undefined];
const resultat = mixte.join(", ");

console.log(resultat);
// "1, deux, true, , "
```

**Note** : `null` et `undefined` deviennent des strings vides.

---

## Split avec expressions régulières (aperçu)

`split()` peut aussi accepter une **expression régulière** comme séparateur :

```javascript
// Séparer sur plusieurs espaces
const texte = "a    b     c";
const parties = texte.split(/\s+/);
console.log(parties); // ["a", "b", "c"]

// Séparer sur virgule ou point-virgule
const liste = "a,b;c,d;e";
const elements = liste.split(/[,;]/);
console.log(elements); // ["a", "b", "c", "d", "e"]

// Séparer sur n'importe quel caractère non-alphanumérique
const texte2 = "hello-world_foo.bar";
const mots = texte2.split(/[^a-z0-9]/i);
console.log(mots); // ["hello", "world", "foo", "bar"]
```

**Note pour débutants** : Les expressions régulières sont un sujet avancé que nous verrons plus tard. Pour l'instant, retenez simplement que c'est possible !

---

## Différences avec d'autres méthodes

### split() vs slice()

```javascript
const texte = "Bonjour";

// split() découpe en tableau
console.log(texte.split(""));  // ["B", "o", "n", "j", "o", "u", "r"]

// slice() extrait une portion (reste une string)
console.log(texte.slice(0, 3)); // "Bon"
```

### join() vs concat()

```javascript
const tableau = ["a", "b", "c"];

// join() convertit en string avec séparateur
console.log(tableau.join("-")); // "a-b-c"

// concat() combine des tableaux (reste un tableau)
console.log(tableau.concat(["d", "e"])); // ["a", "b", "c", "d", "e"]
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier que split() retourne un tableau

```javascript
const texte = "a,b,c";
const resultat = texte.split(",");

// ❌ Erreur : traiter comme une string
console.log(resultat.toUpperCase()); // TypeError

// ✅ C'est un tableau
console.log(resultat[0].toUpperCase()); // "A"
console.log(resultat.map(s => s.toUpperCase())); // ["A", "B", "C"]
```

### ❌ Erreur 2 : Oublier que join() retourne une string

```javascript
const tableau = ["a", "b", "c"];
const resultat = tableau.join(",");

// ❌ Erreur : traiter comme un tableau
console.log(resultat[0]); // "a" (le caractère, pas l'élément)
console.log(resultat.length); // 5 (pas 3 !)

// ✅ C'est une string
console.log(resultat); // "a,b,c"
```

### ❌ Erreur 3 : Utiliser le mauvais séparateur

```javascript
const texte = "a, b, c";

// ❌ Oubli de l'espace après la virgule
const parties = texte.split(",");
console.log(parties); // ["a", " b", " c"] (espaces indésirables)

// ✅ Séparateur correct
const partiesPropres = texte.split(", ");
console.log(partiesPropres); // ["a", "b", "c"]

// ✅ Ou nettoyer après
const nettoyees = texte.split(",").map(s => s.trim());
console.log(nettoyees); // ["a", "b", "c"]
```

### ❌ Erreur 4 : Ne pas vérifier les tableaux vides

```javascript
const texte = "";
const mots = texte.split(" ");

console.log(mots); // [""] (tableau avec une string vide)
console.log(mots.length); // 1 (pas 0 !)

// ✅ Vérifier
if (texte.trim().length === 0) {
    console.log("Texte vide");
}
```

---

## Performance et bonnes pratiques

### Chaîner les méthodes pour la lisibilité

```javascript
// ✅ Clair et lisible
const resultat = texte
    .split(",")
    .map(item => item.trim())
    .filter(item => item.length > 0)
    .join(", ");
```

### Éviter les opérations inutiles

```javascript
// ❌ Inefficace : split puis join immédiatement
const texte = "a,b,c";
const inutile = texte.split(",").join(","); // Même résultat que texte

// ✅ Si pas de transformation, ne pas split/join
if (texte.includes(",")) {
    // travailler directement avec la string
}
```

### Utiliser les bons outils

```javascript
// Pour remplacer un caractère, pas besoin de split/join
// ❌ Complexe
const resultat1 = texte.split(" ").join("-");

// ✅ Plus simple avec replace
const resultat2 = texte.replace(/ /g, "-");
```

---

## Cas d'usage réels

### 1. Système de tags

```javascript
class ArticleManager {
    static formatTags(inputTags) {
        return inputTags
            .toLowerCase()
            .split(",")
            .map(tag => tag.trim())
            .filter(tag => tag.length > 0 && !tag.includes(" "))
            .slice(0, 5); // Maximum 5 tags
    }
}

console.log(ArticleManager.formatTags("JavaScript, React, Node.js, , WebDev"));
// ["javascript", "react", "node.js", "webdev"]
```

### 2. Parser de commandes

```javascript
function parseCommande(input) {
    const parties = input.trim().split(" ");
    const commande = parties[0];
    const arguments = parties.slice(1);

    return { commande, arguments };
}

console.log(parseCommande("/search JavaScript tutorial"));
// { commande: "/search", arguments: ["JavaScript", "tutorial"] }
```

### 3. Formateur d'adresse

```javascript
function formaterAdresse(adresse) {
    const lignes = adresse.split("\n").filter(l => l.trim());
    return lignes.join(", ");
}

const adresse = `
123 Rue de la Paix
75001 Paris
France
`;

console.log(formaterAdresse(adresse));
// "123 Rue de la Paix, 75001 Paris, France"
```

---

## Points clés à retenir

✅ **`split()`** découpe une string en tableau selon un séparateur

✅ **`join()`** assemble un tableau en string avec un séparateur

✅ Ces méthodes sont **complémentaires** et souvent utilisées ensemble

✅ **`split("")`** découpe en caractères individuels

✅ **`join("")`** assemble sans séparateur

✅ Attention aux **espaces** dans les séparateurs

✅ **Filtrer** les éléments vides quand nécessaire

✅ **Penser aux regex** pour des séparateurs complexes (niveau avancé)

✅ Toujours **vérifier le type** retourné (tableau vs string)

---

## Mémo rapide

```javascript
// String → Tableau
"a,b,c".split(",")        // ["a", "b", "c"]
"Bonjour".split("")       // ["B", "o", "n", "j", "o", "u", "r"]
"a b c".split(" ")        // ["a", "b", "c"]

// Tableau → String
["a", "b", "c"].join(",") // "a,b,c"
["a", "b", "c"].join(" ") // "a b c"
["a", "b", "c"].join("")  // "abc"

// Transformation
"a,b,c".split(",").join("-") // "a-b-c"
```

---

## Dans la prochaine section

Nous avons maintenant terminé l'exploration des **strings modernes** ! Dans la prochaine grande section, nous allons découvrir les **opérateurs** en JavaScript, qui permettent d'effectuer des calculs, des comparaisons et des opérations logiques.

---


⏭️ [Opérateurs](/05-javascript-moderne-fondamentaux/04-operateurs/README.md)
