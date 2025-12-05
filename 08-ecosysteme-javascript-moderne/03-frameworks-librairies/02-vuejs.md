🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.3.2 Vue.js : framework progressif 🆕

## Introduction à Vue.js

**Vue.js** (prononcé "view") est un framework JavaScript créé par Evan You en 2014. C'est l'un des frameworks les plus populaires pour construire des interfaces utilisateur, reconnu pour sa **simplicité** et sa **flexibilité**.

### Qu'est-ce que Vue.js ?

Vue.js est un **framework progressif**, ce qui signifie que vous pouvez l'adopter progressivement :
- Commencer par ajouter Vue à une seule page HTML
- L'utiliser pour des composants interactifs spécifiques
- Construire une application complète (Single Page Application)

**Analogie simple :** Vue.js est comme un couteau suisse. Vous pouvez utiliser seulement les outils dont vous avez besoin. Besoin juste d'un tournevis ? Pas besoin de sortir tout le couteau ! Besoin de tous les outils ? Ils sont là aussi.

### Pourquoi "progressif" ?

```
Niveau 1 : Vue simple dans une page HTML
    ↓
Niveau 2 : Composants réutilisables
    ↓
Niveau 3 : Routage (Vue Router)
    ↓
Niveau 4 : Gestion d'état (Pinia)
    ↓
Niveau 5 : Application complète avec build tools
```

Vous n'êtes pas obligé de tout utiliser dès le départ !

---

## Pourquoi utiliser Vue.js ?

### Avantages principaux

1. **Courbe d'apprentissage douce** : Plus facile à apprendre que React ou Angular
2. **Documentation exceptionnelle** : Claire, complète, avec exemples
3. **Syntaxe intuitive** : Proche du HTML/CSS/JS classique
4. **Réactivité automatique** : Les données et l'interface restent synchronisées
5. **Écosystème cohérent** : Outils officiels (Router, Pinia, DevTools)
6. **Performances excellentes** : Léger et rapide
7. **Communauté francophone active** : Beaucoup de ressources en français

### Vue.js vs React

| Caractéristique | **Vue.js** | **React** |
|----------------|------------|-----------|
| **Courbe d'apprentissage** | 🟢 Facile | 🟡 Moyenne |
| **Syntaxe** | HTML-like | JSX |
| **Taille** | ~40 KB | ~45 KB |
| **Création** | Communauté (Evan You) | Facebook/Meta |
| **Outils officiels** | ✅ Oui (Router, Pinia) | ❌ Non (écosystème tiers) |
| **Adoption** | Moyenne | Très élevée |

### Quand utiliser Vue.js ?

- **✅ Applications web interactives**
- **✅ Tableaux de bord et interfaces d'administration**
- **✅ Projets nécessitant une montée en charge progressive**
- **✅ Équipes préférant une syntaxe proche du HTML**
- **✅ Prototypes et MVPs rapides**

### Quand NE PAS utiliser Vue.js ?

- **❌ Sites vitrines simples statiques**
- **❌ Si l'équipe maîtrise déjà un autre framework**
- **❌ Projets nécessitant l'écosystème React/React Native**

---

## Démarrage rapide : Vue.js dans une page HTML

Une des forces de Vue : vous pouvez commencer sans installation !

### Version la plus simple possible

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Ma première app Vue</title>
  <!-- Importer Vue depuis un CDN -->
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <button @click="changerMessage">Cliquer</button>
  </div>

  <script>
    const { createApp } = Vue;

    createApp({
      data() {
        return {
          message: 'Bonjour Vue.js !'
        }
      },
      methods: {
        changerMessage() {
          this.message = 'Message modifié !';
        }
      }
    }).mount('#app');
  </script>
</body>
</html>
```

**Ça fonctionne ! Aucune installation, aucun build tool.** 🎉

---

## Les Fondamentaux de Vue.js

### 1. La Réactivité

Le concept central de Vue est la **réactivité** : quand vos données changent, l'interface se met à jour automatiquement.

```html
<div id="app">
  <p>{{ compteur }}</p>
  <button @click="compteur++">+1</button>
