🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 8.3.3 Angular : framework complet 🆕

## Introduction à Angular

**Angular** est un framework JavaScript complet créé et maintenu par Google depuis 2010. C'est une plateforme complète pour construire des applications web, contrairement à React (bibliothèque) ou Vue (framework progressif).

### Qu'est-ce qu'Angular ?

Angular est un **framework opinionated** (avec des opinions fortes), ce qui signifie qu'il impose une structure et des conventions précises. Tout est inclus dans le framework : routing, formulaires, HTTP, animations, etc.

**Analogie simple :** Si React est comme acheter des ingrédients séparément pour cuisiner, Angular est comme recevoir un kit repas complet avec tous les ingrédients, les ustensiles, et la recette détaillée. Tout est fourni et organisé.

### Angular vs AngularJS

⚠️ **Important : Ne pas confondre !**

- **AngularJS** (2010) : Version 1.x, ancien framework (obsolète)
- **Angular** (2016+) : Version 2+, réécriture complète (actuel)

Quand on parle d'Angular aujourd'hui, on parle d'Angular 2+ (actuellement Angular 17+).

---

## Pourquoi utiliser Angular ?

### Avantages principaux

1. **Framework complet** : Tout est inclus, pas besoin de choisir des bibliothèques
2. **TypeScript obligatoire** : Typage fort, meilleure maintenabilité
3. **Architecture structurée** : Organisation claire pour les grands projets
4. **CLI puissant** : Génération automatique de code
5. **Soutien de Google** : Développement actif, entreprise stable
6. **Injection de dépendances** : Gestion propre des services
7. **Documentation complète** : Ressources exhaustives
8. **Excellent pour l'entreprise** : Conventions strictes, équipes larges

### Inconvénients

1. **Courbe d'apprentissage élevée** : Plus difficile que React ou Vue
2. **Verbeux** : Beaucoup de code boilerplate
3. **Bundle plus lourd** : Application de base plus volumineuse
4. **TypeScript obligatoire** : Apprentissage supplémentaire
5. **Changements de version** : Migrations parfois complexes

### Comparaison rapide

| Caractéristique | **Angular** | **React** | **Vue** |
|----------------|-------------|-----------|---------|
| **Type** | Framework complet | Bibliothèque | Framework progressif |
| **Langage** | TypeScript | JavaScript/JSX | JavaScript |
| **Courbe d'apprentissage** | 🔴 Élevée | 🟡 Moyenne | 🟢 Facile |
| **Taille du bundle** | ~140 KB | ~45 KB | ~40 KB |
| **Outils inclus** | ✅ Tout | ❌ Écosystème tiers | ✅ Officiels |
| **Entreprise** | Facebook/Meta | Google | Communauté |

### Quand utiliser Angular ?

- **✅ Applications d'entreprise complexes**
- **✅ Grandes équipes nécessitant une structure stricte**
- **✅ Projets long-terme nécessitant maintenabilité**
- **✅ Applications nécessitant tout l'écosystème (routing, HTTP, forms)**
- **✅ Équipes TypeScript**

### Quand NE PAS utiliser Angular ?

- **❌ Petits projets ou prototypes rapides**
- **❌ Sites vitrines simples**
- **❌ Équipes débutantes en développement web**
- **❌ Projets nécessitant un bundle très léger**

---

## TypeScript : Le langage d'Angular

Angular utilise **TypeScript** par défaut. TypeScript est JavaScript avec des types statiques.

### JavaScript vs TypeScript

```javascript
// JAVASCRIPT (non typé)
function addition(a, b) {
  return a + b;
}

addition(5, 10);      // 15
addition('5', '10');  // '510' (concaténation de strings !)
```

```typescript
// TYPESCRIPT (typé)
function addition(a: number, b: number): number {
  return a + b;
}

addition(5, 10);      // 15 ✅
addition('5', '10');  // ❌ ERREUR : les strings ne sont pas acceptés
```

### Types de base en TypeScript

```typescript
// Types primitifs
let nom: string = 'Marie';
let age: number = 25;
let estConnecte: boolean = true;

// Tableaux
let nombres: number[] = [1, 2, 3, 4, 5];
let fruits: string[] = ['Pomme', 'Banane', 'Orange'];

// Objets
let utilisateur: { nom: string; age: number } = {
  nom: 'Jean',
  age: 30
};

// Interface (structure réutilisable)
interface Utilisateur {
  nom: string;
  age: number;
  email: string;
}

let user: Utilisateur = {
  nom: 'Marie',
  age: 25,
  email: 'marie@exemple.com'
};

// Type personnalisé
type ID = string | number;  // Union type
let userId: ID = 123;       // ✅
userId = 'abc-123';         // ✅
```

**Pourquoi TypeScript ?**
- Détecte les erreurs avant l'exécution
- Meilleure autocomplétion dans l'éditeur
- Documentation intégrée
- Refactoring plus sûr

---

## Installation et Premier Projet

### Prérequis

1. **Node.js** (version 18.19 ou supérieure)
2. **npm** (inclus avec Node.js)

### Installation de Angular CLI

```bash
npm install -g @angular/cli
```

Vérifier l'installation :
```bash
ng version
```

