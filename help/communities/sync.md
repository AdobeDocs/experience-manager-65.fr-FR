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
translation-type: tm+mt
source-git-commit: acc758b83486e8c623e31bb4a68f3c29dd4848ba

---


# Synchronisation des utilisateurs des communautés {#communities-user-synchronization}

## Présentation {#introduction}

Dans les communautés AEM, à partir du  de publication  (en fonction des autorisations configurées), les *de* site peuvent devenir *membres*, créer des groupes *d’* utilisateurs et modifier leur *demembres.*

*Les données* utilisateur sont un terme utilisé pour faire référence aux *utilisateurs*, aux  *utilisateurs* et aux groupes *d’* utilisateurs.

*Les membres* sont un terme utilisé pour désigner les *utilisateurs* enregistrés dans le  de publication , par opposition aux utilisateurs enregistrés dans le de l’auteur.

Pour plus d’informations sur les données utilisateur, consultez [Gestion des utilisateurs et des groupes](/help/communities/users.md)d’utilisateurs.

## Synchronisation des utilisateurs dans une batterie de publication {#synchronizing-users-across-a-publish-farm}

Par conception, les données utilisateur créées dans le  de publication  n’apparaissent pas dans le de l’auteur .

La plupart des données utilisateur créées dans le de  de l’auteur  sont destinées à rester dans le de l’auteur et ne sont ni synchronisées ni répliquées dans les instances de publication.