</div>

<script>
createApp({
  data() {
    return {
      compteur: 0
    }
  }
}).mount('#app');
</script>
```

**Explication :**
- `{{ compteur }}` affiche la valeur
- `@click="compteur++"` modifie la valeur
- Vue met à jour l'affichage automatiquement ✨

### 2. Les Données (data)

La fonction `data()` retourne un objet contenant toutes les données réactives.

```javascript
createApp({
  data() {
    return {
      nom: 'Marie',
      age: 25,
      estConnecte: false,
      taches: ['Apprendre Vue', 'Créer un projet'],
      utilisateur: {
        prenom: 'Jean',
        nom: 'Dupont'
      }
    }
  }
}).mount('#app');
```

**Important :** Toutes les propriétés définies dans `data()` deviennent réactives.

### 3. L'Interpolation de texte

Utilisez les doubles accolades `{{ }}` pour afficher des données.

```html
<div id="app">
  <h1>{{ titre }}</h1>
  <p>Bonjour {{ prenom }} {{ nom }} !</p>
  <p>2 + 2 = {{ 2 + 2 }}</p>
  <p>{{ message.toUpperCase() }}</p>
</div>
```

**⚠️ Attention :** L'interpolation fonctionne uniquement dans le contenu des balises, pas dans les attributs.

```html
<!-- ❌ INCORRECT -->
<img src="{{ urlImage }}">

<!-- ✅ CORRECT (voir directives v-bind) -->
<img :src="urlImage">
```

---

## Les Directives Vue

Les **directives** sont des attributs spéciaux préfixés par `v-` qui appliquent un comportement réactif au DOM.

### v-bind : Lier des attributs

Lie une valeur à un attribut HTML.

```html
<div id="app">
  <!-- Syntaxe complète -->
  <img v-bind:src="urlImage" v-bind:alt="description">

  <!-- Syntaxe raccourcie (recommandée) -->
  <img :src="urlImage" :alt="description">

  <!-- Lier des classes CSS -->
  <div :class="classeActive">Contenu</div>

  <!-- Lier des styles -->
  <p :style="{ color: couleur, fontSize: taille + 'px' }">Texte stylé</p>
</div>

<script>
createApp({
  data() {
    return {
      urlImage: 'https://exemple.com/photo.jpg',
      description: 'Une belle photo',
      classeActive: 'actif',
      couleur: 'blue',
      taille: 20
    }
  }
}).mount('#app');
</script>
```

### v-on : Gérer les événements

Écoute les événements du DOM.

```html
<div id="app">
  <!-- Syntaxe complète -->
  <button v-on:click="incrementer">Incrémenter</button>

  <!-- Syntaxe raccourcie (recommandée) -->
  <button @click="incrementer">Incrémenter</button>

  <!-- Événements divers -->
  <input @input="gererSaisie" @focus="surFocus">
  <form @submit.prevent="soumettre">
    <button type="submit">Envoyer</button>
  </form>
</div>

<script>
createApp({
  data() {
    return {
      compteur: 0
    }
  },
  methods: {
    incrementer() {
      this.compteur++;
    },
    gererSaisie(event) {
      console.log(event.target.value);
    },
    surFocus() {
      console.log('Input en focus');
    },
    soumettre() {
      console.log('Formulaire soumis');
    }
  }
}).mount('#app');
</script>
```

**Modificateurs d'événements :**
- `.prevent` : `event.preventDefault()`
- `.stop` : `event.stopPropagation()`
- `.once` : Événement déclenché une seule fois

### v-model : Liaison bidirectionnelle

Crée une liaison bidirectionnelle entre un champ de formulaire et une donnée.

```html
<div id="app">
  <input v-model="nom" type="text" placeholder="Votre nom">
  <p>Bonjour {{ nom }} !</p>

  <textarea v-model="message"></textarea>
  <p>Message : {{ message }}</p>

  <input v-model="accepte" type="checkbox">
  <label>J'accepte les conditions</label>
  <p>État : {{ accepte }}</p>

  <select v-model="choix">
    <option value="option1">Option 1</option>
    <option value="option2">Option 2</option>
  </select>
  <p>Choix : {{ choix }}</p>
