---
title: Déploiement de Communities
seo-title: Déploiement de Communities
description: Comment déployer les communautés AEM
seo-description: Comment déployer les communautés AEM
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Déploiement de Communities{#deploying-communities}

## Conditions préalables {#prerequisites}

* [Plateforme AEM 6.5](/help/sites-deploying/deploy.md)

* Licence Communautés AEM

* Licences facultatives pour :

   * [Fonctionnalités d’Adobe Analytics pour les communautés](/help/communities/analytics.md)
   * [MongoDB pour MSRP](/help/communities/msrp.md)
   * [Adobe Cloud pour ASRP](/help/communities/asrp.md)

## Liste de contrôle d&#39;installation {#installation-checklist}

**Pour la plateforme[AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* installer les dernières mises à jour [AEM 6.5](#aem64updates)

* si vous n&#39;utilisez pas les ports par défaut (4502, 4503), [configurez les agents de réplication](#replication-agents-on-author)
* [répliquer la clé de chiffrement](#replicate-the-crypto-key)
* en cas de prise en charge de la mondialisation, [configuration de la traduction](/help/sites-administering/translation.md)automatisée (configuration d’exemple fournie pour le développement)

**Pour la fonctionnalité[Communautés](/help/communities/overview.md)**

* si vous déployez une batterie de [publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifiez l’éditeur principal](#primary-publisher)

* [activer le service tunnel](#tunnel-service-on-author)
* [activer la connexion sociale](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [configuration d’Adobe Analytics](/help/communities/analytics.md)
* configuration d’un service de messagerie [par défaut](/help/communities/email.md)
* identifier le choix pour le stockage [UGC](/help/communities/working-with-srp.md) partagé (**SRP**)

   * if MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [installation et configuration de MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [configurer Solr](/help/communities/solr.md)
      * [sélectionner MSRP](/help/communities/srp-config.md)
   * si SRP de base de données relationnelle [(DSRP)](/help/communities/dsrp.md)

      * [installation du pilote JDBC pour MySQL ;](#jdbc-driver-for-mysql)
      * [installation et configuration de MySQL pour DSRP](/help/communities/dsrp-mysql.md)
      * [configurer Solr](/help/communities/solr.md)
      * [sélectionner DSRP](/help/communities/srp-config.md)
   * si Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * travailler avec votre gestionnaire de compte pour l’approvisionnement
      * [sélectionner ASRP](/help/communities/srp-config.md)
   * if JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * pas un magasin UGC partagé :

         * UGC n’est jamais répliqué
         * UGC uniquement visible sur l’instance ou la grappe AEM dans laquelle il a été saisi
      * valeur par défaut : JSRP
   Pour la fonction **[d’activation](/help/communities/overview.md#enablement-community)**

   * [installation et configuration de FFmpeg](/help/communities/ffmpeg.md)
   * [installation du pilote JDBC pour MySQL ;](#jdbc-driver-for-mysql)
   * [installation d’AEM Communities SCORM-Engine](#scorm-package)
   * [installer et configurer MySQL pour l’activation](/help/communities/mysql.md)






## Dernières versions {#latest-releases}

AEM 6.5 Communities GA fournit un package Communities. Pour en savoir plus sur les mises à jour des [communautés](/help/release-notes/release-notes.md#experiencemanagercommunities)AEM 6.5, consultez les Notes [de mise à jour d’](/help/release-notes/release-notes.md#communities-release-notes.html)AEM 6.5.

### Mises à jour d’AEM 6.5 {#aem-updates}

À partir d’AEM 6.4, les mises à jour apportées aux communautés sont fournies dans le cadre des Fix Packs et Service Packs cumulatifs AEM.

Pour obtenir les dernières mises à jour d’AEM 6.5, voir [Adobe Experience Manager 6.4 Cumulative Fix Packs et Service Packs](https://helpx.adobe.com/experience-manager/aem-releases-updates.html).

### Version History {#version-history}

Comme pour AEM 6.4 et les versions ultérieures, les fonctionnalités et correctifs des communautés AEM font partie des packs de correctifs et des Service Packs cumulatifs des communautés AEM. Il n’existe donc pas de Feature Packs distincts.

### Pilote JDBC pour MySQL {#jdbc-driver-for-mysql}

Deux fonctionnalités Communities utilisent une base de données MySQL :

* pour [activation](/help/communities/enablement.md) : enregistrement des activités et des apprenants SCORM
* pour [DSRP](/help/communities/dsrp.md) : stockage du contenu généré par l’utilisateur (UGC)

Le connecteur MySQL doit être obtenu et installé séparément.

Les étapes nécessaires sont :

1. télécharger l’archive ZIP depuis [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * version doit être >= 5.1.38

1. extraire mysql-connector-java-&lt;version>-bin.jar (lot) de l’archive
1. utilisez la console Web pour installer et démarrer le lot :

   * par exemple, https://localhost:4502/system/console/bundles
   * select **`Install/Update`**
   * Parcourir... pour sélectionner le lot extrait de l’archive ZIP téléchargée
   * vérifiez que* le pilote JDBC d&#39;Oracle Corporation pour MySQLcom.mysql.jdbc* est actif et démarrez-le dans le cas contraire (ou vérifiez les journaux).

1. si vous effectuez l’installation sur un déploiement existant après la configuration de JDBC, redémarrez JDBC sur le nouveau connecteur en réenregistrant la configuration JDBC à partir de la console Web :

   * par exemple, https://localhost:4502/system/console/configMgr
   * localiser `Day Commons JDBC Connections Pool` la configuration
   * sélectionner pour ouvrir
   * select `Save`

1. répéter les étapes 3 et 4 sur toutes les instances d’auteur et de publication

Pour plus d&#39;informations sur l&#39;installation des lots, consultez la page Console [](/help/sites-deploying/configuring-web-console.md#bundles) Web.

#### Exemple : Bundle MySQL Connector installé {#example-installed-mysql-connector-bundle}

![](/help/communities/assets/chlimage_1-125.png)

### Package SCORM {#scorm-package}

SCORM (Shareable Content Object Reference Model) est un ensemble de normes et de spécifications pour l’apprentissage en ligne. SCORM définit également la manière dont le contenu peut être compressé dans un fichier ZIP transférable.

Le moteur SCORM des communautés AEM est requis pour la fonctionnalité [d’activation](/help/communities/overview.md#enablement-community) . Packages Scorm pris en charge sur les communautés AEM 6.5 :

* [cq-social-scorm-package, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) qui inclut le moteur [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Pour installer un package SCORM**

1. Installez le package [cq-social-scorm-package, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) à partir du partage de package.
1. Téléchargez `/libs/social/config/scorm/database_scormengine_data.sql` depuis l’instance cq et exécutez-la dans mysql server pour créer un schéma scormEngineDB mis à niveau.
1. Ajoutez `/content/communities/scorm/RecordResults` dans la propriété Chemins exclus du filtre CSRF depuis `https://<hostname>:<port>/system/console/configMgr` les éditeurs.


#### Journalisation SCORM {#scorm-logging}

Au fur et à mesure de l’installation, toute activité d’activation est généreusement consignée dans la console système.

Si vous le souhaitez, le niveau du journal peut être défini sur WARN pour le `RusticiSoftware.*` package.

Pour utiliser les journaux, voir [Utilisation des enregistrements d’audit et des fichiers](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)journaux.

### MLS AEM Advanced {#aem-advanced-mls}

Pour que la collection SRP (MSRP ou DSRP) prenne en charge la recherche multilingue avancée (MLS), de nouveaux plug-ins Solr sont requis en plus d’un schéma personnalisé et d’une configuration Solr. Tous les éléments requis sont compressés dans un fichier zip téléchargeable.

Le téléchargement MLS avancé (également appelé &quot;phasetwo&quot;) est disponible à partir du référentiel Adobe :

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * version 1.2.40, 6 avril 2016
   * télécharger AEM-SOLR-MLS-phasetwo-1.2.40.zip

Pour plus d’informations sur l’installation et les détails, consultez Configuration [du](/help/communities/solr.md) Solr pour SRP.

### A propos des liens vers le partage de package {#about-links-to-package-share}

**Packages visibles dans Adobe AEM Cloud**

Les liens vers les packages de cette page ne nécessitent aucune instance en cours d’exécution d’AEM, car ils sont destinés au partage de packages sur `adobeaemcloud.com`. Bien que les packs puissent être consultés, le `Install`bouton permet d’installer les packs sur un site hébergé par Adobe. Si vous prévoyez d’effectuer l’installation sur une instance AEM locale, la sélection `Install`entraînera une erreur.

**Installation sur une instance locale AEM**

Pour installer les packages visibles dans `adobeaemcloud.com` une instance locale AEM, le package doit d’abord être téléchargé sur un disque local :

* select the **Assets** tab
* select **download to disk**

Sur l’instance locale d’AEM, utilisez le gestionnaire de packages (par exemple [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) pour télécharger vers le référentiel de packages local d’AEM.

Vous pouvez également accéder au package à l’aide du partage de package à partir de l’instance locale AEM ( [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/), par exemple). Le `Download`bouton sera téléchargé dans le référentiel de packages de l’instance locale AEM.

Une fois dans le référentiel de packages de l’instance locale d’AEM, utilisez le gestionnaire de packages pour installer le package.

Pour plus d’informations, consultez [Comment utiliser des packages](/help/sites-administering/package-manager.md#package-share).

## Déploiements recommandés {#recommended-deployments}

Dans les communautés AEM, un magasin commun est utilisé pour stocker le contenu généré par l’utilisateur (UGC) et est souvent appelé fournisseur de ressources de [stockage (SRP)](/help/communities/working-with-srp.md). Le déploiement recommandé consiste à choisir une option SRP pour la boutique commune.

Le magasin commun prend en charge la modération de l’UGC et l’analyse de cette dernière dans l’environnement de publication, tout en éliminant la nécessité de [réplication](/help/communities/sync.md) de l’UGC.

* [Community Content Store](/help/communities/working-with-srp.md) : décrit les options de stockage SRP pour les communautés AEM

* [Topologies](/help/communities/topologies.md) recommandées : aborde la topologie à utiliser en fonction du cas d’utilisation et du choix du SRP

## Mise à niveau {#upgrading}

Lors de la mise à niveau vers la plate-forme AEM 6.5 à partir des versions précédentes d’AEM, il est important de lire [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md).

Outre la mise à niveau de la plateforme, consultez [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md) pour en savoir plus sur les modifications apportées aux communautés.

## Configurations {#configurations}

### Éditeur principal {#primary-publisher}

Lorsque le déploiement choisi est une batterie de [publication](/help/communities/topologies.md#tarmk-publish-farm), une instance de publication AEM doit être identifiée comme la **`primary publisher`** pour les activités qui ne doivent pas se produire sur toutes les instances, telles que les fonctionnalités reposant sur **notifications **ou **Adobe Analytics**.

Par défaut, la configuration `AEM Communities Publisher Configuration` OSGi est configurée avec la **`Primary Publisher`** case à cocher cochée, de sorte que toutes les instances de publication dans une batterie de publication s’identifient elles-mêmes comme étant le principal.

Par conséquent, il est nécessaire de **modifier la configuration sur toutes les instances** de publication secondaires pour décocher la **`Primary Publisher`** case.

![](/help/communities/assets/chlimage_1-126.png)

Pour toutes les autres instances de publication (secondaires) dans une batterie de publication :

* connectez-vous avec des autorisations d’administrateur
* access the [web console](/help/sites-deploying/configuring-osgi.md)

   * for example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* localisez la `AEM Communities Publisher Configuration`
* sélectionnez l’icône de modification
* désélectionnez la case Editeur **** principal
* sélectionnez **Enregistrer**

### Agents de réplication sur l’auteur {#replication-agents-on-author}

La réplication est utilisée pour le contenu du site créé dans l’environnement de publication, tel que les groupes de la communauté, ainsi que pour la gestion des membres et des groupes de membres de l’environnement d’auteur à l’aide du service [](#tunnel-service-on-author)tunnel.

Pour l’éditeur principal, assurez-vous que la configuration [de l’agent de](/help/sites-deploying/replication.md) réplication identifie correctement le serveur de publication et l’utilisateur autorisé. L’utilisateur autorisé par défaut `admin,` dispose déjà des autorisations appropriées (est membre de `Communities Administrators`).

Pour qu’un autre utilisateur dispose des autorisations appropriées, il doit être ajouté en tant que membre du groupe `administrators` d’utilisateurs (également membre de `Communities Administrators`).

Deux agents de réplication dans l’environnement d’auteur doivent configurer correctement la configuration du transport.

* accéder à la console de réplication sur l’auteur

   * de la navigation globale : **Outils, déploiement, réplication, agents sur l’auteur**

* suivre la même procédure pour les deux agents :

   * **Agent par défaut (publication)**
   * **Agent de réplication inverse (inversion de publication)**

      1. sélectionner l&#39;agent
      1. select **edit**
      1. select the **Transport** tab
      1. si ce n’est pas le port `4503`, modifiez l’ **URI** pour spécifier le port correct.

      1. si vous n’utilisez pas `admin`, modifiez l’ **utilisateur** et le **mot de passe** pour spécifier un membre du groupe `administrators` d’utilisateurs.

Les images suivantes montrent les résultats du changement de port de 4503 à 6103 par :

#### Agent par défaut (publication) {#default-agent-publish}

![](/help/communities/assets/chlimage_1-127.png)

#### Agent de réplication inverse (inversion de publication) {#reverse-replication-agent-publish-reverse}

![](/help/communities/assets/chlimage_1-128.png)

### Service Tunnel sur l’auteur {#tunnel-service-on-author}

Lorsque vous utilisez l’environnement d’auteur pour [créer des sites](/help/communities/sites-console.md), [modifier des propriétés](/help/communities/sites-console.md#modifying-site-properties) du site ou [gérer des membres](/help/communities/members.md)de la communauté, il est nécessaire d’accéder aux membres (utilisateurs) enregistrés dans l’environnement de publication et non aux utilisateurs enregistrés dans l’environnement d’auteur.

Le service tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

Pour activer le service tunnel :

* on **author**
* Connectez-vous avec des droits d’administrateur.
* si l’éditeur n’est pas localhost:4503 ou si l’utilisateur du transport ne l’est pas `admin`, [configurez l’agent de réplication](#replication-agents-on-author)

* accédez à la [console Web](/help/sites-deploying/configuring-osgi.md)

   * for example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* localisez la `AEM Communities Publish Tunnel Service`
* sélectionnez l’icône de modification
* cochez la **activer **case
* sélectionnez **Enregistrer**

![](/help/communities/assets/chlimage_1-129.png)

### Répliquer la clé Crypto {#replicate-the-crypto-key}

Deux fonctionnalités des communautés AEM exigent que toutes les instances de serveur AEM utilisent les mêmes clés de chiffrement. Il s’agit d’ [Analytics](/help/communities/analytics.md) et [ASRP](/help/communities/asrp.md).

Depuis AEM 6.3, le matériel clé est stocké dans le système de fichiers et ne figure plus dans le référentiel.

Pour copier les documents clés de l’auteur vers toutes les autres instances, il est nécessaire de :

* accédez à l’instance AEM, généralement une instance d’auteur, qui contient le matériel clé à copier.

   * locate the `com.adobe.granite.crypto.file` bundle in the local file system
for example,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * le `bundle.info` fichier identifie le lot
   * naviguer dans le dossier de données, par exemple,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * copie des fichiers hmac et maître



* pour chaque instance AEM cible

   * naviguer dans le dossier de données, par exemple,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * coller les 2 fichiers précédemment copiés
   * il est nécessaire d’ [actualiser le lot](#refresh-the-granite-crypto-bundle) Granite Crypto si l’instance AEM cible est en cours d’exécution.


>[!CAUTION]
>
>Si une autre fonction de sécurité a déjà été configurée basée sur les clés de chiffrement, la réplication des clés de chiffrement pourrait endommager la configuration. Pour obtenir de l’aide, [contactez le service à la clientèle](https://helpx.adobe.com/marketing-cloud/contact-support.html).

#### Réplication du référentiel {#repository-replication}

Le fait que le matériel clé soit stocké dans le référentiel, comme c’était le cas pour AEM 6.2 et versions antérieures, peut être conservé en spécifiant la propriété système suivante au premier démarrage de chaque instance AEM (qui crée le référentiel initial) :

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>Il est important de vérifier que l’agent de [réplication sur l’auteur](#replication-agents-on-author) est correctement configuré.

Avec le matériel clé stocké dans le référentiel, la manière de répliquer la clé de chiffrement de l&#39;auteur vers d&#39;autres instances est la suivante :

Using [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* accédez à [https://&lt;serveur>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* select `/etc/key`
* ouvrir `Replication` , panneau
* select `Replicate`

* [actualisation du lot Granite Crypto](#refresh-the-granite-crypto-bundle)

![](/help/communities/assets/chlimage_1-130.png)

#### Actualiser l’offre groupée Granite Crypto {#refresh-the-granite-crypto-bundle}

* sur chaque instance de publication, accédez à la console [Web](/help/sites-deploying/configuring-osgi.md)

   * par exemple, [https://&lt;serveur>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* localiser le `Adobe Granite Crypto Support` lot (com.adobe.granite.crypto)
* sélectionner **Actualiser**

![](/help/communities/assets/chlimage_1-131.png)

* au bout d&#39;un instant, une boîte de dialogue **Réussite **doit s&#39;afficher :
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Si vous utilisez le serveur Apache HTTP, veillez à utiliser le nom de serveur correct pour toutes les entrées pertinentes.

En particulier, veillez à utiliser le nom de serveur correct, et non `localhost`, dans la `RedirectMatch`.

#### exemple httpd.conf {#httpd-conf-sample}

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

### Répartiteur {#dispatcher}

Si vous utilisez un répartiteur, reportez-vous à la section :

* Documentation du [répartiteur](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) AEM
* [Installation de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configuration du répartiteur pour les communautés](/help/communities/dispatcher.md)
* [Problèmes connus](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentation sur les communautés associée {#related-communities-documentation}

* Reportez-vous à la section [Administration des sites de communauté](/help/communities/administer-landing.md) pour en savoir plus sur la création d’un site de communauté, la configuration de modèles de sites de communauté, la modération du contenu de communauté, la gestion des membres et la configuration de la messagerie.

* Visit [Developing Communities](/help/communities/communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.

* Visitez [Création de composants](/help/communities/author-communities.md) de communautés pour apprendre à créer et à configurer des composants de communautés.

