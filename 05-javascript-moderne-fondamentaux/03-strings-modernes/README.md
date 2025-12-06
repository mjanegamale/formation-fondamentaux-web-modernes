🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3 - Strings modernes

## Introduction

Bienvenue dans cette section dédiée aux **strings** (chaînes de caractères) en JavaScript ! Les strings sont l'un des types de données les plus utilisés en programmation. Elles permettent de manipuler du texte : afficher des messages, traiter des entrées utilisateur, formater des données, et bien plus encore.

### Qu'est-ce qu'une string ?

Une **string** est une séquence de caractères qui représente du texte. En JavaScript, les strings peuvent contenir :
- Des lettres : `"Bonjour"`
- Des chiffres (en tant que texte) : `"2025"`
- Des symboles : `"@#$%"`
- Des espaces et caractères spéciaux : `"Hello World!"`
- Même des emojis : `"😀🎉"`

```javascript
const message = "Bonjour le monde !";
const nombre = "42";
const email = "alice@example.com";
```

---

## Pourquoi cette section est importante ?

Les strings sont omniprésentes dans le développement web :
- 💬 **Messages utilisateur** : afficher des notifications, des erreurs, des confirmations
- 📝 **Formulaires** : traiter et valider les entrées de texte
- 🌐 **URLs et chemins** : manipuler des adresses web et des chemins de fichiers
- 📊 **Données** : parser et formater du JSON, CSV, XML
- 🎨 **Contenu dynamique** : créer du HTML, des templates, des emails

Maîtriser les strings est **essentiel** pour devenir un bon développeur web.

---

## Approche moderne

Cette section met l'accent sur les **méthodes modernes** introduites avec **ES6+** (ECMAScript 2015 et versions suivantes), qui rendent le code plus lisible et plus facile à écrire.

Vous apprendrez à :
- 🆕 Utiliser les **template literals** (backticks) pour une syntaxe moderne
- ✅ Privilégier les méthodes modernes comme `includes()`, `startsWith()`, `endsWith()`
- 🎯 Maîtriser les outils essentiels comme `slice()`, `trim()`, `split()` et `join()`
- 📐 Comprendre quand utiliser quelle méthode

---

## Ce que vous allez apprendre

Cette section couvre **7 chapitres** qui vous donneront une maîtrise complète des strings en JavaScript :

### 1. Création et manipulation
Comprendre comment créer des strings avec les différentes notations (guillemets simples, doubles, backticks) et les concepts fondamentaux comme l'échappement et la concaténation.

### 2. Template Literals 🆕
Découvrir la syntaxe moderne avec les backticks qui permet d'insérer facilement des variables dans vos strings et de créer des textes sur plusieurs lignes.

### 3. Propriété length
Apprendre à connaître la longueur d'une string, essentielle pour la validation de formulaires et de nombreuses opérations.

### 4. Méthodes de recherche
Maîtriser les outils pour chercher du contenu dans une string : `indexOf()`, `includes()`, `startsWith()`, `endsWith()`.

### 5. Extraction de sous-chaînes
Apprendre à extraire des portions de texte avec `slice()` et `substring()` pour récupérer exactement ce dont vous avez besoin.

### 6. Transformation
Découvrir comment modifier le contenu des strings : conversion en majuscules/minuscules, suppression des espaces avec `trim()`.

### 7. Split et Join
Maîtriser la conversion entre strings et tableaux pour manipuler du texte structuré (listes, CSV, tags, etc.).

---

## Prérequis

Pour suivre cette section, vous devez avoir compris :
- ✅ Les variables et types de données (Section 5.2)
- ✅ La notion d'immutabilité des strings
- ✅ Les bases de la syntaxe JavaScript

Si vous débutez complètement, assurez-vous d'avoir parcouru les sections précédentes.

---

## Concept clé : l'immutabilité

**Point crucial à retenir** : Les strings sont **immutables** en JavaScript. Cela signifie qu'une fois créée, une string ne peut pas être modifiée.

```javascript
let mot = "Bonjour";

// ❌ Ceci ne modifie PAS la string originale
mot.toUpperCase();
console.log(mot); // Affiche toujours "Bonjour"

// ✅ Il faut assigner le résultat à une variable
mot = mot.toUpperCase();
console.log(mot); // Affiche maintenant "BONJOUR"
```

Toutes les méthodes de manipulation de strings **créent et retournent une nouvelle string** au lieu de modifier l'originale. Vous devez donc toujours **assigner le résultat** si vous voulez conserver la transformation.

---

## Méthodes modernes vs Legacy

Dans cette section, nous mettrons l'accent sur les **méthodes modernes** tout en mentionnant brièvement les approches plus anciennes (legacy) pour que vous puissiez comprendre le code existant.

| Ancien (Legacy) ⚠️ | Moderne (Recommandé) ✅ |
|-------------------|------------------------|
| Concaténation avec `+` | Template literals `` `${variable}` `` |
| `indexOf() !== -1` | `includes()` |
| `indexOf() === 0` | `startsWith()` |
| `substring()` | `slice()` |

