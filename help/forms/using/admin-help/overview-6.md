---
title: Présentation de la configuration SSL
seo-title: Présentation de la configuration SSL
description: Découvrez comment améliorer la sécurité de la communication lors de la configuration de SSL.
seo-description: Découvrez comment améliorer la sécurité de la communication lors de la configuration de SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 100%

---

# Présentation de la configuration SSL {#overview-of-configuring-ssl}

Vous pouvez créer des informations d’identification et configurer SSL (Secure Socket Layer) sur le serveur d’applications afin de mieux sécuriser la communication avec votre serveur d’applications.

En tant que solution de sécurité, Rights Management requiert la configuration de SSL. Lorsque vous configurez des certificats SSL, veillez à n’utiliser que des clés RSA. Les certificats SSL avec clés DSA ne sont pas pris en charge.

Les informations fournies s’appliquent aux procédures d’installation clé en main, automatique et manuelle. Elles décrivent une méthode parmi d’autres, permettant de configurer SSL. Mais vous pouvez également utiliser d’autres méthodes plus appropriées à votre réseau ou à votre organisation.

>[!NOTE]
>
>Il est conseillé de terminer la procédure d’installation, de configuration et de déploiement des modules d’AEM Forms et de vérifier qu’ils s’exécutent correctement, avant de configurer SSL sur le serveur d’applications.

>[!NOTE]
>
>lorsque vous créez des certificats de sécurité et des informations d’identification SSL, utilisez les mêmes droits d’accès utilisateur que ceux du serveur d’applications. Si ce dernier utilise d’autres droits d’accès, le rendu du formulaire au format PDFForm peut ne pas être correct lorsque ContentRootURI pointe vers une adresse https.

Si vous disposez d’un serveur LDAP compatible SSL, configurez User Management en conséquence (voir [Configuration de User Management pour un serveur LDAP compatible SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)).
