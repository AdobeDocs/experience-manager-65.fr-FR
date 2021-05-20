---
title: Synchronisation des utilisateurs des communautés
seo-title: Synchronisation des utilisateurs des communautés
description: Fonctionnement de la synchronisation des utilisateurs
seo-description: Fonctionnement de la synchronisation des utilisateurs
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
role: Administrator
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 12%

---

# Synchronisation des utilisateurs des communautés {#communities-user-synchronization}

## Présentation {#introduction}

Dans AEM Communities, dans l’environnement de publication (en fonction des autorisations configurées), les *visiteurs du site* peuvent devenir *membres*, créer des *groupes d’utilisateurs* et modifier leur *profil du membre* .

*Les* données utilisateur sont un terme qui désigne  *les utilisateurs*, les  *profils utilisateur et les groupes* d’utilisateurs **.

** L’appartenance est un terme utilisé pour désigner les  ** utilisateurs enregistrés dans l’environnement de publication, par opposition aux utilisateurs enregistrés dans l’environnement de création.

Pour plus d’informations sur les données utilisateur, voir [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).

## Synchronisation des utilisateurs sur une ferme de publication {#synchronizing-users-across-a-publish-farm}

Par conception, les données utilisateur créées dans l’environnement de publication n’apparaissent pas dans l’environnement de création.

La plupart des données utilisateur créées dans l’environnement de création sont destinées à rester dans l’environnement de création et ne sont ni synchronisées ni répliquées vers les instances de publication.

Lorsque la [topologie](/help/communities/topologies.md) est une [ferme de publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm), l’enregistrement et les modifications effectués sur une instance de publication doivent être synchronisés avec d’autres instances de publication. Les membres doivent pouvoir se connecter et voir leurs données sur n’importe quel noeud de publication.

Lorsque la synchronisation des utilisateurs est activée, les données utilisateur sont automatiquement synchronisées entre les instances de publication dans la ferme de serveurs.

### Instructions de configuration de la synchronisation des utilisateurs {#user-sync-setup-instructions}

Pour obtenir des instructions détaillées, détaillées sur la manière d’activer la synchronisation sur une ferme de publication, voir :

* [Synchronisation des utilisateurs](/help/sites-administering/sync.md)

## Synchronisation des utilisateurs en arrière-plan {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **package vlt**

   Il s’agit d’un fichier zip de toutes les modifications apportées à un éditeur, qui doit être distribué entre les éditeurs. Les modifications sur un éditeur génèrent des événements qui sont sélectionnés par l’écouteur d’événement change. Cela crée un module vlt contenant toutes les modifications.

* **package de distribution**

   Il contient des informations de distribution pour Sling. Il s’agit d’informations sur l’endroit où le contenu doit être distribué et le moment où il a été distribué en dernier.

## Que se passe-t-il lorsque ... {#what-happens-when}

### Publier le site à partir de la console Sites des communautés {#publish-site-from-communities-sites-console}

Lorsqu’un site de communauté est publié à partir de la [console Sites des communautés](/help/communities/sites-console.md), l’effet est de [répliquer](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) les pages associées, et Sling distribue les groupes d’utilisateurs de communauté créés dynamiquement, y compris leur appartenance.

### L’utilisateur est créé ou le profil est modifié lors de la publication {#user-is-created-or-edits-profile-on-publish}

Par conception, les utilisateurs et les profils créés dans l’environnement de publication (par exemple par auto-inscription, connexion sociale, authentification LDAP) n’apparaissent pas dans l’environnement de création.

Lorsque la topologie est une [ferme de publication](/help/communities/topologies.md) et que la synchronisation des utilisateurs a été correctement configurée, *user* et *profil utilisateur* sont synchronisés dans la ferme de publication à l’aide de la distribution Sling.

### Un nouveau groupe de communautés est créé sur la publication {#new-community-group-is-created-on-publish}

Bien qu’elle soit lancée à partir d’une instance de publication, la création de groupe de communautés, qui entraîne la création de pages de site et d’un nouveau groupe d’utilisateurs, a lieu dans les faits sur l’instance d’auteur.

Dans le cadre du processus, les nouvelles pages du site sont répliquées vers toutes les instances de publication. Le groupe d’utilisateurs de la communauté créé dynamiquement et ses membres sont Sling distribués à toutes les instances de publication.