**Philosophie** : Privilégiez toujours les méthodes modernes pour un code plus clair et maintenable !

---

## Comment utiliser cette section ?

### Pour les débutants complets
Suivez les chapitres dans l'ordre, du 5.3.1 au 5.3.7. Chaque chapitre construit sur les connaissances du précédent.

### Pour ceux qui ont déjà des bases
Vous pouvez sauter directement aux chapitres qui vous intéressent, mais nous vous recommandons de lire au minimum :
- 5.3.2 (Template Literals) - La syntaxe moderne essentielle
- 5.3.4 (Méthodes de recherche) - Les outils du quotidien
- 5.3.7 (Split et Join) - Manipulation de texte structuré

### Approche pratique
Chaque section contient de nombreux exemples concrets. N'hésitez pas à :
- 💻 Tester le code dans la console de votre navigateur
- 🔧 Modifier les exemples pour expérimenter
- 📝 Prendre des notes sur les méthodes qui vous semblent utiles

---

## Ressources complémentaires

Pour approfondir vos connaissances sur les strings :
- **MDN Web Docs** : Documentation de référence sur les strings en JavaScript
- **DevTools Console** : Testez vos strings directement dans le navigateur
- **Can I Use** : Vérifiez la compatibilité des méthodes modernes

---

## À quoi s'attendre ?

À la fin de cette section, vous serez capable de :
- ✅ Créer et manipuler des strings de manière professionnelle
- ✅ Utiliser les template literals pour un code moderne et lisible
- ✅ Rechercher, extraire et transformer du texte efficacement
- ✅ Valider et nettoyer des entrées utilisateur
- ✅ Parser et formater des données textuelles
- ✅ Choisir la bonne méthode pour chaque situation

---

## Plan détaillé de la section

1. **[Création et manipulation](./01-creation-manipulation.md)**
   - Les trois notations pour créer des strings
   - Échappement de caractères
   - Concaténation classique
   - Conversion en string

2. **[Template Literals et interpolation](./02-template-literals.md)** 🆕
   - Syntaxe avec backticks
   - Interpolation avec `${}`
   - Strings multilignes
   - Pourquoi c'est mieux que la concaténation

3. **[Propriété length](./03-propriete-length.md)**
   - Obtenir la longueur d'une string
   - Validation de formulaires
   - Comptage de caractères
   - Différence entre propriété et méthode

4. **[Méthodes de recherche](./04-methodes-recherche.md)**
   - `includes()` - vérifier la présence 🆕
   - `startsWith()` - vérifier le début 🆕
   - `endsWith()` - vérifier la fin 🆕
   - `indexOf()` - obtenir la position ⚠️

5. **[Extraction : substring, slice](./05-extraction-substring-slice.md)**
   - `slice()` - extraction moderne ✅
   - `substring()` - méthode legacy ⚠️
   - Indices négatifs
   - Cas d'usage pratiques

6. **[Transformation](06-transformation.md)**
   - `toLowerCase()` - conversion en minuscules
   - `toUpperCase()` - conversion en majuscules
   - `trim()` - suppression des espaces
   - Normalisation de données

7. **[Split et Join](07-split-join.md)**
   - `split()` - string vers tableau
   - `join()` - tableau vers string
   - Parsing de données CSV
   - Manipulation de listes

---

## Conventions utilisées

Dans cette section, vous verrez ces symboles :

- 🆕 : Fonctionnalité moderne ES6+ (à privilégier)
- ⚠️ : Méthode legacy (à connaître mais ne pas utiliser dans du nouveau code)
- ✅ : Bonne pratique recommandée
- ❌ : Erreur courante à éviter
- 💡 : Astuce pratique
- 🔧 : Outil de développement

---

## Testez vos connaissances

Au fur et à mesure de votre progression, posez-vous ces questions :
- Comment créer une string contenant des guillemets ?
- Quelle est la différence entre `" "`, `' '` et `` ` ` `` ?
- Comment vérifier si une string contient un mot spécifique ?
- Comment obtenir les 5 derniers caractères d'une string ?
- Comment nettoyer les espaces d'une entrée utilisateur ?
- Comment convertir "Bonjour le monde" en ["Bonjour", "le", "monde"] ?

Si vous ne savez pas répondre à ces questions maintenant, pas de panique ! À la fin de cette section, tout cela sera clair. 😊

---

## Prêt à commencer ?

Les strings sont au cœur du développement web. Chaque interaction utilisateur, chaque page web, chaque application utilise des strings. Maîtriser leur manipulation est une compétence fondamentale qui vous servira tout au long de votre carrière de développeur.

Commençons par les bases avec la création et la manipulation de strings !

---


⏭️ [Création et manipulation](/05-javascript-moderne-fondamentaux/03-strings-modernes/01-creation-manipulation.md)
