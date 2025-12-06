🔝 Retour au [Sommaire](/SOMMAIRE.md)

# 5.4.5 - Opérateurs modernes : nullish coalescing (??) et optional chaining (?.)

## Introduction

JavaScript ES2020 et ES2021 ont introduit deux opérateurs modernes qui simplifient considérablement le code lorsqu'on travaille avec des valeurs potentiellement `null` ou `undefined` :

- **`??`** (Nullish Coalescing) - Fournir une valeur par défaut
- **`?.`** (Optional Chaining) - Accéder en toute sécurité aux propriétés

Ces opérateurs rendent le code plus propre, plus sûr et plus facile à lire. Ils sont désormais largement supportés et **recommandés** pour tout nouveau code JavaScript.

🆕 **Nouveauté ES2020/ES2021** - À utiliser sans hésitation !

---

## ?? (Nullish Coalescing) - Valeurs par défaut 🆕

L'opérateur **nullish coalescing** (`??`) retourne la valeur de droite si la valeur de gauche est `null` ou `undefined`.

### Syntaxe

```javascript
valeur ?? valeurParDefaut
```

### Qu'est-ce qu'une valeur "nullish" ?

En JavaScript, seules **deux valeurs** sont considérées comme "nullish" :
- `null`
- `undefined`

**Toutes les autres valeurs** (y compris `0`, `""`, `false`) ne sont **PAS** nullish.

### Exemples de base

```javascript
// null ou undefined → utilise la valeur par défaut
console.log(null ?? "défaut");      // "défaut"
console.log(undefined ?? "défaut"); // "défaut"

// Autres valeurs → utilise la valeur de gauche
console.log(0 ?? "défaut");         // 0
console.log("" ?? "défaut");        // ""
console.log(false ?? "défaut");     // false
console.log(0 ?? 100);              // 0
```

### Pourquoi c'est important ?

Avant `??`, on utilisait `||` pour les valeurs par défaut, mais cela causait des problèmes :

```javascript
// ⚠️ Problème avec || (ancien)
const port = 0;
const portFinal = port || 8080;
console.log(portFinal); // 8080 (problème : 0 est une valeur valide !)

// ✅ Solution avec ?? (moderne)
const portFinal2 = port ?? 8080;
console.log(portFinal2); // 0 (correct : 0 est conservé)
```

---

## ?? vs || - Différence cruciale

### Comparaison directe

| Valeur | `valeur \|\| "défaut"` | `valeur ?? "défaut"` |
|--------|----------------------|-------------------|
| `null` | `"défaut"` | `"défaut"` ✅ |
| `undefined` | `"défaut"` | `"défaut"` ✅ |
| `0` | `"défaut"` ⚠️ | `0` ✅ |
| `""` | `"défaut"` ⚠️ | `""` ✅ |
| `false` | `"défaut"` ⚠️ | `false` ✅ |
| `"valeur"` | `"valeur"` | `"valeur"` |

### Explication

**`||` (OU logique)** :
- Retourne la valeur de droite si la gauche est **falsy** (false, 0, "", null, undefined, NaN)
- ⚠️ Problème : considère 0, "", false comme "absents"

**`??` (Nullish coalescing)** :
- Retourne la valeur de droite **uniquement** si la gauche est `null` ou `undefined`
- ✅ Avantage : respecte 0, "", false comme valeurs valides

### Exemples comparatifs

#### Exemple 1 : Compteur à zéro

```javascript
const compteur = 0;

// ❌ Avec || (incorrect)
const valeur1 = compteur || 10;
console.log(valeur1); // 10 (erreur : 0 est remplacé !)

// ✅ Avec ?? (correct)
const valeur2 = compteur ?? 10;
console.log(valeur2); // 0 (correct : 0 est conservé)
```

#### Exemple 2 : String vide

```javascript
const message = "";

// ❌ Avec || (incorrect pour certains cas)
const affichage1 = message || "Pas de message";
console.log(affichage1); // "Pas de message" (peut-être pas voulu)

// ✅ Avec ?? (correct)
const affichage2 = message ?? "Pas de message";
console.log(affichage2); // "" (string vide est conservée)
```

#### Exemple 3 : Booléen false

