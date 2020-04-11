---
title: Mise à jour des paramètres généraux
seo-title: Mise à jour des paramètres généraux
description: Mettez à jour les paramètres de l’application AEM Forms tels que l’écran d’accueil et recherchez les points et les options de pièces jointes.
seo-description: Mettez à jour les paramètres de l’application AEM Forms tels que l’écran d’accueil et recherchez les points et les options de pièces jointes.
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Mise à jour des paramètres généraux{#updating-general-settings}

Les paramètres généraux de l’application AEM Forms vous permettent de définir des paramètres tels que la récupération des pièces jointes, le mode hors connexion, l’écran d’accueil, la catégorie par défaut et la fréquence d’enregistrement automatique.

## Mise à jour des paramètres généraux de votre application {#working-with-the-form}

Lorsque vous synchronisez votre application avec le serveur AEM Forms, les formulaires et les tâches définies sont téléchargés sur votre périphérique mobile.

La solution d’application AEM Forms prête à l’emploi ne télécharge pas les pièces jointes associées à chaque formulaire lorsque votre application est synchronisée.

Dans l’onglet Général, modifiez les pièces jointes de téléchargement, le mode hors connexion, l’écran d’entrée, les enregistrements automatiques et les paramètres de synchronisation. Vous pouvez modifier [l’écran d’accueil](../../forms/using/home-screen.md) de l’application.

**Accédez à l’onglet Général dans l’écran Paramètres**

1. Pour accéder à l’écran Paramètres, appuyez sur le bouton de menu dans le coin supérieur gauche de l’écran d’accueil, puis appuyez sur **Paramètres**.
1. Dans l’écran des paramètres, appuyez sur l’onglet General (Général).

   ![Paramètres généraux de l’application AEM Forms](assets/gen-settings-1.png)

   Ecran Paramètres généraux

   >[!NOTE]
   >
   >Les options peuvent s’afficher différemment sur différents périphériques mobiles.

### Paramètres généraux {#general-settings}

Vous pouvez apporter les modifications suivantes aux paramètres de votre application.

* **Extraire les pièces jointes de la tâche** : spécifie le téléchargement ou non des pièces jointes associées lors du téléchargement d’une tâche sur votre application.
* **Mode hors ligne** : activer ou désactiver le service hors ligne de l’application AEM Forms. Voir [Travailler en mode hors ligne](/help/forms/using/work-offline-mode.md) pour plus de détails.
* **Écran d’accueil** : définir l’emplacement de départ ([écran d’accueil](../../forms/using/home-screen.md)) de l’application.
 Options disponibles :

   * Forms
   * Tâches
   * Favoris

* **Catégorie par défaut** : permet de sélectionner une catégorie de formulaires à afficher dans l’écran d’accueil. La sélection Tous affiche tous les formulaires dans l’écran d’accueil. Les catégories sont renseignées en fonction des formulaires chargés dans l’application. Les formulaires sont disponibles dans l’application en fonction des paramètres spécifiés dans le serveur AEM Forms.

* **Fréquence** d’enregistrement automatique : Pour définir la fréquence à laquelle votre application [mobile enregistre les données](../../forms/using/autosave-data-app.md) de formulaire localement.
* **Fréquence** de synchronisation : Pour définir la fréquence de synchronisation [de votre application](../../forms/using/sync-app.md) mobile avec le serveur AEM Forms en mode en ligne.
   **Effacer les données locales** : effacer la base de données, y compris les paramètres et données locales pour tous les utilisateurs et le stockage des fichiers du périphérique.

>[!NOTE]
>
>L’effacement du cache vous entraîne immédiatement hors de l’application.
>
>Toutefois, vous serez invité à confirmer l’opération d’effacement du cache.
