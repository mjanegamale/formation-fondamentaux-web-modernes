🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 1.2 - Architecture client-serveur et rôle des navigateurs

## Introduction

Avez-vous déjà réfléchi à ce qui se passe réellement quand vous tapez "www.google.com" dans votre navigateur et appuyez sur Entrée ? En quelques millisecondes, une page s'affiche avec son logo coloré et sa barre de recherche. Cette apparente simplicité cache en réalité un processus fascinant que nous allons découvrir ensemble.

Comprendre l'architecture du web est essentiel pour devenir un bon développeur. C'est comme connaître les règles d'un jeu avant d'y jouer : cela vous permet de mieux comprendre pourquoi et comment les choses fonctionnent.

## Le modèle client-serveur : Une conversation permanente

### L'analogie du restaurant

Pour comprendre le modèle client-serveur, imaginons un restaurant :

**Vous (le client)** :
- Vous entrez dans le restaurant
- Vous consultez le menu
- Vous commandez un plat
- Vous attendez
- Vous recevez votre plat
- Vous le consommez

**Le serveur et la cuisine** :
- Le serveur prend votre commande
- Il la transmet en cuisine
- La cuisine prépare le plat
- Le serveur vous l'apporte

Le web fonctionne exactement de la même manière !

### Comment cela fonctionne sur le web

**Le client** (votre ordinateur/smartphone + navigateur) :
- Demande une page web
- Attend la réponse
- Affiche le résultat

**Le serveur** (un ordinateur distant très puissant) :
- Reçoit la demande
- Prépare les données demandées
- Envoie la réponse

```
┌─────────────┐                          ┌─────────────┐
│             │   1. Requête (demande)   │             │
│   CLIENT    │ ───────────────────────> │   SERVEUR   │
│ (Navigateur)│                          │             │
│             │   2. Réponse (page web)  │             │
│             │ <─────────────────────── │             │
└─────────────┘                          └─────────────┘
```

### Un échange constant

Ce qui est important à comprendre, c'est que :

1. **Le client demande, le serveur répond** : Le client ne peut pas recevoir de données sans les avoir demandées en premier.

2. **Chaque page, chaque image est une requête** : Quand vous chargez une page web avec 10 images, votre navigateur fait en réalité 11 requêtes (1 pour la page + 10 pour les images).

3. **Le serveur ne garde pas de "mémoire"** : Chaque requête est indépendante. C'est pour cela que les sites utilisent des cookies pour "se souvenir" de vous.

## Le navigateur : Votre fenêtre sur le web

### Qu'est-ce qu'un navigateur ?

Un **navigateur web** (ou browser en anglais) est un logiciel qui vous permet d'accéder au web et d'afficher des pages internet.

**Les navigateurs les plus courants** :
- **Google Chrome** (le plus utilisé)
- **Firefox** (open source, respectueux de la vie privée)
- **Safari** (sur les appareils Apple)
- **Microsoft Edge** (remplaçant d'Internet Explorer)
- **Opera**, **Brave** (alternatives moins connues mais de qualité)

### Le rôle du navigateur : Un traducteur et interprète

Le navigateur joue plusieurs rôles essentiels :

#### 1. Envoyer des requêtes HTTP

Quand vous cliquez sur un lien ou tapez une adresse, le navigateur envoie une **requête** au serveur pour obtenir la page.

**Exemple** : Quand vous tapez `www.example.com`, votre navigateur envoie une requête qui ressemble à ça :
```
GET /index.html HTTP/1.1
Host: www.example.com
```

Ne vous inquiétez pas pour les détails techniques, retenez simplement que le navigateur "demande poliment" la page au serveur.

#### 2. Recevoir et interpréter le code

Le serveur répond en envoyant du **code** (HTML, CSS, JavaScript). Le navigateur doit alors :

- **Lire le HTML** : Comprendre la structure de la page
- **Appliquer le CSS** : Donner du style (couleurs, tailles, positions)
- **Exécuter le JavaScript** : Rendre la page interactive

**Analogie** : C'est comme si le serveur vous envoyait les plans d'un meuble IKEA (le code), et que le navigateur l'assemblait et le décorait pour vous (l'affichage final).

#### 3. Afficher le résultat visuel

Le navigateur transforme tout ce code en une page belle et fonctionnelle que vous pouvez voir et utiliser.

#### 4. Gérer l'interactivité

Quand vous cliquez sur un bouton, remplissez un formulaire, ou faites défiler la page, c'est le navigateur qui gère ces interactions.

### Le moteur de rendu

Chaque navigateur possède un **moteur de rendu** qui transforme le code en affichage visuel :

- **Blink** (Chrome, Edge, Opera)
- **Gecko** (Firefox)
- **WebKit** (Safari)

