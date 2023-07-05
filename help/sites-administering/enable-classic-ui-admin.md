---
title: Admin Consoles
seo-title: Admin Consoles
description: Découvrez comment utiliser les Admin Console disponibles dans AEM.
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: 729e5eb99b0c14f3d2fd8c3f4ec636f7fb52124f
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 61%

---


# Admin Consoles{#admin-consoles}

Par défaut, la possibilité de basculer vers l’IU classique via les consoles d’administration a été désactivée. Par conséquent, les icônes contextuelles qui s’affichaient lorsque vous survoliez certaines icônes de console, permettant d’accéder à l’IU classique, ne s’affichent plus.

Chaque console qui possède une version d’IU classique dans `/libs/cq/core/content/nav` peut être réactivée individuellement afin que l’option **IU classique** s’affiche à nouveau lors du survol du curseur sur l’icône de la console.

Dans cet exemple, nous réactivons l’IU classique pour la console Sites.

1. À l’aide de CRXDE Lite, recherchez le nœud correspondant à la console d’administration pour laquelle vous souhaitez réactiver l’IU classique. Il se trouve sous :

   `/libs/cq/core/content/nav`

   Par exemple :

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Sélectionnez le nœud correspondant à la console pour laquelle vous souhaitez réactiver l’IU classique. Dans notre exemple, nous réactiverons l’IU classique pour la console Sites.

   `/libs/cq/core/content/nav/sites`

1. Créez un recouvrement à l’aide de l’option **Nœud de recouvrement** ; par exemple :

   * **Chemin** : `/apps/cq/core/content/nav/sites`
   * **Emplacement du recouvrement** : `/apps/`
   * **Faire correspondre les types de noeud**: principal (cochez la case)

1. Ajoutez la propriété booléenne suivante au nœud recouvert :

   `enableDesktopOnly = {Boolean}true`

1. Le **IU classique** est à nouveau disponible sous la forme d’une option contextuelle dans la console d’administration.

   ![Option contextuelle de l’IU classique](assets/syui-01-2019-02-27-15-16-55.png)

Répétez ces étapes pour chaque console pour laquelle vous souhaitez réactiver l’accès à la version de l’interface utilisateur classique.
