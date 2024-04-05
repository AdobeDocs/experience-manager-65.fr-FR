---
title: Mapper des données de composant à des propriétés Adobe Analytics
description: Découvrez comment mapper les données de composant avec les propriétés de SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 100%

---

# Mapper des données de composant à des propriétés Adobe Analytics{#mapping-component-data-with-adobe-analytics-properties}

Ajoutez à la structure des composants qui rassemblent les données à envoyer à Adobe Analytics. Les composants conçus pour collecter des données d’analyse stockent les données dans la **variable CQ** appropriée. Lorsque vous ajoutez ce type de composant à un framework, celle-ci affiche la liste des variables CQ afin que vous puissiez associer chacune d’elles à la **variable Analytics** appropriée.

![aa-11](assets/aa-11.png)

Lorsque la **vue AEM** est ouverte, les variables Analytics s’affichent dans l’outil de recherche de contenu.

![aa-12](assets/aa-12.png)

Vous pouvez associer plusieurs variables Analytics à une même **variable CQ**.

![chlimage_1-68](assets/chlimage_1-68.png)

Les données mappées sont envoyées vers Adobe Analytics lorsque la page se charge et que les conditions ci-dessous sont remplies :

* La page est associée au framework.
* La page utilise les composants ajoutés au framework.

Appliquez la procédure ci-dessous pour mapper des variables de composants CQ à des propriétés de rapport Adobe Analytics.

1. Dans la **vue AEM**, faites glisser un composant de suivi du sidekick vers le framework. Par exemple, faites glisser le composant **Page** à partir de la catégorie **Général**.

   ![aa-13](assets/aa-13.png)

   Il existe différents groupes de composants par défaut : **Général**, **Commerce**, **Communities**, et **Autre**. Votre instance AEM peut être configurée de manière à afficher différents groupes et composants.

1. Pour mapper des variables Adobe Analytics à des variables définies dans le composant, faites glisser une **variable Analytics** de l’outil de recherche de contenu vers un champ du composant de suivi. Par exemple, faites glisser `Page Name (pageName)` vers `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >L’identifiant de suite de rapports (RSID) sélectionné pour le framework détermine les variables Adobe Analytics qui s’affichent dans l’outil de recherche de contenu.

1. Répétez les deux étapes précédentes pour les autres composants et variables.

   >[!NOTE]
   >
   >Vous pouvez mapper plusieurs variables Analytics (par exemple, `props`, `eVars`, `events`) à une même variable CQ (par exemple, `pagedata.title`).

   >[!CAUTION]
   >
   >Il est vivement recommandé de suivre les indications suivantes :
   >
   >* Les `eVars` et les `props` sont mappées à des variables CQ commençant par `pagedata.X` ou `eventdata.X`,
   >* tandis que les événements doivent être mappés à des variables commençant par `eventdata.events.X`.

1. Pour rendre le framework disponible sur l’instance de publication de votre site, affichez l’onglet **Page** du sidekick et cliquez sur **Activer le cadre.**

## Mappage de variables liées à des produits {#mapping-product-related-variables}

AEM utilise une convention pour nommer les variables liées à des produits et à des événements censés être mappés à des propriétés liées à des produits Adobe Analytics :

| Variable CQ | Variable Analytics | Description |
|--- |--- |--- |
| `product.category` | `product.category` (variable de conversion) | Catégorie de produits. |
| `product.sku` | `product.sku` (variable de conversion) | SKU du produit. |
| `product.quantity` | `product.quantity` (variable de conversion) | Nombre de produits achetés. |
| `product.price` | `product.price` (variable de conversion) | Prix du produit. |
| `product.events.<eventName>` | Événements de succès à associer au produit dans votre rapport. | `product.events` est le préfixe des événements appelés *eventName*. |
| `product.evars.<eVarName>` | Variable(s) de conversion (`eVar`) à associer au produit. | `product.evars` est le préfixe des variables eVar appelées *eVarName*. |

Plusieurs composants d’AEM Commerce utilisent ces noms de variables.

>[!NOTE]
>
>Ne mappez pas la propriété Products Adobe Analytics à une variable CQ. La configuration de mappages liés à un produit, comme indiqué dans le tableau, s’apparente au mappage de la variable Products.

### Vérification des rapports dans Adobe Analytics {#checking-reports-on-adobe-analytics}

1. Connectez-vous au site Web d’Adobe Analytics à l’aide des informations d’identification fournies dans AEM.
1. Assurez-vous que le RSID sélectionné est celui utilisé lors des étapes précédentes.
1. Dans **Rapports** (dans la partie gauche de la page), sélectionnez **Conversion personnalisée**, puis **Conversion personnalisée 1-10** et sélectionnez la variable correspondant à `eVar7`.

1. En fonction de la version d’Adobe Analytics que vous utilisez, vous devez attendre 45 minutes, en moyenne, pour que le rapport soit mis à jour avec le terme recherché utilisé (« aubergine » dans l’exemple).

## Utilisation de l’outil de recherche de contenu (cf#) avec les frameworks Adobe Analytics {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

Au départ, lorsque vous ouvrez un framework Adobe Analytics, l’outil de recherche de contenu contient des variables Analytics prédéfinies sous :

* Trafic
* Conversion
* Événements

Lorsqu’un RSID est sélectionné, toutes les variables appartenant à ce RSID sont ajoutées à la liste.\
L’élément `cf#` est nécessaire pour mapper des variables Analytics aux variables CQ présentes dans les différents composants de suivi. Consultez Configuration d’un framework pour le suivi de base.

