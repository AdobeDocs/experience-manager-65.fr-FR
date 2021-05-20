---
title: Incorporation d’un formulaire adaptatif ou d’une communication interactive dans une application d’une seule page AEM Sites
seo-title: Incorporation de formulaires adaptatifs ou de communications interactives dans des pages AEM Sites
description: Incorporer des formulaires adaptatifs ou une communication interactive dans des pages AEM Sites. Les utilisateurs peuvent remplir et envoyer des formulaires sans quitter la page Sites.
seo-description: Vous pouvez incorporer des formulaires adaptatifs ou une communication interactive dans des pages AEM Sites. Les utilisateurs peuvent remplir et envoyer des formulaires sans quitter la page Sites.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Formulaires adaptatifs
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 13%

---

# Incorporation d’un formulaire adaptatif ou d’une communication interactive dans une application d’une seule page AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Présentation {#overview}

AEM Forms permet aux développeurs de formulaires d’incorporer facilement des formulaires adaptatifs et des communications interactives dans une application à page unique AEM Sites (SPA). Le formulaire adaptatif incorporé et la communication interactive sont entièrement fonctionnels et les utilisateurs peuvent remplir et envoyer le formulaire sans quitter la page. Il permet à l’utilisateur de rester dans le contexte d’autres éléments de la page web et d’interagir simultanément avec le formulaire adaptatif ou la communication interactive.

