🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.1.3 Encodage UTF-8 et attribut lang

## Introduction

Vous êtes-vous déjà demandé pourquoi certains sites web affichent des caractères bizarres comme `Ã©` au lieu de `é`, ou `â‚¬` au lieu de `€` ? La réponse se trouve dans l'**encodage des caractères**. Dans cette section, nous allons démystifier l'encodage UTF-8 et comprendre l'importance de l'attribut `lang` pour créer des sites web vraiment internationaux.

Ces deux éléments peuvent sembler techniques, mais ils sont **essentiels** pour :
- Afficher correctement tous les caractères (français, chinois, arabe, emojis...)
- Améliorer l'accessibilité
- Optimiser le référencement
- Faciliter la traduction

## Qu'est-ce que l'encodage de caractères ?

### Le problème de base

Les ordinateurs ne comprennent que les nombres (0 et 1). Pour afficher du texte, il faut une **table de correspondance** qui dit : "le nombre 65 représente la lettre A, le nombre 66 représente B", etc.

Cette table de correspondance s'appelle un **encodage de caractères**.

### L'histoire en bref

#### ASCII (années 1960) : Le début

L'ASCII (American Standard Code for Information Interchange) était le premier standard :
- Il utilisait 7 bits (128 combinaisons possibles)
- Il contenait uniquement :
  - Les lettres A-Z (majuscules et minuscules)
  - Les chiffres 0-9
  - La ponctuation de base
  - Quelques caractères spéciaux

**Le problème :** Pas de lettres accentuées (é, è, à, ç), pas d'autres alphabets. Impossible d'écrire correctement en français, espagnol, allemand, etc.

#### ISO-8859-1 (Latin-1) : Une première extension

Pour résoudre le problème, on a créé des extensions :
- ISO-8859-1 (Latin-1) pour l'Europe de l'Ouest
- ISO-8859-5 pour le cyrillique
- ISO-8859-6 pour l'arabe
- Et des dizaines d'autres...

**Le problème :** Impossible de mélanger plusieurs langues sur la même page. Impossible d'afficher du français ET du chinois ensemble.

#### UTF-8 : La solution universelle

UTF-8 (Unicode Transformation Format - 8 bits) a résolu tous ces problèmes :
- **Plus de 1 million de caractères possibles**
- Tous les alphabets du monde
- Tous les symboles et emojis
- Compatible avec ASCII (les 128 premiers caractères sont identiques)

C'est devenu le **standard universel** du web moderne.

## UTF-8 en détail

### Qu'est-ce que UTF-8 ?

UTF-8 est un système d'encodage de caractères **variable** :
- Les caractères courants (A-Z, 0-9) utilisent **1 octet**
- Les caractères accentués (é, è, ñ) utilisent **2 octets**
- Les caractères chinois, japonais, arabes utilisent **3 octets**
- Les emojis et symboles rares utilisent **4 octets**

Cette approche est **intelligente** : elle économise de l'espace pour les caractères courants tout en supportant tous les caractères du monde.

### Pourquoi UTF-8 est le standard

**Avantages :**

1. **Universel** : Supporte toutes les langues du monde sur la même page
2. **Rétrocompatible** : Compatible avec ASCII
3. **Efficace** : N'utilise que l'espace nécessaire
4. **Robuste** : Détecte facilement les erreurs
5. **Standard** : Utilisé par plus de 95% des sites web

**Ce que UTF-8 peut afficher :**

```
Français     : Ça va ? C'est l'été !
Espagnol     : ¿Cómo estás? ¡Año nuevo!
Allemand     : Schöne Grüße aus München
Russe        : Привет мир
Arabe        : مرحبا بالعالم
Chinois      : 你好世界
Japonais     : こんにちは世界
Grec         : Γεια σου κόσμε
Emojis       : 😀 🎉 ❤️ 🌍
Symboles     : © ® ™ € £ ¥ ° ½ ¼
Mathématiques: ∑ ∞ ≠ ≤ ≥ π √
```

