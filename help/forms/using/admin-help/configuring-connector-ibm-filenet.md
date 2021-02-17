---
title: Configuration de Connector for IBM FileNet
seo-title: Configuration de Connector for IBM FileNet
description: Découvrez comment configurer le connecteur pour IBM FileNet pour permettre la communication entre AEM forms et IBM FileNet.
seo-description: Découvrez comment configurer le connecteur pour IBM FileNet pour permettre la communication entre AEM forms et IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 94%

---


# Configuration de Connector for IBM FileNet {#configuring-connector-for-ibm-filenet}

Le connecteur pour IBM FileNet permet la communication entre AEM forms et IBM FileNet. Pour plus d’informations, voir Connectors for ECM, dans le [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Dans les versions précédentes, il était possible de stocker des actifs dans un référentiel ECM. Dans cette version, les actifs sont stockés dans le référentiel natif d’AEM forms et les services du fournisseur de référentiel sont ignorés. La migration d’actifs d’un référentiel ECM vers le référentiel AEM forms s’effectue lors de la mise à niveau vers AEM forms. Pour plus d’informations, consultez le guide de mise à niveau d’AEM forms correspondant à votre serveur d’applications.

## Configuration de la connexion à Content Engine {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine fournit des services logiciels permettant de gérer le contenu d’entreprise et les objets commerciaux définis par les clients dans les référentiels de contenu FileNet.

1. Dans Administration Console, sélectionnez Services > Connecteur pour IBM FileNet.
1. Dans le champ URL Content Engine, saisissez l’URL de connexion complète. Par exemple :

   Si vous utilisez FileNet Content Engine 4.x avec le transport CEWS, saisissez :

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Si vous utilisez FileNet Content Engine 4.x avec le transport EJB, qui est pris en charge sur WebLogic, saisissez :

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Dans la liste Dispositif de protection des informations d’identification, sélectionnez l’un de ces niveaux de protection :

   * **Clair :** envoie les informations d’identification sur le réseau en mode non protégé
   * **Symétrique :** envoie les informations d’identification chiffrées sur le réseau

1. Dans la zone Emplacement du fichier de chiffrement, entrez le chemin du fichier de chiffrement :

   * Si vous avez sélectionné Clair comme dispositif de protection des informations d’identification, ce mot-clé et sa valeur sont ignorés.
   * Si vous avez sélectionné le dispositif de protection des informations d’identification Symétrique, le chemin que vous entrez pointe vers l’emplacement d’un fichier de chiffrement sur le serveur Forms qui contient les clés de cryptage à utiliser.

1. Dans le champ Banque d’objets par défaut, entrez le connecteur de banque d’objets auquel AEM forms se connecte par défaut.
1. Dans le champ Nom d’utilisateur, saisissez le nom d’un utilisateur possédant les droits d’accès à la banque d’objets par défaut spécifiée à l’étape précédente.
1. Dans le champ Mot de passe, saisissez le mot de passe de l’utilisateur et cliquez sur Enregistrer.

## Configuration des paramètres de Process Engine  {#configure-the-process-engine-settings}

Connector for IBM FileNet contient le service Process Engine Connector for IBM FileNet, qui permet d’interagir avec IBM FileNet Process Engine. Vous pouvez configurer les paramètres de ce service.

1. Dans Administration Console, sélectionnez Services > Connector for IBM FileNet.
1. Pour activer l’utilisation du service Process Engine Connector pour IBM FileNet, sélectionnez Utiliser le service de Process Engine Connector.
1. Dans le champ Routeur de processus/Point de connexion, saisissez le nom d’hôte ou l’adresse IP et le numéro de port suivi du nom du routeur de processus. Par exemple :

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Dans le champ Nom d’utilisateur, saisissez le nom d’utilisateur utilisé pour établir la connexion au moteur de processus.
1. Dans le champ Mot de passe, saisissez le mot de passe utilisé pour établir la connexion au moteur de processus et cliquez sur Enregistrer.

## Validation des paramètres d’un service  {#validation-of-service-settings}

Si vous saisissez un nom d’utilisateur ou un mot de passe incorrect lors de la configuration de la connexion à Content Engine ou des paramètres de Process Engine, vous obtiendrez les résultats suivants selon que les services sont en cours d’exécution ou non :

* Si les services Repository Provider pour IBM FileNet et Content Repository Connector for IBM FileNet sont arrêtés, aucune erreur n’apparaît lorsque vous enregistrez les informations de configuration du service. Toutefois, lors du prochain démarrage du service, une exception sera générée et le service ne démarrera pas.
* Si ni le service Repository Provider pour IBM FileNet ni le service Content Repository Connector for IBM FileNet ne sont démarrés, le service tente de valider immédiatement les informations d’identification lorsque vous enregistrez les informations de configuration du service. Dans ce cas, une erreur se produit et les informations de configuration ne sont pas enregistrées.

## Modification du fournisseur de services de référentiel  {#change-the-repository-service-provider}

Vous pouvez configurer le fournisseur de services de référentiel à utiliser avec FileNet. Les appels des services de référentiel sont délégués au fournisseur que vous configurez.

Les options suivantes sont disponibles :

**Nom du fournisseur de référentiel actuel :** nom du prestataire de référentiel actuel

**Fournisseur du référentiel IBM FileNet :** fait du fournisseur du référentiel FileNet le fournisseur du référentiel pour le référentiel. Cette option est obsolète.

**fournisseur de référentiel :** fait du fournisseur de référentiel natif le fournisseur de référentiel pour le référentiel

>[!NOTE]
>
>pour sélectionner un fournisseur de services de référentiel qui n’est pas répertorié, configurez RepositoryService dans le composant Applications et services <!-- Fix broken link(See Managing Services) -->

1. Dans Administration Console, sélectionnez Services > Connecteur pour IBM FileNet.
1. Dans la zone Informations sur les fournisseurs de services de référentiel, sélectionnez un autre fournisseur de services de référentiel, puis cliquez sur Enregistrer.
