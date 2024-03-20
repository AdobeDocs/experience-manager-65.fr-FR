---
title: Configurer le connecteur pour EMC Documentum
description: Découvrez comment configurer Connector for EMC Documentum pour permettre la communication entre AEM forms et EMC Documentum.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 11%

---

# Configurer le connecteur pour EMC Documentum {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum permet la communication entre AEM forms et EMC Documentum. Pour plus d’informations, voir Connectors for ECM, dans le [Guide de référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

La configuration de Connector for EMC Documentum implique de configurer la connexion au serveur et les informations d’identification du référentiel.

>[!NOTE]
>
>Dans les versions antérieures , les ressources pouvaient être stockées dans un référentiel ECM. Dans la version actuelle, les actifs sont stockés dans le référentiel natif d’AEM forms et les services du fournisseur de référentiel sont obsolètes. La migration des actifs d’un référentiel ECM vers le référentiel AEM forms est effectuée lorsque vous effectuez une mise à niveau vers AEM forms. Pour plus d’informations, consultez le guide de mise à niveau d’AEM forms correspondant à votre serveur d’applications.

## Configuration de la connexion au serveur {#configuring-the-server-connection}

Cette rubrique décrit les tâches de Connector for EMC Documentum que vous pouvez effectuer sur la page Paramètres de configuration.

>[!NOTE]
>
>Si vous configurez tous les paramètres simultanément, il vous suffit de cliquer une seule fois sur Enregistrer.

### Configuration du serveur {#configure-the-server}

Vous devez configurer les informations du serveur du courtier de connexions. Ces informations sont nécessaires pour se connecter aux référentiels de contenu Documentum et démarrer Connector for EMC Documentum.

1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations de configuration de Documentum, saisissez le nom d’hôte ou l’adresse IP, ainsi que le numéro de port du courtier de connexions. Le numéro de port doit être un entier positif (par exemple, 1489).
1. Cliquez sur Enregistrer.

### Configuration des informations d’identification principales {#configure-principal-credentials}

Lors de la configuration des informations d’identification principales, le nom du référentiel que vous fournissez dépend de si un nom de référentiel explicite est fourni lors de la connexion.

Si vous saisissez un nom d’utilisateur ou un mot de passe incorrect, vous obtiendrez les résultats suivants, selon que le service est en cours d’exécution ou non :

* Si les services Repository Provider pour EMC Documentum et Content Repository Connector pour EMC Documentum sont arrêtés, aucune erreur n’apparaît lorsque vous enregistrez les informations de configuration du service. Cependant, la prochaine fois que vous démarrez le service, une exception est générée et le service ne démarre pas.
* Si les services Repository Provider pour EMC Documentum ou Content Repository Connector pour EMC Documentum sont démarrés, le service tente de valider immédiatement les informations d’identification lorsque vous enregistrez les informations de configuration du service. Dans ce cas, une erreur se produit et les informations de configuration ne sont pas enregistrées.

1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations d’identification principales de Documentum, saisissez le nom et le mot de passe d’un utilisateur disposant de droits de super-administrateur.
1. Si aucun nom de référentiel explicite n’est fourni lors de la connexion, saisissez le nom du référentiel auquel les informations d’identification sont associées.
1. Cliquez sur Enregistrer.

### Modification du fournisseur de services de référentiel {#change-the-repository-service-provider}

Vous pouvez configurer le fournisseur de services de référentiel à utiliser avec Documentum. Les appels du service Repository sont délégués au fournisseur que vous configurez. Les options suivantes sont disponibles :

**Nom du fournisseur de services de référentiel actuel :** nom du fournisseur de services de référentiel actuel.

**Fournisseur de référentiels Documentum ECM (Enterprise Content Management) :** établit le fournisseur de référentiels Documentum comme fournisseur du référentiel. Cette option est obsolète.

**Fournisseur de référentiels :** établit le fournisseur de référentiel natif comme fournisseur du référentiel.