```javascript
const estActif = false;

// ❌ Avec || (incorrect)
const statut1 = estActif || true;
console.log(statut1); // true (erreur : false est remplacé !)

// ✅ Avec ?? (correct)
const statut2 = estActif ?? true;
console.log(statut2); // false (correct : false est conservé)
```

---

## Cas d'usage de ?? (Nullish Coalescing)

### 1. Configuration avec valeurs par défaut

```javascript
function creerServeur(config) {
    const port = config.port ?? 3000;
    const host = config.host ?? "localhost";
    const debug = config.debug ?? false;

    console.log(`Serveur sur ${host}:${port} (debug: ${debug})`);
}

creerServeur({ port: 0, host: "127.0.0.1" });
// Serveur sur 127.0.0.1:0 (debug: false)
// Note : port 0 est conservé (valide pour l'OS)
```

### 2. Propriétés d'objet optionnelles

```javascript
const utilisateur = {
    nom: "Alice",
    age: 0,           // Nouveau-né !
    premium: false
};

const age = utilisateur.age ?? 18;
const premium = utilisateur.premium ?? false;

console.log(age);     // 0 (correct : bébé de 0 an)
console.log(premium); // false (correct : pas premium)
```

### 3. Paramètres de fonction

```javascript
function afficherNotification(message, duree) {
    const dureeFinal = duree ?? 3000;
    console.log(`${message} (pendant ${dureeFinal}ms)`);
}

afficherNotification("Bonjour", 0); // Bonjour (pendant 0ms)
// 0 est une durée valide (notification instantanée)
```

### 4. Valeurs de formulaire

```javascript
const formData = {
    quantite: 0,      // 0 est une quantité valide
    commentaire: "",  // "" est un commentaire valide (vide)
    newsletter: false // false est un choix valide
};

const quantite = formData.quantite ?? 1;
const commentaire = formData.commentaire ?? "Aucun commentaire";
const newsletter = formData.newsletter ?? true;

console.log(quantite);    // 0 (pas 1)
console.log(commentaire); // "" (pas "Aucun commentaire")
console.log(newsletter);  // false (pas true)
```

### 5. Données de l'API

```javascript
const apiResponse = {
    temperature: 0,  // 0°C est une température valide
    vent: null,      // Pas de données de vent
    pression: undefined
};

const temp = apiResponse.temperature ?? "N/A";
const vent = apiResponse.vent ?? "N/A";
const pression = apiResponse.pression ?? 1013;

console.log(temp);     // 0
console.log(vent);     // "N/A"
console.log(pression); // 1013
```

---

## ?. (Optional Chaining) - Accès sécurisé 🆕

L'opérateur **optional chaining** (`?.`) permet d'accéder aux propriétés d'un objet sans erreur si l'objet est `null` ou `undefined`.

### Syntaxe

```javascript
objet?.propriete
objet?.[expression]
fonction?.()
```

### Le problème qu'il résout

Avant `?.`, accéder à une propriété d'un objet null causait une erreur :

```javascript
const utilisateur = null;

// ❌ Erreur : Cannot read property 'nom' of null
console.log(utilisateur.nom);

// ⚠️ Solution ancienne (verbose)
console.log(utilisateur && utilisateur.nom);

// ✅ Solution moderne (élégante)
console.log(utilisateur?.nom); // undefined (pas d'erreur)
```

### Exemples de base

```javascript
const utilisateur = {
    nom: "Alice",
    adresse: {
        ville: "Paris"
    }
};

// ✅ Propriété existe
console.log(utilisateur?.nom); // "Alice"

// ✅ Propriété n'existe pas
console.log(utilisateur?.telephone); // undefined

// ✅ Objet null
const user2 = null;
console.log(user2?.nom); // undefined (pas d'erreur)
```

---

## Accès aux propriétés imbriquées

### Sans optional chaining (ancien) ⚠️

```javascript
const utilisateur = {
    profil: {
        adresse: {
            ville: "Paris"
        }
    }
};

// ❌ Erreur si profil est null
// console.log(utilisateur.profil.adresse.ville);

// ⚠️ Solution ancienne (très verbeux)
const ville = utilisateur &&
              utilisateur.profil &&
              utilisateur.profil.adresse &&
              utilisateur.profil.adresse.ville;
```

