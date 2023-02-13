---
title: Configuration de la solution Correspondence Management
seo-title: Configuring a Correspondence Management solution
description: Configuration de la solution Correspondence Management
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '291'
ht-degree: 100%

---

# Configuration de la solution Correspondence Management {#configuring-a-correspondence-management-solution}

## Définition de l’URL de l’instance d’auteur pour VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Procédez aux étapes suivantes pour définir une URL d’instance d’auteur pour la restauration de la version de l’instance d’auteur :

1. Accédez à *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez l’icône **[!UICONTROL Modifier]** située en regard du paramètre **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** et cliquez dessus.
1. Dans le champ **[!UICONTROL URL d’auteur VersionRestoreManager]**, spécifiez l’URL de l’instance d’auteur VersionRestoreManager.

   **Chaîne d’URL** :

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >S’il existe plusieurs instances d’auteur (en cluster) derrière un équilibreur de charge, spécifiez l’URL de l’équilibreur de charge dans le champ **[!UICONTROL URL d’auteur VersionRestoreManager]**.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Définition de l’URL de l’instance de publication pour ActivationManagerImpl (gestionnaire d’activation de l’instance de publication) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Suivez ces étapes pour définir l’URL de l’instance de publication pour le gestionnaire d’activation de l’instance de publication :

1. Accédez à *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez l’icône **[!UICONTROL Éditer]** située en regard du paramètre **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** et cliquez dessus.
1. Dans le champ **[!UICONTROL ActivationManager Publish URL]** (URL de publication ActivationManager), spécifiez l’URL pour accéder à l’instance de publication ActivationManager. Vous pouvez fournir les URL suivantes.

   * **URL d’équilibreur de charge (recommandée)** : saisissez l’URL de l’équilibreur de charge, si vous avez un serveur Web agissant en tant qu’équilibreur de charge devant la batterie de publication (plusieurs instances de publication non clusterisées).
   * **URL d’instance de publication** : saisissez toute URL d’instance de publication, si vous avez une instance de publication unique ou si le serveur Web donnant la batterie de publication n’est pas accessible à partir de l’environnement d’auteur en raison de restrictions. Dans le cas où l’instance de publication indiquée n’est pas disponible, un mécanisme de secours est disponible pour traiter le côté auteur.
   * **Chaîne d’URL** :

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Cliquez sur **[!UICONTROL Enregistrer]**.

Pour en savoir plus sur la configuration de Correspondence Management, consultez [Propriétés de configuration de Correspondence Management](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).
