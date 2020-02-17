---
title: Utilisation de l’enregistrement automatique dans l’application AEM Forms
seo-title: Utilisation de l’enregistrement automatique dans l’application AEM Forms
description: Apprenez à utiliser enregistrement automatique dans l’application AEM Forms afin d’éviter la perte de données.
seo-description: Apprenez à utiliser enregistrement automatique dans l’application AEM Forms afin d’éviter la perte de données.
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Utilisation de l’enregistrement automatique dans l’application AEM Forms{#using-autosave-in-aem-forms-app}

Lorsqu’un utilisateur saisit des données dans l’application Adobe Experience Manager Forms, la fonction d’enregistrement automatique les enregistre à intervalles réguliers. La fonction d’enregistrement automatique de l’application AEM Forms vous permet d’éviter la perte de données si l’application se ferme accidentellement.

L’application se ferme accidentellement :

* Si votre périphérique s’arrête car sa batterie est faible
* Si l’utilisateur stoppe l’application
* Si une panne inattendue se produit

Vous pouvez spécifier les intervalles auxquels l’application enregistre les données saisies.

>[!NOTE]
>
>Sélectionnez la fréquence d’enregistrement automatique de manière judicieuse. Un enregistrement automatique fréquent peut avoir un impact perceptible sur les performances de votre périphérique.

Suivez les étapes ci-après pour utiliser la fonction d’enregistrement automatique de l’application AEM Forms :

1. Connectez-vous à l’application et accédez à **Paramètres > Général**.
1. In the General screen, use the **Autosave Frequency** option to select the intervals at which you want the app to save the entered data.
   [ ![Définition de la fréquence d’enregistrement automatique](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Lorsque vous redémarrez l’application et que vous vous connectez avec le même nom d’utilisateur, vous êtes invité à restaurer votre tâche à l’aide de la boîte de dialogue de récupération de la tâche non enregistrée. Click **OK** in the Recover Unsaved Task dialog to resume working with the saved task. Vous pouvez cliquer sur **Annuler** pour supprimer les données enregistrées correspondant au dernier enregistrement automatique déclenché et commencer à travailler sur une nouvelle tâche.

   Si vous cliquez sur **OK**, la tâche est restaurée avec les données correspondant au dernier enregistrement automatique déclenché avant que l’application ne s’arrête. Il comprend les données du formulaire et toutes les pièces jointes associées à la tâche.
   [![](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)****** Obtention d’une tâche **récupéréeA. Formulaire de travail en cours** B. Application fermée avec force **C.** L’application a redémarré avec la boîte de dialogue Récupérer la tâche non enregistrée **D. Formulaire restauré avec les données d’origine

