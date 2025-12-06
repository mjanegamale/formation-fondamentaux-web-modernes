🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.8.13 - Méthodes de combinaison : concat, join

## Introduction

Les méthodes `concat()` et `join()` permettent de **combiner** des éléments, mais de manières très différentes :

| Méthode   | Action                          | Retourne            | Modifie l'original ? |
|-----------|---------------------------------|---------------------|----------------------|
| `concat()`| Fusionne des tableaux          | Nouveau tableau     | ❌ NON               |
| `join()`  | Convertit tableau en chaîne    | Chaîne de caractères| ❌ NON               |

Ces deux méthodes sont **immutables** : elles ne modifient pas le tableau original.

---

## concat() - Fusionner des tableaux

La méthode `concat()` crée un **nouveau tableau** en fusionnant le tableau d'origine avec d'autres tableaux et/ou valeurs.

### Syntaxe

```javascript
const nouveauTableau = tableau.concat(valeur1, valeur2, ..., valeurN)
```

**Paramètres** : Tableaux et/ou valeurs à ajouter
**Retour** : Un nouveau tableau contenant tous les éléments

### Fusionner deux tableaux

```javascript
const fruits1 = ["pomme", "banane"];
const fruits2 = ["orange", "kiwi"];

const tous = fruits1.concat(fruits2);

console.log(tous);     // ["pomme", "banane", "orange", "kiwi"]
console.log(fruits1);  // ["pomme", "banane"] (original intact)
console.log(fruits2);  // ["orange", "kiwi"] (original intact)
```

### Fusionner plusieurs tableaux

```javascript
const tab1 = [1, 2];
const tab2 = [3, 4];
const tab3 = [5, 6];

const fusion = tab1.concat(tab2, tab3);

console.log(fusion);  // [1, 2, 3, 4, 5, 6]
```

### Ajouter des valeurs individuelles

```javascript
const nombres = [1, 2, 3];

const nouveau = nombres.concat(4, 5);

console.log(nouveau);  // [1, 2, 3, 4, 5]
```

### Mélanger tableaux et valeurs

```javascript
const tab1 = [1, 2];
const tab2 = [5, 6];

const fusion = tab1.concat(3, 4, tab2, 7);

console.log(fusion);  // [1, 2, 3, 4, 5, 6, 7]
```

### Copier un tableau

Appeler `concat()` sans arguments crée une copie :

```javascript
const original = [1, 2, 3];

const copie = original.concat();

copie[0] = 999;

console.log(original);  // [1, 2, 3] (intact)
console.log(copie);     // [999, 2, 3]
```

---

## concat() vs Spread operator

Le **spread operator** (`...`) est l'alternative moderne à `concat()`.

### Comparaison

```javascript
const tab1 = [1, 2];
const tab2 = [3, 4];

// Avec concat()
const fusion1 = tab1.concat(tab2);

// Avec spread operator (moderne)
const fusion2 = [...tab1, ...tab2];

console.log(fusion1);  // [1, 2, 3, 4]
console.log(fusion2);  // [1, 2, 3, 4]
```

### Avantages du spread operator

Le spread operator est plus **flexible** :

```javascript
const tab1 = [1, 2];
const tab2 = [5, 6];

// Insérer des valeurs au milieu
const nouveau = [...tab1, 3, 4, ...tab2, 7, 8];

console.log(nouveau);  // [1, 2, 3, 4, 5, 6, 7, 8]
```

Avec `concat()`, c'est plus verbeux :

```javascript
const nouveau = tab1.concat(3, 4, tab2, 7, 8);
```

### Quand utiliser quoi ?

**Utilisez le spread operator (`...`)** :
- ✅ Syntaxe plus moderne et lisible
- ✅ Plus flexible pour insérer à différentes positions
- ✅ Compatible avec ES6+

**Utilisez concat()** :
- ✅ Compatibilité avec très anciens navigateurs
- ✅ Code legacy existant
- ✅ Préférence personnelle

