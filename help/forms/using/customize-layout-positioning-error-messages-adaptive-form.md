---
title: Personnalisation de la disposition et de la position des messages d’erreur d’un formulaire adaptatif
seo-title: Personnalisation de la disposition et de la position des messages d’erreur d’un formulaire adaptatif
description: 'Vous pouvez personnaliser la disposition et la position des messages d’erreur d’un formulaire adaptatif. '
seo-description: 'Vous pouvez personnaliser la disposition et la position des messages d’erreur d’un formulaire adaptatif. '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 87%

---


# Personnalisation de la disposition et de la position des messages d’erreur d’un formulaire adaptatif{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

Vous pouvez personnaliser la disposition et la position des messages d’erreur d’un formulaire adaptatif. Vous pouvez exécuter les personnalisations suivantes :

* Personnaliser l’emplacement et la disposition de la légende d’un champ sans apporter de modifications aux propriétés CSS correspondantes
* Personnalisation de la position des messages d’erreur intégrés
* Personnalisation du contenu d’un indicateur d’aide dynamique
* Personnaliser la position des composants de champ (légende, widget, brève description, longue description et composants d’indicateur d’aide) sans apporter de modifications aux propriétés CSS correspondantes

## Personnalisation de la disposition des champs {#customize-layout-of-fields}

Vous pouvez personnaliser la disposition d’un champ spécifique ou de tous les champs pour modifier la position de la légende et des messages d’erreur. Effectuez les étapes suivantes pour appliquer une disposition personnalisée à un champ :

### Personnalisation de la disposition d’un champ spécifique  {#customize-layout-of-a-single-field}

Effectuez les étapes suivantes pour appliquer une disposition personnalisée à un champ spécifique :

1. Ouvrez le formulaire en mode **Style**. Pour ouvrir le formulaire en mode style, dans la barre d’outils de la page, appuyez sur ![liste déroulante de trame](assets/canvas-drop-down.png) > **Style**.
1. Dans la barre latérale, sous **Objets de formulaire**, sélectionnez le champ et appuyez sur le bouton Modifier ![bouton-modifier](assets/edit-button.png).
1. Sélectionnez l’état du champ que vous souhaitez personnaliser, puis spécifiez le style de cet état.

   ![Spécification du style intégré d’un champ](assets/edit-error-state.png)

### Personnalisation de la disposition de tous les champs d’un formulaire {#customize-layout-of-all-the-fields-of-a-form}

Avec AEM Forms, vous pouvez désormais créer un thème et l’appliquer à votre formulaire. L’éditeur de thèmes vous permet de spécifier le style des composants de formulaire dans un seul et même endroit. Lorsque vous créez un thème, vous spécifiez le style au niveau du composant. Pour plus d’informations sur les thèmes, consultez la section [Thèmes dans AEM Forms](../../forms/using/themes.md).

Créez un thème à l’aide de l’éditeur de thèmes pour personnaliser la mise en forme de tous les champs du formulaire. Après avoir créé un thème, effectuez les étapes suivantes pour l’appliquer à un formulaire :

1. Ouvrez votre formulaire en mode d’édition.
1. En mode d’édition, sélectionnez un composant, puis appuyez sur ![niveau champ](assets/field-level.png) > **Conteneur de formulaire adaptatif**, puis sur ![cmppr](assets/cmppr.png).
1. Dans la barre latérale, sous Thème de formulaire adaptatif, sélectionnez le thème que vous avez créé à l’aide de l’éditeur de thèmes.

## Création d’une disposition de champ personnalisée  {#create-a-custom-field-layout}

1. Ouvrez CRXDE Lite. L’URL par défaut est https://&#39;[server]:[port]&#39;/crx/de.
1. Copiez une disposition de champ du nœud /libs/fd/af/layouts/field (par exemple, defaultFieldLayout) vers le nœud /apps (par exemple, /apps/af-field-layout).
1. Renommez le nœud copié et le fichier defaultFieldLayout.jsp. Par exemple, errorOnRight.jsp.

1. Modifiez la valeur des propriétés qtip et jcr:description du noeud copié. Par exemple, redéfinissez la valeur des propriétés sur Erreur sur la droite

1. Pour ajouter de nouveaux styles et un nouveau comportement, créez une bibliothèque cliente sous le nœud /etc node.

   Par exemple, créez à l’emplacement /etc/af-field-layout-clientlib le nœud client-library. Ajoutez la propriété de catégories avec la valeur af.field.errorOnRight et le fichier style.less avec le code suivant :

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. Pour améliorer l’apparence et le comportement, incluez la bibliothèque client créée dans le fichier de dispositiion (errorOnRight.jsp).
1. Ouvrez la boîte de dialogue de modification et sélectionnez l’onglet **Style**. Dans la liste déroulante **Configurer la disposition de champ**, sélectionnez la disposition nouvellement créée, puis cliquez sur **OK**.

Le package ErrorOnRight.zip contient le code permettant d’afficher les messages d’erreur du côté droit des champs.

[Obtenir le fichier](assets/erroronright.zip)
