🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.2.2 Onglet Network et Analyse des Requêtes

## Introduction

Chaque fois que vous visitez un site web, votre navigateur envoie des **dizaines (voire centaines) de requêtes** pour récupérer des données : HTML, CSS, JavaScript, images, polices, API, etc.

L'**onglet Network** des DevTools est votre **panneau de contrôle** pour voir toutes ces requêtes en temps réel. Il vous permet de comprendre ce qui est téléchargé, combien de temps ça prend, et surtout, **ce qui ralentit votre site**.

C'est l'outil indispensable pour optimiser la vitesse de chargement et diagnostiquer les problèmes réseau !

---

## Pourquoi l'onglet Network est crucial ?

### Les requêtes réseau = Goulot d'étranglement principal

**Statistique** : Le temps de chargement d'un site web est souvent déterminé à **70-80% par les requêtes réseau**, pas par le code JavaScript ou CSS.

**Exemples concrets** :
- 🖼️ Une image de 3 MB non optimisée → +2 secondes de chargement
- 🌐 50 requêtes au lieu de 10 → +1.5 secondes
- 🐌 Un serveur lent (500ms de latence) → Chaque requête est pénalisée
- 📦 Fichiers non compressés → 3× plus de données à télécharger

### Ce que vous pouvez découvrir

L'onglet Network révèle :
- 📊 **Combien de requêtes** sont effectuées
- ⏱️ **Combien de temps** prend chaque requête
- 📦 **Combien de données** sont téléchargées
- 🔍 **Quelles requêtes échouent** (404, 500, timeout...)
- 🚦 **L'ordre de chargement** des ressources
- 🐌 **Les goulots d'étranglement** de performance

---

## Accéder à l'onglet Network

### Ouvrir les DevTools

1. **F12** (Windows/Linux) ou **Cmd+Option+I** (Mac)
2. Ou clic droit → **Inspecter**
3. Cliquez sur l'onglet **"Network"**

### Première utilisation

À l'ouverture, vous verrez probablement :
```
⚠️ Enregistrement en cours. Rechargez la page pour voir les requêtes.
```

**Important** : L'onglet Network n'enregistre que **pendant qu'il est ouvert**. Si vous ouvrez les DevTools après le chargement de la page, vous ne verrez pas les requêtes déjà effectuées.

**Solution** : **Rechargez la page** (F5 ou Ctrl+R) avec l'onglet Network ouvert.

---

## Interface de l'onglet Network

### Vue d'ensemble

```
┌─────────────────────────────────────────────────────────┐
│ 🔴 ⚫ 🗑️ 🔍 [Filtres: All XHR JS CSS Img...]            │ ← Barre d'outils
├─────────────────────────────────────────────────────────┤
│ Name          Status  Type    Size    Time   Waterfall  │ ← En-têtes
├─────────────────────────────────────────────────────────┤
│ index.html    200     doc     5.2kB   125ms  ████       │
│ style.css     200     css     15kB    89ms   ░░███      │
│ script.js     200     js      48kB    156ms  ░░░░████   │
│ logo.png      200     img     125kB   234ms  ░░░░░████  │
│ api/users     200     xhr     2.1kB   345ms  ░░░░░░███  │
└─────────────────────────────────────────────────────────┘
│ 🔵 15 requests  |  195 kB transferred  |  1.2s loaded   │ ← Résumé
└─────────────────────────────────────────────────────────┘
```

### Barre d'outils (en haut)

**Icônes principales** :
- 🔴 **Record** : Active/désactive l'enregistrement (rouge = actif)
- ⚫ **Clear** : Efface toutes les requêtes affichées
- 🗑️ **Preserve log** : Garde les requêtes lors de la navigation entre pages
- 🔍 **Filter** : Recherche par nom de fichier ou URL
- ⚙️ **Settings** : Options avancées

**Filtres rapides** :
- **All** : Toutes les requêtes
- **Fetch/XHR** : Requêtes API (fetch, XMLHttpRequest)
- **JS** : Fichiers JavaScript
- **CSS** : Fichiers CSS
- **Img** : Images
- **Media** : Audio/Vidéo
- **Font** : Polices
- **Doc** : Documents HTML
- **WS** : WebSockets
- **Wasm** : WebAssembly
- **Manifest** : Fichiers manifest
- **Other** : Autres types

