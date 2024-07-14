---
title: Synchronisation de l’application
description: Synchronisez l’application AEM Forms sur votre appareil mobile avec le serveur AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 100%

---

# Synchronisation de l’application{#synchronizing-the-app}

## Synchronisation de l’application {#synchronizing-the-app-1}

Les formulaires de votre application sont téléchargés à partir du serveur AEM Forms. Les formulaires sont téléchargés dans les onglets Tâches et Formulaires. Les brouillons créés à partir de formulaires sont téléchargés dans l’onglet Brouillons, et les brouillons créés à partir de tâches sont téléchargés dans l’onglet Tâches. Pour un formulaire autonome sur le serveur OSGi, les formulaires et les brouillons sont téléchargés respectivement dans les onglets Formulaires et Brouillons.

Lorsque vous remplissez et envoyez un formulaire, celui-ci est de nouveau chargé sur le serveur AEM Forms instantanément si l’application est en ligne. Les formulaires sont récupérés du serveur lors de la synchronisation de l’application. Les brouillons, toutefois, sont synchronisés avec le serveur immédiatement lorsque l’application est en ligne.

Lorsque vous êtes connecté avec le serveur AEM Forms, votre application est synchronisée par défaut toutes les 15 minutes. Vous avez toutefois la possibilité de modifier la fréquence de synchronisation. Vous pouvez également synchroniser manuellement l’application à tout moment.

**Synchronisation manuelle de l’application**

Sélectionnez le bouton Synchroniser ![sync-app](assets/sync-app.png) dans le coin inférieur droit de l’écran d’accueil.

**Modification de la fréquence de synchronisation**

1. Pour accéder à l’écran Paramètres, sélectionnez le bouton de menu dans le coin supérieur gauche de l’écran d’accueil, puis sélectionnez **Paramètres**.
1. Dans l’écran Paramètres, sélectionnez l’onglet Général.

   ![Paramètre de fréquence de synchronisation dans la fenêtre Paramètres généraux](assets/gen-settings-2.png)

1. Pour l’option de fréquence de synchronisation, sélectionnez la valeur située à droite de la fréquence de synchronisation.
1. Dans la liste déroulante, sélectionnez la nouvelle fréquence de synchronisation.

### Spécifications techniques {#technical-specifications}

* La logique principale de l’envoi de données d’application hors ligne au serveur AEM Forms est incluse dans runtime/offline/util/offline.js.
* Dans le fichier .js, l’appel de la fonction processOfflineSubmittedSavedTasks(...) envoie vers le serveur les tâches enregistrées/envoyées. Il gère également les erreurs ou les conflits dans le processus de synchronisation. En cas d’échec de l’envoi de la tâche, la tâche est marquée comme en échec dans l’application. En outre, la tâche reste dans votre boîte d’envoi.
* Les fonctions syncSubmittedTask() et syncSavedTask() effectuent des opérations sur des tâches particulières.
* L’appel de la fonction processOfflineSubmittedSavedTasks() est lancé par le composant de liste de tâches lorsqu’un utilisateur ou une utilisatrice choisit de synchroniser l’état hors ligne sur le serveur ou une synchronisation automatique par le thread d’arrière-plan.