### Créer un nouveau projet

```bash
ng new mon-app-angular

# Questions posées :
# - Routing ? Oui (recommandé)
# - Stylesheet ? CSS (ou SCSS si vous préférez)
```

### Démarrer le serveur de développement

```bash
cd mon-app-angular
ng serve

# Ouvrir http://localhost:4200
```

---

## Structure d'un Projet Angular

```
mon-app-angular/
├── node_modules/          # Dépendances
├── src/                   # Code source
│   ├── app/              # Application principale
│   │   ├── app.component.ts      # Composant racine (logique)
│   │   ├── app.component.html    # Template HTML
│   │   ├── app.component.css     # Styles
│   │   ├── app.component.spec.ts # Tests
│   │   └── app.module.ts         # Module principal
│   ├── assets/           # Fichiers statiques (images, etc.)
│   ├── environments/     # Configurations d'environnement
│   ├── index.html        # Page HTML principale
│   ├── main.ts           # Point d'entrée
│   └── styles.css        # Styles globaux
├── angular.json          # Configuration Angular
├── package.json          # Dépendances npm
└── tsconfig.json         # Configuration TypeScript
```

---

## Architecture Angular : Les Bases

Angular est organisé en **modules**, qui contiennent des **composants** et des **services**.

```
Module Angular
├── Composants (UI)
├── Services (Logique métier)
├── Directives (Comportement DOM)
└── Pipes (Transformation de données)
```

### 1. Les Modules (@NgModule)

Un **module** est un conteneur pour organiser l'application.

```typescript
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent  // Composants, directives, pipes
  ],
  imports: [
    BrowserModule // Modules Angular ou tiers
  ],
  providers: [],  // Services
  bootstrap: [AppComponent]  // Composant racine
})
export class AppModule { }
```

**Chaque application Angular a au moins un module : `AppModule`.**

### 2. Les Composants (@Component)

Un **composant** contrôle une partie de l'écran (vue).

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',           // Balise HTML : <app-root>
  templateUrl: './app.component.html',  // Template HTML
  styleUrls: ['./app.component.css']    // Styles CSS
})
export class AppComponent {
  // Propriétés (données)
  titre = 'Mon Application Angular';
  compteur = 0;

  // Méthodes
  incrementer() {
    this.compteur++;
  }
}
```

```html
<!-- app.component.html -->
<h1>{{ titre }}</h1>
<p>Compteur : {{ compteur }}</p>
<button (click)="incrementer()">+1</button>
```

**Structure d'un composant :**
1. **Décorateur @Component** : Métadonnées du composant
2. **Classe TypeScript** : Logique et données
3. **Template HTML** : Structure de la vue
4. **Styles CSS** : Apparence

---

## Les Décorateurs Angular

Les **décorateurs** (préfixés par `@`) ajoutent des métadonnées aux classes.

### Décorateurs principaux

```typescript
// @Component : Définit un composant
@Component({
  selector: 'app-exemple',
  templateUrl: './exemple.component.html',
  styleUrls: ['./exemple.component.css']
})

// @Injectable : Définit un service injectable
@Injectable({
  providedIn: 'root'
})

// @NgModule : Définit un module
@NgModule({
  declarations: [],
  imports: [],
  providers: []
})

// @Input : Propriété reçue du parent
@Input() nom: string;

// @Output : Événement émis vers le parent
@Output() clic = new EventEmitter<void>();
```

---

## Data Binding : Liaison de données

Angular offre plusieurs façons de lier les données au template.

### 1. Interpolation `{{ }}`

Affiche une valeur dans le template.

```typescript
export class AppComponent {
  nom = 'Marie';
  age = 25;

  getNomComplet() {
    return `${this.nom} Dupont`;
  }
}
```

```html
<h1>Bonjour {{ nom }} !</h1>
<p>Âge : {{ age }} ans</p>
<p>{{ getNomComplet() }}</p>
<p>{{ 2 + 2 }}</p>
```

### 2. Property Binding `[propriété]`

Lie une propriété TypeScript à un attribut HTML.

```typescript
export class AppComponent {
  urlImage = 'https://exemple.com/photo.jpg';
  estDesactive = false;
  couleur = 'blue';
}
```

```html
<!-- Attributs HTML -->
<img [src]="urlImage" [alt]="'Photo de ' + nom">
<button [disabled]="estDesactive">Cliquer</button>

<!-- Propriétés CSS -->
<p [style.color]="couleur">Texte coloré</p>

<!-- Classes CSS -->
<div [class.actif]="estDesactive">Contenu</div>
```

### 3. Event Binding `(événement)`

Gère les événements utilisateur.

```typescript
export class AppComponent {
  compteur = 0;
  message = '';

  incrementer() {
    this.compteur++;
  }

  gererClic(event: Event) {
    console.log('Événement :', event);
    this.message = 'Bouton cliqué !';
  }

  gererInput(event: Event) {
    const input = event.target as HTMLInputElement;
    this.message = input.value;
  }
}
```

```html
<!-- Événements de base -->
<button (click)="incrementer()">+1</button>
<button (click)="gererClic($event)">Clic avec event</button>