En fonction de la vue sélectionnée pour le framework, l’outil de recherche de contenu est renseigné par des variables Analytics (dans la vue AEM) ou des variables CQ (dans la vue Analytics).

Vous pouvez effectuer plusieurs opérations sur la liste :

1. Dans la **vue AEM**, la liste peut être filtrée en fonction du type de variable sélectionné à l’aide des trois boutons de filtrage :

   * Si *aucun bouton* n’est sélectionné, la liste complète s’affiche.
   * Si vous sélectionnez le bouton **Trafic**, seules les variables appartenant à la section Trafic sont répertoriées dans la liste..
   * Si vous sélectionnez le bouton **Conversion**, seules les variables appartenant à la section Conversion sont répertoriées dans la liste.
   * Si vous sélectionnez le bouton **Événéments**, la liste n’affiche que les variables qui appartiennent à la section Événements.

   >[!NOTE]
   >
   >Un seul bouton de filtre peut être actif à la fois.

   1. La liste comporte également une fonction de recherche qui filtre les éléments en fonction du texte saisi dans le champ de recherche.
   1. Si vous activez une option de filtrage lors de la recherche d’éléments dans la liste, les résultats affichés seront également filtrés en fonction du bouton actif.
   1. Vous pouvez recharger la liste à tout moment à l’aide du bouton en forme de flèche.
   1. Si vous sélectionnez plusieurs RSID dans le framework, toutes les variables de la liste s’affichent à l’aide de toutes les étiquettes utilisées dans les RSID sélectionnés.