### Les utilisateurs ou les groupes d’utilisateurs sont créés à l’aide de la console Sécurité.{#users-or-user-groups-are-created-using-security-console}

Par défaut, les données utilisateur créées dans l’environnement de publication ne sont pas visibles dans l’environnement de création, et vice versa.

Lorsque la console [Administration et sécurité des utilisateurs](/help/sites-administering/security.md) est utilisée pour ajouter de nouveaux utilisateurs dans l’environnement de publication, la synchronisation des utilisateurs synchronise les nouveaux utilisateurs et leur appartenance à un groupe sur d’autres instances de publication, si nécessaire. La synchronisation des utilisateurs synchronise également les groupes d’utilisateurs créés via la console de sécurité.

### L’utilisateur publie du contenu sur la publication {#user-posts-content-on-publish}

Pour le contenu généré par l’utilisateur (UGC), les données saisies sur une instance de publication sont accessibles via la [SRP configurée](/help/communities/srp-config.md).

## Bonnes pratiques {#bestpractices}

Par défaut, la synchronisation des utilisateurs est **désactivée**. Activer la synchronisation des utilisateurs implique de modifier les configurations OSGi *existantes.* Aucune configuration nouvelle ne doit être ajoutée suite à l’activation de la synchronisation des utilisateurs.

La synchronisation des utilisateurs repose sur l’environnement de création pour gérer les distributions de données utilisateur, même si les données utilisateur ne sont pas créées en mode de création.

**Conditions préalables**

1. Si les utilisateurs et les groupes d’utilisateurs ont déjà été créés sur un éditeur, il est recommandé de [synchroniser manuellement](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) les données utilisateur sur tous les éditeurs avant de configurer et d’activer la synchronisation des utilisateurs.

   Une fois la synchronisation des utilisateurs activée, seuls les utilisateurs et les groupes nouvellement créés sont synchronisés .

