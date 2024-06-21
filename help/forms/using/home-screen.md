---
title: Écran d’accueil
description: Description des composants de l’écran d’accueil de l’application AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 100%

---

# Écran d’accueil{#home-screen}

Lorsque vous vous connectez à l’application AEM Forms, vous êtes redirigé(e) vers l’écran d’accueil.

## Écran d’accueil par défaut {#default-home-screen}

Par défaut, l’écran d’accueil affiche tous les formulaires, y compris les points de départ et les tâches (si le serveur connecté est activé pour le workflow d’AEM Forms), avec les vignettes associées. Vous pouvez spécifier les vignettes dans le serveur AEM Forms.

La figure suivante est annotée avec les légendes des principaux composants de l’écran d’accueil.

![Écran d’accueil de l’application Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Bouton de menu :** sélectionnez le bouton **Menu** pour accéder aux tâches, aux formulaires, à la boîte d’envoi et aux paramètres. Si votre application AEM Forms est connectée à un serveur AEM Forms JEE, l’option Tâches s’affiche. L’option Tâches stocke également les brouillons créés à partir de tâches dans un processus. Pour les serveurs AEM Forms OSGi, l’option Tâches est masquée. La boîte d’envoi stocke les formulaires et les brouillons enregistrés avant de se synchroniser avec le serveur. Tous les formulaires et brouillons enregistrés dans la boîte d’envoi sont chargés sur le serveur AEM Forms lorsque l’application est [synchronisée avec le serveur](../../forms/using/sync-app.md). Pour plus d’informations sur les paramètres, consultez [Mise à jour des paramètres généraux](../../forms/using/update-general-settings.md).
1. **Tâche ou formulaire** : sélectionnez la tâche ou le formulaire répertorié à utiliser.
1. **Points de suspension horizontaux** : indique que les actions sont disponibles pour le formulaire. Appuyez sur les points de suspension pour afficher les actions et la description fournies par l’auteur. Les options **Supprimer le brouillon** et **Terminé** sont visibles lorsque vous sélectionnez les points de suspension.
1. **Icône Actualiser** : sélectionnez l’icône d’actualisation afin de synchroniser votre application avec le serveur AEM Forms.

### Personnalisation de l’écran d’accueil {#customizing-the-home-screen}

![Paramètres généraux](assets/gen-settings.png)

Vous pouvez modifier l’écran d’accueil par défaut de l’application, soit à partir de l’onglet **[Paramètres généraux](../../forms/using/update-general-settings.md)** de l’application, soit à partir de l’onglet **Préférences** dans Workspace HTML.

Toute modification apportée au paramètre d’écran d’accueil de l’application s’applique à l’écran d’accueil de la personne connectée ou travaillant sur l’appareil mobile actuel.

Toutefois, la modification apportée à Workspace HTML s’applique à l’ensemble des utilisateurs et utilisatrices de l’application AEM Forms connectés au serveur AEM Forms.