### Avec optional chaining (moderne) ✅

```javascript
// ✅ Élégant et sûr
const ville = utilisateur?.profil?.adresse?.ville;
console.log(ville); // "Paris"

// Si un élément est null/undefined, retourne undefined
const user2 = { profil: null };
const ville2 = user2?.profil?.adresse?.ville;
console.log(ville2); // undefined (pas d'erreur)
```

---

## Cas d'usage de ?. (Optional Chaining)

### 1. Accès aux API responses

```javascript
const apiData = {
    user: {
        profile: {
            name: "Alice",
            avatar: {
                url: "https://..."
            }
        }
    }
};

// ✅ Sécurisé même si la structure change
const avatarUrl = apiData?.user?.profile?.avatar?.url;
console.log(avatarUrl); // "https://..."

// Si l'API change et n'envoie plus avatar
const apiData2 = {
    user: {
        profile: {
            name: "Bob"
        }
    }
};
const avatarUrl2 = apiData2?.user?.profile?.avatar?.url;
console.log(avatarUrl2); // undefined (pas d'erreur)
```

### 2. Appel de fonctions optionnelles

```javascript
const config = {
    onSuccess: (data) => console.log("Succès :", data),
    // onError n'est pas définie
};

// ✅ Appel sécurisé de fonction
config.onSuccess?.("Données reçues"); // "Succès : Données reçues"
config.onError?.("Erreur"); // Rien ne se passe (pas d'erreur)
```

### 3. Accès aux tableaux

```javascript
const data = {
    utilisateurs: [
        { nom: "Alice" },
        { nom: "Bob" }
    ]
};

// ✅ Accès sécurisé aux éléments du tableau
const premierNom = data?.utilisateurs?.[0]?.nom;
console.log(premierNom); // "Alice"

// Si le tableau n'existe pas
const data2 = { utilisateurs: null };
const nom = data2?.utilisateurs?.[0]?.nom;
console.log(nom); // undefined (pas d'erreur)
```

### 4. Méthodes optionnelles

```javascript
const utilisateur = {
    nom: "Alice",
    afficherProfil() {
        console.log(`Profil de ${this.nom}`);
    }
};

// ✅ Appel de méthode sécurisé
utilisateur.afficherProfil?.(); // "Profil de Alice"
utilisateur.supprimerCompte?.(); // Rien (pas d'erreur)

// Avec objet null
const user2 = null;
user2?.afficherProfil?.(); // Rien (pas d'erreur)
```

### 5. Événements du DOM

```javascript
// ✅ Sécurisé si l'élément n'existe pas
document.getElementById("bouton")?.addEventListener("click", () => {
    console.log("Cliqué");
});

// Ou
const element = document.querySelector(".inexistant");
element?.classList?.add("active"); // Pas d'erreur si element est null
```

---

## Combiner ?? et ?.

Ces deux opérateurs fonctionnent **parfaitement ensemble** :

### Exemple 1 : Valeur par défaut avec accès sécurisé

```javascript
const utilisateur = {
    profil: {
        preferences: {
            theme: null
        }
    }
};

// Accès sécurisé + valeur par défaut
const theme = utilisateur?.profil?.preferences?.theme ?? "clair";
console.log(theme); // "clair"
```

### Exemple 2 : Configuration complexe

```javascript
const config = {
    serveur: {
        // port est undefined
    }
};

const port = config?.serveur?.port ?? 3000;
const host = config?.serveur?.host ?? "localhost";
const debug = config?.serveur?.debug ?? false;

console.log(port);  // 3000
console.log(host);  // "localhost"
console.log(debug); // false
```

### Exemple 3 : Données utilisateur

```javascript
function afficherUtilisateur(data) {
    const nom = data?.utilisateur?.nom ?? "Invité";
    const age = data?.utilisateur?.age ?? 0;
    const ville = data?.utilisateur?.adresse?.ville ?? "Inconnue";

    console.log(`${nom}, ${age} ans, de ${ville}`);
}

afficherUtilisateur({}); // "Invité, 0 ans, de Inconnue"
afficherUtilisateur({
    utilisateur: {
        nom: "Alice",
        age: 25,
        adresse: { ville: "Paris" }
    }
}); // "Alice, 25 ans, de Paris"
```

