---
title: Création de page à partir de fragments de contenu
seo-title: Création de page à partir de fragments de contenu
description: Les fragments de contenu d’AEM vous permettent de concevoir, de créer, d’organiser et d’utiliser du contenu indépendant des pages
seo-description: Les fragments de contenu d’AEM vous permettent de concevoir, de créer, d’organiser et d’utiliser du contenu indépendant des pages
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
translation-type: tm+mt
source-git-commit: 74f259d579bcf8d7a9198f93ef667288787a4493
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 100%

---


# Création de page à partir de fragments de contenu{#page-authoring-with-content-fragments}

Les fragments de contenu Adobe Experience Manager (AEM) sont [créés et gérés en tant que ressources indépendantes de la page](/help/assets/content-fragments/content-fragments.md).

Ils vous permettent de créer du contenu compatible avec tous les canaux, ainsi que des variations (éventuellement spécifiques aux canaux). Vous pouvez ensuite utiliser ces fragments et leurs variantes lors de la création de vos pages de contenu.

En même temps que l’outil d’exportation JSON mis à jour, les fragments de contenu structuré peuvent également être utilisés pour diffuser du contenu AEM via Content Services à des canaux autres que des pages AEM.

>[!NOTE]
>
>Les **fragments de contenu** et les **[fragments d’expérience](/help/sites-authoring/experience-fragments.md)** représentent deux fonctions distinctes d’AEM :
>
>* Les **fragments de contenu** sont des contenus éditoriaux, composés essentiellement de texte et des images associées. Il s’agit exclusivement de contenu, sans aucun élément de conception ni de mise en page.
>* Les **fragments d’expérience** désignent un contenu parfaitement mis en page : un fragment de page web.

>
>
Les fragments d’expérience peuvent être composés de contenu sous la forme de fragments de contenu, mais pas l’inverse.

>[!CAUTION]
>
>Cette page doit être consultée en complément de la page [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md) (et des pages annexes), car elle présente la terminologie et les concepts de base, ainsi que la création et la gestion de fragments.

Grâce aux fragments de contenu :

* **Stratégie de marketing et de campagne**

   * Examen du contenu via des fragments de contenu gérés de manière centralisée.

* **Designer pro**

   * Suivi des ressources de création via les collections associées à des fragments de contenu.

* **Rédacteurs**

   * Rédigent dans l’éditeur de fragment de contenu d’AEM.
   * Peuvent créer des variantes de contenu.
   * Peuvent associer du contenu pertinent à un fragment de contenu.
   * Peuvent utiliser la création de version/les workflows.
   * Peuvent partager un fragment de contenu.
   * Peuvent gérer les traductions de manière centralisée.

* **Producteurs et responsable parcours**

   * Font leur choix parmi des fragments et des variations prédéfinis pour créer du contenu dans AEM.
   * Peuvent compter sur une actualisation continue des fragments et du contenu associé à mesure que les rédacteurs et les designers modifient les fragments et les ressources gérés de manière centralisée.
   * Peuvent se fier à du contenu multimédia associé toujours pertinent.
   * Peuvent créer des variations de contenu ad hoc à la volée tout en garantissant leur gestion centralisée dans le fragment.

## Ajout d’un fragment de contenu à une page   {#adding-a-content-fragment-to-your-page}

1. Ouvrez la page à modifier.

1. Ajoutez le composant **Fragment de contenu** à partir du navigateur **Composants** ou **Insérer un nouveau composant**.

1. Vous pouvez effectuer l’une des actions suivantes :

   * Ouvrir l’explorateur de **ressources** et filtrer sur **Fragments de contenu** (la valeur par défaut est Images). Faites ensuite glisser le fragment en question sur l’instance du composant.

   * Sélectionner le composant de fragment de contenu, puis **Configurer** dans la barre d’outils. Dans la boîte de dialogue, vous pouvez ouvrir la boîte de dialogue de sélection afin de rechercher et de sélectionner le **fragment de contenu** requis.
   >[!NOTE]
   >
   >L’autre méthode consiste à faire glisser un fragment de contenu directement sur la page. Le composant associé est ainsi automatiquement créé (Fragment de contenu).

