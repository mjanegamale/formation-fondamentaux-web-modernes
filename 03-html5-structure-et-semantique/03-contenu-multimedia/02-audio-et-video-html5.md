🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 3.3.2 Éléments audio et vidéo HTML5

## Introduction

Avant HTML5, intégrer de l'audio ou de la vidéo sur un site web nécessitait des plugins externes comme Flash Player. HTML5 a révolutionné cela en introduisant les balises natives `<audio>` et `<video>`, qui permettent de lire des médias directement dans le navigateur, sans plugin.

Dans ce chapitre, nous allons découvrir comment intégrer et contrôler du contenu audio et vidéo de manière professionnelle.

---

## La balise `<audio>`

### Syntaxe de base

La balise `<audio>` permet d'intégrer un fichier audio dans votre page web :

```html
<audio src="musique.mp3" controls>
    Votre navigateur ne supporte pas l'élément audio.
</audio>
```

**Résultat** : Un lecteur audio s'affiche avec des contrôles de lecture (play, pause, volume).

### Attributs essentiels

#### 1. `src` (source)

Indique le chemin vers le fichier audio :

```html
<audio src="audio/podcast.mp3" controls></audio>
```

#### 2. `controls` - **TRÈS IMPORTANT**

Affiche les contrôles de lecture (play, pause, volume, barre de progression) :

```html
<!-- ✅ Avec contrôles : l'utilisateur peut interagir -->
<audio src="musique.mp3" controls></audio>

<!-- ❌ Sans contrôles : l'audio ne peut pas être contrôlé visuellement -->
<audio src="musique.mp3"></audio>
```

⚠️ **Important** : Sans l'attribut `controls`, l'utilisateur ne peut pas contrôler la lecture (sauf via JavaScript). C'est généralement une mauvaise expérience utilisateur.

#### 3. `autoplay` - ⚠️ À utiliser avec prudence

Lance automatiquement la lecture au chargement de la page :

```html
<audio src="musique.mp3" controls autoplay></audio>
```

