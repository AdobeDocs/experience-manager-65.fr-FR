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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2510'
ht-degree: 12%

---


# Synchronisation des utilisateurs des communautés {#communities-user-synchronization}

## Présentation {#introduction}

En AEM Communities, à partir de l’environnement de publication (selon les autorisations configurées), *les visiteurs du site* peuvent devenir *membres*, créer *groupes d’utilisateurs* et modifier leur *profil membre*.

*Les* données utilisateur sont un terme qui désigne  *les utilisateurs*, les  *profils d’* utilisateur et les groupes *d’* utilisateurs.

*L’* appartenance est un terme utilisé pour désigner les  ** utilisateurs enregistrés dans l’environnement de publication, par opposition aux utilisateurs enregistrés dans l’environnement d’auteur.

Pour plus d&#39;informations sur les données utilisateur, consultez [Gestion des utilisateurs et des groupes d&#39;utilisateurs](/help/communities/users.md).

## Synchronisation des utilisateurs sur une batterie de publication {#synchronizing-users-across-a-publish-farm}

Par conception, les données utilisateur créées dans l’environnement de publication n’apparaissent pas dans l’environnement d’auteur.

La plupart des données utilisateur créées dans l’environnement d’auteur sont destinées à rester dans l’environnement d’auteur et ne sont ni synchronisées ni répliquées dans les instances de publication.

Lorsque la [topologie](/help/communities/topologies.md) est une [batterie de publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm), l’enregistrement et les modifications effectués sur une instance de publication doivent être synchronisés avec d’autres instances de publication. Les membres doivent pouvoir se connecter et voir leurs données sur n’importe quel noeud de publication.

Lorsque la synchronisation des utilisateurs est activée, les données utilisateur sont automatiquement synchronisées dans les instances de publication de la batterie.

### Instructions de configuration de la synchronisation des utilisateurs {#user-sync-setup-instructions}

Pour obtenir des instructions détaillées et détaillées sur la façon d’activer la synchronisation sur une batterie de publication, voir :

* [Synchronisation des utilisateurs](/help/sites-administering/sync.md)

## Synchronisation utilisateur en arrière-plan {#user-sync-in-the-background}

![workflow sling-dist](assets/sling-dist-workflow.png)

* **package vlt**

   Il s’agit d’un fichier zip contenant toutes les modifications apportées à un éditeur, qui doit être distribué entre les éditeurs. Les modifications effectuées sur un éditeur génèrent des événements qui sont sélectionnés par l’écouteur du événement de modification. Ceci crée un package vlt contenant toutes les modifications.

* **module de distribution**

   Il contient des informations de distribution pour Sling. Il s&#39;agit d&#39;informations sur l&#39;endroit où le contenu doit être distribué, et quand a-t-il été distribué en dernier.

## Ce qui se passe lorsque ... {#what-happens-when}

### Publier le site à partir de la console Sites des communautés {#publish-site-from-communities-sites-console}

Sur l’auteur, lorsqu’un site communautaire est publié à partir de la [console Sites communautaires](/help/communities/sites-console.md), l’effet est de [reproduire](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) les pages associées, et Sling distribue les groupes d’utilisateurs communautaires créés dynamiquement, y compris leur adhésion.

### L’utilisateur est créé ou modifie le Profil sur Publier {#user-is-created-or-edits-profile-on-publish}

Par conception, les utilisateurs et les profils créés dans l’environnement de publication (par exemple par auto-inscription, connexion sociale, authentification LDAP) n’apparaissent pas dans l’environnement d’auteur.

Lorsque la topologie est une [batterie de publication](/help/communities/topologies.md) et que la synchronisation des utilisateurs a été correctement configurée, les *profil utilisateur* et *utilisateur* sont synchronisés dans la batterie de publication à l’aide de la distribution Sling.

### Un nouveau groupe de communautés est créé sur la publication {#new-community-group-is-created-on-publish}

Bien qu’elle soit lancée à partir d’une instance de publication, la création de groupe de la communauté, qui se traduit par de nouvelles pages de site et un nouveau groupe d’utilisateurs, se produit en fait sur l’instance d’auteur.

Dans le cadre du processus, les nouvelles pages du site sont répliquées sur toutes les instances de publication. Le groupe d’utilisateurs de la communauté créé dynamiquement et ses membres sont Sling distribués à toutes les instances de publication.

