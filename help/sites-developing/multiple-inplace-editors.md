---
title: Configurez l’éditeur de texte enrichi pour plusieurs éditeurs statiques.
description: Créez plusieurs éditeurs statiques dans Adobe Experience Manager en configurant l’éditeur de texte enrichi.
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 100%

---

# Configuration de plusieurs éditeurs statiques {#configure-multiple-in-place-editors}

Vous pouvez configurer l’éditeur de texte enrichi dans Adobe Experience Manager afin qu’il dispose de plusieurs éditeurs statiques. Une fois le composant configuré, vous pouvez sélectionner le contenu approprié et ouvrir l’éditeur adéquat.

![Un éditeur statique spécifique](assets/rte-inplace-editor.png)

## Configuration de plusieurs éditeurs {#configure-multiple-editors}

Pour qu’il soit possible d’activer plusieurs éditeurs statiques, la structure d’un type de nœud `cq:InplaceEditingConfig` a été optimisée avec la définition du type de nœud `cq:ChildEditorConfig`.

Par exemple :

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Pour configurer plusieurs éditeurs, procédez comme suit :

1. Sur le nœud `cq:inplaceEditing` (de type `cq:InplaceEditingConfig`), définissez les propriétés suivantes :

   * Nom : `editorType`
   * Type : `String`
   * Valeur : `hybrid`

1. Créez un nœud sous celui-ci :

   * Nom : `cq:ChildEditors`
   * Type : `nt:unstructured`

1. Sous le nœud `cq:childEditors`, créez un nœud pour chaque éditeur statique :

   * Nom : le nom de chaque nœud est celui de la propriété qu’il représente, comme avec les cibles de dépôt. Par exemple, `image` et `text`.
   * Type : `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >Il existe une corrélation entre les cibles de dépôt définies et les éditeurs enfants. Le nom du nœud `cq:ChildEditorConfig` est considéré comme l’ID de la cible de dépôt à utiliser en tant que paramètre pour l’éditeur enfant sélectionné. Si la sous-zone modifiable ne comporte pas de cible de dépôt, par exemple comme avec un composant texte, le nom de l’éditeur enfant est toujours considéré comme un moyen d’identifier la zone modifiable correspondante.

1. Définissez les propriétés suivantes sur chacun de ces nœuds (`cq:ChildEditorConfig`) :

   * Nom : `type`
   * Valeur : nom de l’éditeur statique enregistré ; par exemple, `image` et `text`.

   * Nom : `title`
   * Valeur : titre affiché dans la liste de sélection des composants des éditeurs disponibles. Par exemple, `Image` et `Text`.

### Configuration supplémentaire pour les éditeurs de texte enrichi (RTE) {#additional-configuration-for-rich-text-editors}

La configuration des éditeurs de texte enrichi est légèrement différente, dans la mesure où vous pouvez configurer chaque instance RTE séparément. Pour plus d’informations, consultez la section [configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md). Pour disposer de plusieurs éditeurs de texte enrichi, vous devez configurer chaque éditeur statique. Adobe recommande de créer le nœud de configuration sous `cq:InplaceEditingConfig` car chaque éditeur de texte enrichi peut avoir une configuration différente. Sous le nouveau nœud, définissez chaque configuration RTE.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>Cependant, dans le cas de l’éditeur de texte enrichi, la propriété `configPath` est prise en charge lorsque le composant ne contient qu’une seule instance de l’éditeur (sous-zone modifiable). Cette utilisation de `configPath` permet de garantir la rétrocompatibilité avec les boîtes de dialogue du composant conçues pour l’ancienne interface utilisateur.

>[!CAUTION]
>
>Ne donnez pas le nom `config` au nœud de configuration de l’éditeur de texte enrichi (RTE). Autrement, les configurations de l’éditeur de texte enrichi ne sont disponibles que pour les administrateurs, et non pour les utilisateurs du groupe `content-author`.

## Exemples de code {#code-samples}

Vous trouverez le code de cette page dans le [projet aem-authoring-hybrideditors sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). Vous pouvez télécharger l’intégralité du projet sous la forme d’[une archive ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## Ajout d’un éditeur statique {#add-an-in-place-editor}

Pour obtenir des informations d’ordre général sur l’ajout d’un éditeur statique, consultez le document [Personnalisation de la création de pages](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Configuration de l’éditeur de texte enrichi dans Experience Manager](/help/sites-administering/rich-text-editor.md)
