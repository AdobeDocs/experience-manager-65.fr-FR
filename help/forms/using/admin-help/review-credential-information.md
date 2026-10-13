---
title: Vérification de l’utilisation des informations d’identification
description: Découvrez comment vérifier les informations d’utilisation des informations d’identification. Les informations d’utilisation des informations d’identification qui décrivent son utilisation sont accessibles via l’extension Acrobat Reader.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
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
source-wordcount: '196'
ht-degree: 94%
---
# Vérifier les informations d’identification de l’utilisateur {#review-credential-use-information}

Les informations d’identification contiennent des informations décrivant son utilisation prévue. Elles sont accessibles par le biais de l’application web pour les utilisateurs finaux et utilisatrices finales des extensions d’Acrobat Reader DC. Vous pouvez utiliser ces informations pour déterminer le type d’informations d’identification installées (évaluation ou production) et les dates de validité.

1. Ouvrez un navigateur web et saisissez l’URL suivante :

   :port/ReaderExtensions (où *port* correspond au numéro de port du serveur d’applications)

1. Connectez-vous à l’aide du nom d’utilisateur et du mot de passe par défaut :

   Nom d’utilisateur ou d’utilisatrice : administrator

   Mot de passe : password

   >[!NOTE]
   >
   >Vous devez disposer de droits d’administration, de super-utilisateur ou de super-utilisatrice pour vous connecter à l’aide du nom d’utilisateur ou d’utilisatrice et du mot de passe par défaut. Pour permettre à d’autres utilisateurs et utilisatrices d’accéder aux Extensions Acrobat Reader DC, créez leurs comptes dans User Management et attribuez-leur le rôle d’application web des Extensions Acrobat Reader DC.

1. Sélectionnez l’alias des informations d’identification dans la liste Sélectionner les informations d’identification et vérifiez les informations incluses dans Date d’expiration et Avis d’utilisation prévue.

>[!NOTE]
>
>La date d’expiration des informations d’identification est également disponible sur la page Paramètres > Trust Store Management > Informations d’identification locales de la console d’administration, sous Date d’expiration.
