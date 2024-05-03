---
title: Vérification de l’utilisation des informations d’identification
description: Découvrez comment vérifier les informations d’utilisation des informations d’identification. Les informations d’utilisation des informations d’identification qui décrivent son utilisation sont accessibles via l’extension Acrobat Reader.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 100%

---

# Vérifier les informations d’identification de l’utilisateur {#review-credential-use-information}

Les informations d’identification contiennent des informations décrivant son utilisation prévue. Elles sont accessibles par le biais de l’application web pour les utilisateurs finaux et utilisatrices finales des extensions d’Acrobat Reader DC. Vous pouvez utiliser ces informations pour déterminer le type d’informations d’identification installées (évaluation ou production) et les dates de validité.

1. Ouvrez un navigateur web et saisissez l’URL suivante :

   http://localhost:port/ReaderExtensions (où *port* correspond au numéro de port du serveur d’applications)

1. Connectez-vous à l’aide du nom d’utilisateur ou d’utilisatrice et du mot de passe par défaut :

   Nom d’utilisateur ou d’utilisatrice : administrator

   Mot de passe : password

   >[!NOTE]
   >
   >Vous devez disposer de droits d’administration, de super-utilisateur ou de super-utilisatrice pour vous connecter à l’aide du nom d’utilisateur ou d’utilisatrice et du mot de passe par défaut. Pour permettre à d’autres utilisateurs et utilisatrices d’accéder aux Extensions Acrobat Reader DC, créez leur compte dans User Management et attribuez-leur le rôle d’application web des Extensions Acrobat Reader DC.

1. Sélectionnez l’alias des informations d’identification dans la liste Sélectionner les informations d’identification et passez en revue les informations incluses dans les sections Date d’expiration et Avis d’utilisation prévue.

>[!NOTE]
>
>La date d’expiration des informations d’identification est également disponible sur la page Paramètres > Trust Store Management > Informations d’identification locales de la console d’administration, sous Date d’expiration.
