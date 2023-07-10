---
title: Opérations de traitement en bloc
seo-title: Bulk Processing Operations
description: null
seo-description: null
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
source-git-commit: d045fc1ac408f992d594a4cb68d1c4eeae2b0de1
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 69%

---


# Opérations de traitement en bloc {#bulk-processing-operations}

## Présentation {#introduction}

Avec la version la plus récente d’AEM, le bouton Tout sélectionner a été étendu à tous les modes : Liste, Colonnes et Carte. Le bouton Tout sélectionner sélectionne désormais tout le contenu d’un dossier ou d’une collection donnée, et pas seulement les ressources et les pages chargées et visibles dans le navigateur client.

Les actions principales ont été activées pour l’opération en bloc : **Déplacer**, **Supprimer** et **Copier**. Une nouvelle boîte de dialogue informera les clients des actions pour lesquelles le traitement en bloc n’est pas disponible.

## Utilisation {#how-to-use}

Un nouveau bouton appelé **Tout sélectionner** a été ajouté aux modes Carte, Liste ou Colonnes. Ce bouton peut être utilisé dans n’importe quelle vue pour sélectionner tous les éléments du jeu de données.

Dans les versions précédentes d’AEM, la sélection était limitée à ce qui était chargé dans le navigateur client. Ces nouvelles modifications ont été introduites pour éviter toute confusion concernant le nombre d’éléments sur lesquels une opération en bloc est effectuée.

Pour l’instant, trois opérations ont été ajoutées au traitement en bloc :

* Déplacer
* Copier
* Supprimer

La prise en charge d’autres opérations sera ajoutée à l’avenir.
Pour utiliser cette fonction, vous devez accéder au dossier ou à la collection où vous souhaitez effectuer des opérations en bloc sur les pages ou sur les ressources.

Sélectionnez ensuite l’un des modes ci-dessous :

### Mode Carte {#card-view}

![Mode Carte affichant les miniatures de différentes ressources d’image.](assets/unu.png)

### Sélection en bloc en mode Carte {#bulk-selection-in-card-view}

Les ressources ou les pages peuvent être sélectionnées en bloc à l’aide du bouton **Tout sélectionner** en haut à droite :

![Bouton Sélectionner tout affiché dans le coin supérieur droit du mode Carte.](assets/doi.png) ![Toutes les images miniatures des ressources d’image en mode Carte s’affichent comme sélectionnées avec des coches.](assets/trei.png)

### Vue Liste {#list-view}

Il en va de même pour le mode Liste :

![L’option Tout sélectionner dans le coin supérieur droit du mode Liste est mise en surbrillance.](assets/patru_modified.png)

### Sélection en bloc dans la vue Liste {#bulk-selection-in-list-view}

Dans la vue Liste, utilisez le bouton **Tout sélectionner** ou utilisez la case à cocher située à gauche pour utiliser la sélection en bloc.

![En mode réel, les miniatures des ressources d’image s’affichent dans des lignes horizontales.](assets/cinci.png) ![Zone de liste affichant les miniatures des ressources d’image et une case à cocher située à gauche de Nom.](assets/sase.png)

### Mode Colonnes {#column-view}

![Mode Colonnes affichant les images miniatures des ressources d’images affichées en colonnes verticales.](assets/sapte.png)

### Sélection en bloc en mode Colonnes {#bulk-selection-in-column-view}

![Toutes les images miniatures des ressources d’image en mode Colonnes s’affichent avec des coches.](assets/opt.png)

## Opérations activées en bloc {#bulk-enabled-operations}

Une fois la sélection effectuée, l’une des trois actions activées en bloc peut être effectuée : **Déplacer**, **Copier** ou **Supprimer**.

Ici, l’opération **Déplacer** est effectuée sur les ressources sélectionnées ci-dessus. Dans n’importe quel de ces modes, toutes les ressources sont alors déplacées vers l’emplacement choisi et pas seulement vers celles qui sont chargées à l’écran.

![Déplacez les ressources présentant un dossier sélectionné en mode Colonnes.](assets/noua.png)

Pour les autres opérations qui ne sont pas activées en bloc, comme **Télécharger**, un avertissement s’affiche indiquant que seuls les éléments chargés dans le navigateur seront inclus dans l’opération.

![Affichage des ressources affiche les ressources d’image sélectionnées, ainsi que la boîte de dialogue contextuelle &quot;Action en bloc non prise en charge&quot;.](assets/zece.png)
