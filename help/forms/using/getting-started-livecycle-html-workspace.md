---
title: Prise en main de l’espace de travail AEM Forms
description: Découvrez comment commencer à utiliser l’espace de travail AEM Forms LiveCycle pour gérer vos processus d’automatisation d’entreprise.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '993'
ht-degree: 100%

---

# Prise en main de l’espace de travail AEM Forms {#getting-started-with-aem-forms-workspace}

Vous pouvez utiliser l’espace de travail AEM Forms pour effectuer les tâches suivantes :

* Démarrage d’un processus d’entreprise
* Afficher et agir sur les tâches qui vous sont affectées ou sur d’autres listes de tâches auxquelles vous avez accès
* Suivre des tâches qui font partie des processus que vous avez démarrés ou auxquels vous avez participé

## Parcourir l’espace de travail AEM Forms {#navigating-html-workspace}

Différents éléments de l’interface utilisateur de l’espace de travail AEM Forms s’affichent selon le processus et la tâche sur lesquels vous travaillez. Vous pouvez afficher ou masquer les onglets Résumé, Formulaires, Détails, Historique, Pièces jointes ou Notes, ou l’ensemble des boutons décrits dans cette aide à tout moment.

Vous pouvez naviguer dans l’interface utilisateur de l’espace de travail AEM Forms en utilisant l’une des méthodes suivantes :

* Cliquez sur les éléments de la barre de navigation supérieure pour accéder à l’option Démarrer le processus, Listes de tâches, Préférences, Suivi, Aide et Déconnexion.
* Cliquez sur l’onglet Démarrer le processus, Tâches ou Suivi pour accéder aux trois principales zones de travail.
* Sur les onglets Démarrer le processus, Tâches et Suivi, cliquez sur les éléments dans la liste du panneau de gauche pour accéder aux favoris, aux catégories de processus, aux modèles de recherche, aux brouillons ou aux tâches assignées. Utilisez la barre de défilement pour afficher d’autres éléments de la liste.
* Tous les boutons d’action (Approuver, Rejeter, Transférer, Consulter, Verrouiller et Partager) s’affichent dans le document et dans la propriété.
* Cliquez sur l’icône Toutes les options dans la barre de navigation, au bas de la page, pour transférer la tâche à un autre utilisateur ou à une autre utilisatrice, partager la tâche avec un autre utilisateur ou une autre utilisatrice, consulter un autre utilisateur ou une autre utilisatrice sur la tâche ou verrouiller la tâche.
* Dans l’onglet Historique, sélectionnez une tâche pour afficher les onglets Pièces jointes et Affectations pour cette tâche.
* Utilisez la touche de tabulation, les touches de direction et la barre d’espace pour naviguer dans l’espace de travail AEM Forms sans l’aide de la souris.

## Utilisation de l’espace de travail AEM Forms avec des lecteurs d’écran {#using-html-workspace-with-screen-readers}

L’espace de travail AEM Forms est une application HTML basée sur le Web compatible avec les lecteurs d’écran. Vous pouvez naviguer dans l’interface de l’espace de travail AEM Forms à l’aide du clavier.

Pour utiliser l’espace de travail AEM Forms avec un lecteur d’écran, gardez à l’esprit les points suivants :

* L’espace de travail AEM Forms est une application HTML standard conforme à tous les outils de lecteur d’écran standard. Vous n’avez pas besoin de script spécifique pour exécuter un outil de lecteur d’écran.
* La navigation dans l’espace de travail AEM Forms s’effectue par le biais des balises d’ancrage, qui peuvent être facilement accessibles au moyen des onglets.
* Le chargement des formulaires peut prendre quelques secondes. Le lecteur d’écran ne vous informe pas de manière audible que le formulaire est en cours de chargement et que vous devez attendre.

## Parcourir l’espace de travail AEM Forms à l’aide du clavier {#navigating-html-workspace-using-a-keyboard}

Lorsque vous naviguez dans l’espace de travail AEM Forms à l’aide du clavier, la navigation est conforme aux conventions d’accessibilité HTML. Dans certaines situations, l’ordre de tabulation ne suit pas l’ordre conventionnel classique. Les conseils suivants vous aident à naviguer dans l’interface :