> 💡 **Conseil** : Dans du code moderne, préférez le spread operator.

---

## Copie superficielle (shallow copy)

⚠️ **Attention** : `concat()` crée une **copie superficielle**, comme le spread operator.

### Avec des valeurs simples (OK)

```javascript
const original = [1, 2, 3];
const copie = original.concat();

copie[0] = 999;

console.log(original);  // [1, 2, 3] ✅ Intact
```

### Avec des objets (attention !)

```javascript
const original = [{ valeur: 1 }, { valeur: 2 }];
const copie = original.concat();

copie[0].valeur = 999;

console.log(original[0].valeur);  // 999 ⚠️ Modifié !
// Les objets sont partagés (même référence)
```

Pour une copie profonde, utilisez `structuredClone()` ou une bibliothèque :

```javascript
const original = [{ valeur: 1 }, { valeur: 2 }];
const copieProfonde = structuredClone(original);

copieProfonde[0].valeur = 999;

console.log(original[0].valeur);  // 1 ✅ Intact
```

---

## join() - Convertir en chaîne de caractères

La méthode `join()` crée une **chaîne de caractères** en joignant tous les éléments du tableau avec un séparateur.

### Syntaxe

```javascript
const chaine = tableau.join(separateur)
```

**Paramètres** :
- `separateur` : Chaîne utilisée pour séparer les éléments (optionnel, défaut : virgule)

**Retour** : Une chaîne de caractères

### Utilisation de base

```javascript
const fruits = ["pomme", "banane", "orange"];

const chaine = fruits.join();

console.log(chaine);  // "pomme,banane,orange"
console.log(typeof chaine);  // "string"
```

### Avec un séparateur personnalisé

```javascript
const mots = ["Bonjour", "tout", "le", "monde"];

// Avec espace
console.log(mots.join(" "));   // "Bonjour tout le monde"

// Avec tiret
console.log(mots.join("-"));   // "Bonjour-tout-le-monde"

// Avec virgule et espace
console.log(mots.join(", "));  // "Bonjour, tout, le, monde"
```

### Séparateur vide

Un séparateur vide colle les éléments :

```javascript
const lettres = ["H", "e", "l", "l", "o"];

const mot = lettres.join("");

console.log(mot);  // "Hello"
```

### Avec des nombres

```javascript
const nombres = [1, 2, 3, 4, 5];

console.log(nombres.join(" + "));  // "1 + 2 + 3 + 4 + 5"
console.log(nombres.join(""));     // "12345"
```

### Tableau vide

```javascript
const vide = [];

console.log(vide.join());       // ""
console.log(vide.join("-"));    // ""
```

### Avec des valeurs spéciales

Les valeurs `null` et `undefined` sont converties en chaînes vides :

```javascript
const valeurs = [1, null, 3, undefined, 5];

console.log(valeurs.join("-"));  // "1--3--5"
```

---

## join() vs toString()

`toString()` est similaire à `join()` sans paramètre :

```javascript
const fruits = ["pomme", "banane", "orange"];

console.log(fruits.toString());  // "pomme,banane,orange"
console.log(fruits.join());      // "pomme,banane,orange"
console.log(fruits.join(","));   // "pomme,banane,orange"
```

### Différences

| Méthode      | Séparateur personnalisé ? | Contrôle          |
|--------------|---------------------------|-------------------|
| `join()`     | ✅ Oui                     | Total             |
| `toString()` | ❌ Non (toujours virgule)  | Limité            |

> 💡 **Conseil** : Utilisez `join()` pour plus de contrôle.

---

## Exemples pratiques complets

### Exemple 1 : Créer une phrase

```javascript
const mots = ["JavaScript", "est", "génial"];

const phrase = mots.join(" ") + " !";

console.log(phrase);  // "JavaScript est génial !"
```

### Exemple 2 : Générer un chemin de fichier

