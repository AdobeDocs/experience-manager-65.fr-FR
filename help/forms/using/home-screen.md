---
title: Écran d’accueil
seo-title: Écran d’accueil
description: Description des composants de l’écran d’accueil de l’application AEM Forms.
seo-description: Description des composants de l’écran d’accueil de l’application AEM Forms
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 85%

---

# Ecran d’accueil{#home-screen}

Lorsque vous vous connectez à l’application AEM Forms, vous êtes redirigé vers l’écran d’accueil.

## Écran d’accueil par défaut {#default-home-screen}

Par défaut, l’écran d’accueil affiche tous les formulaires, y compris les points de départ et les tâches (si le serveur connecté est activé pour le flux de travail d’AEM forms), avec les vignettes associées. Vous pouvez spécifier les vignettes dans le serveur AEM Forms.

La figure suivante est annotée avec les légendes des principaux composants de l’écran d’accueil.

![Écran d’accueil de l’application Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Bouton** Menu : Appuyez sur le bouton  **** Menubutton pour accéder aux tâches, à Forms, à la boîte d’envoi et aux paramètres. Si votre application AEM Forms est connectée à un serveur AEM Forms JEE, vous pouvez voir l’option Tâches. L’option de tâches stocke également les brouillons créés à partir des tâches dans un processus. Pour les serveurs AEM Forms OSGi, l’option Tâches est masquée. La boîte d’envoi stocke les formulaires enregistrés et les brouillons avant sa synchronisation avec le serveur. Tous les formulaires et brouillons enregistrés dans la boîte d’envoi sont chargés sur le serveur AEM Forms lorsque l’application est [synchronisée avec le serveur](../../forms/using/sync-app.md). Pour plus d’informations sur les paramètres, voir [Mise à jour des paramètres généraux](../../forms/using/update-general-settings.md).
1. **Tâche ou formulaire** : Appuyez sur la tâche ou le formulaire répertorier afin de pouvoir travailler dessus.
1. **Points de suspension horizontaux** : Indique si les actions sont disponibles pour le formulaire. Tapez sur les points de suspension pour afficher les actions et la description fournie par l’auteur. L’option **Supprimer le brouillon** et **Complète** est visible lorsque vous appuyez sur les points de suspension.
1. **Icône Synchronisation** : appuyez sur l’icône d’actualisation pour synchroniser votre application avec le serveur AEM Forms.

### Personnalisation de l’écran d’accueil  {#customizing-the-home-screen}

![Paramètres généraux](assets/gen-settings.png)

Vous pouvez modifier l’écran d’accueil par défaut de l’application, soit à partir de l’onglet **[Paramètres généraux](../../forms/using/update-general-settings.md)** de l’application, soit à partir de l’onglet **Préférences** dans Workspace HTML.

Toute modification apportée au paramètre d’écran d’accueil de l’application s’applique à l’écran d’accueil de l’utilisateur connecté ou travaillant sur le périphérique mobile en cours.

Toutefois, la modification apportée à Workspace HTML s’applique à l’ensemble des utilisateurs de l’application AEM Forms connectés au serveur AEM Forms.