## Comment utiliser UTF-8 dans vos pages

### 1. Déclarer UTF-8 dans le HTML

La balise `<meta charset>` doit être **la première chose** dans votre `<head>` :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <!-- Reste du head... -->
</head>
```

**Règles importantes :**
- Cette balise doit apparaître dans les **1024 premiers octets** du fichier
- Placez-la **tout en haut** du `<head>` pour être sûr
- Utilisez toujours `UTF-8` (en majuscules par convention, mais pas obligatoire)

### 2. Sauvegarder vos fichiers en UTF-8

Il ne suffit pas de déclarer UTF-8 dans le HTML, vos **fichiers eux-mêmes** doivent être sauvegardés en UTF-8.

**Dans Visual Studio Code :**

1. Regardez en bas à droite de l'éditeur, vous verrez l'encodage actuel (par exemple "UTF-8")
2. Si ce n'est pas UTF-8, cliquez dessus
3. Choisissez "Save with Encoding" (Enregistrer avec l'encodage)
4. Sélectionnez "UTF-8"

**Vérification :**
- L'encodage par défaut de VS Code est normalement UTF-8
- En cas de doute, vérifiez toujours la barre de statut en bas à droite

### 3. Configurer votre serveur web

Votre serveur web devrait aussi envoyer l'en-tête HTTP correct :

```
Content-Type: text/html; charset=utf-8
```

La plupart des hébergeurs modernes le font automatiquement, mais c'est bon à savoir.

## Que se passe-t-il sans UTF-8 ?

### Problème 1 : Caractères cassés

Sans UTF-8 (ou avec un mauvais encodage), vous voyez :

```
❌ Sans UTF-8 ou mal configuré :
"Ã  la boulangerie, on peut acheter des croissants frais Ã  2â‚¬."

✅ Avec UTF-8 :
"À la boulangerie, on peut acheter des croissants frais à 2€."
```

### Problème 2 : Perte d'information

Si quelqu'un enregistre votre page dans le mauvais encodage, les caractères spéciaux peuvent être **définitivement perdus** ou remplacés par des `?` ou `�`.

### Problème 3 : Problèmes de référencement

Les moteurs de recherche ont plus de mal à indexer correctement votre contenu si l'encodage n'est pas spécifié ou est incorrect.

## L'attribut `lang` : Indiquer la langue

### Qu'est-ce que l'attribut `lang` ?

L'attribut `lang` indique la **langue du contenu** d'un élément HTML. Il se place généralement sur la balise `<html>` pour indiquer la langue principale de la page.

```html
<html lang="fr">
```

### Pourquoi c'est important ?

L'attribut `lang` est crucial pour :

#### 1. **L'accessibilité**

Les **lecteurs d'écran** (utilisés par les personnes aveugles ou malvoyantes) utilisent `lang` pour :
- Choisir la bonne voix et prononciation
- Lire correctement les mots
- Adapter les règles de prononciation

**Exemple :**
Sans `lang`, un lecteur d'écran français lirait "Hello world" avec la prononciation française ("Ello vorld"), ce qui serait incompréhensible.

#### 2. **Les moteurs de recherche**

Google et les autres moteurs utilisent `lang` pour :
- Afficher vos pages dans les résultats de recherche du bon pays
- Comprendre le contenu
- Proposer des traductions pertinentes

#### 3. **Les outils de traduction**

Les outils de traduction automatique (Google Translate, DeepL) utilisent `lang` pour savoir quelle langue traduire.

#### 4. **Le style CSS**

Vous pouvez appliquer des styles différents selon la langue :

```css
/* Guillemets français */
:lang(fr) {
    quotes: "« " " »";
}

