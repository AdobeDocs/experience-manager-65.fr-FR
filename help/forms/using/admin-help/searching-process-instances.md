---
title: Recherche d’instances de processus
seo-title: Recherche d’instances de processus
description: Utilisez la page Recherche de processus pour entrer les critères de recherche qui vous permettront de trouver une instance de processus.
seo-description: Utilisez la page Recherche de processus pour entrer les critères de recherche qui vous permettront de trouver une instance de processus.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 98%

---


# Recherche d’instances de processus{#searching-for-process-instances}

Utilisez la page Recherche de processus pour entrer les critères de recherche qui vous permettront de trouver une instance de processus. Vous pouvez accéder à cette page à partir de la page Processus des formulaires, ou en cliquant sur Rechercher dans la page Instance du processus.

Vous pouvez entrer des critères de base pour effectuer une recherche générale, des attributs spécifiques pour effectuer une recherche détaillée, ou une combinaison de critères de base et d’attributs spécifiques pour effectuer une recherche combinée.

## Exécution d’une recherche générale {#perform-a-general-search}

Si vous souhaitez rechercher un processus, utilisez une recherche générale si vous connaissez l’identificateur de processus de l’instance du processus, si vous recherchez un groupe d’instances de processus liées, ou si seulement quelques instances de processus sont en cours d’exécution.

Pour effectuer une recherche générale, vous entrez des critères de base. Si vous entrez plusieurs critères, la recherche sera exécutée avec une condition ET implicite.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Recherche de processus.
1. Dans la page Recherche de processus, sous Recherche générale, saisissez les critères suivants :

   * **ID du processus :** entier positif qui identifie chaque instance de processus unique.
   * **Etat du processus :** sélectionnez un état dans la liste.
   * **Application :** sélectionnez une application dans la liste. Seules les applications déployées sont affichées.
   * **Nom du processus - Version :** sélectionnez un nom de processus dans le menu. Seuls les processus déployés sont affichés.

1. Cliquez sur Rechercher. La page Instance du processus s’affiche, répertoriant les instances trouvées.

## Exécution d’une recherche de processus détaillée  {#perform-a-detailed-search-for-a-process}

Vous pouvez entrer des attributs spécifiques pour effectuer une recherche détaillée. Une recherche détaillée est plus appropriée si les instances de processus en cours d’exécution sont nombreuses et que vous souhaitez limiter le nombre d’instances trouvées en utilisant des critères de recherche.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Recherche de processus.
1. Dans la page Recherche de processus, sous Recherche détaillée, indiquez vos premiers critères :

   * Dans la liste Attribut, sélectionnez un attribut.
   * Dans la liste Filtre, sélectionnez un opérateur.
   * Dans le champ Valeur, entrez une valeur appropriée pour l’attribut que vous avez sélectionné.

1. Pour ajouter une ligne supplémentaire, sélectionnez Plus de filtres. Un autre ensemble de listes Attribut, Filtre et Valeur s’affiche, de même qu’une liste Condition.
1. Sous Condition, sélectionnez ET ou OU. Répétez les étapes 1 à 3 si nécessaire pour affiner davantage votre recherche.
1. Pour ajouter ou supprimer des lignes, cliquez sur Plus de filtres ou Moins de filtres. Vous pouvez utiliser entre une et quatre lignes.
1. Cliquez sur Rechercher. La page Instance du processus s’affiche, répertoriant les instances trouvées.

[A propos des états d’instances de processus](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Exécution d’une recherche de processus combinée  {#perform-a-combined-search-for-a-process}

Pour créer une recherche basée à la fois sur une recherche générale et une recherche détaillée, avec un ET implicite entre les champs, entrez vos critères de recherche dans les champs Recherche générale et Recherche détaillée de la page Recherche de processus.

Si la recherche est trop limitée, aucune instance ne sera trouvée.
