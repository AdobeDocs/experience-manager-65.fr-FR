---
title: Intégration à Adobe Sign | Gestion des données utilisateur
description: Découvrez l’intégration d’AEM Forms à Adobe Sign pour les signatures électroniques dans les formulaires adaptatifs. Elle prend en charge plusieurs options de signature pour différents workflows.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: a16aea24-4e85-528d-9377-cd80bb039c1d
    internal-label: Acrobat Sign
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 100%
---
# Intégration à Adobe Sign | Gestion des données utilisateur {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] s’intègre à [!DNL  Adobe Sign] pour autoriser les processus de signature électronique dans les formulaires adaptatifs pour traiter des formulaires ou des contrats pour les flux de travail juridiques, commerciaux, de rémunération et de gestion des ressources humaines. Il autorise les processus de signature pour un ou plusieurs utilisateurs, des processus séquentiels et simultanés, la signature de formulaire en tant qu’utilisateur anonyme ou connecté et propose plusieurs méthodes d’authentification pour les utilisateurs.

Lorsqu’un ou plusieurs utilisateurs signent et envoient un formulaire adaptatif, un contrat [!DNL Adobe Sign] contenant des informations sur les signataires est généré.

Pour plus d’informations sur l’intégration d’[!DNL AEM Forms] à [!DNL Adobe Sign], consultez la section [Utiliser Adobe Sign dans un formulaire adaptatif](/help/forms/using/working-with-adobe-sign.md).

## Données utilisateur et stockage de données {#data}

Le formulaire adaptatif activé par [!DNL Adobe Sign] inclut des informations sur les signataires et peut inclure d’autres données utilisateur collectées par le formulaire adaptatif. Le service [!DNL Adobe Sign] enregistre les données de l’utilisateur à l’aide de la signature du contrat. Le contrat est enregistré sur le serveur [!DNL Adobe Sign] configuré dans les services cloud d’[!DNL AEM Forms]. En outre, si le formulaire adaptatif est configuré pour utiliser l’action d’envoi du portail Formulaires, les données de contrat sont enregistrées dans le magasin de données du portail Formulaires avec les données de formulaire.

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Les données utilisateur sont collectées dans le contrat, mais ne sont enregistrées dans aucun des tableaux de service. [!DNL Adobe Sign] permet aux administrateurs et aux administratrice de faire leurs propres choix concernant la gestion des données qu’ils contrôlent dans le service. Les administrateurs et administratrices de confidentialité sur le service d’[!DNL Adobe Sign] peuvent répertorier ou supprimer des contrats en fonction de l’adresse e-mail du demandeur ou de la demandeuse.

[!DNL Adobe Sign] propose une application web qui permet de rechercher des contrats en filtrant par participants et participantes et, si nécessaire, de les supprimer. Pour plus d’informations, consultez la section [Adobe Sign - Fonctionnalité : supprimer les informations de l’utilisateur](https://helpx.adobe.com/fr/sign/using/gdpr-compliance.html).

Les données de contrat pour les formulaires adaptatifs configurés pour utiliser l’action d’envoi du portail Formulaires sont également enregistrées dans le magasin de données du portail Formulaires. Pour accéder aux données du magasin de données du portail Formulaires et les supprimer, voir [Portail Formulaires | Gestion des données utilisateur](/help/forms/using/forms-portal-handling-user-data.md).
