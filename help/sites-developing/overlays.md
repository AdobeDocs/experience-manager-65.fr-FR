---
title: Recouvrements
description: Adobe Experience Manager applique le principe des recouvrements pour vous permettre d’étendre et de personnaliser les consoles et d’autres fonctionnalités.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 100%

---

# Recouvrements{#overlays}

Adobe Experience Manager (AEM), et auparavant CQ, applique depuis longtemps le principe des recouvrements pour vous permettre d’étendre et de personnaliser les [consoles](/help/sites-developing/customizing-consoles-touch.md) et d’autres fonctionnalités (par exemple, la [création de pages](/help/sites-developing/customizing-page-authoring-touch.md)).

Le terme « recouvrement » est utilisé dans de nombreux contextes. Dans ce contexte (extension d’AEM), le recouvrement désigne l’utilisation de la fonctionnalité prédéfinie et l’application de vos propres définitions par-dessus (afin de personnaliser la fonctionnalité standard).

Dans une instance standard, la fonctionnalité prédéfinie est conservée sous `/libs` et il est conseillé de définir votre recouvrement (personnalisations) sous la branche `/apps`. AEM utilise un chemin de recherche pour localiser une ressource, en commençant par la branche `/apps`, puis la branche `/libs` (le [chemin de recherche peut être configuré](#configuring-the-search-paths)). Ce mécanisme signifie que votre recouvrement (et les personnalisations qui y sont définies) est prioritaire.

Depuis AEM 6.0, des modifications ont été apportées à la manière dont les recouvrements sont mis en place et utilisés :

* AEM 6.0 et versions ultérieures - pour les recouvrements liés à [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) (c’est-à-dire, l’IU optimisée pour les écrans tactiles)

   * Méthode

      * Recréez la structure `/libs` appropriée sous `/apps`.

        Cela ne nécessite aucune copie 1:1 ; [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) est utilisé pour effectuer des références croisées avec les définitions d’origine qui sont requises. Sling Resource Merger propose des services pour accéder à des ressources et les fusionner par le biais de mécanismes de différenciation (diff).

      * Sous `/apps`, apportez vos éventuelles modifications.

   * Avantages

      * Plus résistant aux modifications sous `/libs`.
      * Vous ne devez redéfinir que ce qui est réellement nécessaire.

* Recouvrements non liés à Granite et recouvrements avant AEM 6.0

   * Méthode

      * Copiez le contenu de `/libs` vers `/apps`.

        Copiez la sous-branche entière, y compris les propriétés.

      * Sous `/apps`, apportez vos éventuelles modifications.

   * Inconvénients

      * La modification d’un élément sous `/libs` n’entraînera pas la perte des changements effectués. Cependant, il se peut que vous deviez recréer certaines modifications affectant votre recouvrement sous `/apps`.

>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) et les méthodes connexes ne peuvent être utilisés qu’avec [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Cela signifie que la création d’un recouvrement avec une ossature n’est appropriée que pour l’interface utilisateur (IU) tactile standard.
>
>Les recouvrements pour d’autres zones (y compris l’interface utilisateur classique) impliquent la copie du nœud approprié et de l’ensemble de la sous-structure, puis l’apport des modifications requises.

Il est conseillé de recourir aux recouvrements pour de nombreuses modifications, par exemple, pour [configurer vos consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [créer votre catégorie de sélection dans l’explorateur de ressources au niveau du panneau latéral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (lors de la création de pages). Ils sont requis pour les raisons suivantes :

* Vous ***ne devez pas* effectuer de modifications dans la `/libs`branche **.
Les modifications que vous effectuez risquent d’être perdues, car cette branche est sensible aux modifications lorsque vous :

   * procédez à une mise à niveau sur votre instance
   * appliquez un correctif
   * installez un Pack de fonctionnalités

* Ils centralisent vos modifications dans un seul emplacement ; ils facilitent le suivi, la migration, la sauvegarde ou le débogage de vos modifications, suivant les besoins.

## Configurer les chemins de recherche {#configuring-the-search-paths}

Dans le cas des recouvrements, la ressource diffusée est un regroupement des ressources et propriétés récupérées, en fonction des chemins de recherche qui peuvent être définis :

* La ressource **Resolver Search Path**, telle qu’elle est définie dans la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) pour **Apache Sling Resource Resolver Factory**.

   * L’ordre décroissant des chemins de recherche indique leurs priorités respectives.
   * Dans une installation standard, les principales valeurs par défaut sont les suivantes : `/apps`, `/libs`. Par conséquent, le contenu de `/apps` a une priorité supérieure à celui de `/libs` (en d’autres termes, il le *recouvre*).

* Deux utilisateurs du service ont besoin d’un accès JCR:READ à l’emplacement de stockage des scripts. Ces utilisateurs sont : components-search-service (utilisé par les composants de cache et d’accès com.day.cq.wcm.coreto) et sling-scripting (utilisé par org.apache.sling.servlets.resolver pour rechercher des servlets).
* La configuration suivante doit également être définie en fonction de l’emplacement de stockage des scripts (dans cet exemple sous /etc, /libs ou /apps).

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* Enfin, le résolveur de servlet doit également être configuré (dans cet exemple, pour ajouter également /etc).

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## Exemple d’utilisation {#example-of-usage}

Voici quelques exemples présentés dans les cas suivants :

* [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Personnalisation de la création de pages](/help/sites-developing/customizing-page-authoring-touch.md)
