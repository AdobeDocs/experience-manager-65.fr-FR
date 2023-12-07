---
title: Personnalisation des modèles de recherche
description: Vous pouvez créer des modèles de recherche à utiliser dans Workspace pour rechercher des instances de processus à partir des pages de tâches et de suivi. Vous pouvez également modifier ou supprimer des modèles de recherche existants.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bf69de86-2ca6-4d21-936c-07c1debacfa0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 11%

---

# Personnalisation des modèles de recherche {#customizing-search-templates}

Vous pouvez créer des modèles de recherche à utiliser dans Workspace pour rechercher des instances de processus à partir des pages de tâches et de suivi. Vous pouvez également modifier ou supprimer des modèles de recherche existants.

Lors de la création ou de la modification d’un modèle de recherche, vous pouvez spécifier la disposition et l’ordre de tri des résultats de la recherche. Cependant, les utilisateurs peuvent modifier ces paramètres dans Workspace une fois les résultats de recherche affichés.

Vous pouvez créer autant de modèles de recherche que nécessaire.

>[!NOTE]
>
>Lors de l’enregistrement d’un modèle de recherche, vous devez lui attribuer un nom unique. Dans le cas contraire, un modèle existant peut être remplacé sans message d’avertissement.

## Création d’un modèle de recherche simple {#create-a-simple-search-template}

1. Dans Administration Console, cliquez sur Services > Workspace > Modèles de recherche.
1. Indiquez l’objet du modèle dans le champ Description du modèle de recherche de l’onglet Identification .
1. (Facultatif) Cliquez sur l’onglet Critères et indiquez les critères de recherche du modèle.
1. Cliquez sur l’onglet Enregistrer , saisissez un nom unique pour le modèle, puis cliquez sur Enregistrer.

## Créer ou modifier un modèle de recherche {#create-or-edit-a-search-template}

1. Dans Administration Console, cliquez sur Services > Workspace > Modèles de recherche.
1. (Facultatif) Si vous modifiez un modèle existant ou utilisez un modèle existant comme base d’un nouveau modèle, sélectionnez le modèle dans la liste Nom du modèle de recherche .
1. Dans la zone Description du modèle de recherche, indiquez l’objectif du modèle.
1. (Facultatif) Dans la zone Instructions à l’intention des utilisateurs, indiquez les instructions qui peuvent vous aider à utiliser le modèle. Ces instructions s’affichent dans Workspace lorsqu’un utilisateur sélectionne le modèle de recherche.
1. Cliquez sur l’onglet Critères . C’est là que vous définissez un ou plusieurs critères de recherche. Pour ajouter un critère de recherche :

   * Dans la partie supérieure de l’onglet Critère, sélectionnez un élément de processus ou de tâche.

     **Conseil** : *si vous avez préalablement sélectionné l’élément Nom du processus et que vous avez indiqué un processus, toute variable définie pour ce processus peut également être sélectionnée.*

     **Conseil** : *si vous avez sélectionné l’élément de tâche visible, les utilisateurs seront en mesure de supprimer des tâches terminées des résultats de recherche.*

     Les champs de critères de recherche de l’élément sélectionné apparaissent au bas de l’onglet Critère.

   * Pour chaque élément de processus, élément de tâche et variable de processus sélectionné, renseignez les champs de recherche correspondants au bas de l’onglet Critère :

      * Sélectionnez un opérateur relationnel (par exemple &quot;être égal à&quot;) dans la liste fournie et indiquez la valeur de l’opérande dans la zone située à côté.
      * (Facultatif) Pour permettre aux utilisateurs de modifier la valeur de l’opérande dans Workspace, sélectionnez Autoriser l’utilisateur à modifier l’opérande.
      * (Facultatif) Pour permettre aux utilisateurs de modifier l’opérateur relationnel, sélectionnez Autoriser l’utilisateur à sélectionner un autre opérateur relationnel. Dans la liste qui s&#39;affiche, sélectionnez les opérateurs qui seront disponibles pour l&#39;utilisateur.

     **Conseil**: *Si vous avez sélectionné Process Name en tant qu’élément, vous pouvez cliquer sur l’icône en regard du champ de l’opérande pour afficher une liste dans laquelle vous pouvez sélectionner un processus en cours d’exécution sur le serveur Forms. Après avoir sélectionné un processus, toute variable définie pour ce processus peut être sélectionnée dans Variables de processus, dans la partie supérieure de l’onglet Critère.*

     **Conseil** : *vous pouvez supprimer un élément du modèle de recherche en cliquant sur l’icône de suppression en regard du critère de recherche de l’élément.*

1. (Facultatif) Pour chaque en-tête de colonne à afficher dans les résultats de recherche, cliquez sur l’onglet Disposition et procédez comme suit :

   * Sélectionnez un élément de processus ou de tâche et cliquez sur la flèche droite pour le déplacer vers la liste Colonnes à reporter.
   * Dans la liste Colonnes à reporter , sélectionnez l’élément de processus ou de tâche et cliquez sur la flèche Haut ou Bas pour le placer dans l’ordre dans la colonne. Les en-têtes de colonne des résultats de recherche s’affichent dans l’ordre dans lequel ils sont répertoriés ici.
   * (Facultatif) Pour modifier le nom de l’élément de l’en-tête de colonne, sélectionnez l’élément dans la liste Colonnes à reporter et indiquez le nouveau nom.

   >[!NOTE]
   >
   >La mise en page spécifiée dans le modèle de recherche remplace les préférences de l’utilisateur spécifiées pour les en-têtes de colonne dans Workspace.

1. (Facultatif) Pour chaque colonne à trier dans les résultats de recherche, cliquez sur l’onglet Tri et procédez comme suit :

   * Sélectionnez un élément de processus ou de tâche et cliquez sur la flèche droite pour le déplacer vers la liste Ordre de tri.
   * Dans la liste Ordre de tri, sélectionnez l’élément de processus ou de tâche, puis cliquez sur la flèche Haut ou Bas pour le placer dans l’ordre de tri. Les colonnes des résultats de recherche seront triées selon l’ordre dans lequel elles sont répertoriées ici.
   * (Facultatif) Pour trier une colonne dans l’ordre décroissant, cochez la case en regard du nom de l’élément. Si cette case n’est pas cochée, la colonne est triée par ordre croissant.

1. Cliquez sur l’onglet Enregistrer .
1. (Facultatif) Si vous créez un modèle de recherche, attribuez-lui un nom unique. Si vous ne spécifiez pas de nom unique, vous pouvez remplacer un modèle existant.
1. Cliquez sur le bouton Enregistrer .

## Suppression d’un modèle de recherche {#delete-a-search-template}

1. Dans l’onglet Identification , sélectionnez un nom dans la liste Nom du modèle de recherche .
1. Cliquez sur Supprimer ce modèle, puis sur OK.
