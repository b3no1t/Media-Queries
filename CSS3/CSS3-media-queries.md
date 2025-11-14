---
title: "CSS2 Media Queries : les fondations"
export_on_save:
  html: true
---

# Guide complet des Media Queries CSS3

>Avant d'entamer l'apprentissage des media queries, il est essentiel de maîtriser le vocabulaire technique qui constituera la base de votre compréhension. Chaque terme présenté ici sera utilisé tout au long de ce guide et représente un concept fondamental du responsive design.

## Termes fondamentaux

**Media Query** : Une instruction CSS qui permet d'appliquer des règles de style conditionnelles en fonction des caractéristiques de l'appareil de l'utilisateur. Le terme "query" signifie "requête" ou "interrogation" - on interroge donc le navigateur sur les caractéristiques de l'écran avant d'appliquer des styles spécifiques. *C'est comme adapter les meubles selon la taille de la pièce
Vous réorganisez tout votre salon différemment selon que vous êtes dans un studio ou une grande maison.*

**Responsive Design** : Approche de conception web qui vise à créer des interfaces s'adaptant automatiquement et intelligemment à tous les types d'écrans et d'appareils, du smartphone à l'écran de bureau en passant par les tablettes. Le terme "responsive" signifie littéralement "qui répond" - le design répond aux caractéristiques de l'appareil utilisé.

**Breakpoint** : Point de rupture défini en pixels où le design change de mise en page. C'est le seuil à partir duquel une media query s'active ou se désactive. Par exemple, un breakpoint à 600px signifie que le comportement du site changera à cette largeur d'écran précise.

**Viewport** : Zone d'affichage visible de la page web dans la fenêtre du navigateur. C'est littéralement ce que l'utilisateur peut voir sans faire défiler la page. Sur mobile, le viewport correspond à la taille de l'écran du téléphone. Sur desktop, il correspond à la taille de la fenêtre du navigateur.

**Mobile-First** : Méthodologie de développement qui consiste à concevoir et coder d'abord pour les appareils mobiles (petits écrans), puis à enrichir progressivement l'expérience pour les écrans plus grands. Cette approche part du principe que le mobile représente désormais la majorité du trafic web.

**Pixel (px)** : Unité de mesure fondamentale en CSS représentant un point d'affichage à l'écran. Un écran de 1920px de large contient 1920 points horizontalement. C'est l'unité la plus utilisée pour définir les breakpoints car elle offre un contrôle précis.

## Termes CSS spécifiques

**max-width** : Propriété de condition signifiant "largeur maximale". Dans une media query, max-width: 600px cible tous les écrans dont la largeur est inférieure ou égale à 600 pixels. C'est l'outil principal de l'approche desktop-first.

**min-width** : Propriété de condition signifiant "largeur minimale". Dans une media query, min-width: 600px cible tous les écrans dont la largeur est supérieure ou égale à 600 pixels. C'est l'outil principal de l'approche mobile-first.

**Cascade CSS** : Principe fondamental du CSS selon lequel, lorsque plusieurs règles s'appliquent au même élément, c'est la dernière règle définie qui prend le dessus.
*Ce principe est crucial pour comprendre l'ordre des media queries*.

**Block vs Inline** : Deux types d'affichage fondamentaux en HTML. Un élément "block" (comme ``<div>``) occupe toute la largeur disponible et force un retour à la ligne. Un élément "inline" (comme ``<span>``) ne prend que la place nécessaire et reste sur la même ligne.

### Termes d'architecture

**Layout** : Organisation spatiale et structurelle des éléments sur une page web. Le layout définit comment les blocs de contenu sont positionnés les uns par rapport aux autres. En responsive design, le layout change selon la taille d'écran.

**Flexbox** : Système de mise en page CSS moderne permettant d'organiser des éléments de manière flexible et adaptative. Le terme vient de "flexible box" (boîte flexible). C'est l'outil idéal pour créer des mises en page qui s'adaptent automatiquement.

**Orientation** : Direction dans laquelle l'appareil est tenu. "Portrait" signifie vertical (hauteur supérieure à la largeur), "landscape" signifie horizontal (largeur supérieure à la hauteur). Les media queries peuvent détecter cette orientation.

## Documentation de référence

Pour approfondir vos connaissances et consulter la documentation officielle, ces ressources constituent des références incontournables :

