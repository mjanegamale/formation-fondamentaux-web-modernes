🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.3.1 React : composants et état 🆕

## Introduction à React

**React** est une bibliothèque JavaScript créée par Facebook (Meta) en 2013 pour construire des interfaces utilisateur (UI). C'est aujourd'hui l'une des solutions les plus populaires pour développer des applications web modernes.

### Qu'est-ce que React ?

React n'est pas un framework complet, mais une **bibliothèque spécialisée** dans la construction d'interfaces utilisateur. Son principe fondamental est de découper l'interface en **composants réutilisables** qui gèrent leur propre état et affichage.

**Analogie simple :** Imaginez que vous construisez une maison avec des LEGO. Plutôt que de tout construire d'un bloc, vous créez des pièces individuelles (fenêtres, portes, murs) que vous pouvez réutiliser et assembler différemment. React fonctionne de la même manière avec les éléments d'interface.

### Pourquoi utiliser React ?

#### Avantages principaux

1. **Composants réutilisables** : Écrivez une fois, utilisez partout
2. **DOM Virtuel** : Performances optimisées (React ne met à jour que ce qui change)
3. **Unidirectionnalité des données** : Flux de données prévisible et facile à débugger
4. **Écosystème riche** : Immense communauté et milliers de bibliothèques
5. **Syntaxe déclarative** : Vous décrivez "ce que" vous voulez afficher, pas "comment"

#### Quand utiliser React ?

- **✅ Applications web dynamiques** avec beaucoup d'interactions
- **✅ Single Page Applications (SPA)**
- **✅ Tableaux de bord et interfaces complexes**
- **✅ Applications nécessitant des mises à jour fréquentes de l'interface**

#### Quand NE PAS utiliser React ?

- **❌ Sites vitrines simples** (HTML/CSS/JS vanilla suffisent)
- **❌ Sites à contenu majoritairement statique**
- **❌ Projets très simples** (surcharge inutile)

---

## Les Fondamentaux de React

### 1. Les Composants

Un **composant** est une fonction JavaScript qui retourne du JSX (une syntaxe proche du HTML). C'est l'unité de base dans React.

#### Exemple de composant simple

```jsx
// Composant fonctionnel moderne
function Bienvenue() {
  return <h1>Bonjour et bienvenue sur mon site !</h1>;
}
```

#### Composant avec paramètres (props)

```jsx
function Bienvenue(props) {
  return <h1>Bonjour {props.nom} !</h1>;
}

// Utilisation
<Bienvenue nom="Marie" />
// Affichera : Bonjour Marie !
```

#### Déstructuration des props (syntaxe moderne)

```jsx
function Bienvenue({ nom, age }) {
  return (
    <div>
      <h1>Bonjour {nom} !</h1>
      <p>Tu as {age} ans.</p>
    </div>
  );
}

// Utilisation
<Bienvenue nom="Marie" age={25} />
```

### 2. JSX - JavaScript XML

**JSX** est une extension syntaxique de JavaScript qui ressemble à du HTML mais qui est en réalité du JavaScript.

#### Règles importantes du JSX

```jsx
// ✅ CORRECT : Un seul élément parent
function MonComposant() {
  return (
    <div>
      <h1>Titre</h1>
      <p>Paragraphe</p>
    </div>
  );
}

// ❌ INCORRECT : Plusieurs éléments racine
function MonComposant() {
  return (
    <h1>Titre</h1>
    <p>Paragraphe</p>
  );
}

// ✅ SOLUTION : Fragment React (ne crée pas d'élément DOM)
function MonComposant() {
  return (
    <>
      <h1>Titre</h1>
      <p>Paragraphe</p>
    </>
  );
}
```

#### Expressions JavaScript dans JSX

```jsx
function Calculatrice() {
  const nombre1 = 10;
  const nombre2 = 5;

  return (
    <div>
      <p>{nombre1} + {nombre2} = {nombre1 + nombre2}</p>
      <p>Message en majuscules : {"hello".toUpperCase()}</p>
    </div>
  );
}
```

