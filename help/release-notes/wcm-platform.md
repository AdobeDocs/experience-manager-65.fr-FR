---
title: AEM Foundation et référentiel
description: Notes de mise à jour de la plateforme et du référentiel Adobe Experience Manager.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 57%

---


# AEM Foundation et référentiel {#aem-foundation-repository}

## Liste des modifications {#list-of-changes}

### Référentiel {#repository}

* La base d’Adobe Experience Manager 6.5 repose sur les versions mises à jour de la structure OSGi (Apache Sling et Apache Felix) et du référentiel de contenu Java : Apache Jackrabbit Oak 1.10.2.
* Pour un aperçu des problèmes résolus, voir [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) et [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nouvelle version d’Oak Segment Tar présente depuis AEM 6.3 nécessite une migration de référentiel. Cette étape est obligatoire si vous effectuez une mise à niveau à partir d’une ancienne version de TarMK ou si vous souhaitez remplacer le nouveau Segment Tar par un autre type de persistance. Pour en savoir plus sur les avantages du nouveau Segment Tar, voir [FAQ sur la migration vers Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

### Prise en charge de Java {#java-support}

* Nouvelle prise en charge de Java 11, ainsi que de Java 8 déjà pris en charge.
* Pour des performances optimales, remplacez les valeurs par défaut du CPG par d’autres valeurs. Pour plus d’informations, consultez la section [Installation et mise à jour](/help/sites-deploying/custom-standalone-install.md).
* Les mises à jour de maintenance Java 11 et Java 8 sont distribuées par Adobe pour l’utilisation par les clients dans les projets liés aux AEM, lorsqu’elles ne sont pas accessibles au public à partir de Oracle.

### OSGI {#osgi}

* Bibliothèques d&#39;utilitaires OSGi Ajoutées et Converter.

### Projets et workflows {#projects-and-workflows}

* Le nouvel éditeur de modèle de flux de travail introduit dans la version 6.4 a été amélioré afin d’inclure davantage d’opérations telles que Copier et Publier, la prise en charge des variables dans les étapes du flux de travail et les divisions `OR` et `AND` améliorées.

### Recherche {#searching}

* La recherche dans Oak prend désormais en charge les facettes dynamiques. Par exemple, le rail de filtrage dans la recherche de ressources affiche l’estimation du nombre de résultats.
* QueryBuilder a été étendu pour fournir des résultats avec des facettes dynamiques.

### Sécurité {#security}

* Ajout de l’expiration du mot de passe pour l’utilisateur admin.

### Interface utilisateur {#user-interface}

Diverses améliorations ont été apportées à l’interface utilisateur pour la rendre plus productive et conviviale.

* AEM 6.5 propose une nouvelle interface utilisateur de gestion des autorisations pour les utilisateurs et les groupes. Celle-ci facilite l’affichage et la configuration de l’ensemble des privilèges et restrictions sans avoir à passer à CRXDE.
* Les vues de colonnes ne chargent plus maintenant que les entrées visibles à l’écran et en chargent davantage lorsque l’utilisateur commence à faire défiler l’écran. Les vues de liste et de carte le faisaient déjà depuis la version 6.0 (amélioration dans la version 6.4).
* Les Vues de colonne incluent désormais l’état de flux de travail des pages/ressources, le cas échéant.
* L’action Sélectionner tout est un moyen rapide d’exécuter une action avec toutes les pages/ressources du même dossier.
* L’action Sélectionner tout tente d’exécuter l’action sur toutes les pages/ressources, pas seulement sur ce qui a été chargé. Si l’action n’est pas mise à niveau pour gérer les actions en masse, un avertissement s’affiche.

>[!CAUTION]
>
>L’Adobe n’améliorera pas davantage l’interface utilisateur de Classic. Experience Manager 6.5 inclut l’interface utilisateur classique pour une compatibilité ascendante. L’interface utilisateur classique reste entièrement prise en charge tout en étant obsolète [Lire la suite ](/help/sites-deploying/ui-recommendations.md).

### Mise à niveau {#upgrade}

* La procédure de mise à niveau reste en grande partie la même dans la version 6.5.
* Nous continuons à prendre en charge la compatibilité ascendante, l’évaluation de la complexité des mises à niveau et les fonctions de continuité mises à niveau ajoutées dans la version 6.4. Des mises à jour spécifiques à la version ont été apportées à ces domaines, le cas échéant.
* L’assemblage du détecteur de modèle a été simplifié et un seul package évaluera les mises à niveau vers la version 6.5 pour les versions sources disponibles.
* Pour plus d&#39;informations sur la procédure de mise à niveau, consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md).

### Serveur web {#web-server}

* La distribution Quickstart utilise Eclipse Jetty 9.4.15 comme moteur de servlet (AEM 6.4 fourni avec 9.3.22).
