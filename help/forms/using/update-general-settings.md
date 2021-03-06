---
title: Mise à jour des paramètres généraux
seo-title: Updating general settings
description: Mettez à jour les paramètres de l’application AEM Forms tels que l’écran d’accueil et recherchez les points et les options de pièces jointes.
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '388'
ht-degree: 100%

---

# Mise à jour des paramètres généraux{#updating-general-settings}

Les paramètres généraux de l’application AEM Forms vous permettent de définir des paramètres tels que la récupération des pièces jointes, le mode hors connexion, l’écran d’accueil, la catégorie par défaut et la fréquence d’enregistrement automatique.

## Mise à jour des paramètres généraux de votre application {#working-with-the-form}

Lorsque vous synchronisez votre application avec le serveur AEM Forms, les formulaires et les tâches définies sont téléchargés sur votre périphérique mobile.

La solution prête à l’emploi AEM Forms ne transfère pas les pièces jointes associées à chaque formulaire lorsque l’application est synchronisée.

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

   * Formulaires
   * Tâches
   * Favoris

* **Catégorie par défaut** : permet de sélectionner une catégorie de formulaires à afficher dans l’écran d’accueil. La sélection Tous affiche tous les formulaires dans l’écran d’accueil. Les catégories sont renseignées en fonction des formulaires chargés dans l’application. Les formulaires sont disponibles dans l’application en fonction des paramètres spécifiés dans le serveur AEM Forms.

* **Fréquence d’enregistrement** : permet de définir la fréquence à laquelle [l’application mobile enregistre les données](../../forms/using/autosave-data-app.md) en local.
* **Fréquence des synchronisations** : permet de définir la fréquence des [synchronisations de l’application mobile](../../forms/using/sync-app.md) avec le serveur AEM Forms en mode en ligne.
   **Effacer les données locales** : effacer la base de données, y compris les paramètres et données locales pour tous les utilisateurs et le stockage des fichiers du périphérique.

>[!NOTE]
>
>L’effacement du cache vous entraîne immédiatement hors de l’application.
>
>Toutefois, vous serez invité à confirmer l’opération d’effacement du cache.
