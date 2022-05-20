---
title: Incorporation d’un formulaire adaptatif ou d’une communication interactive dans une page des sites AEM
seo-title: Embed an adaptive form or interactive communication in AEM sites page
description: Vous pouvez incorporer des formulaires adaptatifs dans des pages de sites AEM. Les utilisateurs peuvent remplir et envoyer des formulaires sans quitter les pages du site.
seo-description: You can embed adaptive forms in AEM sites pages. Users can fill and submit forms without leaving the site pages.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
feature: Adaptive Forms
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1083'
ht-degree: 100%

---

# Incorporation d’un formulaire adaptatif ou d’une communication interactive dans une page des sites AEM {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## Présentation {#overview}

AEM Forms permet aux développeurs de formulaires d’incorporer facilement des formulaires adaptatifs et des communications interactives dans une page d’AEM Sites ou une page Web hébergée en dehors d’AEM. Le formulaire adaptatif et la communication interactive incorporés fonctionnent parfaitement et les utilisateurs peuvent les remplir et les envoyer sans quitter la page. Cela permet à l’utilisateur de rester dans le contexte des autres éléments de la page Web et d’interagir simultanément avec le formulaire ou la communication interactive.

Pour plus d’informations sur l’incorporation d’un formulaire adaptatif dans une page web externe, consultez la section [Incorporation d’un formulaire adaptatif dans une page web externe](/help/forms/using/embed-adaptive-form-external-web-page.md).

Sur une page AEM Sites, vous pouvez ajouter un formulaire adaptatif ou une communication interactive à l’aide des éléments suivants :

