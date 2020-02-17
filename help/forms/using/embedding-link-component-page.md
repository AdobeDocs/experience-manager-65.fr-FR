---
title: Intégration du composant Link dans une page
seo-title: Intégration du composant Link dans une page
description: Vous pouvez utiliser le composant Link pour lier un document adaptatif ou un formulaire adaptatif depuis la page que vous souhaitez.
seo-description: Vous pouvez utiliser le composant Link pour lier un document adaptatif ou un formulaire adaptatif depuis la page que vous souhaitez.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# Intégration du composant Link dans une page{#embedding-link-component-in-a-page}

## Conditions préalables {#prerequisites}

Le composant Link est membre de la catégorie Document Services. Assurez-vous que la catégorie Document Services est visible dans le navigateur de composants d’AEM. Si la catégorie n’est pas répertoriée, suivez la procédure décrite à la section [Activation des composants d’un portail de formulaires](/help/forms/using/enabling-forms-portal-components.md).

## Composant Link {#link-component}

Le composant Link permet aux créateurs de portails de formulaires de créer un lien vers un formulaire adaptatif depuis n’importe quel point d’une page. Le composant Link est disponible dans la section Document Services du navigateur de composants.

Suivez les étapes ci-après pour ajouter un composant Link à la page :

1. Faites glisser le composant **Link** sur la page. Select the component and tap ![cmppr](assets/cmppr.png). La boîte de dialogue Modifier le composant de lien s’ouvre.

   ![edit-link-component](assets/edit-link-component.png)

1. Dans l’onglet **Affichage**, spécifiez ce qui suit :

   * **Link Caption** : texte ou légende du lien.
   * **Link Tooltip** : info-bulle du lien.
   * **Modèle de mise en page** : modèle pour la mise en page du composant Link.

1. Ouvrez l’onglet **Informations d’actif** et spécifiez le type d’actif. An asset can be a **form**. Selon le type de fichier sélectionné, les options ci-dessous s’affichent : 

   * **Chemin d’accès à l’actif** : chemin d’accès au référentiel de stockage de l’actif.

   * **Type de rendu** : le format de rendu : PDF, HTML ou Auto. Le type de rendu Auto détecte l’environnement de l’utilisateur et effectue le rendu du formulaire en conséquence, au format HTML ou PDF. Par exemple, si le formulaire est utilisé sur un périphérique mobile, le type de rendu Auto est effectué au format HTML.
   * **** URL d’envoi :  URL de la servlet sur laquelle les données du formulaire sont envoyées.
   * **Profil HTML** : profil de rendu du formulaire au format HTML.
   * **Profil PDF** : profil de rendu du formulaire au format PDF.

1. Ouvrez l’onglet **Avancé.** Vous pouvez spécifier des paramètres supplémentaires au format de paire clé-valeur. Lorsque le lien est activé, ces paramètres supplémentaires sont transmis avec le formulaire.

   Appuyez sur **Terminé** pour enregistrer la règle.

## Méthodes recommandées pour l’utilisation du composant Link {#best-practices-for-using-link-component-br}

* Veillez à sélectionner PDF comme type de rendu si le chemin spécifié sous Form Path pointe vers un document dont le format de rendu autorisé est PDF.
* La valeur Submit URL d’un formulaire peut être spécifiée à plusieurs emplacements et l’ordre de priorité s’établit comme suit :

   1. La valeur Submit URL intégrée dans le formulaire (dans le bouton d’envoi) a la priorité la plus élevée.
   1. La valeur Submit URL mentionnée dans Forms Manager possède une priorité moyenne.
   1. La valeur Submit URL mentionnée dans Forms Portal a la priorité la plus faible.