</div>

<script>
createApp({
  data() {
    return {
      nom: '',
      message: '',
      accepte: false,
      choix: 'option1'
    }
  }
}).mount('#app');
</script>
```

**C'est magique !** La donnée et le champ restent toujours synchronisés. ✨

### v-if, v-else-if, v-else : Rendu conditionnel

Affiche ou masque des éléments selon une condition.

```html
<div id="app">
  <button @click="basculerConnexion">
    {{ estConnecte ? 'Se déconnecter' : 'Se connecter' }}
  </button>

  <div v-if="estConnecte">
    <h2>Bienvenue !</h2>
    <p>Vous êtes connecté.</p>
  </div>
  <div v-else>
    <h2>Veuillez vous connecter</h2>
  </div>

  <!-- Exemple avec v-else-if -->
  <p v-if="score >= 18">Excellent !</p>
  <p v-else-if="score >= 15">Très bien</p>
  <p v-else-if="score >= 10">Bien</p>
  <p v-else>Peut mieux faire</p>
</div>

<script>
createApp({
  data() {
    return {
      estConnecte: false,
      score: 16
    }
  },
  methods: {
    basculerConnexion() {
      this.estConnecte = !this.estConnecte;
    }
  }
}).mount('#app');
</script>
```

**v-if vs v-show :**
- `v-if` : Ajoute/retire l'élément du DOM (coût plus élevé)
- `v-show` : Cache avec CSS `display: none` (coût moindre)

```html
<!-- Utilisez v-show si l'élément change souvent d'état -->
<div v-show="estVisible">Contenu visible/caché</div>
```

### v-for : Rendu de listes

Parcourt et affiche des tableaux ou des objets.

```html
<div id="app">
  <!-- Liste simple -->
  <ul>
    <li v-for="fruit in fruits" :key="fruit">
      {{ fruit }}
    </li>
  </ul>

  <!-- Avec index -->
  <ul>
    <li v-for="(fruit, index) in fruits" :key="index">
      {{ index + 1 }}. {{ fruit }}
    </li>
  </ul>

  <!-- Liste d'objets -->
  <div v-for="utilisateur in utilisateurs" :key="utilisateur.id">
    <h3>{{ utilisateur.nom }}</h3>
    <p>{{ utilisateur.email }}</p>
  </div>
</div>

<script>
createApp({
  data() {
    return {
      fruits: ['Pomme', 'Banane', 'Orange'],
      utilisateurs: [
        { id: 1, nom: 'Marie', email: 'marie@exemple.com' },
        { id: 2, nom: 'Jean', email: 'jean@exemple.com' }
      ]
    }
  }
}).mount('#app');
</script>
```

**⚠️ Important :** Toujours utiliser `:key` avec un identifiant unique pour optimiser les performances.

---

## Les Méthodes (methods)

Les méthodes sont des fonctions qui peuvent être appelées depuis le template ou depuis d'autres méthodes.

```html
<div id="app">
  <p>{{ compteur }}</p>
  <button @click="incrementer">+1</button>
  <button @click="decrementer">-1</button>
  <button @click="reinitialiser">Reset</button>
</div>

<script>
createApp({
  data() {
    return {
      compteur: 0
    }
  },
  methods: {
    incrementer() {
      this.compteur++;
    },
    decrementer() {
      this.compteur--;
    },
    reinitialiser() {
      this.compteur = 0;
    }
  }
}).mount('#app');
</script>
```

**Note :** Utilisez `this` pour accéder aux données et aux autres méthodes.

---

## Les Propriétés Calculées (computed)

Les **propriétés calculées** sont des valeurs dérivées qui se mettent à jour automatiquement.

```html
<div id="app">
  <input v-model="prenom" placeholder="Prénom">
  <input v-model="nom" placeholder="Nom">

  <!-- Propriété calculée -->
  <p>Nom complet : {{ nomComplet }}</p>

  <!-- Liste filtrée -->
  <input v-model="recherche" placeholder="Rechercher...">
  <ul>
    <li v-for="fruit in fruitsFiltres" :key="fruit">
      {{ fruit }}
    </li>
  </ul>
