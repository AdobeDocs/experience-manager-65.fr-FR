---
title: Envoi asynchrone de formulaires adaptatifs
description: Apprenez à configurer l’envoi asynchrone pour les formulaires adaptatifs.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 78%

---

# Envoi asynchrone de formulaires adaptatifs{#asynchronous-submission-of-adaptive-forms}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html?lang=fr) |
| AEM 6.5 | Cet article |

Traditionnellement, les formulaires web sont configurés à des fins d’envoi synchrone. Lors d’un envoi synchrone, lorsque les utilisateurs envoient un formulaire, ils sont redirigés vers une page d’accusé de réception, une page de remerciement ou, en cas d’échec de l’envoi, une page d’erreur. Toutefois, les expériences Web modernes telles que les applications d’une seule page gagnent en popularité. Dans une application de ce type, la page Web reste statique tandis que l’interaction entre le client et le serveur se déroule en arrière-plan. Vous pouvez désormais fournir cette expérience avec des formulaires adaptatifs en configurant l’envoi asynchrone.

Lors d’un envoi asynchrone, lorsqu’un utilisateur envoie un formulaire, le développeur de formulaires se connecte à une expérience distincte, notamment la redirection vers un autre formulaire ou une section distincte du site Web. L’auteur peut également ajouter des services distincts comme l’envoi de données à un autre magasin de données ou l’ajout d’un moteur d’analyse personnalisé. En cas d’envoi asynchrone, un formulaire adaptatif se comporte comme une application d’une seule page, car le formulaire ne se recharge pas ou son URL ne change pas lorsque les données du formulaire envoyé sont validées sur le serveur.

Lisez la suite pour plus de détails sur l’envoi asynchrone dans les formulaires adaptatifs.

## Configuration de l’envoi asynchrone {#configure}

Pour configurer l’envoi asynchrone d’un formulaire adaptatif :

1. En mode de création de formulaire adaptatif, sélectionnez l’objet Conteneur de formulaires et choisissez ![cmppr1](assets/cmppr1.png) pour ouvrir ses propriétés.
1. Dans la section des propriétés **[!UICONTROL Envoi]**, activez **[!UICONTROL Utiliser l’envoi asynchrone]**.
1. Dans la section **[!UICONTROL Lors de l’envoi]**, sélectionnez l’une des options suivantes pour effectuer un envoi de formulaire réussi.

   * **[!UICONTROL Rediriger vers l’URL]** : redirige vers l’URL ou la page spécifiée lors de l’envoi du formulaire. Vous pouvez spécifier une URL ou sélectionner le chemin d’accès à une page dans le champ **[!UICONTROL URL/Chemin d’accès restreint.]**
   * **[!UICONTROL Afficher le message]** : affiche un message lors de l’envoi d’un formulaire. Vous pouvez rédiger un message dans le champ de texte situé en dessous de l’option Afficher le message. Le champ de texte prend en charge la mise en forme de texte enrichi.

1. Sélectionner ![check-button1](assets/check-button1.png) pour enregistrer les propriétés.

## Fonctionnement de l’envoi asynchrone {#how-asynchronous-submission-works}

AEM Forms fournit des gestionnaires de succès et d’erreur prêts à l’emploi pour les envois de formulaires. Les gestionnaires sont des fonctions côté client qui s’exécutent selon la réponse du serveur. Lorsqu’un formulaire est envoyé, les données sont transmises au serveur pour validation, ce qui renvoie une réponse au client avec des informations sur l’événement de succès ou d’erreur pour l’envoi. Les informations sont transmises comme paramètres au gestionnaire approprié pour exécuter la fonction.

En outre, les auteurs de formulaire et les développeurs peuvent écrire des règles au niveau du formulaire pour remplacer les gestionnaires par défaut. Pour plus d’informations, voir [Remplacer les gestionnaires par défaut à l’aide de règles](#custom).

Examinons d’abord la réponse du serveur pour les événements de succès et d’erreur.

### Réponse du serveur pour l’événement de succès de l’envoi {#server-response-for-submission-success-event}

La structure de la réponse du serveur pour l’événement de succès de l’envoi est la suivante :

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

La réponse du serveur en cas d’envoi de formulaire réussi comprend :

* Type de format de données du formulaire : XML ou JSON
* Données du formulaire au format XML ou JSON
* Option sélectionnée pour rediriger vers une page ou afficher un message tel que configuré dans le formulaire
* URL de la page ou contenu du message tel que configuré dans le formulaire

Le gestionnaire de succès lit la réponse du serveur et redirige en conséquence vers l’URL de la page configurée ou affiche un message.

### Réponse du serveur pour l’événement d’erreur d’envoi {#server-response-for-submission-error-event}

La structure de la réponse du serveur pour l’événement d’erreur d’envoi est la suivante :

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

La réponse du serveur en cas d’erreur lors de l’envoi du formulaire comprend :

* Raison de l’erreur, échec de la validation CAPTCHA ou côté serveur
* Liste des objets d’erreur, qui inclut l’expression SOM du champ dont la validation a échoué et le message d’erreur correspondant

Le gestionnaire d’erreurs lit la réponse du serveur et affiche le message d’erreur en conséquence sur le formulaire.

## Remplacer les gestionnaires par défaut en utilisant des règles {#custom}

Les développeurs et développeuses, ainsi que les auteurs et autrices de formulaires peuvent écrire des règles au niveau du formulaire, dans l’éditeur de code, pour remplacer les gestionnaires par défaut. La réponse du serveur pour les événements de succès et d’erreur est exposée au niveau du formulaire. Les développeurs peuvent y accéder à l’aide de `$event.data` dans les règles.

Effectuez les étapes suivantes pour écrire des règles dans l’éditeur de code afin de gérer les événements de réussite et d’erreur.

1. Ouvrez le formulaire adaptatif en mode création, sélectionnez un objet de formulaire, puis sélectionnez ![edit-rules1](assets/edit-rules1.png) pour ouvrir l’éditeur de règles.
1. Sélectionner **[!UICONTROL Formulaire]** dans l’arborescence des objets de formulaire et sélectionnez **[!UICONTROL Créer]**.
1. Sélectionnez l’**[!UICONTROL éditeur de code]** dans la liste déroulante de sélection de mode.
1. Dans l’éditeur de code, sélectionnez **[!UICONTROL Modifier le code]**. Sélectionner **[!UICONTROL Modifier]** dans la boîte de dialogue de confirmation.
1. Choisissez **[!UICONTROL Envoi réussi]** ou **[!UICONTROL Erreur d’envoi]** dans la liste déroulante **[!UICONTROL Événement]**.
1. Créez une règle pour l’événement sélectionné et sélectionnez **[!UICONTROL Terminé]** pour enregistrer la règle.
