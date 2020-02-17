---
title: Configuration de plusieurs éditeurs statiques
seo-title: Configuration de plusieurs éditeurs statiques
description: Il est possible de configurer votre composant afin qu’il comporte plusieurs éditeurs statiques.
seo-description: Il est possible de configurer votre composant afin qu’il comporte plusieurs éditeurs statiques.
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Configuration de plusieurs éditeurs statiques{#configuring-multiple-in-place-editors}

Il est possible de configurer votre composant afin qu’il comporte plusieurs éditeurs statiques dans l’interface utilisateur optimisée pour les écrans tactiles.

Une fois le composant configuré, vous pouvez sélectionner le contenu approprié et ouvrir l’éditeur adéquat. Par exemple :

![chlimage_1-8](assets/chlimage_1-8a.png)

## Configuration de plusieurs éditeurs {#configuring-multiple-editors}

Pour qu’il soit possible d’activer plusieurs éditeurs statiques, la structure d’un type de nœud `cq:InplaceEditingConfig` a été optimisée avec la définition du type de nœud `cq:ChildEditorConfig`.

Par exemple :

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Pour configurer plusieurs éditeurs, procédez comme suit :

1. On the node `cq:inplaceEditing` (of type `cq:InplaceEditingConfig`) define the property:

   * Nom:`editorType`
   * Type: `String`
   * Valeur: `hybrid`

1. Créez un nœud sous celui-ci :

   * Nom: `cq:ChildEditors`
   * Type: `nt:unstructured`

1. Sous le nœud `cq:childEditors`, créez un nœud pour chaque éditeur statique :

   * Nom : le nom de chaque nœud doit être celui de la propriété qu’il représente (comme avec les cibles de dépôt). Par exemple, `image`, `text`.
   * Type : cq : `ChildEditorConfig`
   >[!NOTE]
   >
   >Il existe une corrélation entre les cibles de dépôt définies et les éditeurs enfants. Le nom du nœud `cq:ChildEditorConfig` sera considéré comme étant l’ID de la cible de dépôt à utiliser en tant que paramètre pour l’éditeur enfant sélectionné. Si la sous-zone modifiable ne comporte pas de cible de dépôt (comme avec un composant texte, par exemple), le nom de l’éditeur enfant est toujours considéré comme un moyen d’identifier la zone modifiable correspondante.

1. On each of these nodes ( `cq:ChildEditorConfig`) define the properties:

   * Nom: `type`
   * Value: name of the registered in-place editor; for example, `image`, `text`

   * Nom: `title`
   * Value: the title that you want to display in the components selection list (of available editors); for example, `Image`, `Text`

### Configuration supplémentaire pour les éditeurs de texte enrichi (RTE){#additional-configuration-for-rich-text-editors}

La configuration des éditeurs de texte enrichi est légèrement différente, dans la mesure où vous pouvez configurer chaque instance RTE séparément.

>[!NOTE]
>
>Pour plus d’informations, voir [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md).

Pour disposer de plusieurs éditeurs de texte enrichi, une configuration est requise pour chaque éditeur statique :

* Sous `cq:InplaceEditingConfig` définir un `config` noeud.

   * Sous le nœud `config`, définissez chaque configuration RTE.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>Il est conseillé de définir le nœud `config` sous `cq:InplaceEditingConfig`, car chaque éditeur de texte enrichi peut présenter une configuration différente.
>
>Cependant, dans le cas de l’éditeur de texte enrichi, la propriété `configPath` est prise en charge lorsque le composant ne contient qu’une seule instance de l’éditeur (sous-zone modifiable). Cette utilisation de `configPath` permet de garantir la rétrocompatibilité avec les boîtes de dialogue du composant conçues pour l’ancienne interface utilisateur.

## Exemples de code {#code-samples}

**CODE SUR GITHUB**

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrir le projet aem-authoring-hybrideditors sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## Ajout d’un éditeur statique {#adding-an-in-place-editor}

For general information about adding an in-place editor see the document [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).
