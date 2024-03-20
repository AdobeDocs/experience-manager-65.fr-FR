---
title: Vérifier les informations d’identification de l’utilisateur
description: Découvrez comment consulter les informations d’utilisation des informations d’identification. Les informations d’utilisation des informations d’identification qui décrivent son utilisation sont accessibles via l’extension Acrobat Reader.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%

---

# Vérifier les informations d’identification de l’utilisateur {#review-credential-use-information}

Les informations d’identification contiennent des informations décrivant son utilisation prévue, accessibles par le biais de l’application web pour utilisateurs finaux d’Acrobat Reader DC extensions. Vous pouvez utiliser ces informations pour déterminer le type d’informations d’identification installées (évaluation ou production) et ses dates de validité.

1. Ouvrez un navigateur web et saisissez l’URL suivante :

   http://localhost:port/ReaderExtensions (où *port* correspond au numéro de port du serveur d’applications)

1. Connectez-vous à l’aide du nom d’utilisateur et du mot de passe par défaut :

   Nom d’utilisateur : administrator

   Mot de passe : password

   >[!NOTE]
   >
   >Vous devez disposer de droits d’administrateur ou de super utilisateur pour vous connecter à l’aide du nom d’utilisateur et du mot de passe par défaut. Pour permettre à d’autres utilisateurs d’accéder aux extensions Acrobat Reader DC, créez les comptes d’utilisateurs dans User Management et attribuez aux utilisateurs le rôle Application Web des extensions Acrobat Reader DC.

1. Sélectionnez l’alias des informations d’identification dans la liste Sélectionner les informations d’identification et passez en revue les informations incluses dans les sections Date d’expiration et Avis d’utilisation prévue.

>[!NOTE]
>
>La date d’expiration des informations d’identification est également disponible sur la page Paramètres > Trust Store Management > Informations d’identification locales d’Administration Console, sous Date d’expiration.