</div>

<script>
createApp({
  data() {
    return {
      prenom: '',
      nom: '',
      recherche: '',
      fruits: ['Pomme', 'Banane', 'Orange', 'Poire', 'Ananas']
    }
  },
  computed: {
    nomComplet() {
      return `${this.prenom} ${this.nom}`.trim();
    },
    fruitsFiltres() {
      return this.fruits.filter(fruit =>
        fruit.toLowerCase().includes(this.recherche.toLowerCase())
      );
    }
  }
}).mount('#app');
</script>
```

### Computed vs Methods

| **Computed** | **Methods** |
|--------------|-------------|
| Mise en cache | Pas de cache |
| Réexécuté seulement si dépendances changent | Réexécuté à chaque re-rendu |
| Utilisé pour des valeurs dérivées | Utilisé pour des actions |
| Pas de paramètres | Accepte des paramètres |

**Règle :** Utilisez `computed` pour calculer des valeurs, `methods` pour des actions.

---

## Les Observateurs (watchers)

Les **watchers** permettent de réagir aux changements d'une donnée.

```html
<div id="app">
  <input v-model="question" placeholder="Posez une question">
  <p>{{ reponse }}</p>
</div>

<script>
createApp({
  data() {
    return {
      question: '',
      reponse: 'Posez une question !'
    }
  },
  watch: {
    question(nouvelleQuestion, ancienneQuestion) {
      if (nouvelleQuestion.includes('?')) {
        this.reponse = 'Réflexion en cours...';
        setTimeout(() => {
          this.reponse = 'Je ne sais pas !';
        }, 1000);
      }
    }
  }
}).mount('#app');
</script>
```

**Quand utiliser watch ?**
- Requêtes asynchrones déclenchées par un changement
- Effets de bord complexes
- Validation personnalisée

---

## Exemple complet : Liste de tâches

Voici une application complète qui combine tous les concepts.

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Liste de tâches Vue</title>
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 50px auto; }
    .tache { padding: 10px; margin: 5px 0; border: 1px solid #ddd; display: flex; justify-content: space-between; align-items: center; }
    .tache.termine { text-decoration: line-through; opacity: 0.6; }
    button { cursor: pointer; padding: 5px 10px; }
    input[type="text"] { padding: 8px; width: 400px; }
  </style>
</head>
<body>
  <div id="app">
    <h1>Ma Liste de Tâches</h1>

    <!-- Formulaire d'ajout -->
    <div>
      <input
        v-model="nouvelleTache"
        @keyup.enter="ajouterTache"
        type="text"
        placeholder="Nouvelle tâche..."
      >
      <button @click="ajouterTache">Ajouter</button>
    </div>

    <!-- Filtres -->
    <div style="margin: 20px 0;">
      <button @click="filtre = 'tous'">Tous ({{ taches.length }})</button>
      <button @click="filtre = 'actifs'">Actifs ({{ tachesActives.length }})</button>
      <button @click="filtre = 'termines'">Terminés ({{ tachesTerminees.length }})</button>
    </div>

    <!-- Liste des tâches -->
    <div v-if="tachesFiltrees.length === 0">
      <p>Aucune tâche à afficher.</p>
    </div>

    <div
      v-for="tache in tachesFiltrees"
      :key="tache.id"
      :class="['tache', { termine: tache.termine }]"
    >
      <div>
        <input
          type="checkbox"
          v-model="tache.termine"
        >
        {{ tache.texte }}
      </div>
      <button @click="supprimerTache(tache.id)">❌</button>
    </div>

    <!-- Actions globales -->
    <div style="margin-top: 20px;" v-if="taches.length > 0">
      <button @click="toutSupprimer">Tout supprimer</button>
    </div>
  </div>

  <script>
    const { createApp } = Vue;

    createApp({
      data() {
        return {
          nouvelleTache: '',
          filtre: 'tous',
          taches: [
            { id: 1, texte: 'Apprendre Vue.js', termine: false },
            { id: 2, texte: 'Créer un projet', termine: false },
            { id: 3, texte: 'Déployer l\'application', termine: false }
          ],
          prochainId: 4
        }
      },
      computed: {
        tachesActives() {
          return this.taches.filter(t => !t.termine);
        },
        tachesTerminees() {
          return this.taches.filter(t => t.termine);
        },
        tachesFiltrees() {
          if (this.filtre === 'actifs') {
            return this.tachesActives;
          } else if (this.filtre === 'termines') {
            return this.tachesTerminees;
          }
          return this.taches;
        }
      },
      methods: {
        ajouterTache() {
          if (this.nouvelleTache.trim() === '') {
            return;
          }

          this.taches.push({
            id: this.prochainId++,
            texte: this.nouvelleTache,
            termine: false
          });

          this.nouvelleTache = '';
        },
        supprimerTache(id) {
          this.taches = this.taches.filter(t => t.id !== id);
        },
        toutSupprimer() {
          if (confirm('Supprimer toutes les tâches ?')) {
            this.taches = [];
          }
        }
      }
    }).mount('#app');
  </script>
</body>
</html>
```

