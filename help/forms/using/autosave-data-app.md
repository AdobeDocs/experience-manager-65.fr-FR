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
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 86%
---
# Utiliser l’enregistrement automatique dans l’application AEM Forms{#using-autosave-in-aem-forms-app}

>[!NOTE]
>
>L’application AEM Forms est actuellement obsolète. Pour toute question ou aide, contactez [&#128279;](mailto:aemformsapp-android@adobe.com).

Lorsqu’un utilisateur ou une utilisatrice saisit des données dans l’application Adobe Experience Manager Forms, la fonctionnalité d’enregistrement automatique les enregistre à intervalles réguliers. La fonctionnalité d’enregistrement automatique de l’application AEM Forms vous permet d’éviter la perte de données si l’application se ferme accidentellement.

L’application peut se fermer accidentellement :

* si votre appareil s’arrête car sa batterie est faible ;
* Si l’utilisateur stoppe l’application
* Si une panne inattendue se produit

Vous pouvez spécifier les intervalles auxquels l’application enregistre les données saisies.

>[!NOTE]
>
>Sélectionnez la fréquence d’enregistrement automatique de manière judicieuse. Un enregistrement automatique fréquent peut avoir un impact perceptible sur les performances de votre appareil.

Suivez les étapes ci-après pour utiliser la fonction d’enregistrement automatique de l’application AEM Forms :

1. Connectez-vous à l’application et accédez à **Paramètres > Général**.
1. Dans l’écran Général, utilisez l’option **Fréquence d’enregistrement automatique** pour choisir les intervalles auxquels vous voulez que l’application enregistre les données saisies.
   [![Définition de la fréquence d’enregistrement automatique](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Lorsque vous redémarrez l’application et que vous vous connectez avec le même nom d’utilisateur, vous êtes invité à restaurer votre tâche à l’aide de la boîte de dialogue de récupération de la tâche non enregistrée. Cliquez sur **OK** dans la boîte de dialogue Récupérer des documents non sauvegardés pour recommencer à travailler sur la tâche enregistrée. Vous pouvez cliquer sur **Annuler** pour supprimer les données enregistrées correspondant au dernier enregistrement automatique déclenché et commencer à travailler sur une nouvelle tâche.

   Si vous cliquez sur **OK**, la tâche est restaurée avec les données correspondant au dernier enregistrement automatique déclenché avant que l’application ne s’arrête. Elle inclut les données du formulaire et toutes les pièces jointes liées à la tâche.
   [![Récupération d’une tâche &#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Un formulaire de travail en cours **Application B.** fermée de force **L’application C.** a redémarré avec la boîte de dialogue Récupérer la tâche non enregistrée **Formulaire D.** restauré avec les données d’origine