* Si vous n’arrivez pas à quitter les barres d’outils situées dans la partie supérieure du navigateur avec la touche Tab, appuyez sur la combinaison de touches Ctrl+Tab pour entrer dans le contenu de la fenêtre du navigateur.
* L’aide de l’espace de travail AEM Forms s’ouvre dans une fenêtre de navigateur distincte. Après avoir consulté l’aide, le focus retourne à la fenêtre du navigateur qui contient l’espace de travail AEM Forms. Le menu Aide reste affiché lorsque le focus retourne à la fenêtre du navigateur.
* Lorsque vous ouvrez un formulaire pour démarrer un processus ou effectuer une tâche, le focus demeure avec l’élément existant et ne change pas sur le formulaire. Utilisez les touches de tabulation pour déplacer le focus sur le formulaire et parcourez-le. L’ordre de tabulation dans le formulaire dépend du type et de la conception du formulaire.

  Pour les formulaires PDF, lorsque vous allez jusqu’à la fin du formulaire en utilisant la touche Tab ou lorsque vous soumettez le formulaire, la barre d’adresse du navigateur devient active. Vous devez de nouveau passer les menus (mais pas le formulaire en entier) à l’aide de la touche Tab pour accéder aux boutons d’action du formulaire, tels que Enregistrer comme brouillon et Terminer. Si le formulaire est toujours ouvert, vous pouvez également passer les boutons et le retourner dans le formulaire.

## Gestion des préférences {#managing-preferences}

Vous pouvez définir les diverses préférences de l’espace de travail AEM Forms dans les catégories suivantes :

**Absence du bureau :** définissez des préférences pour contrôler comment vos tâches sont affectées à d’autres personnes lorsque vous êtes absent du bureau. Voir [Configuration des préférences d’absence du bureau](todo-lists.md#setting-out-of-office-preferences).

**Files d’attente :** définissez des préférences de partage de votre liste Tâches avec d’autres utilisateurs ou utilisatrices ou de demande d’accès à la liste d’un autre utilisateur ou d’une autre utilisatrice. Voir [Utilisation des tâches des files d’attente de groupe et partagées](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**Paramètres de l’interface :** définit des préférences pour l’interaction avec l’espace de travail AEM Forms. Voir [Définition des préférences de l’interface utilisateur](#set-user-interface-preferences).

### Définition des préférences d’interface utilisateur {#set-user-interface-preferences}

Définissez les préférences de l’interface utilisateur dans l’onglet Préférences > Paramètres de l’interface. Les préférences suivantes sont disponibles :

* **Emplacement de démarrage :** définit la page qui s’affiche lorsque vous vous connectez à l’espace de travail AEM Forms. Les quatre options disponibles sont Démarrer le processus, Tâches, Suivi et Favoris.
* **Message d’invite de fermeture de session :** définit si vous recevez un message d’invite de confirmation de fermeture de session après avoir cliqué sur Fermer la session.
* **Format de date** : indique le format d’affichage de la date utilisé dans l’espace de travail AEM Forms.
* **Format d’heure** : indique le format d’affichage de l’heure utilisé dans l’espace de travail AEM Forms.
* **Notifier les événements de tâche par courrier électronique :** indique si vous recevez un courrier électronique de notification pour les événements de tâche, y compris les affectations de tâche, les rappels et les échéances pour les tâches de votre liste Tâches et des listes Tâches de groupe auxquelles vous appartenez.
* **Joindre les formulaires dans un courrier électronique :** définit si une copie du formulaire est attachée aux courriers électroniques de notification. Les pièces jointes sont prises en charge uniquement pour les formulaires PDF et XDP.
* **Enregistrer régulièrement le brouillon :** définit si les brouillons de formulaires sont régulièrement enregistrés ou non, et ce de manière automatique. Pour enregistrer vos brouillons régulièrement, activez cette option et définissez la durée d’enregistrement automatique de 1 à 30 minutes. Si l’enregistrement automatique est activé et qu’un utilisateur ou une utilisatrice travaille sur un brouillon, ce dernier est enregistré de manière périodique. Le brouillon n’est enregistré automatiquement que lorsqu’il a été modifié depuis le dernier enregistrement ou l’enregistrement automatique. Lorsque le brouillon est enregistré, un message d’alerte s’affiche à l’écran.
