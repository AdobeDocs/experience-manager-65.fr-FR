---
title: Enregistrer les formulaires sous forme de modèles
description: Découvrez comment créer des modèles à partir de formulaires contenant des données requises de manière répétée.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b97175fd-cc3d-457a-af11-1f8c83192eb7
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
source-wordcount: '340'
ht-degree: 95%
---
# Enregistrer les formulaires sous forme de modèles {#save-forms-as-templates}

>[!NOTE]
>
>L’application AEM Forms est actuellement obsolète. Pour toute question ou aide, contactez [&#128279;](mailto:aemformsapp-android@adobe.com).

Parfois, lorsque les utilisateurs et utilisatrices remplissent un formulaire, les entrées de quelques champs restent les mêmes. Pour ces types d’instances, vous pouvez remplir les champs nécessitant des valeurs identiques dans chaque instance et enregistrer le formulaire ou le brouillon comme modèle. Ainsi, chaque fois que vous créerez une instance du modèle, les champs spécifiés seront déjà remplis avec les valeurs spécifiées dans le modèle. Cela vous permet de gagner du temps et de fournir moins d’efforts pour remplir le formulaire.

Procédez comme suit pour créer un modèle :

1. Ouvrez un formulaire et sélectionnez ou remplissez les champs dont les valeurs sont presque identiques à chaque fois que vous l’utilisez. Vous pouvez inclure une pièce jointe au modèle que vous ajoutez généralement lorsque vous remplissez le formulaire.
1. Sélectionnez l’icône **Enregistrer en tant que modèle** ![save_as_template](assets/save_as_template.png). Une boîte de dialogue pour indiquer le nom du modèle s’affiche.
1. Indiquez le nom du modèle et sélectionnez **Enregistrer**. Le modèle apparaît dans le dossier de modèles.

   S’il existe un modèle avec le même nom, une boîte de dialogue s’affiche pour confirmer le remplacement du modèle existant. Pour remplacer le modèle existant par un nouveau modèle, sélectionnez **Continuer** ou, pour enregistrer le modèle sous un autre nom, sélectionnez **Annuler**.

Vous pouvez maintenant ouvrir le modèle enregistré. Chaque fois qu’un modèle s’ouvre, un nouveau formulaire ou une nouvelle tâche est créé et le formulaire affiche les données enregistrées et les options. Grâce aux modèles, vous pouvez modifier les données préremplies, ajouter une pièce jointe, enregistrer en tant que brouillon, envoyer la tâche, ou les utiliser pour créer un autre modèle. Les modèles sont spécifiques aux appareils mobiles et ne sont pas synchronisés avec le serveur Adobe Experience Manager Forms.

Vous pouvez également supprimer un modèle si vous n’en avez plus besoin. Pour supprimer un modèle, accédez au dossier de modèles, sélectionnez les points de suspension, puis **Supprimer le modèle**.

>[!NOTE]
>
>Un modèle est disponible localement et n’est pas synchronisé avec le serveur. L’effacement des données locales de l’application supprime le modèle.
