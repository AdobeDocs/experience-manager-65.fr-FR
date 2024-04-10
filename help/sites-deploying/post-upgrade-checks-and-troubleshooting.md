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
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1793'
ht-degree: 15%

---

# Vérifications et dépannage après une mise à niveau{#post-upgrade-checks-and-troubleshooting}

## Vérifications après mise à niveau {#post-upgrade-checks}

En suivant le [Mise à niveau statique](/help/sites-deploying/in-place-upgrade.md) les activités suivantes doivent être exécutées pour finaliser la mise à niveau. On suppose qu’AEM a été démarré avec le jar 6.5 et que la base de code mise à niveau a été déployée.

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

* [Exécuter le plan de test](#main-pars-header-1167972233)

### Vérification des journaux pour la réussite de la mise à niveau {#verify-logs-for-upgrade-success}

**upgrade.log**

Auparavant, l’inspection de l’état post-mise à niveau de votre instance nécessitait une inspection minutieuse de divers fichiers journaux, de parties du référentiel et du Launchpad. La génération d’un rapport après la mise à niveau peut permettre de détecter les mises à niveau défectueuses avant leur activation.

L’objectif principal de cette fonctionnalité est de réduire le besoin d’interprétation manuelle ou de logique d’analyse complexe sur plusieurs points d’entrée nécessaires pour qualifier la réussite d’une mise à niveau. La solution vise à fournir des informations claires aux systèmes d&#39;automatisation externes afin qu&#39;ils puissent réagir au succès ou à l&#39;échec identifié d&#39;une mise à jour.

Plus précisément, il garantit que :

* Les échecs de mise à niveau détectés par la structure de mise à niveau sont centralisés dans un seul rapport de mise à niveau ;
* Le rapport de mise à niveau comprend des indicateurs sur les interventions manuelles nécessaires.

Pour y remédier, la manière dont les journaux sont générés dans le a été modifiée `upgrade.log` fichier .

Voici un exemple de rapport qui n’affiche aucune erreur lors de la mise à niveau :

![1487887443006](assets/1487887443006.png)

Voici un exemple de rapport affichant un lot n’ayant pas été installé lors de la mise à niveau : 

![1487887532730](assets/1487887532730.png)

**error.log**

Le fichier error.log doit être soigneusement examiné pendant et après le démarrage d’AEM à l’aide du fichier jar de la version cible. Tous les avertissements ou erreurs doivent être examinés. En règle générale, il est préférable de rechercher les problèmes au début du journal. Les erreurs qui se produisent plus tard dans le journal peuvent en fait être les effets secondaires d’une cause principale appelée plus tôt dans le fichier. En cas d’erreurs et d’avertissements répétés, voir ci-dessous pour [Analyse des problèmes liés à la mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Vérification des lots OSGi {#verify-osgi-bundles}

Accédez à la console OSGi `/system/console/bundles` et vérifiez si des lots n’ont pas démarré. Si des lots sont installés, consultez le `error.log` pour déterminer le problème racine.

### Vérification de la version Oak {#verify-oak-version}

Après la mise à niveau, vous devriez voir que la version Oak a été mise à jour vers . **1.10.2**. Pour vérifier la version Oak, accédez à la console OSGi et examinez la version associée aux lots Oak : Oak Core, Oak Commons, Oak Segment Tar.

### Inspection du dossier PreUpgradeBackup {#inspect-preupgradebackup-folder}

Pendant la mise à niveau, AEM tente de sauvegarder les personnalisations et de les stocker sous `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Pour afficher ce dossier en CRXDE Lite, vous devez : [activer temporairement CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

Le dossier avec l’horodatage doit posséder une propriété nommée `mergeStatus` avec la valeur `COMPLETED`. Le **à traiter** le dossier doit être vide et le **écrasé** Le nœud indique quels nœuds ont été remplacés lors de la mise à niveau. Le contenu situé sous le nœud restants indique le contenu qui n’a pas pu être fusionné en toute sécurité pendant la mise à niveau. Si votre implémentation dépend de l’un des nœuds enfants (et n’est pas déjà installé par votre package de code mis à niveau), ils doivent être fusionnés manuellement.

Désactivez le CRXDE Lite à la suite de cet exercice dans un environnement d’évaluation ou de production.

### Validation initiale des pages {#initial-validation-of-pages}

Effectuez une validation initiale sur plusieurs pages dans AEM. En cas de mise à niveau d’un environnement de création, ouvrez la page de démarrage et la page d’accueil ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Dans les environnements de création et de publication, ouvrez quelques pages d’application et testez-les pour vous assurer qu’elles s’affichent correctement. En cas de problème, veuillez consulter le fichier `error.log` pour un dépannage.

### Application de packs de service AEM {#apply-aem-service-packs}

Appliquez tous les packs de services AEM 6.5 pertinents s’ils ont été publiés.

### Migration des fonctionnalités AEM {#migrate-aem-features}

Plusieurs fonctionnalités d’AEM nécessitent des étapes supplémentaires après la mise à niveau. Vous trouverez la liste complète de ces fonctionnalités et les étapes de leur migration dans AEM 6.5 sur le [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) page.

### Vérification des configurations de maintenance planifiées {#verify-scheduled-maintenance-configurations}

#### Activer le nettoyage de la mémoire du magasin de données {#enable-data-store-garbage-collection}

Si vous utilisez un magasin de données basé sur les fichiers, assurez-vous que la tâche de nettoyage de la mémoire du magasin de données est activée et ajoutée à la liste Maintenance hebdomadaire . Suivez les instructions [suivantes](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Cela n’est pas recommandé pour les installations d’entrepôt de données personnalisé S3 ou lors de l’utilisation d’un entrepôt de données partagé.

#### Activation du nettoyage des révisions en ligne {#enable-online-revision-cleanup}

Si vous utilisez MongoMK ou le nouveau format de segment TarMK, assurez-vous que la tâche Nettoyage des révisions est activée et ajoutée à la liste Maintenance quotidienne . Instructions décrites [ici](/help/sites-deploying/revision-cleanup.md).

### Exécuter le plan de test {#execute-test-plan}

Exécuter le plan de test détaillé par rapport à tel que défini [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) sous le **Procédure D&#39;Essai** section.

### Activation des agents de réplication {#enable-replication-agents}

Une fois l’environnement de publication entièrement mis à niveau et validé, activez les agents de réplication dans l’environnement de création. Vérifiez que les agents peuvent se connecter aux instances de publication respectives. Consultez la section [Procédure de mise à niveau](/help/sites-deploying/upgrade-procedure.md) pour plus de détails sur l’ordre des événements. 

### Activation des tâches planifiées personnalisées {#enable-custom-scheduled-jobs}

Toutes les tâches planifiées faisant partie de la base de code peuvent être activées à ce stade.

## Analyse Des Problèmes Liés À La Mise À Niveau {#analyzing-issues-with-upgrade}

Cette section présente certains des scénarios de problème auxquels vous pourriez être confronté lors de la procédure de mise à niveau vers AEM 6.3.

Ces scénarios doivent permettre de déterminer la cause première des problèmes liés à la mise à niveau et d’identifier les problèmes spécifiques aux projets ou aux produits.

### Échec de la migration du référentiel  {#repository-migration-failing-}

La migration des données de CRX2 à Oak doit être réalisable dans tous les scénarios, à commencer par les instances source basées sur CQ 5.4. Veillez à suivre scrupuleusement les instructions de mise à niveau de ce document, notamment la préparation du `repository.xml`, assurez-vous qu’aucun authentificateur personnalisé ne soit démarré via JAAS et que l’instance a été vérifiée pour les incohérences avant de démarrer la migration.

Si la migration est toujours en échec, vous pouvez déterminer la cause première en consultant le fichier `upgrade.log`. Si le problème n’est pas encore connu, signalez-le au service clientèle.

### La Mise À Niveau N’A Pas Été Exécutée {#the-upgrade-did-not-run}

Avant de commencer les étapes de préparation, veillez à exécuter la **source** installez d’abord en l’exécutant avec la commande Java™ -jar aem-quickstart.jar. Cela permet de s’assurer que le fichier quickstart.properties est généré correctement. S’il est manquant, la mise à niveau ne fonctionnera pas. Vous pouvez également vérifier si le fichier est présent en regardant sous `crx-quickstart/conf` dans le dossier d’installation de l’instance source. En outre, lors du démarrage d’AEM pour lancer la mise à niveau, celle-ci doit être exécutée avec la commande Java™ -jar aem-quickstart.jar. Démarrer à partir d’un script de démarrage ne démarrera pas AEM en mode de mise à niveau.

### Échec de la mise à jour des packages et des lots  {#packages-and-bundles-fail-to-update-}

Si l’installation des packages échoue pendant la mise à niveau, les lots qu’ils contiennent ne seront pas mis à jour non plus. Cette catégorie de problèmes est due à une configuration incorrecte du magasin de données. Ils apparaîtront également comme **ERREUR** et **WARN** messages dans le fichier error.log. Comme dans la plupart des cas, la connexion par défaut peut ne pas fonctionner, vous pouvez utiliser CRXDE directement pour examiner et trouver les problèmes de configuration.

### Certains lots AEM ne passent pas à l’état Actif {#some-aem-bundles-are-not-switching-to-the-active-state}

Si des lots ne démarrent pas, recherchez les dépendances non satisfaites.

Si ce problème existe, mais qu’il est lié à l’échec de l’installation d’un package, ce qui a eu pour conséquence que les lots n’ont pas été mis à niveau, ils seront considérés comme incompatibles avec la nouvelle version. Pour plus d’informations sur la résolution de ce problème, voir **Échec de la mise à jour des packages et des lots** ci-dessus.

Il est également recommandé de comparer la liste des lots d’une nouvelle instance AEM 6.5 avec celle de l’instance mise à niveau afin de détecter les lots qui n’ont pas été mis à niveau. Cela permettra de réduire le champ des recherches dans le fichier `error.log`.

### Lots personnalisés ne basculant pas vers le statut Actif {#custom-bundles-not-switching-to-the-active-state}

Si vos lots personnalisés ne passent pas à l’état actif, il est probable qu’une partie du code ne procède pas à l’importation de l’API de modification. Cela entraîne le plus souvent des dépendances insatisfaites.

L’API qui a été supprimée doit être marquée comme obsolète dans l’une des versions précédentes. Vous trouverez peut-être des instructions sur la migration directe de votre code dans cet avis d’obsolescence. L’Adobe vise le contrôle de version sémantique lorsque cela est possible, de sorte que les versions puissent indiquer des modifications avec rupture.

Il est également préférable de vérifier si la modification à l’origine du problème était nécessaire et de l’annuler si ce n’est pas le cas. Vérifiez également si l’augmentation de la version de l’exportation du package a été augmentée plus que nécessaire, après un contrôle de version sémantique strict.

### Interface utilisateur de Platform défectueuse {#malfunctioning-platform-ui}

Si certaines fonctionnalités de l’interface utilisateur ne fonctionnent pas correctement après la mise à niveau, vous devez d’abord vérifier les recouvrements personnalisés de l’interface. Certaines structures peuvent avoir changé et le recouvrement peut nécessiter une mise à jour ou être obsolète.

Ensuite, recherchez toutes les erreurs JavaScript qui peuvent être suivies jusqu’aux extensions ajoutées personnalisées qui sont connectées aux bibliothèques clientes. Il peut en être de même pour les feuilles CSS personnalisées qui peuvent entraîner des problèmes de mise en page AEM.

Enfin, recherchez les configurations incorrectes que JavaScript ne serait peut-être pas en mesure de gérer. C’est généralement le cas avec les extensions incorrectement désactivées.

### Mauvais fonctionnement des composants personnalisés, des modèles ou des extensions d’IU {#malfunctioning-custom-components-templates-or-ui-extensions}

En règle générale, les causes profondes de ces problèmes sont les mêmes que pour les lots qui ne sont pas démarrés ou les packages qui ne sont pas installés, à la seule différence que les problèmes commencent à se produire lors de la première utilisation des composants.

La façon de traiter un code personnalisé erroné consiste d’abord à effectuer des tests de vérification de la fumée pour identifier la cause. Une fois que vous l’avez trouvée, consultez les recommandations de cette section de la [rubrique] pour obtenir des moyens de corriger le problème.

### Personnalisations manquantes sous /etc {#missing-customizations-under-etc}

Les `/apps` et `/libs` sont correctement gérés par la mise à niveau mais les modifications sous `/etc` peuvent nécessiter une restauration manuelle à partir de `/var/upgrade/PreUpgradeBackup` après la mise à niveau. Veillez à inspecter cet emplacement pour identifier tout contenu devant être fusionné manuellement.

### Analyse des journaux error.log et upgrade.log {#analyzing-the-error.log-and-upgrade.log}

Dans la plupart des cas, les journaux doivent être consultés pour les erreurs afin de trouver la cause d’un problème. Cependant, avec les mises à niveau, il est également nécessaire de surveiller les problèmes de dépendance, car les anciens lots peuvent ne pas être mis à niveau correctement.

La meilleure façon d’y parvenir consiste à supprimer le fichier error.log de tous les messages qui ne sont normalement pas liés au problème rencontré. Vous pouvez le faire au moyen d’un outil tel que grep, en utilisant :

```shell
grep -v UnrelatedErrorString
```

Certains messages d’erreur peuvent ne pas s’expliquer immédiatement. Dans ce cas, l’examen du contexte dans lequel elles se produisent peut également aider à comprendre où l’erreur a été créée. Vous pouvez séparer l’erreur à l’aide de :

* `grep -B` pour l’ajout de lignes avant l’erreur

ou

* `grep -A` pour l’ajout de lignes après l’erreur.

Dans certains cas, des erreurs peuvent également se trouver dans des messages AVERTISSEMENT, car il peut y avoir des cas valides menant à cet état et l’application n’est pas toujours en mesure de décider s’il s’agit d’une erreur réelle. Veillez également à consulter ces messages.

### Contacter le support technique d’Adobe {#contacting-adobe-support}

Si vous avez consulté les conseils de cette page et que vous constatez toujours des problèmes, contactez le support technique d’Adobe. Pour fournir autant d’informations que possible à l’ingénieur du support qui travaille sur votre cas, veillez à inclure le fichier upgrade.log de votre mise à niveau.
