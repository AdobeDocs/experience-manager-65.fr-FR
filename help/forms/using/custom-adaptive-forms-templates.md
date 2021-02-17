---
title: Création d’un modèle de formulaire adaptatif personnalisé
seo-title: Création d’un modèle de formulaire adaptatif personnalisé
description: Cet article décrit comment créer des modèles de formulaire adaptatif personnalisés.
seo-description: Cet article décrit comment créer des modèles de formulaire adaptatif personnalisés.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 76%

---


# Création d’un modèle de formulaire adaptatif personnalisé{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms a introduit les modèles dynamiques. Vous pouvez utiliser l’éditeur de modèles de sites AEM pour [créer ou modifier des modèles dynamiques ](../../forms/using/template-editor.md). Les modèles mentionnés dans l’article ci-dessous sont des modèles statiques. Ceux-ci ne sont pas disponibles sur une installation par défaut. [Installez le package de compatibilité](../../forms/using/compatibility-package.md) pour obtenir ces modèles sur votre environnement.

## Conditions préalables {#prerequisites}

* Compréhension de l’AEM [Modèle de page](/help/sites-authoring/templates.md) et [Création de formulaires adaptatifs](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Présentation des [bibliothèques côté client](/help/sites-developing/clientlibs.md) AEM

## Modèle de formulaire adaptatif {#adaptive-form-template}

Un modèle de formulaire adaptatif est un modèle de page AEM spécialisé avec des propriétés et une structure de contenu qui est utilisé pour créer un formulaire adaptatif. Il possède des dispositions, des styles et une structure de contenu initiale de base préconfigurés.

Une fois que vous avez créé un formulaire, les modifications apportées à la structure de contenu du modèle d’origine ne sont pas répercutées dans le formulaire.

## Modèles de formulaire adaptatif par défaut {#default-adaptive-form-templates}

AEM Quickstart fournit les modèles de formulaires adaptatifs suivants :

* Modèle de questionnaire : Vous permet de créer un formulaire adaptatif d’une seule page à l’aide de la disposition réactive dont plusieurs colonnes sont configurées. La disposition s’ajuste automatiquement selon les dimensions des différents écrans sur lesquels vous souhaitez afficher le formulaire.
* Modèle Simple Enrollment : Permet de créer un formulaire adaptatif à plusieurs étapes à l’aide d’une disposition d’assistant. Dans cette disposition, vous pouvez spécifier une expression d’achèvement d’étape pour chaque étape, qui est validée avant que l’assistant ne passe à l’étape suivante.
* Modèle d’inscription avec onglets : Permet de créer un formulaire adaptatif à plusieurs onglets à l’aide d’une disposition d’onglets sur la gauche, dans laquelle vous pouvez consulter les onglets de manière aléatoire.
* Modèle Inscription avancée : permet de créer un formulaire avec plusieurs onglets et l’assistant. Il utilise une disposition d’onglets sur la gauche qui vous permet de consulter les onglets dans n’importe quel ordre. Il utilise les services d’Adobe Document Cloud eSign pour la signature et la vérification. 
* Modèle vierge : permet de créer un formulaire sans aucun contenu d’en-tête, de pied de page et initial. Vous pouvez ajouter des composants tels que des zones de texte, des boutons et des images. Le modèle vierge permet de créer un formulaire que vous pouvez [incorporer dans des pages du site AEM](/help/forms/using/embed-adaptive-form-aem-sites.md).

Ces modèles possèdent la propriété `sling:resourceType` définie sur le composant de page correspondant. Le composant de page effectue le rendu de la page CQ contenant le conteneur du formulaire adaptatif, qui à son tour effectue le rendu du formulaire adaptatif.

Le tableau suivant montre l’association entre les modèles et le composant de page :

<table>
 <tbody>
  <tr>
   <td><p><strong>Template</strong></p> </td>
   <td><p><strong>Composant de page</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## Création d’un modèle de formulaire adaptatif à l’aide de l’éditeur de modèle  {#creating-an-adaptive-form-template-using-template-editor}

Vous pouvez spécifier la structure et le contenu initial d’un formulaire adaptatif à l’aide de l’éditeur de modèles. Par exemple, vous souhaitez que tous les auteurs de formulaire aient quelques zones de texte, des boutons de navigation, ainsi qu’un bouton permettant de soumettre un formulaire d’inscription. Vous pouvez créer un modèle que les auteurs peuvent utiliser pour créer un formulaire compatible à d’autres formulaires d’inscription. L’éditeur de modèles AEM permet d’effectuer les opérations suivantes :

* Ajout de composants d’en-tête et de pied de page d’un formulaire dans le calque de structure
* Fournissez le contenu initial pour le formulaire. 
* Spécifiez un thème.
* Spécifiez des actions telles que l’envoi, la réinitialisation et la navigation.

Pour plus d’informations, voir [Éditeur de modèle](../../forms/using/template-editor.md).

## Création d’un modèle de formulaire adaptatif à partir de CRXDE {#creating-an-adaptive-form-template-from-crxde}

Au lieu d’utiliser les modèles disponibles, vous pouvez créer un modèle et l’utiliser pour créer des formulaires adaptatifs. Les modèles personnalisés reposent sur différents composants de page qui référencent les conteneurs de formulaire adaptatif et les éléments de page comme les en-tête et pied de page.

Vous pouvez créer ces composants à l’aide du composant de page base de votre site Web. Vous pouvez également étendre le composant de page du formulaire adaptatif que les modèles prêts à l’emploi utilisent.

Pour créer un modèle personnalisé comme simpleEnrollmentTemplate, suivez la procédure ci-après.

1. Accédez à CRXDE Lite sur votre instance de création.

1. Sous le répertoire /apps, créez la structure des dossiers pour votre application. Si le nom de l’application est par exemple mycompany, créez un dossier portant ce nom. En règle générale, le dossier d’application contient les répertoires d’installation, de composants, de configuration, de modèles et src. Dans le cadre de cet exemple, créez les dossiers de composants, de configuration et de modèles.

1. Accédez au dossier /libs/fd/af/templates.
1. Copiez le noeud `simpleEnrollmentTemplate`.
1. Accédez au dossier /apps/mycompany/templates. Cliquez avec le bouton droit dessus et sélectionnez **[!UICONTROL Coller]**.
1. Si nécessaire, renommez le nœud de modèle que vous avez copié. Renommez-le par exemple en tant qu’enrollment-template.

1. Accédez à l’emplacement /apps/mycompany/templates/enrollment-template.

1. Modifiez les propriétés `jcr:title` et `jcr:description` du noeud `jcr:content` pour distinguer le modèle du modèle que vous avez copié.

1. Le noeud `jcr:content` du modèle modifié contient les composants `guideContainer` et `guideformtitle`. Le composant `guideContainer` est le conteneur qui contient le formulaire adaptatif. Le composant `guideformtitle` affiche le nom, la description et d’autres informations sur l’application.

   A la place du composant `guideformtitle`, vous pouvez inclure un composant personnalisé ou le composant `parsys`. Par exemple, supprimez le composant `guideformtitle` et ajoutez un composant personnalisé ou le nœud de composant `parsys`. Vérifiez que la propriété `sling:resourceType` du composant référence ce dernier et que la même propriété est définie dans le fichier `component.jsp` de la page.

1. Accédez à l’emplacement /apps/mycompany/templates/enrollment-template/jcr:content.

1. Ouvrez l’onglet **[!UICONTROL Properties]** (Propriétés) et modifier la valeur de la propriété `cq:designPath` en /etc/designs/mycompany.

1. Créez maintenant un nœud /etc/designs/mycompany pour le `cq:Page`type 

## Création d’un composant de page de formulaire adaptatif {#create-an-adaptive-form-page-component}

Le modèle personnalisé possède les mêmes styles que le modèle par défaut, car il référence le composant de page /libs/fd/af/components/page/base. Vous pouvez trouver la référence au composant en tant que propriété `sling:resourceType` définie sur le nœud /apps/mycompany/templates/enrollment-template/jcr:content. Dans la mesure où base est un composant de produit principal, ne modifiez pas ce composant.

1. Accédez au nœud /apps/mycompany/templates/enrollment-template/jcr:content et modifiez la valeur de la propriété `sling:resourceType` en /apps/mycompany/components/page/enrollmentpage
1. Copiez le nœud /libs/fd/af/components/page/base dans le dossier /apps/mycompany/components/page.

1. Renommez le composant copié en `enrollmentpage`.

1. **(Uniquement si vous disposez déjà d’une page de contenu)** Effectuez les étapes suivantes (a-d), si vous disposez d’un  `contentpage`composant existant pour votre site Web. Si vous ne disposez pas d&#39;un composant `contentpage`existant pour votre site Web, vous pouvez laisser la propriété `resourceSuperType`pour pointer vers la page de base prête à l&#39;emploi.

   1. Pour le noeud `enrollmentpage`, définissez la valeur de la propriété `sling:resourceSuperType` sur mycompany/components/page/contentpage. Le composant `contentpage` est le composant de page base de votre site. D’autres composants de page peuvent l’étendre. Supprimez les fichiers de script sous `enrollmentpage`, sauf `head.jsp`, `content.jsp` et `library.jsp`. Le composant `sling:resourceSuperType`, qui est `contentpage` dans ce cas, inclut tous ces scripts. Les en-têtes, dont la barre de navigation et le pied de page, sont hérités du composant `contentpage`

   1. Ouvrez le fichier `head.jsp`.

      Le fichier JSP contient la ligne `<cq.include script="library.jsp"/>`.

      Le fichier `library.jsp` contient la bibliothèque cliente `guide.theme.simpleEnrollment`, qui comporte les styles du formulaire adaptatif.

      Le composant de page `enrollmentpage` possède un fichier `head.jsp` exclusif qui remplace le fichier `head.jsp` du composant `contentpage`.

   1. Incluez tous les scripts du fichier `head.jsp` du composant `contentpage` dans le fichier `head.jsp` du composant `enrollmentpage`.
   1. Dans le script `content.jsp`, vous pouvez ajouter du contenu de page ou des références supplémentaires à d’autres composants inclus lors du rendu de la page. Par exemple, si vous ajoutez l’`applicationformheader` du composant personnalisé, veillez à ajouter la référence suivante au composant dans le fichier JSP :

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      De même, si vous ajoutez un composant `parsys` à la structure du nœud de modèle, incluez également le composant personnalisé.

## Création d&#39;une bibliothèque cliente de formulaire adaptatif {#creating-an-adaptive-form-client-library}

Le fichier `head.jsp` du composant `enrollmentpage` du nouveau modèle comprend une bibliothèque cliente `guide.theme.simpleEnrollment`. Le modèle par défaut utilise également cette bibliothèque cliente. Modifiez le style du nouveau modèle à l’aide de l’une de ces méthodes :

* Définissez un thème personnalisé et remplacez le thème par défaut `guide.theme.simpleEnrollment` par celui-ci.
* Définissez une nouvelle bibliothèque cliente sous /etc/designs/mycompany. Incluez la bibliothèque cliente après l’entrée de thème par défaut dans la page jsp. Incluez tous les styles remplacés et les fichiers JavaScript supplémentaires dans cette bibliothèque cliente.

>[!NOTE]
>
>Un thème désigne une bibliothèque cliente incluse dans le composant de page utilisé pour effectuer le rendu d’un formulaire adaptatif. La bibliothèque cliente régit principalement l’aspect d’un formulaire adaptatif.

