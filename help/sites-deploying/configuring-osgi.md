---
title: Configurer OSGi
seo-title: Configuring OSGi
description: Le framework OSGi est un élément fondamental de la pile technologique d’Adobe Experience Manager (AEM). Il est utilisé pour contrôler les lots composites d’AEM et leur configuration. Cet article explique comment gérer les paramètres de configuration de ces lots.
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 36%

---

# Configurer OSGi{#configuring-osgi}

Le framework [OSGi](https://www.osgi.org/) est un élément fondamental de la pile technologique d’Adobe Experience Manager (AEM). Il est utilisé pour contrôler les lots composites d’AEM et leur configuration.

OSGi &quot;*fournit les primitives normalisées qui permettent de construire des applications à partir de petits composants réutilisables et collaboratifs. Ces composants peuvent être créés dans une application et déployés* ».

Cela permet une gestion facile des lots, car ils peuvent être arrêtés, installés et démarrés individuellement. Les interdépendances sont gérées automatiquement. Chaque composant OSGi (consultez [Spécification OSGi](https://docs.osgi.org/specification/)) est contenu dans l’un des différents lots.

Vous pouvez gérer les paramètres de configuration de ces lots en effectuant l’une des opérations suivantes :

* en utilisant la variable [Console web Adobe CQ](#osgi-configuration-with-the-web-console)
* using [fichiers de configuration](#osgi-configuration-with-configuration-files)
* configurant les [content-nodes (`sling:OsgiConfig`) dans le référentiel](#osgi-configuration-in-the-repository).

L’une ou l’autre des méthodes peut être utilisée bien qu’il existe des différences subtiles, principalement en relation avec les [modes d’exécution](/help/sites-deploying/configure-runmodes.md) :

* [Console Web Adobe CQ](#osgi-configuration-with-the-web-console)

   * La console web est l’interface standard pour la configuration OSGi. Il fournit une interface utilisateur pour la modification des différentes propriétés, dans laquelle les valeurs possibles peuvent être sélectionnées à partir de listes prédéfinies.

      De ce fait, il s’agit de la méthode la plus simple à utiliser.

   * Toutes les configurations effectuées avec la console Web sont appliquées immédiatement et s’appliquent à l’instance en cours, quel que soit le mode d’exécution en cours ou toute modification ultérieure du mode d’exécution.

* [fichiers de configuration](#osgi-configuration-with-configuration-files)

   * Contient les paramètres définis dans la console web.
   * Peuvent être incluses dans des modules de contenu pour une utilisation sur d’autres instances.

* [content-nodes (sling:osgiConfig) du référentiel](#osgi-configuration-in-the-repository)

   * Nécessite une configuration manuelle à l’aide de CRXDE Lite.
   * En raison des conventions de nommage des nœuds `sling:OsgiConfig`, vous pouvez lier la configuration à un [mode d’exécution](/help/sites-deploying/configure-runmodes.md) spécifique. Vous pouvez même enregistrer des configurations pour plusieurs modes d’exécution dans le même référentiel.
   * Toutes les configurations appropriées sont appliquées immédiatement (selon le mode d’exécution).

Quelle que soit la méthode utilisée, toutes ces méthodes de configuration :

* Assurez-vous que la copie ou la réplication du contenu du référentiel recrée des configurations identiques.
* Permet d’extraire des configurations vers FileVault ou Subversion ; soit pour des raisons de sécurité, soit pour d’autres mises à jour.
* Peuvent être enregistrées dans des packages à utiliser lors de la configuration d’autres instances.
* Permet d’effectuer des déploiements de configuration à l’aide de scripts pour propager les détails de configuration.

>[!NOTE]
>
>Les détails de certains paramètres importants sont répertoriés dans les [paramètres de la configuration OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configuration OSGi à l’aide de la console web {#osgi-configuration-with-the-web-console}

Le [Console web](/help/sites-deploying/web-console.md) dans AEM fournit une interface normalisée pour la configuration des lots. Le **Configuration** est utilisé pour configurer les lots OSGi. Il s’agit donc du mécanisme sous-jacent pour configurer les paramètres système d’AEM.

Toutes les modifications apportées sont immédiatement appliquées à la configuration OSGi appropriée. Aucun redémarrage n’est nécessaire.

>[!NOTE]
>
>Les modifications apportées dans la console Web sont enregistrées dans le référentiel sous la forme de [fichiers de configuration](#osgi-configuration-with-configuration-files). Ces fichiers peuvent être inclus dans des modules de contenu pour réutilisation dans d’autres installations.

>[!NOTE]
>
>Dans la console web, toute description qui mentionne les paramètres par défaut est liée aux valeurs par défaut de Sling.
>
>Adobe Experience Manager possède ses propres valeurs par défaut. Par conséquent, les valeurs par défaut définies peuvent différer des valeurs par défaut documentées dans la console.

Pour mettre à jour une configuration avec la console web :

1. Accédez au **Configuration** de la console web en effectuant l’une des opérations suivantes :

   * Ouvrant la console web à partir du lien du menu **Outil -> Opérations**. Après vous être connecté à la console, vous pouvez utiliser le menu déroulant de :

      **OSGi >**

   * L’URL directe ; par exemple :

      `http://localhost:4502/system/console/configMgr`
   Une liste s’affiche.

1. Sélectionnez le lot que vous souhaitez configurer en :

   * en cliquant sur **Modifier** icône pour ce lot
   * en cliquant sur **Nom** du lot

1. Une boîte de dialogue s’ouvre. Vous pouvez y apporter des modifications si nécessaire. Par exemple, définissez la variable **Niveau de journal** to `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Les mises à jour sont enregistrées dans le référentiel sous la forme de [fichiers de configuration](#osgi-configuration-with-configuration-files). Pour localiser ces fichiers par la suite afin de les inclure dans un module de contenu à utiliser sur une autre instance, par exemple, notez l’identité persistante ( `PID`).

1. Cliquez sur **Enregistrer**.

   Les modifications sont immédiatement appliquées à la configuration OSGi correspondante du système en cours d’exécution. Aucun redémarrage n’est requis.

   >[!NOTE]
   >
   >Vous pouvez désormais localiser le [fichiers de configuration](#osgi-configuration-with-configuration-files). Par exemple, pour inclure dans un module de contenu en vue de l’utiliser sur une autre instance.

## Configuration OSGi avec les fichiers de configuration {#osgi-configuration-with-configuration-files}

Les modifications de configuration effectuées à l’aide de la console Web sont conservées dans le référentiel en tant que fichiers de configuration (`.config`) sous :

`/apps`

Ces fichiers peuvent être inclus dans des packages de contenu et réutilisés sur d’autres instances.

>[!NOTE]
>
>Le format des fichiers de configuration est spécifique ; voir la section [Documentation Apache Sling](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) pour plus d’informations.
>
>Pour cette raison, il est recommandé de créer et de gérer le fichier de configuration en apportant des modifications réelles dans la console web.

La console web n’indique pas où, dans le référentiel, vos modifications ont été enregistrées, mais elles peuvent être facilement localisées :

1. Créez le fichier de configuration en [d’effectuer une modification initiale dans la console web ;](#osgi-configuration-with-the-web-console).
1. Ouvrez CRXDE Lite.
1. Dans le **Outils** menu, sélectionnez **Requête ...** .
1. Pour rechercher le PID de la configuration que vous avez mise à jour, envoyez une requête de **Type** `SQL`.

   Par exemple, la **console de gestion Apache Felix OSGi** possède l’identité persistante (PID) :

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   La requête SQL peut donc être :

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Le noeud du fichier de configuration s’affiche.

   Pour l’exemple ci-dessus :

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Vous pouvez ouvrir ce fichier pour afficher vos modifications, mais pour éviter les erreurs de saisie, il est recommandé d’effectuer des modifications avec la console.

1. Vous pouvez désormais créer un module de contenu, contenant ce noeud, et l’utiliser selon les besoins sur vos autres instances.

## Configuration OSGi dans le référentiel {#osgi-configuration-in-the-repository}

Outre l’utilisation de la console web, vous pouvez également définir des détails de configuration dans le référentiel. Cela vous permet de configurer facilement les différents modes d’exécution.

Vous réalisez ces configurations en créant des nœuds `sling:OsgiConfig` dans le référentiel à titre de références dans le système. Ces noeuds reflètent les configurations OSGi et une interface utilisateur leur est formée. Pour mettre à jour les données de configuration, mettez à jour les propriétés du noeud.

Si vous modifiez les données de configuration dans le référentiel, les modifications sont immédiatement appliquées à la configuration OSGi correspondante. C&#39;est comme si les modifications avaient été effectuées à l&#39;aide de la console web, avec la validation et les contrôles de cohérence appropriés. Ce workflow s’applique également à l’action de copie d’une configuration depuis `/libs/` to `/apps/`.

Comme le même paramètre de configuration se trouve à plusieurs endroits, le système :

* recherche tous les nœuds de type `sling:OsgiConfig` ;
* filtre selon le nom du service ;
* filtre selon le mode d’exécution.

>[!NOTE]
>
>Lire aussi [comment définir une configuration basée sur un référentiel pour une instance spécifique uniquement](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=en).

### Ajout d’une nouvelle configuration au référentiel {#adding-a-new-configuration-to-the-repository}

#### Ce que vous devez savoir {#what-you-need-to-know}

Pour ajouter une configuration au référentiel, vous devez connaître les informations suivantes :

1. L’**identité persistante** (PID) du service.

   Référencez le champ **Configurations** dans la console Web. Le nom est indiqué entre parenthèses après le nom du lot (ou dans les **Informations de configuration** vers le bas de la page).

   Par exemple, créez un nœud `com.day.cq.wcm.core.impl.VersionManagerImpl.` pour configurer le **Gestionnaire de versions de gestion de contenu Web d’AEM**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Est spécifique à [mode d’exécution](/help/sites-deploying/configure-runmodes.md) obligatoire ? Créez le dossier :

   * `config` : pour tous les modes d’exécution.
   * `config.author` : pour l’environnement de création
   * `config.publish` : pour l’environnement de publication
   * `config.<run-mode>` - En fonction des besoins

1. Est un **Configuration** ou **Configuration d’usine** nécessaire ?
1. Les paramètres individuels à configurer, y compris toute définition de paramètre existante qui doit être recréée.

   Référencez le champ des paramètres individuels dans la console Web. Le nom s’affiche entre parenthèses pour chaque paramètre.

   Par exemple, créez une propriété 
   `versionmanager.createVersionOnActivation` pour configurer **Créer une version lors de l’activation**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Existe-t-il une configuration dans `/libs`? Pour répertorier toutes les configurations de votre instance, utilisez l’outil **Requête** de CRXDE Lite pour envoyer la requête SQL suivante :

   `select * from sling:OsgiConfig`

   Si tel est le cas, cette configuration peut être copiée vers ` /apps/<yourProject>/`, puis personnalisé dans le nouvel emplacement.

#### Création de la configuration dans le référentiel {#creating-the-configuration-in-the-repository}

Pour ajouter réellement la nouvelle configuration au référentiel :

1. Utilisez CRXDE Lite pour accéder à :

   ` /apps/<yourProject>`

1. S’il n’existe pas, créez la variable `config` folder ( `sling:Folder`) :

   * `config` : applicable à tous les modes d’exécution
   * `config.<run-mode>` : spécifique à un mode d’exécution

1. Sous ce dossier, créez un noeud :

   * Type : `sling:OsgiConfig`
   * Nom : l’identité persistante (PID) ;

      par exemple, pour le Gestionnaire de versions de gestion de contenu Web d’AEM, utilisez `com.day.cq.wcm.core.impl.VersionManagerImpl`.
   >[!NOTE]
   >
   >Lors de la configuration d’usine, ajoutez `-<identifier>` au nom.
   >
   >Comme dans : `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Où `<identifier>` est remplacé par du texte libre que vous devez entrer pour l’instance (vous ne pouvez pas omettre cette information) ; par exemple :
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Pour chaque paramètre à configurer, créez une propriété sur ce noeud :

   * Nom : le nom du paramètre, comme indiqué dans la console Web ; le nom est indiqué entre parenthèses à la fin de la description du champ. Par exemple, pour `Create Version on Activation`, utilisez `versionmanager.createVersionOnActivation`.
   * Type : selon les cas.
   * Valeur : selon les besoins.

   Vous ne devez créer des propriétés que pour les paramètres que vous souhaitez configurer, d’autres utilisent toujours les valeurs par défaut telles qu’elles sont définies par AEM.

1. Enregistrez toutes les modifications.

   Les modifications sont appliquées lorsque le noeud est mis à jour en redémarrant le service (comme pour les modifications effectuées dans la console web).

>[!CAUTION]
>
>Ne modifiez rien dans la variable `/libs` chemin d’accès.

>[!CAUTION]
>
>Le chemin complet d&#39;une configuration doit être correct pour être lu au démarrage.

## Détails de la configuration {#configuration-details}

### Ordre de résolution au démarrage {#resolution-order-at-startup}

L’ordre de priorité suivant est utilisé :

1. Nœuds de référentiel sous `/apps/*/config...`, que ce soit avec le type `sling:OsgiConfig` ou les fichiers de propriété.

1. Nœuds de référentiel avec le type `sling:OsgiConfig` sous `/libs/*/config...`. (définitions prêtes à l’emploi).

1. Tout fichier `.config` provenant de `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. sur le système de fichiers local.

Une configuration générique dans `/libs` peut être masqué par une configuration spécifique au projet dans `/apps`.

### Ordre de résolution à l’exécution {#resolution-order-at-runtime}

Les modifications de configuration effectuées pendant l’exécution du système déclenchent un rechargement avec la configuration modifiée.

L’ordre de priorité suivant s’applique :

1. La modification d’une configuration dans la console web prend effet immédiatement, car elle est prioritaire au moment de l’exécution.
1. Modification d’une configuration dans `/apps` prend effet immédiatement.
1. Modification d’une configuration dans `/libs` prend effet immédiatement, sauf si une configuration dans `/apps`.

### Résolution de plusieurs modes d’exécution {#resolution-of-multiple-run-modes}

Pour les configurations spécifiques au mode d’exécution, plusieurs modes d’exécution peuvent être combinés. Vous pouvez par exemple créer des dossiers de configuration dans le style suivant :

`/apps/*/config.<runmode1>.<runmode2>/`

Les configurations de ces dossiers sont appliquées si tous les modes d’exécution correspondent à un mode d’exécution défini au démarrage.

Par exemple, si une instance a été lancée avec les modes d’exécution `author,dev,emea`, noeuds de configuration dans `/apps/*/config.emea`, `/apps/*/config.author.dev/`, et `/apps/*/config.author.emea.dev/` est appliqué, tandis que les noeuds de configuration dans `/apps/*/config.author.asean/` et `/config/author.dev.emea.noldap/` ne sont pas appliquées.

Si plusieurs configurations correspondant au même PID sont applicables, la configuration comportant le nombre le plus élevé de modes d’exécution correspondants est appliquée.

Par exemple, si une instance a été lancée avec les modes d’exécution `author,dev,emea`, et les deux `/apps/*/config.author/` et `/apps/*/config.emea.author/` définir une configuration pour
`com.day.cq.wcm.core.impl.VersionManagerImpl`, la configuration dans `/apps/*/config.emea.author/` est appliquée.

La granularité de cette règle se trouve au niveau du PID.
Vous ne pouvez pas définir certaines propriétés pour le même PID dans `/apps/*/config.author/` et des propriétés plus spécifiques dans `/apps/*/config.emea.author/` pour le même PID.
La configuration comportant le plus grand nombre de modes d’exécution correspondants est effective pour l’ensemble du PID.

### Configurations standard {#standard-configurations}

La liste suivante présente une petite sélection des configurations disponibles (dans une installation standard) dans le référentiel :

* Auteur - Filtre de gestion de contenu Web d’AEM :

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publication - Filtre de gestion de contenu Web d’AEM :

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publication - Statistiques de page de gestion de contenu Web d’AEM :

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Comme ces configurations se trouvent dans `/libs`, elles ne doivent pas être modifiées directement, mais copiées dans votre zone d’application (`/apps`) avant d’être personnalisées.

Pour répertorier tous les nœuds de configuration de votre instance, utilisez la fonctionnalité **Requête** de CRXDE Lite pour envoyer la requête SQL suivante :

`select * from sling:OsgiConfig`

### Persistance de la configuration {#configuration-persistence}

* Si vous modifiez une configuration par l’intermédiaire de la console Web, elle est (généralement) enregistrée dans le référentiel :

   `/apps/{somewhere}`

   * Par défaut, `{somewhere}` est `system/config`, la configuration est donc enregistrée sur

      `/apps/system/config`

   * Cependant, si vous modifiez une configuration qui provient initialement d’un autre emplacement du référentiel : par exemple :

      /libs/foo/config/someconfig

      La configuration mise à jour est ensuite enregistrée à l’emplacement d’origine ; par exemple :

      `/apps/foo/config/someconfig`

* Les paramètres modifiés par `admin` sont enregistrés dans les fichiers `*.config` sous :

   ```
      /crx-quickstart/launchpad/config
   ```

   * Cette zone est les données privées de l’administrateur de configuration OSGi et contient tous les détails de configuration spécifiés par `admin`, quelle que soit la manière dont ils sont entrés dans le système.
   * Cette zone est un détail de mise en oeuvre et vous ne devez jamais modifier directement ce répertoire.
   * Toutefois, il est utile de connaître l’emplacement de ces fichiers de configuration afin que des copies puissent être prises pour une sauvegarde ou plusieurs installations, ou les deux :

      * Console de gestion OSGi Apache Felix

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Référentiel client CRX Sling

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Ne modifiez jamais les dossiers ou les fichiers sous :
>
>`/crx-quickstart/launchpad/config`
