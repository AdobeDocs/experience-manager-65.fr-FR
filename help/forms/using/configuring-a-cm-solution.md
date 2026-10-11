---
title: Configuration de la solution Correspondence Management
description: Découvrez comment configurer une solution Correspondence Management dans un environnement AEM Forms.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 100%
---
# Configuration de la solution Correspondence Management {#configuring-a-correspondence-management-solution}

## Définition de l’URL de l’instance de création pour VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Procédez aux étapes suivantes pour définir une URL d’instance de création pour la restauration de la version de l’instance de création :

1. Accédez à *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez l’icône **[!UICONTROL Modifier]** située en regard du paramètre **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** et cliquez dessus.
1. Dans le champ **[!UICONTROL URL de création VersionRestoreManager]**, spécifiez l’URL de l’instance de création VersionRestoreManager.

   **Chaîne d’URL** :

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >S’il existe plusieurs instances de création (en cluster) derrière un équilibreur de charge, spécifiez l’URL de l’équilibreur de charge dans le champ **[!UICONTROL URL de création VersionRestoreManager]**.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Définition de l’URL de l’instance de publication pour ActivationManagerImpl (gestionnaire d’activation de l’instance publique) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Suivez ces étapes pour pouvoir définir l’URL de l’instance de publication pour le gestionnaire d’activation de l’instance de publication :

1. Accédez à *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez l’icône **[!UICONTROL Modifier]** située en regard du paramètre **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** et cliquez dessus.
1. Dans l’**[!UICONTROL URL de publication ActivationManager]**, spécifiez l’URL d’accès à l’instance de publication ActivationManager. Vous pouvez fournir les URL ci-après.

   * **URL d’équilibreur de charge (recommandée)** : saisissez l’URL de l’équilibreur de charge, si vous avez un serveur web agissant en tant qu’équilibreur de charge devant la batterie de publication (plusieurs instances de publication non clusterisées).
   * **URL d’instance de publication** : saisissez toute URL d’instance de publication, si vous avez une instance de publication unique ou si le serveur web donnant la batterie de publication n’est pas accessible à partir de l’environnement de création en raison de restrictions. Dans le cas où l’instance de publication indiquée n’est pas disponible, un mécanisme de secours est disponible pour traiter le côté création.
   * **Chaîne d’URL** :

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Cliquez sur **[!UICONTROL Enregistrer]**.

Pour en savoir plus sur la configuration de Correspondence Management, consultez [Propriétés de configuration de Correspondence Management](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).