- MDN Web Docs - [Media Queries](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_media_queries) - La documentation de référence maintenue par Mozilla, exhaustive et précise
- W3Schools - [Responsive Web Design](https://www.w3schools.com/css/css_rwd_intro.asp) - Des tutoriels interactifs et des exemples pratiques
- Can I Use : https://caniuse.com - Pour vérifier la compatibilité des media queries avec différents navigateurs

***

## Le contexte historique et technique

Dans les premières années du web, les sites étaient conçus pour une seule taille d'écran : celle des ordinateurs de bureau, généralement autour de **1024 pixels** de large. Cette approche fonctionnait car les variations d'écrans étaient minimes.

Cependant, l'arrivée des smartphones en **2007**, puis des tablettes, a radicalement transformé le paysage du web.

Aujourd'hui, les utilisateurs naviguent sur des écrans variant de 320 pixels (petits smartphones) à plus de **2560 pixels** (écrans 4K). Sans adaptation, un site conçu pour 1024px de large serait illisible sur un smartphone de 375px et sous-exploité sur un écran de 1920px.

## Le problème fondamental

Observons un problème concret que rencontrent tous les développeurs web débutants.

```html
 <!DOCTYPE html>
 <html lang="fr">
 <head>
   <meta charset="UTF-8">
   <title>Problème de largeur fixe</title>
   <style>
     /* Cette carte a une largeur fixe de 800 pixels */
     .carte {
       width: 800px;           /* Largeur rigide, non adaptative */
       background: lightblue;
       padding: 20px;          /* Espacement interne de 20 pixels */
       margin: 20px;           /* Espacement externe de 20 pixels */
     }
   </style>
 </head>
 <body>
   <div class="carte">
     <h2>Horaires d'ouverture</h2>
     <p>Notre restaurant est ouvert du lundi au vendredi de 12h à 14h</p>
   </div>
 </body>
 </html>
```

### Analyse du problème

Sur un ordinateur avec un écran de 1920px de large, cette carte de 800px s'affiche parfaitement. Mais que se passe-t-il sur un smartphone dont l'écran fait 375px de large ?

La carte nécessite 800px (largeur) + 40px (padding gauche et droite) + 40px (margin gauche et droite) = 880px au total. Sur un écran de 375px, elle déborde de 505 pixels, créant un défilement horizontal désagréable et rendant le contenu partiellement invisible.

#### Conséquences concrètes:

 L'utilisateur doit faire défiler horizontalement pour lire le contenu.
 L'expérience utilisateur est dégradée.
 Le taux de rebond augmente (les visiteurs quittent le site).
 Le référencement Google est pénalisé (Google privilégie les sites mobile-friendly).

#### La solution : Les Media Queries

Les media queries offrent une solution élégante à ce problème en permettant d'appliquer des styles différents selon les caractéristiques de l'appareil. 
Au lieu d'une seule version rigide, vous créez plusieurs versions adaptatives qui se déclenchent automatiquement.

***

## Chapitre 1 : Votre première Media Query

### Comprendre la syntaxe de base

Une media query suit une structure logique et précise. Décomposons-la élément par élément :

```css
@media (max-width: 600px) {
  /* Règles CSS ici */
}
```

#### Analyse détaillée de chaque composant

**@media** : Le mot-clé qui signale au navigateur qu'une condition va suivre. Le symbole @ indique une règle spéciale en CSS (appelée "at-rule").
**Les parenthèses ( )** : Contiennent la condition à tester. C'est une interrogation que le navigateur va évaluer comme vraie ou fausse.
**max-width: 600px** : La condition elle-même. Littéralement : "si la largeur maximale de l'écran est de 600 pixels". En d'autres termes : "si l'écran fait 600px ou moins".
**Les accolades { }** : Délimitent le bloc de règles CSS qui s'appliquera uniquement si la condition est vraie.

## Premier exemple fonctionnel et commenté

Créons ensemble votre première page responsive avec une media query :

````html
 <!DOCTYPE html>
 <html lang="fr">
 <head>
   <meta charset="UTF-8">
   <!-- CRUCIAL : Cette balise indique au navigateur de s'adapter à la taille réelle de l'écran -->
   <!-- Sans elle, les media queries ne fonctionnent pas correctement sur mobile -->
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Ma première media query</title>
   <style>
     /* ===== STYLES DE BASE (s'appliquent à TOUS les écrans) ===== */
     .carte {
       width: 800px;              /* Largeur pour grands écrans */
       background: lightblue;     /* Fond bleu clair */
       padding: 20px;             /* 20px d'espace à l'intérieur */
       margin: 20px auto;         /* Centrage horizontal avec 'auto' */
       border-radius: 8px;        /* Coins arrondis de 8 pixels */
     }
     
     .carte h2 {
       margin-top: 0;               /* Supprime l'espace au-dessus du titre */
       color: #2c3e50;            /* Couleur gris-bleu foncé */
     }
     
     /* ===== MEDIA QUERY POUR PETITS ÉCRANS ===== */
     /* Cette règle s'active uniquement quand l'écran fait 700px ou moins */
     @media (max-width: 700px) {
       .carte {
         width: 90%;            /* Prend 90% de la largeur disponible */
         /* Pourquoi 90% et pas 100% ? Pour garder un peu d'air sur les côtés */
         
         background: lightcoral; /* Change le fond en rose corail */
         /* Ce changement de couleur est juste pour visualiser la transition */
         
         padding: 15px;         /* Réduit le padding pour économiser l'espace */
         margin: 10px auto;     /* Réduit aussi les marges externes */
       }
       
       .carte h2 {
         font-size: 1.2em;      /* Réduit la taille du titre sur mobile */
         /* 1.2em = 1.2 fois la taille de police parente */
       }
     }
   </style>
 </head>
 <body>
   <div class="carte">
     <h2>Bienvenue sur notre site 🎉</h2>
     <p>Réduisez la largeur de votre fenêtre pour voir la carte s'adapter automatiquement. Observez le changement de couleur qui se produit à 700 pixels de large.</p>
   </div>
 </body>
 </html>
````

### Comprendre ce qui se passe étape par étape

#### Scenario 1 : Écran de 1200px (ordinateur de bureau)

Le navigateur lit les styles de base
La carte a une largeur de 800px avec un fond bleu clair
Le navigateur lit la media query @media (max-width: 700px)
Il évalue : "1200px est-il inférieur ou égal à 700px ?" → NON
Les styles dans la media query ne s'appliquent PAS
**Résultat :** carte bleue de 800px

#### Scenario 2 : Écran de 500px (smartphone)

Le navigateur lit les styles de base
La carte commence avec une largeur de 800px et un fond bleu
Le navigateur lit la media query @media(max-width: 700px)
Il évalue : "500px est-il inférieur ou égal à 700px ?" → OUI
Les styles dans la media query REMPLACENT les styles de base
**Résultat :** carte rose corail de 90% de largeur (soit 450px sur un écran de 500px)

#### Scenario 3 : Exactement 700px

La condition max-width: 700px inclut 700px
À 700px, la media query **s'active**
À 701px, elle **se désactive**
Le point de transition est donc précisément à 700px

***

### Exercice pratique guidé

Modifiez l'exemple ci-dessus pour ajouter ces comportements :

#### Objectif 1 : Changer la couleur du texte

````css
@media (max-width: 700px) {

  .carte {
    width: 90%;
    background: lightcoral;
  }

  /* Ajoutez cette règle : */
  .carte p {
    color: #ffffff;        /* Texte blanc pour meilleur contraste */
    font-size: 0.9em;      /* Légèrement plus petit sur mobile */
  }

}
````

##### Pourquoi cette modification ?

Sur mobile, l'espace est précieux. 
Réduire légèrement la taille de police permet d'afficher plus de contenu sans scroll, tout en restant lisible.

##### Objectif 2 : Masquer un élément sur mobile

````html
<!-- Ajoutez ceci dans votre HTML : -->
<div class="carte">
  <h2>Bienvenue sur notre site 🎉</h2>
  <p>Réduisez la largeur de votre fenêtre...</p>
  <p class="detail">Cette information secondaire n'est visible que sur grand écran.</p>
</div>
````

Puis dans votre CSS :

````css
 @media (max-width: 700px) {

   /* Ajoutez cette règle : */
   .detail {
     display: none;        /* Masque cet élément sur petits écrans */
   }

 }
````

#### Pourquoi masquer du contenu ?

Concentrez-vous sur l'essentiel et évitez la surcharge d'informations. 
Les détails secondaires peuvent être cachés pour améliorer la lisibilité.

## Chapitre 2 : Maîtriser les conditions min-width et max-width

**La différence fondamentale entre min et max**
Ces deux conditions sont les piliers des media queries, mais elles fonctionnent de manière opposée. Comprendre cette différence est crucial pour maîtriser le responsive design.

### max-width : Cibler les petits écrans

```css
/* Cette règle dit : "SI l'écran fait AU MAXIMUM 600px" */
/* Autrement dit : "SI l'écran fait 600px OU MOINS" */
@media (max-width: 600px) {
  .element {
    /* Ces styles s'appliquent aux PETITS écrans */
  }
}
```

**Visualisation :**

```text

0px ←────────────────→ 600px ←────────────────→ ∞
       ✅ S'applique         ❌ Ne s'applique pas
```

### min-width : Cibler les grands écrans

```css
/* Cette règle dit : "SI l'écran fait AU MINIMUM 600px" */
/* Autrement dit : "SI l'écran fait 600px OU PLUS" */
@media (min-width: 600px) {
  .element {
    /* Ces styles s'appliquent aux GRANDS écrans */
  }
}
```

**Visualisation :**

```text
0px ←────────────────→ 600px ←────────────────→ ∞
    ❌ Ne s'applique pas      ✅ S'applique
```

#### Cas d'usage typiques

•  Ajouter des colonnes supplémentaires
•  Afficher plus d'informations
•  Augmenter les espacements et marges
•  Activer des effets visuels plus complexes

#### Exemple comparatif détaillé

Créons un composant qui se comporte différemment selon l'approche choisie.

```html
 <!DOCTYPE html>
 <html lang="fr">
 <head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Comparaison min-width vs max-width</title>
   <style>
     /* ========================================
        APPROCHE 1 : DESKTOP-FIRST (max-width)
        ======================================== */
     
     .titre-desktop-first {
       /* Styles pour GRANDS écrans par défaut */
       font-size: 32px;             /* Grande taille pour desktop */
       color: #2c3e50;            /* Bleu foncé */
       text-align: left;            /* Aligné à gauche */
       padding: 30px;               /* Grand espacement */
       background: #ecf0f1;       /* Fond gris clair */
     }
     
     /* On ADAPTE ensuite pour les petits écrans */
     @media (max-width: 768px) {
       .titre-desktop-first {
         font-size: 20px;         /* Réduit pour mobile */
         text-align: center;      /* Centre sur mobile */
         padding: 15px;           /* Réduit l'espacement */
         background: #3498db;   /* Change le fond */
         color: white;            /* Texte blanc pour contraste */
       }
     }
     
     /* ========================================
        APPROCHE 2 : MOBILE-FIRST (min-width)
        ======================================== */
     
     .titre-mobile-first {
       /* Styles pour PETITS écrans par défaut */
       font-size: 20px;           /* Petite taille pour mobile */
       color: white;              /* Texte blanc */
       text-align: center;        /* Centré sur mobile */
       padding: 15px;             /* Petit espacement */
       background: #e74c3c;       /* Fond rouge */
     }
     
     /* On AMÉLIORE ensuite pour les grands écrans */
     @media (min-width: 769px) {
       .titre-mobile-first {
         font-size: 32px;         /* Augmente pour desktop */
         text-align: left;        /* Aligne à gauche */
         padding: 30px;           /* Augmente l'espacement */
         background: #ecf0f1;     /* Fond gris clair */
         color: #2c3e50;          /* Texte bleu foncé */
       }
     }
     
     /* Styles pour la démonstration */
     .container {
       max-width: 1200px;
       margin: 40px auto;
       padding: 20px;
     }
     
     .explication {
       background: #fffacd;
       padding: 15px;
       border-left: 4px solid #f39c12;
       margin: 20px 0;
     }
   </style>
 </head>
 <body>
   <div class="container">
     <div class="explication">
       <strong>Instructions :</strong> Réduisez et agrandissez la fenêtre de votre navigateur. 
       Observez comment les deux titres se comportent différemment selon l'approche utilisée.
     </div>
     
     <h1 class="titre-desktop-first">
       Approche Desktop-First (max-width)
     </h1>
     
     <h1 class="titre-mobile-first">
       Approche Mobile-First (min-width)
     </h1>
     
     <div class="explication">
       <strong>Résultat identique, approche différente :</strong><br>
       • Desktop-First part de grand et réduit<br>
       • Mobile-First part de petit et agrandit<br>
       • Les deux arrivent au même résultat visuel
     </div>
   </div>
 </body>
 </html>
 ```

[codepen link](https://codepen.io/b3no1t/pen/OPNymqV)

### Analyse des deux approches

#### Desktop-First : La logique de réduction

Quand vous utilisez ``max-width``, vous pensez en termes de **réduction** et d'adaptation.
Vous créez d'abord une version complète et riche pour desktop, puis vous "enlevez" des éléments ou réduisez la complexité pour les petits écrans.

**Avantages** :

- **Intuitif** si vous concevez d'abord sur desktop
- Facile de visualiser la version "complète" en premier

**Inconvénients** :

- Peut amener à surcharger la version mobile
- Le code mobile peut devenir une longue liste de réductions
- **Beaucoup moins performant** (le mobile charge tout le CSS desktop d'abord)

#### Mobile-First : La logique d'amélioration progressive

Quand vous utilisez ``min-width``, vous pensez en termes d'**enrichissement**. 
Vous créez d'abord une version simple et épurée pour mobile, puis vous "ajoutez" des fonctionnalités pour les grands écrans.

**Avantages** :

- Force à prioriser le contenu essentiel
- Meilleure performance sur mobile (moins de CSS à surcharger)
- Aligné avec la réalité (60%+ du trafic est mobile, 67% pour cfitech.be)
- Code plus propre et maintenable

**Inconvénients** :

- Nécessite un changement de mentalité (mind-set)
- Peut sembler contre-intuitif au début

### Règle de ciblage précis avec AND

Parfois, vous voulez cibler une plage de tailles spécifique, ni trop petite ni trop grande. 

**C'est là qu'intervient l'opérateur** ``AND`` :

```css
 /* Cible UNIQUEMENT les écrans entre 600px et 900px */
 /* Les tablettes, en quelque sorte */
 @media (min-width: 600px) and (max-width: 900px) {
   .element {
     /* Styles spécifiques aux tablettes */
   }
 }
```

```text

Décomposition logique :

min-width: 600px → "Au moins 600px" → Exclut les petits écrans (< 600px)
            AND → "ET en même temps"
max-width: 900px → "Au maximum 900px" → Exclut les grands écrans (> 900px)
```

**Résultat :** Seuls les écrans entre 600px et 900px (inclus) sont ciblés.

**Visualisation :**

```text
0px ←────→ 600px ←──────────────→ 900px ←────→ ∞
      ❌          ✅ S'applique         ❌
```

### Exemple pratique

```css
 /* Styles de base pour mobile */
.galerie {
  display: block;           /* Une colonne */
}

.photo {
  width: 100%;              /* Pleine largeur */
  margin-bottom: 15px;
}

/* Tablettes : 2 colonnes */
@media (min-width: 600px) and (max-width: 900px) {
  .galerie {
    display: flex;          /* Active Flexbox */
    flex-wrap: wrap;        /* Permet le retour à la ligne */
    gap: 15px;              /* Espace entre les éléments */
  }
  
  .photo {
    width: calc(50% - 8px); /* 2 colonnes avec espace */
    /* calc() fait le calcul : 50% de largeur moins la moitié du gap */
    margin-bottom: 0;       /* Supprime la marge, le gap suffit */
  }
}

/* Desktop : 3 colonnes */
@media (min-width: 901px) {
  .galerie {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }
  
  .photo {
    width: calc(33.333% - 14px); /* 3 colonnes */
  }
}
```

#### Pourquoi ces calculs spécifiques ?

Pour **2 colonnes avec un gap de 15px** :

- Largeur totale = 100%
- Gap total = 15px (entre les deux colonnes)
- Chaque photo = 50% - (15px / 2) = 50% - 8px

Pour **3 colonnes avec un gap de 20px** :

- Largeur totale = 100%
- Gap total = 40px (deux gaps pour trois colonnes)
- Chaque photo = 33.333% - (40px / 3) ≈ 33.333% - 14px

***

## Chapitre 3 : Menu de navigation responsive

**Analyse du comportement attendu**
Un menu de navigation moderne doit s'adapter intelligemment à l'espace disponible.

**Observons** les comportements types :

### Sur mobile (< 600px) :

- Les liens sont empilés verticalement
- Chaque lien occupe toute la largeur
- Les zones tactiles sont grandes (minimum 44px de hauteur recommandée)
- Le design est simplifié

### Sur desktop (≥ 600px) :

- Les liens sont alignés horizontalement
- L'espace est utilisé efficacement
- Des effets de survol (hover) sont possibles
- Plus d'informations peuvent être affichées

### Construction étape par étape

#### Étape 1 : Structure HTML sémantique

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Menu Responsive</title>
</head>
<body>
  <!-- L'élément <nav> indique sémantiquement que c'est une navigation -->
  <!-- Cela aide l'accessibilité et le référencement -->
  <nav class="menu-principal">
    <!-- <ul> pour liste non ordonnée (unordered list) -->
    <ul>
      <!-- Chaque <li> contient un lien -->
      <li><a href="#accueil">Accueil</a></li>
      <li><a href="#services">Services</a></li>
      <li><a href="#portfolio">Portfolio</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</body>
</html>
```

##### Pourquoi cette structure ?

``<nav>`` : Indique aux lecteurs d'écran et aux moteurs de recherche qu'il s'agit d'une navigation.
``<ul>`` et ``<li>`` : Structure sémantique pour une liste de liens

#### Étape 2 : Styles de base (reset et typographie)

```css
/* ===== RESET DES STYLES PAR DÉFAUT ===== */
/* Les navigateurs appliquent des styles par défaut qu'on veut neutraliser */

* {
  margin: 0;              /* Supprime toutes les marges par défaut */
  padding: 0;             /* Supprime tous les paddings par défaut */
  box-sizing: border-box; /* Change le modèle de boîte CSS */
  /* box-sizing: border-box signifie que width inclut padding et border */
  /* Sans cela, width + padding + border = largeur totale (compliqué) */
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  /* Liste de polices de secours : si la première n'est pas disponible, 
     le navigateur essaie la suivante */
  line-height: 1.6;       /* Espacement entre les lignes pour meilleure lisibilité */
}
```

#### Reset ?? : Pourquoi ce reset ?

Chaque navigateur a ses propres styles par défaut (Chrome, Firefox, Safari...). Ce reset crée une base cohérente et **prévisible** pour tous les navigateurs.

#### Étape 3 : Styles du menu (version mobile-first)

```css
/* ===== STYLES MOBILE (base) ===== */

.menu-principal {
  background: #2c3e50;    /* Fond bleu-gris foncé */
  /* Pourquoi ce fond sombre ? Contraste avec le contenu, hiérarchie visuelle */
}

.menu-principal ul {
  list-style: none;       /* Supprime les puces de liste */
  /* Les puces n'ont pas de sens dans un menu de navigation */
}

.menu-principal li {
  /* Sur mobile, les <li> sont déjà en "block" par défaut */
  /* Ils s'empilent donc naturellement verticalement */
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  /* Bordure subtile pour séparer visuellement les liens */
  /* rgba(255,255,255,0.1) = blanc avec 10% d'opacité */
}

.menu-principal li:last-child {
  border-bottom: none;    /* Pas de bordure pour le dernier élément */
  /* Évite une bordure inutile en bas du menu */
}

.menu-principal a {
  /* Le lien est l'élément cliquable, c'est lui qu'on stylise */
  display: block;         /* Transforme le lien en bloc pour occuper toute la largeur */
  /* Par défaut, <a> est "inline" et ne prendrait que la place du texte */
  
  color: white;           /* Texte blanc pour contraste sur fond sombre */
  text-decoration: none;  /* Supprime le soulignement par défaut des liens */
  padding: 15px 20px;     /* 15px haut/bas, 20px gauche/droite */
  /* Zone tactile confortable : au moins 44x44px recommandé pour mobile */
  
  transition: background-color 0.3s; /* Animation douce pour le changement de fond au survol */

}
.menu-principal a:hover,
.menu-principal a:focus {
  background: #34495e;    /* Fond légèrement plus clair au survol/focus / :hover = survol souris, :focus = navigation clavier (accessibilité) */
}
.menu-principal a:active {
  background: #1abc9c;    /* Couleur turquoise lors du clic / Feedback visuel immédiat pour l'utilisateur */
}

```

**Détails techniques importants :**

**`display: block` sur les liens :**
Sans cette propriété, les liens ne prendraient que la largeur de leur texte. En les transformant en blocs, toute la ligne devient cliquable, ce qui est crucial pour l'expérience mobile où les zones tactiles doivent être généreuses.

**Les états des liens (:hover, :focus, :active) :**

- `:hover` : Déclenché quand la souris survole l'élément
- `:focus` : Déclenché quand l'élément est sélectionné au clavier (Tab)
- `:active` : Déclenché au moment précis du clic

**Pourquoi :focus est important :**
L'accessibilité ! Les utilisateurs qui naviguent au clavier (personnes handicapées, power users) doivent pouvoir voir où ils se trouvent dans la navigation.

#### Étape 4 : Adaptation pour desktop avec media query

```css
/* ===== STYLES DESKTOP (amélioration progressive) ===== */

@media (min-width: 600px) {
  /* À partir de 600px, on passe en mode horizontal */
  
  .menu-principal ul {
    display: flex;        /* Active le mode Flexbox */
    /* Flexbox aligne les éléments horizontalement par défaut */
    
    justify-content: center; /* Centre les éléments horizontalement */
    /* Alternatives : flex-start (gauche), flex-end (droite), space-between */
    
    gap: 0;               /* Pas d'espace entre les éléments */
    /* On gère l'espacement avec les bordures visuelles */
  }
  
  .menu-principal li {
    border-bottom: none;  /* Supprime les bordures horizontales */
    border-right: 1px solid rgba(255, 255, 255, 0.1);
    /* Ajoute des séparateurs verticaux entre les liens */
  }
  
  .menu-principal li:last-child {
    border-right: none;   /* Pas de bordure à droite du dernier élément */
  }
  
  .menu-principal a {
    padding: 15px 30px;   /* Augmente le padding horizontal sur desktop */
    /* Plus d'espace = interface plus aérée et confortable */
  }
  
  .menu-principal a:hover {
    background: #1abc9c;  /* Effet hover plus prononcé sur desktop */
    transform: translateY(-2px); /* Soulève légèrement le lien */
    /* Effet subtil mais efficace pour indiquer l'interactivité */
  }
}
```

**Analyse du comportement Flexbox :**

Quand on applique `display: flex` à l'élément `<ul>` :

1. Tous ses enfants directs (`<li>`) deviennent des "flex items"
2. Par défaut, ces items s'alignent horizontalement (direction row)
3. Ils ne retournent pas à la ligne sauf si on ajoute `flex-wrap: wrap`

**Visualisation de la transformation :**

```text
AVANT (mobile) :          APRÈS (desktop) :
┌─────────────┐          ┌──────┬──────┬──────┬──────┐
│ Accueil    │          │Accu..│Serv..│Portf.│Conta.│
├─────────────┤   →      └──────┴──────┴──────┴──────┘
│ Services   │
├─────────────┤          Alignés horizontalement
│ Portfolio  │
├─────────────┤
│ Contact   │
└─────────────┘
```

#### Étape 5 : Code complet avec commentaires

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Menu Navigation Responsive</title>
  <style>
    /* =======================================
       RESET ET BASE
       ======================================= */
    
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      line-height: 1.6;
      background: #ecf0f1; /* Fond général de la page */
    }
    
    /* =======================================
       MENU - VERSION MOBILE (BASE)
       ======================================= */
    
    .menu-principal {
      background: #2c3e50;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      /* Ombre portée subtile pour effet de profondeur */
    }
    
    .menu-principal ul {
      list-style: none;
    }
    
    .menu-principal li {
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    }
    
    .menu-principal li:last-child {
      border-bottom: none;
    }
    
    .menu-principal a {
      display: block;
      color: white;
      text-decoration: none;
      padding: 15px 20px;
      transition: all 0.3s ease;
      /* "all" = anime toutes les propriétés qui changent */
    }
    
    .menu-principal a:hover,
    .menu-principal a:focus {
      background: #34495e;
      padding-left: 25px; /* Décalage vers la droite au survol sur mobile */
      /* Effet subtil qui indique l'interactivité */
    }
    
    .menu-principal a:active {
      background: #1abc9c;
    }
    
    /* =======================================
       MENU - VERSION DESKTOP
       ======================================= */
    
    @media (min-width: 600px) {
      .menu-principal ul {
        display: flex;
        justify-content: center;
      }
      
      .menu-principal li {
        border-bottom: none;
        border-right: 1px solid rgba(255, 255, 255, 0.1);
      }
      
      .menu-principal li:last-child {
        border-right: none;
      }
      
      .menu-principal a {
        padding: 15px 30px;
      }
      
      .menu-principal a:hover {
        background: #1abc9c;
        padding-left: 30px; /* Annule le décalage mobile */
        transform: translateY(-2px);
        /* Soulève le lien de 2px vers le haut */
      }
      
      .menu-principal a:focus {
        outline: 3px solid #f39c12; /* Contour orange pour focus clavier */
        outline-offset: -3px;       /* Contour à l'intérieur de l'élément */
      }
    }
    
    /* =======================================
       MENU - VERSION LARGE DESKTOP (bonus)
       ======================================= */
    
    @media (min-width: 900px) {
      .menu-principal a {
        padding: 20px 40px; /* Encore plus d'espace sur grand écran */
        font-size: 1.1em;   /* Texte légèrement plus grand */
      }
    }
    
    /* =======================================
       CONTENU DE LA PAGE (pour démonstration)
       ======================================= */
    
    .contenu {
      max-width: 1200px;
      margin: 40px auto;
      padding: 20px;
      background: white;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
    
    .section {
      padding: 60px 20px;
      min-height: 300px; /* Hauteur minimum pour visualiser l'ancrage */
    }
    
    .section h2 {
      color: #2c3e50;
      margin-bottom: 20px;
      border-bottom: 3px solid #1abc9c;
      padding-bottom: 10px;
    }
  </style>
</head>
<body>
  <nav class="menu-principal">
    <ul>
      <li><a href="#accueil">Accueil</a></li>
      <li><a href="#services">Services</a></li>
      <li><a href="#portfolio">Portfolio</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
  
  <div class="contenu">
    <section id="accueil" class="section">
      <h2>Accueil</h2>
      <p>Bienvenue sur notre site. Réduisez et agrandissez la fenêtre pour voir le menu s'adapter automatiquement.</p>
      <p>Sur mobile (< 600px) : menu vertical empilé</p>
      <p>Sur desktop (≥ 600px) : menu horizontal centré</p>
      <p>Sur large desktop (≥ 900px) : menu encore plus spacieux</p>
    </section>
    
    <section id="services" class="section">
      <h2>Services</h2>
      <p>Nos services s'adaptent à vos besoins...</p>
    </section>
    
    <section id="portfolio" class="section">
      <h2>Portfolio</h2>
      <p>Découvrez nos réalisations...</p>
    </section>
    
    <section id="contact" class="section">
      <h2>Contact</h2>
      <p>Contactez-nous pour plus d'informations...</p>
    </section>
  </div>
</body>
</html>
```

### Exercices progressifs pour maîtriser le menu

#### Exercice 1 : Modifier les couleurs (débutant)

**Objectif :** Personnaliser le menu avec votre propre palette de couleurs.

**Consigne :**

1. Changez le fond du menu (`background` de `.menu-principal`)
2. Changez la couleur de survol (`:hover`)
3. Assurez-vous que le texte reste lisible (bon contraste)

**Solution exemple :**
```css
.menu-principal {
  background: #8e44ad; /* Violet */
}

.menu-principal a:hover {
  background: #9b59b6; /* Violet plus clair */
}

.menu-principal a:active {
  background: #3498db; /* Bleu au clic */
}
```

**Astuce pour vérifier le contraste :**
Utilisez un outil comme [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) pour vous assurer que votre texte est lisible par tous, y compris les personnes malvoyantes.

#### Exercice 2 : Ajouter un logo (intermédiaire)

**Objectif :** Intégrer un logo qui reste visible et bien positionné sur toutes les tailles d'écran.

**HTML à ajouter :**
```html
<nav class="menu-principal">
  <div class="logo">MonSite</div>
  <ul>
    <li><a href="#accueil">🏠 Accueil</a></li>
    <!-- ... autres liens ... -->
  </ul>
</nav>
```

**CSS à ajouter :**
```css
.menu-principal {
  display: flex;
  flex-direction: column; /* Logo au-dessus sur mobile */
  align-items: center;
}

.logo {
  color: white;
  font-size: 1.5em;
  font-weight: bold;
  padding: 20px;
  letter-spacing: 2px; /* Espacement entre les lettres */
}

@media (min-width: 600px) {
  .menu-principal {
    flex-direction: row;    /* Logo à gauche sur desktop */
    justify-content: space-between;
    padding: 0 20px;
  }
  
  .logo {
    padding: 15px 0;
  }
  
  .menu-principal ul {
    margin: 0; /* Supprime les marges automatiques */
  }
}
```

**Résultat attendu :**
- Mobile : Logo centré au-dessus du menu
- Desktop : Logo à gauche, menu à droite

#### Exercice 3 : Menu hamburger (avancé)

**Objectif :** Créer un bouton hamburger qui affiche/cache le menu sur mobile.

**Note pédagogique :** Cet exercice nécessite du JavaScript pour la fonctionnalité d'affichage/masquage. Voici une version CSS-only avec la technique de la checkbox cachée.

**HTML modifié :**

```html
<nav class="menu-principal">
  <!-- Checkbox cachée qui contrôle l'état du menu -->
  <input type="checkbox" id="menu-toggle" class="menu-toggle">
  
  <!-- Label qui agit comme bouton hamburger -->
  <label for="menu-toggle" class="menu-icon">
    <span></span>
    <span></span>
    <span></span>
  </label>
  
  <ul class="menu-liste">
    <li><a href="#accueil">🏠 Accueil</a></li>
    <li><a href="#services">💼 Services</a></li>
    <li><a href="#portfolio">🎨 Portfolio</a></li>
    <li><a href="#contact">📧 Contact</a></li>
  </ul>
</nav>
```

**CSS complet avec hamburger :**
```css
/* ===== Cache la checkbox (contrôle masqué) ===== */
.menu-toggle {
  display: none; /* Invisible mais fonctionnel */
}

/* ===== Bouton hamburger (3 barres) ===== */
.menu-icon {
  display: block;          /* Visible sur mobile */
  position: absolute;      /* Positionnement indépendant */
  top: 15px;
  right: 20px;
  cursor: pointer;         /* Indique que c'est cliquable */
  z-index: 1000;          /* Au-dessus de tout */
}

.menu-icon span {
  display: block;
  width: 30px;
  height: 3px;
  background: white;
  margin: 6px 0;
  transition: all 0.3s ease;
  border-radius: 2px;
}

/* ===== Animation du hamburger en X quand actif ===== */
.menu-toggle:checked + .menu-icon span:nth-child(1) {
  transform: rotate(45deg) translate(7px, 7px);
  /* Première barre : rotation et déplacement */
}

.menu-toggle:checked + .menu-icon span:nth-child(2) {
  opacity: 0; /* Barre du milieu disparaît */
}

.menu-toggle:checked + .menu-icon span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -7px);
  /* Troisième barre : rotation inverse */
}

/* ===== Menu liste (caché par défaut sur mobile) ===== */
.menu-liste {
  display: none; /* Caché par défaut */
  list-style: none;
}

/* ===== Affiche le menu quand la checkbox est cochée ===== */
.menu-toggle:checked ~ .menu-liste {
  display: block; /* Affiche le menu */
}

/* ===== Sur desktop : menu toujours visible, hamburger caché ===== */
@media (min-width: 600px) {
  .menu-icon {
    display: none; /* Cache le bouton hamburger */
  }
  
  .menu-liste {
    display: flex !important; /* Force l'affichage en flex */
    /* !important nécessaire pour surcharger le display: none du mobile */
    justify-content: center;
  }
  
  /* ... reste du CSS desktop ... */
}
```

**Comment ça fonctionne :**

1. La checkbox est cachée visuellement mais reste fonctionnelle
2. Le label (bouton hamburger) est lié à la checkbox via l'attribut `for="menu-toggle"`
3. Cliquer sur le label coche/décoche la checkbox
4. Le sélecteur CSS `.menu-toggle:checked ~ .menu-liste` détecte quand la checkbox est cochée
5. Quand cochée, le menu s'affiche (`display: block`)

**Pourquoi cette approche ?**
C'est une technique CSS-only qui fonctionne sans JavaScript, idéale pour comprendre les sélecteurs CSS avancés et les états interactifs.

---

JOURS 2

## 🖼️ Chapitre 4 : Projet pratique - Galerie photos responsive

### Objectif du projet

Créer une galerie photos qui s'adapte intelligemment :
- **Mobile (< 600px)** : 1 photo par ligne (100% de largeur)
- **Tablette (600px - 899px)** : 2 photos par ligne (50% chacune)
- **Desktop (≥ 900px)** : 3 photos par ligne (33.33% chacune)

### Analyse préalable de la structure

Avant de coder, réfléchissons à l'organisation du contenu :

STRUCTURE LOGIQUE :

Galerie (conteneur)
└── Photo 1 (carte)
├── Image
└── Description
└── Photo 2 (carte)
├── Image
└── Description
└── Photo 3 (carte)
...


Chaque photo est une "carte" autonome contenant une image et du texte. Cette modularité facilite l'adaptation responsive.

### Construction pas à pas - Approche mobile-first

#### Étape 1 : HTML sémantique et structuré
```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Galerie Photos Responsive</title>
</head>
<body>
  <div class="conteneur">
    <!-- Titre principal de la galerie -->
    <h1 class="titre-galerie">🖼️ Ma Galerie Photos</h1>
    
    <!-- Conteneur de la galerie -->
    <div class="galerie">
      
      <!-- Carte photo 1 -->
      <article class="photo-carte">
        <img src="https://via.placeholder.com/400x300/3498db/ffffff?text=Montagne" 
             alt="Vue sur les montagnes enneigées">
        <div class="photo-info">
          <h3>Montagne Majestueuse</h3>
          <p>Vue panoramique sur les Alpes au lever du soleil ⛰️</p>
        </div>
      </article>
      
      <!-- Carte photo 2 -->
      <article class="photo-carte">
        <img src="https://via.placeholder.com/400x300/e74c3c/ffffff?text=Coucher+soleil" 
             alt="Coucher de soleil sur l'océan">
        <div class="photo-info">
          <h3>Coucher de Soleil</h3>
          <p>Magnifique coucher de soleil sur la côte atlantique 🌅</p>
        </div>
      </article>
      
      <!-- Carte photo 3 -->
      <article class="photo-carte">
        <img src="https://via.placeholder.com/400x300/2ecc71/ffffff?text=Forêt" 
             alt="Forêt dense et verdoyante">
        <div class="photo-info">
          <h3>Forêt Enchantée</h3>
          <p>Au cœur de la forêt amazonienne luxuriante 🌲</p>
        </div>
      </article>
      
      <!-- Carte photo 4 -->
      <article class="photo-carte">
        <img src="https://via.placeholder.com/400x300/f39c12/ffffff?text=Plage" 
             alt="Plage de sable blanc">
        <div class="photo-info">
          <h3>Plage Paradisiaque</h3>
          <p>Sable blanc et eau turquoise aux Maldives 🏖️</p>
        </div>
      </article>
      
      <!-- Carte photo 5 -->
      <article class="photo-carte">
        <img src="https://via.placeholder.com/400x300/9b59b6/ffffff?text=Ville" 
             alt="Skyline urbain illuminé">
        <div class="photo-info">
          <h3>Ville Moderne</h3>
          <p>Skyline de Tokyo au crépuscule 🌃</p>
        </div>
      </article>
      
      <!-- Carte photo 6 -->
      <article class="photo-carte">
        <img src="https://via.placeholder.com/400x300/1abc9c/ffffff?text=Désert" 
             alt="Dunes de sable doré">
        <div class="photo-info">
          <h3>Désert Mystique</h3>
          <p>Dunes infinies du Sahara au clair de lune 🏜️</p>
        </div>
      </article>
      
    </div>
  </div>
</body>
</html>
```

**Détails sémantiques importants :**

**Balise `<article>` :** Représente un contenu autonome et indépendant. Chaque photo-carte est un article car elle a du sens isolément. Cela améliore le SEO et l'accessibilité.

**Attribut `alt` sur les images :** CRUCIAL pour l'accessibilité. Les lecteurs d'écran lisent ces descriptions aux utilisateurs malvoyants. Décrivez toujours le contenu de l'image, pas juste "image".

**Service placeholder.com :** Génère des images de test avec des dimensions et couleurs personnalisées. Le format est : `placeholder.com/LARGEUR x HAUTEUR/COULEUR_FOND/COULEUR_TEXTE?text=TEXTE`

#### Étape 2 : Styles de base (reset et typographie)
```css
/* =======================================
   RESET ET STYLES GLOBAUX
   ======================================= */

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  /* Dégradé violet pour un fond attractif */
  min-height: 100vh; /* Occupe au moins toute la hauteur de l'écran */
  padding: 20px;
}

.conteneur {
  max-width: 1400px;  /* Limite la largeur sur très grands écrans */
  margin: 0 auto;      /* Centre le conteneur */
  /* margin: 0 auto signifie : 
     - 0 pour haut et bas
     - auto pour gauche et droite (= centrage) */
}

.titre-galerie {
  text-align: center;
  color: white;
  font-size: 2.5em;
  margin-bottom: 40px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  /* Ombre portée sur le texte pour le détacher du fond */
}
```

**Pourquoi `min-height: 100vh` ?**
`vh` signifie "viewport height". `100vh` = 100% de la hauteur de la fenêtre. Cela garantit que le fond dégradé couvre tout l'écran, même si le contenu est court.

**Pourquoi `max-width` avec `margin: 0 auto` ?**
Sur un écran ultra-large (2560px), une galerie de 2560px serait difficilement lisible. On limite à 1400px et on centre pour un meilleur confort visuel.

#### Étape 3 : Styles mobiles de la galerie (base)
```css
/* =======================================
   GALERIE - VERSION MOBILE (BASE)
   ======================================= */

.galerie {
  /* Sur mobile, pas besoin de propriétés spéciales */
  /* Les éléments s'empilent naturellement (comportement block par défaut) */
}

.photo-carte {
  background: white;
  border-radius: 12px;    /* Coins arrondis pour look moderne */
  overflow: hidden;        /* Important ! Cache ce qui dépasse du border-radius */
  /* Sans overflow:hidden, l'image dépasserait des coins arrondis */
  
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  /* Ombre légère pour effet de profondeur */
  
  margin-bottom: 20px;    /* Espace entre chaque carte */
  
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  /* Animation douce pour les interactions */
}

.photo-carte:hover {
  transform: translateY(-5px);  /* Soulève la carte de 5px */
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
  /* Ombre plus prononcée = effet de profondeur accru */
}

.photo-carte img {
  width: 100%;           /* Image prend toute la largeur de la carte */
  height: 250px;         /* Hauteur fixe pour uniformité */
  object-fit: cover;     /* CRUCIAL : recadre l'image sans déformation */
  /* object-fit: cover = remplit l'espace en coupant si nécessaire */
  /* Alternative : object-fit: contain = affiche tout sans couper (peut laisser du vide) */
  
  display: block;        /* Supprime l'espace blanc sous l'image */
  /* Les images sont inline par défaut, ce qui crée un petit espace */
}

.photo-info {
  padding: 20px;         /* Espace autour du texte */
}

.photo-info h3 {
  color: #2c3e50;        /* Gris-bleu foncé */
  margin-bottom: 10px;
  font-size: 1.3em;
}

.photo-info p {
  color: #7f8c8d;        /* Gris moyen pour le texte secondaire */
  font-size: 0.95em;
  line-height: 1.5;
}
```

**Explication détaillée de `object-fit: cover` :**

Imaginez une photo de 800x600px qu'on veut afficher dans un cadre de 400x250px.

**Sans `object-fit`** : L'image serait déformée (écrasée ou étirée)

**Avec `object-fit: cover`** : L'image garde ses proportions, remplit tout l'espace, et coupe ce qui dépasse

**Avec `object-fit: contain`** : L'image garde ses proportions, rentre entièrement, mais peut laisser des bandes vides

ORIGINAL (800x600)        cover (400x250)          contain (400x250)
┌───────────────┐        ┌──────────────┐         ┌──────────────┐
│               │        │[partie]      │         │  ┌────────┐  │
│    PHOTO      │   →    │ visible      │    ou   │  │ PHOTO  │  │
│               │        │   [coupé]    │         │  └────────┘  │
└───────────────┘        └──────────────┘         └──────────────┘
(remplit, coupe)         (tout visible, vide)


#### Étape 4 : Adaptation tablette (2 colonnes)
```css
/* =======================================
   GALERIE - VERSION TABLETTE (2 colonnes)
   ======================================= */

@media (min-width: 600px) {
  .galerie {
    display: flex;         /* Active Flexbox */
    flex-wrap: wrap;       /* Permet aux éléments de passer à la ligne */
    /* Sans flex-wrap, tous les éléments essaieraient de tenir sur une ligne */
    
    gap: 20px;             /* Espace entre les cartes (vertical ET horizontal) */
    /* gap remplace margin et simplifie grandement la gestion des espaces */
  }
  
  .photo-carte {
    width: calc(50% - 10px);  /* 2 colonnes avec espace */
    /* Calcul : 50% de largeur moins la moitié du gap (20px / 2 = 10px) */
    /* Pourquoi -10px ? Le gap de 20px est partagé entre 2 éléments (10px chacun) */
    
    margin-bottom: 0;      /* Supprime la marge, le gap suffit */
  }
  
  .photo-carte img {
    height: 220px;         /* Légèrement plus petit sur tablette */
    /* Optimise l'affichage pour 2 colonnes */
  }
}
```

**Visualisation du calcul de largeur :**

CONTENEUR (600px de large)
┌──────────────────────────────────────────────────────┐
│  CARTE 1 (285px)    GAP(20px)    CARTE 2 (285px)     │
│  ┌───────────────┐               ┌───────────────┐   │
│  │               │               │               │   │
│  │     PHOTO     │               │     PHOTO     │   │
│  │               │               │               │   │
│  └───────────────┘               └───────────────┘   │
└──────────────────────────────────────────────────────┘

CALCUL :
Largeur totale = 600px
Gap = 20px
Espace disponible pour les cartes = 600px - 20px = 580px
Chaque carte = 580px / 2 = 290px

EN CSS :
width: calc(50% - 10px)
= calc(300px - 10px)  [50% de 600px]
= 290px ✓

**Pourquoi `flex-wrap: wrap` est essentiel :**

Sans cette propriété, Flexbox essaie de tout mettre sur une ligne, réduisant la largeur des éléments jusqu'à ce qu'ils tiennent tous. 
Avec ``flex-wrap: wrap``, les éléments passent naturellement à la ligne suivante quand il n'y a plus de place.

```css
/* SANS flex-wrap */
┌────┬────┬────┬────┬────┬────┐
│ 1  │ 2  │ 3  │ 4  │ 5  │ 6  │  ← Tous écrasés sur une ligne
└────┴────┴────┴────┴────┴────┘

/* AVEC flex-wrap: wrap */
┌─────────┬─────────┐
│    1    │    2    │  ← Première ligne
├─────────┼─────────┤
│    3    │    4    │  ← Passe automatiquement à la ligne
├─────────┼─────────┤
│    5    │    6    │
└─────────┴─────────┘
```

#### Étape 5 : Adaptation desktop (3 colonnes)

```css
/* =======================================
   GALERIE - VERSION DESKTOP (3 colonnes)
   ======================================= */

@media (min-width: 900px) {
  .galerie {
    gap: 25px;             /* Augmente l'espace entre les cartes */
    /* Plus d'écran = plus d'air, interface plus aérée */
  }
  
  .photo-carte {
    width: calc(33.333% - 17px);  /* 3 colonnes avec espace */
    /* Calcul : 33.333% de largeur moins une portion du gap */
    /* 25px de gap partagé entre 3 éléments ≈ 17px par élément */
  }
  
  .photo-carte img {
    height: 250px;         /* Hauteur standard pour desktop */
  }
  
  /* Effet hover plus prononcé sur desktop */
  .photo-carte:hover {
    transform: translateY(-8px) scale(1.02);
    /* Soulève de 8px ET agrandit légèrement (102%) */
    box-shadow: 0 12px 20px rgba(0, 0, 0, 0.3);
    /* Ombre encore plus marquée */
  }
}
```

**Comprendre le calcul pour 3 colonnes :**

```css
CONTENEUR (1200px de large)
┌──────────────────────────────────────────────────────────────────────┐
│  CARTE 1      GAP     CARTE 2      GAP      CARTE 3                  │
│  ┌─────────┐   25px   ┌─────────┐   25px   ┌─────────┐              │
│  │  PHOTO  │          │  PHOTO  │          │  PHOTO  │              │
│  └─────────┘          └─────────┘          └─────────┘              │
│   383px                383px                383px                    │
└──────────────────────────────────────────────────────────────────────┘

CALCUL DÉTAILLÉ :
Largeur totale = 1200px
Gaps totaux = 25px × 2 = 50px (deux gaps entre trois éléments)
Espace pour cartes = 1200px - 50px = 1150px
Chaque carte = 1150px / 3 ≈ 383px

EN CSS (approximation) :
33.333% de 1200px = 400px
400px - 17px ≈ 383px ✓
```

**Alternative avec gap seul (plus simple) :**

```css
.photo-carte {
  width: calc((100% - 50px) / 3);
  /* 100% - (2 gaps de 25px) divisé par 3 colonnes */, flex-shrink, flex-basis */
}
```


