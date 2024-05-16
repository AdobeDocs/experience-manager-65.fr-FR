---
title: Utiliser l’enregistrement automatique dans l’application AEM Forms
description: Découvrez comment utiliser la fonctionnalité d’enregistrement automatique dans l’application AEM Forms afin d’éviter la perte de données.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '294'
ht-degree: 100%

---

# Utiliser l’enregistrement automatique dans l’application AEM Forms{#using-autosave-in-aem-forms-app}

Lorsqu’un utilisateur ou une utilisatrice saisit des données dans l’application Adobe Experience Manager Forms, la fonctionnalité d’enregistrement automatique les enregistre à intervalles réguliers. La fonctionnalité d’enregistrement automatique de l’application AEM Forms vous permet d’éviter la perte de données si l’application se ferme accidentellement.

L’application se ferme accidentellement :

* si votre appareil s’arrête car sa batterie est faible ;
* Si l’utilisateur stoppe l’application
* si une panne inattendue se produit.

Vous pouvez spécifier les intervalles auxquels l’application enregistre les données saisies.

>[!NOTE]
>
>Sélectionnez la fréquence d’enregistrement automatique de manière judicieuse. Un enregistrement automatique fréquent peut avoir un impact perceptible sur les performances de votre appareil.

Suivez les étapes ci-après pour utiliser la fonction d’enregistrement automatique de l’application AEM Forms :

1. Connectez-vous à l’application et accédez à **Paramètres > Général**.
1. Dans l’écran Général, utilisez l’option **Fréquence d’enregistrement automatique** pour choisir les intervalles auxquels vous voulez que l’application enregistre les données saisies.
   [![Définition de la fréquence d’enregistrement automatique](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Lorsque vous redémarrez l’application et que vous vous connectez avec le même nom d’utilisateur, vous êtes invité à restaurer votre tâche à l’aide de la boîte de dialogue de récupération de la tâche non enregistrée. Cliquez sur **OK** dans la boîte de dialogue Récupérer des documents non sauvegardés pour recommencer à travailler sur la tâche enregistrée. Vous pouvez cliquer sur **Annuler** pour supprimer les données enregistrées correspondant au dernier enregistrement automatique déclenché et commencer à travailler sur une nouvelle tâche.

   Si vous cliquez sur **OK**, la tâche est restaurée avec les données correspondant au dernier enregistrement automatique déclenché avant que l’application ne s’arrête. Elle inclut les données d’un formulaire et toutes les pièces jointes liées à la tâche.
   [![Obtenir une tâche récupérée ](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Un formulaire de travail en cours **B.** Application fermée de force **C.** L’application a redémarré avec la boîte de dialogue Récupérer la tâche non enregistrée **D.** Formulaire restauré avec les données d’origine
