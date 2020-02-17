---
title: AEM Foundation et référentiel
description: Notes de mise à jour spécifiques à la plateforme et au référentiel d’Adobe Experience Manager 6.3.
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# AEM Foundation et référentiel{#aem-foundation-repository}

## Liste des modifications     {#list-of-changes}

### Référentiel {#repository}

* La base d’Adobe Experience Manager 6.5 repose sur les versions mises à jour de la structure OSGi (Apache Sling et Apache Felix) et du référentiel de contenu Java : Apache Jackrabbit Oak 1.10.2.
* Please see [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) and [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) for a full overview of fixed issues.

>[!CAUTION]
>
>* La nouvelle version d’Oak Segment Tar présente depuis AEM 6.3 nécessite une migration de référentiel. Cette étape est obligatoire si vous effectuez une mise à niveau à partir d’une ancienne version de TarMK ou si vous souhaitez remplacer le nouveau Segment Tar par un autre type de persistance. Pour en savoir plus sur les avantages du nouveau Segment Tar, voir [FAQ sur la migration vers Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>



### Prise en charge de Java {#java-support}

* Nouvelle prise en charge de Java 11, ainsi que de Java 8 déjà pris en charge
* Pour des performances optimales, remplacez les valeurs par défaut du CPG par d’autres valeurs. Pour plus d’informations, consultez la section [Installation et mise à jour](/help/sites-deploying/custom-standalone-install.md).
* Les mises à jour de maintenance Java 11 et Java 8 seront distribuées par Adobe pour que les clients puissent les utiliser dans les projets liés à AEM, lorsqu’elles ne sont pas disponibles publiquement auprès d’Oracle.

### OSGI {#osgi}

* Ajout des bibliothèques d’utilitaires OSGi Promises et Converter

### Projets et workflows {#projects-and-workflows}

* Le nouvel éditeur de modèle de workflow ajouté à la version 6.4 a été amélioré afin d’inclure davantage d’opérations telles que la copie et la publication, la prise en charge des variables dans les étapes de workflow et les divisions OR et AND améliorées.

### Recherche {#searching}

* La recherche dans Oak prend désormais en charge les facettes dynamiques. Par exemple, le rail de filtre dans la recherche de ressources affiche la quantité estimée de résultats.
* QueryBuilder a été étendu pour fournir des résultats avec des facettes dynamiques.

### Sécurité {#security}

* Ajout de l’expiration du mot de passe pour l’utilisateur admin.

### Interface utilisateur {#user-interface}

Diverses améliorations ont été apportées à l’interface utilisateur pour la rendre plus productive et conviviale.

* AEM 6.5 propose une nouvelle interface utilisateur de gestion des autorisations pour les utilisateurs et les groupes. Celle-ci facilite l’affichage et la configuration de l’ensemble des privilèges et restrictions sans avoir à passer à CRXDE.
* Les vues de colonnes ne chargent plus maintenant que les entrées visibles à l’écran et en chargent davantage lorsque l’utilisateur commence à faire défiler l’écran. Les vues de liste et de carte le faisaient déjà depuis la version 6.0 (amélioration dans la version 6.4)
* Les vues de colonne incluent désormais l’état du workflow pour les pages/ressources, le cas échéant.
* L’action « Sélectionner tout » est un moyen rapide d’exécuter une action sur toutes les pages/tous les éléments d’un même dossier.
* L’action « Sélectionner tout » tente d’exécuter l’action sur toutes les pages/ressources, pas seulement sur ce qui a été chargé. Une boîte de dialogue d’avertissement s’affiche si l’action n’a pas été mise à niveau pour gérer les actions en bloc.

>[!CAUTION]
>
>* Adobe ne prévoit pas d’apporter d’autres améliorations à l’interface utilisateur classique. AEM 6.5 comprend l’interface utilisateur classique, et les clients effectuant une mise à niveau à partir de versions antérieures peuvent continuer à l’utiliser en l’état. Note that Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).
>



### Mise à niveau {#upgrade}

* La procédure de mise à niveau reste en grande partie la même dans la version 6.5.
* Nous continuons à prendre en charge la compatibilité ascendante, l’évaluation de la complexité des mises à niveau et les fonctions de continuité mises à niveau ajoutées dans la version 6.4. Des mises à jour spécifiques à la version ont été apportées à ces domaines, le cas échéant.
* L’assemblage du détecteur de modèle a été simplifié et un seul package évaluera les mises à niveau vers la version 6.5 pour les versions sources disponibles.
* Please see the [Upgrade documentation](/help/sites-deploying/upgrade.md) for more details on upgrade procedure.

### Serveur web {#web-server}

* La distribution Quickstart utilise Eclipse Jetty 9.4.15 comme moteur de servlet (AEM 6.4 fourni avec la version 9.3.22)

