---
title: '« Tutoriel : publier votre formulaire adaptatif »'
description: Publier le formulaire adaptatif en tant que page AEM, incorporer le formulaire à une page AEM Sites ou à une page web externe
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 100%

---

# Tutoriel : publier votre formulaire adaptatif {#tutorial-publish-your-adaptive-form}

![hero-image](do-not-localize/13-publish-your-adaptive-form-small.png)

Ce tutoriel fait partie de la série [Création de votre premier formulaire adaptatif](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et accomplir le cas d’utilisation complet du tutoriel.

Une fois que le formulaire adaptatif est prêt, vous pouvez le publier pour le mettre à la disposition des utilisateurs finaux. Les utilisateurs finaux peuvent ouvrir le formulaire publié sur n’importe quel appareil et navigateur Internet. Lorsqu’un formulaire adaptatif est publié, le formulaire et le contenu associé sont copiés d’une instance d’auteur AEM à une instance de publication AEM. Le formulaire est mis à la disposition de l’utilisateur final via l’instance de publication.

Pour publier un formulaire adaptatif, utilisez lʼune des méthodes suivantes :

* [Publiez le formulaire adaptatif en tant que page AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporez le formulaire adaptatif dans une page AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporez le formulaire adaptatif dans une page web externe (une page web extérieure à AEM, hébergée en dehors d’AEM)](../../forms/using/publish-your-adaptive-form.md)

## Avant de commencer {#before-you-start}

* **[Configuration d’une instance de publication AEM Forms](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)** : l’instance de publication est une instance d’AEM [!DNL Forms] publique et fonctionnant en mode publication. Dans un environnement de production, l’instance de publication se trouve en dehors du pare-feu de l’entreprise.
* **[Configuration de la réplication et de la réplication inverse](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)** : la réplication copie le contenu de l’instance d’auteur vers une instance de publication et renvoie les entrées utilisateur (par exemple, les entrées de formulaire) de l’instance de publication vers l’instance d’auteur.

## Publiez le formulaire adaptatif en tant que page AEM {#publish-the-adaptive-form-as-an-aem-page}

Lorsque le formulaire adaptatif est publié comme une page AEM, la page web entière ne contient que le formulaire publié. Vous pouvez utiliser l’URL du formulaire adaptatif pour le lier à partir d’une autre page web. Pour publier le formulaire adaptatif **shipping-address-add-update-form** en tant que page AEM :

1. Connectez-vous à lʼinstance dʼauteur AEM [!DNL Forms] et recherchez le formulaire adaptatif shipping-address-add-update-form dans l’interface utilisateur dʼAEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Sélectionnez le formulaire adaptatif shipping-address-add-update-form et sélectionnez **[!UICONTROL Publier]**. Une boîte de dialogue contenant les ressources liées au formulaire adaptatif s’affiche. Sélectionnez **[!UICONTROL Publier]**. Le formulaire adaptatif est publié et une boîte de dialogue de réussite s’affiche.
1. Ouvrez le formulaire sur l’instance de publication. Le formulaire peut être complété et envoyé par l’utilisateur final.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporez le formulaire adaptatif dans une page AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permet aux développeurs de formulaires d’incorporer facilement des formulaires adaptatifs dans une page AEM [!DNL Sites]. Le formulaire adaptatif incorporé est entièrement fonctionnel et les utilisateurs peuvent le remplir et le soumettre sans quitter la page. Il permet à l’utilisateur de rester dans le contexte des autres éléments de la page web et d’interagir simultanément avec le formulaire.

AEM [!DNL Forms] fournit un composant, le conteneur AEM [!DNL Forms], pour incorporer un formulaire adaptatif à une page AEM [!DNL Sites]. Par défaut, le composant n’est pas visible dans le conteneur AEM [!DNL Sites]. Pour activer le composant Conteneur AEM [!DNL Forms] et incorporer le formulaire adaptatif dans une page AEM [!DNL Sites], procédez comme suit :

1. Créez et ouvrez une page dans le site We.Retail pour la modifier. Par exemple, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Le formulaire adaptatif est incorporé à la page du [!DNL Sites].

   Vous pouvez également incorporer le formulaire adaptatif dans une page du [!DNL Site's] We.Retail existante. Par exemple, la page À PROPOS DE NOUS [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Cela vous permet de créer une page plus rapidement. Les étapes ci-dessous utilisent la page nouvellement créée.

   Le site We.Retail est présent nativement dans AEM. Si vous nʼavez pas installé le site We.Retail, consultez la section [Implémentation de référence de We.Retail](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr) pour installer le site.

1. Sélectionnez les informations de la page ![propriétés](assets/properties.png) et sélectionnez l’option **[!UICONTROL Modifier le modèle]** sur la page du site We.Retail que vous avez créée. Le modèle de la page s’ouvre dans un nouvel onglet du navigateur.
1. Sélectionnez le champ **[!UICONTROL conteneur de disposition]**, puis sélectionnez ![gestiondesflux](assets/feedmanagement.png). Dans l’onglet **[!UICONTROL Composants autorisés]**, développez le menu en accordéon **[!UICONTROL Général]**, sélectionnez l’option **[!UICONTROL Formulaire AEM]**, puis sélectionnez ![icône_denregistrement](assets/save_icon.svg). Le composant Conteneur AEM [!DNL Forms] est alors activé pour la page.

1. Ouvrez l’onglet du navigateur contenant la page AEM [!DNL Sites] ouverte à l’étape 1. Sélectionnez le champ **[!UICONTROL Faire glisser les composants ici]**, puis sélectionnez **+.** Dans le champ **[!UICONTROL Insérer un nouveau composant]**, sélectionnez **[!UICONTROL Formulaire AEM]**. Le composant **[!UICONTROL Conteneur AEM Forms]** est alors ajouté à la page.
1. Sélectionnez le composant **[!UICONTROL Conteneur AEM Forms]**, puis sélectionnez ![icône-de-configuration](assets/configure-icon.svg). Une boîte de dialogue contenant les propriétés du conteneur AEM [!DNL Forms] s’affiche. Dans le champ **[!UICONTROL Chemin d’accès à la ressource]**, recherchez et sélectionnez le formulaire adaptatif shipping-address-add-update-form. Sélectionnez ![icône_d’enregistrement](assets/save_icon.svg). Le formulaire adaptatif est incorporé dans la page 
1. Publiez le formulaire adaptatif et la page [!DNL Sites]. Voici quelques points à prendre en considération :

   * Si vous publiez la page AEM [!DNL Sites] pour la première fois et qu’elle comprend un formulaire incorporé, publiez la page [!DNL Sites] et le formulaire incorporé.
   * Si vous modifiez uniquement le formulaire incorporé à une page de site publiée, publiez le formulaire d’origine et les modifications seront répercutées sur la page de site publiée. La page de site publiée comprend une référence au formulaire et n’exige pas de republier la page.
   * Si vous modifiez la page [!DNL Sites] et le formulaire incorporé, republiez la page [!DNL Sites] et le formulaire.

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Ajout du formulaire de changement d’adresse d’expédition et de facturation à une page AEM [!DNL Sites].

## Incorporer le formulaire adaptatif dans une page web externe {#embed-the-adaptive-form-in-an-external-webpage}

Vous pouvez incorporer un formulaire adaptatif dans une page web externe (une page web autre qu’AEM hébergée en dehors d’AEM) en insérant quelques lignes de code JavaScript dans la page web externe. Le code JavaScript envoie une requête HTTP au serveur AEM [!DNL Forms] pour le formulaire adaptatif et les ressources associées et ajoute le formulaire adaptatif à la page web. Pour obtenir des instructions détaillées, consultez la section [Incorporer le formulaire adaptatif dans une page web externe](/help/forms/using/embed-adaptive-form-external-web-page.md).