#### Attributs en JSX

```jsx
function MonImage() {
  const urlImage = "https://exemple.com/image.jpg";
  const description = "Une belle photo";

  return (
    <div>
      {/* className au lieu de class */}
      <div className="conteneur-image">
        <img src={urlImage} alt={description} />
      </div>

      {/* Style en objet JavaScript */}
      <p style={{ color: 'blue', fontSize: '20px' }}>
        Texte stylé
      </p>
    </div>
  );
}
```

**⚠️ Différences importantes avec le HTML :**
- `class` devient `className`
- `for` (label) devient `htmlFor`
- Styles inline en objet : `style={{ propriété: 'valeur' }}`
- Attributs en camelCase : `onClick`, `onChange`, `backgroundColor`

---

## L'État (State)

### Qu'est-ce que l'état ?

L'**état** (state) est un objet qui contient des données propres au composant. Quand l'état change, React **re-rend automatiquement** le composant pour refléter les nouvelles données.

**Analogie :** Imaginez un interrupteur de lumière. Son état peut être "allumé" ou "éteint". Quand vous changez l'état, la lumière change automatiquement.

### useState - Le Hook d'état

React utilise des **Hooks** (fonctions spéciales) pour gérer l'état. Le plus important est `useState`.

#### Syntaxe de base

```jsx
import { useState } from 'react';

function Compteur() {
  // useState retourne un tableau avec 2 éléments :
  // 1. La valeur actuelle de l'état
  // 2. Une fonction pour modifier cet état
  const [compteur, setCompteur] = useState(0);

  return (
    <div>
      <p>Compteur : {compteur}</p>
      <button onClick={() => setCompteur(compteur + 1)}>
        Incrémenter
      </button>
    </div>
  );
}
```

**Décomposition :**
- `const [compteur, setCompteur]` : destructuration du tableau retourné
- `compteur` : variable contenant la valeur actuelle (0 au départ)
- `setCompteur` : fonction pour modifier la valeur
- `useState(0)` : valeur initiale de l'état

#### Exemple : Afficher/Masquer du contenu

```jsx
function ToggleTexte() {
  const [estVisible, setEstVisible] = useState(false);

  return (
    <div>
      <button onClick={() => setEstVisible(!estVisible)}>
        {estVisible ? 'Masquer' : 'Afficher'}
      </button>

      {estVisible && (
        <p>Ce texte peut être affiché ou masqué !</p>
      )}
    </div>
  );
}
```

#### Exemple : Formulaire avec état

```jsx
function FormulaireNom() {
  const [nom, setNom] = useState('');

  const gererChangement = (event) => {
    setNom(event.target.value);
  };

  return (
    <div>
      <input
        type="text"
        value={nom}
        onChange={gererChangement}
        placeholder="Entrez votre nom"
      />
      <p>Bonjour {nom || 'Invité'} !</p>
    </div>
  );
}
```

### État avec plusieurs valeurs

#### Plusieurs useState

```jsx
function Profil() {
  const [nom, setNom] = useState('');
  const [age, setAge] = useState(0);
  const [email, setEmail] = useState('');

  return (
    <div>
      <input
        type="text"
        value={nom}
        onChange={(e) => setNom(e.target.value)}
        placeholder="Nom"
      />
      <input
        type="number"
        value={age}
        onChange={(e) => setAge(Number(e.target.value))}
        placeholder="Âge"
      />
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Email"
      />
    </div>
  );
}
```

#### useState avec un objet (alternative)

```jsx
function Profil() {
  const [profil, setProfil] = useState({
    nom: '',
    age: 0,
    email: ''
  });

  const gererChangement = (champ, valeur) => {
    setProfil({
      ...profil,  // Copie l'objet existant
      [champ]: valeur  // Met à jour le champ modifié
    });
  };

  return (
    <div>
      <input
        type="text"
        value={profil.nom}
        onChange={(e) => gererChangement('nom', e.target.value)}
        placeholder="Nom"
      />
      <p>Nom : {profil.nom}</p>
    </div>
  );
}
```

