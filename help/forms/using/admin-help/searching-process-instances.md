---
title: Rechercher des instances de processus
description: Utilisez la page Recherche de processus pour saisir les critères de recherche permettant de trouver une instance de processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 100%

---

# Rechercher des instances de processus{#searching-for-process-instances}

Utilisez la page Recherche de processus pour saisir les critères de recherche permettant de trouver une instance de processus. Vous pouvez accéder à la page Recherche de processus à partir de la page Forms Workflow ou en cliquant sur Rechercher dans la page Instance du processus.

Vous pouvez saisir des critères de base pour effectuer une recherche générale, des attributs spécifiques pour effectuer une recherche détaillée ou une combinaison de critères de base et d’attributs spécifiques pour effectuer une recherche combinée.

## Exécution d’une recherche générale {#perform-a-general-search}

Une recherche générale d’un processus est plus appropriée si vous connaissez l’ID de processus de l’instance de processus, si vous recherchez un groupe d’instances de processus associées ou si seules quelques instances de processus sont en cours d’exécution.

Saisissez les critères de base pour effectuer une recherche générale. Si vous saisissez plusieurs critères, la recherche est effectuée avec une condition ET implicite.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Recherche de processus.
1. Sur la page Recherche de processus, sous Recherche générale, fournissez les critères suivants :

   * **ID du processus :** entier positif qui identifie chaque instance de processus unique.
   * **Etat du processus :** sélectionnez un état dans la liste.
   * **Application :** sélectionnez une application dans la liste. Seules les applications déployées sont affichées.
   * **Nom du processus - Version :** sélectionnez un nom de processus dans le menu. Seuls les processus déployés sont affichés.

1. Cliquez sur Rechercher. La page Instance du processus s’affiche, répertoriant les instances trouvées.

## Exécution d’une recherche de processus détaillée {#perform-a-detailed-search-for-a-process}

Vous pouvez saisir des attributs spécifiques pour effectuer une recherche détaillée. Une recherche détaillée est plus appropriée si de nombreuses instances de processus sont en cours d’exécution et que vous devez limiter les résultats possibles en fonction de certains critères.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Recherche de processus.
1. Sur la page Recherche de processus, sous Recherche détaillée, spécifiez votre premier jeu de critères :

   * Dans la liste Attribut, sélectionnez un attribut.
   * Dans la liste Filtre, sélectionnez un opérateur.
   * Dans la zone Valeur, saisissez une valeur appropriée pour l’attribut que vous avez sélectionné.

1. Pour ajouter une ligne, sélectionnez Plus de filtres. Un autre ensemble de listes Attribut, Filtre et Valeur s’affiche, avec une liste Condition.
1. Sous Condition, sélectionnez ET ou OU. Répétez les étapes 1 à 3 selon les besoins pour limiter davantage votre recherche.
1. Pour ajouter ou supprimer des lignes, cliquez sur Plus de filtres ou Moins de filtres. Vous pouvez utiliser entre une et quatre lignes.
1. Cliquez sur Rechercher. La page Instance du processus s’affiche, répertoriant les instances trouvées.

[A propos des états d’instances de processus](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Exécution d’une recherche de processus combinée {#perform-a-combined-search-for-a-process}

Pour créer une recherche basée à la fois sur une recherche générale et une recherche détaillée, avec un ET implicite entre les champs, entrez vos critères de recherche dans les champs Recherche générale et Recherche détaillée de la page Recherche de processus.

Si la recherche est trop limitée, aucune instance ne sera trouvée.
