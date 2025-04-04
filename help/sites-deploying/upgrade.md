---
title: Mise à niveau vers Adobe Experience Manager 6.5
description: Découvrez les principes de base de la mise à niveau d’une installation Adobe Experience Manager (AEM) plus ancienne vers AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 100%

---

# Mise à niveau vers Adobe Experience Manager (AEM) 6.5 {#upgrading-to-aem}

Cette section décrit la mise à niveau d’une installation AEM vers AEM 6.5 :

* [Planification de la mise à niveau](/help/sites-deploying/upgrade-planning.md)
* [Évaluation de la complexité de la mise à niveau à l’aide de l’outil de détection des motifs](/help/sites-deploying/pattern-detector.md)
* [Rétrocompatibilité dans AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Procédure de mise à niveau](/help/sites-deploying/upgrade-procedure.md)
* [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Tâches de maintenance avant la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Exécution d’une mise à niveau statique](/help/sites-deploying/in-place-upgrade.md)
* [Vérifications et dépannage après une mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Mises à niveau possibles](/help/sites-deploying/sustainable-upgrades.md)
* [Migration différée du contenu](/help/sites-deploying/lazy-content-migration.md)
* [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md)

Pour une référence conviviale aux instances d’AEM incluses dans ces procédures, les termes suivants sont utilisés tout au long de ces articles :

* L’instance *source* est l’instance AEM à partir de laquelle vous effectuez une mise à niveau.
* L’instance *cible* est celle vers laquelle vous effectuez une mise à niveau.

>[!NOTE]
>
>Dans le cadre des efforts pour améliorer la fiabilité des mises à niveau, AEM a subi une restructuration complète des référentiels. Pour plus d’informations sur l’alignement avec la nouvelle structure, voir [Restructuration des référentiels dans AEM.](/help/sites-deploying/repository-restructuring.md)

## Qu’est-ce qui a changé ? {#what-has-changed}

Voici les principales modifications à souligner au cours des dernières versions d’AEM :

AEM 6.0 a introduit le nouveau référentiel Jackrabbit Oak. Les gestionnaires de persistance ont été remplacés par des [micro noyaux](/help/sites-deploying/platform.md#contentbody_title_4). À partir de la version 6.1, CRX2 n’est plus pris en charge. Un outil de migration appelé crx2oak doit être exécuté pour migrer les référentiels CRX2 à partir des instances 5.6.1. Pour plus d’informations, voir [Utilisation de l’outil de migration CRX2OAK](/help/sites-deploying/using-crx2oak.md).

Si vous utilisez Assets Insights et que vous effectuez une mise à niveau à partir d’une version antérieure à AEM 6.2, les ressources doivent être migrées et doivent posséder des ID générés via un bean JMX. Pour les tests internes d’Adobe, 125 000 ressources ont été migrées en 1 heure dans un environnement TarMK, mais les résultats peuvent varier.

La version 6.3 a introduit un nouveau format `SegmentNodeStore`, qui est la base de cette implémentation de TarMK. Si vous effectuez une mise à niveau à partir d’une version antérieure à AEM 6.3, une migration du référentiel est nécessaire dans le cadre de la mise à niveau, ce qui implique des interruptions du système.

L’équipe d&#39;ingénierie d’Adobe estime la durée du processus à environ 20 minutes. La réindexation n’est pas nécessaire. En outre, une nouvelle version de l’outil crx2oak a été publiée pour fonctionner avec le nouveau format de référentiel.

**Cette migration n’est pas nécessaire dans le cas d’une mise à niveau d’AEM 6.3 vers AEM 6.5.**

Les tâches de maintenance précédant la mise à niveau ont été optimisées pour prendre en charge l’automatisation.

Les options d’utilisation de ligne de commande de l’outil crx2oak ont été modifiées pour favoriser l’automatisation et prendre en charge d’autres chemins de mise à niveau.

Les contrôles après la mise à niveau ont également été optimisés pour favoriser l’automatisation.

La récupération périodique de l’espace mémoire des révisions et la récupération de l’espace mémoire du magasin de données sont désormais des tâches de maintenance de base qui doivent être exécutées régulièrement. Avec l’introduction d’AEM 6.3, Adobe prend en charge et recommande le nettoyage des révisions en ligne. Voir [Nettoyage des révisions](/help/sites-deploying/revision-cleanup.md) pour plus d’informations sur la configuration de ces tâches.

AEM a récemment introduit un [outil de détection des motifs](/help/sites-deploying/pattern-detector.md) qui permet d’évaluer la complexité de la mise à niveau lorsque vous commencez à planifier cette opération. AEM 6.5 met également l’accent sur la [rétrocompatibilité](/help/sites-deploying/backward-compatibility.md) (ou compatibilité descendante) des fonctionnalités. Pour finir, les bonnes pratiques pour les [mises à niveau durables](/help/sites-deploying/sustainable-upgrades.md) sont également ajoutées.

Pour plus d’informations sur ce qui a changé dans les versions d’AEM récentes, consultez les notes de mise à jour complètes :

* [Dernières notes de mise à jour d’Adobe Experience Manager 6.5 Service Pack](/help/release-notes/release-notes.md)

## Vue d’ensemble de la mise à niveau {#upgrade-overview}

La mise à niveau d’AEM est un processus en plusieurs étapes, parfois sur plusieurs mois. La composition suivante a été fournie sous la forme d’une vue d’ensemble des éléments inclus dans un projet de mise à niveau et du contenu inclus dans cette documentation :

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Flux de mise à niveau {#upgrade-overview-1}

Le diagramme ci-dessous capture le flux global recommandé pour mettre en évidence l’approche de mise à niveau. Notez la référence aux nouvelles fonctionnalités introduites par Adobe. La mise à niveau doit commencer par le détecteur de modèles (voir [Évaluation de la complexité de la mise à niveau à l’aide du détecteur de modèles](/help/sites-deploying/pattern-detector.md)) qui vous permet de déterminer la voie à emprunter pour la compatibilité avec AEM 6.4 sur la base des modèles du rapport généré.

Dans la version 6.5, nous avons mis un point d’honneur à ce que toutes les fonctionnalités soient rétrocompatibles. Cependant, si vous constatez des problèmes de rétrocompatibilité, le mode de compatibilité vous permet de différer temporairement le développement, de sorte que votre code personnalisé reste compatible avec la version 6.5. Cette approche vous dispense des activités de développement immédiatement après la mise à niveau (voir [Compatibilité descendante dans AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Enfin, dans le cadre de votre cycle de développement 6.5, les fonctionnalités ajoutées sous Mises à niveau possibles (voir [Mises à niveau possibles](/help/sites-deploying/sustainable-upgrades.md)) vous aident à suivre les bonnes pratiques afin de rendre les prochaines mises à niveau encore plus simples et transparentes.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