* **[Composant Conteneur AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms fournit un composant que vous pouvez ajouter à vos pages de site. Le composant Conteneur AEM Forms vous permet d’incorporer un formulaire adaptatif et une communication interactive.

* **[Explorateur des actifs](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)** Tous les formulaires et toutes les communications interactives que vous créez sont disponibles sous Actifs. Vous pouvez faire glisser et déposer le formulaire sous forme de ressource dans votre page.

## Prérequis {#prerequisites}

Pour incorporer un formulaire adaptatif ou une communication interactive dans une page AEM Sites qui utilise un modèle modifiable, vérifiez que le composant AEM Forms est configuré en tant que composant autorisé dans le modèle associé. Pour plus d’informations, voir **Stratégie et propriétés (conteneur de disposition)** dans [Création de modèles de page](/help/sites-authoring/templates.md).

Si une page de site utilise un modèle statique, vous devez le configurer dans le système de paragraphe de la page de site. Pour plus d’informations, voir [Configuration des composants en mode Création](/help/sites-authoring/default-components-designmode.md).

## Incorporer un formulaire adaptatif ou une communication interactive {#af-component}

Pour incorporer un formulaire adaptatif ou une communication interactive à l’aide du composant Conteneur AEM Forms :

1. Ouvrez la page de sites AEM, en mode Edition, dans laquelle vous souhaitez incorporer un formulaire adaptatif ou une communication interactive.
1. À partir du volet Explorateur des composants, faites glisser et déposez le composant Conteneur AEM Forms sur la page.

   Vous pouvez également rechercher un formulaire adaptatif ou une communication interactive dans le navigateur d’actifs et le glisser-déposer sur la page de sites. Cela inclut le formulaire dans un conteneur AEM Forms.

   >[!NOTE]
   >
   >Les composants de plusieurs conteneurs d’AEM Forms sur une page ne sont pas pris en charge.

1. Appuyez sur le composant Conteneur d’AEM Forms sur la page de site, puis appuyez sur ![settings_icon](assets/settings_icon.png) dans la barre d’action. La boîte de dialogue **[!UICONTROL Modifier le conteneur d’AEM Forms]** s’affiche.
1. Dans la boîte de dialogue Modifier le conteneur d’AEM Forms, précisez ce qui suit.

   * **Type de ressource :** sélectionnez le type de ressource à incorporer. Vous pouvez choisir entre formulaire adaptatif et communication interactive
   * **Chemin d’accès à la ressource** : recherchez et sélectionnez le formulaire adaptatif ou la communication interactive à incorporer. Il est prérempli si vous le faites glisser à partir du navigateur de ressources.
   * (Formulaire adaptatif uniquement) **Publier l’envoi** : sélectionnez l’action à déclencher lors de l’envoi du formulaire. Vous pouvez choisir d’afficher un message de remerciement ou une page de remerciement.

      * **Message de remerciement** : rédigez un message à l’aide de l’éditeur de texte enrichi à afficher après l’envoi du formulaire. Cette option n’est disponible que lorsque vous choisissez d’afficher un message de remerciement.
      * **Page de remerciement** : recherchez et sélectionnez la page à afficher après l’envoi du formulaire. Cette option n’est disponible que lorsque vous choisissez d’afficher une page de remerciement.
      * **Actualiser la page lors de l’envoi** : activez cette option pour actualiser la page contenant le formulaire adaptatif incorporé afin d’afficher la page de remerciement. Dans le cas contraire, la page de remerciement remplace le formulaire adaptatif dans le conteneur d’AEM Forms sans actualiser la page. Cette option n’est disponible que lorsque vous choisissez d’afficher une page de remerciement.
   * **Thème** : sélectionnez un thème qui définit le style des composants de votre formulaire adaptatif ou de votre communication interactive. Style comprend des propriétés d’aspect, comme le style de police, la couleur d’arrière-plan, les dimensions et l’alignement.
   * **Hauteur :** spécifiez la hauteur du conteneur. Laissez ce champ vide pour redimensionner automatiquement le conteneur.
   * **Bibliothèque client CSS** : spécifiez le chemin d’accès à une bibliothèque client CSS.


1. Enregistrez les paramètres. Le formulaire adaptatif ou la communication interactive sont désormais incorporés à la page.

## Publier un formulaire adaptatif ou une communication interactive incorporés {#publishing-embedded-adaptive-form-and-interactive-communication}

Examinons les cas suivants pour publier un actif incorporé (formulaire adaptatif ou communication interactive) à une page de sites AEM :

* Si vous publiez la page de sites AEM pour la première fois et qu’elle inclut un formulaire adaptatif ou une communication interactive, publiez la page de sites et l’actif incorporé.
* Si vous avez uniquement modifié le formulaire adaptatif ou la communication interactive incorporés à une page de site publiée, publiez la ressource d’origine pour que les modifications se reflètent sur la page de site publiée. La page de site publiée comprend une référence à la ressource et ne doit pas être republiée.
* Si vous avez modifié la page de sites et le formulaire adaptatif ou la communication interactive incorporés, republiez la page de sites et l’actif incorporé.

## Modifier un formulaire adaptatif ou une communication interactive incorporés {#modifying-embedded-adaptive-form-and-interactive-communication}

La page de sites AEM conserve une référence au formulaire adaptatif et à la communication interactive dans le Conteneur AEM Forms. Par conséquent, toutes les configurations et les propriétés, telles que le thème, les styles et l’action Envoyer, configurées dans le formulaire adaptatif et la communication interactive d’origine sont conservées dans le formulaire adaptatif et la communication interactive incorporés.

Pour modifier une configuration ou une propriété du formulaire adaptatif ou de la communication interactive incorporés, effectuez l’une des opérations suivantes.

* Ouvrez le formulaire d’origine dans des formulaires adaptatifs ou une communication interactive dans les éditeurs respectifs et modifiez-les.
* Appuyez sur le formulaire adaptatif ou la communication interactive à partir de la page du site en mode d’édition, puis appuyez sur **[!UICONTROL Modifier dans une nouvelle fenêtre]**. Le formulaire d’origine s’affiche en mode d’édition, et vous pouvez alors le modifier.

>[!NOTE]
>
>Les modifications effectuées dans le formulaire adaptatif ou la communication interactive d’origine sont automatiquement reflétées dans le formulaire incorporé. Cependant, vous devez republier le formulaire adaptatif, la communication interactive ou la page du site pour refléter les modifications sur la page publiée.

## Éléments à prendre en compte et bonnes pratiques {#considerations-and-best-practices}

Gardez les points suivants à l’esprit lorsque vous incorporez des formulaires adaptatifs à des pages de sites AEM :

* L’en-tête et le pied de page du formulaire d’origine ne sont pas intégrés dans le formulaire incorporé.
* Les brouillons et les envois de formulaires incorporés sont pris en charge et visibles dans les onglets Brouillons et Formulaires envoyés du portail de formulaires.
* L’action Envoyer configurée sur le formulaire d’origine est conservée dans le formulaire incorporé.
* Le ciblage d’expérience et les tests A/B configurés sur le formulaire d’origine ne fonctionnent pas dans le formulaire incorporé. Cependant, vous pouvez utiliser un ciblage d’expérience au niveau de la page de sites pour présenter différents formulaires basés sur les profils d’utilisateurs.
* Si vous avez configuré Adobe Analytics pour le formulaire d’origine, les données d’analyse du formulaire incorporé seront capturées dans Adobe Analytics. En revanche, elles ne seront pas disponibles dans le rapport d’analyse des formulaires.
