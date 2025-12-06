🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.3.2 - Template Literals (backticks) et interpolation `${}`

## Introduction

Les **template literals** (littéraux de gabarit en français) sont une fonctionnalité moderne introduite avec **ES6** qui révolutionne la façon de travailler avec les strings en JavaScript.

Ils utilisent les **backticks** (`` ` ``) au lieu des guillemets simples ou doubles, et offrent deux avantages majeurs :
1. **L'interpolation** : insérer facilement des variables et expressions directement dans une string
2. **Les strings multilignes** : créer des strings sur plusieurs lignes sans caractères d'échappement

🆕 **C'est la syntaxe moderne recommandée** pour créer des strings complexes en JavaScript !

---

## Les backticks : `` ` ` ``

Les template literals utilisent les **backticks** (accent grave), qui se trouvent généralement sur la même touche que le **7** sur un clavier AZERTY français.

```javascript
// Ancienne méthode avec guillemets
const message1 = "Bonjour";

// Nouvelle méthode avec backticks
const message2 = `Bonjour`;
```

À première vue, ces deux syntaxes semblent identiques, mais les backticks débloquent des fonctionnalités puissantes.

---

## Interpolation avec `${}`

L'**interpolation** permet d'insérer directement des variables et des expressions JavaScript à l'intérieur d'une string en utilisant la syntaxe `${}`.

### Syntaxe de base

```javascript
const variable = valeur;
const message = `Texte ${variable} suite du texte`;
```

### Exemple simple

**Avant (méthode classique avec concaténation) :**

```javascript
const prenom = "Alice";
const age = 25;

const message = "Je m'appelle " + prenom + " et j'ai " + age + " ans.";
console.log(message);
// Affiche : Je m'appelle Alice et j'ai 25 ans.
```

**Maintenant (avec template literals) :**

```javascript
const prenom = "Alice";
const age = 25;

const message = `Je m'appelle ${prenom} et j'ai ${age} ans.`;
console.log(message);
// Affiche : Je m'appelle Alice et j'ai 25 ans.
```

✅ **Beaucoup plus lisible !** On voit directement où les variables seront insérées.

---

## Avantages de l'interpolation

### 1. Lisibilité améliorée

Comparez ces deux versions :

```javascript
const produit = "Ordinateur";
const prix = 899;
const quantite = 2;

// ❌ Difficile à lire avec les +
const message1 = "Vous avez commandé " + quantite + " " + produit + " pour un total de " + (prix * quantite) + "€.";

// ✅ Clair et facile à comprendre
const message2 = `Vous avez commandé ${quantite} ${produit} pour un total de ${prix * quantite}€.`;
```

### 2. Moins d'erreurs

Avec la concaténation, il est facile d'oublier des espaces :

```javascript
// ❌ Oubli d'espace
const nom = "Dupont";
const message = "Bonjour Monsieur" + nom; // BonjourMonsieurDupont

// ✅ Avec template literal, c'est évident
const message2 = `Bonjour Monsieur ${nom}`; // Bonjour Monsieur Dupont
```

### 3. Facilité de maintenance

Si vous devez modifier le message, c'est beaucoup plus simple avec les template literals :

```javascript
const nom = "Alice";
const ville = "Paris";

// Facile de voir la structure du message
const message = `Bienvenue ${nom}, vous êtes connecté depuis ${ville}.`;
```

---

## Expressions dans les template literals

Vous pouvez mettre **n'importe quelle expression JavaScript** valide à l'intérieur de `${}`, pas seulement des variables !

### Calculs mathématiques

```javascript
const prix = 50;
const quantite = 3;

const message = `Total : ${prix * quantite}€`;
console.log(message); // Affiche : Total : 150€
```

### Appels de fonctions

```javascript
function majuscule(texte) {
    return texte.toUpperCase();
}

const prenom = "alice";
const message = `Bonjour ${majuscule(prenom)} !`;
console.log(message); // Affiche : Bonjour ALICE !
```

### Opérations ternaires

```javascript
const age = 17;
const message = `Vous êtes ${age >= 18 ? "majeur" : "mineur"}.`;
console.log(message); // Affiche : Vous êtes mineur.
```

### Expressions complexes

```javascript
const produits = ["pomme", "banane", "orange"];
const message = `Vous avez ${produits.length} produits dans votre panier.`;
console.log(message); // Affiche : Vous avez 3 produits dans votre panier.
```

---

## Strings multilignes

Avant les template literals, créer des strings sur plusieurs lignes était compliqué :

### Ancienne méthode (compliquée)

```javascript
// ❌ Avec \n pour les sauts de ligne
const poeme = "Roses sont rouges,\nViolettes sont bleues,\nLe sucre est doux,\nEt toi aussi.";
console.log(poeme);

// Ou avec concaténation (encore pire)
const message = "Première ligne\n" +
                "Deuxième ligne\n" +
                "Troisième ligne";
```

### Nouvelle méthode (simple et claire)

```javascript
// ✅ Avec template literals : écrivez naturellement !
const poeme = `Roses sont rouges,
Violettes sont bleues,
Le sucre est doux,
Et toi aussi.`;
console.log(poeme);
```

**Résultat :**
```
Roses sont rouges,
Violettes sont bleues,
Le sucre est doux,
Et toi aussi.
```

### Exemple pratique : HTML

Les template literals sont particulièrement utiles pour créer du HTML dynamique :

```javascript
const titre = "Mon Article";
const contenu = "Ceci est le contenu de l'article.";

const html = `
    <article>
        <h2>${titre}</h2>
        <p>${contenu}</p>
    </article>
`;

console.log(html);
```

**Résultat :**
```html
<article>
    <h2>Mon Article</h2>
    <p>Ceci est le contenu de l'article.</p>
</article>
```

---

## Gestion des guillemets

Avec les template literals, vous n'avez plus besoin d'échapper les guillemets simples ou doubles :

```javascript
// ✅ Aucun problème avec les guillemets
const message = `Elle a dit "Bonjour" et c'est parti !`;
console.log(message);
// Affiche : Elle a dit "Bonjour" et c'est parti !
```

Si vous devez absolument utiliser un backtick dans votre string, échappez-le avec `\` :

```javascript
const message = `Utilisez les backticks \` pour créer des template literals.`;
console.log(message);
// Affiche : Utilisez les backticks ` pour créer des template literals.
```

---

## Combinaison : multiligne + interpolation

Le vrai pouvoir des template literals apparaît quand vous combinez les deux fonctionnalités :

```javascript
const prenom = "Sophie";
const age = 28;
const ville = "Lyon";

const presentation = `
Bonjour, je m'appelle ${prenom}.
J'ai ${age} ans.
J'habite à ${ville}.
`;

console.log(presentation);
```

**Résultat :**
```
Bonjour, je m'appelle Sophie.
J'ai 28 ans.
J'habite à Lyon.
```

### Exemple avancé : génération d'email

```javascript
const client = "Martin Dubois";
const numeroCommande = "CMD-2025-001";
const montant = 159.99;
const articles = ["Livre JavaScript", "Clavier mécanique"];

const email = `
Bonjour ${client},

Votre commande n°${numeroCommande} a bien été enregistrée.

Articles commandés :
${articles.map(article => `- ${article}`).join('\n')}

Montant total : ${montant}€

Merci pour votre confiance !

L'équipe
`;

console.log(email);
```

---

## Template literals vs concaténation : comparaison

| Caractéristique | Concaténation `+` | Template Literals `` ` ` `` |
|----------------|-------------------|---------------------------|
| **Lisibilité** | ❌ Faible avec plusieurs variables | ✅ Excellente |
| **Expressions** | ❌ Compliqué | ✅ Simple avec `${}` |
| **Multilignes** | ❌ Nécessite `\n` | ✅ Naturel |
| **Guillemets** | ❌ Échappement nécessaire | ✅ Aucun problème |
| **Maintenance** | ❌ Difficile | ✅ Facile |
| **Performance** | ⚡ Légèrement plus rapide | ⚡ Légèrement plus lent |

**Verdict** : Pour des strings simples, les deux se valent. Dès que ça devient complexe, **utilisez les template literals** ! La différence de performance est négligeable dans 99% des cas.

---

## Cas d'usage courants

### 1. Messages utilisateur

```javascript
const utilisateur = "Alice";
const nouveauxMessages = 5;

const notification = `Bonjour ${utilisateur}, vous avez ${nouveauxMessages} nouveau${nouveauxMessages > 1 ? 'x' : ''} message${nouveauxMessages > 1 ? 's' : ''}.`;
```

### 2. URLs dynamiques

```javascript
const userId = 42;
const endpoint = "users";

const url = `https://api.monsite.com/${endpoint}/${userId}`;
console.log(url); // https://api.monsite.com/users/42
```

### 3. Logs de debug

```javascript
const fonction = "calculerTotal";
const resultat = 150;

console.log(`[DEBUG] ${fonction}() a retourné : ${resultat}`);
// [DEBUG] calculerTotal() a retourné : 150
```

### 4. Création de composants HTML

```javascript
const nom = "Alice";
const avatar = "avatar.jpg";

const profilHTML = `
    <div class="profil">
        <img src="${avatar}" alt="${nom}">
        <h3>${nom}</h3>
    </div>
`;
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Oublier les backticks

```javascript
// ❌ Ceci ne fonctionnera PAS
const message = "Bonjour ${prenom}";  // Affiche littéralement : Bonjour ${prenom}

// ✅ Il faut des backticks
const message = `Bonjour ${prenom}`;
```

### ❌ Erreur 2 : Oublier les accolades

```javascript
const age = 25;

// ❌ Ne fonctionne pas
const message = `J'ai $age ans`;  // Affiche : J'ai $age ans

// ✅ Utilisez ${}
const message = `J'ai ${age} ans`;
```

### ❌ Erreur 3 : Espaces indésirables avec multilignes

```javascript
// ⚠️ Les espaces d'indentation sont inclus
const message = `
    Ligne 1
    Ligne 2
`;
// Résultat :
//     Ligne 1
//     Ligne 2

// ✅ Solution : pas d'indentation ou trim()
const message = `
Ligne 1
Ligne 2
`.trim();
```

---

## Astuce pro : tagged templates

Les template literals ont une fonctionnalité avancée appelée **tagged templates** qui permet de traiter la string avec une fonction personnalisée. C'est un sujet avancé que nous n'aborderons pas ici, mais sachez que c'est possible !

```javascript
// Aperçu (concept avancé)
function highlight(strings, ...values) {
    // Traitement personnalisé
}

const nom = "Alice";
const resultat = highlight`Bonjour ${nom} !`;
```

Cette fonctionnalité est utilisée par des librairies populaires comme **styled-components** en React.

---

## Points clés à retenir

✅ **Template literals** : utilisez les backticks `` ` ` `` pour créer des strings modernes

✅ **Interpolation** : insérez des variables et expressions avec `${}`

✅ **Multilignes** : écrivez naturellement sur plusieurs lignes sans `\n`

✅ **Lisibilité** : votre code est plus clair et facile à maintenir

✅ **Expressions** : mettez n'importe quelle expression JavaScript valide dans `${}`

✅ **Recommandation** : privilégiez les template literals dès que vous avez des variables ou expressions à inclure

---

## Quand utiliser les template literals ?

**✅ À UTILISER :**
- Dès que vous avez des variables à insérer
- Pour des strings multilignes
- Pour créer du HTML ou des templates
- Pour améliorer la lisibilité

**🤷 OPTIONNEL :**
- Pour des strings simples sans variables : `"Bonjour"` ou `` `Bonjour` `` sont équivalents

**❌ PAS NÉCESSAIRE :**
- Si vous n'avez vraiment aucune variable et une string d'une seule ligne courte

---

## Dans la prochaine section

Dans la section **5.3.3 - Propriété length**, nous découvrirons comment obtenir la longueur d'une string et les implications pratiques de cette propriété.

---


⏭️ [Propriété length](/05-javascript-moderne-fondamentaux/03-strings-modernes/03-propriete-length.md)