Lorsque la [topologie](/help/communities/topologies.md) est une batterie [](/help/sites-deploying/recommended-deploys.md#tarmk-farm)de publication, l’enregistrement et les modifications effectuées sur une instance de publication doivent être synchronisés avec d’autres instances de publication. Les membres doivent pouvoir se connecter et voir leurs données sur n’importe quel noeud de publication.

Lorsque la synchronisation des utilisateurs est activée, les données utilisateur sont automatiquement synchronisées dans les instances de publication de la batterie.

### Instructions de configuration de la synchronisation des utilisateurs {#user-sync-setup-instructions}

Pour obtenir des instructions détaillées, étape par étape, sur la manière d’activer la synchronisation sur une batterie de publication, voir :

* [Synchronisation des utilisateurs](/help/sites-administering/sync.md)

## Synchronisation utilisateur en arrière-plan {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **package vlt**

   Il s’agit d’un fichier zip de toutes les modifications effectuées sur un éditeur, qui doit être distribué entre les éditeurs. Les modifications effectuées sur un éditeur génèrent des  qui sont sélectionnées par l’écouteur de  de modification. Cela crée un package vlt qui contient toutes les modifications.

* **module de distribution**

   Il contient des informations de distribution pour Sling. Il s&#39;agit d&#39;informations sur l&#39;endroit où le contenu doit être distribué, et le moment où il a été distribué en dernier.

## What Happens When ... {#what-happens-when}

### Publier le site à partir de la console Sites des communautés {#publish-site-from-communities-sites-console}

Sur l’auteur, lorsqu’un site communautaire est publié à partir de la console [Sites](/help/communities/sites-console.md)des communautés, l’effet est de [reproduire](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) les pages associées, et Sling distribue les groupes d’utilisateurs communautaires créés dynamiquement, y compris leur adhésion.

### L’utilisateur est créé ou modifie le lors de la publication. {#user-is-created-or-edits-profile-on-publish}

Par conception, les utilisateurs et les  de créés dans le de publication  (par exemple par auto-inscription, connexion sociale, authentification LDAP) n’apparaissent pas dans le de l’auteur.

When the topology is a [publish farm](/help/communities/topologies.md) and user sync has been correctly configured, the *user* and *user profile* is synchronized across the publish farm using Sling distribution.

### Un nouveau groupe de communautés est créé lors de la publication. {#new-community-group-is-created-on-publish}

Bien qu’elle ait été lancée à partir d’une instance de publication, la création d’un groupe de communautés, qui se traduit par de nouvelles pages du site et un nouveau groupe d’utilisateurs, se produit en fait sur l’instance d’auteur.

Dans le cadre du processus, les nouvelles pages du site sont répliquées sur toutes les instances de publication. Le groupe d’utilisateurs de la communauté créé dynamiquement et ses membres sont distribués Sling à toutes les instances de publication.

### Les utilisateurs ou les groupes d’utilisateurs sont créés à l’aide de la console Sécurité.{#users-or-user-groups-are-created-using-security-console}

Par défaut, les données utilisateur créées dans l’environnement de publication ne sont pas visibles dans l’environnement de création, et vice versa.

Lorsque la console [Administration et sécurité des utilisateurs](/help/sites-administering/security.md) est utilisée pour ajouter de nouveaux utilisateurs dans l’environnement de publication, la synchronisation des utilisateurs synchronise les nouveaux utilisateurs et leur appartenance à un groupe sur d’autres instances de publication, si nécessaire. La synchronisation des utilisateurs synchronise également les groupes d’utilisateurs créés via la console de sécurité.

### L’utilisateur publie du contenu lors de la publication {#user-posts-content-on-publish}

Pour le contenu généré par l’utilisateur (UGC), les données saisies sur une instance de publication sont accessibles via le SRP [](/help/communities/srp-config.md)configuré.

## Bonnes pratiques {#bestpractices}

Par défaut, la synchronisation des utilisateurs est **désactivée**. Activer la synchronisation des utilisateurs implique de modifier les configurations OSGi *existantes.* Aucune configuration nouvelle ne doit être ajoutée suite à l’activation de la synchronisation des utilisateurs.

La synchronisation des utilisateurs repose sur l’environnement de création pour gérer les distributions de données utilisateur, même si les données utilisateur ne sont pas créées en mode de création.

**Conditions préalables**

1. Si les utilisateurs et les groupes d’utilisateurs ont déjà été créés sur un éditeur, il est recommandé de [synchroniser manuellement](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) les données utilisateur sur tous les éditeurs avant de configurer et d’activer la synchronisation des utilisateurs.

   Une fois la synchronisation des utilisateurs activée, seuls les utilisateurs et les groupes nouvellement créés sont synchronisés .

1. Vérifiez que le code le plus récent a été installé :

   * [Mise à jour de la plateforme AEM](https://helpx.adobe.com/fr/experience-manager/kb/aem62-available-hotfixes.html)
   * [Mises à jour d’AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Les configurations suivantes sont nécessaires pour activer la synchronisation des utilisateurs sur les communautés AEM. Assurez-vous que ces configurations sont correctes pour empêcher l’échec de la distribution de contenu sling.

### Agent de distribution Apache Sling - Fabrique d’agents de synchronisation {#apache-sling-distribution-agent-sync-agents-factory}

Cette configuration récupère le contenu à synchroniser entre les éditeurs. La configuration se trouve sur l’instance d’auteur. L&#39;auteur doit suivre tous les éditeurs qui sont là et où synchroniser toutes les informations.

Les valeurs par défaut dans la configuration sont pour une instance de publication unique. La synchronisation utilisateur s’avère utile pour synchroniser plusieurs instances de publication, comme pour une batterie de publication, d’autres instances de publication doivent être ajoutées à la configuration.

**Comment le contenu est-il synchronisé ?**

L’instance d’auteur ping le point de fin d’exportation des éditeurs. Chaque fois qu’un utilisateur est créé ou mis à jour sur des éditeurs spécifiques (n), l’auteur obtient le contenu à partir de ses points de fin d’exportation et [envoie le contenu](/help/communities/sync.md#main-pars-image-1413756164) à d’autres éditeurs (n-1, à l’exception des éditeurs dont le contenu est récupéré).

Pour configurer la configuration des agents de synchronisation Apache Sling :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html). For example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Locate **Apache Sling Distribution Agent - Sync Agents Factory**.

   * Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

      Vérifier le nom : **socialpubsync.**

   * Select the **Enabled** checkbox.
   * Sélectionnez **Utiliser plusieurs files d’attente.**
   * Spécifiez les points **de fin** Exporter et les points **de fin** Importateur (vous pouvez ajouter d’autres points de fin Exporter et Importer).

      Ces points de fin définissent l’emplacement d’où vous souhaitez obtenir le contenu et l’emplacement où vous souhaitez pousser le contenu. L’auteur récupère le contenu à partir du point de terminaison de l’exportateur spécifié et le transmet aux éditeurs (autres que l’éditeur à partir duquel il a récupéré le contenu).
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Distribution Adobe Granite - Fournisseur secret du transport de mot de passe chiffré {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Il permet à l’auteur d’identifier l’utilisateur autorisé, comme ayant l’autorisation de synchroniser les données utilisateur de l’auteur à la publication.

L’utilisateur [autorisé créé](/help/sites-administering/sync.md#createauthuser) sur toutes les instances de publication aide les éditeurs à se connecter à l’auteur et à configurer la distribution Sling sur l’auteur. Cet utilisateur autorisé dispose de toutes les [listes de contrôle d’accès](/help/sites-administering/sync.md#howtoaddacl)requises.

Chaque fois que des données doivent être installées ou extraites des éditeurs, l’auteur se connecte aux éditeurs à l’aide des informations d’identification (nom d’utilisateur et mot de passe) définies dans cette configuration.

Pour connecter l’auteur aux éditeurs à l’aide d’un utilisateur autorisé :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md).

   For example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Locate **Adobe Granite Distribution - Encrypted Password Transport Secret Provider.**
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifiez la propriété **socialpubsync** - **publishUser.**

1. Définissez le nom d’utilisateur et le mot de passe sur l’utilisateur [](/help/sites-administering/sync.md#createauthorizeduser)autorisé.

   Par exemple, **usersync - admin**

![granit-pâle-trans](assets/granite-paswrd-trans.png)

### Agent de distribution Apache Sling - Fabrique d’agents de file d’attente {#apache-sling-distribution-agent-queue-agents-factory}

Cette configuration permet de configurer les données à synchroniser entre les éditeurs. Lorsque des données sont créées/mises à jour dans les chemins spécifiés dans les racines **** autorisées, &quot;var/community/distribution/diff&quot; est activé et le réplicateur créé récupère les données d’un éditeur et les installe sur d’autres éditeurs.

Pour configurer les données (chemins d’accès aux noeuds) à synchroniser :

1. Connectez-vous avec des droits d’administrateur sur votre instance d’auteur.
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Locate **Apache Sling Distribution Agent - Queue Agents Factory**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifier le nom : **socialpubsync -reverse**

1. Cochez la case **Activé** et enregistrez.
1. Spécifiez les chemins de noeud à répliquer dans les racines **** autorisées.
1. Repeat for each **publish** instance.

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

Cette configuration synchronise l’appartenance au groupe entre les éditeurs.
Si le changement d’appartenance d’un groupe dans un éditeur ne met pas à jour son appartenance sur d’autres éditeurs, assurez-vous que **ref:members** est ajouté aux noms **de propriétés** affichées.

Pour assurer la synchronisation des membres :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Locate **Adobe Granite Distribution - Diff Observer Factory**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

   Vérifier le nom **de l&#39;agent : socialpubsync -reverse**.

1. Select the **Enabled** checkbox.
1. Spécifiez **rep:members** comme description de propertyName dans les noms **de propriétés** recherchées et Enregistrer.

   ![diff-obs](assets/diff-obs.png)

### Déclencheur de distribution Apache Sling - Fabrique de déclencheurs planifiés {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Cette configuration vous permet de configurer l’intervalle d’interrogation (après lequel les éditeurs sont épinglés et les modifications sont extraites par l’auteur) afin de synchroniser les modifications entre éditeurs.

L’auteur interroge les éditeurs toutes les 30 secondes (par défaut). Si des packages sont présents dans le dossier `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, ils seront récupérés et installés sur d’autres éditeurs.

Pour modifier l’intervalle d’interrogation :

1. Connectez-vous avec les droits d’administrateur sur votre instance d’auteur AEM.
1. Accédez à la console [](/help/sites-deploying/configuring-osgi.md)Web, par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Locate **Apache Sling Distribution Trigger - Scheduled Triggers Factory**

   * Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon).

      Vérifier **socialpubsync -schedule-trigger**

   * Définissez l’intervalle en secondes sur l’intervalle souhaité, puis enregistrez.
   ![scheduled-trigger](assets/scheduled-trigger.png)

### Écouteur de synchronisation des utilisateurs AEM Communities {#aem-communities-user-sync-listener}

Pour les problèmes de distribution Sling où il existe une incohérence dans   et les éléments suivants, vérifiez si les propriétés suivantes sont définies dans les configurations du module d’écoute **de synchronisation des utilisateurs d’** AEM Communities :

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

Pour synchroniser  , suivre et notifications

Sur chaque instance de publication AEM :

1. Connectez-vous avec des droits d’administrateur.
1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md). For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Locate **AEM Communities User Sync Listener**.
1. Sélectionnez la configuration existante à ouvrir pour modification (icône représentant un crayon)

   Vérifier le nom : **socialpubsync -schedule-trigger**

1. Définissez les types de **noeud** suivants :

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   Les types de noeud spécifiés dans cette propriété seront synchronisés et les informations de notification (blogs et configurations suivis) sont synchronisées entre les différents éditeurs.

1. Ajouter tous les dossiers à synchroniser dans **DistributedFolders**. Par exemple :

   `segments/scoring`

   `social/relationships`

   `activities`

1. Définissez les modes **ignare** sur :

   `.tokens`

   `system`

   `rep:cache` (puisque nous utilisons des sessions collantes, il n’est pas nécessaire de synchroniser ce noeud avec d’autres éditeurs).

   ![user-sync-listner](assets/user-sync-listner.png)

### Identifiant Sling unique{#unique-sling-id}.

L’instance d’auteur AEM utilise l’identifiant Sling pour identifier l’emplacement d’arrivée des données et vers quels éditeurs elle doit (ou ne doit pas) renvoyer le package.

Assurez-vous que tous les éditeurs d’une batterie de publication possèdent un identifiant Sling unique. Si l’ID Sling est le même pour plusieurs instances de publication dans une batterie de publication, la synchronisation des utilisateurs échoue. Comme l&#39;auteur ne saura pas où récupérer le paquet et où l&#39;installer.

Pour garantir l’identifiant Sling unique des éditeurs dans la batterie de publication, sur chaque instance de publication :

1. Browse to [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Check the value of **Sling ID**.

   ![slingid](assets/slingid.png)

   Si l’identifiant Sling d’une instance de publication correspond à l’identifiant Sling d’une autre instance de publication, alors :

1. Arrêtez l’une des instances de publication qui possède un ID Sling correspondant.
1. Dans le `crx-quickstart/launchpad/felix` répertoire, recherchez et supprimez le fichier nommé *sling.id.file.*

   Par exemple, sur un système Linux :

   `rm -i $(find . -type f -name sling.id.file)`

   Par exemple, sur un système Windows :

   Utilisez l’explorateur Windows et recherchez `sling.id.file`

1. Démarrez l’instance de publication. Au démarrage, un nouvel identifiant Sling lui sera attribué.
1. Validate that the **Sling ID** is now unique.

Répétez ces étapes jusqu’à ce que toutes les instances de publication aient un identifiant Sling unique.

### Fabrique Vault Package Builder {#vault-package-builder-factory}

Pour que les mises à jour soient correctement synchronisées, il est nécessaire de modifier le créateur de packages de chambre forte pour la synchronisation utilisateur.
Dans `/home/users`, un `*/rep:cache` noeud est créé. Il s&#39;agit d&#39;un cache qui est utilisé pour trouver que si nous  sur le nom principal d&#39;un noeud, ce cache peut être utilisé directement.

La synchronisation des utilisateurs peut s’arrêter si `rep :cache` les noeuds sont synchronisés entre les éditeurs.

Pour vous assurer que les mises à jour sont correctement synchronisées entre les éditeurs, sur chaque instance de publication AEM :

1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md)

   For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Locate the **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   Nom du créateur : socialpubsync-vlt.

1. Sélectionnez l’icône Modifier.
1. Ajouter deux de noeud de package  :
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Gestion des stratégies
   * To overwrite existing rep :policy nodes with new ones, add a third Package Filter: `/home/users|+.*/rep:policy`
   * To prevent policies from being distributed, set: `Acl Handling: IGNORE`
   ![Fabrique du générateur de packages Vault](assets/vault-package-builder-factory.png)

## Résolution des problèmes de distribution Sling dans les communautés AEM {#troubleshoot-sling-distribution-in-aem-communities}

Si la distribution Sling échoue, procédez comme suit pour le débogage :

1. **Vérifier les configurations[mal ajoutées](/help/sites-administering/sync.md#improperconfig)**

   Assurez-vous que plusieurs configurations ne sont pas ajoutées ou modifiées, mais que les configurations par défaut existantes doivent être modifiées.
1. **Vérifier les configurations**

   Assurez-vous que toutes les [configurations](/help/communities/sync.md#bestpractices) sont correctement définies dans votre instance d’auteur AEM, comme indiqué dans les [bonnes pratiques](/help/communities/sync.md#main-pars-header-863110628).

1. **Vérifier les autorisations d’utilisateur autorisées**

   Si les packages ne sont pas correctement installés, vérifiez que l’utilisateur [](/help/sites-administering/sync.md#createauthuser) autorisé créé dans la première instance de publication dispose des listes de contrôle d’accès appropriées.

   Pour valider ce paramètre, au lieu de l’utilisateur [autorisé](/help/sites-administering/sync.md#createauthuser) créé, modifiez la configuration du fournisseur [secret de transport de mot de passe chiffré d’](/help/sites-administering/sync.md#adobegraniteencpasswrd) Adobe Granite Distribution - Encrypted Password sur l’instance d’auteur afin d’utiliser les informations d’identification de l’utilisateur administrateur. Maintenant, essayez de réinstaller les paquets. Si la synchronisation de l’utilisateur fonctionne correctement avec les informations d’identification de l’administrateur, cela signifie que l’utilisateur de publication créé ne disposait pas des listes de contrôle d’accès appropriées.

1. **Vérification de la configuration de l’usine Diff Observer**

   Si seuls des noeuds spécifiques ne sont pas synchronisés dans la batterie de publication (par exemple, les membres du groupe ne sont pas synchronisés), assurez-vous que la configuration [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) est activée et **rep : les membres** sont définis dans les noms **des propriétés** affichées.

1. **Vérifiez la configuration de l’écouteur de synchronisation des utilisateurs AEM Communities.** Si les utilisateurs créés sont synchronisés mais que   et les éléments suivants ne fonctionnent pas, assurez-vous que la configuration de l’écouteur de synchronisation des utilisateurs AEM Communities User Sync a :

   * Types de noeud : définis sur **rep:User, pas :unstructured**, **pas :resource**, **rep:ACL**, **sling:Folder et sling:OrderedFolder.******
   * Noeuds ignorables - défini sur **.tokens**, **system** et **rep:cache**.
   * Dossiers distribués : définissez les dossiers à distribuer.

1. **Vérifier les journaux générés lors de la création de l’utilisateur sur l’instance de publication**

   Si les configurations ci-dessus sont définies correctement et que la synchronisation de l’utilisateur ne fonctionne pas, vérifiez les journaux générés lors de la création de l’utilisateur.

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
1. Sur l’instance d’auteur AEM, connectez-vous avec des droits d’administrateur.

   1. Access the [Web Console](/help/sites-deploying/configuring-osgi.md). For example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Locate the configuration **Apache Sling Distribution Agent - Sync Agents Factory**.
   1. Désélectionnez la case **Activé** .

      Lors de la désactivation de la synchronisation de l’utilisateur sur l’instance d’auteur, les points de fin (exportateur et importateur) sont désactivés et l’instance d’auteur est statique. Les paquets **vlt** ne sont pas épinglés ni récupérés par l&#39;auteur.

      Désormais, si un utilisateur est créé sur une instance de publication, le package **vlt** est créé dans le noeud */var/sling/distribution/packages/ socialpubsync - vlt /data* . Et si ces paquets sont poussés par l&#39;auteur vers un autre service. Vous pouvez télécharger et extraire ces données pour vérifier quelles propriétés sont transférées à d’autres services.

1. Accédez à un éditeur et créez un utilisateur sur l’éditeur. En conséquence, des  sont créées.
1. Vérifiez l’ [ordre des journaux](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)créés lors de la création des utilisateurs.
1. Vérifiez si un package **vlt** est créé sur **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. Activez maintenant la synchronisation de l’utilisateur sur l’instance d’auteur AEM.
1. Sur publisher, modifiez les points de fin d’exportateur ou d’importateur dans **Apache Sling Distribution Agent - Sync Agents Factory**.
Nous pouvons télécharger et extraire des données de package pour vérifier quelles propriétés sont transférées à d’autres éditeurs et quelles données sont perdues.
