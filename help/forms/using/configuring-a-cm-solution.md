---
title: Configuration de la solution Correspondence Management
description: Découvrez comment configurer une solution Correspondence Management dans un environnement AEM Forms.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 38%

---

# Configuration de la solution Correspondence Management {#configuring-a-correspondence-management-solution}

## Définition de l’URL de l’instance d’auteur pour VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Suivez les étapes ci-dessous pour définir une URL d’instance de création pour la restauration de version de l’instance de création :

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

Pour définir l’URL de l’instance de publication pour le gestionnaire d’activation de l’instance publique, procédez comme suit :

1. Accédez à *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez et cliquez sur le bouton **[!UICONTROL Modifier]** en regard de l’icône **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** .
1. Dans le **[!UICONTROL URL de publication ActivationManager]** , spécifiez l’URL d’accès à l’instance de publication ActivationManager. Vous pouvez fournir les URL suivantes.

   * **URL de l’équilibreur de charge (recommandée)**: fournissez l’URL de l’équilibreur de charge, si un serveur web agit comme équilibreur de charge devant la batterie de publication (plusieurs instances de publication non clusterisées).
   * **URL de l’instance de publication**: indiquez une URL d’instance de publication. Si vous disposez d’une instance de publication unique ou si le serveur web qui précède la ferme de publication n’est pas accessible à partir de l’environnement de création en raison de restrictions. Si l’instance de publication spécifiée est en panne, un mécanisme de secours est disponible du côté auteur.
   * **Chaîne d’URL** :

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Cliquez sur **[!UICONTROL Enregistrer]**.

Pour plus d’informations sur la configuration de Correspondence Management, voir [Propriétés de configuration de Correspondence Management](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).