/* Guillemets anglais */
:lang(en) {
    quotes: """ """;
}
```

### Codes de langue

Les codes de langue suivent la norme **ISO 639-1** (codes à 2 lettres) :

```html
<html lang="fr">    <!-- Français -->
<html lang="en">    <!-- Anglais -->
<html lang="es">    <!-- Espagnol -->
<html lang="de">    <!-- Allemand -->
<html lang="it">    <!-- Italien -->
<html lang="pt">    <!-- Portugais -->
<html lang="ru">    <!-- Russe -->
<html lang="zh">    <!-- Chinois -->
<html lang="ja">    <!-- Japonais -->
<html lang="ar">    <!-- Arabe -->
```

### Codes de langue avec région

Vous pouvez être plus spécifique en ajoutant un code de région (**ISO 3166-1**) :

```html
<html lang="fr-FR">    <!-- Français (France) -->
<html lang="fr-CA">    <!-- Français (Canada) -->
<html lang="fr-BE">    <!-- Français (Belgique) -->
<html lang="fr-CH">    <!-- Français (Suisse) -->

<html lang="en-US">    <!-- Anglais (États-Unis) -->
<html lang="en-GB">    <!-- Anglais (Royaume-Uni) -->
<html lang="en-AU">    <!-- Anglais (Australie) -->

<html lang="es-ES">    <!-- Espagnol (Espagne) -->
<html lang="es-MX">    <!-- Espagnol (Mexique) -->

<html lang="pt-BR">    <!-- Portugais (Brésil) -->
<html lang="pt-PT">    <!-- Portugais (Portugal) -->
```

**Quand utiliser les codes régionaux ?**
- Si votre contenu cible spécifiquement un pays
- Si votre site a des versions différentes par pays
- Pour des raisons de SEO (référencement local)

**Quand s'en passer ?**
- Si votre contenu est générique (pas spécifique à un pays)
- Dans la plupart des cas, le code à 2 lettres suffit

## Utiliser `lang` pour du contenu multilingue

### Langue principale sur `<html>`

La balise `<html>` définit la langue **par défaut** de la page :

```html
<html lang="fr">
```

Tous les éléments héritent de cette langue, sauf indication contraire.

### Changer de langue localement

Vous pouvez indiquer qu'une partie du contenu est dans une autre langue :

```html
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon site bilingue</title>
</head>
<body>
    <h1>Bienvenue sur mon site</h1>

    <p>Ceci est un paragraphe en français.</p>

    <p lang="en">This paragraph is in English.</p>

    <p>Et nous revenons au français.</p>

    <blockquote lang="es">
        Esta cita está en español.
    </blockquote>
</body>
</html>
```

**Avantages :**
- Les lecteurs d'écran changeront automatiquement de prononciation
- Les moteurs de recherche comprendront le contenu mixte
- Les outils de traduction fonctionneront mieux

### Citations et expressions étrangères

Pour les mots ou expressions étrangères, utilisez également `lang` :

```html
<p>
    En français, on dit "bonjour",
    mais en anglais on dit <span lang="en">"hello"</span>
    et en espagnol <span lang="es">"hola"</span>.
</p>

<p>
    Le terme <i lang="la">curriculum vitae</i> vient du latin.
</p>

<p>
    C'est ce qu'on appelle le <i lang="de">Zeitgeist</i> allemand.
</p>
```

### Pages entièrement dans une autre langue

Si vous créez une page entièrement en anglais sur un site français, changez le `lang` de la balise `<html>` :

```html
<!-- Page française -->
<html lang="fr">
    <!-- ... -->
</html>

<!-- Page anglaise -->
<html lang="en">
    <!-- ... -->
</html>
```

## Exemples pratiques

### Exemple 1 : Site français standard

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boulangerie Martin - Pain artisanal</title>
</head>
<body>
    <h1>Boulangerie Martin</h1>
    <p>Nous fabriquons du pain artisanal depuis 1985.</p>
    <p>Prix : croissant à 1,20€</p>
</body>
</html>
```