```javascript
const dossiers = ["home", "user", "documents", "projet"];

const chemin = dossiers.join("/");

console.log(chemin);  // "home/user/documents/projet"

// Avec extension
const fichier = [...dossiers, "index.html"].join("/");
console.log(fichier);  // "home/user/documents/projet/index.html"
```

### Exemple 3 : Formater des nombres

```javascript
const nombres = [1, 2, 3, 4, 5];

// Liste numérotée
const liste = nombres.map((n, i) => `${i + 1}. Item ${n}`).join("\n");
console.log(liste);
// 1. Item 1
// 2. Item 2
// 3. Item 3
// 4. Item 4
// 5. Item 5
```

### Exemple 4 : Créer une liste HTML

```javascript
const taches = ["Faire courses", "Appeler médecin", "Lire emails"];

const listeHTML = `
<ul>
  ${taches.map(t => `<li>${t}</li>`).join("\n  ")}
</ul>
`;

console.log(listeHTML);
// <ul>
//   <li>Faire courses</li>
//   <li>Appeler médecin</li>
//   <li>Lire emails</li>
// </ul>
```

### Exemple 5 : Construire une URL

```javascript
const baseURL = "https://api.example.com";
const segments = ["users", "123", "posts"];

const url = [baseURL, ...segments].join("/");

console.log(url);  // "https://api.example.com/users/123/posts"
```

### Exemple 6 : Créer un CSV

```javascript
const entetes = ["Nom", "Age", "Ville"];
const donnees = [
  ["Alice", "25", "Paris"],
  ["Bob", "30", "Lyon"],
  ["Charlie", "35", "Marseille"]
];

// En-têtes
const csv = [entetes.join(",")];

// Données
donnees.forEach(ligne => {
  csv.push(ligne.join(","));
});

const fichierCSV = csv.join("\n");

console.log(fichierCSV);
// Nom,Age,Ville
// Alice,25,Paris
// Bob,30,Lyon
// Charlie,35,Marseille
```

### Exemple 7 : Fusionner des collections

```javascript
const utilisateursActifs = [
  { id: 1, nom: "Alice" },
  { id: 2, nom: "Bob" }
];

const utilisateursInactifs = [
  { id: 3, nom: "Charlie" }
];

const nouveauxUtilisateurs = [
  { id: 4, nom: "David" }
];

// Fusionner toutes les listes
const tous = utilisateursActifs
  .concat(utilisateursInactifs, nouveauxUtilisateurs);

console.log(tous.length);  // 4

// Extraire les noms
const noms = tous.map(u => u.nom).join(", ");
console.log(noms);  // "Alice, Bob, Charlie, David"
```

### Exemple 8 : Construire une requête SQL

```javascript
const colonnes = ["nom", "email", "age"];
const table = "utilisateurs";
const conditions = ["age > 18", "ville = 'Paris'"];

const select = `SELECT ${colonnes.join(", ")}`;
const from = `FROM ${table}`;
const where = conditions.length > 0 ? `WHERE ${conditions.join(" AND ")}` : "";

const requete = [select, from, where].filter(Boolean).join("\n");

console.log(requete);
// SELECT nom, email, age
// FROM utilisateurs
// WHERE age > 18 AND ville = 'Paris'
```

---

## split() - L'inverse de join()

La méthode `split()` (des chaînes) fait l'**inverse** de `join()` :

```javascript
// join() : tableau → chaîne
const tableau = ["a", "b", "c"];
const chaine = tableau.join("-");
console.log(chaine);  // "a-b-c"

// split() : chaîne → tableau
const nouveauTableau = chaine.split("-");
console.log(nouveauTableau);  // ["a", "b", "c"]
```

### Exemple pratique : parsing de date

```javascript
const dateString = "2025-12-25";

// Convertir en tableau
const parties = dateString.split("-");
console.log(parties);  // ["2025", "12", "25"]

const [annee, mois, jour] = parties;
console.log(`Jour: ${jour}, Mois: ${mois}, Année: ${annee}`);
// Jour: 25, Mois: 12, Année: 2025

// Reconvertir avec un autre format
const formatFR = [jour, mois, annee].join("/");
console.log(formatFR);  // "25/12/2025"
```

