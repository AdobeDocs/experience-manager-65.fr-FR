---
title: Écran d’accueil
description: Description des composants de l’écran d’accueil de l’application AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 28%

---

# Écran d’accueil{#home-screen}

Lorsque vous vous connectez à l’application AEM Forms, vous êtes redirigé vers l’écran d’accueil.

## Écran d’accueil par défaut {#default-home-screen}

Par défaut, l’écran d’accueil affiche tous les formulaires, y compris les points de départ et les tâches (si le serveur connecté est activé pour le workflow d’AEM Forms), avec les vignettes associées. Vous pouvez spécifier les miniatures dans le serveur AEM Forms.

La figure suivante est annotée avec des légendes aux composants essentiels sur l’écran d’accueil par défaut.

![Écran d’accueil de l’application Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Bouton de menu :** appuyez sur le bouton **Menu** pour accéder aux tâches, aux formulaires, à la boîte d’envoi et aux paramètres. Si votre application AEM Forms est connectée à un serveur AEM Forms JEE, l’option Tâches s’affiche. L’option Tâches stocke également les brouillons créés à partir de tâches dans un processus. Pour les serveurs OSGi AEM Forms, l’option Tâches est masquée. La boîte d’envoi stocke les formulaires enregistrés et les brouillons avant qu’ils ne se synchronisent avec le serveur. Tous les formulaires enregistrés et les brouillons de la boîte d’envoi sont chargés sur le serveur AEM Forms lorsque l’application est [synchronisé avec le serveur](../../forms/using/sync-app.md). Pour plus d’informations sur les paramètres, voir [Mise à jour des paramètres généraux](../../forms/using/update-general-settings.md).
1. **Tâche ou formulaire**: appuyez sur la tâche ou le formulaire répertorié à utiliser.
1. **Points de suspension horizontaux**: indique que les actions sont disponibles pour le formulaire. Appuyez sur les points de suspension pour afficher les actions et la description fournies par l’auteur. Les options **Supprimer le brouillon** et **Terminé** sont visibles lorsque vous appuyez sur les points de suspension.
1. **Icône Actualiser**: appuyez sur l’icône d’actualisation afin de synchroniser votre application avec le serveur AEM Forms.

### Personnalisation de l’écran d’accueil {#customizing-the-home-screen}

![Paramètres généraux](assets/gen-settings.png)

Vous pouvez modifier l’écran d’accueil par défaut de l’application, soit à partir de l’onglet **[Paramètres généraux](../../forms/using/update-general-settings.md)** de l’application, soit à partir de l’onglet **Préférences** dans Workspace HTML.

La modification apportée au paramètre de l’écran d’accueil de l’application affecte l’écran d’accueil de l’utilisateur actuellement connecté ou de l’utilisateur sur le périphérique mobile actif.

Toutefois, la modification apportée à HTML Workspace s’applique à tous les utilisateurs de l’application AEM Forms connectés au serveur AEM Forms.
