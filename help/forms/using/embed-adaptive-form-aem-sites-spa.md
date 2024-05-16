---
title: Incorporer un formulaire adaptatif ou une communication interactive dans une application dʼune seule page AEM Sites
description: Incorporez des formulaires adaptatifs ou une communication interactive dans des pages AEM Sites. Les utilisateurs peuvent remplir et envoyer des formulaires sans quitter les pages de Sites.
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1107'
ht-degree: 100%

---

# Incorporer un formulaire adaptatif ou une communication interactive dans une application dʼune seule page AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

## Vue d’ensemble {#overview}

AEM Forms permet aux équipes de développement de formulaires d’incorporer facilement des formulaires adaptatifs et des communications interactives dans une application monopage AEM Sites. Le formulaire adaptatif et la communication interactive incorporés fonctionnent parfaitement et les utilisateurs peuvent remplir et envoyer le formulaire sans quitter la page. Cela permet à l’utilisateur de rester dans le contexte des autres éléments de la page web et d’interagir simultanément avec le formulaire adaptatif ou la communication interactive.

L’application monopage AEM Sites vous permet dʼajouter un formulaire adaptatif ou une communication interactive à l’aide du [Composant Conteneur d’applications monopages d’AEM Forms](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Il s’agit d’un composant AEM Forms pour les SPA AEM Sites que vous pouvez ajouter à votre page Sites.

Pour plus d’informations sur l’incorporation d’un formulaire adaptatif dans une page AEM Sites non SPA, consultez la section [Incorporation d’un formulaire adaptatif ou d’une communication interactive dans une page AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Prérequis {#prerequisites}

Pour incorporer un formulaire adaptatif ou une communication interactive dans une SPA AEM Sites à l’aide du composant Conteneur SPA AEM Forms, vérifiez que les éléments suivants sont installés :

* Java SE Development Kit 8 ou version ultérieure
* Apache Maven (version 3.3.1 ou ultérieure)
* Instance dʼauteur AEM
* [Package de module complémentaire AEM Forms 6.4.2](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) sur l’instance d’auteur

## Installation du composant Conteneur SPA AEM Forms {#install-aem-forms-spa-container-component}

Pour installer le composant Conteneur SPA AEM Forms, procédez comme suit :

1. [Clonage ou téléchargement du composant AEM Forms pour SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installez le composant AEM Forms pour SPA. Les instructions d’installation du composant se trouvent dans le fichier [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   Le composant comprend un [exemple de composant React](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) qui peut être utilisé pour intégrer le composant Conteneur SPA à un projet SPA basé sur React.

1. [Clonez ou téléchargez un projet SPA basé sur React](https://github.com/adobe/aem-sample-we-retail-journal).
1. Intégrez le composant Conteneur SPA à un projet SPA basé sur React en suivant la procédure décrite dans le fichier [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa—editor).

   Une fois le composant Conteneur SPA AEM Forms installé et intégré à un projet SPA basé sur React, vous pouvez incorporer des formulaires adaptatifs et des communications interactives dans la page AEM Sites.

## Incorporation d’un formulaire adaptatif ou d’une communication interactive {#af-component}

Pour incorporer un formulaire adaptatif ou une communication interactive à l’aide du composant Conteneur SPA AEM Forms, procédez comme suit :

1. Ouvrez la page AEM Sites, en mode Édition, dans laquelle vous souhaitez incorporer un formulaire adaptatif ou une communication interactive.
1. Insérez le composant **AEM Form pour SPA** à l’aide de l’une des options suivantes :

   * Sélectionnez le conteneur de disposition sur la page Sites, puis **+** et choisissez le composant **AEM Form pour SPA**.

   * Depuis le panneau Explorateur des composants, faites glisser et déposez le composant **AEM Form pour SPA** sur la page.
   * Recherchez un formulaire adaptatif ou une communication interactive dans lʼexplorateur de ressources et effectuez une opération de glisser-déposer sur la page Sites. Le formulaire est ainsi incorporé dans un composant Conteneur AEM Forms pour SPA.

   >[!NOTE]
   >
   >Le rendu de plusieurs composants de conteneurs SPA AEM Forms sur une page nʼest pas pris en charge. Plusieurs conteneurs SPA AEM Forms peuvent être incorporés sur une page, mais un seul composant est rendu à la fois. Assurez-vous qu’un seul composant est visible sur une page pour éviter toute erreur.

1. Sélectionnez le composant Conteneur SPA AEM Forms sur la page Sites, puis ![settings_icon](assets/settings_icon.png) dans la barre d’action. La boîte de dialogue **Modifier le conteneur SPA AEM Forms** s’affiche.
1. Dans la boîte de dialogue **Modifier le conteneur AEM Forms**, précisez ce qui suit :

   * **Type de ressource :** sélectionnez le type de ressource à incorporer. Vous pouvez choisir entre **formulaire adaptatif** et **communication interactive**.

   * **Chemin d’accès à la ressource** : recherchez et sélectionnez le formulaire adaptatif ou la communication interactive à incorporer. Le champ se remplit automatiquement si un formulaire adaptatif ou une communication interactive est inséré à l’aide de lʼexplorateur de ressources.
   * **Canal** (Communication interactive uniquement) : sélectionnez le type de canal interactif à incorporer. Les options sont les suivantes : **Canal web** et **Canal d’impression**.

   * **Thème** : sélectionnez un thème qui définit le style des composants de votre formulaire adaptatif ou de votre communication interactive. Style comprend des propriétés d’aspect, comme le style de police, la couleur d’arrière-plan, les dimensions et l’alignement.

1. Sélectionnez ![done_icon](assets/done_icon.png) pour enregistrer les paramètres. Le formulaire adaptatif ou la communication interactive est maintenant incorporé à la page.

## Publier un formulaire adaptatif et une communication interactive incorporés {#publish-embedded-adaptive-form-and-interactive-communication}

Examinons les scénarios suivants pour publier une ressource incorporée (formulaire adaptatif ou communication interactive) sur une page AEM Sites :

* Si vous publiez la page AEM Sites pour la première fois et qu’elle inclut un formulaire adaptatif ou une communication interactive incorporés, publiez la page Sites et la ressource incorporée.
* Si vous avez modifié uniquement le formulaire adaptatif ou la communication interactive incorporés dans une page Sites publiée, publiez la ressource originale et les modifications se reflètent dans la page Sites publiée. La page Sites publiée comprend une référence à la ressource ; il n’est pas nécessaire de la republier.
* Si vous avez modifié la page Sites et le formulaire adaptatif ou la communication interactive incorporés, republiez la page Sites et la ressource incorporée.

## Modifier le formulaire adaptatif et la communication interactive incorporés {#modify-embedded-adaptive-form-and-interactive-communication}

La page AEM Sites conserve une référence au formulaire adaptatif et à la communication interactive dans le conteneur AEM Forms. Par conséquent, toutes les configurations et les propriétés, telles que le thème, les styles et l’action Envoyer, configurées dans le formulaire adaptatif et la communication interactive dʼorigine sont conservées dans le formulaire adaptatif et la communication interactive incorporés.

Pour modifier une configuration ou une propriété du formulaire adaptatif ou de la communication interactive incorporés, effectuez l’une des opérations suivantes.

* Ouvrez le formulaire original dans les formulaires adaptatifs ou la communication interactive dans les éditeurs respectifs et modifiez-les.
* Sélectionnez le formulaire adaptatif ou la communication interactive à partir de la page Sites en mode Modifier, puis sélectionnez **Modifier dans une nouvelle fenêtre**. Le formulaire d’origine s’ouvre en mode dʼédition.

## Éléments à prendre en compte et bonnes pratiques {#considerations-and-best-practices}

Gardez les points suivants à l’esprit lorsque vous incorporez des formulaires adaptatifs à des pages de sites AEM :

* L’en-tête et le pied de page du formulaire d’origine ne sont pas intégrés dans le formulaire incorporé.
* Les brouillons et les envois de formulaires incorporés sont pris en charge et visibles dans les onglets Brouillons et Formulaires envoyés du portail Formulaires.
* L’action Envoyer configurée sur le formulaire d’origine est conservée dans le formulaire incorporé.
* Le ciblage d’expérience et les tests A/B configurés sur le formulaire d’origine ne fonctionnent pas dans le formulaire incorporé. Cependant, vous pouvez utiliser le ciblage d’expérience sur la page Sites pour présenter différents formulaires en fonction des profils d’utilisateurs.
* Si vous avez configuré Adobe Analytics pour le formulaire d’origine, les données d’analyse du formulaire incorporé seront capturées dans Adobe Analytics. En revanche, elles ne seront pas disponibles dans le rapport d’analyse des formulaires.