---

## Comprendre les colonnes

### Name (Nom)

**Ce que ça montre** : Le nom du fichier ou l'URL de la requête

**Exemples** :
```
logo.png
https://api.example.com/users/42
fonts/roboto.woff2
```

**Icônes** :
- 📄 Document HTML
- 🎨 CSS
- ⚙️ JavaScript
- 🖼️ Image
- 🔤 Police

**Cliquez dessus** : Ouvre les détails de la requête (voir plus bas)

### Status (Statut)

**Ce que ça montre** : Code de statut HTTP de la réponse

**Codes courants** :

**2xx - Succès** ✅
- **200 OK** : Tout va bien, ressource récupérée
- **204 No Content** : Succès mais pas de contenu à retourner
- **206 Partial Content** : Contenu partiel (streaming)

**3xx - Redirection** 🔄
- **301 Moved Permanently** : Redirection permanente
- **302 Found** : Redirection temporaire
- **304 Not Modified** : Ressource en cache, pas de téléchargement

**4xx - Erreur client** ⚠️
- **400 Bad Request** : Requête mal formée
- **401 Unauthorized** : Authentification requise
- **403 Forbidden** : Accès interdit
- **404 Not Found** : Ressource introuvable
- **429 Too Many Requests** : Trop de requêtes

**5xx - Erreur serveur** ❌
- **500 Internal Server Error** : Erreur du serveur
- **502 Bad Gateway** : Problème de passerelle
- **503 Service Unavailable** : Service indisponible
- **504 Gateway Timeout** : Timeout de passerelle

**Couleurs dans DevTools** :
- Noir/Gris : 2xx, 3xx (normal)
- Rouge : 4xx, 5xx (erreur)

### Type

**Ce que ça montre** : Type MIME de la ressource

**Valeurs courantes** :
- **document** : HTML
- **stylesheet** : CSS
- **script** : JavaScript
- **xhr** : Requête AJAX/Fetch
- **image** : Image (jpeg, png, webp, svg...)
- **font** : Police (woff, woff2, ttf...)
- **media** : Audio/Vidéo

### Size (Taille)

**Ce que ça montre** : Deux valeurs importantes

**Format** : `[taille transférée] / [taille réelle]`

**Exemples** :
```
45 kB / 150 kB  → Compressé (bien !)
150 kB / 150 kB → Non compressé
(from cache)    → Chargé depuis le cache (excellent !)
(disk cache)    → Cache disque
(memory cache)  → Cache mémoire
```

**Interprétation** :
- Grande différence = compression efficace (gzip, brotli)
- Tailles égales = pas de compression (à améliorer)
- "from cache" = ressource pas retéléchargée (très rapide)

### Time (Temps)

**Ce que ça montre** : Durée totale de la requête (en millisecondes)

**Exemples** :
```
23 ms   → Très rapide ✅
150 ms  → Acceptable 👌
500 ms  → Lent ⚠️
2.5 s   → Très lent ❌
```

**Facteurs d'influence** :
- Latence réseau (ping)
- Taille de la ressource
- Vitesse du serveur
- Compression

### Waterfall (Cascade)

**Ce que ça montre** : Chronologie visuelle de la requête

```
Waterfall
│
│ ░░░░████████░░  ← Chaque barre = une phase
│
└───────────────→ Temps
```

**Segments colorés** (nous détaillerons plus bas) :
- **Gris clair** : Queuing (en attente)
- **Gris** : Stalled (bloqué)
- **Orange** : DNS Lookup (résolution DNS)
- **Orange foncé** : Initial Connection (connexion TCP)
- **Violet** : SSL/TLS (négociation sécurisée)
- **Vert** : Request Sent (envoi de la requête)
- **Bleu** : Waiting (TTFB - Time To First Byte)
- **Vert clair** : Content Download (téléchargement)

---

## Effectuer une analyse complète

### Étape 1 : Charger la page

1. **Ouvrez l'onglet Network**
2. **Activez "Preserve log"** (case à cocher) pour garder l'historique
3. **Cliquez sur "Clear"** 🗑️ pour repartir de zéro
4. **Rechargez la page** (F5 ou Ctrl+R)
5. **Attendez** que tout soit chargé (spinner disparu)