Dans l’application d’une seule page AEM Sites, vous pouvez ajouter un formulaire adaptatif ou une communication interactive à l’aide du [composant de conteneur AEM Forms SPA](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Il s’agit d’un composant AEM Forms pour AEM Sites SPA que vous pouvez ajouter à votre page Sites.

Pour plus d’informations sur l’incorporation d’un formulaire adaptatif dans une AEM Sites non SPA, voir [Incorporation d’un formulaire adaptatif ou d’une communication interactive dans la page AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Prérequis {#prerequisites}

Pour incorporer un formulaire adaptatif ou une communication interactive dans un site d’AEM SPA à l’aide du composant Conteneur AEM Forms, vérifiez que vous avez installé :

* Java SE Development Kit 8 ou version ultérieure
* Apache Maven 3.3.1 ou version ultérieure
* AEM instance d’auteur
* [Module complémentaire AEM Forms 6.4.2 ](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) sur l’instance d’auteur

## Installer le composant Conteneur AEM Forms SPA {#install-aem-forms-spa-container-component}

Exécutez les étapes suivantes pour installer le composant Conteneur AEM Forms SPA :

1. [Cloner ou télécharger le composant AEM Forms pour SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installez le composant AEM Forms pour SPA. Les instructions d’installation du composant sont disponibles dans le fichier [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) .

   Le composant comprend un [exemple de composant React](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) qui peut être utilisé pour intégrer SPA composant de conteneur à un projet SPA basé sur React.

1. [Cloner ou télécharger un projet](https://github.com/adobe/aem-sample-we-retail-journal) de SPA basé sur React.
1. Intégrez SPA composant de conteneur à un projet SPA basé sur React en suivant les instructions disponibles dans le fichier [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) .

   Après avoir installé le composant Conteneur AEM Forms SPA et l’intégration du composant à un projet SPA basé sur React, vous pouvez incorporer des formulaires adaptatifs et des communications interactives dans la page AEM Sites.

## Incorporation d’un formulaire adaptatif ou d’une communication interactive {#af-component}

Pour incorporer un formulaire adaptatif ou une communication interactive à l’aide d’AEM Forms pour SPA composant Conteneur :

1. Ouvrez la page AEM sites, en mode d’édition, dans laquelle vous souhaitez incorporer un formulaire adaptatif ou une communication interactive.
1. Insérez le composant **AEM Formulaire pour SPA** sur la page à l’aide de l’une des options suivantes :

   * Appuyez sur le conteneur de mises en page sur la page Sites, appuyez sur **+** et sélectionnez le composant **AEM Formulaire pour SPA**.

   * Dans le panneau Explorateur de composants, faites glisser et déposez le composant **AEM Formulaire pour SPA** sur la page.
   * Recherchez un formulaire adaptatif ou une communication interactive dans le navigateur Ressources et faites-le glisser sur la page Sites. Il incorpore le formulaire dans une AEM Forms pour SPA conteneur de composants.

   >[!NOTE]
   >
   >Le rendu de plusieurs composants de conteneur AEM Forms SPA sur une page n’est pas pris en charge. Vous pouvez avoir plusieurs conteneurs AEM Forms SPA sur une page, mais un seul composant est rendu à la fois. Assurez-vous qu’un seul composant est visible sur une page pour éviter les incohérences.

1. Appuyez sur le composant Conteneur AEM Forms SPA incorporé dans la page Sites, puis appuyez sur ![settings_icon](assets/settings_icon.png) dans la barre d’actions. La boîte de dialogue **Modifier le conteneur AEM Forms SPA** s’ouvre.
1. Dans la boîte de dialogue **Modifier le conteneur AEM Forms** , spécifiez ce qui suit :

   * **Type d’actif :** sélectionnez le type d’actif à incorporer. Les options sont **Formulaire adaptatif** et **Communication interactive**

   * **Chemin d’accès** à la ressource : Recherchez et sélectionnez le formulaire adaptatif ou la communication interactive à incorporer. Le champ est automatiquement renseigné si un formulaire adaptatif ou une communication interactive est inséré à l’aide du navigateur Ressources.
   * **Canal**  (communication interactive uniquement) : Sélectionnez le type de canal interactif à incorporer. Les options sont **Canal Web** et **Canal d’impression**.

   * **Thème** : Sélectionnez un thème qui définit le style des composants de votre formulaire adaptatif ou de votre communication interactive. Style comprend des propriétés d’aspect, comme le style de police, la couleur d’arrière-plan, les dimensions et l’alignement.

1. Appuyez sur ![done_icon](assets/done_icon.png) pour enregistrer les paramètres. Le formulaire adaptatif ou la communication interactive est désormais incorporé à la page.

## Publier le formulaire adaptatif incorporé et la communication interactive {#publish-embedded-adaptive-form-and-interactive-communication}

Examinez les scénarios suivants pour publier une ressource incorporée (formulaire adaptatif ou communication interactive) sur la page AEM Sites :

* Si vous publiez la page AEM Sites pour la première fois et qu’elle comprend un formulaire adaptatif ou une communication interactive incorporés, publiez la page Sites et la ressource incorporée.
* Si vous avez modifié uniquement le formulaire adaptatif ou la communication interactive incorporés dans une page Sites publiée, publiez la ressource d’origine et les modifications sont répercutées dans la page Sites publiée. La page Sites publiée comprend une référence à la ressource et ne nécessite pas de republier la page.
* Si vous avez modifié la page Sites et le formulaire adaptatif ou la communication interactive incorporés, republiez la page Sites et la ressource incorporée.

## Modifier le formulaire adaptatif incorporé et la communication interactive {#modify-embedded-adaptive-form-and-interactive-communication}

AEM page de sites conserve une référence au formulaire adaptatif et à la communication interactive dans le conteneur AEM Forms. Par conséquent, toutes les configurations et propriétés, telles que le thème, les styles et l’action d’envoi, configurées dans le formulaire adaptatif d’origine et la communication interactive, sont conservées dans le formulaire adaptatif incorporé et la communication interactive.

Pour modifier toute configuration ou propriété du formulaire adaptatif incorporé et de la communication interactive, effectuez l’une des opérations suivantes.

* Ouvrez le formulaire d’origine dans les formulaires adaptatifs ou la communication interactive dans les éditeurs respectifs et modifiez-le.
* Appuyez sur le formulaire adaptatif ou la communication interactive dans la page Sites en mode d’édition, puis appuyez sur **Modifier dans une nouvelle fenêtre**. Le formulaire d’origine s’ouvre en mode d’édition.

## Éléments à prendre en compte et bonnes pratiques {#considerations-and-best-practices}

Gardez les points suivants à l’esprit lorsque vous incorporez des formulaires adaptatifs à des pages de sites AEM :

* L’en-tête et le pied de page du formulaire d’origine ne sont pas intégrés dans le formulaire incorporé.
* Les brouillons et les envois de formulaires incorporés sont pris en charge et visibles dans les onglets Brouillons et Formulaires envoyés du portail de formulaires.
* L’action Envoyer configurée sur le formulaire d’origine est conservée dans le formulaire incorporé.
* Le ciblage d’expérience et les tests A/B configurés sur le formulaire d’origine ne fonctionnent pas dans le formulaire incorporé. Cependant, vous pouvez utiliser le ciblage d’expérience sur la page Sites pour présenter différents formulaires en fonction des profils utilisateur.
* Si vous avez configuré Adobe Analytics pour le formulaire d’origine, les données d’analyse du formulaire incorporé seront capturées dans Adobe Analytics. En revanche, elles ne seront pas disponibles dans le rapport d’analyse des formulaires.
