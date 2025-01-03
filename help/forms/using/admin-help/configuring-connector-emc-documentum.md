---
title: Configurer le connecteur pour EMC Documentum
description: Découvrez comment configurer Connector for EMC Documentum pour permettre la communication entre AEM Forms et EMC Documentum.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 100%

---

# Configurer le connecteur pour EMC Documentum {#configuring-connector-for-emc-documentum}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Connector for EMC Documentum permet la communication entre AEM Forms et EMC Documentum. Pour plus d’informations, voir Connecteurs pour ECM, dans le [Guide de référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

La configuration de Connector for EMC Documentum implique de configurer la connexion au serveur et les informations d’identification du référentiel.

>[!NOTE]
>
>Dans les versions antérieures, les ressources pouvaient être stockées dans un référentiel ECM. Dans la version actuelle, les ressources sont stockées dans le référentiel natif AEM Forms et les services du fournisseur de référentiel sont obsolètes. La migration des ressources d’un référentiel ECM vers le référentiel AEM Forms est effectuée lorsque vous exécutez une mise à niveau vers AEM Forms. Pour plus d’informations, consultez le guide de mise à niveau d’AEM Forms correspondant à votre serveur d’applications.

## Configuration de la connexion au serveur {#configuring-the-server-connection}

Cette rubrique décrit les tâches de Connector for EMC Documentum que vous pouvez effectuer sur la page Paramètres de configuration.

>[!NOTE]
>
>Si vous configurez tous les paramètres simultanément, vous ne devez cliquer sur Enregistrer qu’une seule fois.

### Configuration du serveur {#configure-the-server}

Vous devez configurer les informations du serveur du répartiteur de connexions. Ces informations sont nécessaires pour établir une connexion avec les référentiels de contenu Documentum et lancer le composant Connector for EMC Documentum.

1. Dans la console d’administration, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations de configuration de Documentum, saisissez le nom d’hôte ou l’adresse IP, ainsi que le numéro de port du répartiteur de connexions. Le numéro de port doit être un entier positif (par exemple, 1489).
1. Cliquez sur Enregistrer.

### Configuration des informations d’identification du principal {#configure-principal-credentials}

Lors de la configuration des informations d’identification du principal, le nom du référentiel que vous fournissez dépend du nom de référentiel explicite fourni lors de la connexion.

Si vous saisissez un nom d’utilisateur ou un mot de passe incorrect, vous obtiendrez les résultats suivants, selon que le service est en cours d’exécution ou non :

* Si les services Repository Provider EMC Documentum et Content Repository Connector for EMC Documentum s’arrêtent, aucune erreur n’apparaît lorsque vous enregistrez les informations de configuration du service. Toutefois, lors du prochain démarrage du service, une exception sera déclenchée et le service ne démarrera pas.
* Si les services Repository Provider EMC Documentum et Content Repository Connector for EMC Documentum démarrent, le service tente de valider immédiatement les informations d’identification lorsque vous enregistrez les informations de configuration du service. Dans ce cas, une erreur se produit et les informations de configuration ne sont pas enregistrées.

1. Dans la console d’administration, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations d’identification du principal de Documentum, saisissez le nom et le mot de passe d’un utilisateur ou utilisatrice disposant de droits de super-administration.
1. Si aucun nom de référentiel explicite n’est fourni lors de la connexion, saisissez le nom du référentiel auquel les informations d’identification sont associées.
1. Cliquez sur Enregistrer.

### Modifier le fournisseur du service de référentiel {#change-the-repository-service-provider}

Vous pouvez configurer le fournisseur de services de référentiel à utiliser avec Documentum. Les appels du service de référentiel sont délégués au fournisseur que vous configurez. Les options suivantes sont disponibles :

**Nom du fournisseur de services de référentiel actuel :** nom du fournisseur de services de référentiel actuel.

**Fournisseur de référentiels Documentum ECM (Enterprise Content Management) :** établit le fournisseur de référentiels Documentum comme fournisseur du référentiel. Cette option est obsolète.

**Fournisseur de référentiels :** établit le fournisseur de référentiel natif comme fournisseur du référentiel.