---

## Les Composants Vue

Les **composants** permettent de découper l'interface en morceaux réutilisables.

### Composant simple

```html
<div id="app">
  <bouton-compteur></bouton-compteur>
  <bouton-compteur></bouton-compteur>
</div>

<script>
const { createApp } = Vue;

const app = createApp({});

// Définir un composant
app.component('bouton-compteur', {
  data() {
    return {
      compteur: 0
    }
  },
  template: `
    <button @click="compteur++">
      Cliqué {{ compteur }} fois
    </button>
  `
});

app.mount('#app');
</script>
```

**Chaque instance de composant a son propre état !**

### Composant avec props

```html
<div id="app">
  <carte-utilisateur
    nom="Marie Dupont"
    :age="25"
    email="marie@exemple.com">
  </carte-utilisateur>
</div>

<script>
const app = createApp({});

app.component('carte-utilisateur', {
  props: ['nom', 'age', 'email'],
  template: `
    <div style="border: 1px solid #ddd; padding: 20px; margin: 10px;">
      <h3>{{ nom }}</h3>
      <p>Âge : {{ age }} ans</p>
      <p>Email : {{ email }}</p>
    </div>
  `
});

app.mount('#app');
</script>
```

### Composant avec événements personnalisés

```html
<div id="app">
  <p>Total : {{ total }}</p>
  <bouton-incrementer @incrementer="augmenter"></bouton-incrementer>
</div>

<script>
const app = createApp({
  data() {
    return {
      total: 0
    }
  },
  methods: {
    augmenter() {
      this.total++;
    }
  }
});

app.component('bouton-incrementer', {
  template: `
    <button @click="$emit('incrementer')">
      Incrémenter
    </button>
  `
});

app.mount('#app');
</script>
```

---

## Cycles de vie (Lifecycle Hooks)

Les **hooks de cycle de vie** permettent d'exécuter du code à des moments précis.

```javascript
createApp({
  data() {
    return {
      message: 'Hello'
    }
  },
  // AVANT la création
  beforeCreate() {
    console.log('beforeCreate - Les données ne sont pas encore accessibles');
  },
  // APRÈS la création
  created() {
    console.log('created - Les données sont prêtes');
    // Bon endroit pour les requêtes API
  },
  // AVANT le montage dans le DOM
  beforeMount() {
    console.log('beforeMount - Le DOM n\'est pas encore créé');
  },
  // APRÈS le montage dans le DOM
  mounted() {
    console.log('mounted - Le composant est dans le DOM');
    // Bon endroit pour manipuler le DOM, initialiser des bibliothèques tierces
  },
  // AVANT la mise à jour
  beforeUpdate() {
    console.log('beforeUpdate - Une donnée va changer');
  },
  // APRÈS la mise à jour
  updated() {
    console.log('updated - Le DOM a été mis à jour');
  },
  // AVANT la destruction
  beforeUnmount() {
    console.log('beforeUnmount - Le composant va être détruit');
  },
  // APRÈS la destruction
  unmounted() {
    console.log('unmounted - Le composant est détruit');
    // Bon endroit pour nettoyer (timers, événements, etc.)
  }
}).mount('#app');
```