---

## Props vs State

### Props (Propriétés)

- **Lecture seule** : ne peuvent pas être modifiées par le composant enfant
- Passées **du parent vers l'enfant**
- Permettent de **configurer** un composant

```jsx
// Composant parent
function App() {
  return <Carte titre="React" description="Une bibliothèque JavaScript" />;
}

// Composant enfant (reçoit les props)
function Carte({ titre, description }) {
  return (
    <div>
      <h2>{titre}</h2>
      <p>{description}</p>
    </div>
  );
}
```

### State (État)

- **Modifiable** : peut changer dans le temps
- **Local** au composant
- Déclenche un **re-rendu** quand il change

```jsx
function Compteur() {
  const [nombre, setNombre] = useState(0); // État local

  return (
    <div>
      <p>{nombre}</p>
      <button onClick={() => setNombre(nombre + 1)}>+1</button>
    </div>
  );
}
```

### Tableau récapitulatif

| Caractéristique | **Props** | **State** |
|----------------|-----------|-----------|
| Modifiable | ❌ Non | ✅ Oui |
| Provenance | Du parent | Local au composant |
| Déclenche re-rendu | ❌ Non* | ✅ Oui |
| Usage | Configuration | Données dynamiques |

*Les props peuvent changer si le parent les modifie, ce qui re-rendra l'enfant.

---

## Composition de composants

Un des grands avantages de React est la **composition** : assembler des petits composants pour créer des interfaces complexes.

### Exemple : Liste de tâches simple

```jsx
// Composant pour une tâche individuelle
function Tache({ texte, termine }) {
  return (
    <li style={{ textDecoration: termine ? 'line-through' : 'none' }}>
      {texte}
    </li>
  );
}

// Composant pour la liste de tâches
function ListeTaches() {
  const taches = [
    { id: 1, texte: 'Apprendre React', termine: true },
    { id: 2, texte: 'Créer un projet', termine: false },
    { id: 3, texte: 'Déployer l\'application', termine: false }
  ];

  return (
    <div>
      <h2>Mes tâches</h2>
      <ul>
        {taches.map(tache => (
          <Tache
            key={tache.id}
            texte={tache.texte}
            termine={tache.termine}
          />
        ))}
      </ul>
    </div>
  );
}
```

**⚠️ Important :** Chaque élément d'une liste doit avoir une prop `key` unique pour que React puisse les identifier efficacement.

---

## Gestion d'événements

Les événements en React fonctionnent de manière similaire au JavaScript vanilla, mais avec une syntaxe en camelCase.

### Événements courants

```jsx
function ExemplesEvenements() {
  const [message, setMessage] = useState('');

  const gererClic = () => {
    setMessage('Bouton cliqué !');
  };

  const gererSurvol = () => {
    console.log('Souris sur le bouton');
  };

  const gererSubmit = (event) => {
    event.preventDefault(); // Empêche le rechargement de la page
    setMessage('Formulaire soumis !');
  };

  return (
    <div>
      <button
        onClick={gererClic}
        onMouseEnter={gererSurvol}
      >
        Cliquez-moi
      </button>

      <form onSubmit={gererSubmit}>
        <input type="text" />
        <button type="submit">Envoyer</button>
      </form>

      <p>{message}</p>
    </div>
  );
}
```

### Passer des arguments aux gestionnaires

```jsx
function BoutonsMultiples() {
  const [message, setMessage] = useState('');

  const gererClic = (numero) => {
    setMessage(`Bouton ${numero} cliqué`);
  };

  return (
    <div>
      <button onClick={() => gererClic(1)}>Bouton 1</button>
      <button onClick={() => gererClic(2)}>Bouton 2</button>
      <button onClick={() => gererClic(3)}>Bouton 3</button>
      <p>{message}</p>
    </div>
  );
}
```

