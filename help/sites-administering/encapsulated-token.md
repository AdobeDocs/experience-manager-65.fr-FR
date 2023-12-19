---
title: Prise en charge des jetons encapsulés
description: Découvrez la prise en charge des jetons encapsulés dans AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 89%

---

# Prise en charge des jetons encapsulés{#encapsulated-token-support}

## Présentation {#introduction}

Par défaut, AEM utilise le gestionnaire d’authentification des jetons pour authentifier chaque demande. Toutefois, pour répondre aux demandes d’authentification, le gestionnaire d’authentification des jetons requiert l’accès au référentiel pour chaque demande. Ceci est dû au fait que des cookies sont utilisés pour maintenir l’état d’authentification. En toute logique, l’état doit être conservé dans le référentiel pour valider les requêtes suivantes. Dans les faits, cela signifie que le mécanisme d’authentification est avec état.

Cela est particulièrement important pour l’évolutivité horizontale. Dans une configuration multi-instances comme la ferme de publication décrite ci-dessous, l’équilibrage de charge ne peut pas être réalisé de manière optimale. Avec l’authentification avec état, l’état d’authentification persistant n’est disponible que sur l’instance où la personne est authentifiée pour la première fois.

![chlimage_1-33](assets/chlimage_1-33a.png)

Prenons comme exemple le scénario suivant :

Un personne peut être authentifiée sur l’instance de publication 1, mais si une requête ultérieure est envoyée à l’instance de publication 2, cette instance ne dispose pas de cet état d’authentification persistant, car cet état a été conservé dans le référentiel de publication 1 et la publication 2 possède son propre référentiel.

La solution consiste à configurer des connexions persistantes au niveau de l’équilibreur de charge. Avec des connexions persistantes, un utilisateur serait toujours dirigé vers la même instance de publication. Par conséquent, un équilibrage de charge réellement optimal n’est pas possible.

Si une instance de publication devient inaccessible, tous les utilisateurs authentifiés sur cette instance perdent leur session, Cela est dû au fait que l’accès au référentiel est nécessaire pour valider le cookie d’authentification.

## Authentification sans état avec jeton encapsulé {#stateless-authentication-with-the-encapsulated-token}

Pour permettre une évolutivité horizontale, la solution consiste à recourir à une authentification sans état, grâce à la nouvelle prise en charge des jetons encapsulés dans AEM.

Le jeton encapsulé est un élément de chiffrement qui permet à AEM de créer et de valider de façon sécurisée des informations d’authentification hors ligne, sans accéder au référentiel. Ainsi, une demande d’authentification peut être effectuée sur toutes les instances de publication, sans nécessiter de connexions persistantes. Cela présente également l’avantage d’améliorer les performances d’authentification, car il n’est pas nécessaire d’accéder au référentiel pour chaque demande d’authentification.

Vous pouvez découvrir comment cela fonctionne dans un déploiement distribué géographiquement avec les instances de création MongoMK et de publication TarMK ci-dessous :

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>Le jeton encapsulé concerne l’authentification. Il permet de s’assurer que le cookie peut être validé sans avoir à accéder au référentiel. Cependant, il est toujours nécessaire que l’utilisateur ou l’utilisatrice existe sur toutes les instances et que les informations stockées sous cet utilisateur ou utilisatrice soient accessibles par chaque instance.
>
>Par exemple, si un nouvel utilisateur est créé sur l’instance de publication 1, en raison du fonctionnement du jeton encapsulé, il est authentifié correctement sur l’instance de publication 2. Si l’utilisateur ou l’utilisatrice n’existe pas sur la deuxième instance de publication, la requête échoue toujours.
>

## Configuration du jeton encapsulé {#configuring-the-encapsulated-token}

>[!NOTE]
>Tous les gestionnaires d’authentification qui synchronisent les utilisateurs et reposent sur l’authentification par jeton (comme SAML et OAuth) ne fonctionnent qu’avec des jetons encapsulés si :
>
>* les sessions persistantes sont activées, ou
>
>* les utilisateurs sont déjà créés dans AEM au démarrage de la synchronisation. Cela signifie que les jetons encapsulés ne seront pas pris en charge dans les cas où les gestionnaires **créent** des utilisateurs au cours du processus de synchronisation.

Lors de la configuration du jeton encapsulé, vous devez prendre en compte quelques points :

1. En raison de la cryptographie impliquée, toutes les instances doivent avoir la même clé HMAC. À compter d’AEM 6.3, le matériel de la clé n’est plus stocké dans le référentiel, mais sur le système de fichiers réel. Ainsi, la meilleure façon de répliquer les clés consiste à les copier du système de fichiers de l’instance source vers celle des instances cibles sur lesquelles vous souhaitez répliquer les clés. Pour plus d’informations, consultez « Réplication de la clé HMAC » ci-dessous.
1. Le jeton encapsulé doit être activé. Vous pouvez l’activer avec la console web.

### Réplication de la clé HMAC {#replicating-the-hmac-key}

Pour répliquer la clé sur plusieurs instances, vous devez :

1. Accédez à l’instance AEM, généralement une instance de création, et qui contient le matériel des clés à copier.
1. Localisez le lot `com.adobe.granite.crypto.file` dans le système de fichiers local. Par exemple, sous ce chemin d’accès :

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   Le fichier `bundle.info` à l’intérieur de chaque dossier identifie le nom du lot.

1. Accédez au dossier des données. Par exemple :

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Copier les fichiers HMAC et maîtres.
1. Ensuite, accédez à l’instance cible sur laquelle vous souhaitez dupliquer la clé HMAC, puis accédez au dossier des données. Par exemple :

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. Collez les deux fichiers copiés précédemment.
1. [Actualisez le lot de chiffrement](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) si l’instance cible est déjà en cours d’exécution.

1. Répétez les étapes ci-dessus pour toutes les instances sur lesquelles vous souhaitez répliquer la clé.

#### Activation du jeton encapsulé {#enabling-the-encapsulated-token}

Une fois la clé HMAC répliquée, vous pouvez activer le jeton encapsulé à l’aide de la console Web :

1. Pointez votre navigateur sur `https://serveraddress:port/system/console/configMgr`.
1. Recherchez une entrée nommée **Gestionnaire d’authentification des jetons Adobe Granite** et cliquez dessus.
1. Dans la fenêtre suivante, cochez la case **Activer la prise en charge des jetons encapsulés** et cliquez sur **Enregistrer**.
