---
title: Gestion des informations d’identification locales
description: Découvrez comment gérer les informations d’identification locales à l’aide de Trust Store Management. AEM Forms prend en charge les informations d’identification RSA et DSA au format PKCS12 standard.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 100%

---

# Gérer les informations d’identification locales {#managing-local-credentials}

Les informations d’identification locales sont des informations d’identification de clé privée hébergées dans Trust Store Management. Les *informations d’identification locales* identifient l’emplacement des informations d’identification DES d’un utilisateur ou d’une utilisatrice. Trust Store Management vous permet d’importer, de modifier et de supprimer vos informations d’identification locales en utilisant, par exemple, des fichiers PFX existants.

AEM Forms prend en charge les informations d’identification RSA et DSA jusqu’à 4096 bits au format PKCS12 standard (fichiers .pfx et .p12).

Vous pouvez en importer et en exporter autant que vous le souhaitez. Si vous souhaitez remplacer des informations d’identification expirées en utilisant le même alias, supprimez-les, puis importez les nouvelles informations d’identification avec le même alias.

Pour obtenir des informations et des instructions concernant les extensions Acrobat Reader DC, consultez la section [Configuration des informations d’identification à utiliser avec les extensions Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importation d’informations d’identification {#import-a-credential}

1. Dans la console d’administration, cliquez sur Paramètres >Gestion de Trust Store > Informations d’identification locales.
1. Cliquez sur Importer, puis, sous Type de Trust Store, sélectionnez l’une des options suivantes :

   * **Informations d’identification de signature de document :** informations d’identification utilisées pour émettre une signature numérique sur un document.
   * **Informations d’identification des extensions Acrobat Reader DC :** certificat numérique spécifique des extensions Acrobat Reader DC qui permet l’activation de droits Adobe Reader dans les documents PDF générés.
   * **Par défaut :** indique qu’il s’agit des informations d’identification par défaut à utiliser avec les extensions Acrobat Reader DC.

   Pour plus d’informations sur l’obtention d’informations d’identification, voir [Préparation à l’installation d’AEM Forms](https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf).

1. Dans la zone Alias, saisissez un identifiant pour les informations d’identification. Cet identifiant sert de nom d’affichage aux informations d’identification dans les extensions Acrobat Reader DC et dans le service Signature. Cet alias est également utilisé pour accéder aux informations d’identification par programmation à l’aide du SDK AEM Forms.

   >[!NOTE]
   >
   >Le nom d’alias est automatiquement converti en majuscules à des fins d’affichage. Le nom d’alias n’est pas sensible à la casse lorsque vous y faites référence dans un processus.

1. Cliquez sur Parcourir pour accéder aux informations d’identification, saisissez le mot de passe correspondant, puis cliquez sur OK.

   Si le message d’erreur « Échec de l’import des informations d’identification en raison d’un format de fichier incorrect ou d’un mot de passe incorrect » s’affiche, assurez-vous que le mot de passe est valide.

## Exportation des informations d’identification {#export-a-credential}

Elles sont exportées sous forme de fichiers P12 au format PKCS#12.

1. Dans la console d’administration, cliquez sur Paramètres >Gestion de Trust Store > Informations d’identification locales.
1. Cliquez sur le nom d’alias des informations d’identification à exporter, puis sur Exporter.
1. Dans le champ Mot de passe, saisissez le mot de passe. Ce mot de passe est nouveau et permet de chiffrer les informations d’identification exportées.
1. Cliquez sur Exporter, suivez les instructions pour exporter les informations d’identification, puis cliquez sur OK.

## Modification de l’alias ou du type de Trust Store des informations d’identification {#edit-a-credential-s-alias-or-trust-store-type}

Une fois que des informations d’identification ont été importées, vous pouvez modifier le nom d’alias et le type de Trust Store qui leur sont associés.

1. Dans la console d’administration, cliquez sur Paramètres >Gestion de Trust Store > Informations d’identification locales.
1. Cliquez sur le nom d’alias des informations d’identification à modifier.
1. Cliquez sur Mettre à jour les informations d’identification.
1. Modifiez le nom d’alias et le type de Trust Store selon vos besoins, puis cliquez sur OK.

## Supprimer les informations d’identification {#delete-a-credential}

1. Dans la console d’administration, cliquez sur Paramètres >Gestion de Trust Store > Informations d’identification locales.
1. Cochez les cases correspondant aux informations d’identification à supprimer.
1. Cliquez sur Supprimer, puis sur OK.
