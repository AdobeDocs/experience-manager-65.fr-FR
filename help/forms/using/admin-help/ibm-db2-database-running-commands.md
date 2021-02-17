---
title: '"Base de données IBM DB2 : exécution des commandes pour des opérations de maintenance standard"'
seo-title: '"Base de données IBM DB2 : exécution des commandes pour des opérations de maintenance standard"'
description: Ce document répertorie les commandes IBM DB2 recommandées dans le cadre des opérations de maintenance standard de votre base de données AEM Forms.
seo-description: Ce document répertorie les commandes IBM DB2 recommandées dans le cadre des opérations de maintenance standard de votre base de données AEM Forms.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 89%

---


# Base de données IBM DB2 : exécution des commandes pour des opérations de maintenance standard {#ibm-db-database-running-commands-for-regular-maintenance}

Il est recommandé d’exécuter régulièrement les commandes IBM DB2 suivantes dans le cadre des opérations de maintenance standard de votre base de données AEM forms. Pour obtenir des informations détaillées sur la maintenance et l’amélioration des performances de la base de données DB2, reportez-vous au *Guide d’administration d’IBM DB2*.

* **runstats :** cette commande met à jour les statistiques décrivant les caractéristiques physiques d’une table de base de données et des index associés. Les instructions SQL dynamiques générées par AEM forms utilisent automatiquement ces statistiques mises à jour, mais pour les instructions SQL statiques intégrées à une base de données, l’instruction `db2rbind` doit également être exécutée.
* **db2rbind :** cette commande réassocie tous les packages de la base de données. Utilisez cette commande après avoir exécuté l’utilitaire `runstats` pour revalider tous les packages dans la base de données.
* **reorg table ou index :** cette commande vérifie si une réorganisation de certaines tables et index est nécessaire.

   A mesure que la taille de vos bases de données augmente et qu’elles subissent des modifications, il est important de recalculer régulièrement les statistiques des tables pour améliorer les performances. Ces commandes peuvent être exécutées manuellement en utilisant des scripts ou en utilisant une tâche cron.

>[!NOTE]
>
>avant d’exécuter la commande `runstats`, la base de données doit être alimentée et au moins une synchronisation de répertoires doit avoir été effectuée.

Pour une base de données de petite taille, par exemple 10 000 utilisateurs ou 2 500 groupes, il suffit d’appeler la commande `runstats` pour réduire les délais de synchronisation.

Pour les bases de données plus volumineuses, par exemple 100 000 utilisateurs ou 10 000 groupes, exécutez la commande `reorg` avant la commande `runstats`.

## Utilisation de la commande runstats sur la base de données AEM forms {#use-the-runstats-command-on-your-aem-forms-database}

Exécutez la commande `runstats` sur les tables et index de base de données AEM forms suivants.

>[!NOTE]
>
>la commande `runstats` ne doit être exécutée que lors de la première synchronisation de base de données. Toutefois, elle doit être exécutée à deux reprises pendant ce processus : la première fois pendant la synchronisation des utilisateurs et groupes, puis la seconde fois lors de la synchronisation des membres de groupe. Vérifiez que le script s’exécute totalement chaque fois que vous le lancez.

Pour une syntaxe et une utilisation correctes, consultez la documentation du fabricant de la base de données. Ci-dessous, `<schema>` désigne le schéma associé à votre nom d’utilisateur DB2. Si vous disposez d’une installation DB2 par défaut, il s’agit du nom de schéma de la base de données.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## Exécution de la commande reorg sur la base de données AEM forms {#run-the-reorg-command-on-your-aem-forms-database}

Exécutez la commande `reorg` sur les tables et index de base de données AEM forms suivants. Pour une syntaxe et une utilisation correctes, consultez la documentation du fabricant de la base de données.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```

