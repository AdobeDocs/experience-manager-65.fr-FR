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
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 15%

---

# Vérifications et dépannage après une mise à niveau{#post-upgrade-checks-and-troubleshooting}

## Vérifications après mise à niveau {#post-upgrade-checks}

En procédant comme suit : [Mise à niveau statique](/help/sites-deploying/in-place-upgrade.md) les activités suivantes doivent être exécutées pour finaliser l&#39;upgrade. On suppose que AEM a été démarré avec le jar 6.5 et que la base de code mise à niveau a été déployée.

* [Vérification des journaux pour la réussite de la mise à niveau](#main-pars-header-290365562)

* [Vérification des lots OSGi](#main-pars-header-1637350649)

* [Vérification de la version Oak](#main-pars-header-1293049773)

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

Auparavant, la vérification de l’état de votre instance après la mise à niveau nécessitait une inspection minutieuse de divers fichiers journaux, de parties du référentiel et du pavé de lancement. La génération d’un rapport après la mise à niveau peut aider à détecter les mises à niveau défectueuses avant la mise en service.

L’objectif principal de cette fonctionnalité est de réduire la nécessité d’une interprétation manuelle ou d’une logique d’analyse complexe sur plusieurs points de terminaison requis pour que la mise à niveau soit réussie. La solution vise à fournir des informations non ambiguës pour que les systèmes d’automatisation externes réagissent au succès ou à l’échec identifié d’une mise à jour.

Plus précisément, il garantit que :

* Les échecs de mise à niveau détectés par la structure de mise à niveau sont centralisés dans un seul rapport de mise à niveau ;
* Le rapport de mise à niveau comprend des indicateurs sur l’intervention manuelle nécessaire.

Pour ce faire, des modifications ont été apportées à la manière dont les journaux sont générés dans la variable `upgrade.log` fichier .

Voici un exemple de rapport qui ne présente aucune erreur lors de la mise à niveau :

![1487887443006](assets/1487887443006.png)

Voici un exemple de rapport affichant un lot n’ayant pas été installé lors de la mise à niveau : 

![1487887532730](assets/1487887532730.png)

**error.log**

Le fichier error.log doit être soigneusement examiné pendant et après le démarrage de l’AEM à l’aide du fichier jar de la version cible. Les avertissements ou erreurs doivent être examinés. En général, il est préférable de rechercher les problèmes au début du journal. Les erreurs qui se produisent plus tard dans le journal peuvent être des effets secondaires d’une cause racine appelée plus tôt dans le fichier. En cas d’erreurs répétées et d’avertissements, reportez-vous à la section ci-dessous pour [Analyse des problèmes liés à la mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Vérification des lots OSGi {#verify-osgi-bundles}

Accédez à la console OSGi `/system/console/bundles` et vérifiez si des lots n’ont pas démarré. Si des lots sont à l’état installé, consultez la section `error.log` pour déterminer le problème racine.

### Vérification de la version Oak {#verify-oak-version}

Après la mise à niveau, vous devriez constater que la version d’Oak a été mise à jour vers **1.10.2**. Pour vérifier la version d’Oak, accédez à la console OSGi et observez la version associée aux lots Oak : Oak Core, Oak Commons, Oak Segment Tar.

### Inspection du dossier PreUpgradeBackup {#inspect-preupgradebackup-folder}

Pendant la mise à niveau, AEM tente de sauvegarder les personnalisations et de les stocker sous `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Pour afficher ce dossier dans CRXDE Lite, vous devrez peut-être [activation temporaire du CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

Le dossier avec l’horodatage doit posséder une propriété nommée `mergeStatus` avec la valeur `COMPLETED`. Le **to-process** Le dossier doit être vide et la variable **écrasé** indique les noeuds qui ont été remplacés lors de la mise à niveau. Le contenu situé sous le noeud leftovers indique le contenu qui n’a pas pu être fusionné en toute sécurité pendant la mise à niveau. Si votre mise en oeuvre dépend de l’un des noeuds enfants (et non déjà installé par votre package de code mis à niveau), ils doivent être fusionnés manuellement.

Désactivez le CRXDE Lite suivant cet exercice dans un environnement d’évaluation ou de production.

### Validation initiale des pages {#initial-validation-of-pages}

Effectuez une validation initiale sur plusieurs pages dans AEM. En cas de mise à niveau d’un environnement de création, ouvrez la page de démarrage et la page d’accueil ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Dans les environnements Auteur et Publication, ouvrez quelques pages d’application et testez-les pour qu’ils s’affichent correctement. En cas de problème, veuillez consulter le fichier `error.log` pour un dépannage.

### Application de packs de service AEM {#apply-aem-service-packs}

Appliquez les Service Packs AEM 6.5 appropriés s’ils ont été publiés.

### Migration des fonctionnalités AEM {#migrate-aem-features}

Plusieurs fonctions d’AEM nécessitent des étapes supplémentaires après la mise à niveau. Vous trouverez une liste complète de ces fonctionnalités et étapes pour les migrer dans AEM 6.5 sur la page [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) page.

### Vérification des configurations de maintenance planifiées {#verify-scheduled-maintenance-configurations}

#### Activation du nettoyage de la mémoire d’entrepôt de données {#enable-data-store-garbage-collection}

Si vous utilisez un entrepôt de données basé sur les fichiers, assurez-vous que la tâche de nettoyage de la mémoire d’entrepôt de données est activée et ajoutée à la liste de maintenance hebdomadaire. Suivez les instructions [suivantes](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Ceci n’est pas recommandé pour les installations de magasin de données personnalisé S3 ou lors de l’utilisation d’un entrepôt de données partagé.

#### Activation du nettoyage des révisions en ligne {#enable-online-revision-cleanup}

Si vous utilisez MongoMK ou le nouveau format de segment TarMK, assurez-vous que la tâche de nettoyage de révision est activée et ajoutée à la liste de maintenance quotidienne. Instructions décrites [here](/help/sites-deploying/revision-cleanup.md).

### Exécution du plan de test {#execute-test-plan}

Exécuter le plan de test détaillé par rapport à tel que défini [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) sous le **Procédure de test** .

### Activation des agents de réplication {#enable-replication-agents}

Une fois que l’environnement de publication a été entièrement mis à niveau et validé, activez les agents de réplication dans l’environnement de création. Vérifiez que les agents sont en mesure de se connecter aux instances de publication respectives. Consultez la section [Procédure de mise à niveau](/help/sites-deploying/upgrade-procedure.md) pour plus de détails sur l’ordre des événements. 

### Activation des tâches planifiées personnalisées {#enable-custom-scheduled-jobs}

À ce stade, toutes les tâches planifiées faisant partie de la base de code peuvent être activées.

## Analyse des problèmes liés à la mise à niveau {#analyzing-issues-with-upgrade}

Cette section contient des scénarios de problèmes que vous pouvez rencontrer lors de la procédure de mise à niveau vers AEM 6.3.

Ces scénarios doivent vous aider à déterminer la cause principale des problèmes liés à la mise à niveau et à identifier les problèmes spécifiques au projet ou au produit.

### Échec de la migration du référentiel  {#repository-migration-failing-}

La migration des données de CRX2 vers Oak doit être possible pour tout scénario commençant par les instances source basées sur CQ 5.4. Veillez à suivre exactement les instructions de mise à niveau de ce document qui incluent la préparation de la `repository.xml`, assurez-vous qu’aucun authentificateur personnalisé n’est démarré via JAAS et que l’instance a été vérifiée pour détecter des incohérences avant de démarrer la migration.

Si la migration échoue toujours, vous pouvez déterminer la cause principale en examinant la variable `upgrade.log`. Si le problème n’est pas encore connu, signalez-le au service clientèle.

### La mise à niveau n’a pas été exécutée {#the-upgrade-did-not-run}

Avant de commencer les étapes de préparation, veillez à exécuter la **source** d’abord en l’exécutant avec la commande Java™ -jar aem-quickstart.jar . Cela est nécessaire pour s’assurer que le fichier quickstart.properties est généré correctement. S’il est manquant, la mise à niveau ne fonctionnera pas. Vous pouvez également vérifier si le fichier est présent en regardant sous `crx-quickstart/conf` dans le dossier d’installation de l’instance source. En outre, lorsque vous lancez AEM mise à niveau, elle doit être exécutée avec la commande Java™ -jar aem-quickstart.jar . Le démarrage à partir d’un script de démarrage ne démarre pas AEM en mode de mise à niveau.

### Échec de la mise à jour des packages et des lots  {#packages-and-bundles-fail-to-update-}

Si l’installation des packages échoue pendant la mise à niveau, les lots qu’ils contiennent ne seront pas mis à jour non plus. Cette catégorie de problèmes est due à une mauvaise configuration de l’entrepôt de données. Elles apparaissent également comme **ERROR** et **WARN** messages dans le fichier error.log. Comme dans la plupart de ces cas, la connexion par défaut peut échouer, vous pouvez utiliser CRXDE directement pour examiner et trouver les problèmes de configuration.

### Certains lots AEM ne passent pas à l’état Principal {#some-aem-bundles-are-not-switching-to-the-active-state}

Si des lots ne démarrent pas, recherchez des dépendances insatisfaites.

Si ce problème est présent, mais qu’il est basé sur une installation de package ayant échoué et qui a entraîné la non-mise à niveau des lots, ils seront considérés comme incompatibles pour la nouvelle version. Pour plus d’informations sur la manière de résoudre ce problème, voir **Échec de la mise à jour des packages et des lots** ci-dessus.

Il est également recommandé de comparer la liste de lots d’une nouvelle instance d’AEM 6.5 avec celle mise à niveau pour détecter les lots qui n’ont pas été mis à niveau. Cela permettra de réduire le champ des recherches dans le fichier `error.log`.

### Lots personnalisés sans basculement vers l’état Principal {#custom-bundles-not-switching-to-the-active-state}

Si vos lots personnalisés ne passent pas à l’état principal, il est probable qu’il y ait du code qui n’importe pas l’API de modification. Cela entraîne le plus souvent des dépendances insatisfaites.

Les API supprimées doivent être marquées comme obsolètes dans l’une des versions précédentes. Vous trouverez des instructions sur la migration directe de votre code dans cet avis d’obsolescence. Adobe vise le contrôle de version sémantique lorsque cela est possible afin que les versions puissent indiquer les modifications entraînant une rupture.

Il est également préférable de vérifier si la modification qui a causé le problème était nécessaire et de l’annuler si ce n’est pas le cas. Vérifiez également si l’augmentation de version de l’exportation du package a été plus élevée que nécessaire, suite au contrôle de version sémantique strict.

### Interface utilisateur de Platform dysfonctionnelle {#malfunctioning-platform-ui}

Si certaines fonctionnalités de l’interface utilisateur ne fonctionnent pas correctement après la mise à niveau, vous devez d’abord vérifier les superpositions personnalisées de l’interface. Certaines structures peuvent avoir changé et la superposition peut nécessiter une mise à jour ou est obsolète.

Ensuite, recherchez les erreurs JavaScript pouvant être suivies jusqu’à des extensions ajoutées personnalisées qui sont connectées aux bibliothèques clientes. Il en va de même pour les CSS personnalisées qui peuvent poser des problèmes à la mise en page AEM.

Enfin, recherchez les erreurs de configuration que JavaScript peut ne pas être en mesure de gérer. C’est généralement le cas avec des extensions incorrectement désactivées.

### Fonctionnement des composants personnalisés, des modèles ou des extensions de l’interface utilisateur {#malfunctioning-custom-components-templates-or-ui-extensions}

En règle générale, les causes profondes de ces problèmes sont les mêmes que pour les lots qui ne sont pas démarrés ou les packages qui ne sont pas installés avec la seule différence que les problèmes commencent à se produire lors de la première utilisation des composants.

Pour gérer un code personnalisé erroné, vous devez d’abord effectuer des tests de détection de fumée pour identifier la cause. Une fois que vous l’avez trouvée, consultez les recommandations de cette section de la [rubrique] pour obtenir des moyens de corriger le problème.

### Personnalisations manquantes sous /etc {#missing-customizations-under-etc}

Les `/apps` et `/libs` sont correctement gérés par la mise à niveau mais les modifications sous `/etc` peuvent nécessiter une restauration manuelle à partir de `/var/upgrade/PreUpgradeBackup` après la mise à niveau. Veillez à inspecter cet emplacement pour identifier tout contenu devant être fusionné manuellement.

### Analyse des journaux error.log et upgrade.log  {#analyzing-the-error.log-and-upgrade.log}

Dans la plupart des cas, les logs doivent être consultés pour détecter la cause d&#39;un problème. Toutefois, avec les mises à niveau, il est également nécessaire de surveiller les problèmes de dépendance, car les anciens lots peuvent ne pas être mis à niveau correctement.

Pour ce faire, la meilleure méthode consiste à supprimer le fichier error.log en supprimant tous les messages qui ne sont pas liés au problème auquel vous êtes confronté. Vous pouvez le faire via un outil comme grep, en utilisant :

```shell
grep -v UnrelatedErrorString
```

Certains messages d’erreur peuvent ne pas être immédiatement explicatifs. Dans ce cas, la consultation du contexte dans lequel elles se produisent peut également aider à comprendre où l’erreur a été créée. Vous pouvez séparer l&#39;erreur à l&#39;aide des éléments suivants :

* `grep -B` pour l’ajout de lignes avant l’erreur

ou

* `grep -A` pour l’ajout de lignes après l’erreur.

Dans certains cas, des erreurs peuvent également être trouvées dans les messages AVERTISSEMENT, car il peut y avoir des cas valides menant à cet état et l’application n’est pas toujours en mesure de décider s’il s’agit d’une erreur réelle. Veillez également à consulter ces messages.

### Contacter le support technique d’Adobe {#contacting-adobe-support}

Si vous avez suivi les conseils de cette page et que vous rencontrez toujours des problèmes, contactez le support Adobe. Pour fournir le plus d’informations possible à l’ingénieur du support qui travaille sur votre dossier, veillez à inclure le fichier upgrade.log de votre mise à niveau.