### Les utilisateurs ou les groupes d’utilisateurs sont créés à l’aide de la console Sécurité.{#users-or-user-groups-are-created-using-security-console}

Par défaut, les données utilisateur créées dans l’environnement de publication ne sont pas visibles dans l’environnement de création, et vice versa.

Lorsque la console [Administration et sécurité des utilisateurs](/help/sites-administering/security.md) est utilisée pour ajouter de nouveaux utilisateurs dans l’environnement de publication, la synchronisation des utilisateurs synchronise les nouveaux utilisateurs et leur appartenance à un groupe sur d’autres instances de publication, si nécessaire. La synchronisation des utilisateurs synchronise également les groupes d’utilisateurs créés via la console de sécurité.

### L’utilisateur publie du contenu sur la publication {#user-posts-content-on-publish}

Pour le contenu généré par l’utilisateur (UGC), les données saisies sur une instance de publication sont accessibles par le biais de l’[SRP](/help/communities/srp-config.md) configuré.

## Bonnes pratiques {#bestpractices}

Par défaut, la synchronisation des utilisateurs est **désactivée**. Activer la synchronisation des utilisateurs implique de modifier les configurations OSGi *existantes.* Aucune configuration nouvelle ne doit être ajoutée suite à l’activation de la synchronisation des utilisateurs.

La synchronisation des utilisateurs repose sur l’environnement de création pour gérer les distributions de données utilisateur, même si les données utilisateur ne sont pas créées en mode de création.

**Conditions préalables**

1. Si les utilisateurs et les groupes d’utilisateurs ont déjà été créés sur un éditeur, il est recommandé de [synchroniser manuellement](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) les données utilisateur sur tous les éditeurs avant de configurer et d’activer la synchronisation des utilisateurs.

   Une fois la synchronisation des utilisateurs activée, seuls les utilisateurs et les groupes nouvellement créés sont synchronisés .

