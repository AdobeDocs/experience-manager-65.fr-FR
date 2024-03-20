---
title: Utiliser l’enregistrement automatique dans l’application AEM Forms
description: Découvrez comment utiliser la fonction d’enregistrement automatique dans l’application AEM Forms qui vous permet d’éviter la perte de données.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 57%

---

# Utiliser l’enregistrement automatique dans l’application AEM Forms{#using-autosave-in-aem-forms-app}

Lorsqu’un utilisateur saisit des données dans l’application Adobe Experience Manager Forms, la fonction d’enregistrement automatique les enregistre à intervalles réguliers. La fonction d’enregistrement automatique de l’application AEM Forms vous permet d’éviter toute perte de données si l’application est accidentellement fermée.

Votre application peut se fermer accidentellement :

* Si votre appareil s’arrête en raison d’une batterie faible
* Si l’utilisateur stoppe l’application
* En cas de blocage inattendu

Vous pouvez spécifier les intervalles après lesquels l’application enregistre les données saisies.

>[!NOTE]
>
>Sélectionnez la fréquence d’enregistrement automatique de manière judicieuse. Un enregistrement automatique fréquent peut avoir un impact perceptible sur les performances de votre appareil.

Suivez les étapes ci-après pour utiliser la fonction d’enregistrement automatique de l’application AEM Forms :

1. Connectez-vous à l’application et accédez à **Paramètres > Général**.
1. Dans l’écran Général, utilisez l’option **Fréquence d’enregistrement automatique** pour choisir les intervalles auxquels vous voulez que l’application enregistre les données saisies.
   [![Définition de la fréquence d’enregistrement automatique](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Lorsque vous redémarrez l’application et que vous vous connectez avec le même nom d’utilisateur, vous êtes invité à restaurer votre tâche à l’aide de la boîte de dialogue de récupération de la tâche non enregistrée. Cliquez sur **OK** dans la boîte de dialogue Récupérer des documents non sauvegardés pour recommencer à travailler sur la tâche enregistrée. Vous pouvez cliquer sur **Annuler** pour supprimer les données enregistrées correspondant au dernier enregistrement automatique déclenché et commencer à travailler sur une nouvelle tâche.

   Si vous cliquez sur **OK**, la tâche est restaurée avec les données correspondant au dernier enregistrement automatique déclenché avant que l’application ne s’arrête. Elle inclut les données d’un formulaire et toutes les pièces jointes liées à la tâche.
   [![Obtention d’une tâche récupérée ](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Un formulaire de travail en cours **B.** Application fermée de force **C.** L’application a redémarré avec la boîte de dialogue Récupérer la tâche non enregistrée **D.** Formulaire restauré avec les données d’origine
