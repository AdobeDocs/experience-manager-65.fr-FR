---
title: Mise à niveau vers AEM 6.5
seo-title: Upgrading to AEM 6.5
description: Découvrez les principes de base de la mise à niveau d’une installation d’AEM vers la version AEM 6.5.
seo-description: Learn about the basics of upgrading an older AEM installation to AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
source-git-commit: 02fc145d5ec1458d1f71a2f353b56b944a267f3e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 75%

---

# Mise à niveau vers AEM 6.5 {#upgrading-to-aem}

Dans cette section, nous présentons la mise à niveau d’une installation AEM vers AEM 6.5 :

* [Planification de la mise à niveau](/help/sites-deploying/upgrade-planning.md)
* [Évaluation de la complexité de la mise à niveau à l’aide de l’outil de détection des motifs](/help/sites-deploying/pattern-detector.md)
* [Compatibilité descendante dans AEM 6.5](/help/sites-deploying/backward-compatibility.md)

<!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Procédure de mise à niveau](/help/sites-deploying/upgrade-procedure.md)
* [Mise à niveau du code et des personnalisations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Tâches de maintenance avant la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Exécution d’une mise à niveau statique](/help/sites-deploying/in-place-upgrade.md)
* [Vérifications et dépannage après une mise à niveau ](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Mises à niveau possibles](/help/sites-deploying/sustainable-upgrades.md)
* [Migration différée du contenu](/help/sites-deploying/lazy-content-migration.md)
* [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md)

Pour une référence conviviale aux instances d’AEM incluses dans ces procédures, les termes suivants sont utilisés tout au long de ces articles :

* L’instance *source* est l’instance AEM depuis laquelle vous mettez à niveau.
* L’instance *cible* est celle vers laquelle vous mettez à niveau.

>[!NOTE]
>
>Dans le cadre des efforts pour améliorer la fiabilité des mises à niveau, AEM a subi une restructuration complète des référentiels. Pour plus d’informations sur la façon de les aligner avec la nouvelle structure, voir[ Restructuration des référentiels dans AEM.](/help/sites-deploying/repository-restructuring.md)

## Qu’est-ce qui a changé ? {#what-has-changed}

Voici quelques changements majeurs mis en œuvre avec les dernières versions d’AEM :

AEM 6.0 a introduit le nouveau référentiel Jackrabbit Oak. Les gestionnaires de persistence ont été remplacés par les [micronoyaux](/help/sites-deploying/platform.md#contentbody_title_4). À partir de la version 6.1, CRX2 n’est plus pris en charge. L’outil de migration crx2oak doit être exécuté pour migrer les référentiels CRX2 à partir des instances 5.6.1. Pour plus d’informations, voir [Utilisation de l’outil de migration CRX2OAK](/help/sites-deploying/using-crx2oak.md). 

Si vous souhaitez utiliser Assets Insights et que vous effectuez une mise à niveau à partir d’une version antérieure à AEM 6.2, les ressources doivent être migrées et leurs identifiants doivent être générés via un bean JMX. Lors de nos tests internes, 125 000 ressources ont été migrées en 1 heure dans un environnement TarMK, mais les résultats peuvent varier. 

La version 6.3 a introduit un nouveau format `SegmentNodeStore`, qui est la base de cette implémentation de TarMK. Si vous effectuez une mise à niveau à partir d’une version antérieure à AEM 6.3, une migration du référentiel est nécessaire dans le cadre de la mise à niveau, ce qui implique des interruptions du système.

L’équipe technique d’Adobe estime la durée du processus à environ 20 minutes. Notez que la réindexation ne sera pas nécessaire. En outre, une nouvelle version de l’outil crx2oak a été publiée pour fonctionner avec le nouveau format de référentiel.

**Cette migration n’est pas nécessaire dans le cas d’une mise à niveau d’AEM 6.3 vers AEM 6.5.**

Les tâche de maintenance avant la mise à niveau ont été optimisées dans le cadre de la prise en charge de l’automatisation.

Les options d’utilisation des lignes de commande de l’outil crx2oak ont été modifiées pour être adaptées à l’automatisation et pour prendre en charge plus de chemins de mise à niveau.

Les vérifications après la mise à niveau se sont également adaptées à l’automatisation.

Le nettoyage périodique des révisions et de l’entrepôt de données sont désormais des tâches de maintenance standard qui doivent être exécutées régulièrement. Avec l’introduction d’AEM 6.3, Adobe prend en charge et recommande le nettoyage des révisions en ligne. Voir [Nettoyage des révisions](/help/sites-deploying/revision-cleanup.md) pour plus d’informations sur la configuration de ces tâches. 

AEM a récemment introduit un [outil de détection des motifs](/help/sites-deploying/pattern-detector.md) qui permet d’évaluer la complexité de la mise à niveau lorsque vous commencez à planifier cette opération. AEM 6.5 met également l’accent sur la [rétrocompatibilité](/help/sites-deploying/backward-compatibility.md) (ou compatibilité descendante) des fonctionnalités. Enfin, des meilleures pratiques concernant les [mises à niveau possibles](/help/sites-deploying/sustainable-upgrades.md) ont également été ajoutées.

Pour plus d’informations sur les autres points modifiés dans les versions récentes d’AEM, consultez les notes de mise à jour complètes :

* [Notes de mise à jour générales d’Adobe Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/release-notes.html?lang=fr)
* [Notes de mise à jour d’Adobe Experience Manager 6.5 dernier Service Pack](/help/release-notes/release-notes.md)

## Vue d’ensemble de la mise à niveau  {#upgrade-overview}

La mise à niveau d’AEM consiste en plusieurs étapes et peut parfois se dérouler sur plusieurs mois. L’aperçu suivant vous donne une vue d’ensemble du contenu d’un projet de mise à niveau, ainsi que des éléments inclus dans cette documentation :

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Flux de mise à niveau {#upgrade-overview-1}

Le diagramme ci-dessous illustre le flux recommandé pour la méthode de mise à niveau. Notez la référence aux nouvelles fonctionnalités que nous avons ajoutées. La mise à niveau doit commencer avec le détecteur de motifs (voir [Évaluation de la complexité de la mise à niveau à l’aide du détecteur de motifs](/help/sites-deploying/pattern-detector.md)) qui vous permet de choisir le chemin que vous souhaitez prendre pour des raisons de compatibilité avec AEM 6.4 en fonction des modèles du rapport généré.

Dans la version 6.5, nous avons mis l’accent sur la compatibilité descendante de toutes les nouvelles fonctionnalités. Cependant, lorsque des problèmes de compatibilité descendante se produisent, le mode de compatibilité vous permet de différer temporairement le développement pour que votre code personnalisé reste compatible avec la version 6.5. Cette approche vous permet d’éviter les efforts de développement immédiatement après la mise à niveau (voir [Compatibilité descendante dans AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Enfin, dans votre cycle de développement 6.5, les fonctionnalités introduites sous Mises à niveau possibles (voir [Mises à niveau possibles](/help/sites-deploying/sustainable-upgrades.md)) vous aider à suivre les bonnes pratiques pour rendre les futures mises à niveau encore plus efficaces et transparentes.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
