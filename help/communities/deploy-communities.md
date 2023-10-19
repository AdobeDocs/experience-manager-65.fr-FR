---
title: Déploiement de Communities
description: Découvrez comment déployer des communautés et des fonctionnalités de communauté dans Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '1712'
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

**Pour le [AEM plateforme](/help/sites-deploying/deploy.md#what-is-aem)**

* Installer la dernière [Mises à jour AEM 6.5](#aem64updates)

* Si vous n’utilisez pas les ports par défaut (4502, 4503), [configuration des agents de réplication](#replication-agents-on-author)
* [Réplication de la clé de cryptage](#replicate-the-crypto-key)
* Si elle soutient la mondialisation, [configuration de la traduction automatisée](/help/sites-administering/translation.md)
(exemple de configuration fourni pour le développement)

**Pour le [Fonctionnalités des communautés](/help/communities/overview.md)**

* Si vous déployez une [batterie de publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identification de l’éditeur principal](#primary-publisher)

* [Activation du service tunnel](#tunnel-service-on-author)
* [Activation de la connexion sociale](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configuration d’Adobe Analytics](/help/communities/analytics.md)
* Configurez une [service de messagerie par défaut](/help/communities/email.md)
* Identifier le choix pour [stockage UGC partagé](/help/communities/working-with-srp.md) (**SRP**)

   * Si MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installation et configuration de MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configuration de Solr](/help/communities/solr.md)
      * [Sélectionner MSRP](/help/communities/srp-config.md)

   * Si SRP de base de données relationnelle [(DSRP)](/help/communities/dsrp.md)

      * [Installation du pilote JDBC pour MySQL](#jdbc-driver-for-mysql)
      * [Installation et configuration de MySQL pour DSRP](/help/communities/dsrp-mysql.md)
      * [Configuration de Solr](/help/communities/solr.md)
      * [Sélectionner DSRP](/help/communities/srp-config.md)

   * Si Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Utilisation de votre gestionnaire de compte pour l’approvisionnement
      * [Sélectionner ASRP](/help/communities/srp-config.md)

   * Si JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Magasin de contenu généré par l’utilisateur non partagé :

         * Le contenu généré par l’utilisateur n’est jamais répliqué
         * Le contenu généré par l’utilisateur n’est visible que sur l’instance AEM ou la grappe dans laquelle il a été entré.

         * La valeur par défaut est JSRP

## Dernières versions {#latest-releases}

AEM 6.5 Communities GA inclut le package Communities. Pour en savoir plus sur les mises à jour d’AEM 6.5 [Communautés](/help/release-notes/release-notes.md#experiencemanagercommunities), voir [Notes de mise à jour d’AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Mises à jour AEM 6.5 {#aem-updates}

À compter de la version 6.4 d’AEM, les mises à jour apportées aux communautés sont fournies dans le cadre d’AEM Cumulative Fix Packs et Service Packs.

Pour connaître les dernières mises à jour d’AEM 6.5, voir [Packs de correctifs cumulatifs et Service Packs Adobe Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr).

### Historique des versions {#version-history}

Comme pour AEM 6.4 et versions ultérieures, les fonctionnalités et correctifs d’AEM Communities font partie des packs de correctifs cumulatifs et des Service Packs d’AEM Communities. Il n’existe donc aucun Feature Pack distinct.

### Pilote JDBC pour MySQL {#jdbc-driver-for-mysql}

Une fonctionnalité Communities utilise une base de données MySQL :

* Pour [DSRP](/help/communities/dsrp.md): stockage UGC

Le connecteur MySQL doit être obtenu et installé séparément.

Les étapes nécessaires sont les suivantes :

1. Téléchargez l’archive ZIP à partir de [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La version doit être >= 5.1.38

1. Extraire mysql-connector-java-&lt;version>-bin.jar (lot) de l’archive
1. Utilisez la console web pour installer et démarrer le lot :

   * Par exemple, https://localhost:4502/system/console/bundles
   * Sélectionnez **`Install/Update`**.
   * Parcourir.. pour sélectionner le lot extrait de l’archive ZIP téléchargée
   * Vérifiez que *Pilote JDBC d’Oracle Corporation pour MySQLcom.mysql.jdbc* est active et démarrez-la si ce n’est pas le cas (ou vérifiez les journaux).

1. Si vous effectuez l’installation sur un déploiement existant après la configuration de JDBC, replacez JDBC sur le nouveau connecteur en réenregistrant la configuration JDBC à partir de la console web :
   * Par exemple, https://localhost:4502/system/console/configMgr
   * Localiser `Day Commons JDBC Connections Pool` configuration
   * Sélectionner pour ouvrir
   * Sélectionnez `Save`.

1. Répétez les étapes 3 et 4 sur toutes les instances d’auteur et de publication.

Vous trouverez plus d’informations sur l’installation des lots sur la page [Console web](/help/sites-deploying/web-console.md) page.

#### Exemple : offre groupée MySQL Connector installée {#example-installed-mysql-connector-bundle}

![connector-bundle](assets/connector-bundle.png)



### AEM MLS avancés {#aem-advanced-mls}

Pour que la collection SRP (MSRP ou DSRP) prenne en charge la recherche multilingue avancée (MLS), de nouveaux modules externes Solr sont requis en plus d’un schéma personnalisé et d’une configuration Solr. Tous les éléments requis sont compressés dans un fichier ZIP téléchargeable.

Téléchargement MLS avancé (également appelé `phasetwo`) est disponible à partir du référentiel Adobe :

* AEM-SOLR-MLS-phasetwo

  Pour obtenir le package MLS avancé, voir [AEM MLS avancés](deploy-communities.md#aem-advanced-mls) dans la section deploy de la documentation.

   * Version 1.2.40, 6 avril 2016
   * Téléchargez AEM-SOLR-MLS-phasetwo-1.2.40.zip

Pour plus d’informations sur l’installation, voir [Configuration de Solr](/help/communities/solr.md) pour la SRP.

### À propos des liens vers le partage de modules {#about-links-to-package-share}

**Modules visibles dans Adobe AEM Cloud**

Les liens vers les modules de cette page ne nécessitent aucune instance d’AEM en cours d’exécution, car ils sont destinés au partage de modules sur `adobeaemcloud.com`. Bien que les modules soient visibles, la variable `Install` est destiné à installer les packages sur un site hébergé par Adobe. Si vous envisagez d’effectuer l’installation sur une instance d’AEM locale, sélectionnez `Install` entraîne une erreur.

**Installation sur une instance d’AEM locale**

Pour installer les packages visibles dans `adobeaemcloud.com` sur une instance d’AEM locale, le package doit d’abord être téléchargé sur un disque local :

* Sélectionnez la variable **Ressources** tab
* Sélectionner **télécharger sur le disque**

Sur l’instance d’AEM locale, utilisez Package Manager (par exemple [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)), pour charger vers le référentiel de package d’AEM local.

Vous pouvez également accéder au module à l’aide de Package Share à partir de l’instance d’AEM locale (par exemple, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), la variable `Download` télécharge vers le référentiel de package de l’instance AEM locale.

Une fois que vous vous trouvez dans le référentiel de package de l’instance d’AEM locale, utilisez Package Manager pour installer le package.

Pour plus d’informations, voir [Utilisation de modules](/help/sites-administering/package-manager.md#package-share).

## Déploiements recommandés {#recommended-deployments}

Dans AEM Communities, un magasin commun est utilisé pour stocker le contenu créé par l’utilisateur et est souvent appelé [fournisseur de ressources de stockage (SRP)](/help/communities/working-with-srp.md). Le déploiement recommandé se concentre sur le choix d’une option SRP pour le magasin commun.

Le magasin commun prend en charge la modération et l’analyse du contenu créé par l’utilisateur dans l’environnement de publication, tout en éliminant la nécessité de [réplication](/help/communities/sync.md) de contenu généré par l’utilisateur.

* [Community Content Store](/help/communities/working-with-srp.md) : aborde les options de stockage SRP pour AEM Communities

* [Topologies recommandées](/help/communities/topologies.md) : aborde la topologie à utiliser en fonction du cas d’utilisation et du choix de la SRP.

## Mise à niveau {#upgrading}

Lors de la mise à niveau vers la plateforme AEM 6.5 à partir des versions précédentes d’AEM, il est important de lire [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md).

En plus de la mise à niveau de la plateforme, lisez [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md) pour en savoir plus sur les modifications apportées aux communautés.

## Configurations {#configurations}

### Éditeur de Principal {#primary-publisher}

Lorsque le déploiement sélectionné est un [batterie de publication](/help/communities/topologies.md#tarmk-publish-farm), une instance de publication AEM doit être identifiée en tant que **`primary publisher`** pour les activités qui ne doivent pas se produire sur toutes les instances. Par exemple, des fonctionnalités qui dépendent de **notifications** ou **Adobe Analytics**.

Par défaut, la variable `AEM Communities Publisher Configuration` La configuration OSGi est configurée avec le **`Primary Publisher`** case à cocher cochée, de telle sorte que toutes les instances de publication d’une ferme de publication s’identifient elles-mêmes comme instance principale.

Par conséquent, il est nécessaire de **modifier la configuration sur toutes les instances de publication secondaires ;** pour décocher la variable **`Primary Publisher`** .

![principal-publisher](assets/primary-publisher.png)

Pour toutes les autres instances de publication (secondaires) dans une ferme de publication :

* Connexion avec droits d’administrateur
* Accédez au [console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple : [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Recherchez la variable `AEM Communities Publisher Configuration`
* Sélectionner l’icône de modification
* Décochez la case **Éditeur de Principal** box
* Sélectionnez **Enregistrer**.

### Agents de réplication sur l’auteur {#replication-agents-on-author}

La réplication est utilisée pour le contenu du site créé dans l’environnement de publication, tel que les groupes de la communauté, et la gestion des membres et des groupes de membres de l’environnement de création à l’aide de la fonction [service tunnel](#tunnel-service-on-author).

Pour l’éditeur principal, assurez-vous que la variable [Configuration de l’agent de réplication](/help/sites-deploying/replication.md) identifie correctement le serveur de publication et l’utilisateur autorisé. l’utilisateur autorisé par défaut, `admin,` dispose déjà des autorisations appropriées (est membre de `Communities Administrators`).

Pour que d’autres utilisateurs disposent des autorisations appropriées, ils doivent être ajoutés en tant que membre au `administrators` groupe d’utilisateurs (également membre de `Communities Administrators`).

Il existe deux agents de réplication dans l’environnement de création qui ont besoin que la configuration du transport soit correctement configurée.

* Accès à la console de réplication sur l’auteur

   * Dans la navigation globale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]** > **[!UICONTROL Agents sur l’auteur]**

* Suivez la même procédure pour les deux agents :

   * **Agent par défaut (publication)**
   * **Agent de réplication inverse (publication inversée)**

      1. Sélectionner l’agent
      1. Sélectionner **edit**
      1. Sélectionnez la variable **Transport** tab
      1. Si ce n’est pas un port `4503`, modifiez la variable **URI** pour spécifier le port correct

      1. S’il n’est pas utilisateur `admin`, modifiez la variable **Utilisateur** et **Password** pour spécifier un membre de la fonction `administrators` groupe d’utilisateurs

Les images suivantes montrent les résultats du changement de port de 4503 à 6103 en :

#### Agent par défaut (publication) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Agent de réplication inverse (publication inversée) {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### Service Tunnel sur l’auteur {#tunnel-service-on-author}

Lorsque vous utilisez l’environnement de création pour [créer des sites ;](/help/communities/sites-console.md), [modification des propriétés du site](/help/communities/sites-console.md#modifying-site-properties) ou [gestion des membres de la communauté](/help/communities/members.md), il est nécessaire d’accéder aux membres (utilisateurs) enregistrés dans l’environnement de publication, et non aux utilisateurs enregistrés dans l’environnement de création.

Le service tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

Pour activer le service tunnel :

* Connectez-vous avec les privilèges d’administrateur sur votre instance de création.
* Si l’éditeur n’est pas localhost:4503 ou que l’utilisateur du transport ne l’est pas `admin`, puis [configuration de l’agent de réplication](#replication-agents-on-author)

* Accédez au [Console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple : [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Recherchez la variable `AEM Communities Publish Tunnel Service`
* Sélectionner l’icône de modification
* Vérifiez les **enable** box
* Sélectionnez **Enregistrer**.

  ![tunnel-service](assets/tunnel-service.png)

### Réplication de la clé de chiffrement {#replicate-the-crypto-key}

Il existe deux fonctionnalités d’AEM Communities qui nécessitent que toutes les instances AEM serveur utilisent les mêmes clés de chiffrement. Voici les [Analytics](/help/communities/analytics.md) et [ASRP](/help/communities/asrp.md).

À partir de la version 6.3 d’AEM, le matériel clé est stocké dans le système de fichiers et ne figure plus dans le référentiel.

Pour copier le matériel clé de l’auteur vers toutes les autres instances, il est nécessaire de :

* Accédez à l’instance AEM (généralement une instance d’auteur) qui contient le matériel clé à copier.

   * Recherchez la variable `com.adobe.granite.crypto.file` dans le système de fichiers local, par exemple :

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * La variable `bundle.info` identifie le lot

   * Accédez au dossier de données, par exemple :

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copiez les fichiers de noeud hmac et principal

* Pour chaque instance AEM cible

   * Accédez au dossier de données, par exemple :

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * Coller les deux fichiers précédemment copiés
   * Il est nécessaire de [actualiser le lot Crypto Granite](#refresh-the-granite-crypto-bundle) si l’instance AEM cible est en cours d’exécution

>[!CAUTION]
>
>Si une autre fonctionnalité de sécurité a déjà été configurée basée sur les clés de cryptage, la réplication des clés de cryptage peut endommager la configuration. Pour obtenir de l’aide, [contactez l’assistance clientèle](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support).

#### Réplication du référentiel {#repository-replication}

Il est possible de conserver le matériel clé stocké dans le référentiel, comme c’était le cas pour AEM version 6.2 et antérieure. Spécification de la propriété système `-Dcom.adobe.granite.crypto.file.disable=true` au premier démarrage de chaque instance AEM (qui crée le référentiel initial).

>[!NOTE]
>
>Vérifiez que la variable [agent de réplication sur l’auteur](#replication-agents-on-author) est correctement configuré.

Avec le matériel clé stocké dans le référentiel, la manière de répliquer la clé de chiffrement de l’auteur vers d’autres instances est la suivante :

Utilisation [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Accédez à [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Sélectionnez `/etc/key`.
* Ouvrir `Replication` tab
* Sélectionnez `Replicate`.

* [Actualisation du lot Crypto Granite](#refresh-the-granite-crypto-bundle)

  ![replicare-repository](assets/replicare-repository.png)

#### Actualisation du lot de chiffrement Granite {#refresh-the-granite-crypto-bundle}

* Sur chaque instance de publication, accédez au [Console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple : [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Localiser `Adobe Granite Crypto Support` bundle (com.adobe.granite.crypto)
* Sélectionner **Actualiser**

  ![granite-crypto](assets/granite-crypto.png)

* Après un moment, une **Succès** La boîte de dialogue doit s’afficher :
  `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Si vous utilisez le serveur Apache HTTP, veillez à utiliser le nom de serveur correct pour toutes les entrées pertinentes.

En particulier, veillez à utiliser le nom de serveur correct, et non `localhost`, dans la variable `RedirectMatch`.

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

* AEM [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) documentation
* [Installation du Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=en)
* [Configuration de Dispatcher pour Communities](/help/communities/dispatcher.md)
* [Problèmes connus](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentation sur les communautés connexes {#related-communities-documentation}

* Visite [Administration des sites des communautés](/help/communities/administer-landing.md) pour en savoir plus sur la création d’un site communautaire, la configuration des modèles de site communautaire, la modération du contenu communautaire, la gestion des membres et la configuration de la messagerie.

* Visite [Développement de communautés](/help/communities/communities.md) où vous pouvez en savoir plus sur la structure de composants sociaux (SCF) et la personnalisation des composants et fonctionnalités de Communities.

* Visite [Création de composants Communities](/help/communities/author-communities.md) où vous pouvez apprendre à créer avec et configurer des composants Communities.
