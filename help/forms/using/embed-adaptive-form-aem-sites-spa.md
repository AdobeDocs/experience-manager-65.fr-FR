---
title: Incorporation d’un formulaire adaptatif ou d’une communication interactive dans une application AEM Sites à une seule page
seo-title: Incorporer des formulaires adaptatifs ou des communications interactives dans des pages AEM Sites
description: Incorporer des formulaires adaptatifs ou des communications interactives dans des pages AEM Sites. Les utilisateurs peuvent remplir et envoyer des formulaires sans quitter la page Sites.
seo-description: Vous pouvez incorporer des formulaires adaptatifs ou des communications interactives dans des pages AEM Sites. Les utilisateurs peuvent remplir et envoyer des formulaires sans quitter la page Sites.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 11%

---


# Embed an adaptive form or Interactive Communication in AEM Sites Single Page Application{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Présentation {#overview}

aem forms permet aux développeurs de formulaires d’incorporer aisément des formulaires adaptatifs et des communications interactives dans une application à page unique AEM Sites (SPA). Le formulaire adaptatif incorporé et la communication interactive sont entièrement fonctionnels et les utilisateurs peuvent remplir et envoyer le formulaire sans quitter la page. Il permet à l’utilisateur de rester dans le contexte d’autres éléments de la page Web et d’interagir simultanément avec le formulaire adaptatif ou la communication interactive.

