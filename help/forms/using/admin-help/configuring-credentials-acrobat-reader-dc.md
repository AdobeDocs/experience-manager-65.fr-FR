---
title: Configuration des informations d’identification à utiliser avec les extensions Acrobat Reader DC
description: Découvrez comment configurer les informations d’identification à utiliser avec les extensions Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# Configuration des informations d’identification à utiliser avec les extensions Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Pour appliquer des droits d’utilisation aux documents PDF, configurez AEM forms avec des informations d’identification valides pour Acrobat Reader DC Extensions. Des informations d’identification peuvent avoir été configurées lors de l’installation d’AEM forms. Si vous n’avez pas configuré vos informations d’identification Acrobat Reader DC Extensions lors de l’exécution de Configuration Manager ou si vous devez importer des informations d’identification nouvelles ou de remplacement, vous pouvez le faire à l’aide des pages de gestion du Trust Store.

Si vous utilisez des informations d’identification d’évaluation, remplacez-les par des informations d’identification de production lors du passage à votre environnement de production. Pour mettre à jour des informations d’identification d’évaluation ou expirées, supprimez d’abord les anciennes informations d’identification d’Acrobat Reader DC Extensions.

Pour plus d’informations sur l’obtention d’informations d’identification, voir [Préparation à l’installation d’AEM forms (serveur unique)](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

Trust Store peut contenir plusieurs informations d’identification Acrobat Reader DC Extensions. Désigner l’une de ces informations d’identification comme informations d’identification Reader Extensions par défaut. Les informations d’identification par défaut sont utilisées lorsqu’un utilisateur de Workbench ne parvient pas à déterminer les informations d’identification à utiliser lors de la création du processus. Ces règles s’appliquent aux informations d’identification par défaut :

* Si vous importez des informations d’identification Acrobat Reader DC Extensions et que Trust Store ne contient aucune autre information d’identification Acrobat Reader DC Extensions, elles sont définies comme valeur par défaut.
* Si vous importez des informations d’identification Acrobat Reader DC Extensions avec l’option Par défaut sélectionnée, le type par défaut est supprimé d’un jeu d’informations d’identification par défaut existant. Le jeu d’informations d’identification importé devient la valeur par défaut.
* Vous ne pouvez pas supprimer d’informations d’identification Acrobat Reader DC Extensions par défaut. Pour supprimer les informations d’identification par défaut, définissez d’abord une autre information d’identification comme valeur par défaut. Une exception à cette règle est que s’il n’existe qu’un seul identifiant, vous pouvez le supprimer, même s’il s’agit de la valeur par défaut.
* Vous ne pouvez pas mettre à jour des informations d’identification Acrobat Reader DC Extensions par défaut.

>[!NOTE]
>
>Vous pouvez également importer et supprimer des informations d’identification par programmation. (Voir [Programmation avec les AEM forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).)

## Importation d’informations d’identification Acrobat Reader DC Extensions {#import-a-acrobat-reader-dc-extensions-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cliquez sur Importer, puis, sous Type de Trust Store, sélectionnez Informations d’identification Acrobat Reader DC Extensions.
1. (Facultatif) Pour indiquer que ces informations d’identification sont les informations d’identification par défaut à utiliser avec les extensions Acrobat Reader DC, sélectionnez Par défaut.
1. Dans la zone Alias, saisissez un identifiant pour les informations d’identification. Cet identifiant est utilisé comme nom d’affichage des informations d’identification dans Acrobat Reader DC Extensions. Cet alias est également utilisé pour accéder aux informations d’identification par programmation à l’aide du SDK d’AEM forms.

   >[!NOTE]
   >
   >Le nom d’alias est automatiquement converti en majuscules à des fins d’affichage. Le nom d’alias n’est pas sensible à la casse lorsque vous y faites référence dans un processus.

1. Cliquez sur Choisir un fichier pour accéder aux informations d’identification, saisissez le mot de passe correspondant, puis cliquez sur OK.

   Si le message d’erreur &quot;Échec de l’importation des informations d’identification en raison d’un format de fichier incorrect ou d’un mot de passe incorrect&quot; s’affiche, vérifiez que le mot de passe est valide.

## Suppression d’informations d’identification Acrobat Reader DC Extensions {#remove-a-acrobat-reader-dc-extensions-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Sélectionnez les informations d’identification, puis cliquez sur Supprimer.

## Remplacement des informations d’identification d’Acrobat Reader DC Extensions {#replace-a-acrobat-reader-dc-extensions-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Notez l’alias des informations d’identification existantes, sélectionnez-le, puis cliquez sur Supprimer.
1. Importez les nouvelles informations d’identification en utilisant exactement le même nom d’alias.