### Étape 2 : Observer le résumé

En bas de l'onglet, vous voyez :
```
🔵 45 requests | 2.3 MB transferred | 1.8 MB resources | Finish: 3.2s | DOMContentLoaded: 1.5s | Load: 2.8s
```

**Interprétation** :

**45 requests** : Nombre de requêtes HTTP
- ✅ Moins de 50 : Bon
- ⚠️ 50-100 : À optimiser
- ❌ Plus de 100 : Trop !

**2.3 MB transferred** : Données réellement téléchargées (après compression)
- ✅ Moins de 1 MB : Excellent
- ⚠️ 1-3 MB : Acceptable
- ❌ Plus de 3 MB : Lourd

**1.8 MB resources** : Taille réelle des ressources (avant compression)
- Différence avec "transferred" = efficacité de la compression

**Finish: 3.2s** : Temps total jusqu'à la dernière requête
- ✅ Moins de 3s : Bon
- ⚠️ 3-5s : Moyen
- ❌ Plus de 5s : Lent

**DOMContentLoaded: 1.5s** : Temps jusqu'à ce que le HTML et CSS soient chargés
- ✅ Moins de 2s : Bon

**Load: 2.8s** : Temps jusqu'à ce que TOUTES les ressources soient chargées
- ✅ Moins de 3s : Bon

### Étape 3 : Identifier les problèmes visuels

**Regardez le Waterfall** : Cherchez ces patterns problématiques :

```
❌ MAUVAIS : Requêtes très longues
│ ████████████████████████████  ← 2 secondes !
│ ██
│ ███

✅ BON : Requêtes courtes et parallèles
│ ███
│ ███
│ ████
│ ██
```

**Problèmes à repérer** :
- 🔴 **Barres très longues** : Ressources lentes
- 🔴 **Beaucoup de gris** : Temps d'attente (latence)
- 🔴 **Cascade séquentielle** : Pas de parallélisation
- 🔴 **Status rouge** : Erreurs (404, 500)

### Étape 4 : Trier pour analyser

**Cliquez sur l'en-tête d'une colonne** pour trier :

**Trier par Time (décroissant)** :
```
logo.jpg      2.3s  ← Plus lent en premier
video.mp4     1.8s
script.js     850ms
style.css     120ms
```
→ Identifie les ressources les plus lentes

**Trier par Size (décroissant)** :
```
video.mp4     8.5 MB  ← Plus lourd en premier
bundle.js     2.1 MB
logo.jpg      850 kB
style.css     45 kB
```
→ Identifie les ressources les plus lourdes

**Trier par Name (alphabétique)** :
→ Grouper les fichiers similaires

---

## Analyser une requête en détail

### Cliquer sur une requête

**Cliquez sur n'importe quelle requête** dans la liste → Un panneau s'ouvre avec plusieurs onglets.

### Onglet Headers (En-têtes)

**Ce que ça montre** : Toutes les métadonnées de la requête/réponse

```
General
━━━━━━━
Request URL: https://api.example.com/users/42
Request Method: GET
Status Code: 200 OK
Remote Address: 192.168.1.1:443
```

**Sections importantes** :

#### 1. General (Général)
- **Request URL** : URL complète
- **Request Method** : GET, POST, PUT, DELETE, etc.
- **Status Code** : Code de statut HTTP
- **Remote Address** : Adresse IP du serveur

#### 2. Response Headers (En-têtes de réponse)
```
Content-Type: application/json
Content-Length: 1234
Content-Encoding: gzip        ← Compression activée ✅
Cache-Control: max-age=3600   ← Cache 1 heure ✅
```

**Headers importants pour la performance** :
- **Content-Encoding: gzip** : Compression activée (bien !)
- **Cache-Control** : Directives de cache
- **ETag** : Identifiant de version (pour le cache)
- **Last-Modified** : Date de dernière modification

#### 3. Request Headers (En-têtes de requête)
```
Accept: application/json
User-Agent: Mozilla/5.0...
Cookie: session=abc123...
Authorization: Bearer token...
```

