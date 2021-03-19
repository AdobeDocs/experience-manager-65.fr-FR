---
title: Intégration à Adobe Sign | Gestion des données utilisateur
seo-title: Intégration à Adobe Sign | Gestion des données utilisateur
description: Intégration à Adobe Sign | Gestion des données utilisateur
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 70%

---


# Intégration à Adobe Sign | Gestion des données utilisateur {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] s’intègre à pour autoriser les processus de signature électronique dans les formulaires adaptatifs pour traiter des formulaires ou des contrats pour les flux de travail juridiques, commerciaux, de rémunération et de gestion des ressources humaines. [!DNL  Adobe Sign] Il autorise les processus de signature pour un ou plusieurs utilisateurs, des processus séquentiels et simultanés, la signature de formulaire en tant qu’utilisateur anonyme ou connecté et propose plusieurs méthodes d’authentification pour les utilisateurs.

Lorsqu’un signataire ou plusieurs signataires signent et envoient un formulaire adaptatif, un accord [!DNL Adobe Sign] est généré qui contient des informations sur les signataires.

Pour plus d&#39;informations sur l&#39;intégration de [!DNL AEM Forms] à [!DNL Adobe Sign], voir [Utilisation de Adobe Sign dans un formulaire adaptatif](/help/forms/using/working-with-adobe-sign.md).

## Données utilisateur et stockage de données {#data}

[!DNL Adobe Sign]Le formulaire adaptatif activé par inclut des informations sur les signataires et peut inclure d’autres données utilisateur collectées par le formulaire adaptatif. Le service [!DNL Adobe Sign] enregistre les données utilisateur avec la signature dans l&#39;accord. L&#39;accord est enregistré sur le serveur [!DNL Adobe Sign] configuré dans les services de cloud [!DNL AEM Forms]. Par ailleurs, si le formulaire adaptatif est configuré pour utiliser l’action d’envoi du portail Forms, les données du contrat sont enregistrées dans le stockage de données du portail Forms avec les données du formulaire.

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Les données utilisateur sont collectées dans le contrat mais ne sont enregistrées dans aucune des tables de service. [!DNL Adobe Sign] permet aux administrateurs de faire leurs propres choix concernant la gestion des données qu’ils contrôlent dans le service. Les administrateurs de la confidentialité sur le service [!DNL Adobe Sign] peuvent liste ou supprimer des accords basés sur l&#39;adresse électronique d&#39;un demandeur.

[!DNL Adobe Sign] propose une application Web qui permet de rechercher des contrats en filtrant par participants et, si nécessaire, de les supprimer. Pour plus d’informations, voir [Adobe Sign - Feature : Supprimer les informations utilisateur](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Les données de contrat des formulaires adaptatifs configurés pour utiliser l’action d’envoi du portail Forms sont également enregistrées dans le stockage de données du portail Forms. Pour accéder à des données et les supprimer depuis le stockage de données du portail Forms, reportez-vous à la section [Portail Forms | Gestion des données utilisateur](/help/forms/using/forms-portal-handling-user-data.md).
