---
title: Configuration de Connector for IBM FileNet
description: Découvrez comment configurer Connector for IBM FileNet pour activer la communication entre AEM forms et IBM FileNet.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 17%

---

# Configuration de Connector for IBM FileNet {#configuring-connector-for-ibm-filenet}

Connector for IBM FileNet permet la communication entre AEM forms et IBM FileNet. Pour plus d’informations, voir &quot;Connecteurs pour ECM&quot; dans [Référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Dans les versions antérieures, les ressources pouvaient être stockées dans un référentiel ECM. Dans cette version, les actifs sont stockés dans le référentiel natif d’AEM forms et les services du fournisseur de référentiel sont obsolètes. La migration des actifs d’un référentiel ECM vers le référentiel AEM forms est effectuée lorsque vous effectuez une mise à niveau vers AEM forms. Pour plus d’informations, consultez le guide de mise à niveau d’AEM forms correspondant à votre serveur d’applications.

## Configuration de la connexion à Content Engine {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine fournit des services logiciels pour gérer le contenu d’entreprise et les objets commerciaux définis par les clients dans les référentiels de contenu FileNet.

1. Dans Administration Console, cliquez sur Services > Connector for IBM FileNet.
1. Dans la zone URL de Content Engine, saisissez l’URL de connexion complète. Par exemple :

   Si vous utilisez FileNet Content Engine 4.x avec le transport CEWS, saisissez :

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Si vous utilisez FileNet Content Engine 4.x avec le transport EJB, qui est pris en charge sur WebLogic, saisissez :

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Dans la liste Dispositif de protection des informations d’identification, sélectionnez l’un de ces niveaux de protection :

   * **Clair :** envoie les informations d’identification sur le réseau en mode non protégé
   * **Symétrique :** envoie les informations d’identification chiffrées sur le réseau

1. Dans la zone Emplacement du fichier de chiffrement, saisissez le chemin d’accès au fichier de chiffrement :

   * Si vous avez sélectionné Effacer comme schéma de protection des informations d’identification, ce mot-clé et sa valeur sont ignorés.
   * Si vous avez sélectionné Symétrique comme schéma de protection des informations d’identification, le chemin que vous saisissez pointe vers l’emplacement d’un fichier de chiffrement sur le serveur Forms qui contient les clés de cryptage à utiliser.

1. Dans la zone Banque d’objets par défaut, saisissez le connecteur de banque d’objets auquel AEM forms se connecte par défaut.
1. Dans la zone Nom d’utilisateur , saisissez le nom d’un utilisateur disposant des droits d’accès à la banque d’objets par défaut que vous avez spécifiée à l’étape précédente.
1. Dans la zone Mot de passe, saisissez le mot de passe de l’utilisateur et cliquez sur Enregistrer.

## Configuration des paramètres du moteur de processus {#configure-the-process-engine-settings}

Connector for IBM FileNet contient le service Process Engine Connector for IBM FileNet, qui permet d’interagir avec IBM FileNet Process Engine. Vous pouvez configurer les paramètres de ce service.

1. Dans Administration Console, cliquez sur Services > Connecteur pour IBM FileNet.
1. Pour activer l’utilisation du service Process Engine Connector for IBM FileNet, sélectionnez Use Process Engine Connector Service.
1. Dans la zone Routeur de processus/Point de connexion, saisissez le nom d’hôte ou l’adresse IP et le numéro de port, suivis du nom du routeur de processus. Par exemple :

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Dans la zone User Name, saisissez le nom d’utilisateur utilisé pour se connecter au moteur de processus.
1. Dans la zone Password, saisissez le mot de passe utilisé pour se connecter au moteur de processus et cliquez sur Save.

## Validation des paramètres du service {#validation-of-service-settings}

Si vous saisissez un nom d’utilisateur ou un mot de passe incorrect lors de la configuration de la connexion à Content Engine ou des paramètres du moteur de processus, vous obtiendrez les résultats suivants, selon que les services sont en cours d’exécution ou non :

* Si les services Repository Provider pour IBM FileNet et Content Repository Connector for IBM FileNet sont arrêtés, aucune erreur n’apparaît lorsque vous enregistrez les informations de configuration du service. Cependant, la prochaine fois que vous démarrez le service, une exception est générée et le service ne démarre pas.
* Si le service Repository Provider pour IBM FileNet ou Content Repository Connector for IBM FileNet est démarré, le service tente de valider immédiatement les informations d’identification lorsque vous enregistrez les informations de configuration du service. Dans ce cas, une erreur se produit et les informations de configuration ne sont pas enregistrées.

## Modification du fournisseur de services de référentiel {#change-the-repository-service-provider}

Vous pouvez configurer le fournisseur de services de référentiel à utiliser avec FileNet. Les appels du service Repository sont délégués au fournisseur que vous configurez.

Les options suivantes sont disponibles :

**Nom du fournisseur de référentiels actuel :** le nom du fournisseur de référentiels actuel.

**Fournisseur de référentiels IBM FileNet :** fait du fournisseur de référentiels FileNet le fournisseur du référentiel. Cette option est obsolète.

**fournisseur de référentiels :** fait du fournisseur de référentiels natif le fournisseur du référentiel.

>[!NOTE]
>
>pour sélectionner un fournisseur de services de référentiel qui n’est pas répertorié, configurez RepositoryService dans le composant Applications et services <!-- Fix broken link(See Managing Services) -->

1. Dans Administration Console, cliquez sur Services > Connector for IBM FileNet.
1. Dans la zone Informations sur le fournisseur de services de référentiel, sélectionnez l’autre fournisseur de services de référentiel, puis cliquez sur Enregistrer.