### Exemple 4 : Appel de callback avec valeur par défaut

```javascript
const options = {
    onComplete: null
};

// Appel avec fonction par défaut
const callback = options?.onComplete ?? (() => console.log("Terminé"));
callback(); // "Terminé"
```

---

## Chaînage avec appels de fonctions

### Fonctions optionnelles imbriquées

```javascript
const api = {
    users: {
        get(id) {
            return { id, name: "Alice" };
        }
    }
};

// ✅ Chaînage sécurisé
const userName = api?.users?.get?.(1)?.name;
console.log(userName); // "Alice"

// Si api.users.get n'existe pas
const api2 = { users: {} };
const userName2 = api2?.users?.get?.(1)?.name;
console.log(userName2); // undefined (pas d'erreur)
```

### Avec paramètres dynamiques

```javascript
const data = {
    getUser: (id) => ({ id, name: "Bob" })
};

const id = 42;
const user = data?.getUser?.(id);
console.log(user); // { id: 42, name: "Bob" }
```

---

## Cas pratiques complets

### 1. Gestion de données d'API

```javascript
async function afficherProfil(userId) {
    try {
        const response = await fetch(`/api/users/${userId}`);
        const data = await response.json();

        // Accès sécurisé + valeurs par défaut
        const nom = data?.user?.profile?.fullName ?? "Utilisateur";
        const email = data?.user?.contact?.email ?? "Non renseigné";
        const tel = data?.user?.contact?.phone ?? "Non renseigné";
        const avatar = data?.user?.profile?.avatar?.url ?? "/default-avatar.png";
        const bio = data?.user?.profile?.bio ?? "Aucune biographie";

        return {
            nom,
            email,
            tel,
            avatar,
            bio
        };
    } catch (error) {
        return {
            nom: "Erreur",
            email: "Erreur",
            tel: "Erreur",
            avatar: "/error-avatar.png",
            bio: "Impossible de charger le profil"
        };
    }
}
```

### 2. Configuration d'application

```javascript
function initialiserApp(config) {
    return {
        // Serveur
        port: config?.server?.port ?? 3000,
        host: config?.server?.host ?? "localhost",
        ssl: config?.server?.ssl ?? false,

        // Base de données
        dbHost: config?.database?.host ?? "localhost",
        dbPort: config?.database?.port ?? 5432,
        dbName: config?.database?.name ?? "myapp",

        // Features
        cache: config?.features?.cache ?? true,
        logging: config?.features?.logging ?? true,
        analytics: config?.features?.analytics ?? false,

        // Callbacks
        onStart: config?.hooks?.onStart ?? (() => console.log("Démarré")),
        onError: config?.hooks?.onError ?? ((err) => console.error(err))
    };
}

const appConfig = initialiserApp({
    server: { port: 8080 },
    features: { cache: false }
});

console.log(appConfig.port);  // 8080
console.log(appConfig.cache); // false
console.log(appConfig.dbName); // "myapp"
```

### 3. Manipulation du DOM sécurisée

```javascript
function initialiserInterface() {
    // Éléments potentiellement absents
    const menu = document.querySelector("#menu");
    const sidebar = document.querySelector("#sidebar");
    const modal = document.querySelector("#modal");

    // Initialisation sécurisée
    menu?.classList?.add("initialized");
    sidebar?.setAttribute?.("data-state", "closed");
    modal?.addEventListener?.("click", handleModalClick);

    // Valeurs par défaut
    const menuWidth = menu?.offsetWidth ?? 250;
    const sidebarCollapsed = sidebar?.dataset?.collapsed ?? "true";

    return {
        menuWidth,
        sidebarCollapsed: sidebarCollapsed === "true"
    };
}

function handleModalClick(e) {
    // Accès sécurisé aux propriétés de l'événement
    const targetId = e?.target?.id;
    const targetClass = e?.target?.className;
    const targetData = e?.target?.dataset?.action;

    console.log(`Cliqué sur : ${targetId ?? "élément sans ID"}`);
}
```

