---
title: Configurez l’éditeur de texte enrichi pour créer des pages Web et des sites accessibles.
description: Configurez l’éditeur de texte enrichi pour créer des pages Web et des sites accessibles.
contentOwner: AG
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 47%

---


# Configurer RTE pour créer des pages Web et des sites accessibles {#configure-rte-for-accessibility}

Adobe Experience Manager prend en charge de nombreuses fonctions d&#39;accessibilité standard, conformément à diverses normes d&#39;accessibilité. En outre, les développeurs peuvent personnaliser ou étendre les fonctionnalités afin de créer du contenu accessible à l’aide de composants Experience Manager qui utilisent l’éditeur de texte enrichi (RTE).

Lors de la conception de pages Web et de l’ajout de contenu aux pages, les développeurs et les auteurs de contenu peuvent utiliser les fonctionnalités du RTE pour fournir des informations relatives à l’accessibilité. Par exemple, ajoutez des informations structurelles au moyen d’en-têtes et d’éléments de paragraphe.

Pour configurer et personnaliser ces fonctionnalités, [configurez les modules externes RTE](#configure-the-plugin-features) pour le composant. Par exemple, le module externe `paraformat` vous permet d’ajouter des éléments sémantiques de niveau bloc supplémentaires, y compris l’extension du nombre de niveaux d’en-tête pris en charge au-delà des niveaux de base `H1`, `H2` et `H3` fournis par défaut.

Le RTE est disponible dans divers composants pour l’interface utilisateur tactile et l’interface utilisateur classique. Cependant, le composant Principal à utiliser le RTE est le composant **Texte** disponible pour les deux interfaces. Les images suivantes montrent le RTE avec une gamme de plug-ins activés, y compris `paraformat` :

![Composant de texte (RTE) en mode plein écran dans l’interface utilisateur tactile.](assets/chlimage_1-206.png)

*Figure : Composant Texte de l’interface utilisateur tactile.*

![Boîte de dialogue Modifier (éditeur de texte enrichi) du composant Text dans l’IU classique.](assets/chlimage_1-207.png)

*Figure : Composant Texte de l’interface utilisateur de Classic.*

Pour connaître les différences entre les fonctionnalités RTE disponibles dans les différentes interfaces, voir [Plugins et leurs fonctionnalités](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configuration des fonctionnalités de module externe {#configure-the-plugin-features}

Pour obtenir des instructions complètes sur la configuration du RTE, voir [configuration de la page Editeur de texte enrichi](/help/sites-administering/rich-text-editor.md). Ceci couvre tous les problèmes, y compris les étapes principales :

* [Modules externes et fonctionnalités](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Emplacements de configuration](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Activation d’un module externe et configuration de la propriété features](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configuration d’autres fonctionnalités de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

En configurant un module externe dans la sous-branche `rtePlugins` appropriée du CRXDE Lite, vous pouvez activer toutes les fonctionnalités ou certaines fonctionnalités de ce module externe.

![CRXDE Lite présentant un exemple de rtePlugin.](assets/chlimage_1-208.png)

### Exemple : spécifiez les formats de paragraphe disponibles dans le champ de sélection RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

De nouveaux formats de bloc sémantique peuvent être rendus disponibles pour la sélection comme suit :

1. Selon votre éditeur de texte enrichi, déterminez l’[emplacement de configuration](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations) et accédez-y.
1. [Activez le champ de sélection Paragraphe](/help/sites-administering/rich-text-editor.md). En [activant le module externe](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Spécifiez les formats qui doivent être disponibles dans le champ de sélection Paragraphes](/help/sites-administering/rich-text-editor.md).
1. Les formats de paragraphe sont ensuite à la disposition de l’auteur du contenu des champs de sélection dans l’éditeur de texte enrichi. Ils sont accessibles :

   * Utilisation de l’icône de sélection de paragraphe dans l’interface utilisateur tactile.
   * Utilisation du champ **Format** (sélecteur contextuel) dans l’interface utilisateur classique.

Avec les éléments structurels disponibles dans l’éditeur de texte enrichi via les options de format de paragraphe, AEM constitue une bonne base pour le développement de contenu accessible. Les auteurs de contenu ne peuvent pas utiliser l’éditeur de texte enrichi pour formater la taille de la police ou les couleurs ou d’autres attributs associés, empêchant la création de formatage en ligne. À la place, ils doivent sélectionner les éléments structurels appropriés comme les en-têtes et utiliser des styles globaux choisis via l’option Styles. Ceci garantit une mise en forme nette, de meilleures options pour les utilisateurs qui naviguent avec leurs propres feuilles de style et un contenu correctement structuré.

## Utilisation de la fonction de modification de la source {#use-of-the-source-edit-feature}

Dans certains cas, les auteurs de contenu constateront qu’il est nécessaire d’examiner et d’ajuster le code source HTML créé à l’aide de l’éditeur de texte enrichi. Par exemple, un élément de contenu créé dans l’éditeur de texte enrichi peut nécessiter une mise en forme supplémentaire pour être conforme à la norme WCAG 2.0. Ceci peut s’effectuer avec l’option [Modification de la source](/help/sites-administering/rich-text-editor.md#aboutplugins) de l’éditeur de texte enrichi. Vous pouvez spécifier la fonction [ `sourceedit` dans le module `misctools` ](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilisez la fonction `sourceedit` avec prudence. Les fautes de frappe et/ou les fonctions non prises en charge peuvent entraîner d’autres problèmes.

## Ajouter la prise en charge d&#39;un plus grand nombre d&#39;éléments et d&#39;attributs HTML {#add-support-for-more-html-elements-and-attributes}

Pour étendre davantage les fonctions d’accessibilité d’AEM, vous pouvez étendre les composants existants (par exemple, les composants **Text** et **Table**) en fonction de l’éditeur de texte enrichi avec des éléments et attributs supplémentaires.

La procédure suivante illustre comment étendre le composant **Table** avec un élément **Caption** qui fournit des informations sur un tableau de données aux utilisateurs de technologies d&#39;assistance :

### Exemple : ajoutez la légende à la boîte de dialogue Propriétés du tableau {#example-adding-the-caption-to-the-table-properties-dialog}

Dans le constructeur de l’élément `TablePropertiesDialog`, ajoutez un champ de saisie de texte supplémentaire utilisé pour modifier la légende. Notez que `itemId` doit être défini sur `caption` (c’est-à-dire le nom de l’attribut DOM) pour gérer automatiquement son contenu.

Dans **Table**, définissez explicitement ou supprimez l&#39;attribut de/vers l&#39;élément DOM. La valeur est transmise par la boîte de dialogue dans l’objet `config`. Notez que les attributs DOM doivent être définis/supprimés à l’aide des méthodes `CQ.form.rte.Common` correspondantes (`com` est un raccourci de `CQ.form.rte.Common`) pour éviter les pièges courants des mises en œuvre de navigateur.

>[!NOTE]
>
>Cette procédure ne convient qu’à l’interface utilisateur de Classic.

### Exemple : créez du code HTML accessible lors de l’utilisation de l’accent dans le texte {#create-accessible-html-for-text}

RTE peut utiliser les balises `strong` et `em` à la place de `b` et `i`. Ajoutez le noeud suivant en tant que frère aux noeuds `uiSettings` et `rtePlugins` dans la boîte de dialogue.

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### Instructions détaillées {#step-by-step-instructions}

1. Démarrez CRXDE Lite. Par exemple : [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copier :

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   vers:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Vous devrez peut-être créer des dossiers intermédiaires si ceux-ci n’existent pas déjà.

1. Copier :

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   vers:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Ouvrez le fichier suivant pour le modifier (ouvrez-le en double-cliquant dessus) :

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. Dans la méthode `constructor`, avant la lecture de ligne :

   ```
   var dialogRef = this;
   ```

   Ajoutez le code suivant :

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Ouvrez le fichier suivant :

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. Ajoutez le code suivant à la fin de la méthode `transferConfigToTable` :

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. Enregistrez vos modifications à l&#39;aide de **Enregistrer tout..**.

>[!NOTE]
>
>Le champ de texte brut n’est pas le seul type d’entrée autorisé pour la valeur de l’élément de légende. Vous pouvez utiliser n’importe quel widget ExtJS qui fournit la valeur de la légende par le biais de sa méthode `getValue()`.
>
>Pour ajouter des fonctionnalités de modification pour d’autres éléments et attributs, assurez-vous à la fois :
>
>* La propriété `itemId` de chaque champ correspondant est définie sur le nom de l’attribut DOM approprié (`TablePropertiesDialog`).
>* Que l’attribut est défini et/ou supprimé sur l’élément DOM de manière explicite (`Table`).


>[!MORELIKETHIS]
>
>* [Guide rapide relatif à WCAG 2.0](/help/managing/qg-wcag.md)
>* [Création de contenu accessible (conformité WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

