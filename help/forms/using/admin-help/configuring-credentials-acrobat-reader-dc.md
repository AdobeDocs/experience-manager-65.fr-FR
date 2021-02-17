---
title: Configuration des informations d’identification à utiliser avec les extensions d’Acrobat Reader DC
seo-title: Configuration des informations d’identification à utiliser avec les extensions d’Acrobat Reader DC
description: Découvrez comment configurer les informations d’identification à utiliser avec les extensions Acrobat Reader DC.
seo-description: Découvrez comment configurer les informations d’identification à utiliser avec les extensions Acrobat Reader DC.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 97%

---


# Configuration des informations d’identification à utiliser avec les extensions d’Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Pour appliquer des droits d’utilisation aux documents PDF, configurez AEM Forms avec des informations d’identification valides pour les extensions d’Acrobat Reader DC. Ces informations d’identification ont éventuellement été configurées pendant l’installation d’AEM Forms. Si vous n’avez configuré aucune information d’identification pour les extensions d’Acrobat Reader DC dans Configuration Manager ou si vous devez importer des informations d’identification nouvelles ou modifiées, utilisez les pages de gestion de Trust Store.

Si vous utilisez des informations d’identification d’évaluation, remplacez-les par des informations d’identification de production lors du passage à votre environnement de production. Pour mettre à jour des informations d’identification d’évaluation ou ayant expiré, vous devez tout d’abord supprimer les anciennes informations d’identification des extensions d’Acrobat Reader DC.

Pour plus de précisions sur l’obtention d’informations d’identification, voir [Préparation à l’installation d’AEM Forms sur un seul serveur](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

Le Trust Store peut comporter plusieurs jeux d’informations d’identification des extensions d’Acrobat Reader DC. Vous devez désigner l’un de ces jeux d’informations d’identification en tant que valeurs par défaut des informations d’identification de Reader Extensions. Les informations d’identification par défaut sont utilisées lorsqu’un utilisateur de Workbench ne parvient pas à déterminer quelles informations d’identification utiliser lors de la création du processus. Ces règles s’appliquent aux informations d’identification par défaut :

* Si vous importez un jeu d’informations d’identification pour les extensions d’Acrobat Reader DC et que le Trust Store n’en comporte pas d’autres, il est défini comme valeur par défaut.
* Si vous importez un jeu d’informations d’identification pour les extensions d’Acrobat Reader DC avec l’option Par défaut sélectionnée, le type par défaut est supprimé du jeu d’informations d’identification par défaut existant. Le jeu d’informations d’identification importé devient la valeur par défaut.
* Vous ne pouvez pas supprimer un jeu d’informations d’identification des extensions d’Acrobat Reader DC par défaut. Il vous faut au préalable définir un autre jeu d’informations d’identification comme valeur par défaut. Il existe néanmoins une exception à cette règle : s’il n’existe qu’un seul jeu d’informations d’identification, vous pouvez le supprimer, même s’il s’agit de la valeur par défaut.
* Vous ne pouvez pas mettre à jour un jeu d’informations d’identification des extensions d&#39;Acrobat Reader DC par défaut.

>[!NOTE]
>
>vous pouvez également importer et supprimer des informations d’identification automatiquement (Voir [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63)).

## Importation des données d’identification des extensions d’Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cliquez sur Importer, puis sous Type de Trust Store, sélectionnez Informations d’identification des extensions d’Acrobat Reader DC.
1. (Facultatif) Pour indiquer qu’il s’agit des informations d’identification par défaut à utiliser avec les extensions d’Acrobat Reader DC, sélectionnez Par défaut.
1. Dans la zone Alias, saisissez un identificateur pour les informations d’identification. Cet identifiant sert de nom d’affichage aux informations d’identification dans les extensions d’Acrobat Reader DC. Il permet également d’accéder automatiquement aux informations d’identification via le SDK d’AEM Forms.

   >[!NOTE]
   >
   >le nom d’alias est converti automatiquement en caractères majuscules à des fins d’affichage. Il n’est pas sensible à la casse lorsque vous y faites référence dans un processus.

1. Cliquez sur Choisir un fichier pour accéder aux informations d’identification, saisissez le mot de passe correspondant, puis cliquez sur OK.

   Si le message d’erreur « Echec de l’importation des informations d’identification en raison d’un format de fichier incorrect ou d’un mot de passe incorrect » s’affiche, assurez-vous que le mot de passe est valide.

## Suppression des informations d’identification des extensions d’Acrobat Reader DC  {#remove-a-acrobat-reader-dc-extensions-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Sélectionnez les informations d’identification, puis cliquez sur Supprimer.

## Remplacement des informations d’identification des extensions d’Acrobat Reader DC  {#replace-a-acrobat-reader-dc-extensions-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Notez l’alias existant des informations d’identification, sélectionnez-le, puis cliquez sur Supprimer.
1. Importez les nouvelles informations d’identification à l’aide du même nom d’alias.