**⚠️ ATTENTION** : L'autoplay est généralement **déconseillé** et même **bloqué** par les navigateurs modernes pour plusieurs raisons :
- Mauvaise expérience utilisateur (surprise désagréable)
- Consommation de données mobiles non désirée
- Problèmes d'accessibilité
- Politiques strictes des navigateurs (Chrome, Safari bloquent l'autoplay avec son)

```html
<!-- ❌ ÉVITER : autoplay sans mute -->
<audio src="musique.mp3" controls autoplay></audio>

<!-- ⚠️ Tolérable : autoplay avec mute (mais toujours questionnable) -->
<audio src="ambiance.mp3" controls autoplay muted></audio>
```

#### 4. `loop`

Répète la lecture en boucle une fois terminée :

```html
<audio src="musique-ambiance.mp3" controls loop></audio>
```

Utile pour :
- Musiques d'ambiance
- Effets sonores de fond
- Sons répétitifs

#### 5. `muted`

Démarre le son en mode muet :

```html
<audio src="musique.mp3" controls muted></audio>
```

#### 6. `preload`

Contrôle comment le navigateur doit précharger l'audio :

```html
<!-- Ne précharge rien (économise la bande passante) -->
<audio src="podcast.mp3" controls preload="none"></audio>

<!-- Précharge seulement les métadonnées (durée, dimensions) -->
<audio src="podcast.mp3" controls preload="metadata"></audio>

<!-- Précharge tout le fichier -->
<audio src="podcast.mp3" controls preload="auto"></audio>
```

**Valeurs :**
- `none` : Ne précharge rien
- `metadata` : Précharge uniquement les métadonnées (recommandé par défaut)
- `auto` : Laisse le navigateur décider (peut précharger tout)

---

## Formats audio supportés

Les navigateurs ne supportent pas tous les mêmes formats audio. Voici les principaux :

| Format | Extension | Support | Usage recommandé |
|--------|-----------|---------|------------------|
| **MP3** | .mp3 | 🟢 Excellent (tous les navigateurs) | Usage général, musique |
| **OGG** | .ogg | 🟡 Bon (sauf Safari/IE) | Alternative open-source |
| **WAV** | .wav | 🟢 Bon | Audio non compressé, qualité max |
| **M4A/AAC** | .m4a | 🟢 Bon | Apple, qualité/compression |
| **WebM** | .webm | 🟡 Moyen | Moderne, open-source |

### Format recommandé : MP3

Pour une **compatibilité maximale**, utilisez le **format MP3** qui est supporté par tous les navigateurs modernes.

```html
<audio src="audio/musique.mp3" controls></audio>
```

---

## Balise `<source>` : Support multi-format

Pour assurer une compatibilité maximale avec tous les navigateurs, vous pouvez fournir plusieurs formats du même fichier audio :

```html
<audio controls>
    <source src="audio/musique.mp3" type="audio/mpeg">
    <source src="audio/musique.ogg" type="audio/ogg">
    <source src="audio/musique.wav" type="audio/wav">
    Votre navigateur ne supporte pas l'élément audio.
</audio>
```

**Comment ça fonctionne ?**
1. Le navigateur essaie le premier format (MP3)
2. S'il ne le supporte pas, il passe au suivant (OGG)
3. Et ainsi de suite jusqu'à trouver un format compatible
4. Si aucun format n'est supporté, le texte de fallback s'affiche

**L'attribut `type`** indique le type MIME du fichier :
- `audio/mpeg` pour MP3
- `audio/ogg` pour OGG
- `audio/wav` pour WAV
- `audio/mp4` pour M4A

---

## La balise `<video>`

### Syntaxe de base

La balise `<video>` fonctionne de manière très similaire à `<audio>` :

```html
<video src="video.mp4" controls width="640" height="360">
    Votre navigateur ne supporte pas l'élément vidéo.
</video>
```

### Attributs essentiels

La balise `<video>` partage la plupart des attributs de `<audio>`, avec quelques ajouts :

#### Attributs communs avec `<audio>`

```html
<video src="video.mp4"
       controls
       autoplay
       loop
       muted
       preload="metadata">
</video>
```

- `controls` : Affiche les contrôles (play, pause, volume, plein écran)
- `autoplay` : Lance automatiquement (⚠️ avec `muted` uniquement pour être accepté)
- `loop` : Répète en boucle
- `muted` : Démarre sans son
- `preload` : Stratégie de préchargement

#### Attributs spécifiques aux vidéos

##### 1. `width` et `height`

Définissent les dimensions du lecteur vidéo :

```html
<video src="video.mp4" controls width="800" height="450"></video>
```

**Bonnes pratiques :**
- Spécifiez toujours les dimensions pour éviter les sauts de mise en page
- Respectez le ratio d'aspect original (généralement 16:9)
- Utilisez CSS pour le responsive (nous verrons ça dans le chapitre Responsive Design)

```html
<!-- ✅ BON : Ratio 16:9 respecté (800/450 ≈ 16/9) -->
<video src="video.mp4" controls width="800" height="450"></video>

<!-- ❌ MAUVAIS : Ratio déformé -->
<video src="video.mp4" controls width="800" height="200"></video>
```

##### 2. `poster`

Affiche une image de prévisualisation avant que la vidéo ne soit lancée :

```html
<video src="video.mp4" controls poster="preview.jpg" width="800" height="450">
</video>
```

**Avantages :**
- Améliore l'apparence avant le chargement
- Donne un aperçu du contenu
- Réduit la sensation d'attente

```html
<!-- ✅ BON : avec poster -->
<video src="presentation.mp4"
       controls
       poster="thumbnail-presentation.jpg"
       width="800"
       height="450">
</video>
```

##### 3. `playsinline`

Force la vidéo à se lire dans la page sur iOS (sinon elle s'ouvre en plein écran) :

```html
<video src="video.mp4" controls playsinline width="640" height="360"></video>
```

**Particulièrement utile pour :**
- Vidéos d'arrière-plan
- Petites vidéos intégrées
- Expérience utilisateur cohérente sur mobile

---

## Formats vidéo supportés

Comme pour l'audio, les navigateurs supportent différents formats :

| Format | Extension | Support | Usage recommandé |
|--------|-----------|---------|------------------|
| **MP4** | .mp4 | 🟢 Excellent (tous) | **Recommandé** - Usage général |
| **WebM** | .webm | 🟡 Bon (sauf Safari) | Alternative open-source, moderne |
| **OGG** | .ogv | 🟡 Moyen | Ancien, open-source |
| **MOV** | .mov | 🔴 Limité | Format Apple, éviter sur le web |
| **AVI** | .avi | 🔴 Limité | Ancien, éviter |

### Format recommandé : MP4 (H.264)

Pour une **compatibilité maximale**, utilisez le **format MP4 avec codec H.264** :

```html
<video src="video.mp4" controls width="800" height="450"></video>
```

**Codec vidéo recommandé :** H.264
**Codec audio recommandé :** AAC

---

## Support multi-format pour les vidéos

Comme pour l'audio, vous pouvez fournir plusieurs formats :

```html
<video controls width="800" height="450" poster="preview.jpg">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    <source src="video.ogv" type="video/ogg">
    Votre navigateur ne supporte pas l'élément vidéo.
</video>
```

**Types MIME pour vidéo :**
- `video/mp4` pour MP4
- `video/webm` pour WebM
- `video/ogg` pour OGG

---

## Accessibilité : Sous-titres avec `<track>`

La balise `<track>` permet d'ajouter des sous-titres, des légendes ou des descriptions pour améliorer l'accessibilité :

```html
<video controls width="800" height="450">
    <source src="video.mp4" type="video/mp4">
    <track src="sous-titres-fr.vtt"
           kind="subtitles"
           srclang="fr"
           label="Français"
           default>
    <track src="sous-titres-en.vtt"
           kind="subtitles"
           srclang="en"
           label="English">
</video>
```

### Attributs de `<track>`

#### `src`
Chemin vers le fichier de sous-titres (généralement format **WebVTT** - `.vtt`)

#### `kind`
Type de piste :
- `subtitles` : Sous-titres (traduction des dialogues)
- `captions` : Sous-titres pour sourds et malentendants (inclut les sons)
- `descriptions` : Descriptions audio pour malvoyants
- `chapters` : Chapitres pour la navigation
- `metadata` : Métadonnées

#### `srclang`
Langue de la piste (code ISO : `fr`, `en`, `es`, etc.)

#### `label`
Nom affiché dans le menu des sous-titres

#### `default`
Piste active par défaut

### Format WebVTT

Les fichiers de sous-titres utilisent le format **WebVTT** (`.vtt`) :

```
WEBVTT

00:00:00.000 --> 00:00:03.000
Bonjour et bienvenue dans cette vidéo.

00:00:03.500 --> 00:00:07.000
Aujourd'hui, nous allons apprendre HTML5.

00:00:07.500 --> 00:00:10.000
Commençons par les bases.
```

**Structure :**
- Chaque bloc contient un timestamp (début --> fin)
- Suivi du texte à afficher
- Les blocs sont séparés par une ligne vide

---

## Accessibilité : Bonnes pratiques

### Pour l'audio ET la vidéo

1. **Toujours fournir des contrôles**
```html
<!-- ✅ BON -->
<video src="video.mp4" controls></video>

<!-- ❌ MAUVAIS : pas de contrôles -->
<video src="video.mp4"></video>
```

2. **Fournir un texte de fallback**
```html
<video src="video.mp4" controls>
    <p>Votre navigateur ne supporte pas la vidéo HTML5.
       <a href="video.mp4">Télécharger la vidéo</a>
    </p>
</video>
```

3. **Ajouter des sous-titres pour les vidéos**
```html
<video controls>
    <source src="conference.mp4" type="video/mp4">
    <track src="sous-titres.vtt" kind="captions" srclang="fr" label="Français" default>
</video>
```

4. **Éviter l'autoplay avec son**
```html
<!-- ❌ MAUVAIS : autoplay avec son -->
<video src="video.mp4" autoplay controls></video>

<!-- ✅ ACCEPTABLE : autoplay sans son -->
<video src="video.mp4" autoplay muted controls></video>
```

5. **Fournir une transcription textuelle**

Pour une accessibilité maximale, ajoutez un lien vers une transcription complète :

```html
<video src="interview.mp4" controls width="800" height="450">
    <track src="sous-titres.vtt" kind="captions" srclang="fr" label="Français">
</video>
<p><a href="transcription-interview.html">Lire la transcription complète</a></p>
```

---

## Optimisation des vidéos

### 1. Compression vidéo

Les vidéos peuvent être **très lourdes**. Il est crucial de les optimiser :

**Recommandations :**
- **Résolution** :
  - 1920x1080 (Full HD) maximum pour la plupart des usages
  - 1280x720 (HD) pour un bon compromis qualité/poids
  - 640x360 pour des petites vidéos intégrées

- **Débit (bitrate)** :
  - 5-8 Mbps pour 1080p
  - 2.5-4 Mbps pour 720p
  - 1-1.5 Mbps pour 360p

- **Framerate** :
  - 30 fps pour la majorité des vidéos
  - 24 fps pour un look "cinéma"
  - 60 fps uniquement si nécessaire (sport, gaming)

### 2. Outils de compression

**En ligne :**
- **CloudConvert** : https://cloudconvert.com
- **Clipchamp** : Éditeur en ligne gratuit
- **Handbrake** : Logiciel gratuit et puissant (Mac/Windows/Linux)

**Professionnels :**
- **Adobe Media Encoder**
- **Final Cut Pro / DaVinci Resolve**

### 3. Format et codec

**Recommandation moderne :**
```
Format : MP4
Codec vidéo : H.264
Codec audio : AAC
```

Exemple avec FFmpeg (outil en ligne de commande) :
```bash
ffmpeg -i video-original.mov -c:v libx264 -crf 23 -c:a aac -b:a 128k video-optimise.mp4
```

### 4. Préchargement intelligent

Pour les vidéos lourdes, utilisez `preload="metadata"` :

```html
<video src="video.mp4" controls preload="metadata" width="800" height="450"></video>
```

Cela charge uniquement les informations de base (durée, dimensions) sans télécharger toute la vidéo.

---

## Vidéos responsive

Pour que vos vidéos s'adaptent à toutes les tailles d'écran, utilisez cette technique CSS :

**HTML :**
```html
<div class="video-container">
    <video controls width="800" height="450">
        <source src="video.mp4" type="video/mp4">
    </video>
</div>
```

**CSS :**
```css
.video-container {
    position: relative;
    width: 100%;
    padding-bottom: 56.25%; /* Ratio 16:9 (9/16 = 0.5625) */
    height: 0;
    overflow: hidden;
}

.video-container video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
```

**Résultat :** La vidéo s'adapte automatiquement à la largeur du conteneur tout en conservant son ratio 16:9.

*Note : Nous approfondirons les techniques responsive dans le chapitre 4.5.*

---

## Vidéos d'arrière-plan (Background videos)

Les vidéos en arrière-plan sont tendance mais doivent être utilisées avec parcimonie :

```html
<div class="hero">
    <video autoplay muted loop playsinline class="background-video">
        <source src="background.mp4" type="video/mp4">
    </video>
    <div class="content">
        <h1>Bienvenue sur notre site</h1>
    </div>
</div>
```

**CSS associé :**
```css
.hero {
    position: relative;
    height: 100vh;
    overflow: hidden;
}

.background-video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: -1;
}

.content {
    position: relative;
    z-index: 1;
    color: white;
}
```

**⚠️ Règles importantes pour les vidéos d'arrière-plan :**

1. **Toujours `muted`** (sinon le navigateur bloque l'autoplay)
2. **Courte durée** (10-30 secondes maximum, puis loop)
3. **Très compressée** (qualité réduite acceptable pour un arrière-plan)
4. **Pas sur mobile** (consommation de données, performance)

```css
/* Masquer sur mobile */
@media (max-width: 768px) {
    .background-video {
        display: none;
    }
    .hero {
        background-image: url('fallback-image.jpg');
    }
}
```

---

## Héberger des vidéos : Votre serveur vs Plateformes

### Option 1 : Héberger sur votre serveur

**Avantages :**
- Contrôle total
- Pas de publicité
- Pas de dépendance externe

**Inconvénients :**
- Consomme de la bande passante (coûteux)
- Pas d'optimisation automatique
- Pas de streaming adaptatif

**Quand l'utiliser :**
- Petites vidéos (<50 Mo)
- Nombre limité de visiteurs
- Contrôle total nécessaire

### Option 2 : Plateformes vidéo (YouTube, Vimeo, etc.)

**Avantages :**
- Bande passante illimitée
- Streaming adaptatif automatique
- Qualité ajustée selon la connexion
- CDN mondial

**Inconvénients :**
- Dépendance externe
- Publicités possibles (YouTube)
- Moins de contrôle

**Quand l'utiliser :**
- Vidéos longues
- Beaucoup de trafic
- Budget limité

### Intégrer une vidéo YouTube

```html
<!-- Version responsive avec iframe -->
<div class="video-container">
    <iframe
        width="800"
        height="450"
        src="https://www.youtube.com/embed/VIDEO_ID"
        title="Titre de la vidéo"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen>
    </iframe>
</div>
```

**Même CSS responsive que précédemment.**

---

## Exemples complets

### Exemple 1 : Lecteur audio simple

```html
<article>
    <h2>Épisode 12 - Les bases de HTML5</h2>
    <audio controls>
        <source src="podcast-episode-12.mp3" type="audio/mpeg">
        <source src="podcast-episode-12.ogg" type="audio/ogg">
        <p>Votre navigateur ne supporte pas l'audio HTML5.
           <a href="podcast-episode-12.mp3">Télécharger l'épisode</a>
        </p>
    </audio>
    <p>Durée : 45 minutes | Publié le 3 décembre 2024</p>
</article>
```

### Exemple 2 : Lecteur vidéo accessible

```html
<section>
    <h2>Tutoriel : Créer votre premier site web</h2>

    <video controls width="800" height="450" poster="thumbnail-tuto.jpg">
        <source src="tutoriel-site-web.mp4" type="video/mp4">
        <source src="tutoriel-site-web.webm" type="video/webm">

        <!-- Sous-titres en plusieurs langues -->
        <track src="sous-titres-fr.vtt"
               kind="subtitles"
               srclang="fr"
               label="Français"
               default>
        <track src="subtitles-en.vtt"
               kind="subtitles"
               srclang="en"
               label="English">
        <track src="subtitulos-es.vtt"
               kind="subtitles"
               srclang="es"
               label="Español">

        <p>Votre navigateur ne supporte pas la vidéo HTML5.
           <a href="tutoriel-site-web.mp4">Télécharger la vidéo</a>
        </p>
    </video>

    <p><a href="transcription.html">📄 Lire la transcription complète</a></p>
</section>
```

### Exemple 3 : Vidéo d'arrière-plan (hero section)

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hero Video Background</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .hero {
            position: relative;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }

        .hero-video {
            position: absolute;
            top: 50%;
            left: 50%;
            min-width: 100%;
            min-height: 100%;
            width: auto;
            height: auto;
            transform: translate(-50%, -50%);
            z-index: -1;
        }

        .hero-content {
            position: relative;
            z-index: 1;
            text-align: center;
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
        }

        /* Masquer la vidéo sur mobile */
        @media (max-width: 768px) {
            .hero-video {
                display: none;
            }
            .hero {
                background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
                            url('fallback-image.jpg') center/cover;
            }
        }
    </style>
</head>
<body>
    <section class="hero">
        <video class="hero-video" autoplay muted loop playsinline>
            <source src="background-video.mp4" type="video/mp4">
        </video>

        <div class="hero-content">
            <h1>Bienvenue sur notre site</h1>
            <p>Découvrez nos services exceptionnels</p>
        </div>
    </section>
</body>
</html>
```

---

## Bonnes pratiques récapitulatives

### ✅ À FAIRE

1. **Toujours** inclure l'attribut `controls` (sauf pour vidéos d'arrière-plan)
2. Spécifier `width` et `height` pour les vidéos
3. Utiliser le format **MP3** pour l'audio et **MP4** pour la vidéo (compatibilité maximale)
4. Ajouter des **sous-titres** avec `<track>` pour l'accessibilité
5. Fournir un **texte de fallback** entre les balises
6. Optimiser et compresser les fichiers avant upload
7. Utiliser `poster` pour les vidéos
8. Ajouter `playsinline` pour iOS
9. Utiliser `preload="metadata"` par défaut
10. Fournir un lien de téléchargement alternatif

### ❌ À ÉVITER

1. **Autoplay avec son** (mauvaise UX + bloqué par les navigateurs)
2. Héberger de grandes vidéos sur votre serveur sans CDN
3. Vidéos d'arrière-plan sur mobile
4. Oublier les sous-titres sur des vidéos avec dialogue
5. Fichiers non optimisés et très lourds
6. Formats propriétaires ou peu supportés
7. Absence de contrôles utilisateur
8. Vidéos sans image `poster`

---

## Tableau récapitulatif : Audio vs Vidéo

| Caractéristique | `<audio>` | `<video>` |
|-----------------|-----------|-----------|
| **Attributs communs** | controls, autoplay, loop, muted, preload | ✅ Identiques |
| **Attributs spécifiques** | - | width, height, poster, playsinline |
| **Format recommandé** | MP3 | MP4 (H.264) |
| **Balise `<source>`** | ✅ Oui | ✅ Oui |
| **Balise `<track>`** | ✅ Possible | ✅ Recommandé |
| **Accessibilité** | Transcription textuelle | Sous-titres + transcription |

---

## Points clés à retenir

1. **HTML5 permet d'intégrer audio et vidéo nativement** sans plugin
2. **`controls` est quasi-obligatoire** pour une bonne expérience utilisateur
3. **MP3 pour l'audio, MP4 pour la vidéo** = compatibilité maximale
4. **Les sous-titres (`<track>`) sont essentiels** pour l'accessibilité
5. **Évitez l'autoplay avec son** (bloqué par les navigateurs)
6. **Optimisez toujours vos médias** avant de les mettre en ligne
7. **Considérez YouTube/Vimeo** pour les vidéos volumineuses
8. **Utilisez `<source>` multiple** pour assurer la compatibilité

---

## Ressources complémentaires

- **MDN - `<video>`** : Documentation complète
- **MDN - `<audio>`** : Documentation complète
- **WebVTT Guide** : Format de sous-titres
- **Handbrake** : Outil gratuit de compression vidéo
- **Can I Use** : Vérifier la compatibilité des formats

---

## Prochaine étape

Dans le prochain chapitre, nous découvrirons comment structurer sémantiquement le contenu multimédia avec les balises **`<figure>` et `<figcaption>`**, qui permettent d'associer des légendes à vos images, audios et vidéos de manière professionnelle.

⏭️ [Figures et légendes (figure, figcaption)](/03-html5-structure-et-semantique/03-contenu-multimedia/03-figures-et-legendes.md)
