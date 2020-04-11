---
title: '"Didacticiel : Publier votre formulaire adaptatif"'
seo-title: '"Didacticiel : Publier votre formulaire adaptatif"'
description: Publiez le formulaire adaptatif en tant que page AEM, incorporez le formulaire à une page de sites AEM ou incorporez le formulaire adaptatif dans une page Web externe.
seo-description: Publiez le formulaire adaptatif en tant que page AEM, incorporez le formulaire à une page de sites AEM ou incorporez le formulaire adaptatif dans une page Web externe.
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Tutorial: Publish your adaptive form {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

Une fois le formulaire adaptatif prêt, vous pouvez le publier pour le rendre disponible pour les utilisateurs finaux. Les utilisateurs finaux peuvent ouvrir le formulaire publié sur n’importe quel périphérique et navigateur Internet. Lorsqu’un formulaire adaptatif est publié, le formulaire et le contenu associé sont copiés d’une instance d’auteur AEM vers une instance de publication AEM. Le formulaire est mis à la disposition de l’utilisateur final via l’instance de publication.

Vous disposez des méthodes suivantes pour publier un formulaire adaptatif :

* [Publication du formulaire adaptatif en tant que page AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incorporer le formulaire adaptatif dans une page de sites AEM](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incorporer le formulaire adaptatif dans une page Web externe (une page Web non AEM hébergée en dehors d’AEM)](../../forms/using/publish-your-adaptive-form.md)

## Avant de commencer {#before-you-start}

* **[Configuration d’une instance](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**de publication AEM Forms : L’instance de publication est une instance publique d’AEM Forms s’exécutant en mode de publication. Dans un  de production , l’instance de publication se trouve en dehors du pare-feu de l’entreprise.
* **[Configuration de la réplication et de la réplication](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**inverse : La réplication copie le contenu de l’instance d’auteur vers une instance de publication et renvoie les entrées utilisateur (par exemple, les entrées de formulaire) de l’instance de publication vers l’instance d’auteur.

## Publication du formulaire adaptatif en tant que page AEM {#publish-the-adaptive-form-as-an-aem-page}

Lorsque le formulaire adaptatif est publié en tant que page AEM, la page Web entière contient uniquement le formulaire publié. Vous pouvez utiliser l’URL du formulaire adaptatif pour le lier à partir d’une autre page Web. Pour publier le formulaire adaptatif **d’expédition-address-add-update-form** en tant que page AEM :

1. Connectez-vous à l’instance d’auteur AEM Forms et localisez le formulaire adaptatif d’expédition-address-add-update-form dans l’interface utilisateur d’AEM Forms.
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Sélectionnez le formulaire adaptatif d’expédition-address-add-update-form et appuyez sur **Publier**. Une boîte de dialogue contenant les ressources liées au formulaire adaptatif s’affiche. Appuyez sur **Publier**. Le formulaire adaptatif est publié et une boîte de dialogue de réussite s’affiche.
1. Ouvrez le formulaire sur l’instance de publication. Le formulaire peut être rempli et envoyé par l’utilisateur final.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incorporer le formulaire adaptatif dans une page de sites AEM {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM Forms permet aux développeurs de formulaires d’incorporer facilement des formulaires adaptatifs dans une page de sites AEM. Le formulaire adaptatif incorporé est entièrement fonctionnel et les utilisateurs peuvent le remplir et le soumettre sans quitter la page. Il permet à l’utilisateur de rester dans le contexte d’autres éléments de la page Web et d’interagir simultanément avec le formulaire.

AEM Forms fournit un composant, le AEM Forms, pour incorporer un formulaire adaptatif à une page de sites AEM. Par défaut, le composant n’est pas visible dans le  des sites AEM. Effectuez les étapes suivantes pour activer le composant  de AEM Forms et pour incorporer le formulaire adaptatif dans une page de sites AEM :

1. Créez et ouvrez une page dans le site Web We.Retail pour modification. Par exemple, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). Le formulaire adaptatif est incorporé à la page des sites.

   Vous pouvez également incorporer le formulaire adaptatif dans une page existante du site Web.Retail. Par exemple, la page A PROPOS DE NOUS [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Cela vous permet de gagner du temps pour créer une page. Les étapes ci-dessous utilisent la page nouvellement créée.

   Le site Web We.Retail est fourni avec AEM. Si le site Web We.Retail n&#39;est pas installé sur votre ordinateur, reportez-vous à la section Mise en oeuvre [du guide](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) Web.Retail Reference.

1. Appuyez sur ![Propriétés](assets/properties.png) des informations de page et sélectionnez l’option **Modifier le modèle** dans la page de site Web We.Retail nouvellement créée. Le modèle de la page s’ouvre dans un nouvel onglet du navigateur.
1. Appuyez dans la **de** mise en page et appuyez sur Gestion des ![flux](assets/feedmanagement.png). Dans l’onglet Composants **** autorisés, développez l’accordéon **Général** , sélectionnez l’option Formulaire **** AEM, puis appuyez sur ![](assets/save_icon.svg). Le composant  d’AEM Forms est activé pour la page.

1. Ouvrez l’onglet du navigateur contenant la page Sites AEM ouverte à l’étape 1. Appuyez sur la zone **Faire glisser les composants ici** et appuyez sur **+.** Dans la zone **Insérer un nouveau composant** , appuyez sur **AEM Form.** Le composant de **d’** AEM Forms est ajouté à la page.
1. Appuyez sur le **composant de** AEM Forms et appuyez sur ![](assets/configure-icon.svg). Une boîte de dialogue avec les propriétés du AEM Forms s’affiche. Dans le champ Chemin d’accès **au** fichier, parcourez et sélectionnez le formulaire adaptatif d’expédition-address-add-update-form. Pression ![](assets/save_icon.svg). Le formulaire adaptatif est incorporé dans la page 
1. Publiez le formulaire adaptatif et la page de sites. Voici quelques points à prendre en considération :

   * Si vous publiez la page de sites AEM pour la première fois et qu’elle comprend un formulaire incorporé, publiez la page de sites et le formulaire incorporé.
   * Si vous modifiez uniquement le formulaire incorporé dans une page de site publiée, publiez le formulaire d’origine et les modifications sont répercutées dans la page de site publiée. La page de site publiée comprend une référence au formulaire et n’exige pas de republier la page.
   * Si vous modifiez la page de sites et le formulaire incorporé, republiez la page de sites et le formulaire.
   ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   Formulaire de modification de l’adresse d’expédition et de facturation ajouté à une page de sites AEM.

## Incorporer le formulaire adaptatif dans une page Web externe {#embed-the-adaptive-form-in-an-external-webpage}

Vous pouvez incorporer un formulaire adaptatif à une page Web externe (une page Web non AEM hébergée en dehors d’AEM) en insérant quelques lignes de code JavaScript dans la page Web externe. Le code JavaScript envoie une requête HTTP au serveur AEM Forms pour le formulaire adaptatif et les ressources connexes et ajoute le formulaire adaptatif à la page Web. Pour obtenir des instructions détaillées, voir [Intégration du formulaire adaptatif à une page](/help/forms/using/embed-adaptive-form-external-web-page.md)Web externe.