**Headers utiles pour débugger** :
- **Accept** : Types de contenu acceptés
- **Cookie** : Cookies envoyés
- **Authorization** : Token d'authentification
- **Referer** : Page d'origine

### Onglet Preview (Aperçu)

**Ce que ça montre** : Aperçu formaté de la réponse

**Pour JSON** :
```json
{
  "id": 42,
  "nom": "Alice",
  "email": "alice@example.com",
  "actif": true
}
```
→ Arbre dépliable, facile à lire

**Pour HTML** :
→ Rendu visuel de la page

**Pour Images** :
→ Affichage de l'image avec dimensions

### Onglet Response (Réponse)

**Ce que ça montre** : Contenu brut de la réponse

```
{"id":42,"nom":"Alice","email":"alice@example.com"}
```

**Utilité** : Voir le contenu exact, copier la réponse

**Bouton Copy** : Copier la réponse dans le presse-papiers

### Onglet Timing (Chronométrage)

**Ce que ça montre** : Décomposition du temps de la requête

```
Timing
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Queueing            0.5 ms   ← Temps d'attente dans la file
Stalled            15.2 ms   ← Bloqué (limite de connexions)
DNS Lookup         12.3 ms   ← Résolution du nom de domaine
Initial Connection 45.8 ms   ← Établissement de la connexion TCP
SSL                89.2 ms   ← Négociation SSL/TLS (HTTPS)
Request Sent        0.3 ms   ← Envoi de la requête
Waiting (TTFB)    234.5 ms   ← Attente de la première réponse
Content Download   12.1 ms   ← Téléchargement du contenu
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total:            409.9 ms
```

**Analyse phase par phase** :

#### Queueing (File d'attente)
- **Cause** : Navigateur limite le nombre de connexions simultanées
- **Problème si long** : Trop de requêtes en même temps
- **Solution** : Réduire le nombre de requêtes

#### Stalled (Bloqué)
- **Cause** : Attente d'une connexion disponible
- **Problème si long** : Limite de connexions atteinte (6 par domaine)
- **Solution** : Utiliser un CDN (autre domaine), HTTP/2

#### DNS Lookup (Résolution DNS)
- **Cause** : Conversion du nom de domaine en IP
- **Problème si long** : DNS lent
- **Solution** : DNS prefetch, utiliser un DNS rapide (1.1.1.1, 8.8.8.8)

#### Initial Connection (Connexion initiale)
- **Cause** : Établissement de la connexion TCP (handshake)
- **Problème si long** : Latence réseau élevée
- **Solution** : CDN géographiquement proche, Keep-Alive

#### SSL (Négociation SSL/TLS)
- **Cause** : Sécurisation HTTPS
- **Problème si long** : Certificat lourd, protocole ancien
- **Solution** : HTTP/2, TLS 1.3, OCSP Stapling

#### Request Sent (Requête envoyée)
- **Cause** : Envoi des données de la requête
- **Problème si long** : Requête très grande (POST avec beaucoup de données)
- **Solution** : Réduire la taille des données envoyées

#### Waiting (TTFB - Time To First Byte)
- **Cause** : Temps de traitement côté serveur
- **Problème si long** : Serveur lent, requête complexe
- **Solution** : Optimiser le serveur, cache côté serveur, CDN

#### Content Download (Téléchargement)
- **Cause** : Téléchargement du contenu
- **Problème si long** : Fichier trop lourd, bande passante faible
- **Solution** : Compresser, optimiser les images, utiliser WebP

**Règle générale** :
- **Waiting (TTFB) > 500ms** : Problème serveur
- **DNS + Connection + SSL > 200ms** : Problème de latence/connexion
- **Content Download très long** : Fichier trop lourd

### Onglet Cookies

**Ce que ça montre** : Cookies envoyés et reçus

```
Request Cookies
━━━━━━━━━━━━━━
session    abc123xyz
user_prefs lang=fr

Response Cookies
━━━━━━━━━━━━━━━
new_token  def456uvw
```

### Onglet Initiator (Initiateur)

**Ce que ça montre** : Qui a déclenché cette requête

```
Initiated by:
script.js:42
  └─ fonction chargerUtilisateurs()
```

