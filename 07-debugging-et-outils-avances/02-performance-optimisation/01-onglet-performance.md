🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 7.2.1 Onglet Performance des DevTools

## Introduction

Votre site fonctionne, mais il est **lent**. La page met du temps à s'afficher, les animations saccadent, les clics ne répondent pas immédiatement. Comment identifier la cause exacte du problème ?

L'**onglet Performance** des DevTools est votre **radiographie complète** de l'activité du navigateur. Il enregistre tout ce qui se passe pendant quelques secondes et vous montre exactement où le temps est dépensé.

Dans cette section, nous allons apprendre à utiliser cet outil puissant pour **mesurer, analyser et améliorer** les performances de vos applications web.

---

## Pourquoi les performances sont importantes ?

### L'impact sur l'expérience utilisateur

**Statistiques réelles** :
- ⏱️ **53%** des utilisateurs abandonnent un site si le chargement prend plus de 3 secondes
- 📉 **1 seconde** de délai = 7% de perte de conversions
- ⚡ Les sites rapides ont un meilleur référencement Google
- 💰 Amazon perd **1 milliard** par an pour chaque 100ms de latence

**Analogie** : Imaginez un magasin physique où vous devez attendre 5 secondes entre chaque action. Vous partiriez immédiatement, non ? Sur le web, c'est pareil !

### Ce que "rapide" signifie vraiment

Un site performant, c'est :
- ✅ **Affichage rapide** : Contenu visible en moins de 2 secondes
- ✅ **Interactions fluides** : Réponse instantanée aux clics
- ✅ **Animations fluides** : 60 images par seconde (FPS)
- ✅ **Pas de freeze** : Aucun blocage de l'interface

---

## Accéder à l'onglet Performance

### Ouvrir les DevTools

1. **Méthode 1** : Appuyez sur **F12** (Windows/Linux) ou **Cmd+Option+I** (Mac)
2. **Méthode 2** : Clic droit sur la page → **Inspecter**
3. **Méthode 3** : Menu → Plus d'outils → Outils de développement

### Trouver l'onglet Performance

