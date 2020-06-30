---
title: Configurez RTE pour plusieurs éditeurs en place.
description: Créez plusieurs éditeurs sur place en Adobe Experience Manager en configurant l’éditeur de texte enrichi.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e49411a99a80e91c983afc103a8ea826e75569b8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 26%

---


# Configuration de plusieurs éditeurs sur place {#configure-multiple-in-place-editors}

Vous pouvez configurer l’Editeur de texte enrichi en Adobe Experience Manager de sorte qu’il dispose de plusieurs éditeurs sur place. Une fois le composant configuré, vous pouvez sélectionner le contenu approprié et ouvrir l’éditeur adéquat.

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

Pour configurer plusieurs éditeurs, procédez comme suit :

1. Sur le noeud `cq:inplaceEditing` (de type `cq:InplaceEditingConfig`), définissez les propriétés suivantes :

   * Nom (name) : `editorType`
   * Type : `String`
   * Valeur : `hybrid`

1. Sous ce noeud, créez un noeud :

   * Nom : `cq:ChildEditors`
   * Type : `nt:unstructured`

1. Under `cq:childEditors` node, create a node for each in-place editor:

   * Nom : Le nom de chaque noeud correspond au nom de la propriété qu’il représente, comme c’est le cas pour les cibles de dépôt. Par exemple, `image` et `text`.
   * Type : `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >Il existe une corrélation entre les cibles de dépôt définies et les éditeurs enfants. The name of the `cq:ChildEditorConfig` node is considered as the drop target ID, for use as a parameter to the selected child editor. Si la sous-zone modifiable ne comporte pas de cible de dépôt, par exemple, dans un composant de texte, le nom de l’éditeur enfant est toujours considéré comme un identifiant permettant d’identifier la zone modifiable correspondante.

1. On each of these nodes (`cq:ChildEditorConfig`) define the properties:

   * Nom: `type`.
   * Value: The name of the registered in-place editor; for example, `image` and `text`.

   * Nom: `title`.
   * Valeur : Titre affiché dans la liste de sélection des composants des éditeurs disponibles. Par exemple, `Image` et `Text`.

### Additional configuration for Rich Text Editors {#additional-configuration-for-rich-text-editors}

La configuration des éditeurs de texte enrichi est légèrement différente, dans la mesure où vous pouvez configurer chaque instance RTE séparément. Pour plus d’informations, voir [Configuration de l’éditeur](/help/sites-administering/rich-text-editor.md)de texte enrichi. Pour avoir plusieurs ETC, créez une configuration pour chaque ETC statique. Adobe recommande de créer le nouveau noeud de configuration sous `cq:InplaceEditingConfig` car chaque RTE peut avoir une configuration différente. Sous le nouveau noeud, créez chaque configuration RTE individuelle.

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
>Cependant, dans le cas de l’éditeur de texte enrichi, la propriété `configPath` est prise en charge lorsque le composant ne contient qu’une seule instance de l’éditeur (sous-zone modifiable). This use of `configPath` is provided to support backwards compatibility with older user interface dialogs of the component.

>[!CAUTION]
>
>Ne donnez pas le nom `config` au nœud de configuration de l’éditeur de texte enrichi (RTE). Otherwise, the RTE configurations are available for only the administrators and not for the users in the group `content-author`.

## Code samples {#code-samples}

Vous trouverez le code de cette page sur le projet [aem-authoring-hybrideditors sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). Vous pouvez télécharger le projet complet sous forme [d’archive](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)ZIP.

## Ajouter un éditeur statique {#add-an-in-place-editor}

For general information about adding an in-place editor see the document [customize page authoring](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Configuration de l’éditeur de texte enrichi en Experience Manager](/help/sites-administering/rich-text-editor.md).

