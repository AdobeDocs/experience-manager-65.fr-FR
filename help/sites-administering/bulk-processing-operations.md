---
title: Opérations de traitement en bloc
seo-title: Bulk Processing Operations
description: 'null'
seo-description: null
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---


# Opérations de traitement en bloc {#bulk-processing-operations}

## Présentation  {#introduction}

Avec la version la plus récente d’AEM, le bouton Tout sélectionner a été étendu à toutes les vues : Mode Liste, Colonnes et Carte. Le bouton Tout sélectionner sélectionne désormais tout le contenu d’un dossier ou d’une collection donnée, et pas seulement les ressources et les pages chargées et visibles dans le navigateur client.

Les actions clés ont été activées pour l’opération en bloc : **Déplacer**, **Supprimer** et **Copier**. Une nouvelle boîte de dialogue informera les clients des actions pour lesquelles le traitement en masse n’est pas disponible.

## Utilisation {#how-to-use}

Un nouveau bouton appelé **Tout sélectionner** a été ajouté aux modes Carte, Liste ou Colonnes. Ce bouton peut être utilisé dans n’importe quelle vue pour sélectionner tous les éléments du jeu de données.

Dans les versions précédentes d’AEM, la sélection était limitée à ce qui était chargé dans le navigateur client. Ces nouvelles modifications ont été introduites pour éviter toute confusion concernant le nombre d’éléments sur lesquels une opération en bloc est effectuée.

Pour l’instant, trois opérations ont été ajoutées au traitement en masse :

* Déplacer
* Copier
* Supprimer

La prise en charge d’autres opérations sera ajoutée à l’avenir.
Pour utiliser cette fonction, vous devez accéder au dossier ou à la collection dans lequel vous souhaitez effectuer des opérations en bloc sur les pages ou sur les ressources.

Sélectionnez ensuite l’une des vues, comme illustré ci-dessous :

### Mode Carte {#card-view}

![](assets/unu.png)

### Sélection en bloc en mode Carte {#bulk-selection-in-card-view}

Les ressources ou les pages peuvent être sélectionnées en bloc à l’aide du **Tout sélectionner** en haut à droite :

![](assets/doi.png) ![](assets/trei.png)

### Mode Liste {#list-view}

Il en va de même pour le mode Liste :

![](assets/patru_modified.png)

### Sélection en bloc en mode Liste {#bulk-selection-in-list-view}

En mode Liste, utilisez l’option **Tout sélectionner** ou utilisez la case à cocher située à gauche pour la sélection en bloc.

![](assets/cinci.png) ![](assets/sase.png)

### Mode Colonnes {#column-view}

![](assets/sapte.png)

### Sélection en bloc en mode Colonnes {#bulk-selection-in-column-view}

![](assets/opt.png)

## Opérations activées en bloc {#bulk-enabled-operations}

Une fois la sélection effectuée, l’une des trois actions activées en bloc peut être effectuée : **Déplacer**, **Copier** ou **Supprimer**.

Ici, **Déplacer** est effectuée sur les ressources sélectionnées ci-dessus. Dans n’importe quel affichage, toutes les ressources sont alors déplacées vers l’emplacement choisi et pas seulement vers celles qui sont chargées à l’écran.

![](assets/noua.png)

Pour les autres opérations qui ne sont pas activées en bloc, comme **Télécharger,** un avertissement s’affiche indiquant que seuls les éléments chargés dans le navigateur seront inclus dans l’opération.

![](assets/zece.png)