**Pourquoi c'est important ?** Parfois, les différents moteurs interprètent le code légèrement différemment. C'est pour cela qu'un site peut avoir un comportement légèrement différent selon le navigateur utilisé. Les développeurs doivent tester leurs sites sur plusieurs navigateurs.

## Le serveur : Le cerveau distant

### Qu'est-ce qu'un serveur ?

Un **serveur web** est un ordinateur puissant, toujours allumé, connecté à internet 24h/24 et 7j/7, qui stocke les sites web et les envoie aux clients qui les demandent.

**Analogie** : Si internet était une ville, les serveurs seraient les bibliothèques, les magasins, les bureaux : des bâtiments qui stockent des informations ou des services et sont toujours ouverts.

### Les missions du serveur

#### 1. Stocker les fichiers du site

Le serveur contient tous les fichiers nécessaires au fonctionnement d'un site :
- Fichiers HTML (structure)
- Fichiers CSS (style)
- Fichiers JavaScript (interactivité)
- Images, vidéos, polices
- Bases de données (pour les contenus dynamiques)

#### 2. Traiter les requêtes

Quand une demande arrive, le serveur doit :
- Comprendre ce qui est demandé
- Vérifier si la ressource existe
- Vérifier les permissions (certains contenus sont protégés)
- Préparer la réponse

#### 3. Envoyer les réponses

Le serveur envoie les fichiers demandés au navigateur, accompagnés d'informations sur la réponse (statut, type de contenu, etc.).

### Types de serveurs

Il existe différents types de serveurs web :

**Serveurs de fichiers statiques** :
- Envoient simplement les fichiers tels quels
- Rapides et simples
- Idéaux pour les sites vitrines

**Serveurs d'applications** :
- Génèrent le contenu dynamiquement
- Communiquent avec des bases de données
- Exécutent du code côté serveur (PHP, Python, Node.js...)
- Nécessaires pour les sites complexes (e-commerce, réseaux sociaux)

## Le protocole HTTP/HTTPS : Le langage de communication

### HTTP : HyperText Transfer Protocol

**HTTP** est le "langage" que parlent les navigateurs et les serveurs pour communiquer. C'est un ensemble de règles qui définit comment les demandes et réponses doivent être formatées.

**Analogie** : C'est comme le français ou l'anglais. Pour que deux personnes communiquent, elles doivent parler la même langue. HTTP est la langue commune du web.

### Structure d'une requête HTTP

Chaque requête contient :

1. **La méthode** : Ce que vous voulez faire
   - `GET` : Récupérer une page (le plus courant)
   - `POST` : Envoyer des données (formulaires)
   - `PUT`, `DELETE`, etc. : Autres actions

2. **L'URL** : L'adresse de ce que vous demandez
   - `https://www.example.com/about.html`

3. **Des en-têtes** (headers) : Informations supplémentaires
   - Type de navigateur
   - Langue préférée
   - Cookies
   - Et bien plus...

### Structure d'une réponse HTTP

La réponse du serveur contient :

1. **Un code de statut** : Le résultat de la demande
   - `200` : OK, tout s'est bien passé ✅
   - `404` : Page non trouvée ❌
   - `500` : Erreur du serveur ⚠️

2. **Des en-têtes** : Informations sur la réponse
   - Type de contenu (HTML, image, etc.)
   - Taille du fichier
   - Date de dernière modification

3. **Le corps** : Le contenu demandé
   - Le code HTML de la page
   - Les données d'une image
   - etc.

### HTTPS : La version sécurisée

**HTTPS** (HTTP Secure) est la version chiffrée d'HTTP. C'est exactement le même protocole, mais les données sont **cryptées** pendant le transfert.

**Pourquoi c'est important ?**
- Protège vos mots de passe
- Protège vos informations bancaires
- Empêche l'espionnage de votre navigation
- Garantit l'authenticité du site

**Comment le reconnaître ?**
- Un cadenas 🔒 dans la barre d'adresse
- L'URL commence par `https://` au lieu de `http://`

> **Bon à savoir** : Aujourd'hui, HTTPS est devenu la norme. Les navigateurs affichent des avertissements pour les sites qui utilisent encore HTTP simple. Si vous créez un site, utilisez toujours HTTPS !

## Le voyage d'une page web : Étape par étape

Voyons maintenant ce qui se passe concrètement quand vous visitez un site web. Prenons l'exemple de `https://www.example.com` :

### Étape 1 : Vous tapez l'URL

Vous tapez `www.example.com` dans votre navigateur et appuyez sur Entrée.

### Étape 2 : Résolution DNS

**DNS** (Domain Name System) est comme un annuaire téléphonique d'internet.