**Les plus utilisés :**
- `created()` : Requêtes API, initialisation de données
- `mounted()` : Manipulation du DOM, bibliothèques tierces
- `unmounted()` : Nettoyage (timers, listeners)

---

## Créer un projet Vue avec les outils modernes

### Option 1 : Vue CLI (traditionnel)

```bash
npm install -g @vue/cli
vue create mon-projet
cd mon-projet
npm run serve
```

### Option 2 : create-vue (Vite) ⭐ Recommandé

```bash
npm create vue@latest
# Suivez les instructions
cd mon-projet
npm install
npm run dev
```

**Vite est plus rapide et moderne !**

### Structure d'un projet Vue

```
mon-projet/
├── node_modules/
├── public/
│   └── favicon.ico
├── src/
│   ├── assets/          # Images, CSS
│   ├── components/      # Composants réutilisables
│   │   └── MonComposant.vue
│   ├── views/           # Pages / Vues
│   │   └── HomeView.vue
│   ├── App.vue          # Composant racine
│   └── main.js          # Point d'entrée
├── index.html
├── package.json
└── vite.config.js
```

---

## Fichiers .vue (Single File Components)

Les composants Vue sont généralement dans des fichiers `.vue` avec trois sections.

### Structure d'un fichier .vue

```vue
<!-- MonComposant.vue -->
<template>
  <div class="mon-composant">
    <h2>{{ titre }}</h2>
    <p>{{ message }}</p>
    <button @click="changerMessage">Changer</button>
  </div>
</template>

<script>
export default {
  name: 'MonComposant',
  data() {
    return {
      titre: 'Mon Super Composant',
      message: 'Bienvenue dans Vue.js !'
    }
  },
  methods: {
    changerMessage() {
      this.message = 'Message modifié !';
    }
  }
}
</script>

<style scoped>
.mon-composant {
  border: 2px solid #42b883;
  padding: 20px;
  border-radius: 8px;
}

h2 {
  color: #42b883;
}
</style>
```

**Sections :**
1. `<template>` : Structure HTML du composant
2. `<script>` : Logique JavaScript
3. `<style scoped>` : Styles CSS (scoped = uniquement pour ce composant)

---

## Composition API vs Options API

Vue 3 introduit une nouvelle façon d'écrire des composants : la **Composition API**.

### Options API (classique, ce qu'on a vu jusqu'ici)

```vue
<script>
export default {
  data() {
    return {
      compteur: 0
    }
  },
  methods: {
    incrementer() {
      this.compteur++;
    }
  },
  computed: {
    double() {
      return this.compteur * 2;
    }
  }
}
</script>
```

### Composition API (moderne)

```vue
<script setup>
import { ref, computed } from 'vue';

const compteur = ref(0);

const incrementer = () => {
  compteur.value++;
};

const double = computed(() => compteur.value * 2);
</script>

<template>
  <div>
    <p>Compteur : {{ compteur }}</p>
    <p>Double : {{ double }}</p>
    <button @click="incrementer">+1</button>
  </div>
</template>
```

**Pour les débutants :** Commencez avec l'Options API, elle est plus simple à comprendre. La Composition API devient utile pour des projets plus complexes.

---

## Vue Router : Navigation entre pages

**Vue Router** est la solution officielle pour gérer la navigation dans une SPA Vue.

### Installation

```bash
npm install vue-router@4
```

### Configuration basique

```javascript
// router/index.js
import { createRouter, createWebHistory } from 'vue-router';
import Home from '../views/Home.vue';
import About from '../views/About.vue';

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: About
  }
];

const router = createRouter({
  history: createWebHistory(),
  routes
});

export default router;
```