**Utilité** : Tracer l'origine d'une requête dans votre code

---

## Le Waterfall Chart en détail

### Comprendre le graphique en cascade

Le **Waterfall Chart** est la visualisation la plus importante de l'onglet Network.

```
│ Name           Waterfall
├────────────────────────────────────────────────
│ index.html     ████░░░░░░░░░
│ style.css          ██████░░░
│ script.js          ████████░░░░
│ logo.png               ████████░
│ font.woff2                 ██████░
│ api/users                      ███████░░░░░
└────────────────────────────────────────────────
  0s         1s         2s         3s
```

**Lecture** :
- **Axe horizontal** : Temps (de gauche à droite)
- **Position** : Quand la requête commence
- **Longueur** : Durée de la requête
- **Couleurs** : Phases (DNS, connexion, téléchargement...)

### Patterns à identifier

#### Pattern 1 : Cascade séquentielle (Mauvais)

```
│ index.html     ████
│ style.css              ████
│ script.js                      ████
│ image.jpg                              ████
```

**Problème** : Les requêtes sont **séquentielles** (l'une après l'autre)

**Cause** :
- Fichiers chargés par ordre de découverte dans le HTML
- `<script>` bloquants
- Dépendances en chaîne

**Solution** :
- `async` ou `defer` sur les scripts
- Précharger les ressources critiques (`<link rel="preload">`)
- HTTP/2 pour multiplexing

#### Pattern 2 : Requêtes parallèles (Bon)

```
│ style.css      ████
│ script.js      ████
│ logo.png       ████
│ font.woff2     ████
```

**Avantage** : Plusieurs ressources téléchargées **en même temps**

**Comment** : Le navigateur parallélise automatiquement (6 connexions par domaine)

#### Pattern 3 : Long TTFB (Mauvais)

```
│ api/data       ░░░░░░░░░░░░░░░░████
                 └─ Attente ───┘ DL
```

**Problème** : Longue attente avant la première réponse (barre bleue longue)

**Cause** : Serveur lent, requête complexe, BDD lente

**Solution** : Optimiser le backend, cache serveur, CDN

#### Pattern 4 : Gros téléchargement (Mauvais)

```
│ video.mp4      █████████████████████████████████
```

**Problème** : Téléchargement très long (barre verte longue)

**Cause** : Fichier trop volumineux

**Solution** : Compresser, optimiser, lazy loading, streaming

#### Pattern 5 : Requêtes bloquées (Mauvais)

```
│ file1.js       ░░░░░░░░░░████
│ file2.js       ░░░░░░░░░░████
│ file3.js       ░░░░░░░░░░████
                 └ Stalled ┘
```

**Problème** : Beaucoup de temps "Stalled" (gris)

**Cause** : Limite de connexions atteinte (6 par domaine en HTTP/1.1)

**Solution** : HTTP/2, utiliser un CDN (domaine différent), réduire le nombre de requêtes

---

## Filtrer et rechercher

### Utiliser les filtres rapides

**Cliquez sur un type** pour filtrer :
- **XHR** : Voir uniquement les appels API
- **JS** : Voir uniquement les fichiers JavaScript
- **Img** : Voir uniquement les images

**Exemple d'utilisation** :
1. Cliquez sur **"Img"**
2. Triez par **"Size"** (décroissant)
3. Identifiez les images les plus lourdes à optimiser

### Recherche textuelle

**Dans la barre de recherche** 🔍 :
```
logo          → Trouve toutes les requêtes contenant "logo"
status:404    → Trouve toutes les erreurs 404
method:POST   → Trouve toutes les requêtes POST
domain:api    → Trouve les requêtes vers un domaine contenant "api"
larger-than:1M → Trouve les fichiers > 1 MB
```

**Opérateurs utiles** :
- `status:code` : Filtrer par code de statut
- `method:METHOD` : Filtrer par méthode HTTP
- `domain:texte` : Filtrer par domaine
- `larger-than:taille` : Fichiers plus grands que
- `smaller-than:taille` : Fichiers plus petits que
- `-terme` : Exclure (ex: `-status:200` = tout sauf 200)

### Filtres avancés