1. Dans la vue Adobe Analytics, l’outil de recherche de contenu répertorie toutes les variables CQ appartenant aux composants de suivi que vous faites glisser dans la vue CQ.

   * Par exemple, si le **composant Téléchargement** est le *seul composant déplacé* dans la vue CQ (qui comporte deux variables mappables, *eventdata.downloadLink* et *eventdata.events.startDownload*), l’outil de recherche de contenu se présente comme suit lorsque vous passez à la vue Adobe Analytics :

   ![aa-22](assets/aa-22.png)

   * Vous pouvez faire glisser les variables et les déposer sur une variable Adobe Analytics appartenant à l’une des trois sections de variables (**Trafic**, **Conversion** et **Événements**).

   * Lorsque vous faites glisser un nouveau composant de suivi sur le framework dans la vue CQ, les variables CQ appartenant au composant sont ajoutées automatiquement à l’outil de recherche de contenu (cf#) dans la vue Adobe Analytics.

   >[!NOTE]
   >
   >Une seule variable CQ peut être mappée à une variable Adobe Analytics à un moment donné.

## Utilisation de la vue AEM et de la vue Analytics {#using-aem-view-and-analytics-view}

À tout moment, les utilisateurs et les utilisatrices peuvent alterner entre les deux vues des mappages Adobe Analytics sur une page du framework. Les deux vues offrent une bonne présentation des mappages dans le framework, de deux points de vue différents.

### Vue AEM {#aem-view}

![aa-23](assets/aa-23.png)

En prenant comme exemple l’image ci-dessus, la **vue AEM** possède les propriétés suivantes :

1. Il s’agit de la vue par défaut à l’ouverture du framework.
1. Sur la gauche de l’écran : l’outil de recherche de contenu (cf#) est renseigné par des variables Adobe Analytics en fonction des RSID sélectionnés.
1. En-têtes d’onglets (**vue AEM** et **vue Analytics**) : à utiliser pour basculer entre les vues.

1. **Vue AEM** :

   1. Si le framework comporte des composants hérités de son parent, ils sont répertoriés ici, ainsi que les variables mappées aux composants.

      1. Les composants hérités sont verrouillés.
      1. Pour déverrouiller un composant hérité, double-cliquez sur le cadenas à côté de son nom.
      1. Pour rétablir l’héritage, supprimez le composant déverrouillé, qui retrouvera son statut verrouillé.

   1. **Faire glisser des composants ici pour les inclure dans le framework Analytics** : vous pouvez faire glisser les composants à partir du sidekick et les déposer ici.
   1. Vous trouverez tous les composants actuellement inclus dans le framework Analytics :

      1. Pour ajouter un composant, faites-le glisser depuis l’onglet Composants du sidekick.
      1. Pour supprimer un composant et tous ses mappages, sélectionnez Supprimer dans le menu contextuel correspondant, puis acceptez la suppression dans la boîte de dialogue de confirmation.
      1. Gardez à l’esprit qu’un composant ne peut être supprimé que du framework dans lequel il a été créé et ne peut pas être supprimé des frameworks enfants au sens traditionnel du terme (ils ne peuvent être que remplacés).

### Vue Analytics {#analytics-view}

![aa-24](assets/aa-24.png)

1. Cette vue est accessible en cliquant sur l’onglet **vue Analytics** du framework.
1. Côté gauche : outil de recherche de contenu (cf#) renseigné par des variables CQ en fonction des composants déplacés sur le framework dans la vue CQ.
1. En-têtes d’onglets (**vue AEM** et **vue Analytics**) : à utiliser pour basculer entre les vues.

1. Les trois tableaux (Trafic, Conversion, Événement) répertorient toutes les variables Adobe Analytics disponibles des RSID sélectionnés. Les mappages affichés ici doivent être identiques à ceux de la vue AEM :

   * **Trafic** :

      * Variable de trafic (`prop1`) mappée à une variable CQ (`eventdata.downloadLink`)

      * Lorsque le composant est accompagné d’un cadenas, cela signifie qu’il est hérité d’un framework parent et ne peut donc pas être modifié.

   * **Conversion** :

      * Variable de conversion (`eVar1`) mappée à une variable CQ (`pagedata.title`)

      * La variable de conversion (`eVar3`) est mappée à une expression JavaScript ajoutée en ligne en double-cliquant sur le champ Variable CQ et en saisissant manuellement le code.

   * **Événement** :

      * Variable d’événement (`event1`) mappée à un événement CQ (`eventdata.events.pageView`)

>[!NOTE]
>
>La colonne Variable CQ de chaque table peut également être renseignée en ligne en double-cliquant sur le champ et en ajoutant du texte. Ces champs acceptent JavaScript comme entrée.
>
>Par exemple, à côté de `prop3`, vous pouvez ajouter :
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
>pour envoyer la variable *title* d’une page concaténé avec sa variable *sitesection* à l’aide d’un *:* (deux-points) et précédé du préfixe *Adobe* en tant que `prop3`.
>

>[!CAUTION]
>
>Une seule variable CQ peut être mappée à une variable Adobe Analytics à un moment donné.