- Votre navigateur ne comprend pas "www.example.com"
- Il a besoin d'une **adresse IP** (ex: `93.184.216.34`)
- Le DNS traduit le nom de domaine en adresse IP
- Cette étape prend quelques millisecondes

**Analogie** : C'est comme quand vous cherchez le numéro de téléphone d'un restaurant dans un annuaire à partir de son nom.

### Étape 3 : Connexion au serveur

Le navigateur établit une connexion avec le serveur situé à l'adresse IP trouvée.

Si le site utilise HTTPS, une "poignée de main" sécurisée (SSL/TLS handshake) s'établit pour chiffrer les communications.

### Étape 4 : Envoi de la requête HTTP

Le navigateur envoie une requête GET pour demander la page d'accueil :

```
GET / HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0...
Accept: text/html...
```

### Étape 5 : Le serveur traite la requête

Le serveur :
- Reçoit et analyse la requête
- Localise le fichier demandé (généralement `index.html`)
- Vérifie les permissions
- Prépare la réponse

### Étape 6 : Le serveur envoie la réponse

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<!DOCTYPE html>
<html>
  <head>
    <title>Example</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>Bienvenue !</h1>
    <img src="logo.png">
    <script src="script.js"></script>
  </body>
</html>
```

### Étape 7 : Le navigateur analyse le HTML

Le navigateur lit le HTML et découvre qu'il a besoin d'autres ressources :
- Un fichier CSS (`style.css`)
- Une image (`logo.png`)
- Un fichier JavaScript (`script.js`)

### Étape 8 : Requêtes supplémentaires

Le navigateur envoie **de nouvelles requêtes** pour chaque ressource :

```
GET /style.css HTTP/1.1
GET /logo.png HTTP/1.1
GET /script.js HTTP/1.1
```

Ces requêtes peuvent être envoyées en parallèle pour accélérer le chargement.

### Étape 9 : Construction et affichage

Le navigateur :
1. Construit l'arbre DOM (structure HTML)
2. Applique le CSS (style)
3. Exécute le JavaScript (interactivité)
4. Affiche le résultat final

### Étape 10 : La page est prête !

Vous voyez maintenant la page complète et pouvez interagir avec elle. Tout ce processus a pris moins d'une seconde !

## Les outils de développement (DevTools)

Tous les navigateurs modernes incluent des **outils de développement** (DevTools) qui permettent de voir "sous le capot" et comprendre comment une page fonctionne.

### L'onglet Network (Réseau)

Cet onglet vous permet de voir :
- Toutes les requêtes HTTP effectuées
- Le temps de chargement de chaque ressource
- La taille des fichiers
- Les codes de statut
- Les en-têtes HTTP

**Comment y accéder ?**
- **Windows/Linux** : F12 ou Ctrl + Shift + I
- **Mac** : Cmd + Option + I
- Ou clic droit > "Inspecter l'élément"

> **Note** : Nous explorerons les DevTools en détail dans la section 2.4 de cette formation. Pour l'instant, retenez simplement qu'ils existent et sont vos meilleurs alliés pour comprendre et débugger vos pages web.

## Cache et performances

### Le cache du navigateur

Pour accélérer la navigation, les navigateurs utilisent un **cache** : ils stockent localement des copies de fichiers déjà téléchargés.

**Avantages** :
- Pages plus rapides à charger
- Moins de données téléchargées
- Moins de requêtes au serveur

**Exemple** :
- Première visite : Le logo de Google est téléchargé
- Visites suivantes : Le logo est chargé depuis le cache local (beaucoup plus rapide !)

### Quand le cache peut poser problème

Parfois, le cache peut afficher une ancienne version d'une page même si elle a été mise à jour sur le serveur.

**Solution** : Forcer le rechargement
- **Windows/Linux** : Ctrl + F5 ou Ctrl + Shift + R
- **Mac** : Cmd + Shift + R

Cela vide le cache et re-télécharge tout depuis le serveur.

## Sites statiques vs sites dynamiques

### Sites statiques

**Définition** : Le contenu est fixe. Les fichiers HTML sont créés à l'avance et ne changent pas.

**Caractéristiques** :
- Rapides à charger
- Simples à héberger
- Pas de base de données
- Tous les visiteurs voient le même contenu

**Exemples** :
- Portfolio personnel
- Documentation
- Site vitrine d'entreprise

**Technologies** : HTML, CSS, JavaScript (côté client uniquement)

### Sites dynamiques

**Définition** : Le contenu est généré à la volée par le serveur en fonction de divers paramètres.

**Caractéristiques** :
- Contenu personnalisé pour chaque utilisateur
- Interaction avec une base de données
- Gestion d'utilisateurs et de sessions
- Contenu qui évolue en temps réel

**Exemples** :
- Réseaux sociaux (Facebook, Twitter)
- E-commerce (Amazon)
- Webmails (Gmail)
- Applications web complexes

**Technologies** : HTML, CSS, JavaScript + PHP/Python/Node.js + Base de données

### Le meilleur des deux mondes

Aujourd'hui, de nombreux sites sont des **hybrides** :
- Structure statique pour les performances
- Éléments dynamiques chargés avec JavaScript
- C'est ce qu'on appelle les **Single Page Applications (SPA)**

## Comprendre les URLs

### Anatomie d'une URL

Décortiquons une URL complète :

```
https://www.example.com:443/blog/article-1?lang=fr&theme=dark#section-2
```

1. **Protocole** : `https://`
   - Comment communiquer avec le serveur