---

## Chaîner les méthodes

Vous pouvez combiner `concat()` et `join()` avec d'autres méthodes :

### Exemple 1 : Filtrer puis joindre

```javascript
const mots = ["Bonjour", "", "le", "", "monde"];

// Supprimer les chaînes vides et joindre
const phrase = mots.filter(m => m !== "").join(" ");

console.log(phrase);  // "Bonjour le monde"
```

### Exemple 2 : Transformer puis joindre

```javascript
const nombres = [1, 2, 3, 4, 5];

// Doubler et créer une chaîne
const resultat = nombres
  .map(n => n * 2)
  .join(" + ");

console.log(resultat);  // "2 + 4 + 6 + 8 + 10"
```

### Exemple 3 : Fusionner, trier, puis joindre

```javascript
const groupe1 = ["Charlie", "Alice"];
const groupe2 = ["Bob", "David"];

// Fusionner, trier alphabétiquement, et créer une liste
const liste = groupe1
  .concat(groupe2)
  .sort()
  .map((nom, i) => `${i + 1}. ${nom}`)
  .join("\n");

console.log(liste);
// 1. Alice
// 2. Bob
// 3. Charlie
// 4. David
```

---

## Erreurs courantes et pièges

### ❌ Confondre concat() avec push()

```javascript
const tab1 = [1, 2];
const tab2 = [3, 4];

// ❌ push() modifie l'original
tab1.push(tab2);
console.log(tab1);  // [1, 2, [3, 4]] (tableau imbriqué !)

// ✅ concat() crée un nouveau tableau
const tab3 = [1, 2];
const fusion = tab3.concat([3, 4]);
console.log(fusion);  // [1, 2, 3, 4]
console.log(tab3);    // [1, 2] (original intact)
```

### ❌ Oublier que concat() ne modifie pas l'original

```javascript
const original = [1, 2];

original.concat([3, 4]);  // ❌ Résultat perdu

console.log(original);  // [1, 2] (inchangé)

// ✅ Stocker le résultat
const nouveau = original.concat([3, 4]);
console.log(nouveau);  // [1, 2, 3, 4]
```

### ❌ Utiliser join() sur une chaîne

```javascript
const chaine = "Bonjour";

// ❌ Les chaînes n'ont pas de méthode join()
console.log(chaine.join(" "));  // TypeError!

// ✅ Convertir d'abord en tableau
const tableau = chaine.split("");
console.log(tableau.join(" "));  // "B o n j o u r"
```

### ❌ Copier des tableaux imbriqués

```javascript
const original = [[1, 2], [3, 4]];
const copie = original.concat();

copie[0][0] = 999;

console.log(original[0][0]);  // 999 ⚠️ Modifié !
// concat() ne fait qu'une copie superficielle

// ✅ Copie profonde
const copieProfonde = structuredClone(original);
copieProfonde[0][0] = 999;
console.log(original[0][0]);  // 1 ✅ Intact
```

### ❌ join() avec des objets

```javascript
const objets = [{ nom: "Alice" }, { nom: "Bob" }];

console.log(objets.join(", "));
// "[object Object], [object Object]" ⚠️

// ✅ Extraire d'abord les propriétés
console.log(objets.map(o => o.nom).join(", "));
// "Alice, Bob"
```

---

## Performances

### concat() vs spread

Les performances sont similaires pour des tableaux de taille normale :

```javascript
const tab1 = Array(1000).fill(1);
const tab2 = Array(1000).fill(2);

console.time("concat");
const fusion1 = tab1.concat(tab2);
console.timeEnd("concat");

console.time("spread");
const fusion2 = [...tab1, ...tab2];
console.timeEnd("spread");

// Différence négligeable dans la plupart des cas
```