### Utilisation dans les composants

```vue
<template>
  <div>
    <nav>
      <router-link to="/">Accueil</router-link>
      <router-link to="/about">À propos</router-link>
    </nav>

    <!-- Le composant de la route actuelle s'affiche ici -->
    <router-view></router-view>
  </div>
</template>
```

---

## Pinia : Gestion d'état

**Pinia** est la solution officielle pour gérer un état global (remplace Vuex).

### Installation

```bash
npm install pinia
```

### Créer un store

```javascript
// stores/counter.js
import { defineStore } from 'pinia';

export const useCounterStore = defineStore('counter', {
  state: () => ({
    compteur: 0
  }),
  getters: {
    double: (state) => state.compteur * 2
  },
  actions: {
    incrementer() {
      this.compteur++;
    }
  }
});
```

### Utiliser le store

```vue
<script setup>
import { useCounterStore } from '@/stores/counter';

const store = useCounterStore();
</script>

<template>
  <div>
    <p>Compteur : {{ store.compteur }}</p>
    <p>Double : {{ store.double }}</p>
    <button @click="store.incrementer()">+1</button>
  </div>
</template>
```

---

## Bonnes pratiques Vue.js

### ✅ À FAIRE

1. **Nommer les composants en PascalCase**
   ```javascript
   MonComposant.vue  // ✅
   mon-composant.vue // ❌
   ```

2. **Utiliser des props typées**
   ```javascript
   props: {
     nom: {
       type: String,
       required: true
     },
     age: {
       type: Number,
       default: 0
     }
   }
   ```

3. **Un composant = une responsabilité**

4. **Utiliser `computed` pour les valeurs dérivées**

5. **Toujours utiliser `:key` avec `v-for`**

### ❌ À ÉVITER

1. **Modifier les props directement**
   ```javascript
   // ❌ INCORRECT
   props: ['valeur'],
   methods: {
     changer() {
       this.valeur = 'nouveau'; // ERREUR !
     }
   }

   // ✅ CORRECT : Utiliser un événement
   this.$emit('update:valeur', 'nouveau');
   ```

2. **Manipuler le DOM directement** (utiliser les directives Vue)

3. **Logique métier dans les templates** (utiliser computed/methods)

4. **Oublier le `scoped` dans les styles** (pollution CSS)

---

## Ressources pour aller plus loin

### Documentation officielle
- **Vue.js officiel** : https://vuejs.org/
- **Vue.js en français** : https://fr.vuejs.org/
- **Vue Router** : https://router.vuejs.org/
- **Pinia** : https://pinia.vuejs.org/

### Tutoriels recommandés
- **Vue Mastery** : Cours vidéo de qualité
- **Vue School** : Formations complètes
- **Grafikart (français)** : Excellents tutoriels Vue

### Outils
- **Vue DevTools** : Extension navigateur essentielle
- **Vite** : Build tool officiel
- **Volar** : Extension VS Code pour Vue

### Écosystème
- **Nuxt.js** : Framework Vue pour SSR et sites statiques
- **Vuetify** : Composants Material Design
- **Quasar** : Framework complet (web, mobile, desktop)

---

## Comparaison rapide : Vue vs React

```javascript
// REACT
import { useState } from 'react';

function Compteur() {
  const [compteur, setCompteur] = useState(0);

  return (
    <div>
      <p>{compteur}</p>
      <button onClick={() => setCompteur(compteur + 1)}>+1</button>
    </div>
  );
}
```

```vue
<!-- VUE -->
<template>
  <div>
    <p>{{ compteur }}</p>
    <button @click="compteur++">+1</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      compteur: 0
    }
  }
}
</script>
```

**Vue est souvent considéré comme plus intuitif pour les débutants.**

---

## Concepts clés à retenir

### 1. **Réactivité automatique**
```javascript
data() {
  return { message: 'Hello' }
}
// Modifier message met à jour l'interface automatiquement
```

### 2. **Directives pour le DOM**
```html
v-bind (:)    → Lier attributs
v-on (@)      → Gérer événements
v-model       → Liaison bidirectionnelle
v-if / v-show → Rendu conditionnel
v-for         → Listes
```

