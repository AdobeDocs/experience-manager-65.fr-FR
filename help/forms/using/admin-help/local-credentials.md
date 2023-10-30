---
title: Gérer les informations d’identification locales
description: Découvrez comment gérer les informations d’identification locales à l’aide de Trust Store Management. AEM forms prennent en charge les informations d’identification RSA et DSA dans le formulaire PKCS12 standard.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# Gérer les informations d’identification locales {#managing-local-credentials}

Les informations d’identification locales sont des informations d’identification de clé privée hébergées dans Trust Store Management. A *informations d’identification locales* identifie l’emplacement de stockage des informations d’identification DES d’un utilisateur. Trust Store Management vous permet d’importer et de gérer vos informations d’identification locales à l’aide, par exemple, de fichiers PFX existants, afin que vous puissiez importer, modifier et supprimer des informations d’identification locales.

AEM forms prennent en charge les informations d’identification RSA et DSA jusqu’à 4 096 bits au format PKCS12 standard (fichiers .pfx et .p12).

Vous pouvez importer et exporter un nombre indéfini d’informations d’identification. Si vous souhaitez remplacer des informations d’identification expirées par le même alias, supprimez-les, puis importez les nouvelles informations d’identification avec le même alias.

Pour plus d’informations et d’instructions relatives aux extensions Acrobat Reader DC, voir [Configuration des informations d’identification à utiliser avec les extensions Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importation d’informations d’identification {#import-a-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cliquez sur Importer. Sous Type de Trust Store, sélectionnez l’une des options suivantes :

   * **Informations d’identification de signature de document :** informations d’identification utilisées pour émettre une signature numérique sur un document.
   * **Informations d’identification des extensions Acrobat Reader DC :** Un certificat numérique spécifique aux extensions Acrobat Reader DC qui permet l’activation des droits d’utilisation Adobe Reader dans les documents PDF générés.
   * **Valeur par défaut :** Indique qu’il s’agit des informations d’identification par défaut à utiliser avec les extensions Acrobat Reader DC.

   Pour plus d’informations sur l’obtention d’informations d’identification, voir [Préparation à l’installation d’AEM forms](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

1. Dans la zone Alias, saisissez un identifiant pour les informations d’identification. Cet identifiant est utilisé comme nom d’affichage des informations d’identification dans Acrobat Reader DC Extensions et le service Signature. Cet alias est également utilisé pour accéder aux informations d’identification par programmation à l’aide du SDK d’AEM forms.

   >[!NOTE]
   >
   >Le nom d’alias est automatiquement converti en majuscules à des fins d’affichage. Le nom d’alias n’est pas sensible à la casse lorsque vous y faites référence dans un processus.

1. Cliquez sur Parcourir pour localiser les informations d’identification, saisissez le mot de passe de ces informations, puis cliquez sur OK.

   Si le message d’erreur &quot;Échec de l’importation des informations d’identification en raison d’un format de fichier incorrect ou d’un mot de passe incorrect&quot; s’affiche, vérifiez que le mot de passe est valide.

## Exportation d’informations d’identification {#export-a-credential}

Les informations d’identification sont exportées sous la forme de fichiers P12 au format PKCS#12.

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cliquez sur le nom d’alias des informations d’identification à exporter, puis sur Exporter.
1. Dans la zone Mot de passe, saisissez le mot de passe. Ce mot de passe est nouveau et est utilisé pour chiffrer les informations d’identification exportées.
1. Cliquez sur Exporter, suivez les instructions pour exporter les informations d’identification, puis cliquez sur OK.

## Modification de l’alias ou du type de Trust Store d’une identification {#edit-a-credential-s-alias-or-trust-store-type}

Une fois les informations d’identification importées, vous pouvez modifier leur nom d’alias et leur type de Trust Store.

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cliquez sur le nom d’alias des informations d’identification à modifier.
1. Cliquez sur Mettre à jour les informations d’identification.
1. Modifiez le nom d’alias et le type de Trust Store selon les besoins, puis cliquez sur OK.

## Suppression d’informations d’identification {#delete-a-credential}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cochez les cases correspondant aux informations d’identification à supprimer.
1. Cliquez sur Supprimer, puis sur OK.