### 4. Système de notifications

```javascript
class NotificationManager {
    constructor(options) {
        this.duree = options?.duree ?? 3000;
        this.position = options?.position ?? "top-right";
        this.sound = options?.sound ?? false;
        this.onShow = options?.callbacks?.onShow ?? null;
        this.onClose = options?.callbacks?.onClose ?? null;
    }

    afficher(message, type) {
        const config = {
            texte: message?.texte ?? "Notification",
            titre: message?.titre ?? "Info",
            icone: message?.icone ?? this.getIconeParDefaut(type),
            duree: message?.duree ?? this.duree
        };

        console.log(`[${type?.toUpperCase() ?? "INFO"}] ${config.titre}: ${config.texte}`);

        // Callback optionnel
        this.onShow?.(config);

        // Auto-fermeture
        setTimeout(() => {
            this.onClose?.(config);
        }, config.duree);
    }

    getIconeParDefaut(type) {
        const icones = {
            success: "✅",
            error: "❌",
            warning: "⚠️",
            info: "ℹ️"
        };
        return icones?.[type] ?? "ℹ️";
    }
}

const notif = new NotificationManager({
    duree: 5000,
    callbacks: {
        onShow: (config) => console.log("Notification affichée")
    }
});

notif.afficher({ texte: "Opération réussie" }, "success");
```

### 5. Parser de données complexes

```javascript
function extraireDonnees(response) {
    // Structure complexe potentiellement incomplète
    const data = response?.data;

    return {
        // Informations utilisateur
        userId: data?.user?.id ?? null,
        userName: data?.user?.profile?.displayName ?? "Anonyme",
        userEmail: data?.user?.contact?.email ?? "",
        userAvatar: data?.user?.profile?.images?.avatar?.url ?? null,

        // Paramètres
        theme: data?.settings?.appearance?.theme ?? "auto",
        langue: data?.settings?.locale?.language ?? "fr",
        notifications: data?.settings?.notifications?.enabled ?? true,

        // Statistiques
        posts: data?.stats?.content?.posts ?? 0,
        followers: data?.stats?.social?.followers ?? 0,
        following: data?.stats?.social?.following ?? 0,

        // Dates (avec conversion)
        createdAt: data?.timestamps?.created
            ? new Date(data.timestamps.created)
            : null,
        lastLogin: data?.timestamps?.lastLogin
            ? new Date(data.timestamps.lastLogin)
            : null,

        // Méthodes
        sendMessage: data?.actions?.messaging?.send ?? null,
        blockUser: data?.actions?.moderation?.block ?? null
    };
}

// Utilisation
const result = extraireDonnees({
    data: {
        user: {
            id: 123,
            profile: { displayName: "Alice" }
        },
        stats: {
            content: { posts: 42 }
        }
    }
});

console.log(result.userName);   // "Alice"
console.log(result.posts);      // 42
console.log(result.followers);  // 0 (valeur par défaut)
```

---

## Erreurs courantes à éviter

### ❌ Erreur 1 : Utiliser || au lieu de ??

```javascript
const quantite = 0;

// ❌ Incorrect : 0 est remplacé
const qte1 = quantite || 1;
console.log(qte1); // 1 (erreur)

// ✅ Correct : 0 est conservé
const qte2 = quantite ?? 1;
console.log(qte2); // 0
```

### ❌ Erreur 2 : Confondre ?. et ?.()

```javascript
const obj = {
    methode: () => "résultat"
};

// ❌ Erreur : accès à la fonction, pas appel
const resultat1 = obj?.methode;
console.log(resultat1); // [Function: methode]

// ✅ Correct : appel de fonction
const resultat2 = obj?.methode?.();
console.log(resultat2); // "résultat"
```

### ❌ Erreur 3 : Oublier ?? après ?.

```javascript
const config = {};

// ⚠️ Risqué : retourne undefined
const port1 = config?.port;
console.log(port1); // undefined

// ✅ Sûr : valeur par défaut
const port2 = config?.port ?? 3000;
console.log(port2); // 3000
```

### ❌ Erreur 4 : Utiliser ?. sur des primitives