1. Vérifiez que le code le plus récent a été installé :

   * [Mise à jour de la plateforme AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr)
   * [Mises à jour d’AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Les configurations suivantes sont nécessaires pour activer la synchronisation des utilisateurs sur AEM Communities. Assurez-vous que ces configurations sont correctes pour empêcher l’échec de la distribution de contenu sling.

### Agent de distribution Apache Sling - Fabrique d’agents de synchronisation {#apache-sling-distribution-agent-sync-agents-factory}

Cette configuration récupère le contenu à synchroniser entre les éditeurs. La configuration se trouve sur l’instance d’auteur. L&#39;auteur doit suivre tous les éditeurs qui sont là et où synchroniser toutes les informations.

Les valeurs par défaut dans la configuration sont pour une instance de publication unique. Comme la synchronisation des utilisateurs est utile pour synchroniser plusieurs instances de publication, par exemple pour une batterie de publication, d’autres instances de publication doivent être ajoutées à la configuration.

**Comment le contenu est-il synchronisé ?**

L’instance d’auteur fait pivoter le point de terminaison d’exportateur des éditeurs. Chaque fois qu’un utilisateur est créé ou mis à jour sur des éditeurs spécifiques (n), l’auteur obtient le contenu de ses points de terminaison d’exportation et [envoie le contenu](/help/communities/sync.md#main-pars-image-1413756164) à d’autres éditeurs (n-1, à l’exception des éditeurs dont le contenu est récupéré).

Pour configurer la configuration des agents de synchronisation Apache Sling :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console Web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html). Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localisez **Apache Sling Distribution Agent - Sync Agents Factory**.

   * Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

      Vérifier le nom : **socialpubsync.**

   * Cochez la case **Activé**.
   * Sélectionnez **Utiliser plusieurs files d&#39;attente.**
   * Spécifiez **Points de terminaison de l’exportateur** et **Points de terminaison de l’importateur** (vous pouvez ajouter d’autres points de terminaison d’exportateur et d’importateur).

      Ces points de terminaison définissent l’emplacement d’où vous souhaitez obtenir le contenu et l’emplacement où vous souhaitez pousser le contenu. L’auteur récupère le contenu à partir du point de terminaison d’exportation spécifié et envoie le contenu aux éditeurs (autres que l’éditeur à partir duquel il a récupéré le contenu).
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Distribution Adobe Granite - Fournisseur secret du transport de mot de passe chiffré {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Il permet à l’auteur d’identifier l’utilisateur autorisé, comme ayant l’autorisation de synchroniser les données utilisateur de l’auteur à la publication.

L’[utilisateur autorisé créé](/help/sites-administering/sync.md#createauthuser) sur toutes les instances de publication permet aux éditeurs de se connecter à l’auteur et de configurer la distribution Sling sur l’auteur. Cet utilisateur autorisé dispose de toutes les [ACL](/help/sites-administering/sync.md#howtoaddacl) requises.

Chaque fois que des données doivent être installées ou extraites d’éditeurs, l’auteur se connecte aux éditeurs à l’aide des informations d’identification (nom d’utilisateur et mot de passe) définies dans cette configuration.

Pour connecter l’auteur aux éditeurs à l’aide d’un utilisateur autorisé :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console Web](/help/sites-deploying/configuring-osgi.md).

   Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localisez **Distribution de granit d&#39;Adobe - Fournisseur secret de transport de mot de passe chiffré.**
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifiez la propriété **socialpubsync** - **publishUser.**

1. Définissez le nom d’utilisateur et le mot de passe sur l’[utilisateur autorisé](/help/sites-administering/sync.md#createauthorizeduser).

   Par exemple, **usersync - admin**

![granit-paswrd-trans](assets/granite-paswrd-trans.png)

### Agent de distribution Apache Sling - Fabrique d’agents de file d’attente {#apache-sling-distribution-agent-queue-agents-factory}

Cette configuration permet de configurer les données que vous souhaitez synchroniser entre les éditeurs. Lorsque des données sont créées/mises à jour dans les chemins spécifiés dans **Allowed Roots**, &quot;var/community/distribution/diff&quot; est activé et le réplicateur créé récupère les données d&#39;un éditeur et les installe sur d&#39;autres éditeurs.

Pour configurer les données (chemins d’accès aux noeuds) à synchroniser :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur.
1. Accédez à la [console Web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localisez **Apache Sling Distribution Agent - Queue Agents Factory**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifier le nom : **socialpubsync -reverse**

1. Cochez la case **Activé** et enregistrez.
1. Spécifiez les chemins d’accès aux noeuds à répliquer dans **racines autorisées**.
1. Répétez cette opération pour chaque instance **publish**.

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Distribution de granite d&#39;Adobe - Usine d&#39;observation de la diversité {#adobe-granite-distribution-diff-observer-factory}

Cette configuration synchronise l’appartenance au groupe entre les éditeurs.
Si le changement d’appartenance d’un groupe dans un éditeur ne met pas à jour son appartenance sur d’autres éditeurs, assurez-vous que **ref:members** est ajouté à **noms de propriétés affichées**.

Pour assurer la synchronisation des membres :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console Web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localisez **Distribution de granite d&#39;Adobe - Diff Observer Factory**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifier **nom de l&#39;agent : socialpubsync -reverse**.

1. Cochez la case **Activé**.
1. Spécifiez **rep:members** comme description de propertyName dans **noms de propriétés** et Enregistrer.

   ![diff-obs](assets/diff-obs.png)

### Déclencheur de distribution Apache Sling - Fabrique de déclencheurs planifiés {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Cette configuration vous permet de configurer l’intervalle d’interrogation (après lequel les éditeurs sont épinglés et les modifications sont extraites par l’auteur) afin de synchroniser les modifications entre les éditeurs.

L’auteur interroge les éditeurs toutes les 30 secondes (par défaut). Si des packages se trouvent dans le dossier `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, ils sont récupérés et installés sur d&#39;autres éditeurs.

Pour modifier l’intervalle d’interrogation :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la [console Web](/help/sites-deploying/configuring-osgi.md), par exemple [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localisez **Déclencheur de distribution Apache Sling - Triggers Factory planifié**.

   * Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

      Vérifier **socialpubsync -schedule-trigger**

   * Définissez l’intervalle en secondes sur l’intervalle souhaité, puis enregistrez-le.

   ![scheduled-trigger](assets/scheduled-trigger.png)

### Écouteur de synchronisation des utilisateurs AEM Communities {#aem-communities-user-sync-listener}

Pour les problèmes de distribution Sling où il y a une incohérence dans les abonnements et les éléments suivants, vérifiez si les propriétés suivantes dans les configurations **AEM Communities User Sync Listener** sont définies :

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* Dossiers distribués

Pour synchroniser des abonnements, des suivis et des notifications

Sur chaque instance de publication AEM :

1. Connectez-vous avec des droits d’administrateur.
1. Accédez à la [console Web](/help/sites-deploying/configuring-osgi.md). Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Recherchez **Écouteur de synchronisation utilisateur AEM Communities**.
1. Sélectionner la configuration existante à ouvrir pour modification (icône représentant un crayon)

   Vérifier le nom : **socialpubsync -schedule-trigger**

1. Définissez les **NodeTypes** suivants :

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   Les types de noeud spécifiés dans cette propriété vont se synchroniser et les informations de notification (blogs et configurations suivis) sont synchronisées entre les différents éditeurs.

1. Ajoutez tous les dossiers à synchroniser dans **DistributedFolders**. Par exemple,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Définissez **ignorablenodes** sur :

   `.tokens`

   `system`

   `rep:cache` (puisque nous utilisons des sessions collantes, il n’est pas nécessaire de synchroniser ce noeud avec différents éditeurs).

   ![user-sync-listner](assets/user-sync-listner.png)

### Identifiant Sling unique{#unique-sling-id}.

AEM instance d’auteur utilise l’identifiant Sling pour identifier d’où viennent les données et vers quels éditeurs elle doit (ou ne doit pas) renvoyer le package.

Assurez-vous que tous les éditeurs d’une batterie de publication possèdent un identifiant Sling unique. Si l’ID Sling est identique pour plusieurs instances de publication dans une batterie de publication, la synchronisation des utilisateurs échoue. Comme l&#39;auteur ne sait pas où récupérer le pack et où l&#39;installer.

Pour garantir l’identifiant Sling unique des éditeurs dans la batterie de publication, sur chaque instance de publication :

1. Accédez à [https://_hôte:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Vérifiez la valeur de **Sling ID**.

   ![slingid](assets/slingid.png)

   Si l’identifiant Sling d’une instance de publication correspond à l’identifiant Sling d’une autre instance de publication, alors :

1. Arrêtez l’une des instances de publication qui possède un ID Sling correspondant.
1. Dans le répertoire `crx-quickstart/launchpad/felix`, recherchez et supprimez le fichier *sling.id.file.*

   Par exemple, sur un système Linux :

   `rm -i $(find . -type f -name sling.id.file)`

   Par exemple, sur un système Windows :

   Utilisez l&#39;explorateur Windows et recherchez `sling.id.file`

1. Démarrez l’instance de publication. Au démarrage, un nouvel identifiant Sling lui sera attribué.
1. Vérifiez que l&#39;**identifiant Sling** est désormais unique.

Répétez ces étapes jusqu’à ce que toutes les instances de publication aient un identifiant Sling unique.

### Fabrique Vault Package Builder {#vault-package-builder-factory}

Pour que les mises à jour soient synchronisées correctement, il est nécessaire de modifier le créateur de packages en chambre forte pour la synchronisation utilisateur.
Dans `/home/users`, un noeud `*/rep:cache` est créé. Il s&#39;agit d&#39;un cache qui est utilisé pour trouver que si nous requêtes sur le nom principal d&#39;un noeud alors ce cache peut être utilisé directement.

La synchronisation des utilisateurs peut s’arrêter si `rep :cache` noeuds sont synchronisés entre les éditeurs.

Pour vous assurer que les mises à jour sont correctement synchronisées entre les éditeurs, sur chaque instance de publication AEM :

1. Accédez à la [console Web](/help/sites-deploying/configuring-osgi.md)

   Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localisez le **module Apache Sling Distribution Packaging - Vault Package Builder Factory**

   Nom du créateur : socialpubsync-vlt.

1. Sélectionnez l’icône Modifier.
1. Ajoutez deux Filtres de noeud de package :
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Gestion des stratégies
   * Pour remplacer les noeuds rep : policy existants par de nouveaux noeuds, ajoutez un troisième filtre de package : `/home/users|+.*/rep:policy`
   * Pour empêcher la distribution des stratégies, définissez les éléments suivants : `Acl Handling: IGNORE`

   ![Fabrique du générateur de packages Vault](assets/vault-package-builder-factory.png)

## Résolution des problèmes de distribution Sling en AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Si la distribution Sling échoue, essayez les étapes de débogage suivantes :

1. **Vérifier les configurations  [incorrectement ajoutées](/help/sites-administering/sync.md#improperconfig)**

   Assurez-vous que plusieurs configurations ne sont pas ajoutées ou modifiées, mais que les configurations par défaut existantes doivent être modifiées.
1. **Vérifier les configurations**

   Assurez-vous que toutes les [configurations](/help/communities/sync.md#bestpractices) sont correctement définies dans votre instance d’auteur AEM, comme indiqué dans les [Bonnes pratiques](/help/communities/sync.md#main-pars-header-863110628).

1. **Vérifier les autorisations d’utilisateur autorisées**

   Si les packages ne sont pas correctement installés, vérifiez que l&#39;[utilisateur autorisé](/help/sites-administering/sync.md#createauthuser) créé dans la première instance de publication a les listes de contrôle d’accès appropriées.

   Pour valider ce paramètre, au lieu de [créer un utilisateur autorisé](/help/sites-administering/sync.md#createauthuser), modifiez la configuration [Distribution de granit d’Adobe - Fournisseur secret de transport de mot de passe chiffré ](/help/sites-administering/sync.md#adobegraniteencpasswrd) sur l’instance d’auteur afin d’utiliser les informations d’identification d’utilisateur administrateur. Maintenant, essayez de réinstaller les paquets. Si la synchronisation de l’utilisateur fonctionne correctement avec les informations d’identification de l’administrateur, cela signifie que l’utilisateur de publication créé ne disposait pas de listes de contrôle d’accès appropriées.

1. **Vérifier la configuration de l&#39;usine Diff Observer**

   Si seuls des noeuds spécifiques ne sont pas synchronisés dans la batterie de publication (par exemple, les membres du groupe ne sont pas synchronisés), assurez-vous que la configuration [Distribution de granit d&#39;Adobe - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) est activée et **rep: les membres** sont définis dans **noms de propriétés**.

1. **Vérifiez la configuration du module d’écoute AEM Communities User Sync.** Si les utilisateurs créés sont synchronisés mais que les abonnements et les éléments suivants ne fonctionnent pas, assurez-vous que la configuration de l’écouteur de synchronisation utilisateur AEM Communities est compatible :

   * Types de noeud - définis sur **rep:User, nt : unstructured**, **nt : resource**, **rep:ACL**, **sling:Folder** et **sling:OrderedFolder**.
   * Noeuds ignorables : définis sur **.tokens**, **system** et **rep : cache**.
   * Dossiers distribués : définissez les dossiers à distribuer.

1. **Vérifier les journaux générés lors de la création d’utilisateurs sur l’instance de publication**

   Si les configurations ci-dessus sont définies correctement et que la synchronisation des utilisateurs ne fonctionne pas, vérifiez les journaux générés lors de la création des utilisateurs.

   Vérifiez si l’ordre des journaux est le même, comme suit :

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

1. Désactiver la synchronisation des utilisateurs :
1. Sur AEM instance d’auteur, connectez-vous avec les droits d’administrateur.

   1. Accédez à la [console Web](/help/sites-deploying/configuring-osgi.md). Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Recherchez la configuration **Apache Sling Distribution Agent - Sync Agents Factory**.
   1. Décochez la case **Activé**.

      Lors de la désactivation de la synchronisation des utilisateurs sur l’instance d’auteur, les points de terminaison (exportateur et importateur) sont désactivés et l’instance d’auteur est statique. Les packages **vlt** ne sont pas épinglés ou extraits par l&#39;auteur.

      Désormais, si un utilisateur est créé sur l’instance de publication, le package **vlt** est créé dans le noeud */var/sling/distribution/packages/ socialpubsync - vlt /data*. Et si ces paquets sont poussés par l&#39;auteur vers un autre service. Vous pouvez télécharger et extraire ces données pour vérifier quelles propriétés sont transférées à d’autres services.

1. Accédez à un éditeur et créez un utilisateur sur l’éditeur. En conséquence, des événements sont créés.
1. Vérifiez l&#39;[ordre des journaux](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities), créé lors de la création de l&#39;utilisateur.
1. Vérifiez si un package **vlt** est créé sur **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Désormais, activez la synchronisation des utilisateurs sur AEM instance d’auteur.
1. Dans publisher, modifiez les points de terminaison de l’exportateur ou de l’importateur dans **Apache Sling Distribution Agent - Sync Agents Factory**.
Nous pouvons télécharger et extraire des données de package pour vérifier quelles propriétés sont transférées à d’autres éditeurs et quelles données sont perdues.
