---
title: Personnalisation des modèles de recherche
seo-title: Personnalisation des modèles de recherche
description: Vous pouvez créer des modèles de recherche à utiliser dans Workspace pour rechercher des instances de processus depuis les pages de tâches et de suivi. Vous pouvez également modifier ou supprimer des modèles de recherche existants.
seo-description: Vous pouvez créer des modèles de recherche à utiliser dans Workspace pour rechercher des instances de processus depuis les pages de tâches et de suivi. Vous pouvez également modifier ou supprimer des modèles de recherche existants.
uuid: 2043ba8a-07f0-4054-af3c-f3a14c2183ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6e4b4dfa-3af5-4c21-a2a1-b90ef02d8514
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 88%

---


# Personnalisation des modèles de recherche {#customizing-search-templates}

Vous pouvez créer des modèles de recherche à utiliser dans Workspace pour rechercher des instances de processus depuis les pages de tâches et de suivi. Vous pouvez également modifier ou supprimer des modèles de recherche existants.

Lorsque vous créez ou modifiez un modèle de recherche, vous pouvez définir la mise en page et l’ordre de tri des résultats de recherche. Toutefois, les utilisateurs peuvent modifier ces paramètres dans Workspace après l’affichage des résultats de recherche.

Vous pouvez créer autant de modèles de recherche que vous le souhaitez.

>[!NOTE]
>
>lorsque vous enregistrez un modèle de recherche, vous devez lui affecter un nom unique. Si vous ne le faites pas, un modèle existant risque d’être remplacé sans message d’avertissement.

## Création d’un modèle de recherche simple {#create-a-simple-search-template}

1. Dans Administration Console, cliquez sur Services > Workspace > Modèles de recherche.
1. Dans l’onglet Identification, indiquez l’objectif du modèle dans la zone Description du modèle de recherche.
1. (Facultatif) Cliquez sur l’onglet Critère et indiquez le critère de recherche du modèle.
1. Cliquez sur l’onglet Enregistrer, entrez un nom unique pour le modèle, puis cliquez sur Enregistrer.

## Création ou modification d’un modèle de recherche  {#create-or-edit-a-search-template}

1. Dans Administration Console, cliquez sur Services > Workspace > Modèles de recherche.
1. (Facultatif) Si vous modifiez un modèle existant ou que vous vous servez d’un modèle existant pour en créer un nouveau, sélectionnez le modèle dans la liste Nom du modèle de recherche.
1. Dans la zone Description du modèle de recherche, indiquez l’objectif du modèle de recherche.
1. (Facultatif) Dans la zone Instructions à l’intention des utilisateurs, indiquez les instructions utiles à l’utilisation du modèle de recherche. Celles-ci s’affichent dans Workspace, une fois le modèle de recherche sélectionné.
1. Cliquez sur l’onglet Critère. C’est dans cet onglet que vous définissez un ou plusieurs critères. Pour ajouter un critère de recherche :

   * Dans la partie supérieure de l’onglet Critère, sélectionnez un élément de processus ou de tâche.

      **Conseil** :  *Si vous avez précédemment sélectionné l’élément Nom du processus et que vous avez spécifié un processus, toutes les variables de processus définies dans ce processus peuvent également être sélectionnées.*

      **Conseil** :  *Si vous sélectionnez l’élément Tâche visible, les utilisateurs pourront supprimer les tâches terminées des résultats de la recherche.*

      Les champs relatifs au critère de recherche de l’élément sélectionné s’affichent au bas de l’onglet Critère.

   * Pour chaque élément de processus ou de tâche, ou pour chaque variable de processus sélectionné, remplissez les champs de recherche correspondants, au bas de l’onglet Critère.

      * Sélectionnez un opérateur relationnel (comme égal à) dans la liste fournie et indiquez la valeur de l’opérande dans la boîte qui se trouve à côté.
      * (Facultatif) Pour autoriser des utilisateurs à modifier la valeur de l’opérande dans Workspace, sélectionnez Autoriser l’utilisateur à modifier l’opérande.
      * (Facultatif) Pour autoriser des utilisateurs à modifier l’opérateur relationnel, sélectionnez Autoriser l’utilisateur à sélectionner un autre opérateur relationnel. Dans la liste qui apparaît, sélectionnez les opérateurs auxquels les utilisateurs pourront faire appel.

      **Conseil** :  *Si vous avez sélectionné Nom du processus en tant qu’élément, vous pouvez cliquer sur l’icône en regard du champ de l’opérande pour afficher une liste dans laquelle vous pouvez sélectionner un processus en cours d’exécution sur le serveur Forms. Après avoir sélectionné un processus, toute variable définie pour ce processus peut être sélectionnée dans Variables de processus, dans la partie supérieure de l’onglet Critère.*

      **Conseil** :  *Vous pouvez supprimer un élément du modèle de recherche en cliquant sur l’icône Supprimer en regard des critères de recherche de l’élément.*


1. (Facultatif) Pour chaque en-tête de colonne à afficher dans les résultats de recherche, cliquez sur l’onglet Mise en page et procédez comme suit :

   * Sélectionnez un élément de processus ou de tâche et cliquez droite sur la flèche pour le déplacer vers la liste Colonnes à reporter.
   * Dans cette liste, sélectionnez l’élément de processus ou de tâche et cliquez sur la flèche Haut ou Bas pour le placer dans l’ordre dans la colonne. Les en-têtes de colonne des résultats de recherche s’affichent dans l’ordre selon lequel ils sont répertoriés à cet endroit.
   * (Facultatif) Pour modifier le nom de l’élément de l’en-tête de colonne, sélectionnez-le dans la liste Colonnes de rapport et indiquez le nouveau nom.

   >[!NOTE]
   >
   >la mise en page spécifiée dans le modèle de recherche remplace les préférences de l’utilisateur indiquées pour les en-têtes de colonne dans Workspace.

1. (Facultatif) Pour chaque colonne à trier dans les résultats de recherche, cliquez sur l’onglet Trier et procédez comme suit :

   * Sélectionnez un élément de processus ou de tâche et cliquez sur la flèche droite pour le déplacer vers la liste Ordre de tri.
   * Dans cette liste, sélectionnez l’élément de processus ou de tâche et cliquez sur la flèche haut ou bas pour le replacer selon l’ordre de tri. Les colonnes des résultats de recherche sont triées en fonction de l’ordre dans lequel elles sont répertoriées à cet endroit.
   * (Facultatif) Pour trier une colonne dans l’ordre décroissant, sélectionnez la case à cocher située en regard du nom de l’élément. Si la case à cocher n’est pas sélectionnée, la colonne est triée dans l’ordre croissant.

1. Cliquez sur l’onglet Enregistrer.
1. (Facultatif) Si vous créez un modèle de recherche, affectez-lui un nom unique. Si vous n’indiquez pas un nom unique, vous risquez de remplacer un modèle existant.
1. Cliquez sur le bouton Enregistrer.

## Suppression d’un modèle de recherche  {#delete-a-search-template}

1. Dans l’onglet Identification, sélectionnez un nom dans la liste Nom du modèle de recherche.
1. Cliquez sur Supprimer ce modèle, puis sur OK.