```javascript
const nombre = 42;

// ❌ Inutile : les nombres ne sont jamais null/undefined ici
const valeur = nombre?.toString();

// ✅ Simple
const valeur2 = nombre.toString();
```

### ❌ Erreur 5 : Combiner avec && ou ||

```javascript
// ❌ Erreur de syntaxe
const resultat = valeur ?? "défaut" || "autre";
// SyntaxError: Cannot use '||' with '??'

// ✅ Utilisez des parenthèses
const resultat2 = (valeur ?? "défaut") || "autre";
```

---

## Bonnes pratiques

### ✅ 1. Utilisez ?? pour les valeurs par défaut

```javascript
// ✅ Moderne et précis
const config = {
    port: userConfig?.port ?? 3000,
    debug: userConfig?.debug ?? false
};
```

### ✅ 2. Chaînez ?. pour les objets profonds

```javascript
// ✅ Élégant et sûr
const ville = user?.address?.city?.name ?? "Inconnue";
```

### ✅ 3. Combinez les deux pour maximum de sécurité

```javascript
// ✅ Accès sécurisé + valeur par défaut
const theme = settings?.appearance?.theme ?? "clair";
```

### ✅ 4. Utilisez ?. avec les méthodes du DOM

```javascript
// ✅ Pas d'erreur si l'élément n'existe pas
document.getElementById("menu")?.classList?.add("open");
```

### ✅ 5. Préférez ?? à ||

```javascript
// ⚠️ Ancien : peut causer des bugs
const value = input || "default";

// ✅ Moderne : précis
const value = input ?? "default";
```

---

## Support navigateur

Ces opérateurs sont disponibles dans :
- ✅ Chrome 80+ (2020)
- ✅ Firefox 72+ (2020)
- ✅ Safari 13.1+ (2020)
- ✅ Edge 80+ (2020)
- ✅ Node.js 14+ (2020)

**Recommandation** : Utilisez-les sans hésitation dans tout nouveau projet !

---

## Points clés à retenir

✅ **`??` (Nullish Coalescing)** : valeur par défaut uniquement pour `null` et `undefined`

✅ **`?.` (Optional Chaining)** : accès sécurisé aux propriétés sans erreur

✅ **Différence `??` vs `||`** : `??` ne traite que null/undefined, `||` traite toutes les valeurs falsy

✅ **Combiner les deux** : `objet?.prop?.subProp ?? "défaut"` pour maximum de sécurité

✅ **Utilisez `??`** au lieu de `||` pour les valeurs par défaut

✅ **Utilisez `?.`** pour accéder aux propriétés d'objets potentiellement null/undefined

✅ **Valeurs conservées** : 0, "", false sont conservés avec `??` (contrairement à `||`)

🆕 **ES2020/ES2021** : Ces opérateurs sont modernes et recommandés

---

## Tableau récapitulatif

| Opérateur | Usage | Retourne valeur de droite si gauche est... |
|-----------|-------|-------------------------------------------|
| `\|\|` | OU logique | falsy (0, "", false, null, undefined, NaN) |
| `??` | Valeur par défaut | **null ou undefined seulement** |
| `?.` | Accès sécurisé | null ou undefined (retourne undefined) |

---

## Migration du code ancien

### Avant (ancien code)

```javascript
// ❌ Verbeux et risqué
const port = config && config.port || 3000;
const name = user && user.profile && user.profile.name || "Invité";
```

### Après (code moderne)

```javascript
// ✅ Concis et précis
const port = config?.port ?? 3000;
const name = user?.profile?.name ?? "Invité";
```

---

## Dans la prochaine section

Félicitations ! Vous avez terminé la section sur les **opérateurs** en JavaScript. Vous maîtrisez maintenant :
- Les opérateurs arithmétiques
- Les opérateurs de comparaison (===, !==)
- Les opérateurs logiques (&&, ||, !)
- L'opérateur ternaire (? :)
- Les opérateurs modernes (??, ?.)

Dans le **chapitre suivant (5.5 - Structures de contrôle)**, nous découvrirons comment contrôler le flux d'exécution de votre code avec les conditions et les boucles.

---


⏭️ [Structures de contrôle](/05-javascript-moderne-fondamentaux/05-structures-controle/README.md)
