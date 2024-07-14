---
title: Opérations de traitement en bloc
description: null
page-status-flag: never-activated
contentOwner: sarchiz
docset: aem65
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 35%

---


# Opérations de traitement en bloc {#bulk-processing-operations}

## Présentation {#introduction}

Avec la version la plus récente de Adobe Experience Manager (AEM), le bouton Tout sélectionner a été étendu à tous les affichages : Mode Liste, Colonne et Carte. Le bouton Tout sélectionner sélectionne désormais tout le contenu d’un dossier ou d’une collection donnée, et pas seulement les ressources et les pages chargées et visibles dans le navigateur client.

Les actions clés ont été activées pour l’opération en bloc : **Déplacer**, **Supprimer** et **Copier**. Une nouvelle boîte de dialogue permet aux clients de connaître les actions pour lesquelles le traitement en masse n’est pas disponible.

## Utilisation {#how-to-use}

Un nouveau bouton appelé **Tout sélectionner** a été ajouté aux modes Carte, Liste ou Colonne. Ce bouton peut être utilisé dans n’importe quelle vue pour sélectionner tous les éléments du jeu de données.

Dans les versions précédentes d’AEM, la sélection était limitée à ce qui était chargé dans le navigateur client. Cette nouvelle modification a été introduite afin d’éviter toute confusion concernant le nombre d’éléments sur lesquels une opération en bloc est effectuée.

Pour l’instant, trois opérations ont été ajoutées au traitement en bloc :

* Déplacer
* Copier
* Supprimer

La prise en charge d’autres opérations sera ajoutée à l’avenir.
Pour utiliser cette fonction, accédez au dossier ou à la collection dans lequel vous souhaitez effectuer des opérations en bloc sur les pages ou sur Assets.

Sélectionnez ensuite l’un des modes ci-dessous :

### Mode Carte {#card-view}

![Mode Carte affichant des images miniatures de différentes ressources d’image.](assets/unu.png)

### Sélection en bloc en mode Carte {#bulk-selection-in-card-view}

Les ressources ou les pages peuvent être sélectionnées en bloc à l’aide du bouton **Tout sélectionner** en haut à droite :

![Bouton Sélectionner tout affiché dans le coin supérieur droit du mode Carte.](assets/doi.png) ![Toutes les images miniatures des ressources d’image en mode Carte s’affichent comme sélectionnées avec des coches.](assets/trei.png)

### Vue Liste {#list-view}

Il en va de même pour le mode Liste :

![L’option Tout sélectionner dans le coin supérieur droit du mode Liste est mise en surbrillance.](assets/patru_modified.png)

### Sélection en bloc dans la vue Liste {#bulk-selection-in-list-view}

Dans la vue Liste, utilisez le bouton **Tout sélectionner** ou utilisez la case à cocher située à gauche pour utiliser la sélection en bloc.

![ L’affichage en direct affiche les miniatures des ressources d’image dans des lignes horizontales.](assets/cinci.png) ![Zone de liste affichant les miniatures des images des ressources d’image et une case à cocher à gauche de Nom.](assets/sase.png)

### Vue Colonnes {#column-view}

![Mode Colonnes affichant les images miniatures des ressources d’images affichées en colonnes verticales.](assets/sapte.png)

### Sélection en bloc en mode Colonnes {#bulk-selection-in-column-view}

![Toutes les images miniatures des ressources d’image en mode Colonne sont affichées comme sélectionnées avec des coches.](assets/opt.png)

## Opérations activées en bloc {#bulk-enabled-operations}

Une fois la sélection effectuée, l’une des trois actions activées en bloc peut être effectuée : **Déplacer**, **Copier** ou **Supprimer**.

Ici, l’opération **Déplacer** est effectuée sur les ressources sélectionnées ci-dessus. Dans n’importe quel affichage, toutes les Assets sont déplacées vers l’emplacement choisi et pas seulement vers celles qui sont chargées à l’écran.

![ Déplacer des ressources présentant un dossier sélectionné en mode Colonne.](assets/noua.png)

Pour les autres opérations qui ne sont pas activées en masse, comme **Téléchargement,**, un avertissement s’affiche indiquant que seuls les éléments chargés dans le navigateur sont inclus dans l’opération.

![Vue Assets affichant les ressources d’image sélectionnées et la boîte de dialogue contextuelle &quot;Action en bloc non prise en charge&quot;.](assets/zece.png)