### Exemple 2 : Blog avec citations en anglais

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog Tech - Derniers articles</title>
</head>
<body>
    <article>
        <h1>L'avenir de l'IA</h1>

        <p>L'intelligence artificielle progresse rapidement.</p>

        <blockquote lang="en">
            <p>"The future is already here – it's just not evenly distributed."</p>
            <cite>William Gibson</cite>
        </blockquote>

        <p>Cette citation illustre parfaitement notre époque.</p>
    </article>
</body>
</html>
```

### Exemple 3 : Site multilingue avec sélecteur

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Entreprise Internationale</title>
</head>
<body>
    <nav>
        <ul>
            <li><a href="index-fr.html" lang="fr">Français</a></li>
            <li><a href="index-en.html" lang="en">English</a></li>
            <li><a href="index-es.html" lang="es">Español</a></li>
        </ul>
    </nav>

    <main>
        <h1>Bienvenue</h1>
        <p>Contenu en français...</p>
    </main>
</body>
</html>
```

### Exemple 4 : Contenu académique avec termes latins

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Article académique</title>
</head>
<body>
    <article>
        <h1>Étude comparative</h1>

        <p>
            Cette recherche s'inscrit dans une démarche
            <i lang="la">a posteriori</i>, c'est-à-dire fondée
            sur l'expérience.
        </p>

        <p>
            Nous utilisons le principe du
            <i lang="la">ceteris paribus</i>
            (toutes choses égales par ailleurs).
        </p>
    </article>
</body>
</html>
```

## Vérification et bonnes pratiques

### Comment vérifier l'encodage dans le navigateur

**Chrome / Edge / Firefox :**
1. Ouvrez les DevTools (F12)
2. Allez dans l'onglet "Network" (Réseau)
3. Rechargez la page (F5)
4. Cliquez sur le document HTML
5. Regardez les "Response Headers" : vous devriez voir `charset=utf-8`

**Alternative simple :**
1. Faites un clic droit sur la page
2. "Afficher le code source" ou "View Page Source"
3. Vérifiez que vous voyez bien `<meta charset="UTF-8">`

### Comment vérifier l'attribut lang

**Méthode 1 : Inspecteur**
1. Ouvrez les DevTools (F12)
2. Inspectez la balise `<html>`
3. Vérifiez l'attribut `lang="fr"`

**Méthode 2 : Validateur W3C**
1. Allez sur https://validator.w3.org/
2. Entrez l'URL de votre page ou collez votre code
3. Le validateur vous avertira si `lang` est manquant

**Méthode 3 : Lecteur d'écran**
Si vous voulez vraiment tester l'accessibilité, utilisez un lecteur d'écran gratuit comme NVDA (Windows) ou VoiceOver (Mac) pour entendre si la prononciation est correcte.

## Liste de vérification (Checklist)

Avant de publier votre page, vérifiez :

✅ **Encodage UTF-8**
- [ ] `<meta charset="UTF-8">` est présent dans le `<head>`
- [ ] Il est placé en **premier** dans le `<head>`
- [ ] Le fichier .html est **sauvegardé en UTF-8** dans votre éditeur
- [ ] Les caractères spéciaux (é, è, à, €, etc.) s'affichent correctement

✅ **Attribut lang**
- [ ] `lang="fr"` (ou autre code) est présent sur `<html>`
- [ ] Le code correspond vraiment à la langue du contenu
- [ ] Les citations en langue étrangère ont leur propre attribut `lang`
- [ ] Les termes techniques étrangers sont marqués avec `lang`

## Erreurs courantes et solutions

### Erreur 1 : Caractères bizarres

**Symptôme :**
```
"CafÃ© ouvert Ã  8h - CroÃ»te dorÃ©e - 2â‚¬"
```

**Causes possibles :**
1. Pas de `<meta charset="UTF-8">`
2. Le fichier n'est pas sauvegardé en UTF-8
3. Le serveur envoie un mauvais en-tête

**Solution :**
1. Ajoutez `<meta charset="UTF-8">` en premier dans le `<head>`
2. Dans VS Code, vérifiez l'encodage (bas à droite) et sauvegardez en UTF-8
3. Rechargez la page avec cache vidé (Ctrl+F5)

### Erreur 2 : Attribut lang oublié

**Symptôme :**
Le validateur W3C signale : "The document has no language defined"

**Solution :**
```html
<!-- ❌ Mauvais -->
<html>