2. **Sous-domaine** : `www`
   - Subdivision optionnelle du domaine

3. **Domaine** : `example.com`
   - L'adresse principale du site

4. **Port** : `:443`
   - Généralement caché (80 pour HTTP, 443 pour HTTPS)
   - Le "numéro de porte" du serveur

5. **Chemin** : `/blog/article-1`
   - L'emplacement de la ressource sur le serveur

6. **Paramètres de requête** : `?lang=fr&theme=dark`
   - Informations supplémentaires envoyées au serveur
   - Commence par `?`, séparés par `&`

7. **Fragment** : `#section-2`
   - Ancre vers une section spécifique de la page
   - Traité côté client, pas envoyé au serveur

### URLs relatives vs absolues

**URL absolue** : L'adresse complète
```
https://www.example.com/images/logo.png
```

**URL relative** : Par rapport à la page actuelle
```
images/logo.png
../style.css
/contact.html
```

Les URLs relatives sont très utilisées dans le développement web pour lier les ressources d'un même site.

## Cookies et stockage local

### Les cookies

Les **cookies** sont de petits fichiers texte stockés par le navigateur pour "se souvenir" d'informations.

**Utilisations** :
- Garder l'utilisateur connecté
- Mémoriser les préférences (langue, thème)
- Suivre l'activité (analytics, publicité)

**Important** : Les cookies sont envoyés automatiquement à chaque requête vers le domaine qui les a créés.

### Le stockage local (localStorage/sessionStorage)

Plus moderne que les cookies, le stockage local permet de sauvegarder des données directement dans le navigateur :

- **localStorage** : Données persistantes (restent même après fermeture du navigateur)
- **sessionStorage** : Données temporaires (disparaissent à la fermeture de l'onglet)

Nous verrons comment utiliser ces technologies dans la partie JavaScript de cette formation.

## Points clés à retenir

✅ **Le web fonctionne selon le modèle client-serveur** : Le client demande, le serveur répond

✅ **Le navigateur est un interprète** : Il transforme le code (HTML, CSS, JS) en pages visuelles

✅ **HTTP/HTTPS est le protocole de communication** : HTTPS est la version sécurisée

✅ **Chaque ressource nécessite une requête** : Une page avec 10 images = 11 requêtes

✅ **Le DNS traduit les noms de domaine en adresses IP** : C'est l'annuaire d'internet

✅ **Le cache accélère la navigation** : Le navigateur stocke des copies locales

✅ **Les sites peuvent être statiques ou dynamiques** : Selon qu'ils génèrent du contenu à la volée ou non

✅ **Les DevTools vous permettent de tout voir** : Requêtes, réponses, temps de chargement

## Analogie finale : La lettre postale

Pour résumer, pensez au web comme à un système postal :

- **Vous (le client)** : Vous écrivez une lettre (requête HTTP) demandant une information
- **L'adresse (URL)** : Vous indiquez où envoyer la lettre
- **Le système postal (Internet)** : Achemine votre lettre
- **Le destinataire (le serveur)** : Reçoit votre lettre, cherche l'information demandée
- **La réponse** : Le serveur vous renvoie une lettre avec l'information (réponse HTTP)
- **Votre boîte aux lettres (navigateur)** : Reçoit et vous présente joliment le contenu

La seule différence ? Tout cela se passe en quelques millisecondes au lieu de plusieurs jours !

---

**Prochaine étape** : [1.3 - Les trois piliers du web : HTML, CSS, JavaScript](./03-les-trois-piliers-du-web.md)

Maintenant que vous comprenez comment le web fonctionne "en coulisses", nous allons découvrir les trois technologies fondamentales qui composent toutes les pages web : HTML, CSS et JavaScript.

⏭️ [Les trois piliers du web : HTML, CSS, JavaScript](/01-introduction-au-developpement-web/03-les-trois-piliers-du-web.md)