**Clic droit sur une requête** → Options de filtrage :
- **Block request URL** : Bloquer cette URL
- **Block request domain** : Bloquer tout le domaine
- **Copy** → **Copy as fetch** : Copier la requête comme code fetch()

---

## Simuler des conditions réseau

### Network Throttling (Limitation réseau)

**Pourquoi ?** Votre connexion de développeur est rapide. Vos utilisateurs ont souvent du 3G ou 4G.

**Activer le throttling** :

1. Trouvez le menu déroulant (par défaut : "No throttling")
2. Sélectionnez un profil :
   - **Fast 3G** : ~1.6 Mbps (mobile courant)
   - **Slow 3G** : ~400 Kbps (mobile lent)
   - **Offline** : Aucune connexion (tester mode hors ligne)
   - **Custom** : Créer votre propre profil

**Profils prédéfinis** :
```
Fast 3G
- Download: 1.6 Mbps
- Upload: 750 Kbps
- Latency: 150ms

Slow 3G
- Download: 400 Kbps
- Upload: 400 Kbps
- Latency: 2000ms (2 secondes!)
```

**Utilisation** :
1. Activez **"Fast 3G"**
2. Rechargez la page
3. Observez le temps de chargement

**Révélateur** : Votre site qui charge en 1s chez vous peut prendre 10s en 3G !

### Créer un profil personnalisé

1. Sélectionnez **"Add..."** dans le menu
2. Configurez :
   - **Download** : Vitesse de téléchargement (kbps ou Mbps)
   - **Upload** : Vitesse d'envoi
   - **Latency** : Délai (ms)

**Exemple pour simuler un réseau d'entreprise** :
- Download: 10 Mbps
- Upload: 2 Mbps
- Latency: 50ms

---

## Cas pratiques d'analyse

### Cas 1 : Page qui charge lentement

**Symptôme** : La page met 8 secondes à charger

**Analyse** :

1. **Ouvrez Network** et rechargez
2. **Regardez le résumé** : `180 requests | 5.8 MB | 8.2s`
3. **Triez par Size** (décroissant)

**Découverte** :
```
video-bg.mp4    4.2 MB  ← 72% du poids total !
hero.jpg        800 KB
script.js       450 KB
```

**Problème identifié** : Vidéo de fond non optimisée

**Solutions** :
- ✅ Compresser la vidéo
- ✅ Utiliser un format plus léger (WebM)
- ✅ Lazy loading (charger après le reste)
- ✅ Proposer une image de placeholder
- ✅ Héberger sur un CDN vidéo

### Cas 2 : Trop de requêtes

**Symptôme** : 150 requêtes pour une simple page

**Analyse** :

1. **Filtrez par type** : Img
2. **Comptez** : 85 images !

**Découverte** :
```
icon-1.png   2 KB
icon-2.png   2 KB
icon-3.png   2 KB
... (85 fichiers similaires)
```

**Problème** : Beaucoup de petits fichiers

**Solutions** :
- ✅ **Sprite sheets** : Combiner les icônes en une seule image
- ✅ **Icon fonts** : Utiliser Font Awesome ou similaire
- ✅ **SVG inline** : Intégrer les SVG dans le HTML
- ✅ **HTTP/2** : Permet plus de requêtes parallèles

### Cas 3 : API lente

**Symptôme** : L'interface freeze pendant 3 secondes

**Analyse** :

1. **Filtrez par XHR**
2. **Regardez le Waterfall**

**Découverte** :
```
api/dashboard  ░░░░░░░░░░░░░░░░░░░░████
               └── Waiting 2.8s ──┘ DL
```

**Détails Timing** :
```
Waiting (TTFB): 2.8s  ← Serveur très lent !
```

**Problème** : Backend trop lent

**Solutions** :
- ✅ Optimiser la requête SQL côté serveur
- ✅ Ajouter un cache serveur (Redis)
- ✅ Paginer les résultats
- ✅ Ajouter un index en base de données
- ✅ Utiliser un CDN pour l'API

### Cas 4 : Erreurs 404

**Symptôme** : Des ressources n'ont pas l'air de charger

**Analyse** :

1. **Recherchez** : `status:404`
2. **Identifiez les fichiers manquants**

**Découverte** :
```
font-awesome.woff2   404
old-script.js        404
deleted-image.png    404
```

