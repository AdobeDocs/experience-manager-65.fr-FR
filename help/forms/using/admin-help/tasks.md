---
title: Utilisation de tâches
seo-title: Utilisation de tâches
description: Utilisez la page Recherche de tâche pour rechercher les tâches par nom d’utilisateur ou par identificateur de tâche. Découvrez l’utilisation des tâches.
seo-description: Utilisez la page Recherche de tâche pour rechercher les tâches par nom d’utilisateur ou par identificateur de tâche. Découvrez l’utilisation des tâches.
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 68%

---


# Utilisation de tâches {#working-with-tasks}

Utilisez la page Recherche de tâche pour rechercher les tâches par nom d’utilisateur ou par identificateur de tâche. Les résultats de la recherche s’affichent dans la page Liste de tâches où vous pouvez accéder à l’historique d’une tâche. Vous pouvez également réaffecter une tâche si trop de tâches ont été affectées à un même utilisateur, ou si une tâche lui a été affectée par erreur.

>[!NOTE]
>
>les recherches de tâches ne renvoient aucun résultat pour les noms d’utilisateur commençant par le signe dièse (#). Dans la mesure du possible, évitez de créer des noms d’utilisateur commençant par ce signe.

## Recherche de tâches associées à un utilisateur {#search-for-tasks-associated-with-a-user}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Recherche de tâche.
1. Dans Rechercher par, sélectionnez Nom d’utilisateur. Si vous connaissez une partie du nom de l’utilisateur que vous recherchez, saisissez-la dans ce champ. Cliquez sur Rechercher un utilisateur.
1. La page Rechercher un utilisateur s’affiche. Vous pouvez affiner davantage votre recherche en cherchant par nom ou adresse électronique d’utilisateur. Une fois l’utilisateur que vous recherchez trouvé, sélectionnez le bouton radio situé en regard de celui-ci et cliquez sur OK.
1. Par défaut, la recherche de tâches cherche les tâches actuellement attribuées à l’utilisateur. Pour rechercher également les tâches précédemment attribuées à l’utilisateur, sélectionnez Afficher la tâche non affectée. Pour rechercher aussi les tâches que l’utilisateur a terminées, sélectionnez Afficher la tâche terminée.
1. Cliquez sur Rechercher. La page Liste de tâches s’affiche, répertoriant les résultats de la recherche.

## Recherche d’une tâche dont vous connaissez l’identificateur  {#search-for-a-task-when-you-know-its-task-id}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Recherche de tâche.
1. Dans Rechercher par, sélectionnez ID de la tâche et saisissez l’identificateur de la tâche dans le champ.
1. Cliquez sur Rechercher. La page Liste de tâches s’affiche, répertoriant les résultats de la recherche.

## Utilisation de la liste de tâches  {#working-with-the-task-list}

Les résultats de la recherche de tâches sont affichés dans la page Liste de tâches. Vous pouvez sélectionner une tâche pour ouvrir la page Historique de la tâche. A partir de cette page, vous pouvez affecter la tâche à un autre utilisateur.

Les tâches sont affichées avec les informations suivantes :

**ID de tâche : entier positif attribué par** le processus des formulaires lorsque la tâche est instanciée (initiée par un utilisateur). Vous pouvez utiliser cet identificateur pour assurer le suivi de la tâche sur l’ensemble de son cycle de vie. Cliquez sur ID de la tâche pour afficher les informations relatives à l’historique de la tâche ou pour réaffecter la tâche à un autre utilisateur.

**Etat :** Affecté signifie que la tâche est actuellement affectée à l’utilisateur. Non affecté signifie que la tâche a été affectée auparavant à l’utilisateur. L’état peut également être Terminé.

**Activité :** affiche le formulaire et le nom d’une opération initiale ou de l’opération de traitement qui a généré la tâche.

**ID de processus :** entier positif attribué par le processus des formulaires lorsque le processus est instancié (c’est-à-dire lorsqu’un utilisateur ou une étape automatisée lance un processus). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version :** nom du processus, tel que défini dans Workbench.

**Application :** nom de l’application à laquelle appartient le processus, tel que défini dans Workbench.

**Date de création :** date et heure de création de la tâche.

## Affichage de l’historique de la tâche et réaffectation de tâches {#viewing-task-history-and-reassigning-tasks}

La page Historique de la tâche affiche la liste des utilisateurs et des groupes affectés à une tâche donnée.

Pour chaque affectation de tâche, la liste présente les informations suivantes :

**Nom :** nom de l’utilisateur.

**Etat :** Affecté signifie que la tâche est actuellement attribuée à l’utilisateur. Non affecté signifie que la tâche a été affectée auparavant à l’utilisateur.

**ID de liste de tâches :** identifiant numérique de la file d’attente d’utilisateur à laquelle appartient la tâche. Un processus peut être partagé par plusieurs utilisateurs.

**Type :** indique comment la tâche a été affectée :

**Initial :** la tâche a été affectée à l’utilisateur à l’origine.

**Transférer :** le propriétaire de la tâche d’origine a affecté la tâche à un autre utilisateur.

**Rejeter :** une tâche transférée a été rejetée ou une tâche a été renvoyée à une liste de travail sans avoir été terminée.

**Réclamation :** l’utilisateur a réclamé la tâche dans une liste de tâches partagée.

**Réaffectation :** une durée prédéterminée s’est écoulée (comme définie dans l’action Utilisateur dans Workbench) sans interaction de l’utilisateur et une tâche a été affectée à un autre utilisateur.

**Consulter :** Le propriétaire de la tâche a envoyé cette tâche à un autre utilisateur pour consultation qui peut ouvrir le formulaire, enregistrer les données, modifier les pièces jointes et les notes, mais ne peut pas terminer l&#39;étape. L’utilisateur doit renvoyer la tâche au propriétaire qui lui a demandé de la consulter.

**Réaffectation des administrateurs :** la tâche a été réaffectée par un administrateur.

**Date d’affectation :** date et heure auxquelles la tâche a été affectée à l’utilisateur.

### Affectation d’un nouvel utilisateur à une tâche {#assigning-a-new-user-to-a-task}

La page Affecter un utilisateur répertorie les utilisateurs pouvant être affectés à une tâche. Pour accéder à cette page, cliquez sur Affecter un nouvel utilisateur dans la page Historique de la tâche.

1. Dans le champ Rechercher de la page Affecter un utilisateur, saisissez une partie ou la totalité du nom de l’utilisateur ou de l’adresse électronique.
1. Sous Utilisation, sélectionnez Nom ou Adresse électronique, puis cliquez sur Rechercher. Les utilisateurs correspondant à la recherche s’affichent.
1. Dans la liste, sélectionnez l’utilisateur, puis cliquez sur OK. La page Historique de la tâche s’affiche, présentant la nouvelle affectation d’utilisateur.

