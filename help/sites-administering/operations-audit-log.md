---
title: Maintenance du journal d’audit dans AEM 6
seo-title: Audit Log Maintenance in AEM 6
description: Découvrez la maintenance du journal d’audit dans Adobe Experience Manager (AEM).
seo-description: Learn about Audit Log Maintenance in Adobe Experience Manager (AEM).
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 52%

---

# Maintenance du journal d’audit dans AEM 6{#audit-log-maintenance-in-aem}

Les événements AEM pouvant être inclus dans la journalisation d’audit génèrent une grande quantité de données archivées. Ces données peuvent rapidement augmenter au fil du temps en raison de réplications, de chargements de ressources et d’autres activités du système.

La maintenance du journal d’audit comprend plusieurs parties des fonctionnalités qui permettent d’automatiser la maintenance du journal d’audit sous des stratégies spécifiques.

Il est mis en oeuvre en tant que tâche de maintenance hebdomadaire configurable et est accessible via la console de surveillance du tableau de bord des opérations .

Pour plus d’informations, voir [Documentation du tableau de bord des opérations](/help/sites-administering/operations-dashboard.md).

Il existe trois types de purge du journal d’audit :

1. [Purge du journal d’audit de page](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Purge du journal d’audit de la gestion des ressources numériques](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Purge du journal d’audit de réplication](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Vous pouvez configurer chacune de ces options en créant des règles dans la console web AEM. Une fois configurées, vous pouvez les utiliser en accédant à **Outils - Opérations - Maintenance - Période de maintenance hebdomadaire** et en exécutant la **Tâche de maintenance du journal d’audit**.

## Configuration de la purge du journal d’audit de page {#configure-page-audit-log-purging}

Pour configurer la purge du journal d’audit, procédez comme suit :

1. Accédez à la section d’administration de la console web en faisant pointer votre navigateur sur `http://localhost:4502/system/console/configMgr/`.

1. Recherchez un élément nommé **Règle de purge du journal d’audit de pages** et cliquez dessus.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Ensuite, configurez le planificateur de purge en fonction de vos besoins. Les options disponibles sont les suivantes :

   * **Nom de la règle :** le nom de la règle de stratégie d’audit ;
   * **Chemin d’accès au contenu :** chemin d’accès au contenu auquel la règle s’appliquera.
   * **Âge minimum :** la durée (en jours) pendant laquelle les journaux d’audit doivent être conservés ;
   * **Type de journal d’audit :** type de journal d’audit à purger.

   >[!NOTE]
   >
   >Le chemin d’accès au contenu s’applique uniquement aux enfants du nœud `/var/audit/com.day.cq.wcm.core.page` dans le référentiel.

1. Enregistrez la règle.
1. La règle que vous avez créée doit être exposée dans le tableau de bord des opérations pour qu’elle soit exécutée. Pour ce faire, accédez à **Outils - Opérations - Maintenance** dans l’écran de bienvenue d’AEM.

1. Appuyez sur la carte **Période de maintenance hebdomadaire**.

1. Vous trouverez la tâche de maintenance déjà présente dans la carte **Tâche de maintenance du journal d’audit**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Vous pouvez inspecter la date de la prochaine exécution, configurer la prochaine exécution ou l’exécuter manuellement en appuyant sur le bouton de lecture.

Dans AEM 6.3, si la période de maintenance planifiée se ferme avant que la tâche de purge du journal d’audit ne puisse se terminer, la tâche s’arrête automatiquement. Elle reprend lorsque commence la période de maintenance suivante.

**Dans AEM 6.5**, vous pouvez arrêter manuellement une tâche de purge du journal d’audit en cours d’exécution en cliquant sur le bouton **Arrêter**. Lors de la prochaine exécution, la tâche reprendra en toute sécurité.

>[!NOTE]
>
>Arrêter la tâche de maintenance signifie suspendre son exécution sans perdre la trace de la tâche déjà en cours.

## Configuration de la purge du journal d’audit DAM {#configure-dam-audit-log-purging}

1. Rendez-vous dans la console Système sur *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Recherchez **Purge du journal d’audit DAM** et cliquez sur le résultat.
1. Dans la fenêtre suivante, configurez la règle. Les options sont les suivantes :

   * **Nom de la règle :** le nom de la règle de stratégie d’audit ;
   * **Chemin d’accès au contenu :** chemin d’accès au contenu auquel la règle s’appliquera.
   * **Âge minimum :** le temps (en jours) pendant lequel les journaux d’audit doivent être conservés.
   * **Types d’événements de la gestion des journaux d’audit :** les types d’événements de contrôle DAM qui doivent être purgés.

1. Cliquez sur **Enregistrer** pour enregistrer votre configuration

## Configuration de la purge du journal d’audit de réplication  {#configure-replication-audit-log-purging}

1. Rendez-vous dans la console Système sur *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Recherchez **Planificateur de purge du journal d’audit de réplication** et cliquez sur le résultat
1. Dans la fenêtre suivante, configurez la règle. Les options sont les suivantes :

   * **Nom de la règle :** nom de la règle de stratégie d’audit
   * **Chemin d’accès au contenu :** chemin d’accès au contenu auquel la règle s’appliquera.
   * **Âge minimum :** le temps (en jours) pendant lequel les journaux d’audit doivent être conservés.
   * **Types d’événement de réplication du journal d’audit :** les types d’événements de contrôle de réplication qui doivent être purgés ;

1. Cliquez sur **Enregistrer** pour enregistrer votre configuration.
