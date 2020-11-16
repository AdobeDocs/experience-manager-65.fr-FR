---
title: Éditeur
seo-title: Éditeur
description: Découvrez comment revenir à l’éditeur de l’interface utilisateur classique.
seo-description: Découvrez comment revenir à l’éditeur de l’interface utilisateur classique.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 90%

---


# Éditeur{#editor}

Par défaut, la possibilité de basculer vers de l’éditeur vers l’interface utilisateur classique a été désactivée.

Pour réactiver l’option **Ouvrir dans l’IU classique** dans le menu **informations sur la page**, procédez comme suit.

1. À l’aide de CRXDE Lite, recherchez le nœud suivant :

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Par exemple, 

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Create an overlay using the **Overlay Node** option; for example:

   * **Chemin**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Emplacement du recouvrement**: `/apps/`
   * **Faire correspondre les types de nœuds** : actif (cochez la case)

1. Ajoutez la propriété de texte à valeurs multiples ci-dessous au nœud de recouvrement :

   `sling:hideProperties = ["granite:hidden"]`

1. L’option **Ouvrir dans l’IU classique** est toujours disponible dans le menu des **Informations de la page** lors de la modification des pages.

   ![](assets/syui-03-2019-02-27-15-19-48.png)