<!-- Événements de formulaire -->
<input (input)="gererInput($event)" type="text">
<form (submit)="soumettre()">
  <button type="submit">Envoyer</button>
</form>
```

### 4. Two-Way Binding `[(ngModel)]`

Liaison bidirectionnelle (données ↔ interface).

**⚠️ Nécessite FormsModule**

```typescript
// app.module.ts
import { FormsModule } from '@angular/forms';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule  // ← Ajouter ceci
  ]
})
```

```typescript
// composant
export class AppComponent {
  nom = '';
  age = 0;
}
```

```html
<input [(ngModel)]="nom" type="text" placeholder="Nom">
<p>Bonjour {{ nom }} !</p>

<input [(ngModel)]="age" type="number">
<p>Âge : {{ age }} ans</p>
```

**C'est comme `v-model` en Vue ou state + onChange en React !**

---

## Directives Structurelles

Les **directives structurelles** modifient la structure du DOM.

### *ngIf : Affichage conditionnel

```typescript
export class AppComponent {
  estConnecte = false;
  age = 16;

  basculerConnexion() {
    this.estConnecte = !this.estConnecte;
  }
}
```

```html
<!-- *ngIf simple -->
<div *ngIf="estConnecte">
  <h2>Bienvenue !</h2>
  <p>Vous êtes connecté.</p>
</div>

<!-- *ngIf avec else -->
<div *ngIf="estConnecte; else nonConnecte">
  <h2>Bienvenue !</h2>
</div>

<ng-template #nonConnecte>
  <h2>Veuillez vous connecter</h2>
</ng-template>

<!-- *ngIf avec then et else -->
<div *ngIf="age >= 18; then majeur else mineur"></div>

<ng-template #majeur>
  <p>Vous êtes majeur</p>
</ng-template>

<ng-template #mineur>
  <p>Vous êtes mineur</p>
</ng-template>
```

### *ngFor : Boucle sur les listes

```typescript
export class AppComponent {
  fruits = ['Pomme', 'Banane', 'Orange', 'Poire'];

  utilisateurs = [
    { id: 1, nom: 'Marie', age: 25 },
    { id: 2, nom: 'Jean', age: 30 },
    { id: 3, nom: 'Paul', age: 28 }
  ];
}
```

```html
<!-- Liste simple -->
<ul>
  <li *ngFor="let fruit of fruits">
    {{ fruit }}
  </li>
</ul>

<!-- Avec index -->
<ul>
  <li *ngFor="let fruit of fruits; let i = index">
    {{ i + 1 }}. {{ fruit }}
  </li>
</ul>

<!-- Liste d'objets -->
<div *ngFor="let user of utilisateurs">
  <h3>{{ user.nom }}</h3>
  <p>Âge : {{ user.age }} ans</p>
</div>

<!-- Variables disponibles -->
<div *ngFor="let item of items; let i = index; let first = first; let last = last; let even = even; let odd = odd">
  <p>Index: {{ i }}</p>
  <p *ngIf="first">Premier élément</p>
  <p *ngIf="last">Dernier élément</p>
  <p *ngIf="even">Ligne paire</p>
</div>
```

**⚠️ Important :** Toujours utiliser `trackBy` pour les grandes listes (optimisation).

```typescript
trackByUserId(index: number, user: any): number {
  return user.id;
}
```

```html
<div *ngFor="let user of utilisateurs; trackBy: trackByUserId">
  {{ user.nom }}
</div>
```

### *ngSwitch : Sélection multiple

```typescript
export class AppComponent {
  couleur = 'rouge';
}
```

```html
<div [ngSwitch]="couleur">
  <p *ngSwitchCase="'rouge'">Vous avez choisi rouge</p>
  <p *ngSwitchCase="'bleu'">Vous avez choisi bleu</p>
  <p *ngSwitchCase="'vert'">Vous avez choisi vert</p>
  <p *ngSwitchDefault>Couleur inconnue</p>
</div>
```

---

## Directives d'Attributs

Les **directives d'attributs** modifient l'apparence ou le comportement d'un élément.

### ngClass : Classes CSS conditionnelles

```typescript
export class AppComponent {
  estActif = true;
  estImportant = false;
  classes = 'grande bleu';
}
```

```html
<!-- Objet -->
<div [ngClass]="{ 'actif': estActif, 'important': estImportant }">
  Contenu
</div>

<!-- Tableau -->
<div [ngClass]="['grande', 'bleu', estActif ? 'actif' : '']">
  Contenu
</div>

<!-- String -->
<div [ngClass]="classes">
  Contenu
</div>
```

### ngStyle : Styles inline conditionnels

```typescript
export class AppComponent {
  couleur = 'red';
  taille = 20;
}
```

```html
<p [ngStyle]="{
  'color': couleur,
  'font-size': taille + 'px',
  'font-weight': estImportant ? 'bold' : 'normal'
}">
  Texte stylé
