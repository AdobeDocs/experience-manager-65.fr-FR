---
title: Configuration des informations d’identification à utiliser avec les extensions Acrobat Reader DC
description: Découvrez comment configurer les informations d’identification à utiliser avec les extensions Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
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
source-wordcount: '583'
ht-degree: 100%
---
# Configuration des informations d’identification à utiliser avec les extensions Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Pour appliquer des droits d’utilisation aux documents PDF, configurez AEM forms avec des informations d’identification valides pour les extensions Acrobat Reader DC. Des informations d’identification peuvent avoir été configurées lors de l’installation d’AEM forms. Si vous n’avez pas configuré vos informations d’identification pour les extensions Acrobat Reader DC lors de l’exécution de Configuration Manager ou si vous devez importer des informations d’identification nouvelles ou de remplacement, vous pouvez le faire à l’aide des pages de gestion du Trust Store.

Si vous utilisez des informations d’identification d’évaluation, remplacez-les par des informations d’identification de production lors du passage à votre environnement de production. Pour mettre à jour des informations d’identification d’évaluation ou ayant expiré, supprimez d’abord les anciennes informations d’identification des extensions Acrobat Reader DC.

Pour plus d’informations sur l’obtention d’informations d’identification, voir [Préparation à l’installation d’AEM Forms (serveur unique)](https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf).

Trust Store peut comporter plusieurs informations d’identification pour les extensions Acrobat Reader DC. Désignez l’une de ces informations d’identification comme informations d’identification des extensions Reader par défaut. Les informations d’identification par défaut sont utilisées lorsqu’un utilisateur ou une utilisatrice de Workbench ne parvient pas à déterminer les informations d’identification à utiliser lors de la création du processus. Ces règles s’appliquent aux informations d’identification par défaut :

* Si vous importez des informations d’identification pour les extensions Acrobat Reader DC et que Trust Store n’en comporte pas d’autres, elle sont définies comme valeur par défaut.
* Si vous importez des informations d’identification pour les extensions Acrobat Reader DC avec l’option Par défaut sélectionnée, le type par défaut est supprimé du jeu d’informations d’identification par défaut existant. Le jeu d’informations d’identification importé devient la valeur par défaut.
* Vous ne pouvez pas supprimer des informations d’identification par défaut des extensions Acrobat Reader DC. Pour supprimer les informations d’identification par défaut, définissez d’abord d’autres informations d’identification comme valeur par défaut. Une exception à cette règle est que s’il n’existe qu’une seule information d’identification, vous pouvez la supprimer, même s’il s’agit de la valeur par défaut.
* Vous ne pouvez pas mettre à jour des informations d’identification par défaut pour les extensions Acrobat Reader DC.

>[!NOTE]
>
>Vous pouvez également importer et supprimer des informations d’identification par programmation. (Voir [Programmation avec AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).)

## Importer des informations d’identification pour les extensions Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

1. Dans la console d’administration, cliquez sur Paramètres > Gestion du Trust Store > Informations d’identification locales.
1. Cliquez sur Importer, puis, sous Type de Trust Store, sélectionnez Informations d’identification pour les extensions Acrobat Reader DC.
1. (Facultatif) Pour indiquer que ces informations d’identification constituent les informations d’identification par défaut à utiliser avec les extensions Acrobat Reader DC, sélectionnez Par défaut.
1. Dans la zone Alias, saisissez un identifiant pour les informations d’identification. Cet identifiant est utilisé comme nom d’affichage des informations d’identification dans les extensions Acrobat Reader DC. Cet alias est également utilisé pour accéder aux informations d’identification par programmation à l’aide du SDK AEM Forms.

   >[!NOTE]
   >
   >Le nom d’alias est automatiquement converti en majuscules à des fins d’affichage. Le nom d’alias n’est pas sensible à la casse lorsque vous y faites référence dans un processus.

1. Cliquez sur Choisir un fichier pour localiser les informations d’identification, saisissez le mot de passe correspondant, puis cliquez sur OK.

   Si le message d’erreur « Échec de l’import des informations d’identification en raison d’un format de fichier incorrect ou d’un mot de passe incorrect » s’affiche, assurez-vous que le mot de passe est valide.

## Suppression d’informations d’identification pour les extensions Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. Dans la console d’administration, cliquez sur Paramètres > Gestion du Trust Store > Informations d’identification locales.
1. Sélectionnez les informations d’identification, puis cliquez sur Supprimer.

## Remplacement des informations d’identification pour les extensions Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. Dans la console d’administration, cliquez sur Paramètres > Gestion du Trust Store > Informations d’identification locales.
1. Notez l’alias des informations d’identification existantes, sélectionnez-le, puis cliquez sur Supprimer.
1. Importez les nouvelles informations d’identification en utilisant exactement le même nom d’alias.
