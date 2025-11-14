---
title: "CSS2 Media Queries : les fondations"
export_on_save:
  html: true
  toc: true
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
[codepen link](https://codepen.io/b3no1t/pen/LENpyKM)

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

[codepen link](https://codepen.io/b3no1t/pen/wBGKzGj)

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

>Happy coding !
