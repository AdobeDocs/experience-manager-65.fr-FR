---
title: Personnaliser les consoles
description: AEM fournit divers mécanismes pour vous permettre de personnaliser les consoles de votre instance de création.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 99%

---

# Personnaliser les consoles {#customizing-the-consoles}

>[!CAUTION]
>
>Ce document explique comment personnaliser la création de pages dans l’IU tactile moderne et ne s’applique pas à l’IU classique.

AEM comporte plusieurs mécanismes pour vous permettre de personnaliser les consoles et la [fonctionnalité de création de pages](/help/sites-developing/customizing-page-authoring-touch.md) de votre instance de création.

* Clientlibs
Les bibliothèques clientes (clientlibs) vous permettent d’étendre l’implémentation par défaut afin d’obtenir la nouvelle fonctionnalité, tout en réutilisant les fonctions, objets et méthodes standard. Lors de la personnalisation, vous pouvez créer votre propre bibliothèque cliente sous `/apps.` Par exemple, elle peut contenir le code requis pour votre composant personnalisé.

* Recouvrements
Les recouvrements sont basés sur les définitions de nœuds et vous permettent de recouvrir les fonctionnalités standard (dans `/libs` ) avec vos propres fonctionnalités personnalisées (dans `/apps`). Lors de la création d’un recouvrement, il n’est pas nécessaire de disposer d’une copie 1:1 de l’original, car Sling Resource Merger autorise l’héritage.

Ils peuvent être utilisés de différentes manières pour étendre vos consoles AEM. Une petite sélection est abordée ci-dessous (à un niveau élevé).

>[!NOTE]
>
>Pour plus d’informations, voir :
>
>* Utiliser et créer des [clientlibs](/help/sites-developing/clientlibs.md).
>* Utiliser et créer des [recouvrements](/help/sites-developing/overlays.md).
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
>Consultez l’article de la base de connaissances [Résolution des problèmes liés à l’IU tactile d’AEM](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-16935) pour découvrir d’autres conseils et outils.

## Personnaliser l’affichage par défaut d’une console {#customizing-the-default-view-for-a-console}

Vous pouvez personnaliser l’affichage par défaut (colonne, carte, liste) d’une console :

1. Vous pouvez réorganiser les vues en recouvrant l’entrée requise depuis l’emplacement suivant :

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

1. Vous pouvez créer vos propres composants et inclure les bibliothèques clientes correspondantes pour les actions personnalisées. Par exemple, une action **Promouvoir sur Twitter** à :

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Elle peut ensuite être connectée à un élément de la barre d’outils sur la console :

   `/apps/<yourProject>/admin/ext/launches`

   Par exemple, en mode de sélection :

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Limiter une action de la barre d’outils à un groupe spécifique {#restrict-a-toolbar-action-to-a-specific-group}

1. Vous pouvez utiliser une condition de rendu personnalisée pour superposer l’action standard et imposer des conditions spécifiques qui doivent être remplies avant son rendu.

   Par exemple, créez un composant pour contrôler les conditions de rendu en fonction du groupe :

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

Pour personnaliser les colonnes dans la vue Liste :

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

1. Vous pouvez maintenant sélectionner la colonne dans le configurateur de colonnes de la vue Liste.

### Filtrer les ressources {#filtering-resources}

Lors de l’utilisation d’une console, un cas d’utilisation courant se présente lorsque l’utilisateur ou l’utilisatrice doit effectuer un choix parmi des ressources (par exemple, des pages, des composants, des ressources, etc.). Cela peut prendre la forme d’une liste, par exemple à partir de laquelle l’auteur ou l’autrice doit choisir un élément.

Pour maintenir la liste à une taille raisonnable et adaptée au cas d’utilisation, un filtre peut être mis en œuvre sous la forme d’un prédicat personnalisé. Pour plus d’informations, voir [Personnaliser la création de page : filtrage des ressources](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources).
