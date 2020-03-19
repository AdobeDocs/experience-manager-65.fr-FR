---
title: Guide de composants de communauté
seo-title: Guide de composants de communauté
description: Un outil de développement interactif pour commencer avec le cadre des composants sociaux (SCF)
seo-description: Un outil de développement interactif pour commencer avec le cadre des composants sociaux (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
translation-type: tm+mt
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# Guide de composants de communauté  {#community-components-guide}

Le guide Composants communautaires est un outil de développement interactif pour le cadre des composantes [sociales (SCF)](scf.md). Il fournit un  des composants de communautés AEM disponibles ou des fonctionnalités plus complexes créées à partir de plusieurs composants.

En plus des informations de base pour chaque composant, le guide permet d&#39;expérimenter le fonctionnement des composants/fonctionnalités SCF et la manière dont ils peuvent être configurés ou personnalisés.

Pour plus d’informations sur les fondamentaux de développement relatifs à chaque composant, voir [Fonctionnalités et composants essentiels](essentials.md).

## Prise en main {#getting-started}

Ce guide est destiné aux installations de développement des instances d’auteur (localhost:4502) et de publication (localhost:4503).

Pour accéder au site Composants de la communauté, accédez à

* [https://&lt;serveur>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Les interactions avec les composantes des communautés varient selon les éléments suivants :

* Le serveur (auteur ou publication)
* Indique si le du site est connecté ou non
* Si vous êtes connecté, les privilèges attribués au membre
* Indique si le SRP par défaut, [JSRP](jsrp.md), est utilisé ou non

Sur l’auteur, pour passer en mode d’édition, insérez soit `editor.html` , soit `cf#` comme premier segment de chemin après le nom du serveur :

* Interface utilisateur standard:

   [https://&lt;serveur>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* IU classique :

   [https://&lt;serveur>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>En mode d’édition, les liens d’une page ne sont pas actifs.
>
>Pour accéder à une page de composant, sélectionnez tout d’abord le mode  pour activer les liens.
>
>La page de composant s’affichant dans le navigateur, revenez en mode d’édition afin d’ouvrir la boîte de dialogue de modification du composant.
>
>For general authoring information, view the [quick guide to authoring pages](../../help/sites-authoring/qg-page-authoring.md).
>
>If not familiar with AEM, view the documentation on [basic handling](../../help/sites-authoring/basic-handling.md).

### Page d’accueil {#home-page}

Le guide fournit une liste des composants SCF disponibles pour les  de et le prototypage le long du côté gauche de la page.

Guide des composants affiché sur une instance d’auteur en mode d’édition :

![chlimage_1-404](assets/chlimage_1-404.png)

## Pages de composants {#component-pages}

Sélectionnez un composant dans le  le long du côté gauche de la page.

![chlimage_1-405](assets/chlimage_1-405.png)

Le corps principal du guide s’affiche :

1. Titre : Nom du composant sélectionné
1. [Bibliothèques](#client-side-libraries)côté client :  d’un ou de plusieurs requis 
1. [Inclus](scf.md#add-or-include-a-communities-component): Si le composant peut être inclus dynamiquement, l’état peut être basculé en mode d’édition Auteur :

   * Si vous l’ajoutez, le texte affiché est le suivant : &quot;Ce composant est inclus via son noeud par.&quot;
   * S’il est inclus, le texte affiché est le suivant : &quot;Ce composant est inclus dynamiquement.&quot;
   * Si ce n’est pas le cas, aucun texte n’est affiché.

1. Exemple de composant ou de fonction : instance active du composant ou de la fonction. Si un composant est modifié, il peut l’être avec les modifications apportées aux modèles, aux feuilles de style CSS et aux données fournies dans la section d’onglet.

>[!NOTE]
>
>Après avoir effectué une sélection à gauche, le composant apparaît en dessous, plutôt qu’à côté, de la liste des composants lorsque la fenêtre du navigateur est trop étroite.

### Interactions Auteur {#author-interactions}

Lors de l’utilisation du guide sur une instance d’auteur, il est possible de configurer un composant en ouvrant sa boîte de dialogue. Les informations destinées aux développeurs sont fournies dans la section Essentials [des](essentials.md) composants et des fonctionnalités de la documentation, tandis que les paramètres des boîtes de dialogue sont décrits dans la section Composants [des](author-communities.md) communautés pour les auteurs.

Pour le guide Composants de la communauté, certains paramètres de la boîte de dialogue des composants sont superposés avec l’état de bascule [Incluable](scf.md#add-or-include-a-communities-component) . Pour basculer entre l’utilisation de la ressource existante ou d’une ressource incluse dynamiquement, en mode d’édition, sélectionnez le composant et le texte inclus, puis -cliquez pour ouvrir la boîte de dialogue de modification :

![chlimage_1-406](assets/chlimage_1-406.png)

Sous l’onglet **Modèles** :

![chlimage_1-407](assets/chlimage_1-407.png)

* **Inclure le composant enfant avec sling:include**

   Si cette option n’est pas cochée, le Guide des composants utilise la ressource existante dans le référentiel (un noeud jcr qui est un enfant d’un noeud par).

   * le texte affiché est : &quot;Ce composant est inclus via son noeud par.&quot;
   Si cette option est cochée, le Guide des composants utilise sling pour inclure de manière dynamique un composant de la ressourceType du noeud enfant (ressource non existante).

   * le texte affiché est : &quot;Ce composant est inclus dynamiquement.&quot;
   Cette option n’est pas cochée par défaut.

### Interactions de publication {#publish-interactions}

Lors de l’utilisation du guide sur une instance de publication, il est possible d’expérimenter les composants et fonctionnalités en tant que de site (non connecté) et membres disposant de divers privilèges lors de leur connexion.

>[!NOTE]
>
>Sachez que si le SRP est laissé par défaut à [JSRP](jsrp.md), l’UGC saisi sur l’instance de publication est uniquement visible lors de la publication et *non* visible à partir de la console de [modération](moderate-ugc.md) de l’instance d’auteur.

## Bibliothèques côté client {#client-side-libraries}

Les bibliothèques côté client (clientlibs) répertoriées pour chaque composant sont celles *requises* pour être référencées lorsque le composant est placé sur une page. Les clientlibs fournissent un moyen de gérer et d’optimiser le téléchargement du code JavaScript et CSS utilisé pour rendre le composant dans le navigateur.

Pour plus d’informations, consultez [Clientlibs for Communities Components](clientlibs.md)(en anglais).

## Emprunt d’identité {#impersonation}

Dans l’instance d’auteur, où l’un d’eux est souvent connecté en tant qu’administrateur ou développeur, pour expérimenter le composant connecté en tant qu’autre utilisateur, utilisez la zone de texte à gauche du bouton **[!UICONTROL d’emprunt d’identité]** pour saisir le nom d’utilisateur ou effectuez une sélection dans le déroulant, puis cliquez sur le bouton. Cliquez sur Rétablir pour vous déconnecter et mettre fin à l’emprunt d’identité.

L’instance de publication n’a pas besoin de s’incarner. Il vous suffit d’utiliser le lien Connexion/Déconnexion pour vous faire passer pour des utilisateurs variés, tels que les utilisateurs [de la](tutorials.md#demo-users)démonstration.

## Personnalisation {#customization}

Une fois activé, chaque composant SCF est disponible pour le prototypage d’éventuelles personnalisations en modifiant temporairement le modèle, le CSS et les données du composant.

### Activation de la personnalisation {#enabling-customization}

>[!NOTE]
>
>**Cet outil est en lecture seule**. Aucune des modifications apportées aux modèles, aux pages CSS ou aux données n’est enregistrée dans le référentiel.

Pour tester rapidement les personnalisations, la `scg:showIde`propriété doit être ajoutée au noeud JCR de contenu de la page de composant et définie sur true.

Utilisation du composant de commentaires comme exemple, sur l’instance d’auteur ou de publication, connecté avec des droits d’administrateur :

1. Accédez à [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   For example, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Sélectionnez le `jcr:content` noeud du composant

   Par exemple, `/content/community-components/en/comments/jcr:content`

1. Ajouter une propriété

   * **Nom** `scg:showIde`
   * **Type** `String`
   * **Valeur** `true`

1. Select **[!UICONTROL Save All]**
1. Rechargement de la page Commentaires dans le guide

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Notez qu’il existe maintenant 3 onglets pour les modèles, CSS et Data.

![chlimage_1-408](assets/chlimage_1-408.png) ![chlimage_1-409](assets/chlimage_1-409.png)

### Onglet Modèles {#templates-tab}

Sélectionnez l’onglet Modèles pour afficher les modèles associés au composant.

L’éditeur de modèles permet de compiler et d’appliquer les modifications locales à l’instance de composant exemple en haut de la page sans affecter le composant dans le référentiel.

L’exécution de la compilation sur les modifications locales met en évidence les erreurs en plaçant un point dans la gouttière et en marquant le texte en rouge.

### Onglet CSS {#css-tab}

Sélectionnez l’onglet CSS pour afficher le fichier CSS associé au composant.

Si un composant est un composite de plusieurs composants, certaines feuilles de style CSS peuvent être répertoriées sous l’un des autres composants.

L’éditeur CSS permet de modifier la page CSS et de l’appliquer à l’exemple d’instance de composant en haut de la page.

Une règle peut être sélectionnée pour mettre en surbrillance les parties du DOM à l’aide de cette règle en cliquant sur en regard de la règle dans la gouttière.

### Onglet Données {#data-tab}

Sélectionnez l’onglet Données pour afficher les données du point de fin .social.json. Ces données sont modifiables et appliquées à l’instance de composant exemple.

Les erreurs de syntaxe peuvent être marquées dans la gouttière et mises en évidence dans l’éditeur.