<!-- ✅ Bon -->
<html lang="fr">
```

### Erreur 3 : Mauvais code de langue

**Symptôme :**
Les outils de traduction proposent la mauvaise langue, ou le lecteur d'écran utilise la mauvaise prononciation.

**Solution :**
Vérifiez que vous utilisez le bon code :
```html
<!-- ❌ Mauvais -->
<html lang="french">      <!-- Ce n'est pas un code valide -->
<html lang="FR">          <!-- FR = code pays, pas langue -->

<!-- ✅ Bon -->
<html lang="fr">          <!-- Code ISO 639-1 correct -->
<html lang="fr-FR">       <!-- Avec région si nécessaire -->
```

### Erreur 4 : Charset trop bas dans le head

**Symptôme :**
Des caractères bizarres apparaissent quand même, surtout dans le `<title>` ou les premières lignes.

**Solution :**
```html
<!-- ❌ Mauvais : charset après d'autre contenu -->
<head>
    <title>Café de la gare</title>
    <meta charset="UTF-8">  <!-- Trop tard ! -->
</head>

<!-- ✅ Bon : charset en PREMIER -->
<head>
    <meta charset="UTF-8">  <!-- En premier ! -->
    <title>Café de la gare</title>
</head>
```

### Erreur 5 : Oublier lang sur les sections en langue étrangère

**Symptôme :**
Les lecteurs d'écran prononcent mal les citations en anglais, espagnol, etc.

**Solution :**
```html
<!-- ❌ Mauvais -->
<p>Comme le disait Einstein : "Imagination is more important than knowledge"</p>

<!-- ✅ Bon -->
<p>Comme le disait Einstein : <q lang="en">Imagination is more important than knowledge</q></p>
```

## Impact sur le SEO

### Google et l'encodage

Google privilégie UTF-8 et recommande explicitement de l'utiliser. Un encodage incorrect peut :
- Rendre votre contenu illisible pour les robots
- Entraîner des erreurs d'indexation
- Diminuer votre classement dans les résultats

### Google et l'attribut lang

L'attribut `lang` aide Google à :
- Comprendre dans quelle langue est votre contenu
- Afficher votre page dans les bonnes versions linguistiques de Google
- Proposer votre contenu aux utilisateurs de la bonne région

**Exemple :**
- Une page avec `lang="fr"` sera mieux classée sur google.fr
- Une page avec `lang="en-US"` sera mieux classée sur google.com (USA)

## Cas particuliers

### Les emojis

Les emojis fonctionnent en UTF-8 ! Vous pouvez les utiliser directement :

```html
<p>Bienvenue sur notre site ! 😊</p>
<p>Nous livrons dans toute la France 🇫🇷</p>
<p>Contactez-nous : 📧 contact@site.fr</p>
```

Mais attention :
- Tous les emojis ne sont pas supportés partout
- Leur rendu varie selon le système (Windows, Mac, Android, iOS)
- Utilisez-les avec modération (accessibilité)

### Les caractères spéciaux HTML

Certains caractères ont une signification spéciale en HTML et doivent être échappés :

```html
<!-- ❌ Problématique -->
<p>5 < 10 et 10 > 5</p>

<!-- ✅ Correct avec entités HTML -->
<p>5 &lt; 10 et 10 &gt; 5</p>