Dans l’application AEM Sites Single Page, vous pouvez ajouter un formulaire adaptatif ou une communication interactive à l’aide du composant [Conteneur](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[AEM Forms SPA.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Il s’agit d’un composant AEM Forms pour les ZPS AEM Sites que vous pouvez ajouter à votre page Sites.

Pour plus d’informations sur l’incorporation d’un formulaire adaptatif dans une AEM Sites non SPA, voir [Incorporation d’un formulaire adaptatif ou communication interactive dans la page](/help/forms/using/embed-adaptive-form-aem-sites.md)AEM Sites.

## Conditions préalables {#prerequisites}

Pour incorporer un formulaire adaptatif ou une communication interactive dans une application d’application d’une seule page à l’aide du composant Conteneur d’application d’une seule page à l’aide de AEM Forms, assurez-vous que vous avez installé les éléments suivants :

* Java SE Development Kit 8 ou version ultérieure
* Apache Maven 3.3.1 ou version ultérieure
* aem instance d’auteur
* [Package](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) de module complémentaire AEM Forms 6.4.2 sur l’instance d’auteur

## Installer le composant Conteneur AEM Forms SPA {#install-aem-forms-spa-container-component}

Exécutez les étapes suivantes pour installer le composant Conteneur AEM Forms SPA :

1. [Cloner ou télécharger le composant AEM Forms pour l’application d’une seule page](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installez le composant AEM Forms pour l’application d’une seule page. Les instructions d’installation du composant sont disponibles dans le fichier [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) .

   Le composant comprend un [exemple de composant](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) Réagir qui peut être utilisé pour intégrer le composant conteneur SPA à un projet SPA basé sur Réagir.

1. [Cloner ou télécharger un projet](https://github.com/adobe/aem-sample-we-retail-journal)SPA basé sur React.
1. Intégrez le composant de conteneur d’application d’une seule page à un projet d’application d’une seule page en utilisant les instructions du fichier [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) .

   Après avoir installé le composant Conteneur d’application d’une seule page AEM Forms et intégré le composant à un projet d’application d’une seule page, vous pouvez incorporer des formulaires adaptatifs et des communications interactives dans la page AEM Sites.

## Incorporation d’un formulaire adaptatif ou d’une communication interactive {#af-component}

Pour incorporer un formulaire adaptatif ou une communication interactive à l’aide du composant de Conteneur AEM Forms for SPA :

1. Ouvrez la page de sites AEM, en mode d’édition, dans laquelle vous souhaitez incorporer un formulaire adaptatif ou une communication interactive.
1. Insérez le composant Formulaire **AEM pour l’application d’une seule page** à l’aide de l’une des options suivantes :

   * Appuyez sur le conteneur de mise en page de la page Sites, appuyez sur **+** et sélectionnez le composant Formulaire **AEM pour l’application d’une seule page** .

   * From the Component browser panel, drag-drop the **AEM Form for SPA** component on the page.
   * Recherchez un formulaire adaptatif ou une communication interactive dans le navigateur Ressources et faites-le glisser sur la page Sites. Il incorpore le formulaire dans un conteneur de composant AEM Forms for SPA.

   >[!NOTE]
   >
   >Le rendu de plusieurs composants de Conteneur AEM Forms SPA sur une page n’est pas pris en charge. Vous pouvez avoir plusieurs Conteneurs AEM Forms SPA sur une page, mais un seul composant est rendu à la fois. Assurez-vous qu’un seul composant est visible sur une page pour éviter les incohérences.

1. Tap the embedded AEM Forms SPA Container component in the sites page, and then tap ![settings_icon](assets/settings_icon.png) on the action bar. The **Edit AEM Forms SPA Container** dialog opens.
1. In the **Edit AEM Forms Container** dialog, specify the following:

   * **Type d’actif :** sélectionnez le type d’actif à incorporer. The options are **Adaptive Form** and **Interactive Communication**

   * **Chemin d’accès** au fichier : Recherchez et sélectionnez le formulaire adaptatif ou la communication interactive à incorporer. Le champ est renseigné automatiquement si un formulaire adaptatif ou une communication interactive est inséré à l’aide de l’explorateur Ressources.
   * **Canal** (communication interactive uniquement) : Sélectionnez le type de canal interactif à incorporer. Les options sont Canal **** Web et Canal **** Imprimer.

   * **Thème**: Sélectionnez un thème qui définit la mise en forme des composants de votre formulaire adaptatif ou de votre communication interactive. Style comprend des propriétés d’aspect telles que le style de police, la couleur d’arrière-plan, les dimensions et l’alignement.

1. Tap ![done_icon](assets/done_icon.png) to save the settings. Le formulaire adaptatif ou la communication interactive est désormais incorporé à la page.

## Publier le formulaire adaptatif incorporé et la communication interactive {#publish-embedded-adaptive-form-and-interactive-communication}

Examinez les scénarios suivants pour publier une ressource incorporée (formulaire adaptatif ou communication interactive) sur la page AEM Sites :

* Si vous publiez la page AEM Sites pour la première fois et qu’elle comprend un formulaire adaptatif incorporé ou une communication interactive, publiez la page Sites et la ressource incorporée.
* Si vous avez modifié uniquement le formulaire adaptatif incorporé ou la communication interactive dans une page de sites publiée, publiez le fichier d’origine et les modifications sont répercutées dans la page de sites publiée. La page Sites publiée contient une référence à la ressource et ne nécessite pas de republier la page.
* Si vous avez modifié la page Sites et le formulaire adaptatif incorporé ou la communication interactive, republiez la page Sites et la ressource incorporée.

## Modification du formulaire adaptatif incorporé et de la communication interactive {#modify-embedded-adaptive-form-and-interactive-communication}

La page AEM sites conserve une référence au formulaire adaptatif et à la communication interactive dans le Conteneur AEM Forms. Par conséquent, toutes les configurations et propriétés, telles que le thème, les styles et l’action d’envoi, configurées dans le formulaire adaptatif d’origine et la communication interactive, sont conservées dans le formulaire adaptatif incorporé et la communication interactive.

Pour modifier toute configuration ou propriété du formulaire adaptatif incorporé et de la communication interactive, effectuez l’une des opérations suivantes.

* Ouvrez le formulaire d’origine dans les formulaires adaptatifs ou dans la communication interactive dans les éditeurs respectifs et modifiez-le.
* Tap the adaptive form or Interactive Communication from within the Sites page in edit mode and then tap **Edit in a new window**. Le formulaire d’origine s’ouvre en mode d’édition.

## Eléments à prendre en compte et bonnes pratiques {#considerations-and-best-practices}

Gardez les points suivants à l’esprit lorsque vous incorporez des formulaires adaptatifs à des pages de sites AEM :

* L’en-tête et le pied de page du formulaire d’origine ne sont pas intégrés dans le formulaire incorporé.
* Les brouillons et les envois de formulaires incorporés sont pris en charge et visibles dans les onglets Brouillons et Formulaires envoyés du portail de formulaires.
* L’action Envoyer configurée sur le formulaire d’origine est conservée dans le formulaire incorporé.
* Le ciblage d’expérience et les tests A/B configurés sur le formulaire d’origine ne fonctionnent pas dans le formulaire incorporé. Cependant, vous pouvez utiliser le ciblage d’expérience sur la page Sites pour présenter différents formulaires en fonction des profils d’utilisateur.
* Si Adobe Analytics est configuré pour le formulaire d’origine, les données d’analyse du formulaire incorporé sont capturées dans Adobe Analytics. En revanche, elles ne seront pas disponibles dans le rapport d’analyse des formulaires.