**Problème** : Références à des fichiers supprimés

**Solutions** :
- ✅ Supprimer les références dans le HTML/CSS
- ✅ Vérifier les chemins (relatif vs absolu)
- ✅ Uploader les fichiers manquants

### Cas 5 : CORS errors

**Symptôme** : Erreurs dans la console sur les requêtes API

**Analyse dans Network** :

```
api/data    (failed)  CORS error
```

**Détails Headers** :
```
Access-Control-Allow-Origin: (absent)
```

**Problème** : Le serveur n'autorise pas les requêtes cross-origin

**Solutions** :
- ✅ Configurer CORS sur le serveur
- ✅ Ajouter l'en-tête `Access-Control-Allow-Origin: *`
- ✅ Utiliser un proxy en développement

---

## Export et partage

### Exporter un enregistrement HAR

**HAR = HTTP Archive** : Format standard pour sauvegarder les requêtes réseau

**Comment exporter** :

1. Clic droit dans l'onglet Network
2. Sélectionnez **"Save all as HAR with content"**
3. Sauvegardez le fichier `.har`

**Utilité** :
- Partager avec des collègues
- Analyser hors ligne
- Comparer avant/après optimisations
- Debugger en équipe

### Importer un HAR

1. Glissez-déposez un fichier `.har` dans l'onglet Network
2. Ou : Clic droit → **"Import HAR file..."**

### Copier une requête

**Clic droit sur une requête** → **Copy** → Plusieurs options :

**Copy as fetch** :
```javascript
fetch("https://api.example.com/users/42", {
  "headers": {
    "accept": "application/json",
    "authorization": "Bearer token..."
  },
  "method": "GET"
});
```
→ Code JavaScript prêt à coller dans la console !

**Copy as cURL** :
```bash
curl 'https://api.example.com/users/42' \
  -H 'accept: application/json' \
  -H 'authorization: Bearer token...'
```
→ Commande terminal pour reproduire la requête

**Copy URL** : Copie juste l'URL

**Copy response** : Copie le contenu de la réponse

---

## Bloquer des requêtes

### Pourquoi bloquer ?

Pour tester :
- Comment le site réagit si une ressource ne charge pas
- L'impact de scripts tiers (analytics, pub)
- Les fallbacks et gestion d'erreurs

### Bloquer une requête spécifique

1. **Clic droit** sur la requête
2. **"Block request URL"**
3. Une icône 🚫 apparaît
4. Rechargez → Cette requête échouera (status: failed)

### Bloquer un domaine entier

1. **Clic droit** sur une requête du domaine
2. **"Block request domain"**
3. Toutes les requêtes vers ce domaine échoueront

**Exemple d'utilisation** :
Bloquer Google Analytics pour tester le site sans tracking.

### Voir les requêtes bloquées

**Cliquez sur l'icône ⚙️** → **"Network request blocking"**

Liste des règles de blocage :
```
URL pattern                         Enabled
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
*google-analytics.com*              ☑
*facebook.com*                      ☑
https://cdn.example.com/old.js      ☑
```

**Décochez** pour réactiver temporairement

---

## Astuces et bonnes pratiques

### ✅ À faire

1. **Toujours tester avec throttling**
   - Votre connexion ≠ celle des utilisateurs
   - Fast 3G minimum pour les tests

2. **Activer "Preserve log"**
   - Garde l'historique lors de la navigation
   - Essentiel pour tracer les redirections

3. **Utiliser les filtres**
   - XHR pour débugger les API
   - Img pour optimiser les images
   - Status:404 pour trouver les erreurs

4. **Analyser le Timing**
   - TTFB long → Problème serveur
   - Content Download long → Fichier lourd
   - Stalled/Queueing long → Trop de requêtes

5. **Exporter des HAR pour comparaison**
   - Avant optimisation
   - Après optimisation
   - Mesurer l'amélioration

### ❌ À éviter

1. **Ne pas tester uniquement en local**
   - Latence locale = 0ms (irréaliste)
   - Testez sur un serveur de staging

2. **Ne pas ignorer les petits fichiers**
   - 100 fichiers de 1 KB = 100 requêtes
   - Impact > 1 fichier de 100 KB

