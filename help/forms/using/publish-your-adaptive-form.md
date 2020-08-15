---
title: '"Didacticiel : Publier votre formulaire adaptatif"'
seo-title: '"Didacticiel : Publier votre formulaire adaptatif"'
description: Publiez le formulaire adaptatif en tant que page AEM, incorporez le formulaire à une page AEM Sites ou incorporez le formulaire adaptatif dans une page Web externe.
seo-description: Publiez le formulaire adaptatif en tant que page AEM, incorporez le formulaire à une page AEM Sites ou incorporez le formulaire adaptatif dans une page Web externe.
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 9%

---


# Tutorial: Publish your adaptive form {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

Une fois le formulaire adaptatif prêt, vous pouvez le publier pour le rendre disponible pour les utilisateurs finaux. Les utilisateurs finaux peuvent ouvrir le formulaire publié sur n’importe quel périphérique et navigateur Internet. Lorsqu’un formulaire adaptatif est publié, le formulaire et le contenu associé sont copiés d’une instance d’auteur AEM vers une instance de publication AEM. Le formulaire est mis à la disposition de l’utilisateur final via l’instance de publication.

Vous disposez des méthodes suivantes pour publier un formulaire adaptatif :

* [Publier le formulaire adaptatif en tant que page AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporer le formulaire adaptatif dans une page AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporer le formulaire adaptatif dans une page Web externe (une page Web non AEM hébergée en dehors de l’AEM)](../../forms/using/publish-your-adaptive-form.md)

## Avant de commencer {#before-you-start}

* **[Configurez une instance](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)** de publication AEM Forms : L’instance de publication est une instance publique d’AEM s’exécutant en mode de publication. [!DNL Forms] Dans un environnement de production, l’instance de publication se trouve en dehors du pare-feu de l’entreprise.
* **[Configuration de la réplication et de la réplication](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)** inverse : La réplication copie le contenu de l’instance d’auteur vers une instance de publication et renvoie les entrées utilisateur (par exemple, les entrées de formulaire) de l’instance de publication vers l’instance d’auteur.

## Publier le formulaire adaptatif en tant que page AEM {#publish-the-adaptive-form-as-an-aem-page}

Lorsque le formulaire adaptatif est publié en tant que page AEM, la page Web entière contient uniquement le formulaire publié. Vous pouvez utiliser l’URL du formulaire adaptatif pour le lier à partir d’une autre page Web. Pour publier le formulaire adaptatif **d&#39;expédition-address-add-update-form** en tant que page d&#39;AEM :

1. Connectez-vous à l’instance d’ [!DNL Forms] auteur de l’AEM et recherchez le formulaire adaptatif d’expédition-address-add-update-form dans l’interface utilisateur AEM [!DNL Forms] .
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Sélectionnez le formulaire adaptatif d’expédition-address-add-update-form et appuyez sur **[!UICONTROL Publier]**. Une boîte de dialogue contenant les actifs liés au formulaire adaptatif s’affiche. Appuyez sur **[!UICONTROL Publier]**. Le formulaire adaptatif est publié et une boîte de dialogue de réussite s’affiche.
1. Ouvrez le formulaire sur l’instance de publication. Le formulaire peut être rempli et envoyé par l’utilisateur final.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporer le formulaire adaptatif dans une page AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

aem [!DNL Forms] permet aux développeurs de formulaires d’incorporer aisément des formulaires adaptatifs dans une [!DNL Sites] page AEM. Le formulaire adaptatif incorporé est entièrement fonctionnel et les utilisateurs peuvent le remplir et le soumettre sans quitter la page. Il permet à l’utilisateur de rester dans le contexte d’autres éléments de la page Web et d’interagir simultanément avec le formulaire.

aem [!DNL Forms] fournissent un composant, AEM [!DNL Forms] Conteneur, pour l’intégration d’un formulaire adaptatif à une page de l’AEM [!DNL Sites] . Par défaut, le composant n’est pas visible dans AEM [!DNL Sites] conteneur. Effectuez les étapes suivantes pour activer le composant [!DNL Forms] Conteneur AEM et pour incorporer le formulaire adaptatif dans une [!DNL Sites] page AEM :