Dans la barre d'onglets en haut des DevTools, cherchez **"Performance"** :
- Si vous ne le voyez pas, cliquez sur **">>"** (plus d'onglets)
- Ou utilisez **Ctrl+Shift+P** (Cmd+Shift+P sur Mac) et tapez "Performance"

### Première impression

L'onglet Performance peut sembler **intimidant** au premier abord :
- Beaucoup de graphiques
- Des termes techniques
- Une interface dense

**Rassurez-vous** : Nous allons décortiquer chaque élément ensemble. À la fin de cette section, vous saurez exactement quoi regarder !

---

## Faire un enregistrement de performance

### Préparer l'enregistrement

**Avant d'enregistrer** :

1. **Fermez les onglets inutiles** : Chaque onglet consomme des ressources
2. **Désactivez les extensions** : Elles peuvent fausser les mesures
3. **Mode navigation privée** (optionnel) : Pour éviter l'impact du cache et des extensions
4. **Rechargez la page** : Partez d'un état propre

### Méthode 1 : Enregistrement manuel (recommandé pour débuter)

**Étape par étape** :

1. **Cliquez sur le cercle** ⏺️ (Record) en haut à gauche
   - Le cercle devient rouge : l'enregistrement a commencé

2. **Interagissez avec votre page** :
   - Cliquez sur des boutons
   - Faites défiler la page
   - Ouvrez des menus
   - Faites ce qui est lent

3. **Arrêtez l'enregistrement** :
   - Cliquez sur le carré ⏹️ (Stop)
   - Ou attendez 10-20 secondes et arrêtez

4. **Patientez** : Les DevTools analysent les données (quelques secondes)

**Conseil** : Enregistrez entre **5 et 10 secondes**. Plus court = pas assez de données. Plus long = difficile à analyser.

### Méthode 2 : Enregistrement avec rechargement de page

**Pour mesurer le chargement initial** :

1. **Cliquez sur l'icône de rafraîchissement** 🔄 à côté du Record
   - La page se recharge automatiquement
   - L'enregistrement démarre
   - L'enregistrement s'arrête automatiquement après le chargement

**Utilisation** : Mesurer la vitesse de chargement d'une page

### Méthode 3 : Enregistrement programmatique

Dans votre code JavaScript :

```javascript
// Démarrer l'enregistrement
performance.mark('debut-operation');

// Votre code à mesurer
faireQuelqueChose();

// Terminer l'enregistrement
performance.mark('fin-operation');
performance.measure('operation', 'debut-operation', 'fin-operation');

// Voir les résultats
const mesures = performance.getEntriesByType('measure');
console.log(mesures);
```

**Utilisation** : Mesurer une opération spécifique dans votre code

---

## Comprendre l'interface

Une fois l'enregistrement terminé, vous voyez plusieurs sections. Décryptons-les !

### Vue d'ensemble (en haut)

```
┌─────────────────────────────────────────────────────┐
│  FPS  │████████▓▓░░████████████████                 │
│  CPU  │██████████████▓▓▓░░████████                  │
│  NET  │══════════════════════════════               │
└─────────────────────────────────────────────────────┘
     0s      1s      2s      3s      4s
```

Cette section montre **3 graphiques temporels** :

#### 1. FPS (Frames Per Second)

**Ce que ça montre** : Fluidité des animations

```
FPS  │████████▓▓░░████████
     │
60   ├─────────── Vert : Fluide (60 FPS)
30   ├─────────── Jaune : Saccadé (30-60 FPS)
0    └─────────── Rouge : Freeze (<30 FPS)
```

**Interprétation** :
- ✅ **Vert** (60 FPS) : Parfait ! Animations fluides
- ⚠️ **Jaune** (30-60 FPS) : Légèrement saccadé
- ❌ **Rouge** (<30 FPS) : Très saccadé, problème !

**Analogie** : Comme un film au cinéma. 60 FPS = fluide comme au cinéma. 15 FPS = comme un vieux film muet saccadé.

#### 2. CPU (Processeur)

**Ce que ça montre** : Utilisation du processeur par catégorie

**Code couleur** :
- 🟦 **Bleu** : Chargement (Loading)
- 🟨 **Jaune** : JavaScript (Scripting)
- 🟪 **Violet** : Rendu (Rendering)
- 🟩 **Vert** : Peinture (Painting)
- 🟫 **Gris** : Autre (System)
- ⬜ **Blanc** : Idle (Inactif - c'est bien !)

**Interprétation** :
```
CPU  │██████████████████  ← Mauvais : CPU saturé
CPU  │████░░░░████░░░░░░  ← Bon : Pics courts, beaucoup de blanc
```

Si vous voyez **beaucoup de jaune** (JavaScript), votre code JS est peut-être trop lourd.

#### 3. NET (Network - Réseau)

**Ce que ça montre** : Activité réseau (requêtes HTTP)

```
NET  │══════════════════
     │ │││││ │││  ││
     │
     └─ Chaque barre = une requête
```

**Interprétation** :
- Beaucoup de barres = beaucoup de requêtes (peut ralentir)
- Barres longues = requêtes lentes
- Barres au début = chargement initial
- Barres plus tard = requêtes dynamiques (fetch, XHR)

### Timeline principale (milieu)

C'est la **partie la plus importante** ! Elle montre en détail ce qui s'est passé.

#### Frames (Images)

Chaque barre verticale = une frame (image affichée)

```
Frames │ ▌▌ ▌▌ ▌▌ ▌▌ ▌▌  ← Espacement régulier = bon
       │
Frames │ ▌▌ ▌▌ ▌     ▌  ← Trous = frame drop = saccades
```

**Frame drop** : Une "image manquée" qui cause des saccades

#### Main (Thread principal)

Montre **tout ce que fait le navigateur** :

```
Main   │ ┌────────┐ ┌──┐ ┌─────┐
       │ │Function│ │JS│ │Parse│
       │ └────────┘ └──┘ └─────┘
```

Chaque bloc représente une **tâche** :
- **Fonction JavaScript** : Votre code qui s'exécute
- **Parse HTML** : Analyse du HTML
- **Recalculate Style** : Calcul des styles CSS
- **Layout** : Calcul des positions
- **Paint** : Dessin des pixels

**Règle d'or** : Aucune tâche ne devrait dépasser **50ms** (pour maintenir 60 FPS : 1000ms / 60 = 16.67ms par frame, mais on vise moins pour laisser de la marge).

#### Raster et GPU

Activités du GPU (carte graphique) pour le rendu final.

---

## Zoomer et naviguer

### Zoomer sur une période

**Pourquoi zoomer ?** Pour examiner en détail une période spécifique.

**Méthodes** :

1. **Avec la souris** :
   - Cliquez et glissez sur la vue d'ensemble (graphiques FPS/CPU/NET en haut)
   - La timeline se met à jour

2. **Avec la molette** :
   - Molette = Zoom in/out
   - Maintenir **Shift** + Molette = Scroll horizontal

3. **Raccourcis clavier** :
   - **W** : Zoom in (agrandir)
   - **S** : Zoom out (rétrécir)
   - **A** : Aller à gauche
   - **D** : Aller à droite

### Sélectionner une tâche

**Cliquez sur un bloc** dans la timeline Main pour voir les détails :

```
Main   │ ┌────────┐
       │ │Function│ ← Cliquez ici
       │ └────────┘

📊 Détails affichés en bas :
- Nom de la fonction
- Durée d'exécution
- Fichier source et ligne
- Call stack
```

---

## Analyser les performances : Méthode pratique

### Étape 1 : Identifier les zones rouges

**Cherchez les pics** dans les graphiques :

```
FPS  │████████░░░░░░████████
                 ↑
            Zone problématique !
```

Si vous voyez du **rouge dans le FPS**, c'est là qu'il y a un problème.

### Étape 2 : Examiner le CPU

**Dans la zone rouge, regardez le CPU** :

```
CPU  │████████████████
     │ 🟨🟨🟨🟨 ← Beaucoup de jaune = JavaScript lent
```

**Code couleur** :
- 🟨 **Beaucoup de jaune** → Problème JavaScript
- 🟪 **Beaucoup de violet** → Problème de rendu CSS
- 🟩 **Beaucoup de vert** → Problème de peinture

### Étape 3 : Zoomer sur le problème

**Zoomez sur la zone rouge** pour voir les détails :

```
Main   │ ┌──────────────────────────┐
       │ │ calculateTotal()         │ ← 250ms ! Trop long !
       │ └──────────────────────────┘
```

Vous voyez maintenant **quelle fonction** prend trop de temps !

### Étape 4 : Analyser la fonction

**Cliquez sur le bloc** pour voir les détails :

```
📊 Summary (Résumé)
━━━━━━━━━━━━━━━━━━━━━
Function: calculateTotal
File: script.js:42
Duration: 253.2ms        ← Le problème !
Self Time: 180.5ms
Total Time: 253.2ms
```

**Vocabulaire** :
- **Self Time** : Temps passé dans cette fonction uniquement
- **Total Time** : Temps incluant les sous-fonctions appelées

### Étape 5 : Voir le code source

**En bas, onglet "Bottom-Up"** :

```
Self Time    Total Time    Activity
180.5ms      253.2ms      calculateTotal  script.js:42
 72.7ms       72.7ms      │─ forEach      (native)
```

**Cliquez sur "script.js:42"** → Vous êtes amené à la ligne de code !

---

## Les indicateurs clés à surveiller

### FPS (Frames Per Second)

**Objectif** : Maintenir **60 FPS**

**Pourquoi 60 ?** La plupart des écrans rafraîchissent à 60 Hz. 60 FPS = parfaitement fluide.

**Calcul** : 1000ms / 60 frames = **16.67ms par frame**

Si une opération prend plus de 16ms, vous "ratez" une frame → saccade visible.

**Exemples** :
- ✅ Animation à 60 FPS : Fluide comme de l'eau
- ⚠️ Animation à 30 FPS : Saccadé mais acceptable
- ❌ Animation à 15 FPS : Très saccadé, mauvaise UX

### Long Tasks (Tâches longues)

**Définition** : Toute tâche qui prend **plus de 50ms**

```
Main   │ ┌─────────────────────┐
       │ │    Long Task!       │ ← 85ms = Problème
       │ └─────────────────────┘
         └──────────────────────┘
                 85ms
```

**Pourquoi c'est un problème ?**
- Bloque le thread principal
- L'interface ne répond plus
- L'utilisateur voit un freeze

**Dans l'interface** : Les long tasks ont un **triangle rouge** dans le coin ⚠️

### Rendering (Rendu)

**Les étapes du rendu** :

1. **Recalculate Style** : Calculer les styles CSS
2. **Layout** : Calculer les positions et tailles
3. **Update Layer Tree** : Mettre à jour les couches
4. **Paint** : Dessiner les pixels
5. **Composite Layers** : Combiner les couches

**Problème courant** : Layout et Paint répétés = "Layout Thrashing"

---

## Cas pratiques d'analyse

### Cas 1 : Animation saccadée

**Symptôme** : FPS qui chute pendant une animation

**Enregistrement** :
```
FPS  │███████░░░░░░░░░███████
               ↑
        Animation démarre
```

**Analyse** :
1. Zoomer sur la zone rouge
2. Regarder la timeline Main
3. Identifier les tâches lourdes

**Exemple** :
```javascript
// ❌ MAUVAIS : Force le recalcul à chaque frame
function animer() {
  element.style.left = element.offsetLeft + 1 + 'px'; // Lecture + Écriture
  requestAnimationFrame(animer);
}
```

**Onglet Performance montre** :
```
Main │ ┌───┐┌───┐┌───┐┌───┐┌───┐
     │ │Cal││Lay││Pai││Cal││Lay│... ← Layout répété !
```

**Solution** :
```javascript
// ✅ BON : Utilise transform (GPU)
function animer() {
  position += 1;
  element.style.transform = `translateX(${position}px)`;
  requestAnimationFrame(animer);
}
```

### Cas 2 : Chargement lent de page

**Symptôme** : La page met 5 secondes à s'afficher

**Enregistrement** : Utilisez "Record and reload" 🔄

**Analyse** :
```
CPU  │████████████████░░░░░░
     │ 🟦🟦🟦🟨🟨🟪🟪
     │
     0s      2s      4s

Interprétation :
0-1s : Bleu (Loading) → Téléchargement des ressources
1-3s : Jaune (Scripting) → JavaScript s'exécute
3-4s : Violet (Rendering) → Rendu de la page
```

**Dans NET** :
```
NET  │═══════════════
     │ ││││││││││││
     │
     └─ Beaucoup de requêtes → Trop de fichiers ?
```

**Problème identifié** : 50 requêtes réseau !

**Solution** : Grouper les fichiers, utiliser un bundler

### Cas 3 : Clic qui répond lentement

**Symptôme** : 500ms entre le clic et la réaction

**Enregistrement** : Record pendant que vous cliquez

**Analyse** :
```
Main │ ┌──────────────────────┐
     │ │ handleClick()        │ ← 480ms !
     │ │  └─ processData()    │
     │ │     └─ forEach()     │
     │ └──────────────────────┘
```

**Cliquer sur le bloc** :
```
Summary
━━━━━━━━━━━
handleClick()
Self Time: 50ms
Total Time: 480ms

Appelle :
└─ processData() : 430ms
   └─ forEach() : 420ms  ← Le coupable !
```

**Code problématique** :
```javascript
function handleClick() {
  const items = Array(100000).fill(0);
  items.forEach(item => {
    // Traitement lourd
  });
}
```

**Solution** : Traiter par petits lots (chunking)

### Cas 4 : Scroll saccadé

**Symptôme** : Le défilement de la page n'est pas fluide

**Enregistrement** : Record pendant que vous scrollez

**Analyse** :
```
FPS  │████░░░░░░░░████░░░░░░░░
     │    ↑         ↑
     │  Saccade   Saccade
```

À chaque saccade, regarder le CPU :
```
Main │ ┌────────┐
     │ │onScroll│ ← Se déclenche à chaque pixel !
     │ └────────┘
```

**Code problématique** :
```javascript
// ❌ MAUVAIS : Trop d'événements
window.addEventListener('scroll', () => {
  // Code lourd exécuté à chaque pixel de scroll
});
```

**Solution** : Throttle ou debounce

```javascript
// ✅ BON : Limite à 1 fois tous les 100ms
let isThrottled = false;
window.addEventListener('scroll', () => {
  if (isThrottled) return;
  isThrottled = true;

  // Code ici

  setTimeout(() => { isThrottled = false; }, 100);
});
```

---

## Fonctionnalités avancées

### Screenshots (Captures d'écran)

**Activer les screenshots** :
1. Cliquez sur l'icône **paramètres** ⚙️ (en haut à droite de l'onglet Performance)
2. Cochez **"Screenshots"**

**Utilité** : Voir visuellement ce qui s'affichait à chaque moment

```
┌─────┬─────┬─────┬─────┐
│     │     │     │     │  ← Miniatures de la page
└─────┴─────┴─────┴─────┘
  0s    1s    2s    3s
```

Survolez une miniature → l'affichage à ce moment précis

### Memory (Mémoire)

**Activer le profiling mémoire** :
1. Paramètres ⚙️
2. Cochez **"Memory"**

**Nouveau graphique** :
```
Memory │  ╱╲╱╲╱╲╱╲╱╲
       │ ╱          ╲    ← Si descend jamais = fuite mémoire
       │╱            ╲
       └──────────────────
         JS Heap (Tas JavaScript)
```

**Interprétation** :
- Mémoire qui **monte et descend** : Normal (GC = Garbage Collection)
- Mémoire qui **monte sans descendre** : Fuite mémoire (memory leak)

### Web Vitals

**Activer Web Vitals** :
1. Paramètres ⚙️
2. Cochez **"Web Vitals"**

**Indicateurs Google** :
- **LCP** (Largest Contentful Paint) : Temps avant affichage du plus gros élément
- **FID** (First Input Delay) : Délai avant première interaction
- **CLS** (Cumulative Layout Shift) : Stabilité visuelle

Ces métriques sont utilisées par Google pour le référencement !

---

## Optimiser basé sur les résultats

### Si beaucoup de JavaScript (jaune) 🟨

**Problème** : Code JavaScript trop lourd

**Solutions** :
- ✅ Réduire les boucles inutiles
- ✅ Utiliser des algorithmes plus efficaces
- ✅ Lazy loading (charger à la demande)
- ✅ Web Workers (exécuter en arrière-plan)

### Si beaucoup de Rendering (violet) 🟪

**Problème** : Trop de recalculs de layout

**Solutions** :
- ✅ Éviter de lire/écrire le DOM en boucle
- ✅ Utiliser `transform` et `opacity` (GPU)
- ✅ Grouper les modifications DOM
- ✅ Utiliser `requestAnimationFrame`

### Si beaucoup de Painting (vert) 🟩

**Problème** : Trop de zones à repeindre

**Solutions** :
- ✅ Réduire la zone de repeinture
- ✅ Utiliser `will-change` CSS
- ✅ Créer des couches GPU séparées
- ✅ Éviter les ombres et dégradés complexes

### Si beaucoup de Loading (bleu) 🟦

**Problème** : Ressources trop lourdes ou trop nombreuses

**Solutions** :
- ✅ Compresser les images (WebP, AVIF)
- ✅ Minifier JS/CSS
- ✅ Utiliser un CDN
- ✅ Réduire le nombre de requêtes
- ✅ Lazy loading des images

---

## Astuces et bonnes pratiques

### ✅ À faire

1. **Enregistrez des sessions courtes** (5-10 secondes)
   - Plus facile à analyser
   - Moins de données à traiter

2. **Désactivez les extensions** pendant les tests
   - Elles peuvent fausser les mesures
   - Mode navigation privée recommandé

3. **Comparez avant/après**
   - Enregistrez avant optimisation
   - Enregistrez après optimisation
   - Mesurez l'amélioration

4. **Utilisez les screenshots**
   - Voir visuellement ce qui se passe
   - Identifier quand le contenu apparaît

5. **Cherchez les patterns**
   - Long tasks répétés
   - Frame drops réguliers
   - Pics de CPU

### ❌ À éviter

1. **Ne pas enregistrer trop longtemps**
   - Au-delà de 20 secondes = difficile à analyser
   - Les DevTools peuvent ralentir

2. **Ne pas ignorer les warnings**
   - Triangles rouges ⚠️ = signaux importants
   - Long tasks = à investiguer

3. **Ne pas optimiser à l'aveugle**
   - Toujours **mesurer d'abord**
   - Optimiser ce qui est vraiment lent
   - Ne pas optimiser prématurément

4. **Ne pas tester sur une machine puissante seulement**
   - Testez sur des appareils plus faibles
   - Throttling CPU dans DevTools (settings)

---

## Outils complémentaires

### Throttling (Simulation d'appareil lent)

**Pourquoi ?** Votre machine de développement est plus puissante que les appareils des utilisateurs.

**Activer le throttling** :
1. Paramètres ⚙️ de l'onglet Performance
2. CPU : **4× slowdown** (ou 6×)
3. Network : **Fast 3G** ou **Slow 3G**

**Résultat** : Vous voyez les performances réelles sur des appareils moyens.

### Lighthouse (Audit automatique)

Lighthouse analyse automatiquement les performances :

1. Onglet **Lighthouse** des DevTools
2. Cliquez **"Generate report"**
3. Attendez l'analyse (30-60 secondes)
4. Score de performance + recommandations

**Complémentaire** : Lighthouse donne des suggestions, Performance montre les détails.

### Network Throttling

Dans l'onglet **Network** :
- Simuler une connexion lente
- Voir l'impact sur le chargement
- Identifier les requêtes bloquantes

---

## Checklist d'analyse

Quand vous analysez les performances, suivez cette checklist :

### ✅ Avant l'enregistrement

- [ ] Fermé les onglets inutiles
- [ ] Désactivé les extensions (ou mode privé)
- [ ] Décidé ce que je veux mesurer (chargement, interaction, animation)
- [ ] Préparé les actions à effectuer

### ✅ Pendant l'enregistrement

- [ ] Enregistrement lancé
- [ ] Actions effectuées de manière naturelle
- [ ] Durée entre 5 et 10 secondes
- [ ] Enregistrement arrêté

### ✅ Après l'enregistrement

- [ ] Regardé la vue FPS pour identifier les zones rouges
- [ ] Examiné la répartition CPU (jaune/violet/vert/bleu)
- [ ] Zoomé sur les zones problématiques
- [ ] Identifié les long tasks (>50ms)
- [ ] Cliqué sur les tâches pour voir les détails
- [ ] Noté les fonctions/fichiers problématiques

### ✅ Correction et vérification

- [ ] Corrigé le code identifié
- [ ] Effectué un nouvel enregistrement
- [ ] Comparé les résultats avant/après
- [ ] Vérifié l'amélioration des FPS
- [ ] Testé sur appareil réel si possible

---

## Interpréter les résultats : Guide visuel

### Bon profil de performance

```
FPS  │████████████████████████████  ← Vert constant
CPU  │██░░██░░██░░██░░██░░██░░██░░  ← Pics courts, beaucoup de blanc
NET  │══ ══ ══                      ← Peu de requêtes, au début
     └────────────────────────────
       0s    1s    2s    3s    4s
```

**Caractéristiques** :
- ✅ FPS stable à 60
- ✅ CPU avec beaucoup de temps idle (blanc)
- ✅ Peu de requêtes réseau
- ✅ Aucun long task

### Mauvais profil de performance

```
FPS  │████░░░░░░░░░░░░████░░░░░░░░  ← Rouge fréquent
CPU  │████████████████████████████  ← Saturé, pas de blanc
NET  │═════════════════════════════  ← Requêtes continues
     └────────────────────────────
       0s    1s    2s    3s    4s
```

**Caractéristiques** :
- ❌ FPS qui chute en rouge
- ❌ CPU saturé en permanence
- ❌ Beaucoup de requêtes réseau
- ❌ Présence de long tasks

---

## Vocabulaire technique simplifié

**Frame** : Une "image" affichée à l'écran. 60 FPS = 60 images par seconde.

**Long Task** : Tâche qui prend plus de 50ms et bloque l'interface.

**Scripting** : Exécution de code JavaScript.

**Rendering** : Calcul des styles et positions des éléments.

**Painting** : Dessin des pixels à l'écran.

**Layout** : Calcul de la taille et position de chaque élément.

**Reflow** : Recalcul du layout (coûteux en performance).

**Repaint** : Redessin d'éléments sans changer leur position.

**Compositing** : Combinaison des différentes couches visuelles.

**Thread** : Fil d'exécution. Le "Main thread" est le principal.

**Idle** : Temps où le navigateur ne fait rien (c'est bien !).

---

## Points clés à retenir

🎯 **L'onglet Performance = Radiographie de votre site**
- Enregistre tout pendant quelques secondes
- Montre exactement où le temps est dépensé
- Identifie les goulots d'étranglement

📊 **Trois graphiques essentiels**
- FPS : Fluidité (objectif : 60 FPS constant)
- CPU : Répartition du travail (cherchez beaucoup de blanc)
- NET : Requêtes réseau (moins = mieux)

🟨 **Code couleur CPU**
- Jaune = JavaScript
- Violet = Rendu
- Vert = Peinture
- Bleu = Chargement

⚠️ **Long Tasks = Ennemi #1**
- Plus de 50ms = problème
- Bloque l'interface
- Cause des freezes

🔍 **Méthode d'analyse**
1. Identifier les zones rouges (FPS bas)
2. Zoomer sur ces zones
3. Regarder la timeline Main
4. Cliquer sur les tâches longues
5. Voir la fonction responsable
6. Optimiser cette fonction
7. Ré-enregistrer pour vérifier

✨ **Objectifs de performance**
- FPS : 60 constant
- Pas de long tasks (>50ms)
- CPU avec beaucoup de temps idle
- Interactions répondent en <100ms

---

## Pour aller plus loin

L'onglet Performance est un outil puissant mais complexe. Ne vous découragez pas si tout n'est pas clair immédiatement !

**Progression naturelle** :
1. **Semaine 1** : Comprendre FPS, CPU, NET
2. **Semaine 2** : Identifier les long tasks
3. **Semaine 3** : Analyser les fonctions problématiques
4. **Semaine 4** : Optimiser basé sur les données

Avec la pratique, vous développerez des **réflexes** et saurez immédiatement où regarder !

---

> 💡 **Citation de Donald Knuth** :
> *"Premature optimization is the root of all evil."*
>
> Mais l'optimisation **basée sur des mesures réelles** avec l'onglet Performance ? Ça, c'est de la sagesse ! 📊⚡

⏭️ [Onglet Network et analyse des requêtes](/07-debugging-et-outils-avances/02-performance-optimisation/02-onglet-network.md)