</p>
```

---

## Communication entre Composants

### 1. Parent → Enfant avec @Input

**Composant parent :**
```typescript
// parent.component.ts
export class ParentComponent {
  nomUtilisateur = 'Marie';
  ageUtilisateur = 25;
}
```

```html
<!-- parent.component.html -->
<app-enfant [nom]="nomUtilisateur" [age]="ageUtilisateur"></app-enfant>
```

**Composant enfant :**
```typescript
// enfant.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-enfant',
  template: `
    <div>
      <h3>{{ nom }}</h3>
      <p>Âge : {{ age }} ans</p>
    </div>
  `
})
export class EnfantComponent {
  @Input() nom: string = '';
  @Input() age: number = 0;
}
```

### 2. Enfant → Parent avec @Output

**Composant enfant :**
```typescript
// enfant.component.ts
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-enfant',
  template: `
    <button (click)="envoyer()">Envoyer au parent</button>
  `
})
export class EnfantComponent {
  @Output() messageEnvoye = new EventEmitter<string>();

  envoyer() {
    this.messageEnvoye.emit('Message depuis l\'enfant !');
  }
}
```

**Composant parent :**
```typescript
// parent.component.ts
export class ParentComponent {
  messageRecu = '';

  recevoirMessage(message: string) {
    this.messageRecu = message;
  }
}
```

```html
<!-- parent.component.html -->
<app-enfant (messageEnvoye)="recevoirMessage($event)"></app-enfant>
<p>Message reçu : {{ messageRecu }}</p>
```

---

## Les Services et Injection de Dépendances

Les **services** contiennent la logique métier réutilisable.

### Créer un service

```bash
ng generate service services/data
# ou
ng g s services/data
```

```typescript
// data.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'  // Service disponible partout
})
export class DataService {
  private compteur = 0;

  incrementer() {
    this.compteur++;
  }

  getCompteur(): number {
    return this.compteur;
  }

  getUtilisateurs() {
    return [
      { id: 1, nom: 'Marie', email: 'marie@exemple.com' },
      { id: 2, nom: 'Jean', email: 'jean@exemple.com' }
    ];
  }
}
```

### Utiliser un service

```typescript
// app.component.ts
import { Component, OnInit } from '@angular/core';
import { DataService } from './services/data.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  compteur = 0;
  utilisateurs: any[] = [];

  // Injection de dépendance
  constructor(private dataService: DataService) {}

  ngOnInit() {
    this.utilisateurs = this.dataService.getUtilisateurs();
    this.compteur = this.dataService.getCompteur();
  }

  incrementer() {
    this.dataService.incrementer();
    this.compteur = this.dataService.getCompteur();
  }
}
```

**Avantages des services :**
- Centralise la logique métier
- Réutilisable dans plusieurs composants
- Facilite les tests
- Partage de données entre composants

---

## Requêtes HTTP

Angular inclut `HttpClient` pour les requêtes API.

### Configuration

```typescript
// app.module.ts
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    BrowserModule,
    HttpClientModule  // ← Ajouter ceci
  ]
})
```

### Service HTTP

```typescript
// user.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

interface User {
  id: number;
  name: string;
  email: string;
}

@Injectable({
  providedIn: 'root'
})
export class UserService {
  private apiUrl = 'https://jsonplaceholder.typicode.com/users';

  constructor(private http: HttpClient) {}

  // GET : Récupérer tous les utilisateurs
  getUsers(): Observable<User[]> {
    return this.http.get<User[]>(this.apiUrl);
  }

  // GET : Récupérer un utilisateur
  getUser(id: number): Observable<User> {
    return this.http.get<User>(`${this.apiUrl}/${id}`);
  }

  // POST : Créer un utilisateur
  createUser(user: User): Observable<User> {
    return this.http.post<User>(this.apiUrl, user);
  }

  // PUT : Modifier un utilisateur
  updateUser(id: number, user: User): Observable<User> {
    return this.http.put<User>(`${this.apiUrl}/${id}`, user);
  }

  // DELETE : Supprimer un utilisateur
  deleteUser(id: number): Observable<void> {
    return this.http.delete<void>(`${this.apiUrl}/${id}`);
  }
}
```

### Utilisation dans un composant

```typescript
// app.component.ts
import { Component, OnInit } from '@angular/core';
import { UserService } from './services/user.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  users: any[] = [];
  chargement = false;
  erreur = '';

  constructor(private userService: UserService) {}

  ngOnInit() {
    this.chargerUtilisateurs();
  }

  chargerUtilisateurs() {
    this.chargement = true;

    this.userService.getUsers().subscribe({
      next: (data) => {
        this.users = data;
        this.chargement = false;
      },
      error: (err) => {
        this.erreur = 'Erreur lors du chargement';
        this.chargement = false;
        console.error(err);
      }
    });
  }
}
```

```html
<!-- app.component.html -->
<div *ngIf="chargement">Chargement...</div>
<div *ngIf="erreur">{{ erreur }}</div>

<ul *ngIf="!chargement && !erreur">
  <li *ngFor="let user of users">
    {{ user.name }} - {{ user.email }}
  </li>
</ul>
```

---

## RxJS et Observables

Angular utilise **RxJS** (Reactive Extensions for JavaScript) pour la programmation réactive.

### Qu'est-ce qu'un Observable ?

Un **Observable** est un flux de données dans le temps. C'est comme une promesse qui peut retourner plusieurs valeurs.

```typescript
import { Observable } from 'rxjs';