1. Au début, le contenu des éléments **Principal** et **Maître** (variation) est affiché. Vous pouvez [sélectionner d’autres éléments et/ou variantes](#selecting-the-element-or-variation) en fonction de vos besoins.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Pour plus d’informations sur les autres fonctionnalités d’édition, voir aussi :
   >
   >
   >
   >    * [Mise en page réactive](/help/sites-authoring/responsive-layout.md)
   >    * [Modification du contenu de la page](/help/sites-authoring/editing-content.md)


### Sélection de l’élément ou de la variation {#selecting-the-element-or-variation}

Ouvrez la boîte de dialogue **Configuration** du fragment pour configurer le fragment à utiliser dans la page active. La boîte de dialogue peut dépendre du composant utilisé.

Dans la boîte de dialogue de configuration appropriée, vous pouvez sélectionner les paramètres disponibles, parmi lesquels :

* **Fragment de contenu**

   Spécifiez le fragment à utiliser.

* **Mode d’affichage** :

   * **Un seul élément texte**

   * **Plusieurs éléments**

* **Élément**

   * Le type **Principal** par défaut est toujours disponible.
   * Une sélection est disponible si le fragment a été créé avec le modèle approprié.

   >[!NOTE]
   >
   >Les éléments disponibles dépendent du modèle utilisé.

* **Variation**

   * Le **maître** par défaut sera toujours disponible.
   * Une sélection est disponible si des variations ont été créées pour le fragment.

* **Paragraphes** : indiquez la plage de paragraphes à inclure :

   * **Tous**
   * **Plage** : par exemple, `1`, `3-5`, `9-*`

      * **Gérer les en-têtes comme leurs propres paragraphes**

* **Gérer les en-têtes comme leurs propres paragraphes**

### Connexion rapide à l’éditeur de fragment    {#quick-connection-to-fragment-editor}

Vous pouvez ouvrir la source du fragment à modifier (la ressource) à l’aide de l’icône **Modifier** située dans la barre d’outils du composant. Vous pourrez ainsi [modifier et gérer le fragment de contenu](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Comme toujours, la modification de la source du fragment affectera toutes les pages qui font référence à ce fragment de contenu.

### Ajout de contenu intermédiaire    {#adding-in-between-content}

Lorsqu’un fragment de contenu particulier est ajouté à la page, un espace réservé **Faire glisser les composants ici** est présent entre chaque paragraphe HTML (en haut/en bas) du fragment.

Cela permet d’ajouter du contenu supplémentaire [à l’intérieur (c’est-à-dire au niveau intermédiaire)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) du contenu du fragment (au niveau de tout point disponible), sans avoir à modifier le fragment racine.

Dans le cas du contenu intermédiaire, plusieurs possibilités vous sont offertes :

* Ajouter des composants à partir de l’[explorateur de composants](/help/sites-authoring/author-environment-tools.md#components-browser).
* Ajouter des ressources à partir de l’[explorateur de ressources](/help/sites-authoring/author-environment-tools.md#assets-browser).
* Utiliser du [contenu associé](#using-associated-content) comme source de contenu intermédiaire.

>[!CAUTION]
>
>Le contenu intermédiaire est du contenu de page. Il n’est pas stocké dans le fragment de contenu.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>Vous pouvez également [insérer des ressources visuelles (images) dans le fragment proprement dit](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Les ressources visuelles insérées dans le fragment sont liées au paragraphe précédent dans le fragment. Cela signifie que vous ne pouvez pas placer le contenu intermédiaire entre une ressource visuelle et le paragraphe précédent.

>[!CAUTION]
>
>Une fois le contenu intermédiaire ajouté à un fragment de votre page, la modification de la structure du fragment de contenu sous-jacent (c’est-à-dire dans l’éditeur de fragment de contenu) risque de donner lieu à des résultats erronés/inattendus.
>
>Si cela se produit, le contenu intermédiaire est conservé tel quel :
>
>* Les composants intermédiaires occupent une position absolue dans la séquence de composants du flux de fragments. Cette position ne varie pas, même en cas de modification du contenu des paragraphes dans le fragment.
>
>  
Cela peut donner l’impression que le positionnement relatif a changé, dans la mesure où les paragraphes intermédiaires n’ont aucune relation contextuelle avec les paragraphes (de fragment) près desquels ils sont placés.
>* À moins que ces deux structures de paragraphes ne soient en conflit ; dans ce cas, le contenu intermédiaire n’est pas affiché (bien qu’il soit toujours présent en interne).

>



### Utilisation de contenu associé    {#using-associated-content}

Si vous avez [associé du contenu](/help/assets/content-fragments/content-fragments-assoc-content.md) au [fragment de contenu](/help/assets/content-fragments/content-fragments.md), ces ressources seront disponibles à partir du panneau latéral (après avoir placé le fragment sur la page de contenu). Le contenu associé est en fait une source spéciale de contenu pour le [contenu intermédiaire](#adding-in-between-content).

>[!NOTE]
>
>Différentes méthodes permettent d’ajouter des [ressources visuelles (des images, par exemple)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) au fragment et/ou à la page.

>[!NOTE]
>
>Si plusieurs fragments de contenu sont présents dans une page, l’onglet **Contenu associé** présente les ressources associées à tous les fragments.

Une fois que vous avez ajouté un fragment avec du contenu associé à votre page, un nouvel onglet (**Contenu associé**) est ouvert dans le panneau latéral.

Dans cet onglet, vous pouvez faire glisser les ressources vers l’emplacement souhaité (un composant existant ou une position où le composant adéquat sera créé) :

![cfm-6420-03](assets/cfm-6420-03.png)

### Ressources insérées dans le fragment {#assets-inserted-into-the-fragment}

Si des ressources (des images, par exemple) ont été insérées dans le fragment proprement dit, les options permettant de les modifier dans l’éditeur de page sont limitées.  <!-- Removed link as it was a 404 on helpx -->

Dans le cas d’une image, par exemple, vous pouvez effectuer les opérations suivantes :

* Recadrer, faire pivoter ou retourner l’image.
* Ajouter un titre ou un texte secondaire.
* Spécifier une taille.
* Vous pouvez également configurer la mise en page.

Les autres modifications (déplacement, copie, suppression, etc.) doivent être effectuées dans l’éditeur de fragment.

### Publication {#publishing}

Les fragments doivent être publiés pour pouvoir être utilisés dans les pages web que vous avez publiées :

* Un fragment peut être publié une fois [qu’il a été créé dans la console Ressources](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment).
* Si un *fragment non publié* est utilisé dans une page en cours de publication, le fragment peut également être publié à ce moment.

