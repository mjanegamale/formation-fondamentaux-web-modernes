🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.1.1 Points d'arrêt conditionnels

## Introduction

Vous avez déjà utilisé des `console.log()` pour débugger votre code ? C'est un bon début, mais il existe une méthode beaucoup plus puissante et professionnelle : **les points d'arrêt** (ou *breakpoints* en anglais).

Dans cette section, nous allons découvrir les **points d'arrêt conditionnels**, un outil indispensable qui vous permettra d'inspecter votre code uniquement dans les situations qui vous intéressent.

---

## Qu'est-ce qu'un point d'arrêt ?

### Définition simple

Un **point d'arrêt** est un marqueur que vous placez dans votre code pour dire au navigateur :
*"Arrête-toi ici et laisse-moi voir ce qui se passe !"*

Quand le navigateur rencontre un point d'arrêt, il :
1. ⏸️ **Met en pause** l'exécution du code
2. 🔍 **Vous permet d'inspecter** les variables et l'état de votre application
3. ⏭️ **Attend vos instructions** pour continuer

### Analogie

Imaginez que votre code est un film. Un point d'arrêt, c'est comme appuyer sur **pause** à un moment précis pour examiner une scène image par image.

---

## Le problème avec les points d'arrêt simples

### Exemple de situation

Prenons ce code qui traite une liste d'utilisateurs :

```javascript
function traiterUtilisateurs(utilisateurs) {
  for (let i = 0; i < utilisateurs.length; i++) {
    const user = utilisateurs[i];
    console.log(`Traitement de ${user.nom}`);
    // ... traitement complexe ...
  }
}

const users = [
  { id: 1, nom: "Alice", age: 25 },
  { id: 2, nom: "Bob", age: 30 },
  { id: 3, nom: "Charlie", age: 35 },
  // ... 100 autres utilisateurs ...
];

traiterUtilisateurs(users);
```

### Le problème

Imaginons que vous avez un bug qui n'apparaît que pour **un utilisateur spécifique** (par exemple, Charlie avec l'id 3).

Si vous placez un **point d'arrêt simple** dans la boucle, le code va s'arrêter **à chaque itération** :
- Arrêt pour Alice ❌ (pas intéressant)
- Arrêt pour Bob ❌ (pas intéressant)
- Arrêt pour Charlie ✅ (c'est lui qu'on veut !)
- Arrêt pour les 100 autres ❌❌❌ (très pénible !)

**Résultat** : vous allez devoir cliquer "Continuer" plus de 100 fois pour arriver à Charlie ! 😫

---

## La solution : les points d'arrêt conditionnels

### Qu'est-ce qu'un point d'arrêt conditionnel ?

Un **point d'arrêt conditionnel** vous permet de dire :
*"Arrête-toi à cette ligne, MAIS seulement si une certaine condition est vraie."*

Dans notre exemple, on pourrait dire :
*"Arrête-toi dans la boucle, mais seulement quand user.id === 3"*

### Avantage

Le code s'exécute normalement jusqu'à ce que la condition soit remplie, puis il se met en pause **uniquement** au bon moment. Plus besoin de cliquer 100 fois !

---

## Comment créer un point d'arrêt conditionnel

### Étape par étape (Chrome DevTools)

#### 1. Ouvrir les DevTools

- Appuyez sur **F12** (Windows/Linux) ou **Cmd+Option+I** (Mac)
- Allez dans l'onglet **Sources**

#### 2. Trouver votre fichier JavaScript

Dans le panneau de gauche, naviguez jusqu'à votre fichier .js

#### 3. Placer un point d'arrêt conditionnel

Il y a deux méthodes :

**Méthode A : Clic droit sur le numéro de ligne**

