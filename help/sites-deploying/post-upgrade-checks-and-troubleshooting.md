---
title: 'Vérifications et dépannage après une mise à niveau '
seo-title: 'Vérifications et dépannage après une mise à niveau '
description: Découvrez comment résoudre les problèmes qui peuvent apparaître à la suite d’une mise à niveau.
seo-description: Découvrez comment résoudre les problèmes qui peuvent apparaître à la suite d’une mise à niveau.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 95%

---


# Vérifications et dépannage après une mise à niveau {#post-upgrade-checks-and-troubleshooting}

## Vérifications après une mise à niveau {#post-upgrade-checks}

Après la [mise à niveau statique](/help/sites-deploying/in-place-upgrade.md), les activités suivantes doivent être exécutées pour finaliser la mise à niveau. Nous partons du principe qu’AEM a été démarré avec le jar 6.5 et que la base de code mis à niveau a été déployée.

* [Vérifiez les journaux pour la réussite de la mise à niveau](#main-pars-header-290365562)

* [Vérification des lots OSGi](#main-pars-header-1637350649)

* [Vérification de la version Oak](#main-pars-header-1293049773)

* [Inspection du dossier PreUpgradeBackup](#main-pars-header-988995987)

* [Validation initiale des pages](#main-pars-header-20827371)
* [Application des modules de service AEM](#main-pars-header-215142387)

* [Migration des fonctionnalités AEM](#main-pars-header-1434457709)

* [Vérification des configurations de maintenance planifiées](#main-pars-header-1552730183)

* [Activation des agents de réplication](#main-pars-header-823243751)

* [Activation des tâches planifiées personnalisées](#main-pars-header-244535083)

* [Exécution du plan de test](#main-pars-header-1167972233)

### Vérification des journaux pour la réussite de la mise à niveau {#verify-logs-for-upgrade-success}

**upgrade.log**

Auparavant, la vérification de l’état de votre instance après la mise à niveau nécessitait une inspection soignée des différents fichiers de journal, des parties du référentiel et du pavé de lancement. La génération d’un rapport après la mise à niveau peut aider à détecter des mises à niveau défectueuses avant de les publier.

Le principal objectif de cette fonction est de réduire le besoin d’interprétation manuelle ou d’analyse logique complexe sur plusieurs points de terminaison nécessaires pour juger la réussite d’une mise à niveau. La solution vise à fournir des informations non ambiguës permettant aux systèmes externes d’automatisation de réagir en fonction de la réussite ou de l’échec identifié d’une mise à niveau.

Plus spécifiquement, cela garantit que :

* Les échecs de mise à niveau détectés par la structure de mise à niveau sont centralisés dans un seul rapport de mise à niveau ;
* Le rapport de mise à niveau inclut des indicateurs sur une intervention manuelle nécessaire.

Pour cela, les modifications ont été apportées à la façon dont les journaux sont générés dans le fichier `upgrade.log`.

Voici un exemple de rapport n’affichant aucune erreur lors de la mise à niveau :

![1487887443006](assets/1487887443006.png)

Voici un exemple de rapport affichant un lot n’ayant pas été installé lors de la mise à niveau : 

![1487887532730](assets/1487887532730.png)

**error.log**

Le fichier error.log doit être soigneusement passé en revue pendant et après le démarrage d’AEM à l’aide du jar de la version cible. Les avertissements ou les erreurs doivent être vérifiés. En général, il est conseillé de rechercher les problèmes au début du journal. Les erreurs qui surviennent par la suite dans le journal peuvent en réalité être des effets secondaires d’une cause principale signalée tôt au début du fichier. Si des erreurs et des avertissements s’affichent à plusieurs reprises, voir la section ci-dessous [Analyse des problèmes avec la mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Vérification des lots OSGi {#verify-osgi-bundles}

Accédez à la console OSGi `/system/console/bundles` et vérifiez si des lots ne sont pas démarrés. Si des lots sont installés, consultez le fichier `error.log` pour identifier le problème racine.

### Vérifiez la version Oak {#verify-oak-version}

Après la mise à niveau, vous devez constater qu’Oak a été mis à jour vers la version **1.10.2**. Pour vérifier la version Oak, accédez à la console OSGi et inspectez la version associée aux lots Oak : Oak Core, Oak Commons, Oak Segment Tar.

### Inspectez le fichier PreUpgradeBackup {#inspect-preupgradebackup-folder}

Au cours de la mise à niveau, AEM tentera de sauvegarder les personnalisations et de les stocker sous `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Pour afficher ce dossier dans CRXDE Lite, vous avez peut-être besoin d’[activer temporairement CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

Le dossier avec l’horodatage doit posséder une propriété nommée `mergeStatus` avec la valeur `COMPLETED` (TERMINÉ). Le dossier **to-process** doit être vide et le nœud **overwritten** (remplacé) indique les nœuds qui ont été remplacés lors de la mise à niveau. Le contenu sous le nœud **leftovers** indique le contenu qui ne peut pas être fusionné en toute sécurité lors de la mise à niveau. Si votre implémentation dépend de nœuds enfants (pas déjà installés par votre module de code mis à niveau), ils doivent être fusionnés manuellement.

Désactivez CRXDE Lite après cet exercice si vous êtes dans un environnement intermédiaire ou de production.

### Validation initiale des pages  {#initial-validation-of-pages}

Effectuez une première validation de plusieurs pages dans AEM. Si vous mettez à niveau un environnement d’auteur, ouvrez la page de Début et la page d’accueil ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Dans les environnements de création et de publication, ouvrez quelques pages d’application et testez-les pour vous assurer qu’elles fonctionnent correctement. En cas de problème, veuillez consulter le fichier `error.log` pour un dépannage.

### Appliquez les modules de service AEM {#apply-aem-service-packs}

Appliquez tout Service Pack AEM 6.5 qui a été publié, le cas échéant.

### Migration des fonctions AEM {#migrate-aem-features}

Plusieurs fonctions AEM requièrent des étapes supplémentaires après la mise à niveau. Une liste complète de ces fonctions et les étapes permettant de les migrer dans AEM 6.5 se trouve sur la page [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md).

### Vérifiez les configurations de maintenance planifiée {#verify-scheduled-maintenance-configurations}

#### Activation du nettoyage de la mémoire d’entrepôt de données {#enable-data-store-garbage-collection}

Si vous utilisez un entrepôt de données de fichiers, assurez-vous que la tâche de nettoyage de la mémoire d’entrepôt de données est activée et ajoutée à la liste de maintenance hebdomadaire. Suivez les instructions [suivantes](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Cette méthode n’est pas recommandée pour les installations d’entrepôt des données personnalisées s3 ni lors de l’utilisation d’un entrepôt de données partagé.

#### Activation du nettoyage des révisions en ligne  {#enable-online-revision-cleanup}

Si vous utilisez MongoMK ou le nouveau format de segment TarMK, assurez-vous que la tâche de nettoyage des révisions est activée et ajoutée à la liste de maintenance quotidienne. Les instructions sont décrites [ici](/help/sites-deploying/revision-cleanup.md).

### Exécution du plan de test  {#execute-test-plan}

Exécutez le plan de test détaillé tel que défini dans [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md) dans la section **Procédure de test**.

### Activation des agents de réplication  {#enable-replication-agents}

Une fois que l’environnement de publication a été entièrement mis à niveau et validé, activez les agents de réplication dans l’environnement de création. Vérifiez que les agents peuvent se connecter aux instances de publication respectives. Voir [Procédure de mise à niveau](/help/sites-deploying/upgrade-procedure.md) pour plus de détails sur l’ordre des événements. 

### Activez les tâches planifiées personnalisées {#enable-custom-scheduled-jobs}

Toutes les tâches planifiées dans le cadre de la base de code peuvent être activées.

## Analyse des problèmes de la mise à niveau  {#analyzing-issues-with-upgrade}

Cette section comporte des scénarios de problèmes que l’on peut rencontrer au cours d’une procédure de mise à niveau vers AEM 6.3.

Ces scénarios doivent vous permettre de trouver la cause première des problèmes de mise à niveau et d’identifier des problèmes spécifiques à un projet ou un produit.

### Échec de la migration du référentiel  {#repository-migration-failing-}

La migration des données de CRX2 à Oak doit être réalisable en toutes situations, à commencer par les instances source basées sur CQ 5.4. Assurez-vous de suivre de près les instructions de mise à niveau de ce document, y compris la préparation du fichier `repository.xml`. Ainsi, vous garantissez qu’aucun authentificateur personnalisé ne puisse démarrer via JAAS et que l’instance a été testée pour éviter les incohérences avant de démarrer la migration.

Si la migration est toujours en échec, vous pouvez déterminer la cause première en consultant le fichier `upgrade.log`. Si le problème n’est pas encore connu, signalez-le au service clientèle.

### Échec de l’exécution de la mise à niveau  {#the-upgrade-did-not-run}

Avant de lancer les étapes de préparation, assurez-vous d’abord de lancer l’instance **source** en l’exécutant avec la commande Java aem-quickstart.jar. Cela est nécessaire pour vous assurer que le fichier quickstart.properties est généré correctement. Autrement, la mise à niveau ne peut pas fonctionner. Vous pouvez également vérifier si le fichier est présent en regardant sous `crx-quickstart/conf` dans le dossier d’installation de l’instance source. En outre, le démarrage d’AEM pour lancer la mise à niveau doit être exécuté avec la commande Java -jar aem-quickstart.jar. Le lancement à partir d’un script de démarrage ne permettra pas de démarrer AEM en mode de mise à niveau.

### Échec de la mise à jour des modules et des lots   {#packages-and-bundles-fail-to-update-}

Si l’installation des modules échoue au cours de la mise à niveau, les lots qu’ils contiennent ne sont également pas mis à jour. Ce type d’erreur provient généralement d’une mauvaise configuration du magasin de données. Il apparaît sous la forme de messages nommés **ERROR** et **WARN** dans le journal error.log. Comme, dans la plupart des cas, la connexion par défaut ne fonctionne pas, vous pouvez utiliser CRXDE directement afin d’inspecter et de rechercher les problèmes de configuration.

### Certains lots AEM ne passent pas à l’état actif  {#some-aem-bundles-are-not-switching-to-the-active-state}

En présence de lots qui ne démarrent pas, vous devez rechercher des dépendances non respectées.

Si ce problème est présent mais qu’il est basé sur une installation de module défaillante qui a empêché la mise à niveau des lots, ces derniers ne sont pas compatibles avec la nouvelle version. Pour plus d’informations sur la résolution de ce problème, voir **Échec de la mise à jour de modules et de lots** ci-dessus.

Il est également recommandé de comparer la liste des lots d’une instance AEM 6.5 neuve avec celle de l’instance mise à niveau afin de détecter les lots qui n’ont pas été mis à niveau. Cela permettra de réduire le champ des recherches dans le fichier `error.log`.

### Les lots personnalisés ne passent pas à l’état actif {#custom-bundles-not-switching-to-the-active-state}

Si les lots personnalisés ne passent pas à l’état actif, il est probable qu’une partie du code ne procède pas à l’importation de l’API de modification, ce qui conduit le plus souvent à des dépendances non respectées.

L’API qui a été supprimée doit être marquée comme obsolète dans l’une des versions précédentes. Vous trouverez des instructions sur une migration directe du code dans la notice d’obsolescence. Adobe cherche à obtenir une création de versions sémantique, le cas échéant, afin que les versions puissent indiquer les modifications de rupture.

Il est également recommandé de vérifier si la modification qui a causé le problème était absolument nécessaire et l’annuler si ce n’est pas le cas. Vérifiez également si l’augmentation de version de l’exportation du module a été plus importante que nécessaire, en suivant une création de versions sémantique.

### Dysfonctionnement de l’interface utilisateur de la plate-forme  {#malfunctioning-platform-ui}

Lorsque certaines fonctionnalités de l’interface utilisateur ne fonctionnent pas correctement après la mise à niveau, vous devez tout d’abord vérifier les recouvrements personnalisés de l’interface. Certaines structures peuvent avoir changé et le recouvrement peut nécessiter une mise à jour ou est obsolète.

Ensuite, recherchez les erreurs Javascript qui peuvent être attribuées à des extensions ajoutées personnalisées qui sont raccrochées à clientlibs. Il en va de même avec le CSS personnalisé qui peut poser problèmes au recouvrement AEM.

Enfin, recherchez une configuration incorrecte que Javascript n’arrive pas à gérer. C’est généralement le cas avec des extensions incorrectement désactivées.

### Dysfonctionnement de composants, modèles ou extensions de l’interface utilisateur personnalisée  {#malfunctioning-custom-components-templates-or-ui-extensions}

Dans la plupart des cas, les causes premières de ces problèmes sont les mêmes que pour les lots qui ne sont pas démarrés ou les modules non installés avec pour seule différence que les problèmes commencent à se produire lors de la première utilisation des composants.

La manière de gérer le code personnalisé erroné consiste à réaliser en premier lieu un test de détection de fumée afin d’identifier la cause. Une fois que vous l’avez trouvé, consultez les recommandations de cette section [link] de l’article pour savoir comment les corriger.

### Personnalisations manquantes sous /etc {#missing-customizations-under-etc}

`/apps` et  `/libs` sont bien gérées par la mise à niveau, mais les modifications apportées à la version  `/etc` peuvent nécessiter une restauration manuelle à partir de  `/var/upgrade/PreUpgradeBackup` la mise à niveau. Veillez à inspecter cet emplacement pour identifier tout contenu devant être fusionné manuellement.

### Analyse des journaux error.log et upgrade.log  {#analyzing-the-error.log-and-upgrade.log}

Dans la plupart des cas, les journaux doivent être consultés à la recherche d’erreurs afin de trouver la cause d’un problème. Néanmoins, dans le cas d’une mise à niveau, il est également requis de surveiller les problèmes de dépendance car des lots anciens n’ont peut-être pas été mis à niveau correctement.

Cette surveillance consiste à éplucher le journal error.log en supprimant tous les messages qui ne sont pas liés au problème auquel vous êtes confronté. Vous pouvez réaliser cette opération à l’aide d’un outil comme grep, en utilisant la ligne de code :

```shell
grep -v UnrelatedErrorString
```

Certains messages d’erreur peuvent ne pas être immédiatement explicatifs. Dans ce cas, l’étude du contexte dans lequel ils se sont produits peut également aider à comprendre où l’erreur a été créée. Vous pouvez séparer l’erreur à l’aide de :

* `grep -B` pour ajouter des lignes avant l&#39;erreur ;

ou

* `grep -A` pour ajouter des lignes après.

Dans quelques rares cas, vous rencontrez des messages WARN accompagnant l’erreur. En effet, l’erreur peut provenir d’un problème réel et l’application n’est pas toujours en mesure de déterminer s’il s’agit d’une véritable erreur. Assurez-vous de consulter également ces messages.

### Contacter le support technique d’Adobe  {#contacting-adobe-support}

Si vous avez consulté les recommandations de cette page, mais continuez toujours à avoir des problèmes, veuillez vous adresser au support technique d’Adobe. Pour fournir le plus d’information possible au technicien d’assistance qui s’occupe de votre cas, veillez à inclure le fichier upgrade.log de votre mise à niveau.
