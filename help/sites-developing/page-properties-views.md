---
title: Personnaliser les vues des propriétés de la page
seo-title: Customizing Views of Page Properties
description: Chaque page comporte un ensemble de propriétés que vous pouvez modifier selon vos besoins.
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 63%

---

# Personnaliser les vues des propriétés de la page{#customizing-views-of-page-properties}

Chaque page comporte un ensemble de [properties](/help/sites-authoring/editing-page-properties.md) qui peuvent être affichés et modifiés par les utilisateurs ; certaines sont requises lors de la création de la page (création d’une vue), d’autres peuvent être affichées et modifiées ultérieurement (modification d’une vue). Ces propriétés de page sont définies et mises à la disposition des utilisateurs dans la boîte de dialogue (`cq:dialog`) du composant de page approprié.

>[!CAUTION]
>
>L’affichage des propriétés de page ne peut pas être personnalisé dans l’interface utilisateur classique.

Le statut par défaut de chaque propriété de la page est :

* masqué dans la vue de création (par exemple, **Créer une page** assistant)

* disponible dans la vue d’édition (par exemple, **Afficher les propriétés**)

Les champs doivent être configurés spécifiquement si une modification est requise. Pour ce faire, utilisez les propriétés de noeud appropriées :

* Propriété de page à rendre disponible dans la vue de création (par exemple : **Créer une page** assistant) :

   * Nom : `cq:showOnCreate`
   * Type : `Boolean`

* Propriété de page à afficher dans la vue d’édition (par exemple : **Affichage**/**Modifier**) **Propriétés** ) :

   * Nom : `cq:hideOnEdit`
   * Type : `Boolean`

Reportez-vous, par exemple, aux paramètres des champs regroupés sous l’onglet **Autres titres et description** de l’onglet **De base** du composant Page de base. Ils sont visibles dans l’assistant **Créer une page**, étant donné que `cq:showOnCreate` a été défini sur `true` :

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consultez le [Tutoriel sur l’extension des propriétés de page](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=fr) pour obtenir un guide sur la personnalisation des propriétés de page.

## Configurer vos propriétés de page {#configuring-your-page-properties}

Vous pouvez également configurer les champs disponibles en configurant la boîte de dialogue de votre composant de page et en appliquant les propriétés de noeud appropriées.

Par exemple, l’assistant [**Créer une page**](/help/sites-authoring/managing-pages.md#creating-a-new-page) affiche, par défaut, les champs regroupés sous **Autres titres et description**. Pour masquer ces derniers, définissez la configuration suivante :

1. Créez votre composant de page sous `/apps`.
1. Créez un remplacement (à l’aide de la méthode *dialog diff* fournie par [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) pour la section `basic` de votre composant de page ; par exemple :

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Pour référence :
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   Cependant, vous ne devez ***rien*** modifier dans le chemin `/libs`.
   >
   En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
   >
   La méthode recommandée pour la configuration et d’autres modifications est la suivante :
   >
   1. Recréez l’élément requis (tel qu’il existe dans `/libs`) sous `/apps`.
   1. Apportez les modifications désirées dans `/apps`.

1. Définissez la propriété `path` sur `basic` pour pointer vers le remplacement de l’onglet de base (voir également l’étape suivante). Par exemple :

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Créez un remplacement de la section `basic` - `moretitles` à l’emplacement correspondant ; par exemple :

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Appliquez la propriété de nœud appropriée :

   * **Nom** : `cq:showOnCreate`
   * **Type** : `Boolean`
   * **Valeur** : `false`

   Le **Autres titres et description** ne s’affichera plus dans la section **Créer une page** assistant.

>[!NOTE]
>
Lors de la configuration des propriétés de page à utiliser avec des Live Copies, voir [Configuration des verrous MSM sur les propriétés de page](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) pour plus d’informations.

## Exemple de configuration des propriétés de page {#sample-configuration-of-page-properties}

Cet exemple illustre la technique dialog diff de [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) ; y compris l’utilisation de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Il illustre également l’utilisation de `cq:showOnCreate` et de `cq:hideOnEdit`.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-page-dialog sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).
