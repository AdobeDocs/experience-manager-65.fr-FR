---
title: Personnaliser les consoles
seo-title: Customizing the Consoles
description: AEM fournit divers mécanismes pour vous permettre de personnaliser les consoles de votre instance de création
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 44%

---

# Personnaliser les consoles {#customizing-the-consoles}

>[!CAUTION]
>
>Ce document décrit comment personnaliser des consoles dans l’IU tactile moderne et ne s’applique pas à l’IU classique.

AEM fournit divers mécanismes pour vous permettre de personnaliser les consoles (et les [fonctionnalité de création de pages](/help/sites-developing/customizing-page-authoring-touch.md)) de votre instance de création.

* Clientlibs Clientlibs vous permet d’étendre l’implémentation par défaut pour créer de nouvelles fonctionnalités, tout en réutilisant les fonctions, objets et méthodes standard. Lors de la personnalisation, vous pouvez créer votre propre bibliothèque cliente sous `/apps.` Par exemple, il peut contenir le code requis pour votre composant personnalisé.

* Recouvrements Les superpositions reposent sur des définitions de noeud et vous permettent de superposer la fonctionnalité standard (dans `/libs`) avec vos propres fonctionnalités personnalisées (dans `/apps`). Lors de la création d’une incrustation, une copie 1:1 de l’original n’est pas nécessaire, car Sling Resource Merger permet l’héritage.

Elles peuvent être utilisées de différentes manières pour étendre vos consoles AEM. Une petite sélection est abordée ci-dessous (à un niveau élevé).

>[!NOTE]
>
>Pour plus d’informations, voir :
>
>* Utilisation et création [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilisation et création [superpositions](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>


>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recréez l’élément requis (tel qu’il existe dans `/libs`) sous `/apps`.
>
>1. Apportez les modifications désirées dans `/apps`.
>

Par exemple, les emplacements suivants dans la structure `/libs` risquent d’être recouverts :

* Consoles (toutes les consoles basées sur les pages de l’IU Granite), par exemple :

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Consultez l’article de la base de connaissances [Résolution des problèmes liés à l’IU tactile d’AEM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html) pour découvrir d’autres conseils et outils.

## Personnalisation de l’affichage par défaut d’une console {#customizing-the-default-view-for-a-console}

Vous pouvez personnaliser la vue par défaut (colonne, carte, liste) d’une console :

1. Vous pouvez réorganiser les vues en recouvrant l’entrée requise depuis l’emplacement suivant :

   `/libs/wcm/core/content/sites/jcr:content/views`

   La première entrée est la valeur par défaut.

   Les nœuds disponibles correspondent aux options d’affichage disponibles :

   * `column`
   * `card`
   * `list`

1. Par exemple, dans un recouvrement de liste :

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Définissez la propriété suivante :

   * **Nom** : `sling:orderBefore`
   * **Type** : `String`
   * **Valeur** : `column`

### Ajouter une nouvelle action à la barre d’outils {#add-new-action-to-the-toolbar}

1. Vous pouvez créer vos propres composants et inclure les bibliothèques clientes correspondantes pour les actions personnalisées. Par exemple, un **Promouvoir le Twitter** Action à l’adresse :

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Elle peut ensuite être connectée à un élément de la barre d’outils sur la console :

   `/apps/<yourProject>/admin/ext/launches`

   Par exemple, en mode de sélection :

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Limitation d’une action de barre d’outils à un groupe spécifique {#restrict-a-toolbar-action-to-a-specific-group}

1. Vous pouvez utiliser une condition de rendu personnalisée pour superposer l’action standard et imposer des conditions spécifiques qui doivent être remplies avant son rendu.

   Par exemple, créez un composant pour contrôler les conditions de rendu en fonction du groupe :

   `/apps/myapp/components/renderconditions/group`

1. Pour les appliquer à l’action Créer un site sur la console Sites :

   `/libs/wcm/core/content/sites`

   Créez le recouvrement :

   `/apps/wcm/core/content/sites`

1. Ajoutez ensuite la condition de rendu pour l’action :

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   En utilisant des propriétés sur ce nœud, vous pouvez définir les `groups` autorisés à effectuer l’action spécifique ; par exemple, les `administrators`.

### Personnalisation des colonnes dans la vue Liste {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Cette fonction est optimisée pour les champs de colonnes de texte ; pour les autres types de données, il est possible de remplacer `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` dans `/apps`.

Pour personnaliser les colonnes en mode Liste :

1. Recouvrez la liste des colonnes disponibles.

   * Sur le nœud :

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * Ajoutez des colonnes ou supprimez des colonnes existantes.

   Consultez [Utilisation des recouvrements (et fusion de ressources Sling) pour plus d’informations.](/help/sites-developing/overlays.md)

1. Facultatif :

   * Si vous souhaitez connecter des données supplémentaires, vous devez écrire un [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) avec une
     `pageInfoProviderType`.

   Par exemple, consultez la classe/le lot joint (à partir de GitHub) ci-dessous.

1. Vous pouvez désormais sélectionner la colonne dans le paramétrateur de colonnes du mode Liste.

### Filtrage des ressources {#filtering-resources}

Lors de l’utilisation d’une console, un cas d’utilisation courant se présente lorsque l’utilisateur doit effectuer une sélection dans des ressources (par exemple, pages, composants, ressources, etc.). Cela peut prendre la forme d’une liste, par exemple, à partir de laquelle l’auteur doit choisir un élément.

Pour maintenir la liste à une taille raisonnable et adaptée au cas d’utilisation, un filtre peut être mis en oeuvre sous la forme d’un prédicat personnalisé. Voir [cet article](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) pour plus d’informations.
