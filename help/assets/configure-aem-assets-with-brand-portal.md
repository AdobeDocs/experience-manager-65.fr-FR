---
title: Configuration d’AEM Assets avec Brand Portal
seo-title: Configuration d’AEM Assets avec Brand Portal
description: Découvrez comment configurer AEM Assets avec Brand Portal pour publier des ressources et des collections sur Brand Portal.
seo-description: Découvrez comment configurer AEM Assets avec Brand Portal pour publier des ressources et des collections sur Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: fb59bd52be86894e93063f4b7c32aef0ed23250b
workflow-type: tm+mt
source-wordcount: '1748'
ht-degree: 60%

---


# Configuration d’AEM Assets avec Brand Portal {#configure-integration-65}

Adobe Experience Manager (AEM) Assets est configuré avec Brand Portal via Adobe I/O, qui fournit un jeton IMS pour autoriser votre client Brand Portal.

>[!NOTE]
>
>La configuration d’AEM Assets avec Brand Portal via Adobe I/O est prise en charge sur AEM 6.5.4.0 et versions ultérieures.
>
>Auparavant, Brand Portal était configuré dans l’interface utilisateur classique via la passerelle OAuth héritée, qui fait appel à l’échange de jetons JWT pour obtenir un jeton d’accès IMS en vue de l’autorisation.
>
>La configuration via application OAuth héritée n’est plus prise en charge à partir du 6 avril 2020 et est remplacée par la configuration via Adobe I/O.


>[!TIP]
>
>***Pour les clients existants uniquement***
>
>Il est recommandé de continuer à utiliser la configuration de la passerelle OAuth héritée. Si vous rencontrez des problèmes avec la configuration héritée de la passerelle OAuth, supprimez la configuration existante et créez une configuration via Adobe I/O.