1. Faites un **clic droit** sur le numéro de la ligne où vous voulez vous arrêter
2. Sélectionnez **"Add conditional breakpoint..."** (Ajouter un point d'arrêt conditionnel)
3. Une petite fenêtre apparaît

**Méthode B : Transformer un point d'arrêt existant**

1. Placez d'abord un point d'arrêt normal (clic sur le numéro de ligne)
2. Faites un **clic droit** sur le point d'arrêt (le rond bleu/orange)
3. Sélectionnez **"Edit breakpoint..."** (Modifier le point d'arrêt)

#### 4. Écrire la condition

Dans la fenêtre qui apparaît, écrivez votre condition JavaScript. Par exemple :

```javascript
user.id === 3
```

#### 5. Valider

Appuyez sur **Entrée**. Le point d'arrêt devient **orange** (au lieu de bleu) pour indiquer qu'il est conditionnel.

### Reconnaissance visuelle

- 🔵 **Point d'arrêt normal** : rond bleu
- 🟠 **Point d'arrêt conditionnel** : rond orange avec un point d'interrogation

---

## Exemples pratiques de conditions

### 1. Vérifier une valeur spécifique

```javascript
// S'arrêter uniquement quand l'ID est 42
id === 42

// S'arrêter uniquement pour un prénom spécifique
nom === "Charlie"

// S'arrêter uniquement si le montant est négatif
montant < 0
```

### 2. Vérifier un compteur de boucle

```javascript
// S'arrêter à la 50ème itération
i === 50

// S'arrêter après 100 itérations
compteur > 100

// S'arrêter uniquement aux itérations paires
i % 2 === 0
```

### 3. Conditions complexes

```javascript
// S'arrêter si l'utilisateur est majeur ET actif
user.age >= 18 && user.actif === true

// S'arrêter si le prix est hors limites
prix < 0 || prix > 1000

// S'arrêter si l'email est invalide
!email.includes('@')
```

### 4. Vérifier l'existence de propriétés

```javascript
// S'arrêter si la propriété "email" n'existe pas
!user.email

// S'arrêter si un tableau est vide
array.length === 0

// S'arrêter si un objet est null ou undefined
data === null || data === undefined
```

### 5. Utiliser des méthodes

```javascript
// S'arrêter si le nom commence par "A"
nom.startsWith('A')

// S'arrêter si le tableau contient "erreur"
messages.includes('erreur')

// S'arrêter si la longueur du texte dépasse 100
texte.length > 100
```

---

## Cas d'usage concrets

### Cas 1 : Débugger une boucle problématique

**Situation** : Vous avez une boucle qui traite 1000 éléments, mais un seul pose problème.

```javascript
function traiterCommandes(commandes) {
  for (let i = 0; i < commandes.length; i++) {
    const commande = commandes[i];

    // 🟠 Point d'arrêt conditionnel ici :
    // Condition : commande.id === "CMD-12345"

    calculerTotal(commande);
  }
}
```

**Solution** : Placez un point d'arrêt conditionnel avec la condition `commande.id === "CMD-12345"`

### Cas 2 : Traquer une valeur qui devient invalide

**Situation** : Une variable devient `undefined` ou `null` à un moment donné, et vous voulez savoir quand.

```javascript
function mettreAJourScore(joueur, points) {
  joueur.score += points;

  // 🟠 Point d'arrêt conditionnel ici :
  // Condition : joueur.score === null || joueur.score === undefined

  afficherScore(joueur);
}
```

**Solution** : Condition `joueur.score === null || joueur.score === undefined`

### Cas 3 : Détecter un calcul incorrect

**Situation** : Un calcul produit parfois des résultats négatifs, ce qui ne devrait jamais arriver.

```javascript
function calculerPrix(article, quantite, remise) {
  const sousTotal = article.prix * quantite;
  const montantRemise = sousTotal * remise;
  const total = sousTotal - montantRemise;

  // 🟠 Point d'arrêt conditionnel ici :
  // Condition : total < 0

  return total;
}
```

**Solution** : Condition `total < 0` pour détecter les prix négatifs

### Cas 4 : Surveiller les changements d'état

**Situation** : Un état change de manière inattendue, vous voulez voir quand.

```javascript
function changerStatut(tache, nouveauStatut) {
  // 🟠 Point d'arrêt conditionnel ici :
  // Condition : nouveauStatut === "supprimé" && tache.important === true

  tache.statut = nouveauStatut;
  sauvegarderTache(tache);
}
```

**Solution** : Condition `nouveauStatut === "supprimé" && tache.important === true`

---

## Astuces et bonnes pratiques

### ✅ À faire

1. **Soyez spécifique** : Plus votre condition est précise, moins vous aurez d'arrêts inutiles

2. **Utilisez des expressions simples** : Les conditions doivent retourner `true` ou `false`

3. **Testez vos conditions** : Vous pouvez tester votre expression dans la console avant de l'utiliser

4. **Combinez plusieurs conditions** : Utilisez `&&` (ET) et `||` (OU) pour affiner

5. **N'oubliez pas les parenthèses** : Pour les expressions complexes
   ```javascript
   (age > 18 && age < 65) || statut === "vip"
   ```

### ❌ À éviter

1. **Conditions qui modifient l'état** :
   ```javascript
   // ❌ MAUVAIS : modifie la variable
   compteur++

   // ✅ BON : vérifie juste la valeur
   compteur === 10
   ```

2. **Appels de fonctions avec effets de bord** :
   ```javascript
   // ❌ MAUVAIS : appelle une fonction qui fait des choses
   enregistrerLog(data)

   // ✅ BON : vérifie juste les propriétés
   data.status === "error"
   ```

3. **Conditions trop complexes** : Si votre condition devient illisible, découpez-la

---

## Différence avec console.log()

### Avec console.log() (ancienne méthode)

```javascript
function traiterDonnees(items) {
  for (let i = 0; i < items.length; i++) {
    const item = items[i];

    // On doit ajouter des logs partout 😓
    console.log("Item actuel:", item);
    console.log("ID:", item.id);

    if (item.id === 42) {
      console.log("🎯 Trouvé l'item 42 !");
      console.log("Prix:", item.prix);
      // ... plus de logs ...
    }

    traiter(item);
  }
}
```

**Inconvénients** :
- 😓 Code pollué par les logs
- 🗑️ Il faut les retirer ensuite
- 📝 Information limitée (que ce qu'on a pensé à logger)
- 🐌 Ralentit l'exécution si beaucoup de logs

### Avec point d'arrêt conditionnel (méthode moderne)

```javascript
function traiterDonnees(items) {
  for (let i = 0; i < items.length; i++) {
    const item = items[i];

    // 🟠 Point d'arrêt conditionnel : item.id === 42

    traiter(item);
  }
}
```

**Avantages** :
- ✨ Code propre, sans modifications
- 🔍 Accès à TOUTES les variables et l'état complet
- ⚡ Pas d'impact sur les performances
- 🎯 Arrêt uniquement quand nécessaire

---

## Gérer les points d'arrêt conditionnels

### Voir tous vos points d'arrêt

Dans les DevTools, onglet **Sources**, regardez le panneau **Breakpoints** sur la droite. Vous y verrez :
- 📝 Liste de tous vos points d'arrêt
- 📍 Fichier et ligne de chaque point d'arrêt
- 🟠 Indication visuelle pour les conditionnels
- ✅ Case à cocher pour activer/désactiver temporairement

### Modifier une condition

1. Faites un **clic droit** sur le point d'arrêt (dans le code ou dans la liste)
2. Choisissez **"Edit breakpoint..."**
3. Modifiez la condition
4. Validez avec **Entrée**

### Supprimer un point d'arrêt conditionnel

**Méthode 1** : Cliquez sur le rond orange dans la marge du code

**Méthode 2** : Clic droit → **"Remove breakpoint"**

**Méthode 3** : Dans le panneau Breakpoints, clic droit → **"Remove breakpoint"**

### Désactiver temporairement

Plutôt que de supprimer un point d'arrêt, vous pouvez le **désactiver** :
- Dans le panneau **Breakpoints**, décochez la case ☐
- Le point d'arrêt reste en place mais ne s'activera pas
- Utile pour le réactiver plus tard sans réécrire la condition

### Désactiver TOUS les points d'arrêt

En haut du panneau Breakpoints, il y a un bouton **"Deactivate breakpoints"** (icône de pause barrée).
Pratique pour laisser votre code s'exécuter normalement sans supprimer vos configurations.

---

## Quand utiliser les points d'arrêt conditionnels ?

### ✅ Situations idéales

1. **Boucles avec beaucoup d'itérations**
   - Quand vous cherchez un élément spécifique parmi des milliers

2. **Événements répétitifs**
   - Détecter un clic problématique parmi des centaines

3. **Valeurs invalides**
   - S'arrêter uniquement quand une erreur se produit

4. **Cas limites**
   - Détecter les situations exceptionnelles (valeurs nulles, tableaux vides, etc.)

5. **Debugging par élimination**
   - Tester différentes hypothèses une par une

### ⚠️ Quand un point d'arrêt simple suffit

Si vous voulez inspecter le code :
- Au début d'une fonction précise
- À une seule ligne spécifique
- Sans condition particulière

→ Utilisez un **point d'arrêt simple** (plus rapide à configurer)

---

## Dépannage

### "Mon point d'arrêt ne s'active jamais"

**Causes possibles** :

1. **La condition n'est jamais vraie**
   - Vérifiez votre condition dans la console
   - Utilisez `console.log()` temporairement pour voir les valeurs

2. **La ligne n'est jamais exécutée**
   - Vérifiez que le code passe bien par cette ligne
   - Placez un point d'arrêt simple pour tester

3. **Erreur de syntaxe dans la condition**
   - Testez votre expression dans la console avant
   - Vérifiez les noms de variables (sensible à la casse !)

4. **La variable n'existe pas dans ce scope**
   - La variable doit être accessible à cette ligne
   - Vérifiez la portée (scope) de vos variables

### "Le point d'arrêt s'active trop souvent"

**Solutions** :

1. **Affinez la condition** avec `&&` (ET) :
   ```javascript
   // Au lieu de :
   user.actif === true

   // Utilisez :
   user.actif === true && user.id === 42
   ```

2. **Utilisez des négations** pour exclure des cas :
   ```javascript
   item.prix > 0 && item.prix < 1000
   ```

### "Je ne trouve pas comment créer un point d'arrêt conditionnel"

**Vérifiez** :
- Vous êtes bien dans l'onglet **Sources** des DevTools
- Vous faites un **clic droit** sur le **numéro de ligne** (pas sur le code)
- Votre navigateur est à jour (Chrome 73+ ou Firefox 60+)

---

## Comparaison avec d'autres techniques

### Points d'arrêt conditionnels vs debugger;

Vous pouvez aussi utiliser le mot-clé `debugger;` dans votre code :

```javascript
if (user.id === 42) {
  debugger; // Le code s'arrête ici si DevTools ouvert
}
```

**Différences** :

| Aspect | Point d'arrêt conditionnel | debugger; |
|--------|---------------------------|-----------|
| **Code modifié** | Non ✅ | Oui ❌ |
| **Flexibilité** | Modifiable sans recharger | Nécessite modification du code |
| **Production** | Aucun impact | Doit être retiré ⚠️ |
| **Rapidité** | Configuration visuelle | Rapide à écrire |

**Recommandation** : Privilégiez les points d'arrêt conditionnels pour une approche professionnelle et non invasive.

---

## Points clés à retenir

🎯 **Un point d'arrêt conditionnel = pause ciblée**
- S'arrête uniquement quand une condition est vraie
- Évite les arrêts inutiles dans les boucles

🟠 **Reconnaissance visuelle**
- Point d'arrêt normal = bleu 🔵
- Point d'arrêt conditionnel = orange 🟠

✏️ **Création simple**
- Clic droit sur numéro de ligne → "Add conditional breakpoint"
- Écrire une expression qui retourne true/false

⚡ **Avantages majeurs**
- Code non modifié
- Gain de temps énorme
- Accès complet aux variables

🔍 **Utilisez-les pour**
- Boucles avec beaucoup d'itérations
- Détecter des valeurs invalides
- Traquer des bugs intermittents
- Comprendre des comportements complexes

---

## Prochaine étape

Maintenant que vous maîtrisez les points d'arrêt conditionnels, vous êtes prêt à découvrir les **watch expressions** qui vous permettront de surveiller des valeurs en temps réel pendant l'exécution.

---

> 💡 **Conseil de pro** :
> La maîtrise des points d'arrêt conditionnels distingue les développeurs juniors des développeurs intermédiaires. C'est un outil que vous utiliserez quotidiennement dans votre carrière !

⏭️ [Watch expressions](/07-debugging-et-outils-avances/01-debugging-javascript-avance/02-watch-expressions.md)
