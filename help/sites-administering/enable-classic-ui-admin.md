---
title: Consoles d’administration
seo-title: Consoles d’administration
description: Comment utiliser les consoles d’administration disponibles dans AEM.
seo-description: Comment utiliser les consoles d’administration disponibles dans AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 69%

---


# Consoles d’administration{#admin-consoles}

Par défaut, la possibilité de basculer vers l’IU classique via les consoles d’administration a été désactivée. Par conséquent, les icônes contextuelles qui s’affichaient lors du survol du curseur sur certaines icônes de la console, et qui permettaient d’accéder à l’IU classique, ne sont plus affichées.

Every console that has a Classic UI version in `/libs/cq/core/content/nav` can be re-enabled individually so that the **Classic UI** option once again pops up over the console icon when it is moused over.

Dans cet exemple, nous réactivons l’IU classique pour la console Sites.

1. A l’aide de CRXDE Lite, recherchez le noeud correspondant à la console d’administration pour laquelle vous souhaitez réactiver l’interface utilisateur classique. Il se trouve sous :

   `/libs/cq/core/content/nav`

   Par exemple, 

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Sélectionnez le nœud correspondant à la console pour laquelle vous souhaitez réactiver l’IU classique. Dans notre exemple, nous allons recréer l’IU classique pour la console Sites.

   `/libs/cq/core/content/nav/sites`

1. Create an overlay using the **Overlay Node** option; for example:

   * **Chemin**: `/apps/cq/core/content/nav/sites`
   * **Emplacement du recouvrement**: `/apps/`
   * **Faire correspondre les types de nœuds** : actif (cochez la case)

1. Ajoutez la propriété booléenne suivante au nœud recouvert :

   `enableDesktopOnly = {Boolean}true`

1. L’option **IU classique** est toujours disponible en tant qu’option d’élément contextuel dans la console d’administration.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

Répétez ces étapes pour chaque console pour laquelle vous souhaitez réactiver l’accès à la version d’IU classique.