1. Vérifiez que le code le plus récent a été installé :

   * [Mise à jour de la plateforme AEM](https://helpx.adobe.com/fr/experience-manager/kb/aem62-available-hotfixes.html)
   * [Mises à jour d’AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Les paramétrages suivants sont nécessaires pour permettre la synchronisation des utilisateurs sur AEM Communities. Assurez-vous que ces configurations sont correctes pour empêcher l’échec de la distribution de contenu sling.

### Agent de distribution Apache Sling - Fabrique d’agents de synchronisation {#apache-sling-distribution-agent-sync-agents-factory}

Cette configuration récupère le contenu à synchroniser dans les éditeurs. La configuration se trouve sur l’instance d’auteur . L’auteur doit effectuer le suivi de tous les éditeurs présents et où synchroniser toutes les informations.

Les valeurs par défaut de la configuration concernent une seule instance de publication. Comme la synchronisation des utilisateurs est utile pour synchroniser plusieurs instances de publication, comme pour une ferme de publication, des instances de publication supplémentaires doivent être ajoutées à la configuration.

**Comment le contenu est-il synchronisé ?**

L’instance d’auteur envoie un ping au point de terminaison de l’exportateur des éditeurs. Chaque fois qu’un utilisateur est créé ou mis à jour sur des éditeurs spécifiques (n), l’auteur obtient le contenu à partir de ses points de terminaison d’exportateur et [envoie le contenu](/help/communities/sync.md#main-pars-image-1413756164) à d’autres éditeurs (n-1, à l’exception des éditeurs à partir desquels le contenu est récupéré).

Pour configurer la configuration des agents de synchronisation Apache Sling :

1. Connectez-vous avec les privilèges d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html). Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Recherchez **Agent de distribution Apache Sling - Fabrique d’agents de synchronisation**.

   * Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

      Vérifiez le nom : **socialpubsync.**

   * Cochez la case **Activé** .
   * Sélectionnez **Utiliser plusieurs files d’attente.**
   * Spécifiez **Points de terminaison de l’exportateur** et **Points de terminaison de l’importateur** (vous pouvez ajouter d’autres points de terminaison de l’exportateur et de l’importateur).

      Ces points de terminaison définissent l’emplacement d’où vous souhaitez obtenir le contenu et l’emplacement où vous souhaitez pousser le contenu. L’auteur récupère le contenu à partir du point de terminaison de l’exportateur spécifié et envoie le contenu aux éditeurs (autres que l’éditeur à partir duquel il a récupéré le contenu).
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Distribution Adobe Granite - Fournisseur secret du transport de mot de passe chiffré {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Il permet à l’auteur d’identifier l’utilisateur autorisé, comme ayant l’autorisation de synchroniser les données utilisateur de l’auteur à la publication.

L’utilisateur [autorisé créé](/help/sites-administering/sync.md#createauthuser) sur toutes les instances de publication aide les éditeurs à se connecter à l’auteur et à configurer la distribution Sling sur l’auteur. Cet utilisateur autorisé possède toutes les [listes de contrôle d’accès ](/help/sites-administering/sync.md#howtoaddacl) requises.

Chaque fois que des données doivent être installées ou récupérées auprès des éditeurs, l’auteur se connecte aux éditeurs à l’aide des informations d’identification (nom d’utilisateur et mot de passe) définies dans cette configuration.

Pour connecter l’auteur aux éditeurs à l’aide d’un utilisateur autorisé :

1. Connectez-vous avec les privilèges d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console web](/help/sites-deploying/configuring-osgi.md).

   Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Recherchez **Distribution Granite Adobe - Fournisseur secret de transport de mot de passe chiffré.**
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifiez la propriété **socialpubsync** - **publishUser.**

1. Définissez le nom d’utilisateur et le mot de passe sur l’[utilisateur autorisé](/help/sites-administering/sync.md#createauthorizeduser).

   Par exemple, **usersync - admin**

![granite-pasword-trans](assets/granite-paswrd-trans.png)

### Agent de distribution Apache Sling - Fabrique d’agents de file d’attente {#apache-sling-distribution-agent-queue-agents-factory}

Cette configuration est utilisée pour configurer les données que vous souhaitez synchroniser entre les éditeurs. Lorsque les données sont créées/mises à jour dans les chemins spécifiés dans **Racines autorisées**, la variable &quot;var/community/distribution/diff&quot; est activée et le réplicateur créé récupère les données d’un éditeur et les installe sur d’autres éditeurs.

Pour configurer les données (chemins d’accès aux noeuds) à synchroniser :

1. Connectez-vous avec les privilèges d’administrateur sur votre instance de création.
1. Accédez à la [console web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Recherchez **Agent de distribution Apache Sling - Fabrique d’agents de file d’attente**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifiez le nom : **socialpubsync -reverse**

1. Cochez la case **Activé** et enregistrez.
1. Spécifiez les chemins d’accès aux noeuds à répliquer dans **Racines autorisées**.
1. Répétez cette opération pour chaque instance **publish**.

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Distribution Granite des Adobes - Fabrique observateur diff {#adobe-granite-distribution-diff-observer-factory}

Cette configuration synchronise l’appartenance des groupes entre les éditeurs.
Si la modification de l’appartenance d’un groupe dans un éditeur ne met pas à jour son appartenance sur d’autres éditeurs, assurez-vous que **ref:members** est ajouté à **noms de propriétés**.

Pour garantir la synchronisation des membres :

1. Connectez-vous avec les privilèges d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localisez **Distribution Granite d’Adobe - Fabrique observateur diff**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifiez le **nom de l’agent : socialpubsync -reverse**.

1. Cochez la case **Activé** .
1. Spécifiez **rep:members** comme description pour propertyName dans **noms de propriétés** et enregistrez.

   ![diff-obs](assets/diff-obs.png)

### Déclencheur de distribution Apache Sling - Fabrique de déclencheurs planifiés {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Cette configuration vous permet de configurer l’intervalle d’interrogation (au-delà duquel les éditeurs sont ingérés et les modifications sont extraites par l’auteur) pour synchroniser les modifications entre les éditeurs.

L’auteur interroge les éditeurs toutes les 30 secondes (par défaut). Si des modules sont présents dans le dossier `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, ils seront récupérés et installés sur d’autres éditeurs.

Pour modifier l’intervalle d’interrogation :

1. Connectez-vous avec les privilèges d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console Web](/help/sites-deploying/configuring-osgi.md), par exemple [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localisez **Déclencheur de distribution Apache Sling - Fabrique de déclencheurs planifiés**

   * Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

      Vérifiez **socialpubsync -scheduled-trigger**

   * Définissez l’intervalle en secondes sur l’intervalle souhaité, puis enregistrez.

   ![scheduled-trigger](assets/scheduled-trigger.png)

### Écouteur de synchronisation des utilisateurs AEM Communities {#aem-communities-user-sync-listener}

Pour les problèmes de distribution Sling où il y a une incohérence dans les abonnements et les suivants, vérifiez si les propriétés suivantes dans les configurations **Écouteur de synchronisation des utilisateurs AEM Communities** sont définies :

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

Pour synchroniser les abonnements, les informations suivantes et les notifications

Sur chaque instance de publication AEM :

1. Connectez-vous avec les privilèges d’administrateur.
1. Accédez à la [console web](/help/sites-deploying/configuring-osgi.md). Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Recherchez **Écouteur de synchronisation des utilisateurs AEM Communities**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifiez le nom : **socialpubsync -scheduled-trigger**

1. Définissez les **NodeTypes** suivants :

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   Les types de noeuds spécifiés dans cette propriété se synchronisent et les informations de notification (blogs et configurations suivis) sont synchronisées entre les différents éditeurs.

1. Ajoutez tous les dossiers à synchroniser dans **DistributedFolders**. Par exemple,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Définissez **ignorablenodes** sur :

   `.tokens`

   `system`

   `rep:cache` (puisque nous utilisons des sessions persistantes, nous n’avons pas besoin de synchroniser ce noeud avec différents éditeurs).

   ![user-sync-listner](assets/user-sync-listner.png)

### Identifiant Sling unique{#unique-sling-id}.

AEM instance d’auteur utilise l’identifiant Sling pour identifier à partir de quel endroit les données arrivent et vers quels éditeurs elle doit (ou ne doit pas) renvoyer le module.

Assurez-vous que tous les éditeurs d’une ferme de publication possèdent un identifiant Sling unique. Si l’identifiant Sling est le même pour plusieurs instances de publication dans une ferme de publication, la synchronisation des utilisateurs échoue. Comme l’auteur ne sait pas où récupérer le module et où l’installer.

Pour garantir un identifiant Sling unique des éditeurs dans la ferme de publication, sur chaque instance de publication :

1. Accédez à [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Vérifiez la valeur de **Sling ID**.

   ![slingid](assets/slingid.png)

   Si l’identifiant Sling d’une instance de publication correspond à l’identifiant Sling d’une autre instance de publication, alors :

1. Arrêtez l’une des instances de publication ayant un identifiant Sling correspondant.
1. Dans le répertoire `crx-quickstart/launchpad/felix`, recherchez et supprimez le fichier nommé *sling.id.file.*

   Par exemple, sur un système Linux :

   `rm -i $(find . -type f -name sling.id.file)`

   Par exemple, sur un système Windows :

   Utilisez l’explorateur Windows et recherchez `sling.id.file`

1. Démarrez l’instance de publication. Au démarrage, un nouvel identifiant Sling lui sera attribué.
1. Vérifiez que l’**ID Sling** est désormais unique.

Répétez ces étapes jusqu’à ce que toutes les instances de publication aient un identifiant Sling unique.

### Fabrique Vault Package Builder {#vault-package-builder-factory}

Pour que les mises à jour soient correctement synchronisées, il est nécessaire de modifier le créateur de modules Vault pour la synchronisation des utilisateurs.
Dans `/home/users`, un noeud `*/rep:cache` est créé. Il s’agit d’un cache qui permet de trouver que si nous effectuons une requête sur le nom principal d’un noeud, ce cache peut être utilisé directement.

La synchronisation des utilisateurs peut s’arrêter si les noeuds `rep :cache` sont synchronisés entre les éditeurs.

Pour vous assurer que les mises à jour sont correctement synchronisées entre les éditeurs, sur chaque instance de publication AEM :

1. Accédez à la [console web](/help/sites-deploying/configuring-osgi.md)

   Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localisez le **Module de distribution Apache Sling - Fabrique Vault Package Builder**

   Nom du créateur : socialpubsync-vlt.

1. Sélectionnez l’icône de modification.
1. Ajoutez deux filtres de noeuds de module :
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Gestion des stratégies
   * Pour remplacer les noeuds rep:policy existants par de nouveaux noeuds, ajoutez un troisième filtre de module : `/home/users|+.*/rep:policy`
   * Pour empêcher la distribution des stratégies, définissez : `Acl Handling: IGNORE`

   ![Fabrique du générateur de packages Vault](assets/vault-package-builder-factory.png)

## Résolution des problèmes de distribution Sling dans AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Si la distribution Sling échoue, essayez les étapes de débogage suivantes :

1. **Rechercher les configurations  [ajoutées de manière incorrecte](/help/sites-administering/sync.md#improperconfig)**

   Assurez-vous que plusieurs configurations ne sont pas ajoutées ni modifiées. Les configurations par défaut existantes doivent être modifiées.
1. **Vérifier les configurations**

   Assurez-vous que toutes les [configurations](/help/communities/sync.md#bestpractices) sont correctement définies dans votre instance d’auteur AEM, comme indiqué dans la section [Bonnes pratiques](/help/communities/sync.md#main-pars-header-863110628).

1. **Vérifier les autorisations d’utilisateur autorisées**

   Si les packages ne sont pas installés correctement, vérifiez que l’utilisateur [autorisé](/help/sites-administering/sync.md#createauthuser) créé dans la première instance de publication possède les listes de contrôle d’accès correctes.

   Pour valider cette opération, au lieu de la configuration [utilisateur autorisé ](/help/sites-administering/sync.md#createauthuser) créée, modifiez la configuration [Distribution Granite d’Adobe - Fournisseur secret de transport de mot de passe chiffré](/help/sites-administering/sync.md#adobegraniteencpasswrd) sur l’instance d’auteur pour utiliser les informations d’identification d’utilisateur administrateur. Maintenant, essayez de réinstaller les packages. Si la synchronisation de l’utilisateur fonctionne correctement avec les informations d’identification de l’administrateur, cela signifie que l’utilisateur de publication créé ne disposait pas des listes de contrôle d’accès appropriées.

1. **Vérification de la configuration de l’usine Diff Observer**

   Si seuls des noeuds spécifiques ne sont pas synchronisés dans la ferme de publication (par exemple, les membres du groupe ne sont pas synchronisés), assurez-vous que la configuration [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) est activée et **rep : Les membres** sont définis dans **noms des propriétés**.

1. **Vérifiez la configuration du récepteur de synchronisation des utilisateurs AEM Communities.** Si les utilisateurs créés sont synchronisés mais que les abonnements et les suivants ne fonctionnent pas, assurez-vous que la configuration du récepteur de synchronisation des utilisateurs d’AEM Communities dispose des éléments suivants :

   * Types de noeuds : définis sur **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder** et **sling:OrderedFolder**.
   * Noeuds ignorables : définis sur **.tokens**, **system** et **rep:cache**.
   * Dossiers distribués : définis sur les dossiers à répartir.

1. **Vérifier les journaux générés lors de la création de l’utilisateur sur l’instance de publication**

   Si les configurations ci-dessus sont correctement définies et que la synchronisation des utilisateurs ne fonctionne pas, vérifiez les journaux générés lors de la création de l’utilisateur.

   Vérifiez si l’ordre des logs est le même, comme suit :

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

Pour déboguer :

1. Désactivez la synchronisation des utilisateurs :
1. Sur AEM instance d’auteur, connectez-vous avec les privilèges d’administrateur.

   1. Accédez à la [console web](/help/sites-deploying/configuring-osgi.md). Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Recherchez la configuration **Agent de distribution Apache Sling - Fabrique d’agents de synchronisation**.
   1. Décochez la case **Activé** .

      Lors de la désactivation de la synchronisation des utilisateurs sur l’instance d’auteur, les points de terminaison (exportateur et importateur) sont désactivés et l’instance d’auteur est statique. Les packages **vlt** ne sont ni ingérés ni récupérés par l’auteur.

      Désormais, si un utilisateur est créé sur l’instance de publication, le package **vlt** est créé dans le noeud */var/sling/distribution/packages/ socialpubsync - vlt /data* . Et si ces modules sont transmis par l’auteur à un autre service. Vous pouvez télécharger et extraire ces données pour vérifier toutes les propriétés qui sont transmises à d’autres services.

1. Accédez à un éditeur et créez un utilisateur sur l’éditeur. Par conséquent, des événements sont créés.
1. Vérifiez l’ [ordre des journaux](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities), créés lors de la création de l’utilisateur.
1. Vérifiez si un package **vlt** est créé sur **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Maintenant, activez la synchronisation des utilisateurs sur AEM instance d’auteur.
1. Sur l’éditeur, modifiez les points de terminaison de l’exportateur ou de l’importateur dans **Agent de distribution Apache Sling - Fabrique d’agents de synchronisation**.
Nous pouvons télécharger et extraire des données de package pour vérifier toutes les propriétés qui sont transmises à d’autres éditeurs et quelles données sont perdues.
