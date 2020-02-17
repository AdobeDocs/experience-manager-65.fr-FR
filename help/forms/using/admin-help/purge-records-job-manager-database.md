---
title: Purge d’enregistrements de la base de données de Job Manager.
seo-title: Purge d’enregistrements de la base de données de Job Manager.
description: Les données de processus de grande taille peuvent entraîner une baisse des performances d’AEM forms. Il est recommandé de purger ces données de processus lorsque des enregistrements ne sont plus nécessaires.
seo-description: Les données de processus de grande taille peuvent entraîner une baisse des performances d’AEM forms. Il est recommandé de purger ces données de processus lorsque des enregistrements ne sont plus nécessaires.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Purge d’enregistrements de la base de données de Job Manager.{#purge-records-from-the-job-manager-database}

Les données générées lors de l’appel d’un processus de longue durée peuvent occuper un espace considérable, réduisant les performances d’AEM forms et monopolisant un espace disque superflu. Il est recommandé de purger ces données de processus lorsque des enregistrements ne sont plus nécessaires.

Vous pouvez utiliser Administration Console pour effectuer une purge individuelle des enregistrements obsolètes ou planifier des purges régulières automatiques. D’autres méthodes de purge des enregistrements obsolètes sont présentées dans la section [Purge des données de processus](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Accès à la page Planificateur de purge de travaux**

1. Dans l’angle supérieur droit de la page d’Administration Console, cliquez sur Health Monitor.
1. Cliquez sur l’onglet Planificateur de purge de travaux.

Les informations relatives aux purges actuellement planifiées s’affichent dans la zone Informations du planificateur de purge de travaux.

>[!NOTE]
>
>cliquer sur Arrêter le planificateur permet d’arrêter toute purge planifiée, mais n’arrêtera pas un travail de purge en cours.

**Planification d’une purge individuelle**

1. Sélectionnez Une fois seulement.
1. Dans la zone Purger le filtre des enregistrements terminés, spécifiez le nombre de jours ou de semaines au bout desquels un enregistrement est considéré comme obsolète et prêt à être purgé.

   >[!NOTE]
   >
   >les enregistrements liés aux processus non terminés ne seront pas purgés, même s’ils sont plus anciens que l’âge spécifié.

1. Spécifiez le moment auquel la purge aura lieu. Cochez la case Utiliser la date et l’heure actuelles, ou désélectionnez-la et cliquez sur les icônes de calendrier et d’horloge pour spécifier la date et l’heure de la purge.

   >[!NOTE]
   >
   >si vous spécifiez une date et une heure de début antérieures à la date actuelle, la purge se lancera dès que vous cliquerez sur Démarrer le planificateur.

1. Cliquez sur Démarrer le planificateur. Tous les paramètres de planificateur précédemment définis seront remplacés par les nouveaux.

**Configuration d’un calendrier de purges automatiques**

1. Sélectionnez Récurrence tous les et spécifiez le nombre de jours ou de semaines entre les purges.
1. Dans la zone Purger le filtre des enregistrements terminés, spécifiez le nombre de jours ou de semaines au bout desquels un enregistrement est considéré comme obsolète et prêt à être purgé. Vous ne pouvez pas définir la valeur sur `0`.

   >[!NOTE]
   >
   >les enregistrements liés aux processus non terminés ne seront pas purgés, même s’ils sont plus anciens que l’âge spécifié.

1. Spécifiez le moment auquel les purges commenceront. Cochez la case Utiliser la date et l’heure actuelles, ou désélectionnez-la et cliquez sur les icônes de calendrier et d’horloge pour spécifier la date et l’heure de la purge.

   >[!NOTE]
   >
   >Si vous spécifiez une date et une heure de début antérieures à la date actuelle, AEM forms calcule la date logique de départ suivante selon la date indiquée. Par exemple, si vous planifiez le 9 avril une tâche de purge hebdomadaire à partir du 7 avril, la première purge sera effectuée le 14 avril.

1. Cliquez sur Démarrer le planificateur. Tous les paramètres de planificateur précédemment définis seront remplacés par les nouveaux.