3. **Ne pas oublier les erreurs**
   - 404, 500 = ressources qui ralentissent
   - Cherchez le rouge dans Status

4. **Ne pas optimiser sans mesurer**
   - Toujours comparer avant/après
   - Utilisez les HAR exports

---

## Indicateurs de performance réseau

### Objectifs à viser

**Nombre de requêtes** :
- ✅ Excellent : < 25 requêtes
- 👌 Bon : 25-50 requêtes
- ⚠️ Moyen : 50-100 requêtes
- ❌ Mauvais : > 100 requêtes

**Poids total transféré** :
- ✅ Excellent : < 500 KB
- 👌 Bon : 500 KB - 1 MB
- ⚠️ Moyen : 1-3 MB
- ❌ Mauvais : > 3 MB

**Temps de chargement total** :
- ✅ Excellent : < 2s
- 👌 Bon : 2-3s
- ⚠️ Moyen : 3-5s
- ❌ Mauvais : > 5s

**TTFB (Time To First Byte)** :
- ✅ Excellent : < 200ms
- 👌 Bon : 200-500ms
- ⚠️ Moyen : 500ms-1s
- ❌ Mauvais : > 1s

---

## Checklist d'analyse Network

### ✅ Analyse initiale

- [ ] Rechargé la page avec Network ouvert
- [ ] Regardé le résumé (requests, transferred, time)
- [ ] Identifié les métriques hors objectifs

### ✅ Analyse des ressources

- [ ] Trié par Size pour trouver les fichiers lourds
- [ ] Trié par Time pour trouver les requêtes lentes
- [ ] Filtré par type (Img, JS, CSS, XHR) pour analyse ciblée
- [ ] Cherché les status en erreur (404, 500)

### ✅ Analyse du Waterfall

- [ ] Identifié les patterns problématiques (cascade, blocages)
- [ ] Vérifié le TTFB des requêtes API
- [ ] Repéré les requêtes très longues
- [ ] Noté les requêtes qui se bloquent mutuellement

### ✅ Tests avec throttling

- [ ] Testé en Fast 3G
- [ ] Mesuré le temps de chargement
- [ ] Identifié les priorités d'optimisation

### ✅ Documentation

- [ ] Exporté le HAR "avant optimisation"
- [ ] Listé les problèmes identifiés
- [ ] Défini le plan d'action

---

## Points clés à retenir

🌐 **L'onglet Network = Vue complète du trafic réseau**
- Toutes les requêtes HTTP visualisées
- Détails complets pour chaque requête
- Chronologie visuelle (Waterfall)

📊 **Colonnes essentielles**
- Name : Fichier/URL
- Status : Code HTTP (200, 404, 500...)
- Size : Poids transféré vs réel
- Time : Durée totale
- Waterfall : Chronologie visuelle

🔍 **Trois façons d'analyser**
1. Résumé global (nombre, poids, temps)
2. Liste triée (par taille, temps, status)
3. Waterfall (patterns, blocages, cascade)

⏱️ **Timing détaillé**
- DNS, Connection, SSL : Latence réseau
- Waiting (TTFB) : Vitesse du serveur
- Content Download : Poids du fichier

🎯 **Objectifs de performance**
- < 50 requêtes
- < 1 MB transféré
- < 3s temps total
- TTFB < 500ms

🔧 **Outils de test**
- Throttling réseau (Fast 3G, Slow 3G)
- Filtres par type et status
- Export HAR pour comparaison
- Blocage de requêtes pour tests

---

## Pour aller plus loin

L'onglet Network est votre allié principal pour optimiser les performances réseau. Utilisez-le **systématiquement** avant et après chaque optimisation pour mesurer l'impact réel.

**Prochaine étape** : Combiner Network avec l'onglet Performance pour une vue complète des performances !

---

> 💡 **Loi de Murphy appliquée au web** :
> *"Votre site se chargera toujours 10× plus lentement chez vos utilisateurs que chez vous."*
>
> C'est pour ça que l'onglet Network et le throttling existent ! 🌐📊

⏭️ [Lighthouse et audits automatiques](/07-debugging-et-outils-avances/02-performance-optimisation/03-lighthouse-audits.md)
