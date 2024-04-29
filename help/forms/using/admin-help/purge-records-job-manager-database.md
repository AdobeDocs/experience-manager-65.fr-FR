---
title: Purger les enregistrements de la base de données de Job Manager
description: Des données de processus volumineuses peuvent entraîner une baisse des performances d’AEM Forms. Il est recommandé de purger les données de processus lorsque vous n’avez plus besoin des enregistrements.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '471'
ht-degree: 100%

---

# Purger les enregistrements de la base de données de Job Manager {#purge-records-from-the-job-manager-database}

Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui diminue les performances d’AEM Forms et utilise de l’espace disque inutilement. Il est recommandé de purger les données de processus lorsque vous n’avez plus besoin des enregistrements.

Vous pouvez utiliser la console d’administration pour effectuer une purge ponctuelle des enregistrements obsolètes ou pour planifier des purges automatiques régulières. D’autres méthodes pour purger les enregistrements obsolètes sont abordées dans [Purger les données du processus](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Accéder à la page Planificateur de purge des traitements**

1. Dans la console d’administration, cliquez sur Health Monitor dans le coin supérieur droit de la page.
1. Cliquez sur l’onglet Planificateur de purge des traitements.

Les informations sur les purges actuellement planifiées s’affichent dans la zone Informations sur le planificateur de purge des traitements.

>[!NOTE]
>
>Cliquer sur Arrêter le planificateur arrête toutes les purges planifiées dans le futur, mais n’arrête pas un traitement de purge déjà en cours.

**Planifier une purge ponctuelle**

1. Sélectionnez Une seule fois.
1. Dans la zone Filtrer les enregistrements terminés par une purge, spécifiez le nombre de jours ou de semaines après lequel un enregistrement est considéré comme obsolète et prêt à être purgé.

   >[!NOTE]
   >
   >Les enregistrements liés aux processus qui n’ont pas été terminés ne sont pas purgés, même s’ils sont plus anciens que l’âge spécifié.

1. Spécifiez quand la purge aura lieu. Cochez la case Utiliser la date et l’heure actuelles ou décochez la case et cliquez sur les icônes de calendrier et d’horloge pour spécifier la date et l’heure auxquelles la purge sera effectuée.

   >[!NOTE]
   >
   >Si vous spécifiez une date et une heure de début antérieures, la purge se produit immédiatement lorsque vous cliquez sur Démarrer le planificateur.

1. Cliquez sur Démarrer le planificateur. Tous les paramètres du planificateur précédemment planifiés sont remplacés par les nouveaux paramètres.

**Configurer un planning de purge automatique**

1. Sélectionnez Répéter chaque et spécifiez le nombre de jours ou de semaines entre les purges.
1. Dans la zone Filtrer les enregistrements terminés par une purge, spécifiez le nombre de jours ou de semaines après lequel un enregistrement est considéré comme obsolète et prêt à être purgé. Vous ne pouvez pas définir la valeur sur `0`.

   >[!NOTE]
   >
   >Les enregistrements liés aux processus qui n’ont pas été terminés ne sont pas purgés, même s’ils sont plus anciens que l’âge spécifié.

1. Précisez quand les purges commenceront. Cochez la case Utiliser la date et l’heure actuelles ou décochez la case et cliquez sur les icônes de calendrier et d’horloge pour spécifier la date et l’heure auxquelles la purge sera effectuée.

   >[!NOTE]
   >
   >Si vous spécifiez une date et une heure de début passées, AEM Forms calcule la prochaine date de début logique en fonction de la date que vous avez spécifiée. Par exemple, si vous planifiez les purges de traitement de manière hebdomadaire à partir du 7 avril et que nous sommes désormais le 9 avril, la première purge aura lieu le 14 avril.

1. Cliquez sur Démarrer le planificateur. Tous les paramètres du planificateur précédemment planifiés sont remplacés par les nouveaux paramètres.