// Promesse : une seule valeur
const promesse = fetch('/api/users');
promesse.then(data => console.log(data));

// Observable : plusieurs valeurs possibles
const observable = new Observable(observer => {
  observer.next(1);
  observer.next(2);
  observer.next(3);
  setTimeout(() => observer.next(4), 1000);
});

observable.subscribe(valeur => console.log(valeur));
// Affiche : 1, 2, 3, puis 4 après 1 seconde
```

### Opérateurs RxJS courants

```typescript
import { of } from 'rxjs';
import { map, filter, debounceTime } from 'rxjs/operators';

// map : Transformer les valeurs
of(1, 2, 3, 4, 5)
  .pipe(
    map(x => x * 2)
  )
  .subscribe(x => console.log(x));
// Affiche : 2, 4, 6, 8, 10

// filter : Filtrer les valeurs
of(1, 2, 3, 4, 5)
  .pipe(
    filter(x => x % 2 === 0)
  )
  .subscribe(x => console.log(x));
// Affiche : 2, 4

// debounceTime : Attendre avant d'émettre
// Utile pour les champs de recherche
searchInput.valueChanges
  .pipe(
    debounceTime(300)  // Attendre 300ms après la dernière saisie
  )
  .subscribe(valeur => this.rechercher(valeur));
```

---

## Routing : Navigation entre pages

Angular Router permet de créer des applications à pages multiples (SPA).

### Configuration basique

```typescript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { ContactComponent } from './contact/contact.component';