Cette aide décrit les deux cas d’utilisation suivants :
* [Nouvelle configuration](#configure-new-integration-65): Si vous êtes un nouvel utilisateur du portail de marques et souhaitez configurer votre instance d’auteur AEM Assets avec Brand Portal, vous pouvez créer une nouvelle configuration sur les E/S Adobe.
* [Configuration](#upgrade-integration-65)de la mise à niveau : Si vous êtes un utilisateur du portail de marque existant dont l’instance d’auteur AEM Assets est configurée avec Brand Portal sur la passerelle OAuth héritée, il est recommandé de supprimer les configurations existantes et de créer une nouvelle configuration sur les E/S Adobe.

Cette aide s’adresse à un public familiarisé avec les technologies suivantes :

* Installation, configuration et administration des packs Adobe Experience Manager et AEM

* Utilisation des systèmes d’exploitation Linux et Microsoft Windows

## Conditions préalables {#prerequisites}

Pour configurer AEM Assets avec Brand Portal, vous devez disposer des éléments suivants :

* Une instance d’auteur AEM Assets en cours d’exécution avec le dernier Service Pack
* URL du client Brand Portal
* Un utilisateur disposant de droits d’administrateur système sur l’organisation IMS du client Brand Portal


[Téléchargement et installation d’AEM 6.5](#aemquickstart)

[Télécharger et installer le dernier Service Pack AEM](#servicepack)

### Téléchargement et installation d’AEM 6.5 {#aemquickstart}

Il est recommandé d’utiliser AEM 6.5 pour configurer une instance d’auteur AEM. Si vous ne l’avez pas, téléchargez-le à partir des emplacements suivants :

* If you are an existing AEM customer, download AEM 6.5 from [Adobe Licensing website](http://licensing.adobe.com).

* If you are an Adobe partner, use [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) to request AEM 6.5.

Après avoir téléchargé AEM, consultez la page [Déploiement et maintenance](https://helpx.adobe.com/fr/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall) pour obtenir des instructions sur la configuration d’une instance d’auteur AEM.

### Télécharger et installer le dernier Service Pack AEM {#servicepack}

Pour obtenir des instructions détaillées, voir

* [Notes de mise à jour d’AEM 6.5, Pack de services ](https://helpx.adobe.com/fr/experience-manager/6-5/release-notes/sp-release-notes.html)

**Contactez le service à la clientèle** si vous ne parvenez pas à trouver le dernier package ou Service Pack d’AEM.

## Création d’une configuration {#configure-new-integration-65}

Effectuez les étapes suivantes dans la séquence répertoriée si vous configurez AEM Assets avec Brand Portal pour la première fois :
1. [Obtention d’un certificat public](#public-certificate)
1. [Création de l’intégration Adobe I/O](#createnewintegration)
1. [Création d’une configuration de compte IMS](#create-ims-account-configuration)
1. [Configuration du service cloud](#configure-the-cloud-service)
1. [Test de la configuration](#test-integration)

### Création de la configuration IMS {#create-ims-configuration}

La configuration IMS authentifie votre client Brand Portal avec l’instance d’auteur AEM Assets.

La configuration IMS comprend deux étapes :

* [Obtention d’un certificat public](#public-certificate)
* [Création d’une configuration de compte IMS](#create-ims-account-configuration)

### Obtention d’un certificat public {#public-certificate}

Un certificat public permet d’authentifier votre profil sur Adobe I/O.

1. Connexion à votre instance d’auteur AEM AssetsURL par défaut : http:// localhost:4502/aem/start.html
1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** >> **[!UICONTROL Adobe IMS Configurations]**.

   ![Interface utilisateur de configuration du compte Adobe IMS](assets/ims-config1.png)

1. La page Configurations d’Adobe IMS s’ouvre.

   Cliquez sur **[!UICONTROL Créer]**.

   This will take you to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page.

1. Par défaut, l’onglet **Certificat** s’ouvre.

   Dans **Solution cloud**, sélectionnez **[!UICONTROL Adobe Brand Portal]**.

1. Mark the checkbox **[!UICONTROL Create new certificate]** and specify an **alias** for the certificate. L’alias sert de nom à la boîte de dialogue.

1. Cliquez sur **[!UICONTROL Créer un certificat]**. Une boîte de dialogue s’affiche. Cliquez sur **[!UICONTROL OK]** pour générer le certificat public.

   ![Création d’un certificat](assets/ims-config2.png)

1. Cliquez sur **[!UICONTROL Télécharger la clé publique]** et enregistrez le fichier de certificat *AEM-Adobe-IMS.crt* sur votre ordinateur. Le fichier de certificat est utilisé pour [créer une intégration Adobe I/O](#createnewintegration).

   ![Téléchargement du certificat](assets/ims-config3.png)

1. Cliquez sur **[!UICONTROL Suivant]**.

   Dans l’onglet **Compte**, vous créez le compte Adobe IMS, mais vous avez pour cela besoin des détails d’intégration. Gardez cette page ouverte pour l’instant.

   Ouvrez un nouvel onglet et [créez une intégration Adobe I/O](#createnewintegration) pour obtenir les détails d’intégration des configurations de compte IMS.

### Création de l’intégration Adobe I/O {#createnewintegration}

L’intégration Adobe I/O génère une clé API, un secret client et une charge utile (JWT), dont vous avez besoin pour configurer les configurations de compte IMS.

1. Connectez-vous à la console Adobe I/O avec les droits d’administrateur système sur l’organisation IMS du client Brand Portal.

   URL par défaut : [https://console.adobe.io/](https://console.adobe.io/)

1. Cliquez sur **[!UICONTROL Créer une intégration]**.

1. Sélectionnez **[!UICONTROL Accéder à une API]**, puis cliquez sur **[!UICONTROL Continuer]**.

   ![Création d’une intégration](assets/create-new-integration1.png)

1. La page Créer une intégration s’affiche.

   Sélectionnez votre entreprise dans la liste déroulante.

   Dans **[!UICONTROL Experience Cloud]**, sélectionnez **[!UICONTROL AEM Brand Portal]** et cliquez sur **[!UICONTROL Continuer]**.

   Si l’option Brand Portal est désactivée, assurez-vous d’avoir sélectionné la bonne entreprise dans la liste déroulante au-dessus de l’option **[!UICONTROL Adobe Services]** (Services Adobe). Si vous ne connaissez pas le nom de votre entreprise, contactez votre administrateur.

   ![Création d’une intégration](assets/create-new-integration2.png)

1. Spécifiez le nom et la description de l’intégration. Cliquez sur **[!UICONTROL Select a File from your computer]** (Sélectionner un fichier sur votre ordinateur) et téléchargez le fichier `AEM-Adobe-IMS.crt` téléchargé dans la section [obtenir des certificats publics](#public-certificate).

1. Sélectionnez le profil de votre entreprise.

   Ou sélectionnez le profil **[!UICONTROL Assets Brand Portal]** par défaut et cliquez sur **[!UICONTROL Créer une intégration]**. L’intégration est créée.

1. Appuyez sur **[!UICONTROL Continue to integration details]** (Continuer vers les détails d’intégration) pour afficher les informations d’intégration.

   Copiez la **[!UICONTROL clé API]**.

   Cliquez sur **[!UICONTROL Retrieve Client Secret]** (Récupérer le secret client) et copiez la clé secrète client.

   ![Clé API, secret client et informations de charge utile d’une intégration](assets/create-new-integration3.png)

1. Accédez à l’onglet **[!UICONTROL JWT]** et copiez la **[!UICONTROL charge JWT]**.

   Les informations de clé API, de clé secrète client et de charge utile JWT seront utilisées pour créer la configuration du compte IMS.

### Création d’une configuration de compte IMS {#create-ims-account-configuration}

Vérifiez que vous avez effectué les étapes suivantes :

* [Obtention d’un certificat public](#public-certificate)
* [Création de l’intégration Adobe I/O](#createnewintegration)

**Procédure de création de la configuration du compte IMS :**

1. Ouvrez la page Configuration IMS de l’onglet **[!UICONTROL Comptes]**. Vous avez gardé la page ouverte à la fin de la section [Obtention d’un certificat public](#public-certificate).

1. Spécifiez un **[!UICONTROL titre]** pour le compte IMS.

   Dans **[!UICONTROL Serveur d’autorisation]**, entrez l’adresse URL : [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Collez la clé API, le secret client et la charge utile JWT que vous avez copiés à la fin de [Création de l’intégration Adobe I/O](#createnewintegration).

   Cliquez sur **[!UICONTROL Créer]**.

   L’intégration est créée.

   ![Configuration du compte IMS](assets/create-new-integration6.png)


1. Sélectionnez la configuration IMS et cliquez sur **[!UICONTROL Contrôle de l’intégrité]**. Une boîte de dialogue s’affiche.

   Cliquez sur **[!UICONTROL Vérifier]**. Une fois la connexion établie, le message *Jeton récupéré avec succès* s’affiche.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Vous ne devez avoir qu’une seule configuration IMS. N’en créez pas plusieurs.
>
>Assurez-vous que la configuration IMS réussit le contrôle d’intégrité. Si tel n’est pas le cas, elle n’est pas valide. Vous devez la supprimer et créer une configuration valide.


### Configuration du service cloud {#configure-the-cloud-service}

Pour créer une configuration de service cloud Brand Portal, procédez comme suit :

1. Connexion à votre instance d’auteur AEM Assets

   URL par défaut : http:// localhost:4502/aem/start.html
1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services >> AEM Brand Portal]**.

   La page Configurations de Brand Portal s’affiche.

1. Cliquez sur **[!UICONTROL Créer]**.

1. Saisissez un **[!UICONTROL titre]** pour la configuration.

   Sélectionnez la configuration IMS que vous avez créée à l’étape [Création d’une configuration de compte IMS](#create-ims-account-configuration).

   Dans **[!UICONTROL URL du service]**, entrez votre URL du client Brand Portal.

   ![](assets/create-cloud-service.png)

1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**. La configuration cloud est alors créée. Votre instance d’auteur AEM Assets est maintenant intégrée au client du portail de marque.

### Test de la configuration {#test-integration}

1. Connexion à votre instance d’auteur AEM Assets

   URL par défaut : http:// localhost:4502/aem/start.html

1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment >> Replication]**.

   ![](assets/test-integration1.png)

1. La page Réplication s’ouvre.

   Cliquez sur **[!UICONTROL Agents sur l’auteur]**.

   ![](assets/test-integration2.png)

1. Quatre agents de réplication sont créés pour chaque client.

   Localisez les agents de réplication de votre locataire du portail de marque.

   Cliquez sur l’URL de l’agent de réplication.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >Les agents de réplication fonctionnent en parallèle et partagent la répartition des tâches de manière égale, augmentant ainsi la vitesse de publication de quatre fois la vitesse initiale. Une fois le service cloud configuré, aucune configuration supplémentaire n’est requise pour activer les agents de réplication activés par défaut pour permettre la publication parallèle de plusieurs actifs.

   >[!NOTE]
   >
   >Évitez de désactiver tout agent de réplication, car cela peut entraîner l’échec de la réplication de certaines ressources.


1. To verify the connection between AEM Assets author and Brand Portal, click **[!UICONTROL Test Connection]**.

   ![](assets/test-integration4.png)

1. En bas des résultats du test, vérifiez que la réplication a réussi.

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >Les agents de réplication fonctionnent en parallèle et partagent la répartition des tâches de manière égale, augmentant ainsi la vitesse de publication de quatre fois la vitesse initiale. Une fois le service cloud configuré, aucune configuration supplémentaire n’est requise pour activer les agents de réplication activés par défaut pour permettre la publication parallèle de plusieurs actifs.

1. Vérifiez les résultats du test sur les quatre agents de réplication un par un.


   >[!NOTE]
   >
   >Évitez de désactiver tout agent de réplication, car cela peut entraîner l’échec de la réplication de certaines ressources.

Le portail de marque a été correctement configuré avec votre instance d’auteur AEM Assets. Vous pouvez maintenant :

* [Publication de ressources à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publication de dossiers à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publication de collections à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-collection.md)
* [Configurez l’approvisionnement](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) des ressources pour permettre aux utilisateurs du portail de marque de contribuer et de publier des ressources sur AEM Assets.

## Mise à niveau de la configuration {#upgrade-integration-65}

Effectuez les étapes suivantes dans la séquence répertoriée pour mettre à niveau les configurations existantes :
1. [Vérification des tâches en cours](#verify-jobs)
1. [Supprimer les configurations existantes](#delete-existing-configuration)
1. [Création d’une configuration](#configure-new-integration-65)

### Vérification des tâches en cours {#verify-jobs}

Assurez-vous qu’aucune tâche de publication ne s’exécute sur votre instance d’auteur AEM Assets avant d’apporter des modifications. Pour cela, vous pouvez vérifier les quatre agents de réplication et vous assurer que la file d&#39;attente est idéale/vide.

1. Connexion à votre instance d’auteur AEM Assets

   URL par défaut : http:// localhost:4502/aem/start.html

1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment >> Replication]**.

1. La page Réplication s’ouvre.

   Cliquez sur **[!UICONTROL Agents sur l’auteur]**.

   ![](assets/test-integration2.png)

1. Localisez les agents de réplication de votre locataire du portail de marque.

   Assurez-vous que la **file d&#39;attente est inactive** pour tous les agents de réplication, aucun travail de publication n&#39;est actif.

   ![](assets/test-integration3.png)

### Supprimer les configurations existantes {#delete-existing-configuration}

Vous devez exécuter la liste de vérification suivante lors de la suppression des configurations existantes.
* Supprimer les quatre agents de réplication
* Suppression du service cloud
* Supprimer un utilisateur MAC

1. Connectez-vous à votre instance d’auteur AEM Assets et ouvrez CRX Lite en tant qu’administrateur.

   URL par défaut : http:// localhost:4502/crx/de/index.jsp

1. Accédez à `/etc/replications/agents.author` et supprimez les quatre agents de réplication de votre locataire du portail de marque.

   ![](assets/delete-replication-agent.png)

1. Accédez à `/etc/cloudservices/mediaportal` la configuration **du service** Cloud et supprimez-la.

   ![](assets/delete-cloud-service.png)

1. Accédez à `/home/users/mac` l’utilisateur **** MAC de votre locataire du portail de marque et supprimez-le.

   ![](assets/delete-mac-user.png)


Vous pouvez désormais [créer une configuration](#configure-new-integration-65) sur votre instance d’auteur AEM 6.5 sur les E/S Adobe.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

Une fois la réplication réussie, vous pouvez publier des ressources, des dossiers et des collections sur Brand Portal. Pour plus d’informations, voir :

* [Publication de ressources sur Brand Portal](/help/assets/brand-portal-publish-assets.md)
* [Publication de dossiers sur Brand Portal](/help/assets/brand-portal-publish-folder.md)
* [Publication de collections sur Brand Portal](/help/assets/brand-portal-publish-collection.md)
