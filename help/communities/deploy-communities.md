---
title: Déploiement de Communities
seo-title: Déploiement de Communities
description: Comment déployer AEM Communities
seo-description: Comment déployer AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 4%

---

# Déploiement de Communities {#deploying-communities}

## Prérequis {#prerequisites}

* [Plateforme AEM 6.5](/help/sites-deploying/deploy.md)

* Licence AEM Communities

* Licences facultatives pour :

   * [Fonctionnalités d’Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB pour MSRP](/help/communities/msrp.md)
   * [Adobe Cloud pour ASRP](/help/communities/asrp.md)

## Liste de contrôle d’installation {#installation-checklist}

**Pour la plateforme  [AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* Installez la dernière [AEM mises à jour 6.5](#aem64updates)

* Si vous n’utilisez pas les ports par défaut (4502, 4503), alors [configurez les agents de réplication](#replication-agents-on-author)
* [Réplication de la clé de cryptage](#replicate-the-crypto-key)
* Si vous prenez en charge la mondialisation, [configurez la traduction automatisée](/help/sites-administering/translation.md)
(l’exemple de configuration est fourni pour le développement)

**Pour la fonctionnalité  [Communities](/help/communities/overview.md)**

* Si vous déployez une [ferme de publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifiez l’éditeur Principal](#primary-publisher)

* [Activation du service tunnel](#tunnel-service-on-author)
* [Activation de la connexion sociale](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configuration d’Adobe Analytics](/help/communities/analytics.md)
* Configuration d’un [service de messagerie par défaut](/help/communities/email.md)
* Identifiez le choix pour le [stockage UGC partagé](/help/communities/working-with-srp.md) (**SRP**).

   * Si MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installation et configuration de MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configuration de Solr](/help/communities/solr.md)
      * [Sélectionner MSRP](/help/communities/srp-config.md)
   * Si la base de données relationnelle SRP [(DSRP)](/help/communities/dsrp.md)

      * [Installation du pilote JDBC pour MySQL](#jdbc-driver-for-mysql)
      * [Installation et configuration de MySQL pour DSRP](/help/communities/dsrp-mysql.md)
      * [Configuration de Solr](/help/communities/solr.md)
      * [Sélectionner DSRP](/help/communities/srp-config.md)
   * Si Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Utilisation de votre gestionnaire de compte pour l’approvisionnement
      * [Sélectionner ASRP](/help/communities/srp-config.md)
   * Si JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Magasin UGC non partagé :

         * Le contenu généré par l’utilisateur n’est jamais répliqué.
         * Contenu généré par l’utilisateur visible uniquement sur l’instance AEM ou la grappe dans laquelle il a été saisi

         * La valeur par défaut est JSRP
   Pour la **[fonction d’activation](/help/communities/overview.md#enablement-community)**

   * [Installation et configuration de FFmpeg](/help/communities/ffmpeg.md)
   * [Installation du pilote JDBC pour MySQL](#jdbc-driver-for-mysql)
   * [Installation d’AEM Communities SCORM-Engine](#scorm-package)
   * [Installation et configuration de MySQL pour activation](/help/communities/mysql.md)





## Dernières versions {#latest-releases}

AEM 6.5 Communities GA inclut le package Communities. Pour en savoir plus sur les mises à jour apportées à AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consultez les [Notes de mise à jour d’AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Mises à jour d’AEM version 6.5 {#aem-updates}

À compter de la version 6.4 d’AEM, les mises à jour apportées aux communautés sont fournies dans le cadre d’AEM Cumulative Fix Packs et Service Packs.

Pour connaître les dernières mises à jour d’AEM 6.5, voir [Adobe Experience Manager 6.4 Cumulative Fix Packs et Service Packs](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr).

### Historique des versions {#version-history}

Comme pour AEM 6.4 et versions ultérieures, les fonctionnalités et correctifs d’AEM Communities font partie des packs de correctifs cumulatifs et des Service Packs d’AEM Communities. Il n’existe donc aucun Feature Pack distinct.

### Pilote JDBC pour MySQL {#jdbc-driver-for-mysql}

Deux fonctionnalités de Communities utilisent une base de données MySQL :

* Pour [enablement](/help/communities/enablement.md) : enregistrement des activités SCORM et des apprenants
* Pour [DSRP](/help/communities/dsrp.md) : stockage du contenu généré par l’utilisateur

Le connecteur MySQL doit être obtenu et installé séparément.

Les étapes nécessaires sont les suivantes :

1. Téléchargez l’archive ZIP à partir de [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La version doit être >= 5.1.38

1. Extrayez mysql-connector-java-&lt;version>-bin.jar (lot) de l’archive.
1. Utilisez la console web pour installer et démarrer le lot :

   * Par exemple, https://localhost:4502/system/console/bundles
   * Sélectionner **`Install/Update`**
   * Parcourir.. pour sélectionner le lot extrait de l’archive ZIP téléchargée
   * Vérifiez que *le pilote JDBC d’Oracle Corporation pour MySQLcom.mysql.jdbc* est principal et démarrez-le dans le cas contraire (ou vérifiez les journaux).

1. Si vous effectuez l’installation sur un déploiement existant après la configuration de JDBC, replacez JDBC sur le nouveau connecteur en réenregistrant la configuration JDBC à partir de la console web :
   * Par exemple, https://localhost:4502/system/console/configMgr
   * Localisation de la configuration `Day Commons JDBC Connections Pool`
   * Sélectionner pour ouvrir
   * Sélectionner `Save`

1. Répétez les étapes 3 et 4 sur toutes les instances d’auteur et de publication.

Vous trouverez plus d’informations sur l’installation des lots sur la page [Console web](/help/sites-deploying/web-console.md).

#### Exemple : Bundle MySQL Connector installé {#example-installed-mysql-connector-bundle}

![connector-bundle](assets/connector-bundle.png)

### Package SCORM {#scorm-package}

SCORM (Share Content Object Reference Model) est un ensemble de normes et de spécifications pour l’apprentissage en ligne. SCORM définit également la manière dont le contenu peut être compressé dans un fichier ZIP transférable.

Le moteur SCORM AEM Communities est requis pour la fonction [activation](/help/communities/overview.md#enablement-community) . Packages de notation pris en charge sur AEM 6.5 Communities :

* [cq-social-scorm-package, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) qui comprend le moteur  [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Pour installer un package SCORM**

1. Installez le [cq-social-scorm-package, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) à partir du partage de modules.
1. Téléchargez `/libs/social/config/scorm/database_scormengine_data.sql` à partir de l’instance cq et exécutez-la dans le serveur mysql pour créer un schéma scormEngineDB mis à niveau.
1. Ajoutez `/content/communities/scorm/RecordResults` dans la propriété Chemins exclus du filtre CSRF `https://<hostname>:<port>/system/console/configMgr` sur les éditeurs.


#### Journalisation SCORM {#scorm-logging}

Lors de l’installation, toutes les activités d’activation sont généreusement consignées dans la console système.

Si vous le souhaitez, le niveau de journal peut être défini sur WARN pour le package `RusticiSoftware.*`.

Pour utiliser les journaux, voir [Utilisation des enregistrements d’audit et des fichiers journaux](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### AEM MLS avancé {#aem-advanced-mls}

Pour que la collection SRP (MSRP ou DSRP) prenne en charge la recherche multilingue avancée (MLS), de nouveaux modules externes Solr sont requis en plus d’un schéma personnalisé et d’une configuration Solr. Tous les éléments requis sont compressés dans un fichier ZIP téléchargeable.

Le téléchargement MLS avancé (également appelé &quot;phasetwo&quot;) est disponible à partir du référentiel Adobe :

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * Version 1.2.40, 6 avril 2016
   * Téléchargez AEM-SOLR-MLS-phasetwo-1.2.40.zip

Pour plus d’informations sur l’installation, voir [Configuration Solr](/help/communities/solr.md) pour SRP.

### À propos des liens vers le partage de modules {#about-links-to-package-share}

**Modules visibles dans Adobe AEM Cloud**

Les liens vers les modules de cette page ne nécessitent aucune instance d’AEM en cours d’exécution, car ils sont destinés à un partage de modules sur `adobeaemcloud.com`. Bien que les packages soient visibles, le bouton `Install` permet d’installer les packages sur un site hébergé par Adobe. Si vous envisagez d’installer sur une instance d’AEM locale, la sélection de `Install` entraînera une erreur.

**Installation sur une instance d’AEM locale**

Pour installer les packages visibles dans `adobeaemcloud.com` sur une instance d’AEM locale, le package doit d’abord être téléchargé sur un disque local :

* Sélectionnez l’onglet **Ressources**
* Sélectionnez **télécharger sur le disque**

Sur l’instance d’AEM locale, utilisez le gestionnaire de modules (par exemple [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) pour charger le fichier dans le référentiel de modules AEM local.

Vous pouvez également accéder au package à l’aide du partage de package à partir de l’instance AEM locale (par exemple, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)). Le bouton `Download` est téléchargé vers le référentiel de package de l’instance AEM locale.

Une fois que vous êtes dans le référentiel de package de l’instance d’AEM locale, utilisez le gestionnaire de packages pour installer le package.

Pour plus d’informations, voir [Comment utiliser les packages](/help/sites-administering/package-manager.md#package-share).

## Déploiements recommandés {#recommended-deployments}

Dans AEM Communities, un magasin commun est utilisé pour stocker le contenu généré par l’utilisateur et est souvent appelé [fournisseur de ressources de stockage (SRP)](/help/communities/working-with-srp.md). Le déploiement recommandé consiste à choisir une option SRP pour le magasin commun.

Le magasin commun prend en charge la modération et l’analyse du contenu créé par l’utilisateur dans l’environnement de publication, tout en éliminant la nécessité de [réplication](/help/communities/sync.md) du contenu créé par l’utilisateur.

* [Community Content Store](/help/communities/working-with-srp.md)  : présente les options de stockage SRP pour les communautés AEM

* [Topologies](/help/communities/topologies.md)  recommandées : aborde la topologie à utiliser en fonction du cas d’utilisation et du choix de la SRP.

## Mise à niveau {#upgrading}

Lors de la mise à niveau vers la plateforme AEM 6.5 à partir des versions précédentes d’AEM, il est important de lire [Mise à niveau vers la version 6.5](/help/sites-deploying/upgrade.md) d’Adobe.

Outre la mise à niveau de la plateforme, consultez la section [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md) pour en savoir plus sur les modifications apportées aux communautés.

## Configurations {#configurations}

### Éditeur Principal {#primary-publisher}

Lorsque le déploiement choisi est une [ferme de publication](/help/communities/topologies.md#tarmk-publish-farm), une instance de publication AEM doit être identifiée comme **`primary publisher`** pour les activités qui ne doivent pas se produire sur toutes les instances, telles que les fonctionnalités qui reposent sur les **notifications** ou **Adobe Analytics**.

Par défaut, la configuration OSGi `AEM Communities Publisher Configuration` est configurée avec la case à cocher **`Primary Publisher`** cochée, de sorte que toutes les instances de publication dans une batterie de publication s’identifient elles-mêmes comme Principales.

Par conséquent, il est nécessaire de **modifier la configuration sur toutes les instances de publication secondaires** pour décocher la case **`Primary Publisher`**.

![Principal éditeur](assets/primary-publisher.png)

Pour toutes les autres instances de publication (secondaires) dans une ferme de publication :

* Connexion avec droits d’administrateur
* Accédez à la [console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Recherchez le `AEM Communities Publisher Configuration`
* Sélectionner l’icône de modification
* Décochez la case **Principal Publisher**
* Sélectionnez **Enregistrer**

### Agents de réplication sur l’auteur {#replication-agents-on-author}

La réplication est utilisée pour le contenu du site créé dans l’environnement de publication, comme les groupes de communautés, ainsi que pour la gestion des membres et des groupes de membres de l’environnement de création à l’aide du [service tunnel](#tunnel-service-on-author).

Pour l’éditeur Principal, assurez-vous que la [configuration de l’agent de réplication](/help/sites-deploying/replication.md) identifie correctement le serveur de publication et l’utilisateur autorisé. L’utilisateur autorisé par défaut, `admin,`, dispose déjà des autorisations appropriées (est membre de `Communities Administrators`).

Pour que certains autres utilisateurs disposent des autorisations appropriées, ils doivent être ajoutés en tant que membres au groupe d’utilisateurs `administrators` (également membre de `Communities Administrators`).

Il existe deux agents de réplication dans l’environnement de création qui ont besoin que la configuration du transport soit correctement configurée.

* Accès à la console de réplication sur l’auteur

   * Dans la navigation globale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]** > **[!UICONTROL Agents sur l’auteur]**

* Suivez la même procédure pour les deux agents :

   * **Agent par défaut (publication)**
   * **Agent de réplication inverse (publication inversée)**

      1. Sélectionner l’agent
      1. Sélectionnez **edit**
      1. Sélectionnez l’onglet **Transport**
      1. Si le port n’est pas `4503`, modifiez l’**URI** pour spécifier le port approprié.

      1. Si l’utilisateur n’est pas `admin`, modifiez les **Utilisateur** et **Mot de passe** pour spécifier un membre du groupe d’utilisateurs `administrators`.

Les images suivantes montrent les résultats du changement de port de 4503 à 6103 en :

#### Agent par défaut (publication) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Agent de réplication inverse (publication inversée) {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### Service Tunnel sur l’auteur {#tunnel-service-on-author}

Lorsque vous utilisez l’environnement de création pour [créer des sites](/help/communities/sites-console.md), [modifier les propriétés du site](/help/communities/sites-console.md#modifying-site-properties) ou [gérer les membres de la communauté](/help/communities/members.md), il est nécessaire d’accéder aux membres (utilisateurs) enregistrés dans l’environnement de publication, et non aux utilisateurs enregistrés dans l’environnement de création.

Le service tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

Pour activer le service tunnel :

* Connectez-vous avec les privilèges d’administrateur sur votre instance de création.
* Si l’éditeur n’est pas localhost:4503 ou que l’utilisateur du transport n’est pas `admin`,
ensuite [configurer l’agent de réplication](#replication-agents-on-author)

* Accédez à la [console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Recherchez le `AEM Communities Publish Tunnel Service`
* Sélectionner l’icône de modification
* Cochez la case **enable**
* Sélectionnez **Enregistrer**

   ![tunnel-service](assets/tunnel-service.png)

### Répliquer la clé de chiffrement {#replicate-the-crypto-key}

Il existe deux fonctionnalités d’AEM Communities qui nécessitent que toutes les instances AEM serveur utilisent les mêmes clés de chiffrement. Il s’agit de [Analytics](/help/communities/analytics.md) et [ASRP](/help/communities/asrp.md).

À partir de la version 6.3 d’AEM, le matériel clé est stocké dans le système de fichiers et ne figure plus dans le référentiel.

Pour copier les documents clés de l’auteur vers toutes les autres instances, il est nécessaire de :

* Accédez à l’instance d’AEM, généralement une instance d’auteur, qui contient le matériel clé à copier.

   * Localisez le lot `com.adobe.granite.crypto.file` dans le système de fichiers local,
par exemple,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * Le fichier `bundle.info` identifie le lot.
   * Naviguez dans le dossier data,
par exemple,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copiez les fichiers hmac et de noeud Principal.


* Pour chaque instance AEM cible

   * Naviguez dans le dossier data,
par exemple,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Coller les 2 fichiers précédemment copiés
   * Il est nécessaire d’[actualiser le lot Granite Crypto](#refresh-the-granite-crypto-bundle) si l’instance AEM cible est en cours d’exécution.


>[!CAUTION]
>
>Si une autre fonctionnalité de sécurité a déjà été configurée basée sur les clés de cryptage, la réplication des clés de cryptage peut endommager la configuration. Pour obtenir de l’aide, [contactez l’assistance clientèle](https://helpx.adobe.com/fr/marketing-cloud/contact-support.html).

#### Réplication du référentiel {#repository-replication}

Le fait que le matériel clé soit stocké dans le référentiel, comme c’était le cas pour AEM version 6.2 et antérieure, peut être conservé en spécifiant la propriété système suivante au premier démarrage de chaque instance AEM (qui crée le référentiel initial) :

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>Il est important de vérifier que l’agent de réplication [sur author](#replication-agents-on-author) est correctement configuré.

Avec le matériel clé stocké dans le référentiel, la manière de répliquer la clé de chiffrement de l’auteur vers d’autres instances est la suivante :

Utilisation de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Accédez à [https://&lt;serveur>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Sélectionner `/etc/key`
* Ouvrir l’onglet `Replication`
* Sélectionner `Replicate`

* [Actualisation du lot Crypto Granite](#refresh-the-granite-crypto-bundle)

   ![replicare-repository](assets/replicare-repository.png)

#### Actualisez le lot de chiffrement Granite {#refresh-the-granite-crypto-bundle}

* Sur chaque instance de publication, accédez à la [console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple, [https://&lt;serveur>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Localisez le lot `Adobe Granite Crypto Support` (com.adobe.granite.crypto)
* Sélectionnez **Actualiser**

   ![granite-crypto](assets/granite-crypto.png)

* Après un moment, une boîte de dialogue **Succès** doit s’afficher :
   `Operation completed successfully.`

### Serveur HTTP Apache {#apache-http-server}

Si vous utilisez le serveur Apache HTTP, veillez à utiliser le nom de serveur correct pour toutes les entrées pertinentes.

En particulier, veillez à utiliser le nom de serveur correct, et non `localhost`, dans la balise `RedirectMatch`.

#### Exemple httpd.conf {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Si vous utilisez un Dispatcher, voir :

* Documentation AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)
* [Installation de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configuration de Dispatcher pour Communities](/help/communities/dispatcher.md)
* [Problèmes connus](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentation sur les communautés associée {#related-communities-documentation}

* Reportez-vous à la section [Administration des sites de communauté](/help/communities/administer-landing.md) pour en savoir plus sur la création d’un site de communauté, la configuration de modèles de sites de communauté, la modération du contenu de communauté, la gestion des membres et la configuration de la messagerie.

* Visitez [Développement de communautés](/help/communities/communities.md) pour en savoir plus sur la structure de composants sociaux (SCF) et la personnalisation des composants et fonctionnalités de communautés.

* Consultez la section [Création de composants de communautés](/help/communities/author-communities.md) pour savoir comment créer et configurer des composants de communautés.
