---
title: Configuration de l’éditeur de texte enrichi pour produire des sites accessibles
description: Découvrez comment configurer l’éditeur de texte enrichi (RTE) pour produire des sites accessibles.
uuid: 87539fee-3ecc-49f4-af3d-8dde72399c28
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ff0f006d-461c-4cc4-b6eb-d665f3f3b498
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# Configuration de l’éditeur de texte enrichi pour produire des sites accessibles {#configuring-rte-for-producing-accessible-sites}

AEM prend en charge à la fois :

* Les fonctions d’accessibilité standard, notamment le texte de remplacement pour les images
* Des fonctionnalités supplémentaires qui sont accessibles lors de la création de contenu avec les composants qui utilisent l’éditeur de texte enrichi (RTE)

Les auteurs de contenu peuvent utiliser les fonctions de l’éditeur de texte enrichi afin de fournir des informations d’accessibilité lors de l’ajout de contenu à une page. Cela peut impliquer l’ajout d’informations structurelles via des en-têtes et des éléments de paragraphe.

Vous pouvez [configurer et personnaliser ces fonctions en configurant des modules externes RTE](#configuring-the-plugin-features) pour le composant. For example, the `paraformat` plugin allows you to add additional block level semantic elements, including extending the number of heading levels supported beyond the basic `H1`, `H2` and `H3` provided by default.

Le RTE est disponible dans divers composants de l’interface utilisateur tactile et classique. Cependant, le composant principal pour l’utilisation de l’éditeur de texte enrichi est le composant **Texte**.

The **Text** component in AEM is available for both the touch-enabled and the classic UIs. Les illustrations suivantes présentent l’éditeur de texte enrichi avec une plage de modules externes activés, y compris `paraformat` :

* The **Text** component in the touch-enabled UI:

   ![Composant de texte (RTE) en mode plein écran dans l’interface utilisateur tactile.](assets/chlimage_1-206.png)

* Composant **Text** dans l’IU classique :

   ![Boîte de dialogue Modifier (éditeur de texte enrichi) du composant Text dans l’IU classique.](assets/chlimage_1-207.png)

>[!NOTE]
>
>Il existe des différences entre les fonctionnalités RTE disponibles dans l’interface utilisateur classique et l’interface utilisateur tactile. Pour plus d’informations, voir
>
>* [Modules externes et leurs fonctionnalités](/help/sites-administering/rich-text-editor.md#aboutplugins)
>* [Plugins et leurs fonctionnalités - IU tactile](/help/sites-administering/rich-text-editor.md#aboutplugins)
>



## Configuration des fonctionnalités de module externe {#configuring-the-plugin-features}

Les instructions complètes sur la configuration de l’éditeur de texte enrichi sont disponibles sur la page [Configuration de l’éditeur de texte enrichi.](/help/sites-administering/rich-text-editor.md) Ceci couvre tous les problèmes, y compris les étapes principales :

* [Modules externes et leurs fonctionnalités](/help/sites-administering/rich-text-editor.md#aboutplugins)
* [Emplacements de configuration](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Activation d’un module externe et configuration de la propriété features](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Configuration d’autres fonctionnalités de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

By configuring a plugin within the appropriate `rtePlugins` sub-branch in CRXDE Lite (see the following image), you can activate either all or specific features for that plugin.

![CRXDE Lite présentant un exemple de sous-branche rtePlugin.](assets/chlimage_1-208.png)

### Exemple : spécification des formats de paragraphes disponibles dans le champ de sélection de l’éditeur de texte enrichi {#example-specifying-paragraph-formats-available-in-rte-selection-field}

De nouveaux formats de bloc sémantique peuvent être rendus disponibles pour la sélection comme suit :

1. Selon votre éditeur de texte enrichi, déterminez l’[emplacement de configuration](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations) et accédez-y.
1. [Activez le champ de sélection Paragraphe](/help/sites-administering/rich-text-editor.md). En [activant le module externe](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Spécifiez les formats qui doivent être disponibles dans le champ de sélection Paragraphes](/help/sites-administering/rich-text-editor.md).
1. Les formats de paragraphe sont ensuite à la disposition de l’auteur du contenu des champs de sélection dans l’éditeur de texte enrichi. Ils sont accessibles :

   * Utilisation de l’icône représentant un curseur de paragraphe dans l’interface utilisateur tactile.
   * Using the **Format** field (pop-up selector) in the Classic UI.

Avec les éléments structurels disponibles dans l’éditeur de texte enrichi via les options de format de paragraphe, AEM constitue une bonne base pour le développement de contenu accessible. Les auteurs de contenu ne peuvent pas utiliser l’éditeur de texte enrichi pour formater la taille de la police ou les couleurs ou d’autres attributs associés, empêchant la création de formatage en ligne. À la place, ils doivent sélectionner les éléments structurels appropriés comme les en-têtes et utiliser des styles globaux choisis via l’option Styles. Ceci garantit une mise en forme nette, de meilleures options pour les utilisateurs qui naviguent avec leurs propres feuilles de style et un contenu correctement structuré.

## Utilisation de l’option Modification de la source {#use-of-the-source-edit-feature}

Dans certains cas, les auteurs de contenu constateront qu’il est nécessaire d’examiner et d’ajuster le code source HTML créé à l’aide de l’éditeur de texte enrichi. Par exemple, un élément de contenu créé dans l’éditeur de texte enrichi peut nécessiter une mise en forme supplémentaire pour être conforme à la norme WCAG 2.0. Ceci peut s’effectuer avec l’option [Modification de la source](/help/sites-administering/rich-text-editor.md#aboutplugins) de l’éditeur de texte enrichi. You can specify the [ `sourceedit` feature on the `misctools` plugin](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Use the `sourceedit` feature carefully. Les fautes de frappe et/ou les fonctions non prises en charge peuvent entraîner d’autres problèmes.

## Ajout de la prise en charge des éléments et attributs HTML supplémentaires {#adding-support-for-additional-html-elements-and-attributes}

Pour étendre davantage les fonctions d’accessibilité d’AEM, vous pouvez étendre les composants existants (par exemple, les composants **Text** et **Table**) en fonction de l’éditeur de texte enrichi avec des éléments et attributs supplémentaires.

The following procedure illustrates how to extend the **Table** component with a **Caption** element that provides information about a data table to assistive technology users:

### Exemple - Ajout de la légende à la boîte de dialogue Propriétés du tableau {#example-adding-the-caption-to-the-table-properties-dialog}

Dans le constructeur de l’élément `TablePropertiesDialog`, ajoutez un champ de saisie de texte supplémentaire utilisé pour modifier la légende. Note that `itemId` must be set to `caption` (i.e. the DOM attribute’s name) to automatically handle its content.

Dans le composant **Table**, vous devez définir ou supprimer explicitement l’attribut vers/depuis l’élément DOM. La valeur est transmise par la boîte de dialogue dans l’objet `config`. Notez que les attributs DOM doivent être définis/supprimés à l’aide des méthodes `CQ.form.rte.Common` correspondantes (`com` est un raccourci de `CQ.form.rte.Common`) pour éviter les pièges courants des mises en œuvre de navigateur.

>[!NOTE]
>
>Cette procédure convient uniquement à l’IU classique.

### Instructions détaillées {#step-by-step-instructions}

1. Démarrez CRXDE Lite. Par exemple : [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copier:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   vers :

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Vous devrez peut-être créer des dossiers intermédiaires si ceux-ci n’existent pas déjà.

1. Copier:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   vers :

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

1. Add the following code at the end of the `transferConfigToTable` method:

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

1. Save your changes using **Save All…**

>[!NOTE]
>
>Le champ de texte brut n’est pas le seul type d’entrée autorisé pour la valeur de l’élément de légende. Any ExtJS widget, that provides the caption’s value through its `getValue()` method, could be used.
>
>Pour ajouter des fonctionnalités de modification pour d’autres éléments et attributs, assurez-vous à la fois :
>
>* The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
>* Que l’attribut est défini et/ou supprimé sur l’élément DOM de manière explicite (`Table`).


>[!MORELIKETHIS]
>
>* [Guide rapide relatif à WCAG 2.0](/help/managing/qg-wcag.md)
>* [Création d’un contenu accessible (conformité WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)

