---
title: Présentation de la configuration SSL
description: Découvrez comment améliorer la sécurité des communications en configurant SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 14%

---

# Présentation de la configuration SSL {#overview-of-configuring-ssl}

Vous pouvez créer des informations d’identification SSL (Secure Sockets Layer) et configurer SSL sur le serveur d’applications afin d’améliorer la sécurité de la communication avec votre serveur d’applications.

En tant que produit de sécurité, Rights Management requiert la configuration de SSL. Lors de la configuration des certificats SSL, veillez à n’utiliser que des clés RSA. Les certificats SSL avec clés DSA ne sont pas pris en charge.

Les informations fournies s’appliquent aux installations clé en main, automatiques et manuelles. Il offre un exemple de méthode de configuration SSL. Vous pouvez également utiliser d’autres méthodes plus appropriées à votre réseau ou organisation.

>[!NOTE]
>
>Il est recommandé de terminer l’installation, la configuration et le déploiement de vos modules forms AEM et de vous assurer que les produits s’exécutent correctement avant de configurer SSL sur le serveur d’applications.

>[!NOTE]
>
>Lors de la création de certificats de sécurité et d’informations d’identification SSL, utilisez les mêmes privilèges de compte d’utilisateur que ceux utilisés pour exécuter le serveur d’applications. Si le serveur d’applications est exécuté à l’aide d’autres privilèges utilisateur, le rendu du formulaire pour les rendus PDFForm peut échouer lorsque ContentRootURI pointe vers https.

Si vous disposez d’un serveur LDAP compatible SSL, configurez la gestion des utilisateurs et utilisatrices pour l’utiliser. (Voir [Configuration de la gestion des utilisateurs et utilisatrices pour un serveur LDAP compatible SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
