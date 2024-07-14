---
title: Déploiement de Communities
description: Comment déployer AEM Communities
content-type: reference
topic-tags: deploying
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 2%

---


# Déploiement de Communities{#deploying-communities}

## Conditions préalables {#prerequisites}

* [Plateforme AEM 6.5](/help/sites-deploying/deploy.md)

* Licence AEM Communities

* Licences facultatives pour :

   * [Fonctionnalités d’Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB pour MSRP](/help/communities/msrp.md)
   * [Adobe Cloud pour ASRP](/help/communities/asrp.md)

## Liste de contrôle d’installation {#installation-checklist}

**Pour la [plateforme AEM](/help/sites-deploying/deploy.md#what-is-aem)** :

* Installez les dernières [mises à jour AEM 6.5](#aem64updates).

* Si vous n&#39;utilisez pas les ports par défaut (4502, 4503), alors [configurez les agents de réplication](#replication-agents-on-author).
* [Réplication de la clé de chiffrement](#replicate-the-crypto-key)
* Si vous prenez en charge la mondialisation, [configurer la traduction automatisée](/help/sites-administering/translation.md)
(l’exemple de configuration est fourni pour le développement).

**Pour la [fonctionnalité Communities](/help/communities/overview.md)** :

* Si vous déployez une [ferme de publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [ identifiez l’éditeur principal](#primary-publisher)

* [Activation du service tunnel](#tunnel-service-on-author)
* [Activation de la connexion sociale](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configuration d’Adobe Analytics](/help/communities/analytics.md)
* Configuration d’un [service de messagerie par défaut](/help/communities/email.md)
* Identifiez le choix de l&#39;[espace de stockage UGC partagé](/help/communities/working-with-srp.md) (**SRP**)

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

      * Contactez le gestionnaire de compte pour la mise en service.
      * [Sélectionner ASRP](/help/communities/srp-config.md)

   * Si JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Magasin de contenu généré par l’utilisateur non partagé :

         * Le contenu généré par l’utilisateur n’est jamais répliqué.
         * Le contenu généré par l’utilisateur n’est visible que sur une instance AEM ou une grappe dans laquelle il a été saisi.

      * La valeur par défaut est JSRP


## Dernières versions {#latest-releases}

AEM 6.5 Communities GA inclut le package Communities. Pour en savoir plus sur les mises à jour d’AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consultez les [Notes de mise à jour d’AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Mises à jour AEM 6.5 {#aem-updates}

À compter de la version 6.4 d’AEM, les mises à jour apportées aux communautés sont fournies dans le cadre d’AEM Cumulative Fix Packs et Service Packs.

Pour les dernières mises à jour d’AEM 6.5, voir [Adobe Experience Manager 6.4 Cumulative Fix Packs and Service Packs](https://helpx.adobe.com/fr/experience-manager/aem-releases-updates.html).

### Historique des versions {#version-history}

Comme pour AEM 6.4 et versions ultérieures, les fonctionnalités et correctifs d’AEM Communities font partie des packs de correctifs cumulatifs et des Service Packs d’AEM Communities. Il n’existe donc aucun Feature Pack distinct.

### Pilote JDBC pour MySQL {#jdbc-driver-for-mysql}

Une fonctionnalité Communities utilise une base de données MySQL :

* Pour [DSRP](/help/communities/dsrp.md) : stockage du contenu créé par l’utilisateur

Le connecteur MySQL doit être obtenu et installé séparément.

Les étapes nécessaires sont les suivantes :

1. Téléchargez l’archive ZIP depuis [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La version doit être >= 5.1.38

1. Extraire `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. Utilisez la console web pour installer et démarrer le lot :

   * Par exemple, https://localhost:4502/system/console/bundles
   * Sélectionnez **`Install/Update`**.
   * Parcourir.. pour sélectionner le lot extrait de l’archive ZIP téléchargée
   * Vérifiez que *Oracle Corporation&#39;s JDBC Driver for MySQLcom.mysql.jdbc* est actif et démarrez-le dans le cas contraire (ou vérifiez les journaux).

1. Si vous effectuez l’installation sur un déploiement existant après la configuration de JDBC, replacez JDBC sur le nouveau connecteur en réenregistrant la configuration JDBC à partir de la console web :

   * Par exemple, https://localhost:4502/system/console/configMgr
   * Recherchez la configuration `Day Commons JDBC Connections Pool` et sélectionnez pour ouvrir la configuration.
   * Sélectionnez `Save`.

1. Répétez les étapes 3 et 4 sur toutes les instances d’auteur et de publication.

Vous trouverez plus d’informations sur l’installation des lots sur la page [Console web](/help/sites-deploying/web-console.md#bundles).

#### Exemple : offre groupée MySQL Connector installée {#example-installed-mysql-connector-bundle}

![Bundle de connecteur MySQL de la console web Adobe Experience Manager](../assets/mysql-connector.png)

### AEM MLS avancés {#aem-advanced-mls}

Pour que la collection SRP (MSRP ou DSRP) prenne en charge la recherche multilingue avancée (MLS), de nouveaux modules externes Solr sont requis en plus d’un schéma personnalisé et d’une configuration Solr. Tous les éléments requis sont compressés dans un fichier ZIP téléchargeable.

Le téléchargement MLS avancé (également appelé &quot;phasetwo&quot;) est disponible à partir du référentiel Adobe :

* [AEM-SOLR-MLS-phasetwo](https://repo1.maven.org/maven2/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * Version 1.2.40, 6 avril 2016
   * Téléchargez AEM-SOLR-MLS-phasetwo-1.2.40.zip

Pour plus d’informations sur l’installation, consultez la page [Configuration Solr](/help/communities/solr.md) pour SRP.

### À propos des liens vers le partage de modules {#about-links-to-package-share}

**Packages visibles dans Adobe AEM Cloud**

Les liens vers les modules de cette page ne nécessitent aucune instance d’AEM en cours d’exécution, car ils sont destinés au partage de modules sur `adobeaemcloud.com`. Bien que les packages soient visibles, le bouton `Install` permet d’installer les packages sur un site hébergé par Adobe. Si vous envisagez d’effectuer l’installation sur une instance d’AEM locale, la sélection de `Install` entraîne une erreur.

**Installation sur une instance d’AEM locale**

Pour installer les packages visibles dans `adobeaemcloud.com` sur une instance d’AEM locale, le package doit d’abord être téléchargé sur un disque local :

* Sélectionnez l’onglet **Assets**
* Sélectionnez **télécharger sur le disque**

Sur l’instance d’AEM locale, utilisez un gestionnaire de modules (par exemple, [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) pour charger vers le référentiel de modules d’AEM local.

Vous pouvez également accéder au module à l’aide du partage de modules à partir de l’instance d’AEM locale (par exemple, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)). Le bouton `Download` est téléchargé vers le référentiel de modules de l’instance AEM locale.

Une fois que vous vous trouvez dans le référentiel de package de l’instance d’AEM locale, utilisez Package Manager pour installer le package.

Pour plus d’informations, consultez la page [Utilisation de packages](/help/sites-administering/package-manager.md#package-share).

## Déploiements recommandés {#recommended-deployments}

Dans AEM Communities, un magasin commun est utilisé pour stocker le contenu créé par l’utilisateur et est souvent appelé [fournisseur de ressources de stockage (SRP)](/help/communities/working-with-srp.md). Le déploiement recommandé se concentre sur le choix d’une option SRP pour le magasin commun.

Le magasin commun prend en charge la modération et l’analyse du contenu créé par l’utilisateur dans l’environnement de publication tout en éliminant la nécessité de [réplication](/help/communities/sync.md) du contenu créé par l’utilisateur.

* [Community Content Store](/help/communities/working-with-srp.md) : aborde les options de stockage SRP pour AEM Communities

* [Topologies recommandées](/help/communities/topologies.md) : aborde la topologie à utiliser en fonction du cas d’utilisation et du choix de la SRP.

## Mise à niveau {#upgrading}

Lors de la mise à niveau vers la plateforme AEM 6.5 à partir des versions précédentes d’AEM, il est important de lire [Mise à niveau vers la version 6.5](/help/sites-deploying/upgrade.md).

Outre la mise à niveau de la plateforme, lisez [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md) pour en savoir plus sur les modifications apportées aux communautés.

## Configurations {#configurations}

### Éditeur de Principal {#primary-publisher}

Lorsque le déploiement choisi est une [ferme de publication](/help/communities/topologies.md#tarmk-publish-farm), une instance de publication AEM doit être identifiée comme **`primary publisher`** pour les activités qui ne doivent pas se produire sur toutes les instances. Par exemple, les fonctionnalités qui reposent sur **notifications** ou **Adobe Analytics**.

Par défaut, la configuration OSGi `AEM Communities Publisher Configuration` est configurée avec la case à cocher **`Primary Publisher`** cochée, de sorte que toutes les instances de publication dans une ferme de publication s’identifient elles-mêmes comme instance principale.

Par conséquent, il est nécessaire de **modifier la configuration sur toutes les instances de publication secondaires** pour décocher la case **`Primary Publisher`** .

![Boîte de dialogue de configuration de l’éditeur AEM Communities présentant la case à cocher Principal de l’éditeur](../assets/primary-publisher.png)

Pour toutes les autres instances de publication (secondaires) dans une ferme de publication :

* Connexion avec droits d’administrateur
* Accédez à la [console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Localisez le `AEM Communities Publisher Configuration`
* Sélectionner l’icône de modification
* Décochez la case **Principal Publisher**
* Sélectionnez **Enregistrer**.

### Agents de réplication sur l’auteur {#replication-agents-on-author}

La réplication est utilisée pour le contenu du site créé dans l’environnement de publication, comme les groupes de communautés, et la gestion des membres et des groupes de membres de l’environnement de création à l’aide du [service tunnel](#tunnel-service-on-author).

Pour l’éditeur principal, assurez-vous que la [configuration de l’agent de réplication](/help/sites-deploying/replication.md) identifie correctement le serveur de publication et l’utilisateur autorisé. L’utilisateur autorisé par défaut, `admin`, dispose déjà des autorisations appropriées (est membre de `Communities Administrators`).

Pour que certains autres utilisateurs disposent des autorisations appropriées, ils doivent être ajoutés en tant que membres au groupe d’utilisateurs `administrators` (également membre de `Communities Administrators`).

Il existe deux agents de réplication dans l’environnement de création qui ont besoin que la configuration du transport soit correctement configurée.

* Accès à la console de réplication sur l’auteur

   * À partir de la navigation globale : **Outils, déploiement, réplication, agents sur l’auteur**

* Suivez la même procédure pour les deux agents :

   * **Agent par défaut (publication)**
   * **Agent de réplication inverse (publication inverse)**

      1. Sélectionnez l’agent.
      1. Sélectionnez **edit**.
      1. Sélectionnez l’onglet **Transport**
      1. S’il ne s’agit pas du port `4503`, modifiez l’ **URI** pour spécifier le port approprié.

      1. Si ce n&#39;est pas l&#39;utilisateur `admin`, modifiez les **User** et **Password** pour spécifier un membre du groupe d&#39;utilisateurs `administrators`.

Les images suivantes montrent les résultats du changement de port de 4503 à 6103 par :

#### Agent par défaut (publication) {#default-agent-publish}

![configure-limits](../assets/default-agent-publish.png)

#### Agent de réplication inverse (publication inversée) {#reverse-replication-agent-publish-reverse}

![Agent de réplication inverse (réactifs de publication) montrant qu’il est activé ou activé.](../assets/reverse-replication-agent.png)

### Service Tunnel sur l’auteur {#tunnel-service-on-author}

Lors de l’utilisation de l’environnement de création pour [créer des sites](/help/communities/sites-console.md), [modifier les propriétés du site](/help/communities/sites-console.md#modifying-site-properties) ou [gérer les membres de la communauté](/help/communities/members.md), il est nécessaire d’accéder aux membres (utilisateurs) enregistrés dans l’environnement de publication, et non aux utilisateurs enregistrés dans l’environnement de création.

Le service tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

Pour activer le service tunnel :

* Sur **author**, connectez-vous avec des privilèges d’administrateur.
* Si l’éditeur n’est pas localhost:4503 ou que l’utilisateur du transport n’est pas `admin`,
ensuite [configurez l’agent de réplication](#replication-agents-on-author).

* Accédez à la [console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Localisez le `AEM Communities Publish Tunnel Service`
* Sélectionner l’icône de modification
* Cochez la case **enable**
* Sélectionnez **Enregistrer**.

![Service de tunnel AEM Communities Publish affichant la case à cocher &quot;activer&quot;, sélectionnée ou cochée.](../assets/tunnel-service.png)

### Réplication de la clé de chiffrement {#replicate-the-crypto-key}

Il existe deux fonctionnalités d’AEM Communities qui nécessitent que toutes les instances AEM serveur utilisent les mêmes clés de chiffrement. Il s’agit de [Analytics](/help/communities/analytics.md) et [ASRP](/help/communities/asrp.md).

À compter de la version AEM 6.3, le matériel clé est stocké dans le système de fichiers et ne figure plus dans le référentiel.

Pour copier le matériel clé de l’auteur vers toutes les autres instances, il est nécessaire de :

* Accédez à l’instance AEM (généralement une instance d’auteur) qui contient le matériel clé à copier.

   * Localisez le lot `com.adobe.granite.crypto.file` dans le système de fichiers local

     Par exemple :

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * Le fichier `bundle.info` identifie le lot

   * Accès au dossier de données
par exemple,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * Copiez les fichiers de noeud hmac et principal.

* Pour chaque instance AEM cible

   * Accès au dossier de données
par exemple,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * Coller les deux fichiers précédemment copiés
   * Il est nécessaire de [actualiser le lot Granite Crypto](#refresh-the-granite-crypto-bundle) si l’instance AEM cible est en cours d’exécution.

>[!CAUTION]
>
>Si une autre fonctionnalité de sécurité a déjà été configurée basée sur les clés de cryptage, la réplication des clés de cryptage peut endommager la configuration. Pour obtenir de l’aide, [contactez l’assistance clientèle](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support).

#### Réplication du référentiel {#repository-replication}

Il est possible de conserver le matériel clé stocké dans le référentiel, comme c’était le cas pour AEM version 6.2 et antérieure. Indiquez la propriété système suivante au premier démarrage de chaque instance AEM (qui crée le référentiel initial) :

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>Il est important de vérifier que l’agent de réplication [sur l’auteur](#replication-agents-on-author) est correctement configuré.

Avec le matériel clé stocké dans le référentiel, la manière de répliquer la clé de chiffrement de l’auteur vers d’autres instances est la suivante :

Utilisation de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Accédez à [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Sélectionnez `/etc/key`.
* Ouvrir l’onglet `Replication`
* Sélectionnez `Replicate`.

* [actualiser le lot Crypto Granite](#refresh-the-granite-crypto-bundle)

![ CRXDE Lite affichant le chemin /etc/key dans le panneau de gauche et l&#39;onglet Réplication sélectionné dans le panneau inférieur droit.](../assets/replicare-repository.png)

#### Actualisation du lot de chiffrement Granite {#refresh-the-granite-crypto-bundle}

* Sur chaque instance de publication, accédez à la [console web](/help/sites-deploying/configuring-osgi.md)

   * Par exemple, [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Localisez le lot `Adobe Granite Crypto Support` (com.adobe.granite.crypto)
* Sélectionnez **Actualiser**

![Actualisation du lot de prise en charge de Crypto Granite Adobe.](../assets/refresh-granite-bundle.png)

* Après un moment, une boîte de dialogue **Success** doit s’afficher :
  `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Si vous utilisez le serveur Apache HTTP, veillez à utiliser le nom de serveur correct pour toutes les entrées pertinentes.

En particulier, veillez à utiliser le nom de serveur correct, et non `localhost`, dans le `RedirectMatch`.

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

* AEM documentation [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr)
* [Installation du Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=fr)
* [Configuration de Dispatcher pour les communautés](/help/communities/dispatcher.md)
* [Problèmes connus](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentation sur les communautés connexes {#related-communities-documentation}

* Visitez [Administration de sites de communautés](/help/communities/administer-landing.md) pour en savoir plus sur la création d’un site de communauté, la configuration de modèles de site de communauté, la modération de contenu de communauté, la gestion des membres et la configuration de la messagerie.

* Consultez [Développement de communautés](/help/communities/communities.md) où vous pouvez en savoir plus sur la structure de composants sociaux (SCF) et la personnalisation des composants et fonctionnalités de communautés.

* Visitez la page [Création de composants de communautés](/help/communities/author-communities.md) où vous pouvez apprendre à créer et configurer des composants de communautés.

