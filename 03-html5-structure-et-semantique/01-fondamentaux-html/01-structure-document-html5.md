🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.1.1 Structure d'un document HTML5

## Introduction

Tous les documents HTML5 suivent une structure de base commune, un peu comme toutes les lettres commencent par une formule de politesse et se terminent par une signature. Cette structure est essentielle : elle permet aux navigateurs de comprendre et d'afficher correctement votre contenu.

Dans cette section, nous allons découvrir **la structure minimale** que doit contenir tout document HTML5 valide.

## La structure de base minimale

Voici le squelette minimum d'un document HTML5 :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titre de ma page</title>
</head>
<body>
    <!-- Votre contenu visible va ici -->
</body>
</html>
```

Cette structure peut sembler intimidante au premier abord, mais nous allons la décortiquer élément par élément pour que tout devienne clair.

## Décortiquons chaque élément

### 1. Le DOCTYPE

```html
<!DOCTYPE html>
```

**À quoi ça sert ?**

Le DOCTYPE (déclaration de type de document) est la **toute première ligne** de votre fichier HTML. C'est comme une carte d'identité qui dit au navigateur : "Bonjour, je suis un document HTML5 !"

**Points importants :**
- Cette ligne doit toujours être en **première position**, sans aucun espace ou caractère avant
- En HTML5, elle est devenue très simple : `<!DOCTYPE html>` (en majuscules ou minuscules, peu importe)
- Dans les anciennes versions de HTML, cette ligne était beaucoup plus longue et complexe
- Sans cette ligne, les navigateurs peuvent entrer en "mode quirks" et afficher votre page de manière incorrecte

**Analogie :** C'est comme montrer votre passeport à la douane avant d'entrer dans un pays.

### 2. La balise `<html>`

```html
<html lang="fr">
    <!-- Tout le reste du document -->
</html>
```

**À quoi ça sert ?**

La balise `<html>` est l'**élément racine** de votre document. Tout le contenu de votre page doit être à l'intérieur de cette balise. C'est le conteneur principal qui englobe absolument tout.

**L'attribut `lang` :**
- `lang="fr"` indique que le contenu principal de la page est en français
- Utilisez `lang="en"` pour l'anglais, `lang="es"` pour l'espagnol, etc.
- Cet attribut est important pour :
  - L'accessibilité (les lecteurs d'écran utilisent cette information)
  - Les moteurs de recherche (pour le référencement)
  - La traduction automatique
  - La prononciation correcte du contenu

**Structure :**
- Elle s'ouvre avec `<html lang="fr">`
- Elle se ferme avec `</html>` à la toute fin du document
- Entre les deux, vous avez deux sections principales : `<head>` et `<body>`

### 3. La section `<head>`

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titre de ma page</title>
</head>
```

**À quoi ça sert ?**

La section `<head>` (tête) contient les **métadonnées** : des informations **sur** votre page, mais qui ne sont pas directement affichées dans la fenêtre du navigateur. C'est la section "administrative" de votre document.

**Analogie :** Si votre page web était un livre, le `<head>` contiendrait la page de couverture, l'ISBN, l'éditeur, etc. - des informations importantes mais qui ne font pas partie de l'histoire elle-même.

**Que trouve-t-on dans le `<head>` ?**

#### a) La balise `<meta charset="UTF-8">`

```html
<meta charset="UTF-8">
```

Cette balise définit l'**encodage des caractères** de votre document. UTF-8 permet d'afficher correctement :
- Les lettres accentuées (é, è, à, ç, etc.)
- Les caractères spéciaux (€, ©, ™, etc.)
- Les alphabets non-latins (chinois, arabe, cyrillique, etc.)

**Important :** Cette balise doit être placée en **premier** dans le `<head>`, dans les 1024 premiers octets du fichier. Sans elle, vous risquez de voir des caractères bizarres (�, Ã©, etc.) à la place de vos accents.

#### b) La balise `<meta name="viewport">`

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Cette balise est **essentielle pour le responsive design** (adaptation aux mobiles et tablettes).

