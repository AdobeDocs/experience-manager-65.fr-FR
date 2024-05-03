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
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 100%

---

# Configuration de la solution Correspondence Management {#configuring-a-correspondence-management-solution}

## Définition de l’URL de l’instance de création pour VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Procédez aux étapes suivantes pour définir une URL d’instance de création pour la restauration de la version de l’instance de création :

1. Accédez à *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez l’icône **[!UICONTROL Modifier]** située en regard du paramètre **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** et cliquez dessus.
1. Dans le champ **[!UICONTROL URL d’auteur VersionRestoreManager]**, spécifiez l’URL de l’instance d’auteur VersionRestoreManager.

   **Chaîne d’URL** :

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >S’il existe plusieurs instances d’auteur (en cluster) derrière un équilibreur de charge, spécifiez l’URL de l’équilibreur de charge dans le champ **[!UICONTROL URL d’auteur VersionRestoreManager]**.

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