### join() est rapide

`join()` est optimisé et très performant :

```javascript
const grand = Array(10000).fill("test");

console.time("join");
const resultat = grand.join(", ");
console.timeEnd("join");  // Très rapide (< 1ms)
```

---

## Cas d'usage avancés

### Construire un breadcrumb

```javascript
const chemin = ["Accueil", "Produits", "Électronique", "Ordinateurs"];

// Créer un fil d'Ariane
const breadcrumb = chemin.join(" > ");
console.log(breadcrumb);
// "Accueil > Produits > Électronique > Ordinateurs"

// Avec HTML
const breadcrumbHTML = chemin
  .map((page, i) => {
    const isLast = i === chemin.length - 1;
    return isLast
      ? `<span>${page}</span>`
      : `<a href="#">${page}</a>`;
  })
  .join(" › ");

console.log(breadcrumbHTML);
// <a href="#">Accueil</a> › <a href="#">Produits</a> › ... <span>Ordinateurs</span>
```

### Générer des tags

```javascript
const tags = ["javascript", "web", "tutoriel"];

// Pour affichage
const tagsString = tags.map(t => `#${t}`).join(" ");
console.log(tagsString);  // "#javascript #web #tutoriel"

// Pour URL
const tagsURL = tags.join(",");
console.log(`/articles?tags=${tagsURL}`);
// "/articles?tags=javascript,web,tutoriel"
```

### Combiner plusieurs sources

```javascript
const systemFonts = ["Arial", "Helvetica"];
const customFonts = ["Roboto", "Open Sans"];
const fallback = ["sans-serif"];

const fontStack = systemFonts
  .concat(customFonts, fallback)
  .map(f => f.includes(" ") ? `"${f}"` : f)
  .join(", ");

console.log(`font-family: ${fontStack};`);
// font-family: Arial, Helvetica, Roboto, "Open Sans", sans-serif;
```

---

## Points clés à retenir

- ✅ **concat()** : fusionne des tableaux → retourne nouveau tableau
- ✅ **join()** : convertit tableau en chaîne → retourne string
- ✅ Les deux méthodes sont **immutables** (ne modifient pas l'original)
- ✅ concat() peut fusionner plusieurs tableaux et valeurs
- ✅ Spread operator (`...`) est l'alternative moderne à concat()
- ✅ join() accepte un séparateur personnalisé (défaut : virgule)
- ✅ join("") colle les éléments sans séparateur
- ✅ split() est l'inverse de join()
- ✅ concat() et join() font des **copies superficielles**
- ✅ Ces méthodes peuvent être chaînées avec d'autres

---

## Bonnes pratiques

- ✅ Préférez le **spread operator** à concat() dans du code moderne
- ✅ Utilisez join() pour créer des **chaînes formatées**
- ✅ Combinez split() et join() pour **transformer des formats**
- ✅ Chaînez avec map() pour transformer avant de joindre
- ✅ Attention aux **copies superficielles** avec des objets
- ✅ Utilisez join() plutôt que toString() pour plus de contrôle
- ✅ Nommez clairement vos variables de résultat

---

## Conclusion

`concat()` et `join()` sont des méthodes complémentaires qui facilitent la manipulation de tableaux :

- **concat()** pour combiner des données
- **join()** pour les présenter sous forme de texte

Bien que concat() soit souvent remplacé par le spread operator dans du code moderne, join() reste une méthode essentielle pour convertir des tableaux en chaînes formatées.

---

**Félicitations !** 🎉 Vous avez terminé le chapitre sur les tableaux modernes en JavaScript. Vous maîtrisez maintenant toutes les méthodes essentielles pour manipuler efficacement les tableaux. Dans le prochain chapitre, vous apprendrez à utiliser JavaScript pour interagir avec les pages web via le DOM (Document Object Model).

⏭️ [Manipulation du DOM](/05-javascript-moderne-fondamentaux/09-manipulation-dom/README.md)
