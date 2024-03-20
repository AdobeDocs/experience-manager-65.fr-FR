---
title: Configurez l’éditeur de texte enrichi pour créer des pages web et des sites accessibles.
description: Configurez l’éditeur de texte enrichi pour créer des pages web et des sites accessibles.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 90%

---

# Configuration de l’éditeur de texte enrichi pour créer des pages web et des sites accessibles {#configure-rte-for-accessibility}

Adobe Experience Manager prend en charge de nombreuses fonctions d’accessibilité standard conformément à diverses normes d’accessibilité. En outre, l’équipe de développement peut personnaliser ou étendre des fonctionnalités permettant de créer du contenu accessible à l’aide de composants Experience Manager qui utilisent l’éditeur de texte enrichi (RTE).

Lors de la conception de pages web et de l’ajout de contenu aux pages, l’équipe de développement et les auteurs de contenu peuvent utiliser les fonctionnalités de l’éditeur de texte enrichi pour fournir des informations relatives à l’accessibilité. Par exemple, ajoutez des informations structurelles par le biais d’en-têtes et d’éléments de paragraphe.

Pour configurer et personnaliser ces fonctionnalités, [configurez les modules externes d’éditeur de texte enrichi](#configure-the-plugin-features) pour le composant. Par exemple, le module externe `paraformat` vous permet d’ajouter des éléments sémantiques de niveau bloc supplémentaires, y compris d’étendre le nombre de niveaux d’en-tête pris en charge au-delà des niveaux `H1`, `H2` et `H3` de base fournis par défaut.

L’éditeur de texte enrichi est disponible dans divers composants pour l’interface utilisateur tactile et l’interface utilisateur classique. Cependant, le premier composant à utiliser pour l’éditeur de texte enrichi est le composant **Texte** qui est disponible pour les deux interfaces. Les illustrations suivantes présentent l’éditeur de texte enrichi avec une plage de modules externes activés, y compris `paraformat` :

![Composant Texte (éditeur de texte enrichi) en mode plein écran dans l’IU optimisée pour les écrans tactiles](assets/chlimage_1-206.png)

*Image : composant Texte de l’interface utilisateur tactile*

![Boîte de dialogue Modifier (éditeur de texte enrichi) du composant Texte dans l’IU classique](assets/chlimage_1-207.png)

*Image : composant Texte de l’interface utilisateur classique*

Pour connaître les différences entre les fonctionnalités de l’éditeur de texte enrichi disponibles dans les différentes interfaces, consultez les [Modules externes et leurs fonctionnalités](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configuration des fonctionnalités de module externe {#configure-the-plugin-features}

Pour obtenir des instructions complètes sur la configuration de l’éditeur de texte enrichi, consultez la page [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md). Celle-ci couvre tous les problèmes, y compris les principales étapes :

* [Modules externes et leurs fonctionnalités](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Emplacements de configuration](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Activation d’un module externe et configuration de la propriété features](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configuration d’autres fonctionnalités de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

En configurant un module externe dans la sous-branche `rtePlugins` appropriée dans CRXDE Lite (voir image suivante), vous pouvez activer toutes les fonctionnalités ou certaines fonctionnalités spécifiques pour ce module externe.

![CRXDE Lite présentant un exemple de rtePlugin](assets/chlimage_1-208.png)

### Exemple : spécification des formats de paragraphes disponibles dans le champ de sélection de l’éditeur de texte enrichi {#example-specifying-paragraph-formats-available-in-rte-selection-field}

De nouveaux formats de bloc sémantique peuvent être mis à disposition pour sélection par :

1. Selon votre éditeur de texte enrichi, déterminez son [emplacement de configuration](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations) et accédez-y.
1. [Activation du champ de sélection Paragraphes](/help/sites-administering/rich-text-editor.md); par [activation du module externe](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Spécifiez les formats qui doivent être disponibles dans le champ de sélection Paragraphes .](/help/sites-administering/rich-text-editor.md).
1. Les formats de paragraphe sont ensuite à la disposition de l’auteur du contenu des champs de sélection dans l’éditeur de texte enrichi. Ils sont accessibles :

   * à l’aide du paragraphe pied-de-mouche dans l’IU optimisée pour les écrans tactiles ;
   * en utilisant le champ **Format** (sélecteur pop-up) dans l’IU classique.

Avec les éléments structurels disponibles dans l’éditeur de texte enrichi via les options de format de paragraphe, AEM constitue une bonne base pour le développement de contenu accessible. Les auteurs de contenu ne peuvent pas utiliser l’éditeur de texte enrichi pour formater la taille de la police ou les couleurs ou d’autres attributs associés, ce qui empêche toute création de formatage en ligne. À la place, ils doivent sélectionner les éléments structurels appropriés comme les en-têtes et utiliser des styles globaux choisis via l’option Styles. Cela garantit un balisage propre, de plus grandes options pour les utilisateurs qui naviguent avec leurs propres feuilles de style et du contenu correctement structuré.

## Utilisation de la fonction de modification de la source {#use-of-the-source-edit-feature}

Dans certains cas, les auteurs de contenu constateront qu’il est nécessaire d’examiner et d’ajuster le code source HTML créé à l’aide de l’éditeur de texte enrichi. Par exemple, un élément de contenu créé dans l’éditeur de texte enrichi peut nécessiter une mise en forme supplémentaire pour être conforme à la norme WCAG 2.0. Ceci peut s’effectuer avec l’option [Modification de la source](/help/sites-administering/rich-text-editor.md#aboutplugins) de l’éditeur de texte enrichi. Vous pouvez spécifier la fonction [`sourceedit` du module externe `misctools`](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilisez la fonction `sourceedit` avec prudence. Les fautes de frappe et/ou les fonctions non prises en charge peuvent entraîner d’autres problèmes.

## Ajout de la prise en charge d’éléments et d’attributs HTML supplémentaires {#add-support-for-more-html-elements-and-attributes}

Pour étendre davantage les fonctions d’accessibilité d’AEM, vous pouvez étendre les composants existants (par exemple, les composants **Texte** et **Tableau**) en fonction de l’éditeur de texte enrichi avec des éléments et attributs supplémentaires.

La procédure suivante explique comment étendre le composant **Tableau** avec un élément **Légende** qui fournit des informations sur un tableau de données aux utilisateurs de la technologie d’assistance :

### Exemple - Ajout de la légende à la boîte de dialogue Propriétés du tableau {#example-adding-the-caption-to-the-table-properties-dialog}

Dans le constructeur de l’élément `TablePropertiesDialog`, ajoutez un champ de saisie de texte supplémentaire utilisé pour modifier la légende. Notez que `itemId` doit être défini sur `caption` (c’est-à-dire le nom de l’attribut DOM) pour gérer automatiquement son contenu.

Dans le composant **Tableau**, vous devez définir ou supprimer explicitement l’attribut vers ou depuis l’élément DOM. La valeur est transmise par la boîte de dialogue dans l’objet `config`. Notez que les attributs DOM doivent être définis ou supprimés à l’aide des méthodes `CQ.form.rte.Common` correspondantes (`com` est un raccourci de `CQ.form.rte.Common`) pour éviter les pièges courants des mises en œuvre de navigateur.

>[!NOTE]
>
>Cette procédure convient uniquement à l’IU classique.

### Exemple : créer un HTML accessible lors de l’utilisation de la mise en évidence dans le texte {#create-accessible-html-for-text}

L’éditeur de texte enrichi peut utiliser les balises `strong` et `em` à la place de `b` et `i`. Ajoutez le noeud suivant en tant que frère au `uiSettings` et `rtePlugins` dans la boîte de dialogue.

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

1. Démarrez CRXDE Lite. Par exemple : [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copier :

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   vers :

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Vous devrez peut-être créer des dossiers intermédiaires si ceux-ci n’existent pas déjà.

1. Copier :

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

1. Ajoutez le code suivant à la fin de la méthode `transferConfigToTable` :

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

1. Enregistrez vos modifications à l’aide de la commande **Enregistrer tout**.

>[!NOTE]
>
>Le champ de texte brut n’est pas le seul type d’entrée autorisé pour la valeur de l’élément de légende. Vous pouvez utiliser n’importe quel widget ExtJS, qui fournit la valeur de la légende à l’aide de la méthode `getValue()`.
>
>Pour ajouter des fonctionnalités de modification pour d’autres éléments et attributs, assurez-vous à la fois :
>
>* Que la propriété `itemId` de chaque champ correspondant est définie sur le nom de l’attribut DOM approprié (`TablePropertiesDialog`).
>* Que l’attribut est défini et/ou supprimé sur l’élément DOM de manière explicite (`Table`).

>[!MORELIKETHIS]
>
>* [Guide rapide relatif à WCAG 2.0](/help/managing/qg-wcag.md)
>* [Création d’un contenu accessible (conformité WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)