1. Créez et ouvrez une page du site Web.Retail pour modification. Par exemple, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). The adaptive form is embedded to the [!DNL Sites] page.

   Vous pouvez également incorporer le formulaire adaptatif dans une [!DNL Site's] page Web.Retail existante. Par exemple, la page A PROPOS DE NOUS [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Cela vous permet de gagner du temps pour créer une page. Les étapes ci-dessous utilisent la page nouvellement créée.

   Le site We.Retail est livré avec AEM. Si le site Web We.Retail n&#39;est pas installé, consultez la section Mise en oeuvre [des références](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) We.Retail pour installer le site.

1. Appuyez sur ![les informations de page de propriétés](assets/properties.png) et sélectionnez l’option **[!UICONTROL Modifier le modèle]** dans la page de site Web.Retail qui vient d’être créée. Le modèle de la page s’ouvre dans un nouvel onglet du navigateur.
1. Appuyez sur dans la zone de conteneur **[!UICONTROL de]** mise en page et appuyez sur ![gestion](assets/feedmanagement.png)des flux. Dans l’onglet Composants **** autorisés **[!UICONTROL , développez l’accordéon]** Général **[!UICONTROL , sélectionnez l’option Formulaire]** ![AEM, puis appuyez sursave_icon. ](assets/save_icon.svg) Le composant de [!DNL Forms] Conteneur AEM est activé pour la page.

1. Ouvrez l’onglet du navigateur contenant la [!DNL Sites] page AEM ouverte à l’étape 1. Appuyez sur la zone **[!UICONTROL Faire glisser les composants ici]** et appuyez sur **+.** Dans la zone **[!UICONTROL Insérer un nouveau composant]** , appuyez sur Formulaire **** AEM. Le composant Conteneur **** AEM Forms est ajouté à la page.
1. Appuyez sur le composant conteneur **** AEM Forms et appuyez sur ![configure-icon](assets/configure-icon.svg). Une boîte de dialogue présentant les propriétés du [!DNL Forms] Conteneur AEM s’affiche. Dans le champ Chemin d’accès **[!UICONTROL au]** fichier, recherchez et sélectionnez le formulaire adaptatif d’expédition-address-add-update-form. Appuyez sur ![save_icon](assets/save_icon.svg). Le formulaire adaptatif est incorporé dans la page 
1. Publiez le formulaire adaptatif et la [!DNL Sites] page. Voici quelques points à prendre en considération :

   * If you publish the AEM [!DNL Sites] page for the first time and it includes an embedded form, publish the [!DNL Sites] page and the embedded form.
   * Si vous modifiez uniquement le formulaire incorporé dans une page de site publiée, publiez le formulaire d’origine et les modifications sont répercutées dans la page de site publiée. La page de site publiée comprend une référence au formulaire et n’exige pas de republier la page.
   * If you modify the [!DNL Sites] page and the embedded form, republish the [!DNL Sites] page and the form.

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   Formulaire Changement d&#39;adresse d&#39;expédition et de facturation ajouté à une [!DNL Sites] page d&#39;AEM.

## Incorporer le formulaire adaptatif dans une page Web externe {#embed-the-adaptive-form-in-an-external-webpage}

Vous pouvez incorporer un formulaire adaptatif à une page Web externe (une page Web non AEM hébergée en dehors de AEM) en insérant quelques lignes de code JavaScript dans la page Web externe. Le code JavaScript envoie une requête HTTP au [!DNL Forms] serveur d’AEM pour le formulaire adaptatif et les ressources connexes et ajoute le formulaire adaptatif à la page Web. Pour obtenir des instructions détaillées, voir [Intégration du formulaire adaptatif à une page](/help/forms/using/embed-adaptive-form-external-web-page.md)Web externe.