**Que signifie chaque partie ?**
- `width=device-width` : la largeur de la page correspond à la largeur de l'écran de l'appareil
- `initial-scale=1.0` : le niveau de zoom initial est de 100% (pas de zoom par défaut)

Sans cette balise, votre site risque d'apparaître tout petit sur mobile, obligeant les utilisateurs à zoomer et à faire défiler horizontalement.

#### c) La balise `<title>`

```html
<title>Titre de ma page</title>
```

Le titre de votre page est **l'élément le plus important** du `<head>`. Il apparaît :
- Dans l'onglet du navigateur
- Dans les favoris/marque-pages
- Dans les résultats de recherche Google
- Dans les partages sur les réseaux sociaux

**Bonnes pratiques pour le titre :**
- Soyez **descriptif** et **unique** pour chaque page
- Limitez-vous à **50-60 caractères** pour qu'il ne soit pas tronqué dans les résultats de recherche
- Incluez des mots-clés pertinents (mais naturellement)
- Évitez les titres génériques comme "Accueil" ou "Page 1"

**Exemples :**
- ❌ Mauvais : "Accueil"
- ✅ Bon : "Boulangerie Martin - Pain artisanal à Lyon"

### 4. La section `<body>`

```html
<body>
    <!-- Tout votre contenu visible va ici -->
    <h1>Bienvenue sur mon site</h1>
    <p>Ceci est mon premier paragraphe.</p>
</body>
```

**À quoi ça sert ?**

La section `<body>` (corps) contient **tout le contenu visible** de votre page web : textes, images, vidéos, formulaires, etc. C'est la partie que vos visiteurs verront et avec laquelle ils interagiront.

**Analogie :** Si le `<head>` était la couverture d'un livre, le `<body>` serait toutes les pages de l'histoire à l'intérieur.

**Que trouve-t-on dans le `<body>` ?**
- Tous les éléments de contenu (titres, paragraphes, listes, etc.)
- Les images et médias
- Les formulaires
- Les tableaux
- Les liens de navigation
- Bref : **tout ce qui est affiché** dans la fenêtre du navigateur

## La hiérarchie complète

Visualisons la structure complète sous forme d'arbre :

```
<!DOCTYPE html>
│
└── <html>
    │
    ├── <head>
    │   ├── <meta charset>
    │   ├── <meta viewport>
    │   └── <title>
    │
    └── <body>
        └── [Contenu visible]
```

Cette hiérarchie est appelée le **DOM** (Document Object Model) - la représentation en arbre de votre document HTML.

## Exemple complet et commenté

Voici un exemple de document HTML5 complet avec des commentaires explicatifs :

```html
<!DOCTYPE html>
<!-- Déclaration du type de document : HTML5 -->

<html lang="fr">
<!-- Élément racine, contenu en français -->

<head>
    <!-- Section des métadonnées (non visibles) -->

    <meta charset="UTF-8">
    <!-- Encodage UTF-8 pour les caractères spéciaux -->

    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Configuration pour le responsive design -->

    <title>Ma première page web - Apprendre HTML5</title>
    <!-- Titre affiché dans l'onglet du navigateur -->
</head>

<body>
    <!-- Section du contenu visible -->

    <h1>Bonjour le monde !</h1>
    <!-- Titre principal de niveau 1 -->

    <p>Ceci est ma première page HTML5.</p>
    <!-- Un paragraphe de texte -->

    <p>Je commence à comprendre la structure d'un document web !</p>
    <!-- Un autre paragraphe -->

</body>

</html>
<!-- Fin du document -->
```

## Points clés à retenir

### 1. L'ordre est important
La structure doit toujours suivre cet ordre :
1. `<!DOCTYPE html>`
2. `<html>`
3. `<head>` (avec son contenu)
4. `<body>` (avec son contenu)
5. Fermeture de `</html>`

### 2. Les balises ouvrantes et fermantes
- Chaque balise qui s'ouvre doit se fermer : `<html>` ... `</html>`
- Les balises `<meta>` sont des balises auto-fermantes (pas de balise de fermeture séparée)
- L'indentation aide à visualiser la hiérarchie

