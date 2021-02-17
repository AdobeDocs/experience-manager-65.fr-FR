---
title: Personnalisation des consoles
seo-title: Personnalisation des consoles
description: AEM comporte plusieurs mécanismes pour vous permettre de personnaliser les consoles de votre instance de création.
seo-description: AEM comporte plusieurs mécanismes pour vous permettre de personnaliser les consoles de votre instance de création.
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 77%

---


# Personnalisation des consoles {#customizing-the-consoles}

>[!CAUTION]
>
>Ce document décrit comment personnaliser les consoles de l’IU moderne et compatible avec les écrans tactiles, et ne s’applique pas à l’IU classique.

AEM comporte plusieurs mécanismes pour vous permettre de personnaliser les consoles (et la [fonctionnalité de création de pages](/help/sites-developing/customizing-page-authoring-touch.md)) de votre instance de création.

* Clientlibs Les bibliothèques clientes (clientlibs) vous permettent d’étendre l’implémentation par défaut afin d’obtenir la nouvelle fonctionnalité, tout en réutilisant les fonctions, objets et méthodes standard. Lors de la personnalisation, vous pouvez créer votre propre bibliothèque cliente sous `/apps.` Par exemple, elle peut contenir le code requis pour votre composant personnalisé.

* Incrustations
Les incrustations sont basées sur les définitions de noeud et vous permettent de superposer la fonctionnalité standard (dans `/libs`) avec votre propre fonctionnalité personnalisée (dans `/apps`). Lors de la création d’un recouvrement, une copie 1:1 de l’original n’est pas nécessaire, car la fusion de ressources Sling prend en compte l’héritage.

Ils peuvent être utilisés de différentes manières pour étendre les consoles AEM. Une petite sélection est abordée ci-dessous (à un niveau élevé).

>[!NOTE]
>
>Pour plus d’informations, voir :
>
>* Utilisation et création de [bibliothèques clientes](/help/sites-developing/clientlibs.md).
>* Utilisation et création d’[incrustations](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>
>
Ce thème est également abordé dans la session [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) – [Personnalisation de l’interface utilisateur pour AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).

>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recréer l’élément requis (c.-à-d. tel qu’il existe dans `/libs`) sous `/apps`
   >
   >
1. Apportez les modifications désirées dans `/apps`

>



Par exemple, l’emplacement suivant dans la structure `/libs` peut être superposé :

* Consoles (toutes les consoles basées sur les pages de l’IU Granite), par exemple :

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Voir l’article de la base de connaissances [Résolution des problèmes liés à l’IU tactile d’AEM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html) pour d’autres conseils et outils.

## Personnalisation du mode par défaut pour une console {#customizing-the-default-view-for-a-console}

Vous pouvez personnaliser le mode par défaut (colonnes, carte ou liste) pour une console :

1. Vous pouvez réorganiser les modes en recouvrant l’entrée requise à partir de l’emplacement suivant :

   `/libs/wcm/core/content/sites/jcr:content/views`

   La première entrée est la valeur par défaut.

   Les noeuds disponibles correspondent aux options de vue disponibles :

   * `column`
   * `card`
   * `list`

1. Par exemple, dans un recouvrement du mode Liste :

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Définissez la propriété suivante :

   * **Nom** : `sling:orderBefore`
   * **Type** : `String`
   * **Valeur**: `column`

### Ajout d’une action à la barre d’outils {#add-new-action-to-the-toolbar}

1. Vous pouvez créer vos propres composants et inclure les bibliothèques clientes correspondantes pour des actions personnalisées. Par exemple, une action **Promouvoir sur Twitter** à l’emplacement :

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Elle peut ensuite être connectée à un élément de la barre d’outils sur la console :

   `/apps/<yourProject>/admin/ext/launches`

   Par exemple, en mode de sélection :

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Limitation d’une action de la barre d’outils à un groupe spécifique {#restrict-a-toolbar-action-to-a-specific-group}

1. Vous pouvez utiliser une condition de rendu personnalisé pour recouvrir l’action standard et imposer des conditions spécifiques qui doivent être remplies avant le rendu.

   Par exemple, créez un composant pour contrôler les conditions de rendu selon le groupe :

   `/apps/myapp/components/renderconditions/group`

1. Pour les appliquer à l’action Créer un site sur la console Sites :

   `/libs/wcm/core/content/sites`

   Créez le recouvrement :

   `/apps/wcm/core/content/sites`

1. Ajoutez ensuite la condition de rendu pour l’action :

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   En utilisant les propriétés de ce noeud, vous pouvez définir l&#39;`groups` autorisé à exécuter l&#39;action spécifique ; par exemple, `administrators`

### Personnalisation des colonnes en mode Liste {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Cette fonction est optimisée pour les colonnes de champs de texte ; pour les autres types de données, il est possible de superposer `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` dans `/apps`.

Pour personnaliser les colonnes en mode Liste :

1. Recouvrez la liste des colonnes disponibles.

   * Sur le noeud :

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * Ajoutez des colonnes ou supprimez des colonnes existantes.
   Voir [Utilisation des recouvrements (et la fusion de ressources Sling) pour plus d’informations.](/help/sites-developing/overlays.md)

1. Si vous le souhaitez :

   * Si vous souhaitez ajouter des données supplémentaires, vous devez écrire un [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) avec un
      `pageInfoProviderType` property.

   Par exemple, voir la classe/le lot (tiré de GitHub) ci-dessous.

1. Vous pouvez maintenant sélectionner la colonne dans le configurateur de colonnes du mode Liste.

### Filtrage des ressources  {#filtering-resources}

Lorsqu’une console est utilisée, un cas d’utilisation fréquent est la nécessité pour l’utilisateur de choisir des ressources (par exemple, des pages, des composants, des ressources, etc.). Cela peut prendre la forme d’une liste dans laquelle l’auteur doit sélectionner un élément.

Pour que la liste garde une taille raisonnable et reste pertinente par rapport au cas d’utilisation, un filtre peut être mis en œuvre sous la forme d’un prédicat personnalisé. Voir [cet article](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) pour en savoir plus.
