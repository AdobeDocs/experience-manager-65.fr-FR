---
title: Configuration de la solution Correspondence Management
seo-title: Configuration de la solution Correspondence Management
description: Configuration de la solution Correspondence Management
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 78%

---


# Configuration de la solution Correspondence Management {#configuring-a-correspondence-management-solution}

## Définition de l’URL de l’instance d’auteur pour VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Procédez aux étapes suivantes pour définir une URL d’instance d’auteur pour la restauration de la version de l’instance d’auteur :

1. Go to *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez l’icône **[!UICONTROL Modifier]** située en regard du paramètre **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** et cliquez dessus.
1. In the **[!UICONTROL VersionRestoreManager Author URL]** field, specify the URL of Author instance of VersionRestoreManager.

   **Chaîne** d’URL :

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >If there are multiple author instances (Clustered) fronted by a Load Balancer, specify the URL to the load balancer in the **[!UICONTROL VersionRestoreManager Author URL]** field.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Définition de l’URL de l’instance de publication pour ActivationManagerImpl (gestionnaire d’activation de l’instance de publication) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Suivez ces étapes pour définir l’URL de l’instance de publication pour le gestionnaire d’activation de l’instance de publication :

1. Go to *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Connectez-vous avec les informations d’identification d’utilisateur de la console de gestion OSGi. Les informations d’identification d’administrateur par défaut sont/admin.
1. Recherchez l’icône **[!UICONTROL Éditer]** située en regard du paramètre **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** et cliquez dessus.
1. Dans le champ **[!UICONTROL ActivationManager Publish URL]** (URL de publication ActivationManager), spécifiez l’URL pour accéder à l’instance de publication ActivationManager. Vous pouvez fournir les URL suivantes.

   * **URL d’équilibreur de charge (recommandée)** : saisissez l’URL de l’équilibreur de charge, si vous avez un serveur Web agissant en tant qu’équilibreur de charge devant la batterie de publication (plusieurs instances de publication non clusterisées).
   * **URL d’instance de publication** : saisissez toute URL d’instance de publication, si vous avez une instance de publication unique ou si le serveur Web donnant la batterie de publication n’est pas accessible à partir de l’environnement d’auteur en raison de restrictions. Dans le cas où l’instance de publication indiquée n’est pas disponible, un mécanisme de secours est disponible pour traiter le côté auteur.
   * **Chaîne** d’URL :

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Cliquez sur **[!UICONTROL Save]**.

Pour en savoir plus sur la configuration de Correspondence Management, consultez [Propriétés de configuration de Correspondence Management](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
