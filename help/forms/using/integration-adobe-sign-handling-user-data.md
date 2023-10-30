---
title: Intégration à Adobe Sign | Gestion des données utilisateur
description: AEM Forms intègre Adobe Sign pour les signatures électroniques dans les formulaires adaptatifs. Il prend en charge plusieurs options de signature pour différents workflows.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 54%

---

# Intégration à Adobe Sign | Gestion des données utilisateur {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] s’intègre à pour autoriser les processus de signature électronique dans les formulaires adaptatifs pour traiter des formulaires ou des contrats pour les flux de travail juridiques, commerciaux, de rémunération et de gestion des ressources humaines. [!DNL  Adobe Sign] Il autorise les processus de signature pour un ou plusieurs utilisateurs, des processus séquentiels et simultanés, la signature de formulaire en tant qu’utilisateur anonyme ou connecté et propose plusieurs méthodes d’authentification pour les utilisateurs.

Lorsqu’un ou plusieurs utilisateurs signent et envoient un formulaire adaptatif, un contrat [!DNL Adobe Sign] contenant des informations sur les signataires est généré.

Pour plus d’informations sur l’intégration d’[!DNL AEM Forms] à [!DNL Adobe Sign], consultez la section [Utiliser Adobe Sign dans un formulaire adaptatif](/help/forms/using/working-with-adobe-sign.md).

## Données utilisateur et stockage de données {#data}

Le formulaire adaptatif activé par [!DNL Adobe Sign] inclut des informations sur les signataires et peut inclure d’autres données utilisateur collectées par le formulaire adaptatif. Le service [!DNL Adobe Sign] enregistre les données de l’utilisateur à l’aide de la signature du contrat. L&#39;accord est enregistré sur un [!DNL Adobe Sign] serveur configuré dans [!DNL AEM Forms] services cloud. En outre, si le formulaire adaptatif est configuré pour utiliser l’action d’envoi du portail Forms, les données de contrat sont enregistrées dans l’entrepôt de données du portail Forms avec les données de formulaire.

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Les données utilisateur sont collectées dans le contrat, mais ne sont enregistrées dans aucune des tables de service. [!DNL Adobe Sign] permet aux administrateurs d’effectuer leurs propres choix sur la gestion des données qu’ils contrôlent dans le service. Les administrateurs de confidentialité sur le service d’[!DNL Adobe Sign] peuvent répertorier ou supprimer des contrats en fonction de l’adresse e-mail du demandeur.

[!DNL Adobe Sign] propose une application web permettant la recherche des accords par les participants, et si nécessaire, leur suppression. Pour plus d’informations, consultez la section [Adobe Sign - Fonctionnalité : supprimer les informations de l’utilisateur](https://helpx.adobe.com/fr/sign/using/gdpr-compliance.html).

Les données d’accord pour les formulaires adaptatifs configurés pour utiliser l’action d’envoi du portail Forms sont également enregistrées dans l’entrepôt de données du portail Forms. Pour accéder aux données de l’entrepôt de données de Forms Portal et les supprimer, voir [Portail Forms | Gestion des données utilisateur](/help/forms/using/forms-portal-handling-user-data.md).
