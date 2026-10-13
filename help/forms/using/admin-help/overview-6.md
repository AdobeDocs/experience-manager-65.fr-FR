---
title: Présentation de la configuration SSL
description: Découvrez comment améliorer la sécurité de la communication grâce à la configuration SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
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
source-wordcount: '213'
ht-degree: 100%
---
# Présentation de la configuration SSL {#overview-of-configuring-ssl}

Vous pouvez créer des informations d’identification Secure Sockets Layer (SSL) et configurer SSL sur le serveur d’applications afin de mieux sécuriser la communication avec votre serveur d’applications.

En tant que solution de sécurité, Rights Management requiert la configuration SSL. Lorsque vous configurez des certificats SSL, veillez à n’utiliser que des clés RSA. Les certificats SSL avec clés DSA ne sont pas pris en charge.

Les informations fournies s’appliquent aux procédures d’installation clé en main, automatique et manuelle. Elles décrivent une méthode parmi d’autres, permettant de configurer SSL. Mais vous pouvez également utiliser d’autres méthodes plus appropriées à votre réseau ou à votre organisation.

>[!NOTE]
>
>Il est conseillé de terminer la procédure d’installation, de configuration et de déploiement des modules d’AEM Forms et de vérifier qu’ils s’exécutent correctement, avant de configurer SSL sur le serveur d’applications.

>[!NOTE]
>
>Lorsque vous créez des certificats de sécurité et des informations d’identification SSL, utilisez les mêmes droits d’accès utilisateur que ceux du serveur d’applications. Si ce dernier utilise d’autres droits d’accès, le rendu du formulaire au format PDFForm peut ne pas être correct lorsque ContentRootURI pointe vers une adresse https.

Si vous disposez d’un serveur LDAP compatible SSL, configurez la gestion des utilisateurs et utilisatrices pour fonctionner avec celui-ci. (Voir [Configuration de la gestion des utilisateurs et utilisatrices pour un serveur LDAP compatible SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