>[!NOTE]
>
>Pour sélectionner un fournisseur de services de référentiel non répertorié, configurez le service RepositoryService dans Applications et Services > Gestion des services.<!-- Fix broken link (See Managing Services) -->

1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations sur le fournisseur de services de référentiel, sélectionnez un autre fournisseur de services de référentiel.
1. Cliquez sur Enregistrer.

## Configuration des informations d’identification du référentiel {#configuring-repository-credentials}

Les informations d’identification de Documentum sont utilisées dans le contexte du système d’AEM forms. Les informations d’identification du référentiel sont spécifiques à des référentiels spécifiques dans Documentum. Vous pouvez fournir des informations d’identification pour n’importe quel nombre de référentiels ; toutefois, vous ne pouvez spécifier qu’un seul jeu d’informations d’identification par référentiel.

### Ajout d’informations d’identification de référentiel {#add-a-repository-credential}

1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres des informations d’identification du référentiel.
1. Cliquez sur Ajouter. La page Informations d’identification du système Documentum s’affiche.
1. Saisissez un nom pour le référentiel.
1. Saisissez un nom d’utilisateur et un mot de passe.
1. Cliquez sur Enregistrer.

Si les services Content Repository Connector for EMC Documentum et/ou Repository for EMC Documentum sont en cours d’exécution, les informations d’identification sont vérifiées par rapport au référentiel spécifié avant d’être stockées dans la base de données. Si les informations d’identification ne sont pas valides ou existent, un message d’erreur s’affiche.

### Suppression d’informations d’identification de référentiel {#remove-a-repository-credential}

1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Cochez la case en regard du référentiel duquel vous souhaitez supprimer les informations d’identification, puis cliquez sur Supprimer. Les informations d’identification du référentiel sélectionné sont supprimées de la base de données.

### Modification du nom d’utilisateur et du mot de passe des informations d’identification du référentiel {#change-the-user-name-and-password-for-a-repository-credential}

1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Cliquez sur le nom du référentiel pour lequel modifier les informations d’identification.
1. Modifiez le nom d’utilisateur ou le mot de passe du référentiel, ou les deux. (Le nom du référentiel est en lecture seule.)
1. Cliquez sur Enregistrer.

Si les services Content Repository Connector for EMC Documentum et/ou Repository for EMC Documentum sont en cours d’exécution, les informations d’identification sont vérifiées par rapport au référentiel spécifié avant d’être stockées dans la base de données. Si les informations d’identification ne sont pas valides ou existent, un message d’erreur s’affiche.

## Activation de la demande de partage des files d’attente de Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Certaines étapes manuelles sont requises pour s’assurer que la fonction de demande de partage de file d’attente de tâche dans Workspace fonctionne correctement avec Connector for EMC Documentum.

1. Une fois AEM forms déployé et Workbench installé, connectez-vous à Workbench et ouvrez la vue Resources. Vous allez déterminer l’emplacement du fichier QueueSharing.swf à partir de cette vue.
1. Faites glisser le fichier QueueSharing.swf de la vue Resources vers le bureau Windows ou un emplacement équivalent, en fonction de votre système d’exploitation.
1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Sous Informations du fournisseur de services de référentiel, remplacez le fournisseur de référentiel configuré par Fournisseur du référentiel EMC Documentum.
1. Démarrez Workbench et copiez le fichier QueueSharing.swf à l’emplacement où vous l’avez initialement copié (par exemple, le bureau Windows ou un autre emplacement) dans un répertoire existant dans le référentiel EMC Documentum.
1. Dans la vue Workbench Processes, ouvrez le processus Queue Sharing.
1. Dans la vue Variables, ouvrez les propriétés de la variable &quot;theForm&quot; et modifiez l’URI pour qu’il corresponde au chemin d’accès où vous avez placé le fichier QueueSharing.swf à l’étape 5.
1. Enregistrez le processus.
1. Migrez le processus vers l’environnement de production conformément à la politique de votre entreprise.