---

## Rendu conditionnel

Afficher différents éléments selon des conditions.

### Avec l'opérateur ternaire

```jsx
function MessageConnexion({ estConnecte }) {
  return (
    <div>
      {estConnecte ? (
        <h1>Bienvenue !</h1>
      ) : (
        <h1>Veuillez vous connecter</h1>
      )}
    </div>
  );
}
```

### Avec l'opérateur &&

```jsx
function Notification({ messages }) {
  return (
    <div>
      <h1>Bonjour !</h1>
      {messages.length > 0 && (
        <p>Vous avez {messages.length} nouveau(x) message(s)</p>
      )}
    </div>
  );
}
```

### Avec des variables

```jsx
function Meteo({ temperature }) {
  let message;

  if (temperature > 25) {
    message = "Il fait chaud !";
  } else if (temperature > 15) {
    message = "Il fait bon.";
  } else {
    message = "Il fait froid !";
  }

  return <p>{message}</p>;
}
```

---

## Structure d'un projet React typique

Lorsque vous créez un projet React (avec Create React App ou Vite), voici une structure courante :

```
mon-app/
├── node_modules/          # Dépendances (généré automatiquement)
├── public/                # Fichiers statiques
│   └── index.html        # Page HTML principale
├── src/                   # Code source
│   ├── components/       # Composants réutilisables
│   │   ├── Bouton.jsx
│   │   └── Carte.jsx
│   ├── App.jsx           # Composant principal
│   ├── App.css           # Styles du composant App
│   ├── index.js          # Point d'entrée
│   └── index.css         # Styles globaux
├── package.json           # Dépendances et scripts
└── README.md
```

### Exemple de fichier index.js

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### Exemple de fichier App.jsx

```jsx
import { useState } from 'react';
import './App.css';

function App() {
  const [compteur, setCompteur] = useState(0);

  return (
    <div className="App">
      <h1>Mon Application React</h1>
      <p>Compteur : {compteur}</p>
      <button onClick={() => setCompteur(compteur + 1)}>
        Incrémenter
      </button>
    </div>
  );
}

export default App;
```

---

## Démarrer avec React

### Option 1 : Create React App (traditionnel)

```bash
npx create-react-app mon-app
cd mon-app
npm start
```

### Option 2 : Vite (moderne, plus rapide) ⭐ Recommandé

```bash
npm create vite@latest mon-app -- --template react
cd mon-app
npm install
npm run dev
```

**Vite** est plus rapide et plus léger que Create React App. C'est l'outil recommandé aujourd'hui.

---

## Concepts clés à retenir

### 1. **Composant = Fonction qui retourne du JSX**
```jsx
function MonComposant() {
  return <div>Hello</div>;
}
```

### 2. **Props = Données passées du parent à l'enfant**
```jsx
<Enfant nom="Marie" age={25} />
```

### 3. **State = Données locales qui peuvent changer**
```jsx
const [valeur, setValeur] = useState(initialValue);
```

### 4. **JSX = HTML-like dans JavaScript**
```jsx
return <div className="conteneur">{variable}</div>;
```

### 5. **React re-rend quand le state change**
```jsx
setCompteur(compteur + 1); // Déclenche un re-rendu
```

---

## Bonnes pratiques pour débutants

### ✅ À FAIRE

1. **Nommer les composants avec une majuscule**
   ```jsx
   function MonComposant() { } // ✅
   function monComposant() { }  // ❌
   ```

2. **Un composant par fichier** (pour les gros projets)

3. **Utiliser des composants fonctionnels** (pas de classes en 2025)

4. **Déstructurer les props**
   ```jsx
   function Carte({ titre, description }) { } // ✅
   function Carte(props) { props.titre }      // ⚠️ Moins lisible
   ```

5. **Toujours donner une `key` aux éléments de liste**
   ```jsx
   {items.map(item => <div key={item.id}>{item.nom}</div>)}
   ```

