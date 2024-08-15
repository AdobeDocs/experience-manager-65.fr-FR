---
title: Vérifications et dépannage après une mise à niveau
description: Découvrez comment résoudre les problèmes qui peuvent apparaître après une mise à niveau.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: ceac2b52-6885-496d-9517-5fc7291ad070
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 99%

---

# Vérifications et dépannage après une mise à niveau{#post-upgrade-checks-and-troubleshooting}

## Vérifications après mise à niveau {#post-upgrade-checks}

Après la [mise à niveau statique](/help/sites-deploying/in-place-upgrade.md), les activités suivantes doivent être exécutées pour finaliser la mise à niveau. Nous supposons qu’AEM a été démarré avec jar 6.5 et que la base de code mise à niveau a été déployée.

* [Vérification des journaux pour la réussite de la mise à niveau](#main-pars-header-290365562)

* [Vérification des lots OSGi](#main-pars-header-1637350649)

* [Vérifier la version d’Oak](#main-pars-header-1293049773)

* [Inspection de dossier PreUpgradeBackup](#main-pars-header-988995987)

* [Validation initiale des pages](#main-pars-header-20827371)
* [Application de packs de service AEM](#main-pars-header-215142387)

* [Migration des fonctionnalités AEM](#main-pars-header-1434457709)

* [Vérification des configurations de maintenance planifiées](#main-pars-header-1552730183)

* [Activation des agents de réplication](#main-pars-header-823243751)

* [Activation des tâches planifiées personnalisées](#main-pars-header-244535083)

* [Exécution du plan de test](#main-pars-header-1167972233)

### Vérification des journaux pour la réussite de la mise à niveau {#verify-logs-for-upgrade-success}

**upgrade.log**

Auparavant, la vérification de l’état de votre instance après la mise à niveau nécessitait une inspection minutieuse de divers fichiers journaux, de parties du référentiel et du lanchpad. La génération d’un rapport après la mise à niveau permet de détecter les mises à niveau défectueuses avant la mise en service.

L’objectif principal de cette fonctionnalité est de réduire la nécessité d’une interprétation manuelle ou d’une logique d’analyse complexe sur plusieurs points d’entrée requis pour que la mise à niveau soit réussie. La solution vise à fournir des informations non ambiguës pour que les systèmes d’automatisation externes réagissent au succès ou à l’échec identifié d’une mise à jour.

Plus précisément, il garantit ce qui suit :

* les échecs de mise à niveau détectés par la structure de mise à niveau sont centralisés dans un seul rapport de mise à niveau ;
* le rapport de mise à niveau comprend des indicateurs sur l’intervention manuelle nécessaire.

Pour cela, les modifications ont été apportées à la façon dont les journaux sont générés dans le fichier `upgrade.log`.

Voici un exemple de rapport n’affichant aucune erreur lors de la mise à niveau :

![1487887443006](assets/1487887443006.png)

Voici un exemple de rapport affichant un lot n’ayant pas été installé lors de la mise à niveau : 

![1487887532730](assets/1487887532730.png)

**error.log**

Le fichier error.log doit être soigneusement examiné pendant et après le démarrage d’AEM à l’aide du fichier jar de la version cible. Les avertissements et erreurs doivent être examinés. En général, il est préférable de rechercher les problèmes au début du journal. Les erreurs qui se produisent plus tard dans le journal peuvent en fait être des effets secondaires d’une cause racine repérée plus tôt dans le fichier. En cas d’erreurs et d’avertissements répétés, reportez-vous à la section ci-dessous pour [Analyser les problèmes liés à la mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Vérification des lots OSGi {#verify-osgi-bundles}

Accédez à la console OSGi `/system/console/bundles` et vérifiez si des lots n’ont pas démarré. Si des lots sont installés, consultez le fichier `error.log` pour identifier le problème racine.

### Vérifier la version d’Oak {#verify-oak-version}

Après la mise à niveau, vous devez constater qu’Oak a été mis à jour vers la version **1.10.2**. Pour vérifier la version d’Oak, accédez à la console OSGi et examinez la version associée aux lots Oak : Oak Core, Oak Commons, Oak Segment Tar.

### Inspection du dossier PreUpgradeBackup {#inspect-preupgradebackup-folder}

Pendant la mise à niveau, AEM tente de sauvegarder les personnalisations et de les stocker sous `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Pour afficher ce dossier dans CRXDE Lite, vous avez peut-être besoin d’[activer temporairement CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

Le dossier avec l’horodatage doit posséder une propriété nommée `mergeStatus` avec la valeur `COMPLETED`. Le dossier **to-process** doit être vide et le nœud **overwritten** indique les nœuds qui ont été remplacés lors de la mise à niveau. Le contenu situé sous le nœud leftovers indique le contenu qui n’a pas pu être fusionné en toute sécurité pendant la mise à niveau. Si votre mise en œuvre dépend de l’un des nœuds enfants (et non déjà installé par votre package de code mis à niveau), ils doivent être fusionnés manuellement.

Désactivez CRXDE Lite après cet exercice dans un environnement d’évaluation ou de production.

### Validation initiale des pages {#initial-validation-of-pages}

Effectuez une validation initiale sur plusieurs pages dans AEM. En cas de mise à niveau d’un environnement de création, ouvrez la page de démarrage et la page d’accueil ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Dans les environnements de création et de publication, ouvrez quelques pages d’application et testez-les pour vous assurer qu’elles fonctionnent correctement. En cas de problème, veuillez consulter le fichier `error.log` pour un dépannage.

### Application de packs de service AEM {#apply-aem-service-packs}

Appliquez les Packs de services AEM 6.5 appropriés s’ils ont été publiés.

### Migration des fonctionnalités AEM {#migrate-aem-features}

Plusieurs fonctionnalités AEM nécessitent des étapes supplémentaires après la mise à niveau. Vous trouverez une liste complète de ces fonctionnalités et des étapes pour les migrer dans AEM 6.5 sur la page [Mise à niveau du code et personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md).

### Vérification des configurations de maintenance planifiées {#verify-scheduled-maintenance-configurations}

#### Activer la récupération de l’espace mémoire du magasin de données {#enable-data-store-garbage-collection}

Si vous utilisez un magasin de données basé sur les fichiers, assurez-vous que la tâche de nettoyage de l’espace mémoire du magasin de données est activée et ajoutée à la liste de maintenance hebdomadaire. Les instructions sont décrites sous [Nettoyage des révisions](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Cela n’est pas recommandé pour les installations de magasin de données personnalisé S3 ou lors de l’utilisation d’un magasin de données partagé.

#### Activation du nettoyage des révisions en ligne {#enable-online-revision-cleanup}

Si vous utilisez MongoMK ou le nouveau format de segment TarMK, assurez-vous que la tâche de nettoyage de révision est activée et ajoutée à la liste de maintenance quotidienne. Les instructions sont décrites sous [Nettoyage des révisions](/help/sites-deploying/revision-cleanup.md).

### Exécution du plan de test {#execute-test-plan}

Exécutez le plan de test détaillé tel que défini dans [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) dans la section **Procédure de test**.

### Activation des agents de réplication {#enable-replication-agents}

Une fois que l’environnement de publication a été entièrement mis à niveau et validé, activez les agents de réplication dans l’environnement de création. Vérifiez que les agents sont en mesure de se connecter aux instances de publication respectives. Consultez la section [Procédure de mise à niveau](/help/sites-deploying/upgrade-procedure.md) pour plus de détails sur l’ordre des événements. 

### Activation des tâches planifiées personnalisées {#enable-custom-scheduled-jobs}

À ce stade, toutes les tâches planifiées faisant partie de la base de code peuvent être activées.

## Analyser les problèmes liés à la mise à niveau {#analyzing-issues-with-upgrade}

Cette section contient des scénarios de problèmes que vous pouvez rencontrer lors de la procédure de mise à niveau vers AEM 6.3.

Ces scénarios doivent vous permettre de déterminer la cause principale des problèmes liés à la mise à niveau et à identifier les problèmes spécifiques au projet ou au produit.

### Échec de la migration du référentiel  {#repository-migration-failing-}

La migration des données de CRX2 à Oak doit être réalisable en toutes situations, à commencer par les instances source basées sur CQ 5.4. Assurez-vous de suivre de près les instructions de mise à niveau de ce document, y compris la préparation du fichier `repository.xml`. Ainsi, vous garantissez qu’aucun authentificateur personnalisé ne puisse démarrer via JAAS et que l’instance a été testée pour éviter les incohérences avant de démarrer la migration.

Si la migration est toujours en échec, vous pouvez déterminer la cause première en consultant le fichier `upgrade.log`. Si le problème n’est pas encore connu, signalez-le au service clientèle.

### La mise à niveau n’a pas été exécutée. {#the-upgrade-did-not-run}

Avant de commencer les étapes de préparation, veillez à exécuter d’abord l’instance **source** en l’exécutant avec la commande Java™ -jar aem-quickstart.jar. Cela est nécessaire pour s’assurer que le fichier quickstart.properties est généré correctement. S’il est manquant, la mise à niveau ne fonctionnera pas. Vous pouvez également vérifier si le fichier est présent en regardant sous `crx-quickstart/conf` dans le dossier d’installation de l’instance source. En outre, lorsque vous démarrez AEM pour lancer la mise à niveau, celui-ci doit être exécuté avec la commande Java™ -jar aem-quickstart.jar. Le démarrage à partir d’un script de démarrage ne démarre pas AEM en mode de mise à niveau.

### Échec de la mise à jour des packages et des lots  {#packages-and-bundles-fail-to-update-}

Si l’installation des packages échoue pendant la mise à niveau, les lots qu’ils contiennent ne seront pas mis à jour non plus. Cette catégorie de problèmes est due à une mauvaise configuration du magasin de données. Ils apparaissent également sous la forme de messages **ERROR** (erreur) et **WARN** (avertissement) dans error.log. Étant donné que dans la plupart de ces cas, la connexion par défaut peut ne pas fonctionner, vous pouvez utiliser CRXDE directement pour inspecter et trouver les problèmes de configuration.

### Certains lots AEM ne passent pas à l’état actif. {#some-aem-bundles-are-not-switching-to-the-active-state}

Si des lots ne démarrent pas, recherchez des dépendances insatisfaites.

Si ce problème est présent mais qu’il est dû à un échec de l’installation du package qui a entraîné la non-mise à niveau des lots, ils seront considérés comme incompatibles pour la nouvelle version. Pour plus d’informations sur la manière de résoudre ce problème, voir **Échec de la mise à jour des packages et des lots** ci-dessus.

Il est également recommandé de comparer la liste des lots d’une nouvelle instance AEM 6.5 avec celle de l’instance mise à niveau afin de détecter les lots qui n’ont pas été mis à niveau. Cela permettra de réduire le champ des recherches dans le fichier `error.log`.

### Les lots personnalisés ne passent pas à l’état actif {#custom-bundles-not-switching-to-the-active-state}

Si vos lots personnalisés ne passent pas à l’état actif, il est très probable qu’une partie du code omette d’importer l’API de modification. Cela entraîne le plus souvent des dépendances non satisfaites.

Les API supprimées doivent être marquées comme obsolètes dans l’une des versions précédentes. Vous trouverez des instructions sur la migration directe de votre code dans cet avis d’obsolescence. Adobe vise à employer un contrôle de version sémantique lorsque cela est possible afin que les versions puissent indiquer les modifications qui entraînent des incompatibilités.

Il est également préférable de vérifier si la modification qui a causé le problème était nécessaire et de l’annuler si ce n’est pas le cas. Vérifiez également si la nouvelle version du package d’exportation est plus élevée que nécessaire, à l’aide du contrôle de version sémantique strict.

### L’interface utilisateur de la plateforme ne fonctionne pas correctement {#malfunctioning-platform-ui}

Si certaines fonctionnalités de l’interface utilisateur ne fonctionnent pas correctement après la mise à niveau, vous devez en premier lieu vérifier les recouvrements personnalisés de l’interface. Certaines structures peuvent avoir été modifiées et les recouvrements peuvent nécessiter une mise à jour ou sont devenus obsolètes.

Ensuite, vérifiez la présence d’erreurs JavaScript pouvant provenir d’extensions ajoutées personnalisées connectées à des bibliothèques clientes. Cela concerne également les CSS personnalisées, qui peuvent engendrer des problèmes dans la mise en page AEM.

Enfin, vérifier la présence d’erreurs de configuration que JavaScript peut ne pas être en mesure de gérer. Cela se produit généralement lorsque des extensions ne sont pas correctement désactivées.

### Des composants personnalisés, modèles ou extensions de l’interface utilisateur ne fonctionnent pas correctement {#malfunctioning-custom-components-templates-or-ui-extensions}

En règle générale, l’origine de ces problèmes est la même que celle des lots qui ne démarrent pas ou des packages qui ne s’installent pas, la seule différence étant que les problèmes commencent à se produire lors de la première utilisation des composants.

Pour résoudre du code personnalisé erroné, vous devez d’abord effectuer des tests de détection de fumée pour identifier la cause du problème. Une fois que vous l’avez trouvée, consultez les recommandations de cette section de la [rubrique] pour obtenir des moyens de corriger le problème.

### Personnalisations manquantes sous /etc {#missing-customizations-under-etc}

Les `/apps` et `/libs` sont correctement gérés par la mise à niveau mais les modifications sous `/etc` peuvent nécessiter une restauration manuelle à partir de `/var/upgrade/PreUpgradeBackup` après la mise à niveau. Veillez à inspecter cet emplacement pour identifier tout contenu devant être fusionné manuellement.

### Analyse des journaux error.log et upgrade.log {#analyzing-the-error.log-and-upgrade.log}

Dans la plupart des cas, les journaux doivent être consultés afin d’y chercher des erreurs pour détecter la cause d’un problème. Toutefois, pour les mises à niveau, il est également nécessaire de surveiller les problèmes de dépendance, car les anciens lots peuvent ne pas être mis à niveau correctement.

Pour ce faire, la meilleure méthode consiste à élaguer le fichier error.log en supprimant tous les messages qui ne sont pas liés au problème auquel vous êtes confronté. Vous pouvez le faire à l’aide d’un outil comme grep, en utilisant la méthode suivante :

```shell
grep -v UnrelatedErrorString
```

Certains messages d’erreur peuvent ne pas être immédiatement descriptifs. Dans ce cas, regarder le contexte dans lequel ceux-ci se produisent peut vous aider à comprendre où l’erreur s’est créée. Vous pouvez séparer l&#39;erreur à l’aide des éléments suivants :

* `grep -B` pour l’ajout de lignes avant l’erreur

ou

* `grep -A` pour l’ajout de lignes après l’erreur.

Dans de rares cas, des erreurs peuvent également se trouver dans les messages AVERTISSEMENT, car il peut y avoir des cas valides qui mènent à cet état, et l’application n’est pas toujours capable de déterminer s’il s’agit d’une véritable erreur. Il est important que vous consultiez également ces messages.

### Contacter le support technique d’Adobe {#contacting-adobe-support}

Si vous avez suivi les conseils de cette page et que vous rencontrez toujours des problèmes, contactez l’assistance d’Adobe. Pour fournir le plus d’informations possible à l’ingénieur ou l’ingénieure de l’équipe d’assistance qui travaille sur votre incident, incluez le fichier upgrade.log de votre mise à niveau.
