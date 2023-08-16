---
title: Recouvrements
description: Adobe Experience Manager applique le principe des incrustations pour vous permettre d’étendre et de personnaliser les consoles et d’autres fonctionnalités.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 35%

---

# Recouvrements{#overlays}

Adobe Experience Manager (AEM), et auparavant CQ, applique depuis longtemps le principe des incrustations pour vous permettre d’étendre et de personnaliser les [consoles](/help/sites-developing/customizing-consoles-touch.md) et d’autres fonctionnalités (par exemple, [création de pages](/help/sites-developing/customizing-page-authoring-touch.md)).

Recouvrement est un terme utilisé dans de nombreux contextes. Dans ce contexte (extension d’AEM), une superposition signifie prendre la fonctionnalité prédéfinie et y imposer vos propres définitions (pour personnaliser la fonctionnalité standard).

Dans une instance standard, la fonctionnalité prédéfinie est conservée sous `/libs` et il est recommandé de définir votre recouvrement (vos personnalisations) sous le `/apps` branche. AEM utilise un chemin de recherche pour localiser une ressource, en commençant par la branche `/apps`, puis la branche `/libs` (le [chemin de recherche peut être configuré](#configuring-the-search-paths)). Ce mécanisme signifie que votre recouvrement (et les personnalisations qui y sont définies) est prioritaire.

Depuis AEM 6.0, des modifications ont été apportées à la manière dont les superpositions sont implémentées et utilisées :

* AEM 6.0 et versions ultérieures - pour [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)incrustations liées (IU tactile)

   * Méthode

      * Recréez la structure `/libs` appropriée sous `/apps`.

        Cela ne nécessite aucune copie 1:1 ; [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) est utilisé pour effectuer des références croisées avec les définitions d’origine qui sont requises. Sling Resource Merger fournit des services pour accéder aux ressources et les fusionner avec des mécanismes de différenciation.

      * Sous `/apps`, apportez toute modification.

   * Avantages

      * Plus résistant aux modifications sous `/libs`.
      * Ne redéfinissez que ce qui est nécessaire.

* Superpositions et superpositions non Granite avant AEM 6.0

   * Méthode

      * Copiez le contenu de `/libs` vers `/apps`.

        Copiez la sous-branche entière, y compris les propriétés.

      * Sous `/apps`, apportez toute modification.

   * Inconvénients

      * La modification d’un élément sous `/libs` n’entraînera pas la perte des changements effectués. Cependant, il se peut que vous deviez recréer certaines modifications affectant votre recouvrement sous `/apps`.

>[!CAUTION]
>
>La variable [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) et les méthodes associées ne peuvent être utilisées qu’avec [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Cela signifie que la création d’un recouvrement avec une ossature n’est appropriée que pour l’interface utilisateur (IU) tactile standard.
>
>Les superpositions pour d’autres zones (y compris l’interface utilisateur classique) impliquent la copie du noeud approprié et de l’ensemble de la sous-structure, puis l’apport des modifications requises.

Les recouvrements sont la méthode recommandée pour de nombreuses modifications, telles que [configuration des consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [création de votre catégorie de sélection dans l’explorateur de ressources dans le panneau latéral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (utilisé lors de la création de pages). Ils sont requis pour les raisons suivantes :

* ***Ne pas* apportez des modifications dans le `/libs` branche **Toute modification que vous apportez peut être perdue, car cette branche est sujette à des modifications lorsque vous :

   * mise à niveau sur votre instance
   * appliquer un correctif ;
   * installer un Feature Pack ;

* Ils centralisent vos modifications à un seul emplacement ; ce qui facilite le suivi, la migration, la sauvegarde ou le débogage de vos modifications, le cas échéant.

## Configuration des chemins de recherche {#configuring-the-search-paths}

Pour les superpositions, la ressource diffusée est un agrégat des ressources et propriétés récupérées, en fonction des chemins de recherche qui peuvent être définis :

* La ressource **Resolver Search Path**, telle qu’elle est définie dans la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) pour **Apache Sling Resource Resolver Factory**.

   * L’ordre descendant des chemins de recherche indique leurs priorités respectives.
   * Dans une installation standard, les principales valeurs par défaut sont les suivantes : `/apps`, `/libs` - pour que le contenu de `/apps` a une priorité plus élevée que celle de `/libs` (c’est-à-dire : *superpositions* it).

* Deux utilisateurs du service ont besoin d’un accès JCR:READ à l’emplacement de stockage des scripts. Ces utilisateurs sont : components-search-service (utilisé par les composants de cache et d’accès com.day.cq.wcm.coreto) et sling-scripting (utilisé par org.apache.sling.servlets.resolver pour rechercher des servlets).
* La configuration suivante doit également être définie en fonction de l’emplacement de stockage des scripts (dans cet exemple sous /etc, /libs ou /apps).

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* Enfin, le Servlet Resolver doit également être configuré (dans cet exemple, pour ajouter /etc).

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## Exemple d’utilisation {#example-of-usage}

Voici quelques exemples présentés dans les cas suivants :

* [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Personnalisation de la création de pages](/help/sites-developing/customizing-page-authoring-touch.md)
