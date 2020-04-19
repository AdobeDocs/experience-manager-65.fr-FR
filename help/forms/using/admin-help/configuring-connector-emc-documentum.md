---
title: Configuration de Connector for EMC Documentum
seo-title: Configuration de Connector for EMC Documentum
description: Découvrez comment configurer le connecteur pour EMC Documentum pour permettre la communication entre AEM Forms et EMC Documentum.
seo-description: Découvrez comment configurer le connecteur pour EMC Documentum pour permettre la communication entre AEM Forms et EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Configuration de Connector for EMC Documentum {#configuring-connector-for-emc-documentum}

Le connecteur pour EMC Documentum permet la communication entre AEM forms et EMC Documentum. Pour plus d’informations, voir Connectors for ECM, dans le [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_63).

La configuration de Connector for EMC Documentum requiert de configurer la connexion du serveur et les informations d’identification du référentiel.

>[!NOTE]
>
>Dans les versions précédentes, il était possible de stocker des actifs dans un référentiel ECM. Dans la version actuelle, les actifs sont stockés dans le référentiel natif d’AEM forms et les services du fournisseur de référentiel sont ignorés. La migration d’actifs d’un référentiel ECM vers le référentiel AEM forms s’effectue lors de la mise à niveau vers AEM forms. Pour plus d’informations, consultez le guide de mise à niveau d’AEM forms correspondant à votre serveur d’applications.

## Configuration de la connexion au serveur {#configuring-the-server-connection}

Cette rubrique décrit les tâches de Connector for EMC Documentum que vous pouvez effectuer à partir de la page Paramètres de configuration.

>[!NOTE]
>
>Si vous configurez tous les paramètres simultanément, vous ne devez cliquer sur Enregistrer qu’une seule fois.

### Configuration du serveur {#configure-the-server}

Vous devez configurer les informations du serveur courtier de connexions. Ces informations sont nécessaires pour établir une connexion avec les référentiels de contenu Documentum et lancer le composant Connector for EMC Documentum.

1. Dans Administration Console, cliquez sur Services > Connecteur pour EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations de configuration de Documentum, entrez le nom d’hôte ou l’adresse IP ainsi que le numéro de port du courtier de connexions. Il doit s’agir d’un nombre entier positif (par exemple 1489).
1. Cliquez sur Enregistrer.

### Configuration des informations d’identification principales {#configure-principal-credentials}

Lors de la configuration des informations d’identification principales, le nom du référentiel que vous indiquez dépend du nom de référentiel explicite fourni lors de la connexion.

Si vous saisissez un nom d’utilisateur ou un mot de passe incorrect, vous obtiendrez les résultats suivants selon que le service est en cours d’exécution ou non :

* Si les services Repository Provider pour EMC Documentum et Content Repository Connector pour EMC Documentum sont arrêtés, aucune erreur n’apparaît lorsque vous enregistrez les informations de configuration du service. Toutefois, lors du prochain démarrage du service, une exception sera générée et le service ne démarrera pas.
* Si le service Repository Provider pour EMC Documentum ou Content Repository Connector pour EMC Documentum est démarré, le service tente de valider immédiatement les informations d’identification lorsque vous enregistrez les informations de configuration du service. Dans ce cas, une erreur se produit et les informations de configuration ne sont pas enregistrées.

1. Dans Administration Console, cliquez sur Services > Connecteur pour EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations d’identification principales de Documentum, saisissez le nom d’utilisateur et le mot de passe d’un utilisateur disposant de droits de super administrateur.
1. Si aucun nom de référentiel explicite n’est fourni lors de la connexion, entrez le nom du référentiel auquel les informations d’identification sont associées.
1. Cliquez sur Enregistrer.

### Modification du fournisseur de services de référentiel {#change-the-repository-service-provider}

Vous pouvez configurer le fournisseur de services de référentiel à utiliser avec Documentum. Les appels des services de référentiel sont délégués au fournisseur que vous configurez. Les options suivantes sont disponibles :

**Nom du du référentiel actuel :** Nom du de référentiel actuel

**Fournisseur de référentiel ECM Documentum :** Fait du fournisseur de référentiel Documentum le fournisseur du référentiel pour le référentiel. Cette option est obsolète.

**fournisseur de référentiel :** Fait du fournisseur de référentiel natif le fournisseur du référentiel

>[!NOTE]
>
>To select a repository service provider other than those listed, configure RepositoryService in Applications and Services > Service Management. <!-- Fix broken link (See Managing Services) -->.

1. Dans Administration Console, cliquez sur Services > Connecteur pour EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations sur les fournisseurs de services de référentiel, sélectionnez un autre fournisseur de services de référentiel.
1. Cliquez sur Enregistrer.

## Configuration des informations d’identification du référentiel {#configuring-repository-credentials}

Les informations d’identification de Documentum sont utilisées dans le contexte du système AEM forms. Les informations d’identification de référentiel sont propres aux référentiels particuliers de Documentum. Vous pouvez fournir des informations d’identification pour un nombre quelconque de référentiels, mais vous ne pouvez en spécifier qu’un ensemble par référentiel.

### Ajout d’informations d’identification de référentiel {#add-a-repository-credential}

1. Dans Administration Console, cliquez sur Services > Connector for EMC Documentum > Paramètres d’identification du référentiel.
1. Cliquez sur Ajouter. La page Informations d’identification du système Documentum s’affiche.
1. Entrez le nom du référentiel.
1. Entrez un nom d’utilisateur et un mot de passe.
1. Cliquez sur Enregistrer.

Si les services Content Repository Connector for EMC Documentum et/ou Repository for EMC Documentum sont en cours d’exécution, les informations d’identification sont vérifiées par rapport au référentiel spécifié avant d’être stockées dans la base de données. Si elles sont incorrectes ou existent déjà, un message d’erreur s’affiche.

### Suppression d’informations d’identification de référentiel {#remove-a-repository-credential}

1. Dans Administration Console, cliquez sur Services > Connecteur pour EMC Documentum > Paramètres de configuration.
1. Cochez la case en regard du référentiel pour lequel supprimer les informations d’identification et cliquez sur Supprimer. Les informations d’identification du référentiel sélectionné sont supprimées de la base de données.

### Modification du nom d’utilisateur et du mot de passe des informations d’identification de référentiel {#change-the-user-name-and-password-for-a-repository-credential}

1. Dans Administration Console, cliquez sur Services > Connecteur pour EMC Documentum > Paramètres de configuration.
1. Cliquez sur le nom du référentiel pour lequel modifier les informations d’identification.
1. Changez le nom d’utilisateur ou le mot de passe du référentiel ou bien ces deux éléments. (le nom du référentiel est en lecture seule).
1. Cliquez sur Enregistrer.

Si les services Content Repository Connector for EMC Documentum et/ou Repository for EMC Documentum sont en cours d’exécution, les informations d’identification sont vérifiées par rapport au référentiel spécifié avant d’être stockées dans la base de données. Si elles sont incorrectes ou existent déjà, un message d’erreur s’affiche.

## Activation de la demande pour le partage des files d’attente de Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Certaines tâches manuelles sont requises pour vérifier que la fonction de demande de partage d’une file d’attente de tâches dans Workspace fonctionne correctement avec Connector for EMC Documentum.

1. Une fois AEM forms déployé et Workbench installé, connectez-vous à Workbench et ouvrez l’affichage Ressources. Celui-ci vous permet de localiser le fichier QueueSharing.swf.
1. Faites glisser le fichier QueueSharing.swf de l’affichage Ressources vers le bureau de Windows ou un emplacement équivalent dans votre système d’exploitation.
1. Dans Administration Console, cliquez sur Services > Connecteur pour EMC Documentum > Paramètres de configuration.
1. Sous Informations du fournisseur de service de référentiel, remplacez le fournisseur de référentiel configuré par Fournisseur du référentiel EMC Documentum.
1. Démarrez Workbench et copiez le fichier QueueSharing.swf à l’emplacement où vous l’aviez copié la première fois (par exemple, le bureau de Windows ou un autre emplacement) dans un répertoire existant du référentiel EMC Documentum.
1. Dans l’affichage Processus de Workbench, ouvrez le processus Partage des files d’attente.
1. Dans l’affichage Variables, ouvrez les propriétés de la variable « theForm » et spécifiez dans l’URI le répertoire où vous avez placé le fichier QueueSharing.swf à l’étape 5.
1. Enregistrez le processus.
1. Migrez le processus vers l’environnement de production, conformément à la stratégie de votre entreprise.

