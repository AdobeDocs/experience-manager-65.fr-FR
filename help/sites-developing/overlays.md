---
title: Recouvrements
seo-title: Overlays
description: AEM applique le principe des recouvrements pour vous permettre d’étendre et de personnaliser les consoles et d’autres fonctionnalités.
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 66%

---

# Recouvrements{#overlays}

AEM (et, avant cela, CQ) applique depuis longtemps déjà le principe des incrustations pour vous permettre d’étendre et de personnaliser les [consoles](/help/sites-developing/customizing-consoles-touch.md) et d’autres fonctionnalités (la [création de pages](/help/sites-developing/customizing-page-authoring-touch.md), par exemple).

Recouvrement est un terme qui peut être utilisé dans de nombreux contextes. Dans ce contexte, l’incrustation désigne l’utilisation de la fonctionnalité prédéfinie et l’application de vos propres définitions par-dessus (afin de personnaliser la fonctionnalité standard).

Dans une instance standard, la fonctionnalité prédéfinie est conservée sous `/libs` et il est recommandé de définir votre recouvrement (vos personnalisations) sous le `/apps` branche. AEM utilise un chemin de recherche pour trouver une ressource, en recherchant d’abord la variable `/apps` puis la branche `/libs` (la branche [le chemin de recherche peut être configuré.](#configuring-the-search-paths)). Ce mécanisme signifie que votre incrustation (et les personnalisations qui y sont définies) est prioritaire.

Depuis AEM 6.0, des modifications ont été effectuées sur le plan de la mise en œuvre et de l’utilisation des incrustations :

* AEM 6.0 et versions ultérieures : pour les incrustations liées à [Granite](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) (interface utilisateur tactile)

   * Méthode

      * Recréez la structure `/libs` appropriée sous `/apps`.

         Cela ne nécessite aucune copie 1:1 ; [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) est utilisé pour effectuer des références croisées avec les définitions d’origine qui sont requises. Sling Resource Merger propose des services pour accéder à des ressources et les fusionner par le biais de mécanismes de différenciation (diff).

      * Le cas échéant, effectuez des modifications sous `/apps`.
   * Avantages

      * Plus résistant aux modifications sous `/libs`.
      * Vous ne devez redéfinir que ce qui est réellement nécessaire.


* Incrustations non Granite et incrustations antérieures à AEM 6.0

   * Méthode

      * Copiez le contenu depuis `/libs` to `/apps`

         Vous devez copier la sous-branche entière, y compris les propriétés.

      * Le cas échéant, effectuez des modifications sous `/apps`.
   * Inconvénients

      * Bien que vos modifications ne seront pas perdues lorsque quelque chose change sous `/libs`, vous devrez peut-être recréer certaines modifications qui se produisent dans votre incrustation sous `/apps`.


>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) et les méthodes connexes ne peuvent être utilisées qu’avec [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Cela signifie que la création d’un recouvrement avec une ossature n’est appropriée que pour l’interface utilisateur (IU) tactile standard.
>
>Les incrustations relatives à d’autres zones (y compris l’IU classique) impliquent la copie du nœud approprié et de toute la sous-structure, apportant ainsi les modifications nécessaires.

Il est conseillé de recourir aux incrustations pour de nombreuses modifications ; par exemple, pour [configurer vos consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [créer votre catégorie de sélection dans l’explorateur de ressources dans le panneau latéral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (utilisé lors de la création de pages). Elles sont requises pour les raisons suivantes :

* You ***must not* apportez des modifications dans le `/libs` branche **Toute modification que vous apportez peut être perdue, car cette branche est sujette à des modifications lorsque vous :

   * mettez à niveau votre instance ;
   * appliquez un correctif logiciel ;
   * installez un Feature Pack.

* Elles centralisent vos modifications dans un seul emplacement ; cela facilite le suivi, la migration, la sauvegarde et/ou le débogage de vos modifications, suivant les besoins.

## Configuration des chemins de recherche {#configuring-the-search-paths}

Dans le cas des incrustations, la ressource diffusée est un regroupement des ressources et propriétés récupérées, en fonction des chemins de recherche qui peuvent être définis :

* La ressource **Resolver Search Path**, telle qu’elle est définie dans la [configuration OSGi ](/help/sites-deploying/configuring-osgi.md) pour **Apache Sling Resource Resolver Factory**.

   * L’ordre des chemins de recherche de haut en bas indique leurs priorités respectives.
   * Dans une installation standard, les Principaux paramètres par défaut sont les suivants : `/apps`, `/libs` - pour que le contenu de `/apps` a une priorité plus élevée que celle de `/libs` (c.-à-d. *superpositions* it).

* Deux utilisateurs du service ont besoin d’un accès JCR:READ à l’emplacement de stockage des scripts. Ces utilisateurs sont les suivants : components-search-service (utilisé par les com.day.cq.wcm.core access/cache components) et sling-scripting (utilisé par org.apache.sling.servlets.resolver pour rechercher des servlets).
* La configuration suivante doit également être configurée en fonction de l’emplacement où vous placez vos scripts (dans cet exemple sous /etc, /libs ou /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Enfin, le résolveur de servlet doit également être configuré (dans cet exemple pour ajouter /etc également).

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Exemple d’utilisation {#example-of-usage}

Quelques exemples sont donnés pour les scénarios suivants :

* [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Personnalisation de la création de pages](/help/sites-developing/customizing-page-authoring-touch.md)