>[!NOTE]
>
>Pour sélectionner un fournisseur de services de référentiel non répertorié, configurez le service RepositoryService dans Applications et Services > Gestion des services.<!-- Fix broken link (See Managing Services) -->

1. Dans la console d’administration, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Dans la zone Informations sur le fournisseur de services de référentiel, sélectionnez un autre fournisseur de services de référentiel.
1. Cliquez sur Enregistrer.

## Configuration des informations d’identification du référentiel {#configuring-repository-credentials}

Les informations d’identification de Documentum sont utilisées dans le contexte du système AEM Forms. Les informations d’identification de référentiel sont spécifiques à des référentiels spécifiques dans Documentum. Vous pouvez fournir des informations d’identification pour n’importe quel nombre de référentiels ; toutefois, vous ne pouvez spécifier qu’un seul jeu par référentiel.

### Ajout d’informations d’identification de référentiel {#add-a-repository-credential}

1. Dans la console d’administration, cliquez sur Services > Connector for EMC Documentum > Paramètres des informations d’identification du référentiel.
1. Cliquez sur Ajouter. La page Informations d’identification du système Documentum s’affiche.
1. Saisissez le nom du référentiel.
1. Saisissez un nom d’utilisateur et un mot de passe.
1. Cliquez sur Enregistrer.

Si les services Content Repository Connector for EMC Documentum et/ou Repository for EMC Documentum sont en cours d’exécution, les informations d’identification sont vérifiées par rapport au référentiel spécifié avant d’être stockées dans la base de données. Si les informations d’identification ne sont pas correctes ou existent déjà, un message d’erreur s’affiche.

### Suppression des informations d’identification de référentiel {#remove-a-repository-credential}

1. Dans la console d’administration, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Cochez la case en regard du référentiel pour lequel supprimer les informations d’identification et cliquez sur Supprimer. Les informations d’identification du référentiel sélectionné sont supprimées de la base de données.

### Modification du nom d’utilisateur et du mot de passe des informations d’identification de référentiel {#change-the-user-name-and-password-for-a-repository-credential}

1. Dans la console d’administration, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Cliquez sur le nom du référentiel pour lequel modifier les informations d’identification.
1. Modifiez le nom d’utilisateur ou le mot de passe du référentiel ou bien ces deux éléments. (Le nom du référentiel est en lecture seule).
1. Cliquez sur Enregistrer.

Si les services Content Repository Connector for EMC Documentum et/ou Repository for EMC Documentum sont en cours d’exécution, les informations d’identification sont vérifiées par rapport au référentiel spécifié avant d’être stockées dans la base de données. Si les informations d’identification ne sont pas correctes ou existent déjà, un message d’erreur s’affiche.

## Activation de la demande de partage de files d’attente de Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Certaines tâches manuelles sont requises pour vérifier que la fonction de demande de partage d’une file d’attente de tâches dans Workspace fonctionne correctement avec Connector for EMC Documentum.

1. Une fois AEM Forms déployé et Workbench installé, connectez-vous à Workbench et ouvrez l’affichage Ressources. Celui-ci vous permet de localiser le fichier QueueSharing.swf.
1. Faites glisser le fichier QueueSharing.swf de l’affichage Ressources vers le bureau de Windows ou un emplacement équivalent dans votre système d’exploitation.
1. Dans la console d’administration, cliquez sur Services > Connector for EMC Documentum > Paramètres de configuration.
1. Sous Informations du fournisseur de services de référentiel, remplacez le fournisseur de référentiels configuré par Fournisseur de référentiels EMC Documentum.
1. Démarrez Workbench et copiez le fichier QueueSharing.swf à l’emplacement où vous l’avez copié la première fois (par exemple, le bureau Windows ou un autre emplacement) dans un répertoire existant du référentiel EMC Documentum.
1. Dans l’affichage Processus de Workbench, ouvrez le processus Partage des files d’attente.
1. Dans la vue Variables, ouvrez les propriétés de la variable « theForm » et modifiez l’URI pour qu’il corresponde au chemin où vous avez placé le fichier QueueSharing.swf à l’étape 5.
1. Enregistrez le processus.
1. Migrez le processus vers l’environnement de production conformément à la politique de votre entreprise.
