---
title: Prise en charge des jetons encapsulés
seo-title: Prise en charge des jetons encapsulés
description: Familiarisez-vous avec la prise en charge des jetons encapsulés dans AEM.
seo-description: Familiarisez-vous avec la prise en charge des jetons encapsulés dans AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
translation-type: tm+mt
source-git-commit: 215f062f80e7abfe35698743ce971394d01d0ed6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 88%

---


# Prise en charge des jetons encapsulés{#encapsulated-token-support}

## Présentation {#introduction}

Par défaut, AEM utilise le gestionnaire d’authentification des jetons pour authentifier chaque demande. Cependant, pour traiter des demandes d’authentification, le gestionnaire d’authentification des jetons doit avoir accès au référentiel pour chaque demande. Ceci est dû au fait que des cookies sont utilisés pour maintenir l’état d’authentification. Logiquement, l’état doit perdurer dans le référentiel afin de valider les demandes ultérieures. En effet, cela signifie que le mécanisme d’authentification tient compte de tous les détails de l’état de l’activité à laquelle il participe.

Cela est particulièrement important pour l’évolutivité horizontale. Dans une configuration comportant plusieurs instances, comme la ferme de serveurs de publication représentée ci-dessous, l’équilibrage de charge ne peut pas être exécuté de façon optimale. Lorsque l’authentification tient compte de l’état, l’état d’authentification conservé est disponible uniquement sur l’instance sur laquelle l’utilisateur s’est authentifié.

![chlimage_1-33](assets/chlimage_1-33a.png)

Imaginez le scénario suivant à titre d’exemple :

Un utilisateur peut être authentifié sur l’instance de publication 1, mais si une demande ultérieure est envoyée sur l’instance de publication 2, cet état d’authentification conservé n’existe pas sur cette instance, car il a été conservé dans le référentiel de l’instance de publication 1, et l’instance de publication 2 possède son propre référentiel.

La solution consiste à configurer des connexions persistantes au niveau de l’équilibreur de charge. Avec des connexions persistantes, un utilisateur serait toujours dirigé vers la même instance de publication. Par conséquent, il n’est pas possible de vraiment optimiser l’équilibrage de charge.

Si une instance de publication devient inaccessible, tous les utilisateurs authentifiés sur cette instance perdent leur session, puisque pour valider le cookie d’authentification, il est nécessaire d’accéder au référentiel.

## Authentification sans état avec le jeton encapsulé {#stateless-authentication-with-the-encapsulated-token}

Pour permettre une évolutivité horizontale, la solution consiste à recourir à une authentification sans état grâce à la nouvelle prise en charge des jetons encapsulés dans AEM.

Le jeton encapsulé est un élément de cryptographie qui permet aux AEM de créer et de valider en toute sécurité des informations d&#39;authentification hors ligne, sans accéder au référentiel. Ainsi, une demande d’authentification peut être effectuée sur toutes les instances de publication, sans nécessiter de connexions persistantes. Elle offre également l’avantage d’optimiser les performances d’authentification, car il n’est pas nécessaire d’accéder au référentiel pour chaque demande d’authentification.

Vous pouvez découvrir comment cela fonctionne dans un déploiement distribué géographiquement avec les instances de création MongoMK et de publication TarMK ci-dessous :

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>Le jeton encapsulé concerne l’authentification. Il permet de s’assurer que le cookie peut être validé sans avoir à accéder au référentiel. Cependant, l’utilisateur doit exister sur toutes les instances et chaque instance doit pouvoir accéder aux informations stockées pour cet utilisateur.
>
>Par exemple, si un nouvel utilisateur est créé sur l’instance de publication 1, en raison du fonctionnement du jeton encapsulé, il est authentifié correctement sur l’instance de publication 2. Si l’utilisateur n’existe pas sur la deuxième instance de publication, la demande ne réussit toujours pas.


## Configuration du jeton encapsulé {#configuring-the-encapsulated-token}

>[!NOTE]
>Tous les gestionnaires d’authentification qui synchronisent les utilisateurs et reposent sur l’authentification par jeton (tels que SAML et OAuth) ne fonctionnent qu’avec des jetons encapsulés si :
>
>* Les sessions bascules sont activées ou
   >
   >
* Les utilisateurs sont déjà créés dans AEM lors du début de la synchronisation. Cela signifie que les jetons encapsulés ne seront pas pris en charge dans les situations où les gestionnaires **créent** des utilisateurs pendant le processus de synchronisation.


Lors de la configuration du jeton encapsulé, différents éléments doivent être pris en compte :

1. Compte tenu du chiffrement impliqué, toutes les instances doivent posséder la même clé HMAC. À compter d’AEM 6.3, le matériel de la clé n’est plus stocké dans le référentiel, mais sur le système de fichiers réel. Ainsi, la meilleure façon de répliquer les clés consiste à les copier du système de fichiers de l’instance source vers celle des instances cibles sur lesquelles vous souhaitez répliquer les clés. Consultez les informations supplémentaires dans la section « Réplication de la clé HMAC » ci-dessous.
1. Le jeton encapsulé doit être activé. Cette opération peut être effectuée à l’aide de la console web.

### Réplication de la clé HMAC {#replicating-the-hmac-key}

The HMAC key is present as a binary property of `/etc/key` in the repository. Vous pouvez la télécharger séparément en cliquant sur le lien **afficher** en regard :

![chlimage_1-35](assets/chlimage_1-35a.png)

Pour répliquer la clé sur plusieurs instances, procédez comme suit :

1. Accédez à l’instance AEM, généralement une instance de création, et qui contient le matériel des clés à copier.
1. Cherchez le lot `com.adobe.granite.crypto.file` dans le système de fichiers local. Par exemple, sous ce chemin d’accès :

   * &lt;rép-install-aem-création>/crx-quickstart/launchpad/felix/bundle21

   Le fichier `bundle.info` à l’intérieur de chaque dossier identifie le nom du lot.

1. Accédez au dossier des données. Par exemple :

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copiez les fichiers HMAC et les fichiers principaux.
1. Ensuite, accédez à l’instance cible sur laquelle vous souhaitez dupliquer la clé HMAC, puis accédez au dossier des données. Par exemple :

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Collez les deux fichiers copiés précédemment.
1. [Actualisez le lot de chiffrement](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) si l’instance cible est déjà en cours d’exécution.

1. Répétez les étapes ci-dessus pour toutes les instances sur lesquelles vous souhaitez répliquer la clé.

#### Activation du jeton encapsulé {#enabling-the-encapsulated-token}

Une fois la clé HMAC répliquée, vous pouvez activer le jeton encapsulé à l’aide de la console web :

1. Pointez votre navigateur sur `https://serveraddress:port/system/console/configMgr`
1. Recherchez une entrée nommée **Day CRX Token Authentication Handler** et cliquez dessus.
1. Dans la fenêtre suivante, cochez la case **Activer la prise en charge des jetons encapsulés** et cliquez sur **Enregistrer**.

