---
title: Composant de page SPA
description: Dans une SPA, le composant de page ne fournit pas les éléments HTML de ses composants enfants, mais à la place délègue cette tâche au framework SPA. Ce document explique comment cela rend le composant de page SPA unique.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 91%

---

# Composant de page SPA{#spa-page-component}

Dans une SPA, le composant de page ne fournit pas les éléments HTML de ses composants enfants, mais à la place délègue cette tâche au framework SPA. Ce document explique comment cela rend le composant de page SPA unique.

>[!NOTE]
>
>L’éditeur SPA est la solution recommandée pour les projets qui nécessitent SPA rendu côté client basé sur une structure (par exemple, React ou Angular).

## Présentation {#introduction}

Le composant de page d’une application sur une seule page (SPA) ne fournit pas les composants HTML de ses composants enfants via un fichier HTL ou JSP et des objets de ressource. Cette opération est déléguée à la structure SPA. La représentation des composants enfants est récupérée en tant que structure de données JSON (à savoir le modèle). Les composants SPA sont ensuite ajoutés à la page conformément au modèle JSON fourni. En tant que telle, la composition initiale du corps du composant de page diffère de celle du code HTML prérendu.

## Gestion du modèle de page {#page-model-management}

La résolution et la gestion du modèle de page sont déléguées à un module [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) fourni. La SPA doit interagir avec le module `PageModelManager` lorsqu’il s’initialise pour récupérer le modèle de page initial et s’enregistrer pour les mises à jour du modèle – générées principalement lorsque l’auteur modifie la page via l’éditeur de page. Le module `PageModelManager` est accessible par projet SPA sous la forme d’un package npm. En tant qu’interprète entre AEM et la SPA, `PageModelManager` est destiné à accompagner la SPA.

Pour autoriser la création de la page, une bibliothèque client nommée `cq.authoring.pagemodel.messaging` doit être ajoutée pour fournir un canal de communication entre la SPA et l’éditeur de page. Si le composant de page SPA hérite du composant wcm/core de page, les options suivantes sont fournies pour rendre la catégorie de bibliothèque client `cq.authoring.pagemodel.messaging` disponible :

* Si le modèle est modifiable, ajoutez la catégorie de bibliothèque client à la politique de page.
* Ajoutez la catégorie de bibliothèque client à l’aide du fichier `customfooterlibs.html` du composant de page.

N’oubliez pas de limiter l’inclusion de la catégorie `cq.authoring.pagemodel.messaging` au contexte de l’éditeur de page.

## Type de données de communication {#communication-data-type}

Le type de données de communication est défini sur un élément HTML dans le composant de page AEM à l’aide de l’attribut `data-cq-datatype`. Lorsque le type de données de communication est défini sur JSON, les requêtes GET atteignent les points d’entrée du modèle Sling d’un composant. À la suite d’une mise à jour dans l’éditeur de page, la représentation JSON du composant mis à jour est envoyée à la bibliothèque modèle de page. Celle-ci informe ensuite l’application sur une seule page des mises à jour.

**Composant de page SPA –`body.html`**

```
<div id="page"></div>
```

En plus de constituer une bonne pratique pour ne pas retarder la génération du modèle DOM, le framework SPA exige que les scripts soient ajoutés à la fin du corps.

**Composant de page SPA –`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Propriétés des ressources de métadonnées qui décrivent le contenu SPA :

**Composant de page SPA –`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>Le sélecteur de modèle par défaut est défini de manière statique lors de la demande de la représentation de modèle Sling d’un composant.

## Propriétés des métadonnées {#meta-properties}

* `cq:wcmmode` : mode WCM des éditeurs (par exemple, page, modèle)
* `cq:pagemodel_root_url` : URL du modèle racine de l’application. Crucial lors de l’accès direct à une page enfant, car le modèle de page enfant est un fragment du modèle racine de l’application. Le module ` [PageModelManager](/help/sites-developing/spa-page-component.md)` recompose ensuite de manière systématique le modèle initial de l’application en accédant à l’application à partir de son point d’entrée racine.

* `cq:pagemodel_router` : activation ou désactivation du module ` [ModelRouter](/help/sites-developing/spa-routing.md)` de la bibliothèque `PageModelManager`

* `cq:pagemodel_route_filters` : liste séparée par des virgules ou expressions régulières fournissant des routes que ` [ModelRouter](/help/sites-developing/spa-routing.md)` doit ignorer.

>[!CAUTION]
>
>Ce document utilise l’application We.Retail Journal à des fins de démonstration uniquement. N’utilisez pas pour le travail d’un projet.
>
>Tout projet AEM doit utiliser la variable [AEM Archétype de projet](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr), qui prend en charge SPA projets à l’aide de React ou d’Angular et qui utilise le SDK SPA. Tous les projets de SPA sur doivent être basés sur Maven Archetype for Starter Kit.

## Synchronisation des recouvrements de l’éditeur de page {#page-editor-overlay-synchronization}

La synchronisation des recouvrements est assurée par le même observateur de mutation que celui fourni par la catégorie `cq.authoring.page`.

## Configuration de la structure exportée JSON du modèle Sling {#sling-model-json-exported-structure-configuration}

Lorsque les fonctionnalités de routage sont activées, on part du principe que l’exportation JSON de l’application sur une seule page contient les différentes routes de l’application grâce à l’exportation JSON du composant de navigation AEM. La sortie JSON du composant de navigation AEM peut être configurée dans la politique de contenu de page racine de l’application sur une seule page au moyen des deux propriétés suivantes :

* `structureDepth` : nombre correspondant à la profondeur de l’arborescence exportée
* `structurePatterns` : regex ou tableau de regex correspondant à la page à exporter

Elle peut être affichée dans l’exemple de contenu de SPA dans `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