### 3. Le contenu visible vs invisible
- `<head>` → Informations **sur** la page (invisibles)
- `<body>` → Contenu **de** la page (visible)

### 4. Les balises minimales obligatoires
Pour un document HTML5 valide, vous devez avoir **au minimum** :
- `<!DOCTYPE html>`
- `<html>`
- `<head>` avec `<title>`
- `<body>`

### 5. La sémantique commence ici
Même au niveau de la structure de base, HTML5 est sémantique : chaque élément a un rôle précis et ne doit pas être utilisé pour autre chose.

## Questions fréquentes

**Q : Puis-je mettre du contenu visible dans le `<head>` ?**
Non, tout le contenu visible doit être dans le `<body>`. Le `<head>` est réservé aux métadonnées.

**Q : L'ordre du contenu dans le `<head>` est-il important ?**
Oui et non. Le `<meta charset>` doit être le plus tôt possible. Pour le reste, il y a des recommandations de bonnes pratiques, mais le navigateur comprendra dans la plupart des cas.

**Q : Dois-je vraiment écrire tout ça à chaque fois ?**
Au début, oui, pour apprendre. Ensuite, votre éditeur de code (comme VS Code) peut générer cette structure automatiquement avec des snippets (raccourcis). Tapez `!` puis `Tab` dans VS Code pour voir la magie opérer !

**Q : Que se passe-t-il si j'oublie le DOCTYPE ou la balise html ?**
Le navigateur essaiera quand même d'afficher votre page, mais il pourrait y avoir des comportements imprévisibles. C'est comme construire une maison sans fondations : ça peut tenir, mais ce n'est pas une bonne idée.

**Q : Puis-je ajouter plusieurs balises `<title>` ?**
Non, il ne doit y avoir qu'un seul `<title>` par page. Si vous en mettez plusieurs, seul le premier sera pris en compte.

## Conseils pratiques

### Utilisez un snippet (raccourci)

Dans VS Code, tapez simplement :
```
!
```
Puis appuyez sur `Tab`, et la structure complète sera générée automatiquement !

### Validez votre structure

Utilisez le validateur du W3C (https://validator.w3.org/) pour vérifier que votre structure est correcte. C'est gratuit et très utile pour apprendre.

### Indentez proprement

Une bonne indentation rend votre code lisible :

✅ **Bon :**
```html
<html>
    <head>
        <title>Mon titre</title>
    </head>
    <body>
        <h1>Mon contenu</h1>
    </body>
</html>
```

❌ **Mauvais :**
```html
<html>
<head>
<title>Mon titre</title>
</head>
<body>
<h1>Mon contenu</h1>
</body>
</html>
```

### Commentez votre code

N'hésitez pas à ajouter des commentaires pour vous souvenir de ce que fait chaque section :

```html
<!-- Début de l'en-tête -->
<head>
    <!-- ... -->
</head>
<!-- Fin de l'en-tête -->
```

## Visualisation dans le navigateur

Quand vous créez ce document et l'ouvrez dans un navigateur :

1. **Le DOCTYPE** : invisible, mais indique au navigateur comment interpréter le document
2. **L'attribut `lang`** : invisible, mais aide les technologies d'assistance
3. **Le `<head>`** : complètement invisible (sauf le `<title>` qui apparaît dans l'onglet)
4. **Le `<body>`** : tout ce qui s'affiche dans la fenêtre principale

## Prochaines étapes

Maintenant que vous comprenez la structure de base d'un document HTML5, nous allons approfondir chaque élément :

- Les métadonnées et leur importance pour le SEO
- L'encodage des caractères en détail
- Comment utiliser les DevTools pour inspecter cette structure

Cette structure de base est la fondation sur laquelle tout votre code HTML sera construit. Prenez le temps de bien la comprendre et de la mémoriser : vous l'utiliserez dans chaque page web que vous créerez !

---

**Section suivante** : [3.1.2 Doctype, balises head et métadonnées](./02-doctype-head-et-metadonnees.md)

⏭️ [Doctype, balises head et métadonnées](/03-html5-structure-et-semantique/01-fondamentaux-html/02-doctype-head-et-metadonnees.md)