### ❌ À ÉVITER

1. **Modifier directement le state**
   ```jsx
   // ❌ INCORRECT
   compteur = compteur + 1;

   // ✅ CORRECT
   setCompteur(compteur + 1);
   ```

2. **Oublier le `key` dans les listes**

3. **Utiliser `class` au lieu de `className`**

4. **Appeler directement une fonction dans onClick**
   ```jsx
   // ❌ INCORRECT (s'exécute immédiatement)
   <button onClick={maFonction()}>Clic</button>

   // ✅ CORRECT
   <button onClick={maFonction}>Clic</button>
   <button onClick={() => maFonction(param)}>Clic</button>
   ```

---

## Exemple complet : Application de compteur avancée

Voici un exemple qui combine tous les concepts vus :

```jsx
import { useState } from 'react';

function Compteur() {
  const [compteur, setCompteur] = useState(0);
  const [pas, setPas] = useState(1);

  const incrementer = () => {
    setCompteur(compteur + pas);
  };

  const decrementer = () => {
    setCompteur(compteur - pas);
  };

  const reinitialiser = () => {
    setCompteur(0);
  };

  const gererChangementPas = (event) => {
    setPas(Number(event.target.value));
  };

  return (
    <div className="compteur">
      <h1>Compteur React</h1>

      <div className="affichage">
        <p style={{
          fontSize: '48px',
          color: compteur >= 0 ? 'green' : 'red'
        }}>
          {compteur}
        </p>
      </div>

      <div className="controles">
        <button onClick={decrementer}>-{pas}</button>
        <button onClick={reinitialiser}>Réinitialiser</button>
        <button onClick={incrementer}>+{pas}</button>
      </div>

      <div className="reglages">
        <label>
          Pas d'incrémentation :
          <input
            type="number"
            value={pas}
            onChange={gererChangementPas}
            min="1"
          />
        </label>
      </div>

      {compteur > 100 && (
        <p className="alerte">🎉 Vous avez dépassé 100 !</p>
      )}
    </div>
  );
}

export default Compteur;
```

---

## Prochaines étapes

Maintenant que vous comprenez les bases de React, vous pouvez explorer :

1. **useEffect** - Pour gérer les effets de bord (requêtes API, timers, etc.)
2. **Hooks personnalisés** - Créer vos propres hooks réutilisables
3. **React Router** - Navigation entre pages
4. **Gestion d'état globale** - Context API, Redux, Zustand
5. **Requêtes API** - Avec fetch ou des bibliothèques comme Axios
6. **Formulaires complexes** - Validation, gestion d'erreurs
7. **Optimisation** - React.memo, useMemo, useCallback

---

## Ressources pour aller plus loin

### Documentation officielle
- **React.dev** (nouvelle doc officielle) : https://react.dev/
- Tutoriel interactif officiel : https://react.dev/learn

### Tutoriels recommandés
- **FreeCodeCamp** - Cours React gratuits
- **Scrimba** - Cours interactifs React
- **React en français** - Grafikart, Underscore

### Outils utiles
- **React DevTools** - Extension navigateur pour débugger React
- **Vite** - Outil de build moderne
- **CodeSandbox** - Éditeur en ligne pour tester React

---

## Conclusion

React transforme la façon de créer des interfaces web en rendant le code **modulaire**, **réutilisable** et **prévisible**. Les concepts de **composants** et d'**état** sont au cœur de cette approche.

**Ce qu'il faut retenir :**
- React = Composants + Props + State
- JSX = Syntaxe HTML-like dans JavaScript
- useState = Gestion de données dynamiques
- Toujours utiliser `set...` pour modifier le state
- La composition de composants permet de créer des interfaces complexes

Avec ces fondamentaux, vous êtes prêt à construire vos premières applications React ! 🚀

---


⏭️ [Vue.js : framework progressif](/08-ecosysteme-javascript-moderne/03-frameworks-librairies/02-vuejs.md)