### 3. **Options API structure**
```javascript
{
  data()      → État local
  computed    → Valeurs calculées
  methods     → Fonctions
  watch       → Observateurs
  mounted()   → Après le montage
}
```

### 4. **Composants = Blocs réutilisables**
```vue
<mon-composant :prop="valeur" @evenement="action" />
```

### 5. **Écosystème officiel cohérent**
- Vue Router (navigation)
- Pinia (état global)
- Vite (build tool)

---

## Exemple final : Compteur avancé

```vue
<!-- CompteurAvance.vue -->
<template>
  <div class="compteur">
    <h1>Compteur Vue.js</h1>

    <div class="affichage" :class="{ negatif: compteur < 0 }">
      <p>{{ compteur }}</p>
    </div>

    <div class="controles">
      <button @click="decrementer" :disabled="compteur === 0">
        -{{ pas }}
      </button>
      <button @click="reinitialiser">Reset</button>
      <button @click="incrementer">+{{ pas }}</button>
    </div>

    <div class="reglages">
      <label>
        Pas :
        <input
          type="number"
          v-model.number="pas"
          min="1"
        >
      </label>
    </div>

    <div v-if="afficherStats" class="stats">
      <p>Historique : {{ historique.length }} actions</p>
      <p>Maximum atteint : {{ max }}</p>
    </div>

    <button @click="afficherStats = !afficherStats">
      {{ afficherStats ? 'Masquer' : 'Afficher' }} stats
    </button>
  </div>
</template>

<script>
export default {
  name: 'CompteurAvance',
  data() {
    return {
      compteur: 0,
      pas: 1,
      historique: [],
      afficherStats: false
    }
  },
  computed: {
    max() {
      return this.historique.length > 0
        ? Math.max(...this.historique)
        : 0;
    }
  },
  methods: {
    incrementer() {
      this.compteur += this.pas;
      this.historique.push(this.compteur);
    },
    decrementer() {
      if (this.compteur > 0) {
        this.compteur -= this.pas;
        this.historique.push(this.compteur);
      }
    },
    reinitialiser() {
      this.compteur = 0;
      this.historique = [];
    }
  },
  watch: {
    compteur(nouveau, ancien) {
      console.log(`Compteur passé de ${ancien} à ${nouveau}`);
    }
  }
}
</script>

<style scoped>
.compteur {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 2px solid #42b883;
  border-radius: 10px;
  text-align: center;
}

.affichage {
  font-size: 48px;
  font-weight: bold;
  color: #42b883;
  margin: 20px 0;
}

.affichage.negatif {
  color: #e74c3c;
}

.controles button {
  margin: 5px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

.reglages {
  margin: 20px 0;
}

.stats {
  background: #f0f0f0;
  padding: 10px;
  margin: 20px 0;
  border-radius: 5px;
}
</style>
```

---

## Conclusion

Vue.js est un excellent choix pour apprendre le développement web moderne. Sa **syntaxe intuitive**, sa **documentation exceptionnelle** et sa **courbe d'apprentissage progressive** en font un framework idéal pour les débutants.

**Points forts de Vue.js :**
- ✅ Facile à apprendre et à utiliser
- ✅ Documentation claire et complète
- ✅ Réactivité automatique et performante
- ✅ Écosystème officiel cohérent
- ✅ Excellent pour les projets de toutes tailles
- ✅ Communauté active et bienveillante

**Ce qu'il faut retenir :**
- Vue = HTML enrichi avec directives et réactivité
- Directives (`v-if`, `v-for`, `v-model`, etc.) pour contrôler le DOM
- Composants pour organiser le code
- Options API simple et intuitive
- Écosystème complet (Router, Pinia, Vite)

Avec ces fondamentaux, vous êtes prêt à créer vos premières applications Vue.js ! 🚀

---


⏭️ [Angular : framework complet](/08-ecosysteme-javascript-moderne/03-frameworks-librairies/03-angular.md)