<!-- ✅ Ou en UTF-8 dans du contenu textuel -->
<p>Le prix est de 10€ (inférieur à 20€)</p>
```

**Entités HTML courantes :**
```html
&lt;    →  <   (less than)
&gt;    →  >   (greater than)
&amp;   →  &   (ampersand)
&quot;  →  "   (guillemet double)
&copy;  →  ©   (copyright)
&euro;  →  €   (euro)
```

Avec UTF-8, vous pouvez souvent taper directement `©` ou `€`, sauf pour `<`, `>`, et `&` qui ont un sens spécial en HTML.

### Sites multilingues complets

Pour un site vraiment multilingue, utilisez l'attribut `hreflang` dans vos liens :

```html
<head>
    <link rel="alternate" hreflang="fr" href="https://www.site.com/fr/">
    <link rel="alternate" hreflang="en" href="https://www.site.com/en/">
    <link rel="alternate" hreflang="es" href="https://www.site.com/es/">
    <link rel="alternate" hreflang="x-default" href="https://www.site.com/">
</head>
```

Cela aide Google à comprendre les relations entre les versions linguistiques de votre site.

## Récapitulatif : Ce qu'il faut retenir

### UTF-8 : L'encodage universel
- ✅ **Toujours** utiliser UTF-8 en 2025
- ✅ Déclarer `<meta charset="UTF-8">` en **premier** dans le `<head>`
- ✅ Sauvegarder vos fichiers en UTF-8 dans votre éditeur
- ✅ Vérifier que les caractères spéciaux s'affichent correctement

### L'attribut lang : La langue du contenu
- ✅ **Toujours** définir `lang="fr"` (ou autre) sur `<html>`
- ✅ Utiliser les codes ISO 639-1 (2 lettres)
- ✅ Ajouter des codes régionaux si nécessaire (`fr-FR`, `en-US`)
- ✅ Marquer les changements de langue dans le contenu avec `lang`

### Impact
- 🎯 **Accessibilité** : Les lecteurs d'écran fonctionnent correctement
- 🔍 **SEO** : Meilleur référencement dans les moteurs de recherche
- 🌍 **International** : Votre site est vraiment mondial
- 👥 **UX** : Meilleure expérience utilisateur

## Ressources complémentaires

### Documentation officielle
- **Unicode.org** : https://unicode.org/ - Tout sur UTF-8
- **W3C I18N** : https://www.w3.org/International/ - Internationalisation du web
- **MDN Web Docs** : https://developer.mozilla.org/ - Documentation sur `charset` et `lang`

### Outils de test
- **Validateur W3C** : https://validator.w3.org/
- **Test UTF-8** : https://www.w3.org/International/questions/qa-html-encoding-declarations
- **Liste codes de langue** : https://www.loc.gov/standards/iso639-2/php/code_list.php

### Polices et caractères
- **Google Fonts** : https://fonts.google.com/ - Polices qui supportent UTF-8
- **Unicode Table** : https://unicode-table.com/ - Explorer tous les caractères UTF-8

## Conclusion

L'encodage UTF-8 et l'attribut `lang` peuvent sembler être de petits détails techniques, mais ils sont **fondamentaux** pour créer un web moderne, accessible et international.

**Deux lignes de code qui changent tout :**

```html
<html lang="fr">
<head>
    <meta charset="UTF-8">
```

Ces deux éléments garantissent que :
- Votre contenu s'affiche correctement partout
- Votre site est accessible à tous
- Les moteurs de recherche comprennent votre contenu
- Votre site peut évoluer vers le multilinguisme

Prenez l'habitude de **toujours** les inclure dès le début de chaque projet. C'est la marque d'un développeur web professionnel et consciencieux.

Dans la prochaine section, nous verrons comment valider votre HTML et utiliser les DevTools pour inspecter et déboguer votre structure de document.

---

**Section suivante** : [3.1.4 Validation HTML et inspection avec DevTools](./04-validation-html-et-devtools.md)

⏭️ [Validation HTML et inspection avec DevTools](/03-html5-structure-et-semantique/01-fondamentaux-html/04-validation-html-et-devtools.md)