const routes: Routes = [
  { path: '', component: HomeComponent },           // Page d'accueil
  { path: 'about', component: AboutComponent },     // /about
  { path: 'contact', component: ContactComponent }, // /contact
  { path: '**', redirectTo: '' }                    // Route par défaut (404)
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### Template principal

```html
<!-- app.component.html -->
<nav>
  <a routerLink="/" routerLinkActive="actif" [routerLinkActiveOptions]="{exact: true}">
    Accueil
  </a>
  <a routerLink="/about" routerLinkActive="actif">À propos</a>
  <a routerLink="/contact" routerLinkActive="actif">Contact</a>
</nav>

<!-- Le composant de la route actuelle s'affiche ici -->
<router-outlet></router-outlet>
```

### Navigation programmatique

```typescript
import { Router } from '@angular/router';

export class MonComponent {
  constructor(private router: Router) {}

  allerVersAbout() {
    this.router.navigate(['/about']);
  }

  retournerEnArriere() {
    window.history.back();
  }
}
```

### Routes avec paramètres

```typescript
// Définir la route
const routes: Routes = [
  { path: 'user/:id', component: UserDetailComponent }
];
```

```typescript
// Récupérer le paramètre
import { ActivatedRoute } from '@angular/router';

export class UserDetailComponent implements OnInit {
  userId: string = '';

  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    this.userId = this.route.snapshot.paramMap.get('id') || '';

    // Ou observer les changements
    this.route.paramMap.subscribe(params => {
      this.userId = params.get('id') || '';
    });
  }
}
```

---

## Pipes : Transformation de données

Les **pipes** transforment les données dans le template.

### Pipes intégrés

```html
<!-- uppercase : Majuscules -->
<p>{{ 'hello' | uppercase }}</p>
<!-- Affiche : HELLO -->

<!-- lowercase : Minuscules -->
<p>{{ 'HELLO' | lowercase }}</p>
<!-- Affiche : hello -->

<!-- date : Formater une date -->
<p>{{ dateActuelle | date:'dd/MM/yyyy' }}</p>
<p>{{ dateActuelle | date:'long' }}</p>

<!-- currency : Formater une devise -->
<p>{{ prix | currency:'EUR' }}</p>
<!-- Affiche : €25.00 -->

<!-- number : Formater un nombre -->
<p>{{ 3.14159 | number:'1.2-2' }}</p>
<!-- Affiche : 3.14 -->

<!-- json : Debug (affiche l'objet) -->
<pre>{{ utilisateur | json }}</pre>

<!-- slice : Extraire un sous-ensemble -->
<p>{{ 'Hello World' | slice:0:5 }}</p>
<!-- Affiche : Hello -->

<!-- Chaîner plusieurs pipes -->
<p>{{ nom | lowercase | slice:0:10 }}</p>
```

### Créer un pipe personnalisé

```bash
ng generate pipe pipes/reverse
```

```typescript
// reverse.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'reverse'
})
export class ReversePipe implements PipeTransform {
  transform(value: string): string {
    return value.split('').reverse().join('');
  }
}
```

```html
<p>{{ 'Angular' | reverse }}</p>
<!-- Affiche : ralugnA -->
```

---

## Formulaires en Angular

Angular propose deux approches pour les formulaires.

### 1. Template-Driven Forms (Simple)

**Configuration :**
```typescript
// app.module.ts
import { FormsModule } from '@angular/forms';

@NgModule({
  imports: [FormsModule]
})
```

**Utilisation :**
```typescript
export class AppComponent {
  utilisateur = {
    nom: '',
    email: '',
    age: 0
  };

  soumettre() {
    console.log('Formulaire soumis :', this.utilisateur);
  }
}
```

```html
<form #monFormulaire="ngForm" (ngSubmit)="soumettre()">
  <div>
    <label>Nom :</label>
    <input
      type="text"
      [(ngModel)]="utilisateur.nom"
      name="nom"
      required
      #nom="ngModel"
    >
    <div *ngIf="nom.invalid && nom.touched" class="erreur">
      Le nom est requis
    </div>
  </div>

  <div>
    <label>Email :</label>
    <input
      type="email"
      [(ngModel)]="utilisateur.email"
      name="email"
      required
      email
      #email="ngModel"
    >
    <div *ngIf="email.invalid && email.touched" class="erreur">
      Email invalide
    </div>
  </div>

  <button type="submit" [disabled]="monFormulaire.invalid">
    Envoyer
  </button>
</form>

<p>Formulaire valide : {{ monFormulaire.valid }}</p>
```

### 2. Reactive Forms (Avancé)

Plus puissant et recommandé pour les formulaires complexes.

**Configuration :**
```typescript
// app.module.ts
import { ReactiveFormsModule } from '@angular/forms';

@NgModule({
  imports: [ReactiveFormsModule]
})
```

**Utilisation :**
```typescript
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

export class AppComponent {
  formulaire: FormGroup;

  constructor(private fb: FormBuilder) {
    this.formulaire = this.fb.group({
      nom: ['', [Validators.required, Validators.minLength(3)]],
      email: ['', [Validators.required, Validators.email]],
      age: [0, [Validators.required, Validators.min(18)]]
    });
  }

  soumettre() {
    if (this.formulaire.valid) {
      console.log('Données :', this.formulaire.value);
    }
  }

  get nom() {
    return this.formulaire.get('nom');
  }

  get email() {
    return this.formulaire.get('email');
  }
}
```

```html
<form [formGroup]="formulaire" (ngSubmit)="soumettre()">
  <div>
    <label>Nom :</label>
    <input type="text" formControlName="nom">
    <div *ngIf="nom?.invalid && nom?.touched" class="erreur">
      <div *ngIf="nom?.errors?.['required']">Le nom est requis</div>
      <div *ngIf="nom?.errors?.['minlength']">Minimum 3 caractères</div>
    </div>
  </div>

  <div>
    <label>Email :</label>
    <input type="email" formControlName="email">
    <div *ngIf="email?.invalid && email?.touched" class="erreur">
      <div *ngIf="email?.errors?.['required']">L'email est requis</div>
      <div *ngIf="email?.errors?.['email']">Email invalide</div>
    </div>
  </div>

  <button type="submit" [disabled]="formulaire.invalid">
    Envoyer
  </button>
</form>
```

---

## Lifecycle Hooks : Cycles de vie

Angular appelle des méthodes à des moments précis du cycle de vie d'un composant.

```typescript
import { Component, OnInit, OnDestroy, OnChanges, SimpleChanges } from '@angular/core';

export class MonComponent implements OnInit, OnDestroy, OnChanges {

  // 1. Constructeur (pas un hook Angular)
  constructor() {
    console.log('1. Constructor');
  }

  // 2. Quand les @Input changent
  ngOnChanges(changes: SimpleChanges) {
    console.log('2. ngOnChanges', changes);
  }

  // 3. Initialisation du composant
  ngOnInit() {
    console.log('3. ngOnInit - Bon endroit pour les requêtes API');
    // Requêtes HTTP, initialisations
  }

  // 4. Après vérification du contenu projeté
  ngAfterContentInit() {
    console.log('4. ngAfterContentInit');
  }

  // 5. Après chaque vérification du contenu projeté
  ngAfterContentChecked() {
    console.log('5. ngAfterContentChecked');
  }

  // 6. Après initialisation de la vue
  ngAfterViewInit() {
    console.log('6. ngAfterViewInit - Bon endroit pour manipuler le DOM');
    // Manipulation du DOM, initialisation de bibliothèques tierces
  }

  // 7. Après chaque vérification de la vue
  ngAfterViewChecked() {
    console.log('7. ngAfterViewChecked');
  }

  // 8. Avant destruction du composant
  ngOnDestroy() {
    console.log('8. ngOnDestroy - Nettoyage');
    // Désabonnement des observables, nettoyage des timers
  }
}
```

**Les plus utilisés :**
- `ngOnInit()` : Initialisation, requêtes API
- `ngOnDestroy()` : Nettoyage, désabonnements
- `ngOnChanges()` : Réagir aux changements des @Input

---

## CLI Angular : Commandes essentielles

### Génération de code

```bash
# Créer un composant
ng generate component components/mon-composant
ng g c components/mon-composant

# Créer un service
ng generate service services/mon-service
ng g s services/mon-service

# Créer un module
ng generate module modules/mon-module
ng g m modules/mon-module

# Créer une directive
ng generate directive directives/ma-directive
ng g d directives/ma-directive

# Créer un pipe
ng generate pipe pipes/mon-pipe
ng g p pipes/mon-pipe

# Créer une guard (protection de routes)
ng generate guard guards/auth
ng g g guards/auth
```

### Build et déploiement

```bash
# Développement
ng serve              # Lance le serveur de développement
ng serve --open       # Ouvre dans le navigateur
ng serve --port 4300  # Change le port

# Production
ng build              # Build pour production
ng build --prod       # Alias pour la production

# Tests
ng test               # Lance les tests unitaires
ng e2e                # Lance les tests end-to-end
```

---

## Exemple complet : Application Liste de Tâches

### Générer les composants

```bash
ng g c components/task-list
ng g c components/task-item
ng g s services/task
```

### Service

```typescript
// task.service.ts
import { Injectable } from '@angular/core';

export interface Task {
  id: number;
  texte: string;
  termine: boolean;
}

@Injectable({
  providedIn: 'root'
})
export class TaskService {
  private tasks: Task[] = [
    { id: 1, texte: 'Apprendre Angular', termine: false },
    { id: 2, texte: 'Créer un projet', termine: false }
  ];
  private nextId = 3;

  getTasks(): Task[] {
    return this.tasks;
  }

  addTask(texte: string): void {
    this.tasks.push({
      id: this.nextId++,
      texte,
      termine: false
    });
  }

  toggleTask(id: number): void {
    const task = this.tasks.find(t => t.id === id);
    if (task) {
      task.termine = !task.termine;
    }
  }

  deleteTask(id: number): void {
    this.tasks = this.tasks.filter(t => t.id !== id);
  }
}
```

### Composant Liste

```typescript
// task-list.component.ts
import { Component, OnInit } from '@angular/core';
import { TaskService, Task } from '../../services/task.service';

@Component({
  selector: 'app-task-list',
  templateUrl: './task-list.component.html',
  styleUrls: ['./task-list.component.css']
})
export class TaskListComponent implements OnInit {
  tasks: Task[] = [];
  nouvelleTache = '';
  filtre = 'tous'; // 'tous' | 'actifs' | 'termines'

  constructor(private taskService: TaskService) {}

  ngOnInit() {
    this.tasks = this.taskService.getTasks();
  }

  get tasksFiltrees(): Task[] {
    if (this.filtre === 'actifs') {
      return this.tasks.filter(t => !t.termine);
    } else if (this.filtre === 'termines') {
      return this.tasks.filter(t => t.termine);
    }
    return this.tasks;
  }

  get tasksActives(): number {
    return this.tasks.filter(t => !t.termine).length;
  }

  ajouterTache() {
    if (this.nouvelleTache.trim()) {
      this.taskService.addTask(this.nouvelleTache);
      this.nouvelleTache = '';
    }
  }

  basculerTache(id: number) {
    this.taskService.toggleTask(id);
  }

  supprimerTache(id: number) {
    this.taskService.deleteTask(id);
  }
}
```

```html
<!-- task-list.component.html -->
<div class="task-container">
  <h1>Ma Liste de Tâches Angular</h1>

  <!-- Formulaire d'ajout -->
  <div class="add-task">
    <input
      type="text"
      [(ngModel)]="nouvelleTache"
      (keyup.enter)="ajouterTache()"
      placeholder="Nouvelle tâche..."
    >
    <button (click)="ajouterTache()">Ajouter</button>
  </div>

  <!-- Filtres -->
  <div class="filters">
    <button
      [class.actif]="filtre === 'tous'"
      (click)="filtre = 'tous'"
    >
      Tous ({{ tasks.length }})
    </button>
    <button
      [class.actif]="filtre === 'actifs'"
      (click)="filtre = 'actifs'"
    >
      Actifs ({{ tasksActives }})
    </button>
    <button
      [class.actif]="filtre === 'termines'"
      (click)="filtre = 'termines'"
    >
      Terminés ({{ tasks.length - tasksActives }})
    </button>
  </div>

  <!-- Liste des tâches -->
  <div *ngIf="tasksFiltrees.length === 0" class="empty">
    Aucune tâche à afficher
  </div>

  <div class="task-list">
    <div
      *ngFor="let task of tasksFiltrees"
      class="task-item"
      [class.termine]="task.termine"
    >
      <input
        type="checkbox"
        [checked]="task.termine"
        (change)="basculerTache(task.id)"
      >
      <span>{{ task.texte }}</span>
      <button (click)="supprimerTache(task.id)" class="delete">❌</button>
    </div>
  </div>
</div>
```

```css
/* task-list.component.css */
.task-container {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
}

.add-task {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.add-task input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
}

.filters {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.filters button {
  padding: 8px 15px;
  cursor: pointer;
}

.filters button.actif {
  background-color: #007bff;
  color: white;
}

.task-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  margin-bottom: 5px;
}

.task-item.termine span {
  text-decoration: line-through;
  opacity: 0.6;
}

.task-item span {
  flex: 1;
}

.delete {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 16px;
}
```

---

## Bonnes pratiques Angular

### ✅ À FAIRE

1. **Utiliser TypeScript strictement**
   ```typescript
   // tsconfig.json
   "strict": true
   ```

2. **Un composant par fichier**

3. **Services pour la logique métier**
   ```typescript
   // ✅ Logique dans un service
   export class UserService {
     getUsers() { /* ... */ }
   }

   // ❌ Logique dans le composant
   export class UserComponent {
     getUsers() { /* ... */ }
   }
   ```

4. **Désabonner des Observables**
   ```typescript
   ngOnDestroy() {
     this.subscription.unsubscribe();
   }
   ```

5. **Utiliser async pipe dans les templates**
   ```html
   <div *ngFor="let user of users$ | async">
     {{ user.name }}
   </div>
   ```

6. **OnPush Change Detection pour les performances**
   ```typescript
   @Component({
     changeDetection: ChangeDetectionStrategy.OnPush
   })
   ```

### ❌ À ÉVITER

1. **Logique dans les templates**
2. **Manipuler le DOM directement** (utiliser les directives)
3. **Oublier de typer** (TypeScript any partout)
4. **Services dans les composants** (utiliser l'injection)
5. **Modules trop gros** (diviser en feature modules)

---

## Ressources pour aller plus loin

### Documentation officielle
- **Angular.io** : https://angular.io/
- **Angular en français** : https://angular.fr/

### Tutoriels recommandés
- **Tour of Heroes** : Tutoriel officiel Angular
- **Angular University** : Cours approfondis
- **Fireship.io** : Tutoriels rapides et concis

### Outils
- **Angular DevTools** : Extension Chrome/Firefox
- **Augury** : Ancienne extension de debug
- **Angular CLI** : Outil en ligne de commande

### Écosystème
- **Angular Material** : Composants Material Design
- **NgRx** : Gestion d'état (Redux pour Angular)
- **Ionic** : Applications mobiles avec Angular
- **NestJS** : Backend Node.js avec TypeScript (inspiré d'Angular)

---

## Angular vs React vs Vue : Récapitulatif

| Critère | **Angular** | **React** | **Vue** |
|---------|-------------|-----------|---------|
| **Type** | Framework complet | Bibliothèque UI | Framework progressif |
| **Langage** | TypeScript | JavaScript/TypeScript | JavaScript |
| **Courbe d'apprentissage** | 🔴 Élevée | 🟡 Moyenne | 🟢 Facile |
| **Taille (min+gzip)** | ~140 KB | ~45 KB | ~40 KB |
| **Architecture** | Opinionated | Flexible | Progressive |
| **CLI** | ✅ Excellent | ⚠️ CRA (moins maintenu) | ✅ Excellent |
| **Data Binding** | Two-way natif | One-way | Les deux |
| **Entreprise** | Google | Meta | Communauté |
| **Cas d'usage** | Apps entreprise | Apps de toutes tailles | Apps de toutes tailles |

**Choisir Angular si :**
- Projet d'entreprise complexe
- Équipe TypeScript
- Structure stricte souhaitée
- Besoin de tout l'écosystème

**Choisir React si :**
- Flexibilité maximale
- Écosystème riche
- React Native (mobile)

**Choisir Vue si :**
- Débutants
- Projet progressif
- Syntaxe HTML-like préférée

---

## Concepts clés à retenir

### 1. **TypeScript est obligatoire**
```typescript
interface User {
  nom: string;
  age: number;
}
```

### 2. **Architecture en modules, composants, services**
```
Module
├── Composants (@Component)
└── Services (@Injectable)
```

### 3. **Data binding multiple**
```html
{{ valeur }}          Interpolation
[propriété]           Property binding
(événement)           Event binding
[(ngModel)]           Two-way binding
```

### 4. **Directives structurelles**
```html
*ngIf    Conditionnel
*ngFor   Boucles
*ngSwitch  Switch
```

### 5. **RxJS pour l'asynchrone**
```typescript
this.http.get().subscribe(data => {});
```

### 6. **Injection de dépendances**
```typescript
constructor(private service: MonService) {}
```

### 7. **CLI puissant**
```bash
ng generate component mon-composant
```

---

## Conclusion

Angular est un **framework complet et puissant** idéal pour les applications d'entreprise complexes. Sa structure stricte, son typage TypeScript et son écosystème complet en font un excellent choix pour les grands projets nécessitant maintenabilité et scalabilité.

**Points forts d'Angular :**
- ✅ Framework tout-en-un (routing, HTTP, forms, etc.)
- ✅ TypeScript pour la robustesse
- ✅ Architecture claire et structurée
- ✅ CLI puissant et productif
- ✅ Excellent pour l'entreprise
- ✅ Soutien de Google

**Points d'attention :**
- ⚠️ Courbe d'apprentissage élevée
- ⚠️ Plus verbeux que React ou Vue
- ⚠️ Bundle plus lourd
- ⚠️ Moins flexible

**Ce qu'il faut retenir :**
- Angular = Framework complet + TypeScript + RxJS
- Architecture structurée : Modules → Composants → Services
- Data binding multiple : interpolation, property, event, two-way
- CLI Angular génère tout le code nécessaire
- RxJS pour la programmation réactive
- Injection de dépendances pour les services

Angular demande plus d'investissement initial mais offre une structure solide pour les projets ambitieux ! 🚀

---


⏭️ [Quand utiliser un framework ?](/08-ecosysteme-javascript-moderne/03-frameworks-librairies/04-quand-utiliser-framework.md)
